# GDPRArt5SecuritySpec.md — ТЗ для GDPR Art.5 и Login & Security

**Версия:** 1.4 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик, DevOps  
**Статус:** 🔴 Часть блокирует публикацию · 🟡 Часть — требования для предотвращения штрафов (€20 млн / 4% оборота)

> **Смежные документы:**  
> [AccountDeletionSpec.md](AccountDeletionSpec.md) — удаление аккаунта  
> [AccessibilitySpec.md](AccessibilitySpec.md) — кнопка Contact DPO  
> [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md) — GDPR Art.25 / Art.17 аудит

---

## Содержание

1. [3️⃣ Login & Security — Полная спецификация раздела](#login--security)  
   1.1 [Change Password](#31-change-password)  
   1.2 [Two-Factor Authentication (2FA)](#32-two-factor-authentication-2fa)  
   1.3 [Third-Party Login (Sign in with Apple / Google / Facebook)](#33-third-party-login)  
   1.4 [Active Sessions](#34-active-sessions)  
   1.5 [Login History](#35-login-history)  
   1.6 [Блокеры публикации для Login & Security](#36-блокеры-публикации)
2. [GDPR Art.5(1)(f) — Безопасность: HTTPS, шифрование](#2-gdpr-art51f--https-и-шифрование)
3. [GDPR Art.5(2) — Подотчётность](#3-gdpr-art52--подотчётность)
4. [Consent History — История согласий](#4-consent-history--история-согласий)
5. [Audit Log — Журнал аудита (внутренний)](#5-audit-log--журнал-аудита)
6. [DPO Contact — Контакт ответственного за данные](#6-dpo-contact)
7. [Полная структура Settings → Login & Security](#7-полная-структура-экрана)
8. [Чеклист для разработчика](#8-чеклист-для-разработчика)

---

## Login & Security

**Путь в приложении:** Settings → Login & Security  
**Правовое основание:** ⚖️ GDPR Art.5(1)(f) · App Store §5.1.1(v) · Google Play Policy  
**Статус:** 🔴 Часть является блокером публикации

> **Контекст регистрации Bestme:**  
> Пользователь может зарегистрироваться четырьмя способами:
> 1. **Email + пароль** (собственная система)  
> 2. **Sign in with Google**  
> 3. **Sign in with Apple**  
> 4. **Sign in with Facebook**  
>
> При регистрации через собственную систему: **телефон не собирается**.  
> Поэтому 2FA = **Email OTP** (первичный) + **TOTP-приложение** (опционально).  
> **SMS 2FA** предлагается только если пользователь добавил телефон в профиль позже.

---

### 3.1 Change Password

**Путь:** Settings → Login & Security → Change Password  
**Применимость:** Только для аккаунтов, зарегистрированных через email + пароль  
(Для пользователей, вошедших только через Google/Apple/Facebook — этот пункт скрыт или неактивен)

**Статус публикации:** ✅ Не блокер (но требуется для любого аккаунта с паролем)

**UX-поток:**
```
Settings → Login & Security
  Пароль: ••••••••••           [Изменить →]

→ Экран "Change Password"

  Current Password:   [___________________]  👁
  New Password:       [___________________]  👁
  Confirm Password:   [___________________]  👁

  Требования к паролю:
  • Минимум 8 символов
  • Хотя бы 1 заглавная буква
  • Хотя бы 1 цифра или спецсимвол

                              [Save New Password]
```

**Backend требования:**

| Параметр | Значение |
|---|---|
| **Подтверждение текущего пароля** | Обязательно перед сменой |
| **Хеширование** | bcrypt cost ≥ 12 или Argon2id |
| **Запрет повтора** | Последние 3 пароля нельзя использовать повторно |
| **После смены** | Инвалидировать все сессии кроме текущей (GDPR Art.5(1)(f)) |
| **Rate limit** | Не более 5 попыток смены за 15 минут |
| **Уведомление** | Email: «Ваш пароль был изменён» (с IP + время + кнопка «Не я — заблокировать») |
| **Audit Log** | Записать `password_changed` с IP и User-Agent |

> 💡 Если пользователь забыл текущий пароль → кнопка «Forgot password?» на экране → стандартный reset-flow по email.

#### Реализация с Supabase + React Native

> **Стек:** Supabase Auth · React Native · Supabase Edge Functions · PostgreSQL (custom tables)

**Почему нельзя просто вызвать `supabase.auth.updateUser({ password })`:**  
Supabase не проверяет текущий пароль перед сменой — `updateUser` меняет пароль сразу для уже аутентифицированного пользователя. Это значит, что если кто-то завладел активной сессией, он может сменить пароль без знания старого. **Нужна явная повторная аутентификация.**

##### Шаг 1 — Повторная аутентификация (проверка текущего пароля)

```typescript
// React Native (client)
// Перед сменой пароля проверяем текущий пароль через повторный вход
const verifyCurrentPassword = async (email: string, currentPassword: string) => {
  const { error } = await supabase.auth.signInWithPassword({
    email,
    password: currentPassword,
  });
  if (error) throw new Error('Неверный текущий пароль');
  // Пользователь подтверждён — можно менять пароль
};
```

> ⚠️ Supabase применяет встроенный rate limit к `signInWithPassword` (защита от brute force). Дополнительный rate limit на Edge Function нужен для логирования попыток и блокировки на уровне приложения.

##### Шаг 2 — Смена пароля через Edge Function (с проверкой истории)

Менять пароль напрямую через `supabase.auth.updateUser` на клиенте **нельзя** — нет возможности проверить историю паролей и инвалидировать другие сессии. Используем Edge Function:

```typescript
// Edge Function: supabase/functions/change-password/index.ts
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'
import * as bcrypt from 'https://deno.land/x/bcrypt/mod.ts'

Deno.serve(async (req) => {
  const { newPassword } = await req.json()
  const authHeader = req.headers.get('Authorization')!
  
  // Клиентский Supabase для получения user_id из токена
  const supabase = createClient(
    Deno.env.get('SUPABASE_URL')!,
    Deno.env.get('SUPABASE_ANON_KEY')!,
    { global: { headers: { Authorization: authHeader } } }
  )
  const { data: { user } } = await supabase.auth.getUser()
  if (!user) return new Response('Unauthorized', { status: 401 })

  // Admin-клиент для привилегированных операций
  const adminSupabase = createClient(
    Deno.env.get('SUPABASE_URL')!,
    Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')!
  )

  // 1. Проверка истории паролей (последние 3)
  const { data: history } = await adminSupabase
    .from('password_history')
    .select('password_hash')
    .eq('user_id', user.id)
    .order('created_at', { ascending: false })
    .limit(3)

  for (const entry of history ?? []) {
    if (await bcrypt.compare(newPassword, entry.password_hash)) {
      return new Response(
        JSON.stringify({ error: 'Этот пароль уже использовался. Выберите другой.' }),
        { status: 400 }
      )
    }
  }

  // 2. Смена пароля через Admin API
  const { error } = await adminSupabase.auth.admin.updateUserById(user.id, {
    password: newPassword,
  })
  if (error) return new Response(JSON.stringify({ error: error.message }), { status: 500 })

  // 3. Сохраняем новый пароль в историю (bcrypt hash)
  const newHash = await bcrypt.hash(newPassword)
  await adminSupabase.from('password_history').insert({
    user_id: user.id,
    password_hash: newHash,
  })

  // 4. Инвалидируем ВСЕ другие сессии (оставляем только текущую)
  // Supabase не поддерживает "logout всех кроме текущей" нативно.
  // Решение: обновляем поле force_relogin_at — при следующем refresh_token
  // middleware проверяет это поле и отклоняет старые токены.
  await adminSupabase
    .from('user_security_settings')
    .upsert({ user_id: user.id, force_relogin_at: new Date().toISOString() })

  // 5. Audit log
  const ip = req.headers.get('x-forwarded-for') ?? 'unknown'
  const ua = req.headers.get('user-agent') ?? 'unknown'
  await adminSupabase.from('audit_log').insert({
    user_id: user.id,
    event: 'password_changed',
    ip_address: ip,
    user_agent: ua,
  })

  // 6. Email-уведомление (через Supabase custom SMTP или Resend/SendGrid)
  // Вызываем отдельную Edge Function или Supabase Email Hook
  await fetch(`${Deno.env.get('SUPABASE_URL')}/functions/v1/send-security-email`, {
    method: 'POST',
    headers: { Authorization: `Bearer ${Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')}` },
    body: JSON.stringify({
      to: user.email,
      template: 'password_changed',
      data: { ip, time: new Date().toISOString() },
    }),
  })

  return new Response(JSON.stringify({ success: true }), { status: 200 })
})
```

##### Шаг 3 — Вызов из React Native

```typescript
// React Native (client)
const changePassword = async (currentPassword: string, newPassword: string) => {
  const { data: { user } } = await supabase.auth.getUser()
  if (!user?.email) throw new Error('Нет email')

  // 1. Сначала повторная аутентификация (проверка текущего пароля)
  await verifyCurrentPassword(user.email, currentPassword)

  // 2. Вызов Edge Function для смены с историей и инвалидацией сессий
  const { data: { session } } = await supabase.auth.getSession()
  const response = await fetch(
    `${SUPABASE_URL}/functions/v1/change-password`,
    {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${session?.access_token}`,
      },
      body: JSON.stringify({ newPassword }),
    }
  )

  if (!response.ok) {
    const err = await response.json()
    throw new Error(err.error ?? 'Ошибка смены пароля')
  }

  // 3. После успеха — пользователь остаётся в системе (текущая сессия активна)
  // Supabase выдаёт новый токен автоматически через refreshSession
}
```

##### Схема базы данных (дополнительные таблицы)

```sql
-- Хранение истории паролей (последние N хэшей)
CREATE TABLE password_history (
  id           UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id      UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  password_hash TEXT NOT NULL,
  created_at   TIMESTAMPTZ DEFAULT NOW()
);

-- RLS: только service_role может читать/писать
ALTER TABLE password_history ENABLE ROW LEVEL SECURITY;
CREATE POLICY "service_only" ON password_history USING (false); -- блокируем клиентский доступ

-- Таблица для инвалидации сессий
CREATE TABLE user_security_settings (
  user_id         UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  force_relogin_at TIMESTAMPTZ,   -- при смене пароля обновляется; старые токены отклоняются
  updated_at      TIMESTAMPTZ DEFAULT NOW()
);
ALTER TABLE user_security_settings ENABLE ROW LEVEL SECURITY;
CREATE POLICY "user_own" ON user_security_settings USING (auth.uid() = user_id);
```

> ℹ️ **Инвалидация сессий:** Supabase Admin API (`signOut(userId, 'global')`) завершает **все** сессии включая текущую. Для «завершить все кроме текущей» используется подход с `force_relogin_at`: при каждом обновлении токена middleware (или Supabase Auth Hook `custom_access_token`) сравнивает время выдачи токена с `force_relogin_at`. Если токен выдан **до** этого времени — он считается невалидным.

##### Rate limit (5 попыток за 15 минут)

Supabase имеет встроенные rate limits для Auth-эндпоинтов (настраиваются в Dashboard → Auth → Rate Limits). Дополнительно реализуем прикладной rate limit в Edge Function:

```sql
-- Таблица для rate limiting попыток смены пароля
CREATE TABLE rate_limit_log (
  id         UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id    UUID NOT NULL,
  action     TEXT NOT NULL,          -- 'change_password', 'login', etc.
  created_at TIMESTAMPTZ DEFAULT NOW()
);
CREATE INDEX ON rate_limit_log (user_id, action, created_at);
```

```typescript
// В Edge Function — проверка перед сменой пароля
const fifteenMinAgo = new Date(Date.now() - 15 * 60 * 1000).toISOString()
const { count } = await adminSupabase
  .from('rate_limit_log')
  .select('*', { count: 'exact', head: true })
  .eq('user_id', user.id)
  .eq('action', 'change_password')
  .gte('created_at', fifteenMinAgo)

if ((count ?? 0) >= 5) {
  return new Response(
    JSON.stringify({ error: 'Слишком много попыток. Подождите 15 минут.' }),
    { status: 429 }
  )
}
await adminSupabase.from('rate_limit_log').insert({
  user_id: user.id, action: 'change_password'
})
```

---

#### Специальный случай: OAuth-пользователь хочет установить пароль

> **Вопрос:** Пользователь вошёл через Google/Apple/Facebook — у него нет пароля. Может ли он установить пароль для своего аккаунта?

**Ответ: Да. Supabase это поддерживает. Это юридически корректно и рекомендуется.**

**Как это работает технически:**
```typescript
// Пользователь, вошедший через OAuth, устанавливает пароль впервые
// Для него нет "текущего пароля" — не нужна re-auth
const setInitialPassword = async (newPassword: string) => {
  const { error } = await supabase.auth.updateUser({ password: newPassword })
  if (error) throw error
  // После этого пользователь может входить и через OAuth, и через email+пароль
}
```

> ⚠️ Supabase требует, чтобы у OAuth-пользователя был верифицированный email для установки пароля. Если email не верифицирован — сначала отправить подтверждение.

**UX в приложении:**
```
Settings → Login & Security

  Способы входа:
  🟢 Google (подключено)
  🟢 Apple (подключено)
  🔘 Email + Пароль: не установлен    [Установить пароль →]

→ Экран "Установить пароль"
  (здесь нет поля "Текущий пароль" — его нет)

  Новый пароль:        [___________________]  👁
  Подтвердить пароль:  [___________________]  👁

  Требования к паролю:
  • Минимум 8 символов
  • Хотя бы 1 заглавная буква
  • Хотя бы 1 цифра или спецсимвол

                            [Сохранить пароль]

→ После установки: email-уведомление «К вашему аккаунту добавлен вход по паролю»
→ Секция меняется на: Пароль: ••••••••••  [Изменить →]
```

**По закону:** Добавление пароля к OAuth-аккаунту — это расширение способов входа. Никаких специальных правовых ограничений нет. Это стандартная практика (как в GitHub, Notion и др.). Обязательно:
1. Отправить email-уведомление «К аккаунту добавлен вход по паролю» (защита от несанкционированных действий)
2. Записать в Audit Log: `password_set_for_oauth_account`

**Разграничение в секции Change Password:**

| Тип аккаунта | Что видит в Settings → Login & Security |
|---|---|
| Email + пароль (регистрация через email) | `Пароль: ••••••••  [Изменить →]` |
| OAuth-only (никогда не устанавливал пароль) | `Пароль: не установлен  [Установить →]` |
| OAuth + установил пароль позже | `Пароль: ••••••••  [Изменить →]` |
| Логика | `has_password` проверяется через Supabase: `user.identities` содержит identity с `provider = 'email'` |

```typescript
// React Native: как определить, есть ли у пользователя пароль
const hasEmailPassword = (user: User): boolean => {
  return user.identities?.some(i => i.provider === 'email') ?? false
}
```

---

#### Сводная таблица: что реализуется где

| Требование | Где реализуется | Инструмент Supabase |
|---|---|---|
| Проверка текущего пароля | Клиент (React Native) | `supabase.auth.signInWithPassword` |
| Смена пароля | Edge Function | `auth.admin.updateUserById` |
| Проверка истории паролей | Edge Function + DB | Таблица `password_history` + bcrypt |
| Инвалидация других сессий | Edge Function + DB | Таблица `user_security_settings.force_relogin_at` |
| Rate limit 5/15мин | Edge Function + DB | Таблица `rate_limit_log` |
| Email-уведомление «пароль изменён» | Edge Function | Custom SMTP / Resend / SendGrid |
| Audit log `password_changed` | Edge Function | Таблица `audit_log` |
| OAuth-пользователь устанавливает пароль | Клиент + Edge Function | `supabase.auth.updateUser({ password })` |

---

### 3.2 Two-Factor Authentication (2FA)

**Путь:** Settings → Login & Security → Two-Factor Authentication  
**Применимость:** Только для аккаунтов с паролем (email + пароль).  
Для OAuth-пользователей (Google/Apple/FB) — 2FA управляется на стороне провайдера; в приложении Bestme не отображается.

**Статус публикации:** 🟡 Не блокер для MVP, рекомендуется в Sprint 2

**Какие методы 2FA поддерживаются:**

| Метод | Когда доступен | Приоритет |
|---|---|---|
| **Email OTP** (6-значный код на email) | Всегда (email есть у всех) | ✅ Первичный метод |
| **TOTP App** (Google Authenticator, Authy) | Всегда | ✅ Опциональный |
| **SMS OTP** | Только если пользователь добавил телефон в профиль | 🟡 Дополнительный |

> ⚠️ **SMS 2FA НЕ запрашивается при регистрации** — телефон не собирается. SMS-опция появляется в настройках 2FA только если пользователь добавил телефон в §1 Account Info.

**UX-поток включения 2FA:**
```
Settings → Login & Security → Two-Factor Authentication

  Двухфакторная аутентификация         [OFF → Включить]

→ Нажать [Включить]

→ Экран "Choose 2FA Method"
   ○ Email Code  — код придёт на user@example.com
   ○ Authenticator App — Google Authenticator, Authy
   ○ SMS Code (если телефон добавлен) — ••• ••• 99

→ Выбрать "Email Code"
   → Отправить код на email → ввести 6 цифр → [Подтвердить]
   → ✅ 2FA включена

→ Выбрать "Authenticator App"
   → Показать QR-код и TOTP secret
   → «Откройте Google Authenticator / Authy и отсканируйте QR-код»
   → Введите 6-значный код из приложения: [______]  [Подтвердить]
   → ✅ 2FA включена

→ После успешного включения:
   «Сохраните резервные коды. Они помогут войти, если вы потеряете доступ к методу 2FA.»
   [Показать 10 резервных кодов]  [Скопировать]  [Скачать]
```

**UX-поток входа с 2FA (email + пароль):**
```
Пользователь вводит email + пароль → [Войти]
→ Backend: credentials верны + two_factor_enabled=true
→ Показать экран "Подтверждение личности"
   "Введите 6-значный код из вашего приложения-аутентификатора"
   [  ][ ][ ] - [ ][ ][ ]
   [Подтвердить]    [Использовать резервный код]
→ Код верен → выдать access_token → войти
→ Код неверен → «Неверный код. Осталось попыток: N»
```

**Backend требования:**

| Параметр | Значение |
|---|---|
| **variable_name** | `two_factor_enabled` |
| **Тип** | Boolean |
| **Default** | `false` — включается добровольно |
| **TOTP-стандарт** | RFC 6238, 6 цифр, 30-секундное окно, HMAC-SHA1 |
| **TOTP secret** | Хранить зашифрованным (AES-256), не в открытом виде |
| **Email OTP срок** | 10 минут |
| **Rate limit** | Не более 5 попыток ввода кода за 15 минут → временная блокировка |
| **Backup codes** | 10 одноразовых кодов, показать один раз, хранить как bcrypt-хэши |
| **Аудит** | `2fa_enabled`, `2fa_disabled`, `2fa_method_changed` |

**Почему 2FA рекомендуется, даже если не обязательна (GDPR Art.5(1)(f)):**  
При утечке данных регулятор спросит «какие меры безопасности были приняты?». Наличие опциональной 2FA — весомый аргумент, что меры были «надлежащими». Отсутствие 2FA само по себе не нарушение, но при инциденте без 2FA риск штрафа значительно возрастает.

---

### 3.3 Third-Party Login

**Путь:** Settings → Login & Security → Sign in with / Linked Accounts  
**Применимость:** Все пользователи

**Статус публикации:** 🔴 **ДВА БЛОКЕРА** — оба обязательны для App Store

> 🔴 **БЛОКЕР 1 — App Store §5.1.3 (Sign in with Apple — обязателен):**  
> Если приложение предлагает вход через **любой** сторонний провайдер (Google, Facebook и т.д.), оно **ОБЯЗАНО** также предлагать **Sign in with Apple**. Bestme предлагает Google + Facebook → **Sign in with Apple обязателен**. Отсутствие Sign in with Apple = **автоматический отказ в публикации**.

> 🔴 **БЛОКЕР 2 — App Store §5.1.1(v) (кнопка Disconnect):**  
> Если пользователь вошёл через Sign in with Apple (или другой OAuth-провайдер), он **обязан иметь возможность отключить** эту связь прямо в приложении. Отсутствие кнопки Disconnect = **отказ в публикации**.

**Варианты состояния аккаунта:**

| Тип регистрации | Что показывается |
|---|---|
| Зарегистрирован через email | Google/Apple/Facebook = [Подключить] |
| Зарегистрирован через Google | Google = [Подключено — Отключить]; Apple/Facebook = [Подключить] |
| Зарегистрирован через Apple | Apple = [Подключено — Отключить]; Google/Facebook = [Подключить] |
| Несколько способов добавлено | Каждый со своим статусом |

**UX-экран:**
```
Settings → Login & Security

─── Связанные аккаунты (Linked Accounts) ──────────────

  🍎 Apple           [Подключено]    [Отключить]
  🔵 Google          [Подключить]
  🔷 Facebook        [Подключить]

─────────────────────────────────────────────────────

  ⚠️ Прежде чем отключить последний способ входа,
     убедитесь, что у вас установлен пароль.
```

**Логика кнопки Disconnect:**
1. Если у пользователя **только один** способ входа → нельзя отключить без установки пароля:
   ```
   «Сначала установите пароль, затем можно отключить Apple.»
   [Установить пароль]
   ```
2. Если у пользователя **несколько** способов входа → отключение разрешено сразу.
3. После отключения: удалить `provider_id` из таблицы `auth_providers`.

**UX-поток подключения нового провайдера:**
```
Пользователь нажимает [Подключить] рядом с Google
→ OAuth-редирект на Google
→ Успешно → «Google-аккаунт подключён» → кнопка меняется на [Подключено | Отключить]
→ Audit Log: `oauth_provider_connected` (provider=google)
```

**Backend требования:**

```sql
CREATE TABLE auth_providers (
  id           UUID PRIMARY KEY,
  user_id      UUID NOT NULL REFERENCES users(id),
  provider     TEXT NOT NULL,   -- 'google' | 'apple' | 'facebook' | 'email'
  provider_id  TEXT NOT NULL,   -- внешний ID от провайдера
  email        TEXT,            -- email от провайдера (может отличаться)
  connected_at TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE (provider, provider_id)
);
```

| Требование | Детали |
|---|---|
| **Sign in with Apple** | Использовать Apple's «Hide My Email» если пользователь выбрал | обязательно хранить `apple_user_id`, не email |
| **Sign in with Google** | Google Sign-In SDK (iOS/Android), PKCE для веба |
| **Sign in with Facebook** | Facebook Login SDK |
| **Revoke токен при Disconnect** | При отключении провайдера — вызвать API провайдера для отзыва токена |
| **Защита от orphan-аккаунта** | Не разрешать удаление последнего `auth_provider`, если пароль не установлен |
| **Аудит** | `oauth_provider_connected`, `oauth_provider_disconnected` |

---

### 3.4 Active Sessions

**Путь:** Settings → Login & Security → Active Sessions  
**Применимость:** Все пользователи  
**Статус публикации:** 🟡 Рекомендуется; не является строгим блокером, но GDPR Art.5(1)(f) требует механизм отзыва доступа

**UX-экран:**
```
📱 ACTIVE SESSIONS

✅ Текущее устройство
   iPhone 14 Pro · iOS 17.2
   Москва, Россия · 19 марта 2026, 14:23

📱 iPhone 12 Mini
   Последняя активность: 28 февраля 2026
   Берлин, Германия
   [Завершить сессию]

💻 MacBook Pro (Chrome 122)
   Последняя активность: 10 марта 2026
   Тель-Авив, Израиль
   [Завершить сессию]

━━━━━━━━━━━━━━━━━━━━━━━━
[Завершить все другие сессии]
```

**Backend требования:**

| Параметр | Значение |
|---|---|
| **Таблица** | `sessions`: user_id, device_name, device_type, ip_address, last_active_at, created_at, is_current |
| **Access token** | JWT, срок действия 15 минут |
| **Refresh token** | Secure HTTP-only cookie или Keychain/Keystore, срок 30 дней |
| **Автоистечение** | Refresh token истекает через 30 дней неактивности |
| **При смене пароля** | Инвалидировать ВСЕ сессии кроме текущей |
| **При завершении сессии** | Удалить refresh_token, запись в `sessions` |
| **Аудит** | `session_created`, `session_terminated` (с IP, User-Agent) |

---

### 3.5 Login History

**Путь:** Settings → Login & Security → Login History  
**Применимость:** Все пользователи  
**Статус публикации:** 🟡 Рекомендуется для пользователей; GDPR Art.5(1)(f) требует логирование (во внутренний Audit Log — обязательно)

> 💡 **Разница между Login History и Active Sessions:**  
> - **Active Sessions** = устройства, на которых сейчас выполнен вход (можно завершить)  
> - **Login History** = исторический журнал всех входов/выходов (только просмотр)

**UX-экран:**
```
🕐 ИСТОРИЯ ВХОДОВ

Март 2026

  ✅ Вход выполнен
     iPhone 14 Pro · iOS 17.2
     Москва, Россия · 19 марта 2026, 14:23

  ⚠️ Неудачная попытка входа
     Неизвестное устройство
     Киев, Украина · 15 марта 2026, 03:11
     [Это не я → Защитить аккаунт]

  ✅ Вход выполнен
     MacBook Pro (Chrome 122)
     Тель-Авив, Израиль · 10 марта 2026, 11:44

Февраль 2026

  ✅ Вход выполнен через Google
     iPhone 12 Mini · iOS 16.5
     Берлин, Германия · 28 февраля 2026, 09:05

  🔒 Выход (пользователь завершил сессию)
     MacBook Pro · 25 февраля 2026, 18:30

─────────────────────────────────
Показываются записи за последние 90 дней.
```

**Backend требования:**

| Параметр | Значение |
|---|---|
| **Хранение** | 90 дней (отображаются пользователю); Audit Log хранится 3 года (внутренний) |
| **Что логировать** | IP, User-Agent, тип входа (email / Google / Apple / Facebook / 2FA), статус (успех / неудача), геолокация (страна/город по IP) |
| **Геолокация** | IP → страна/город (MaxMind GeoIP или аналог); хранить только страну+город, не точные координаты |
| **Endpoint** | `GET /api/user/login-history?page=1&limit=20` |
| **«Это не я»** | Кнопка на подозрительном входе → смена пароля + инвалидация всех сессий + оповещение по email |
| **Аудит** | Часть Audit Log (см. §5) |

---

### 3.6 Блокеры публикации

**Что ОБЯЗАТЕЛЬНО для App Store / Google Play:**

| # | Что | Где | Закон / Правило | Статус |
|---|---|---|---|---|
| 1 | **Sign in with Apple** обязателен, если есть Google или Facebook login | §3.3 Third-Party Login | **App Store §5.1.3** | 🔴 **БЛОКЕР** |
| 2 | **Кнопка Disconnect** для каждого подключённого OAuth-провайдера | §3.3 Third-Party Login | **App Store §5.1.1(v)** | 🔴 **БЛОКЕР** |
| 3 | **In-app путь удаления аккаунта** | AccountDeletionSpec.md | App Store §5.1.1(v) · Google Play | 🔴 **БЛОКЕР** (документ отдельный) |

**Что РЕКОМЕНДУЕТСЯ (штраф GDPR при нарушении, не блокирует App Store):**

| # | Что | Приоритет |
|---|---|---|
| Change Password | Обязательно для любого email-аккаунта | Sprint 1 |
| Active Sessions | GDPR Art.5(1)(f) — право завершить сессию | Sprint 2 |
| 2FA (Email OTP + TOTP) | GDPR Art.5(1)(f) — «надлежащие меры» | Sprint 2 |
| Login History | Прозрачность; «Это не я» — защита пользователя | Sprint 2 |

---

## 2. GDPR Art.5(1)(f) — HTTPS и шифрование

### Что говорит закон

> «Персональные данные должны обрабатываться с обеспечением надлежащей безопасности, включая защиту от несанкционированной или незаконной обработки, от случайной потери, уничтожения или повреждения, с применением надлежащих технических или организационных мер.»
> — GDPR Art.5(1)(f)

### Что это означает на практике для приложения

Три конкретных механизма: **2FA** (детали — §3.2), **HTTPS**, **управление сессиями** (детали — §3.4).

---

### 2.1 2FA — Двухфакторная авторизация

> 📎 Полная UX/backend спецификация 2FA находится в [§3.2 Two-Factor Authentication](#32-two-factor-authentication-2fa).

**Краткий ответ на ключевые вопросы:**

| Вопрос | Ответ |
|---|---|
| Обязателен ли 2FA по GDPR? | ❌ **Нет** — GDPR не называет 2FA явно. Он требует «надлежащие технические меры» (Art.5(1)(f)). 2FA — одна из таких мер, но не единственная. |
| Нужен ли телефон для 2FA? | ❌ **Нет** — SMS 2FA не предлагается, если телефон не собирается. Стандарт для Bestme: **Email OTP + TOTP App**. SMS — только если пользователь добавил телефон в профиль. |
| Достаточно ли HTTPS + bcrypt без 2FA для публикации? | ✅ **Да** — 2FA рекомендуется в Sprint 2, не блокирует App Store / GDPR MVP. |

---

### 2.2 HTTPS — Шифрование передачи данных

**Что это:**  
Все данные между приложением и сервером передаются только по зашифрованному каналу HTTPS (TLS 1.2+). Никаких HTTP-запросов с персональными данными.

**ТЗ для Backend/DevOps:**

| Требование | Детали |
|---|---|
| **TLS версия** | Минимум TLS 1.2, рекомендуется TLS 1.3 |
| **Сертификат** | Let's Encrypt или коммерческий CA (не self-signed в production) |
| **HSTS** | `Strict-Transport-Security: max-age=31536000; includeSubDomains` |
| **Certificate Pinning** | Рекомендуется для мобильного приложения (iOS: NSURLSession; Android: OkHttp CertificatePinner) |
| **API endpoints** | Все endpoints только HTTPS. HTTP → 301 redirect на HTTPS |
| **WebSockets** | Только `wss://` (не `ws://`) |
| **Шифрование в покое** | БД: шифрование на уровне диска (AWS RDS encryption, PostgreSQL encryption) |
| **Шифрование паролей** | bcrypt, cost factor ≥12 (или Argon2id) |

**ТЗ для мобильного приложения:**
- iOS: `NSAppTransportSecurity` — `NSAllowsArbitraryLoads = false`.
- Android: `network_security_config.xml` — `<domain-config cleartextTrafficPermitted="false">`.
- Никогда не логировать access tokens, пароли, personal data в console/Logcat.

---

### 2.3 Управление сессиями

> 📎 Полная UX/backend спецификация Active Sessions находится в [§3.4 Active Sessions](#34-active-sessions).

**Ключевые требования GDPR:**
- Пользователь должен уметь завершить сессию на любом устройстве (право на отзыв доступа).
- При смене пароля — инвалидировать все сессии кроме текущей.
- Хранить IP и User-Agent для Audit Log.

---

## 3. GDPR Art.5(2) — Подотчётность

### Что говорит закон

> «Контролёр несёт ответственность за соблюдение принципов и должен быть в состоянии продемонстрировать это соответствие.»
> — GDPR Art.5(2)

### Что это означает для продукта

Четыре конкретных элемента: DPO контакт, Privacy Policy, Consent History, Audit Log.

---

## 4. Consent History — История согласий

### Что это

Лог всех согласий, которые пользователь дал в приложении: принятие Terms of Service, Privacy Policy, маркетинговые рассылки, TCPA SMS consent, UGC Terms. Пользователь может посмотреть, что и когда он принял.

### Почему нужно (GDPR Art.5(2) + Art.7(1))

GDPR Art.7(1): «контролёр должен быть в состоянии продемонстрировать, что субъект данных дал согласие». Если регулятор спросит «когда пользователь принял вашу политику?» — вы должны предоставить точный timestamp.

### Где находится в приложении

Settings → Your Data → Consent History

### ТЗ для Consent History

**База данных:**
```sql
CREATE TABLE consent_log (
  id              UUID PRIMARY KEY,
  user_id         UUID NOT NULL,
  consent_type    TEXT NOT NULL,  -- 'terms_of_service' | 'privacy_policy' | 'marketing_email' | 'sms_marketing' | 'ugc_terms' | 'att_tracking'
  consent_version TEXT NOT NULL,  -- '2.1' (версия документа)
  action          TEXT NOT NULL,  -- 'granted' | 'withdrawn'
  ip_address      INET,
  user_agent      TEXT,
  created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

**Что записывать:**

| Событие | consent_type | Когда |
|---|---|---|
| Принятие Terms of Service | `terms_of_service` | При регистрации |
| Принятие Privacy Policy | `privacy_policy` | При регистрации |
| Opt-in маркетинговые email | `marketing_email` | Если чекбокс поставлен |
| Opt-out маркетинговые email | `marketing_email` (action=withdrawn) | Если отписался |
| SMS consent (TCPA) | `sms_marketing` | При добавлении телефона |
| UGC Terms acceptance | `ugc_terms` | При первом контенте |
| ATT (iOS tracking) | `att_tracking` | После ATT диалога |
| Обновление ToS (новая версия) | `terms_of_service` | При принятии новой версии |

**UI для Consent History:**
```
📋 Your Consent History

Showing all permissions and agreements you've made.

✅ Terms of Service (v2.1)
   Accepted on Jan 15, 2026 · 14:23 UTC
   
✅ Privacy Policy (v3.0)
   Accepted on Jan 15, 2026 · 14:23 UTC

✅ SMS Marketing Consent
   Accepted on Feb 3, 2026 · 09:15 UTC
   [Withdraw SMS Consent]

❌ Marketing Emails
   Declined on Jan 15, 2026
   [Opt In]
   
✅ Community Guidelines (UGC Terms)
   Accepted on Jan 20, 2026 · 16:45 UTC

[Download as PDF]    [Email to me]
```

**Backend требования:**
- Все согласия записываются атомарно с транзакцией.
- Никогда не удалять записи Consent Log — только добавлять новые записи `action=withdrawn`.
- Endpoint: `GET /api/user/consent-history` → возвращает отсортированный список.
- Export: `GET /api/user/consent-history/export?format=pdf` → для GDPR Art.20 (право на переносимость).

---

## 5. Audit Log — Журнал аудита (внутренний)

### Что это

**Внутренний** журнал событий, связанных с обработкой персональных данных. **Не показывается пользователю** напрямую (хотя частично входит в Data Export по GDPR Art.20). Используется для ответов на запросы регуляторов.

### Почему нужно (GDPR Art.5(2))

Если регулятор проверит вашу компанию, он спросит: «Покажите журнал обработки данных». Без Audit Log вы не сможете ответить на большинство вопросов.

### ТЗ для Audit Log

**База данных:**
```sql
CREATE TABLE audit_log (
  id              UUID PRIMARY KEY,
  user_id         UUID,           -- NULL для системных событий
  actor_id        UUID,           -- кто выполнил действие (пользователь или admin)
  actor_type      TEXT,           -- 'user' | 'admin' | 'system'
  event_type      TEXT NOT NULL,  -- см. список ниже
  resource_type   TEXT,           -- 'profile' | 'post' | 'message' | 'account' | ...
  resource_id     UUID,
  metadata        JSONB,          -- дополнительный контекст
  ip_address      INET,
  user_agent      TEXT,
  created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

**Какие события логировать:**

| event_type | Описание |
|---|---|
| `login_success` | Успешный вход |
| `login_failed` | Неудачная попытка входа |
| `login_2fa_success` | Успешный вход с 2FA |
| `login_2fa_failed` | Неудачный ввод 2FA-кода |
| `2fa_enabled` | Включение двухфакторки |
| `2fa_disabled` | Отключение двухфакторки |
| `2fa_method_changed` | Смена метода 2FA |
| `password_changed` | Изменение пароля |
| `password_reset_requested` | Запрос сброса пароля |
| `email_changed` | Изменение email |
| `phone_changed` | Изменение телефона |
| `oauth_provider_connected` | Подключён Google/Apple/Facebook |
| `oauth_provider_disconnected` | Отключён Google/Apple/Facebook |
| `profile_updated` | Изменение данных профиля |
| `data_export_requested` | Запрос экспорта данных |
| `data_export_completed` | Данные экспортированы |
| `account_deletion_requested` | Запрос на удаление аккаунта |
| `account_deleted` | Аккаунт удалён |
| `admin_access` | Администратор просмотрел/изменил данные пользователя |
| `consent_granted` | Пользователь дал согласие (ссылка на consent_log) |
| `consent_withdrawn` | Пользователь отозвал согласие |
| `session_created` | Сессия создана (вход) |
| `session_terminated` | Сессия завершена (пользователем или системой) |
| `deindex_requested` | Запрос на де-индексацию в поисковиках (GDPR Art.17(2)) |

**Хранение:** Минимум 3 года. Шифрование строк с ip_address и user_agent (GDPR Art.32).  
**Доступ:** Только DevOps/Security team + compliance officers. Не доступен обычным поддержке.

---

## 6. DPO Contact

> Подробное ТЗ для кнопки Contact DPO — в [AccessibilitySpec.md §4](AccessibilitySpec.md#4-кнопка-contact-dpo)

**Краткое:** Разместить контактный email `dpo@bestme.app` в:
1. Settings → Help & Support → «Contact Data Protection Officer»
2. Settings → Your Data → «Questions about your data? Contact our DPO»
3. Privacy Policy (обязательно по GDPR Art.13(1)(b))
4. Сайт bestme.app/privacy → раздел «Contact»

---

## 7. Полная структура экрана

**Settings → Login & Security**

```
🔒 LOGIN & SECURITY

─── Аккаунт ──────────────────────────────────────────
  Email: user@example.com                [Изменить →]
  Пароль: ••••••••••                     [Изменить →]
  (скрыто для OAuth-аккаунтов без пароля)

─── Безопасность ─────────────────────────────────────
  Двухфакторная аутентификация           [ВЫКЛ → Включить]
  (только для email-аккаунтов)

  Активные сессии (3 устройства)         [Управлять →]
  История входов                         [Просмотреть →]

─── Связанные аккаунты ───────────────────────────────
  🍎 Apple       [Подключено]   [Отключить]   🔴 обязательно
  🔵 Google      [Подключить]
  🔷 Facebook    [Подключить]

─────────────────────────────────────────────────────
  ⚠️ Для отключения последнего способа входа
     сначала установите пароль.
```

**Settings → Your Data**

```
📊 YOUR DATA

Privacy Controls
  Do Not Sell My Personal Information    [Toggle: OFF]
  Personalised Ads                       [Toggle: ON]

Data Access
  Download Your Data                     [Request Export →]
  Consent History                        [View →]

Account
  Delete Account                         [→]

Legal
  Contact DPO (Data Protection Officer)  [Contact →]
  Privacy Policy                         [Read →]
```

---

## 8. Чеклист для разработчика

### 🔴 Sprint 1 — БЛОКЕРЫ ПУБЛИКАЦИИ (обязательно до App Store / Google Play)

**UI (App Store §5.1.3 + §5.1.1(v)):**
- [ ] **Sign in with Apple** реализован и отображается наравне с Google/Facebook (обязательно если есть любой 3rd-party login — App Store §5.1.3)
- [ ] Кнопка **[Отключить / Disconnect]** для каждого подключённого OAuth-провайдера (Apple/Google/Facebook)
- [ ] Защита от orphan: если последний способ входа — запросить установку пароля перед отключением
- [ ] **In-app путь удаления аккаунта** — Settings → Account → Account Management → Delete Account *(см. AccountDeletionSpec.md)*

**Google Play (с авг. 2024):**
- [ ] URL веб-страницы `bestme.app/account/delete` указан в Google Play Console → App Content → Data deletion *(см. AccountDeletionSpec.md)*

---

### 🟡 Sprint 2 — GDPR Art.5 (после получения публикации)

**Backend (обязательно):**
- [ ] Все API-endpoints только HTTPS, HTTP → redirect 301
- [ ] TLS 1.2+ на всех серверах, HSTS заголовок настроен
- [ ] Пароли хранятся как bcrypt/Argon2id (не MD5/SHA1)
- [ ] Таблица `auth_providers` создана (Google / Apple / Facebook / email)
- [ ] Таблица `sessions` создана, refresh tokens ротируются
- [ ] Таблица `consent_log` создана, все согласия записываются
- [ ] Таблица `audit_log` создана, события логируются (включая `oauth_provider_connected/disconnected`)
- [ ] Change Password: подтверждение текущего пароля, инвалидация сессий, уведомление на email
- [ ] Revoke OAuth-токен при Disconnect

**iOS (обязательно):**
- [ ] `NSAllowsArbitraryLoads = false` в Info.plist
- [ ] Certificate Pinning для production
- [ ] Sensitive data не логируются в os_log
- [ ] Tokens хранятся в Keychain (не UserDefaults)

**Android (обязательно):**
- [ ] `cleartextTrafficPermitted="false"` в network_security_config.xml
- [ ] Tokens хранятся в Android Keystore / EncryptedSharedPreferences
- [ ] Sensitive data не логируются в Logcat (ProGuard/R8 убирает logs в release)

**UI (обязательно):**
- [ ] Экран Change Password с валидацией (мин. 8 символов, заглавная буква, цифра/спецсимвол)
- [ ] Экран 2FA: выбор метода (Email OTP / TOTP App / SMS если телефон добавлен), backup codes
- [ ] Экран Active Sessions: список устройств, кнопка «Завершить сессию», «Завершить все другие»
- [ ] Экран Login History: список входов/выходов, кнопка «Это не я»
- [ ] Экран Consent History в Settings → Your Data
- [ ] Кнопка «Contact DPO» в Help & Support

**Документы (обязательно):**
- [ ] dpo@bestme.app создан и мониторится
- [ ] Privacy Policy обновлена: контакт DPO (GDPR Art.13(1)(b))
- [ ] Retention Policy задокументирована

---

## Ответ на вопрос: Нужна ли отдельная веб-страница /account/delete?

**Да, нужна веб-страница. Но in-app путь тоже нужен. Это разные вещи.**

| Компонент | Нужен? | Почему |
|---|---|---|
| **Веб-страница** `bestme.app/account/delete` | ✅ **Обязательно** | Google Play Developer Policy (с авг. 2024) **явно требует** URL веб-страницы в Google Play Console → App Content → Data deletion. Без URL нельзя опубликовать. |
| **In-app путь** Settings → Account → Account Management → Delete Account | ✅ **Обязательно** | App Store §5.1.1(v) требует in-app путь. Google Play также. |
| Оба вместе | ✅ **Да** | НЕ замена друг друга. Нужны ОБА. |

> 📎 Подробная спецификация веб-формы удаления — в [AccountDeletionSpec.md](AccountDeletionSpec.md).

---

*GDPRArt5SecuritySpec.md v1.4 · Bestme · март 2026*  
*Смежные документы: [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md), [AccessibilitySpec.md](AccessibilitySpec.md)*
