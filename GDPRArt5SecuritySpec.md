# GDPRArt5SecuritySpec.md — ТЗ для GDPR Art.5: Безопасность, DPO, Consent History

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик, DevOps  
**Статус:** 🟡 Требования для предотвращения штрафов (штраф до €20 млн или 4% оборота)

> **Важно:** Эти требования **не блокируют ревью** App Store / Google Play, но их нарушение может привести к штрафам от регуляторов GDPR (особенно ЕС, Израиль). Реализовывать в Sprint 2, после получения публикации.

---

## Содержание

1. [GDPR Art.5(1)(f) — Целостность и конфиденциальность (безопасность)](#1-gdpr-art51f--целостность-и-конфиденциальность)
2. [GDPR Art.5(2) — Подотчётность](#2-gdpr-art52--подотчётность)
3. [Consent History — История согласий](#3-consent-history--история-согласий)
4. [Audit Log — Журнал аудита (внутренний)](#4-audit-log--журнал-аудита)
5. [DPO Contact — Контакт ответственного за данные](#5-dpo-contact)
6. [Как выглядит в приложении](#6-как-выглядит-в-приложении)
7. [Чеклист для разработчика](#7-чеклист-для-разработчика)

---

## 1. GDPR Art.5(1)(f) — Целостность и конфиденциальность

### Что говорит закон

> «Персональные данные должны обрабатываться с обеспечением надлежащей безопасности, включая защиту от несанкционированной или незаконной обработки, от случайной потери, уничтожения или повреждения, с применением надлежащих технических или организационных мер.»
> — GDPR Art.5(1)(f)

### Что это означает на практике для приложения

Три конкретных механизма: **2FA (двухфакторная авторизация)**, **HTTPS (шифрование передачи)**, **управление сессиями**.

---

### 1.1 2FA — Двухфакторная авторизация

**Что это:**  
При входе в аккаунт пользователь дополнительно подтверждает личность вторым методом: SMS-код, email-код, или TOTP-приложение (Google Authenticator, Authy).

**Где находится в приложении:**  
Settings → Login & Security → Two-Factor Authentication (2FA)

**Почему нужно (GDPR Art.5(1)(f)):**  
Если аккаунт взломают из-за отсутствия 2FA — это нарушение «надлежащей безопасности». Регулятор может выписать штраф даже если утечки данных не было — достаточно показать, что меры были недостаточны.

**ТЗ для 2FA:**

| Параметр | Значение |
|---|---|
| **variable_name** | `two_factor_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `false` (рекомендуется предлагать включить при регистрации) |
| **Методы** | SMS (TOTP via Twilio Verify) · Email OTP · TOTP App (RFC 6238) |

**Поток включения 2FA:**
```
Пользователь нажимает «Enable 2FA»
→ Выбирает метод: SMS / Email / Authenticator App
→ SMS/Email: вводит номер/email → получает 6-значный код → вводит код → ✅ Включено
→ Authenticator App: сканирует QR-код (TOTP secret) → вводит 6-значный код → ✅ Включено
→ Система сохраняет: two_factor_enabled=true, two_factor_method, recovery_codes (10 кодов)
```

**Поток входа с 2FA:**
```
Пользователь вводит email + пароль
→ Backend проверяет credentials → если верно и two_factor_enabled=true
→ Отправляет OTP (SMS/Email) или ждёт TOTP
→ Пользователь вводит код
→ Backend верифицирует → выдаёт access_token
```

**Backend требования:**
- TOTP: RFC 6238, 6 цифр, 30-секундное окно, HMAC-SHA1.
- Backup codes: 10 одноразовых кодов, показать один раз, хранить как bcrypt-хэши.
- Rate limiting: не более 5 попыток ввода кода за 15 минут → блокировка.
- Логировать: успешный вход с 2FA, неудачные попытки, смену метода 2FA.

---

### 1.2 HTTPS — Шифрование передачи данных

**Что это:**  
Все данные между приложением и сервером передаются только по зашифрованному каналу HTTPS (TLS 1.2+). Никаких HTTP-запросов с персональными данными.

**Почему нужно (GDPR Art.5(1)(f)):**  
Передача персональных данных по HTTP — прямое нарушение «надлежащей безопасности». Это одно из первых, что проверяет регулятор при расследовании.

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
- iOS: `NSAppTransportSecurity` — не добавлять исключения без крайней необходимости. Включить `NSAllowsArbitraryLoads = false`.
- Android: `network_security_config.xml` — добавить `<domain-config cleartextTrafficPermitted="false">`.
- Никогда не логировать access tokens, пароли, personal data в console/Logcat.

---

### 1.3 Управление сессиями (Session Management)

**Что это:**  
Контроль над активными сессиями пользователя — список устройств, на которых выполнен вход, возможность завершить сессию на любом устройстве, автоматическое завершение по истечении времени.

**Где находится в приложении:**  
Settings → Login & Security → Active Sessions (Активные сессии)

**Почему нужно (GDPR Art.5(1)(f)):**  
Если пользователь потерял устройство — он должен иметь возможность немедленно завершить сессию на нём. Это минимизирует риск несанкционированного доступа.

**ТЗ для управления сессиями:**

| Параметр | Значение |
|---|---|
| **Хранение** | Таблица `sessions`: user_id, device_name, device_type, ip_address, last_active_at, created_at, is_current |
| **Access token** | JWT, срок действия 15 минут |
| **Refresh token** | Secure HTTP-only cookie или хранилище Keychain/Keystore, срок 30 дней |
| **Автоистечение** | Refresh token истекает через 30 дней неактивности |

**Что показывать пользователю (UI):**
```
📱 Active Sessions

[✓ Current] iPhone 14 Pro · Moscow, Russia
             Last active: Just now

[  ] MacBook Pro · Berlin, Germany
             Last active: 2 days ago
             [Sign Out This Device]

[  ] iPhone 12 · Unknown location
             Last active: 15 days ago
             [Sign Out This Device]

[Sign Out All Other Devices]
```

**Backend требования:**
- При входе: создать запись в `sessions`.
- При выходе с конкретного устройства: удалить refresh_token, инвалидировать сессию.
- При «Sign Out All»: удалить все refresh tokens кроме текущего.
- При смене пароля: инвалидировать ВСЕ сессии кроме текущей.
- Логировать: создание сессии (IP, User-Agent), завершение сессии.

---

## 2. GDPR Art.5(2) — Подотчётность

### Что говорит закон

> «Контролёр несёт ответственность за соблюдение принципов и должен быть в состоянии продемонстрировать это соответствие.»
> — GDPR Art.5(2)

### Что это означает для продукта

Четыре конкретных элемента: DPO контакт, Privacy Policy, Consent History, Audit Log.

---

## 3. Consent History — История согласий

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

## 4. Audit Log — Журнал аудита (внутренний)

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
| `2fa_enabled` | Включение двухфакторки |
| `2fa_disabled` | Отключение двухфакторки |
| `password_changed` | Изменение пароля |
| `email_changed` | Изменение email |
| `phone_changed` | Изменение телефона |
| `profile_updated` | Изменение данных профиля |
| `data_export_requested` | Запрос экспорта данных |
| `data_export_completed` | Данные экспортированы |
| `account_deletion_requested` | Запрос на удаление аккаунта |
| `account_deleted` | Аккаунт удалён |
| `admin_access` | Администратор просмотрел/изменил данные пользователя |
| `consent_granted` | Пользователь дал согласие (ссылка на consent_log) |
| `consent_withdrawn` | Пользователь отозвал согласие |
| `session_terminated` | Сессия завершена (пользователем или системой) |
| `deindex_requested` | Запрос на де-индексацию в поисковиках (GDPR Art.17(2)) |

**Хранение:** Минимум 3 года. Шифрование строк с ip_address и user_agent (GDPR Art.32).  
**Доступ:** Только DevOps/Security team + compliance officers. Не доступен обычным поддержке.

---

## 5. DPO Contact

> Подробное ТЗ для кнопки Contact DPO — в [AccessibilitySpec.md §4](AccessibilitySpec.md#4-кнопка-contact-dpo)

**Краткое:** Разместить контактный email `dpo@bestme.app` в:
1. Settings → Help & Support → «Contact Data Protection Officer»
2. Settings → Your Data → «Questions about your data? Contact our DPO»
3. Privacy Policy (обязательно по GDPR Art.13(1)(b))
4. Сайт bestme.app/privacy → раздел «Contact»

---

## 6. Как выглядит в приложении

### Settings → Login & Security

```
🔒 LOGIN & SECURITY

Account
  Email: user@example.com                [Change]
  Password: ••••••••••                   [Change]

Security
  Two-Factor Authentication (2FA)        [OFF → Enable]
  Active Sessions (3 devices)            [Manage →]
  Login History                          [View →]

Third-Party Login
  Connected with Google                  [Disconnect]
  Connected with Apple                   [Disconnect]
  Facebook                               [Connect]
```

### Settings → Your Data

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

### Settings → Login & Security → Active Sessions

```
📱 ACTIVE SESSIONS

✅ Current Device
iPhone 14 Pro · iOS 17.2
Moscow, Russia · March 18, 2026, 14:23

📱 iPhone 12 Mini
Last active: Feb 28, 2026
Berlin, Germany
[Sign Out This Device]

💻 MacBook Pro (Chrome)
Last active: Mar 10, 2026
Tel Aviv, Israel
[Sign Out This Device]

━━━━━━━━━━━━━━━━━
[Sign Out All Other Devices]
```

---

## 7. Чеклист для разработчика

### Sprint 2 — GDPR Art.5 (после получения публикации)

**Backend (обязательно):**
- [ ] Все API-endpoints только HTTPS, HTTP → redirect 301
- [ ] TLS 1.2+ на всех серверах
- [ ] HSTS заголовок настроен
- [ ] Пароли хранятся как bcrypt/Argon2id (не MD5/SHA1)
- [ ] Таблица `sessions` создана, refresh tokens ротируются
- [ ] Таблица `consent_log` создана, все согласия записываются
- [ ] Таблица `audit_log` создана, 18 типов событий логируются

**iOS (обязательно):**
- [ ] `NSAllowsArbitraryLoads = false` в Info.plist
- [ ] Certificate Pinning настроен для production
- [ ] Sensitive data не логируются в os_log
- [ ] Tokens хранятся в Keychain (не UserDefaults)

**Android (обязательно):**
- [ ] `cleartextTrafficPermitted="false"` в network_security_config.xml
- [ ] Tokens хранятся в Android Keystore / EncryptedSharedPreferences
- [ ] Sensitive data не логируются в Logcat (ProGuard/R8 убирает logs в release)

**UI (обязательно):**
- [ ] Экран 2FA: включение/выключение, выбор метода, backup codes
- [ ] Экран Active Sessions: список устройств, кнопка «Sign out»
- [ ] Экран Consent History в Settings → Your Data
- [ ] Кнопка «Contact DPO» в Help & Support

**Документы (обязательно):**
- [ ] dpo@bestme.app создан и мониторится
- [ ] Privacy Policy обновлена: добавлен контакт DPO (GDPR Art.13(1)(b))
- [ ] Retention Policy задокументирована (сколько хранятся какие данные)

---

## Ответ на вопрос: Нужна ли отдельная веб-страница /account/delete?

**Да, нужна веб-страница. Но in-app путь тоже нужен. Это разные вещи.**

| Компонент | Нужен? | Почему |
|---|---|---|
| **Веб-страница** `bestme.app/account/delete` | ✅ **Обязательно** | Google Play Developer Policy (с авг. 2024) **явно требует** URL веб-страницы в поле «App Content → Data deletion» в Google Play Console. Без этого URL нельзя опубликовать приложение. |
| **In-app путь** Settings → Account → Delete Account | ✅ **Обязательно** | App Store §5.1.1(v) требует, чтобы удаление было доступно из самого приложения. Google Play также требует in-app путь. |
| Оба вместе | ✅ **Да** | Это НЕ замена друг друга. Нужны ОБА. |

**Что должна содержать веб-страница `/account/delete`:**
```
Страница: bestme.app/account/delete

Заголовок: Delete Your BestMe Account

Описание: "To delete your account, please enter your email address. 
We will send you a confirmation link."

Поле: Email address [____________]
Кнопка: [Send Deletion Request]

Ниже:
"You can also delete your account directly in the app:
Settings → Account → Account Management → Delete Account"

"Data Deletion Timeline:
• Your profile and posts will be removed immediately
• Personal data will be deleted within 30 days
• Backup data will be deleted within 90 days
• See our Privacy Policy for details"
```

**Backend для веб-формы:**
- Получить email → найти аккаунт → отправить email с confirmation link.
- Confirmation link → активировать процесс удаления (тот же что и in-app).
- Если аккаунта нет → показать «If an account exists, you'll receive an email» (не раскрывать, есть ли аккаунт).

---

*GDPRArt5SecuritySpec.md v1.0 · Bestme · март 2026*  
*Смежные документы: [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md), [AccessibilitySpec.md](AccessibilitySpec.md)*
