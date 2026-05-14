# Bestme — Полная структура настроек личного профиля v2.0
> **Версия:** 2.0 — полная перезапись с учётом ВСЕХ законов
> **Дата:** март 2026
> **Юрисдикции:** ЕС · США · Канада · Израиль · Калифорния
> **Законы:** GDPR Art.5/7/8/13/15-22/25/32/33/37 · DSA Art.14/17/18/20/25-29 · ePrivacy · Apple App Store (02.2026) · Google Play (2024) · TCPA 47 U.S.C. §227 · CAN-SPAM · CASL · COPPA
>
> **Обозначения:**
> ⚖️ = обязательно по закону (нарушение → штраф или отказ в публикации)
> 🔴 = критический блокер публикации в App Store / Google Play
> 🟡 = важно до значительного роста
> 🟢 = рекомендация
> 💡 = UX-норма
> 🚫 = нельзя выключить
> ✅ = реализовано
> ❌ = отсутствует, добавить
> NEW = новое требование v2.0

---

## GDPR ART.5 — ПРИНЦИПЫ ОБРАБОТКИ ДАННЫХ (ОСНОВА ВСЕЙ АРХИТЕКТУРЫ)

> **Все настройки ниже спроектированы в соответствии с 7 принципами GDPR Art.5.**
> Каждое поле, каждый default, каждый поток должен соответствовать этим принципам.

| Принцип | GDPR Art.5(1) | Как реализован в настройках |
|---|---|---|
| **Законность, справедливость, прозрачность** | Art.5(1)(a) | Privacy Policy ссылка + Onboarding Disclosure + GDPR Art.13 уведомление при регистрации |
| **Ограничение целей** | Art.5(1)(b) | Данные собираются только для указанных целей; запрет повторного использования для AI без opt-in |
| **Минимизация данных** | Art.5(1)(c) | Собираем только то, что нужно (имя, email, dob); телефон опционален |
| **Точность** | Art.5(1)(d) | Пользователь может редактировать все данные своего профиля |
| **Ограничение хранения** | Art.5(1)(e) | Политика хранения данных: 30 дней на восстановление после деактивации; немедленное удаление при Delete Account |
| **Целостность и конфиденциальность** | Art.5(1)(f) | 2FA, шифрование в передаче (HTTPS), управление сессиями |
| **Подотчётность** | Art.5(2) | DPO контакт, Privacy Policy, Consent History, аудит журнал |

---

## ПЕРВЫЙ ЭКРАН — Settings (главное меню)

| # | Иконка | Пункт (EN) | Пункт (RU) | ⚖️ | Основание |
|---|---|---|---|---|---|
| 1 | 👤 | Account | Аккаунт | ⚖️ | App Store §5.1.1(v) · Google Play · GDPR Art.17 |
| 2 | 🔒 | Privacy & Visibility | Приватность и видимость | ⚖️ | GDPR Art.25 — Privacy by Default |
| 3 | 🛡️ | Login & Security | Вход и безопасность | ⚖️ | GDPR Art.32 · App Store §4.8 |
| 4 | 🔔 | Notifications | Уведомления | ⚖️ | GDPR · CASL · CAN-SPAM · TCPA |
| 5 | 👥 | Friends | Друзья | 💡 | UX-норма соцсети |
| 6 | 📝 | Content & Moderation | Контент и модерация | ⚖️ | DSA Art.14 · App Store §1.2 · Google Play UGC |
| 7 | 📦 | Your Data | Ваши данные | ⚖️ | GDPR Art.15–22 · CCPA §1798.100–120 · Quebec L25 |
| 8 | ♿ | Accessibility | Доступность | ⚖️ | EAA 2019/882 · ADA · Israel Disability Law 5758-1998 · AODA · CA Unruh |
| 9 | ❓ | Help & Support | Помощь и поддержка | ⚖️ | App Store §1.5 · Google Play · DSA Art.14 |

---

## ОБЯЗАТЕЛЬНЫЕ ПОТОКИ (ONBOARDING / ПЕРВОЕ ИСПОЛЬЗОВАНИЕ)

> Эти экраны НЕ являются частью меню Settings, но обязательны по закону и должны быть задокументированы здесь для разработчиков и QA.

### 🔴 ПОТОК 1: Onboarding Disclosure — регистрация 18+ (GDPR Art.25(2)) NEW

**Когда:** при регистрации пользователя 18+ лет, до показа главного экрана  
**Закон:** GDPR Art.25(2) — открытый профиль по умолчанию законен для 18+ только при явном уведомлении  
**UI:**

```
┌──────────────────────────────────────────────┐
│         Добро пожаловать в Bestme            │
│                                              │
│  Ваш профиль будет виден другим              │
│  пользователям по умолчанию.                 │
│                                              │
│  Это значит, что ваше имя, фото и            │
│  публичные посты могут увидеть все           │
│  участники платформы.                        │
│                                              │
│  Вы можете изменить это в любой момент       │
│  в Настройки → Приватность.                  │
│                                              │
│  Ваш email, телефон и дата рождения          │
│  ВСЕГДА скрыты от других пользователей.      │
│                                              │
│  [Понятно, продолжить]                       │
│                                              │
│  Просматривая приложение, вы соглашаетесь   │
│  с [Условиями использования] и              │
│  [Политикой конфиденциальности].             │
└──────────────────────────────────────────────┘
```

---

### 🔴 ПОТОК 2: UGC Terms Acceptance — первый контент (App Store §1.2 + Google Play UGC) NEW

**Когда:** при ПЕРВОЙ попытке создать пост, оставить комментарий, загрузить фото  
**Закон:** Apple App Store §1.2 · Google Play UGC Policy  
**Важно:** НЕ pre-checked checkbox. Явное действие пользователя.

```
┌──────────────────────────────────────────────┐
│       Правила сообщества Bestme              │
│                                              │
│  Прежде чем публиковать первый контент,      │
│  ознакомьтесь с нашими правилами.            │
│                                              │
│  Запрещено публиковать:                      │
│  • Контент сексуального насилия над детьми   │
│  • Hate speech и дискриминацию              │
│  • Угрозы, травлю, харассмент               │
│  • Насилие и жестокий контент               │
│  • Мошенничество и спам                     │
│                                              │
│  Нарушения приводят к удалению контента     │
│  и блокировке аккаунта.                     │
│                                              │
│  [Условия использования] · [Правила сообщ.] │
│                                              │
│  [✓ Принять и продолжить]  [Отмена]         │
└──────────────────────────────────────────────┘
```

---

### 🔴 ПОТОК 3: Prominent Disclosure — перед запросом Push/Camera/Photos (Google Play) NEW

**Когда:** ДО системного диалога запроса разрешений (Push, Camera, Photos)  
**Закон:** Google Play User Data Policy — Prominent Disclosure & Consent  
**Важно:** Должен быть в потоке использования, не только в Privacy Policy

**Push-уведомления:**
```
┌──────────────────────────────────────────────┐
│  Bestme хочет отправлять уведомления        │
│                                              │
│  Мы используем push-уведомления для:        │
│  • Сообщений от друзей                      │
│  • Важных обновлений безопасности аккаунта  │
│  • Комментариев к вашим постам              │
│                                              │
│  Маркетинговые уведомления — только с       │
│  вашего явного согласия. Отключить можно    │
│  в любой момент: Настройки → Уведомления.   │
│                                              │
│  [Продолжить]   [Не сейчас]                 │
└──────────────────────────────────────────────┘
```

---

### 🔴 ПОТОК 4: ATT Диалог — iOS 14.5+ (App Store §5.1.2(i)) NEW

**Когда:** при первом запуске приложения (только iOS, если используются analytics/ads SDK)  
**Закон:** Apple App Store §5.1.2(i) · App Tracking Transparency  
**Реализация:** Системный iOS диалог NSUserTrackingUsageDescription.  
**NSUserTrackingUsageDescription (текст для Info.plist):**

```
Bestme использует данные для улучшения
персонализации ленты и аналитики
приложения. Вы можете отозвать согласие
в любой момент: iPhone Настройки → Bestme.
```

---

### 🔴 ПОТОК 5: TCPA SMS Consent — при добавлении телефона NEW

**Когда:** при добавлении/изменении номера телефона в Account Settings  
**Закон:** TCPA 47 U.S.C. §227(b) — штраф $1 500 за каждое SMS без письменного согласия  
**Важно:** чекбокс должен быть ПУСТЫМ по умолчанию (явный opt-in, не pre-checked)

```
┌──────────────────────────────────────────────┐
│  Номер телефона: +1 (XXX) XXX-XXXX           │
│                                              │
│  [ ] Я соглашаюсь получать SMS от Bestme    │
│      на этот номер.                          │
│      Частота сообщений: по необходимости     │
│      (OTP, безопасность, аккаунт).           │
│      Стандартные тарифы SMS применяются.     │
│      Для отписки ответьте STOP.              │
│                                              │
│      [Политика SMS-коммуникации]             │
│                                              │
│  Ваш телефон НИКОГДА не виден другим         │
│  пользователям (phone_visibility = Only Me). │
│                                              │
│  [Сохранить]   [Отмена]                      │
└──────────────────────────────────────────────┘
```

---

### 🔴 ПОТОК 6: Delete Account Modal — с объяснением де-индексации (GDPR Art.17(2)) NEW

**Когда:** при нажатии «Delete account» в Account Settings  
**Закон:** GDPR Art.17(2) · App Store §5.1.1(v) · Google Play

```
┌──────────────────────────────────────────────┐
│       Удаление аккаунта                      │
│                                              │
│  ⚠️ Это действие необратимо.                │
│                                              │
│  Что произойдёт:                             │
│  ✓ Все ваши данные будут удалены             │
│  ✓ Ваши посты и комментарии — удалены        │
│  ✓ Аккаунт нельзя восстановить               │
│  ✓ Ваш профиль будет удалён из поисковых    │
│    систем (до 30 дней)                       │
│                                              │
│  Что мы сохраним на срок до 90 дней:         │
│  • Данные для предотвращения мошенничества   │
│  • Данные для соблюдения требований закона   │
│  (см. Privacy Policy раздел «Хранение»)      │
│                                              │
│  Введите пароль для подтверждения:           │
│  [____________]                              │
│                                              │
│  [🗑 Удалить аккаунт навсегда]  [Отмена]    │
└──────────────────────────────────────────────┘
```

---

---

## 1. 👤 ACCOUNT — Аккаунт

**Обоснование:** ⚖️ App Store §5.1.1(v) · Google Play · GDPR Art.17 · GDPR Art.5(1)(d) Accuracy

### L2: Основная информация профиля

| L3 — Пункт | variable_name | Тип | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|---|
| Profile photo | `profile_photo_url` | Действие (загрузить / удалить) | — | 💡 | — |
| Display name | `display_name` | Текстовое поле | — | 💡 | — |
| Username / @handle | `username` | Текстовое поле (уникальный) | — | 💡 | — |
| Email address | `email` | Текстовое поле (верифицированный) | — | ⚖️ | GDPR Art.5(1)(d) — точность |
| Phone number | `phone` | Текстовое поле (опционально) + TCPA consent | — | ⚖️ | GDPR · **TCPA §227** — см. Поток 5 |
| Date of birth | `date_of_birth` | Дата | — | ⚖️ | **COPPA** (блок < 13) · GDPR Art.8 · DSA Art.28 |
| Gender | `gender` | Выбор (ENUM + «Не указывать») | `NOT_SPECIFIED` | 💡 | — |
| Language | `locale` | Выбор из списка | System locale | 💡 | — |
| Country / Region | `country_code` | Выбор | — | ⚖️ | GDPR Art.3 — применимое право |
| Bio / About | `bio` | Текстовое поле | — | 💡 | — |
| Website | `profile_website` | URL | — | 💡 | — |

> **⚖️ Date of birth**: если пользователь указал возраст < 18 → **заблокировать регистрацию** с сообщением «К сожалению, вы не можете зарегистрироваться». Приложение только для взрослых (отсутствуют механизмы родительского контроля).

### L2: Управление аккаунтом

| L3 — Пункт | Тип | ⚖️/💡 | Закон | Примечание |
|---|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация) | ⚖️ | GDPR Art.17 | Данные сохраняются; доступ заморожен на срок до возвращения пользователя. |
| **Delete account** *(🔴 ОБЯЗАТЕЛЬНО)* | Действие (постоянное удаление) | ⚖️ 🔴 | GDPR Art.17 · CCPA §1798.105 · **App Store §5.1.1(v)** · **Google Play** | См. Поток 6 (Модальное окно). Требует пароль. |

> **🔴 App Store §5.1.1(v)**: кнопка Delete account ОБЯЗАНА быть в настройках — без этого Apple отклонит приложение  
> **🔴 Google Play**: кнопка Delete account в приложении + отдельная веб-форма `https://bestme.com/account/delete` (URL вносится в Play Console)  
> **⚖️ GDPR Art.17(2)**: при удалении — backend автоматически вызывает Google Search Console API + Yandex.Webmaster API + Bing для де-индексации профиля, если профиль был `account_private=OFF`.

---

## 2. 🔒 PRIVACY & VISIBILITY — Приватность и видимость

**Обоснование:** ⚖️ GDPR Art.25 — Privacy by Default · GDPR Art.5(1)(c) Data Minimisation

### Экран подразделов Privacy & Visibility

| Подраздел | Описание | ⚖️/💡 |
|---|---|---|
| Account Privacy | Кто видит ваш профиль | ⚖️ GDPR Art.25 |
| Contact Info Privacy | Кто видит email/телефон/город | ⚖️ GDPR Art.25 + TCPA |
| Content Visibility | Кто видит посты, фото, активность | ⚖️ GDPR Art.25 |
| Interactions | Кто может писать, комментировать, отмечать | ⚖️ DSA Art.14 |
| Discoverability | Поиск, SEO-индексация, рекомендации | ⚖️ GDPR Art.17 + Art.22 + DSA Art.27 |
| Blocked Accounts | Список заблокированных пользователей | ⚖️ App Store §1.2 · Google Play UGC |

---

### 2.1 Account Privacy — Приватность аккаунта

> Приложение **только для 18+** — единый набор дефолтов без возрастных развилок.

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| Private account | `account_private` | Toggle ON/OFF | `OFF` (открытый) | ⚖️ | GDPR Art.25 — открытый профиль законен для 18+ |
| Profile in search results | `profile_searchable` | Toggle ON/OFF | `ON` | ⚖️ | GDPR Art.17 — право на забвение (opt-out) |
| SEO indexing (Google/Yandex/Bing) | `seo_indexable` | Toggle ON/OFF | **`OFF`** | ⚖️ | **GDPR Art.25(2) — СТРОГО OFF, штраф до 10 млн €** |
| Activity status / online status | `online_status_visible` | Toggle ON=Friends / OFF=Nobody | `ON` (=Friends) | ⚖️ | GDPR Art.25 · ePrivacy |
| Show age | `birthday_visibility` | ENUM: Full date / Age only / Friends only / Only me / Hidden | `FRIENDS_AGE` | ⚖️ | GDPR Art.9 |
| Show relationship status | `relationship_visible` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

**Важные примечания:**
> ✅ `account_private = OFF` **законно** для 18+ (открытый профиль для взрослых, CNIL/ICO подтвердили)  
> ⚠️ `seo_indexable`: нельзя ставить ON по умолчанию (GDPR Art.25(2)); пользователь может включить вручную  
> ⚠️ `online_status_visible ON` = видят ТОЛЬКО ДРУЗЬЯ (не все пользователи платформы)

---

### 2.2 Contact Info Privacy — Видимость контактной информации

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Who sees email | `email_visibility` | **`ONLY_ME`** | ⚖️ | **GDPR Art.25 · CAN-SPAM — НИКОГДА не PUBLIC** |
| Who sees phone | `phone_visibility` | **`ONLY_ME`** | ⚖️ | **GDPR Art.25 · TCPA §227 — НИКОГДА не PUBLIC** |
| Who sees city | `city_visibility` | `FRIENDS` | 💡 | GDPR Art.25 |
| Who sees website | `website_visibility` | `PUBLIC` | 💡 | — |
| Who sees social links | `social_links_visibility` | `PUBLIC` | 💡 | — |

> **⚠️ TCPA §227**: телефон пользователя НИКОГДА не должен быть публично виден другим пользователям или третьим лицам без дополнительных согласий.
> **⚠️ CAN-SPAM + GDPR**: email пользователя аналогично НИКОГДА не отображается публично.

---

### 2.3 Content Visibility — Видимость контента

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Default post privacy | `default_post_privacy` | `FRIENDS` | ⚖️ | GDPR Art.25 Privacy by Default |
| Default media privacy (Photos/Videos) | `default_media_privacy` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Who sees my friends list | `friends_list_visibility` | `FRIENDS` | 💡 | — |
| Who sees my activity feed | `activity_visibility` | `FRIENDS` | 💡 | — |
| Who sees my likes/reactions | `likes_visibility` | `FRIENDS` | 💡 | — |
| Who sees my challenges | `challenges_visibility` | `FRIENDS` | 💡 | — |
| Who sees my rewards/badges | `rewards_visibility` | `FRIENDS` | 💡 | — |

**ENUM-значения видимости (стандарт):**
`EVERYONE` | `FRIENDS` | `FRIENDS_OF_FRIENDS` | `ONLY_ME`

---

### 2.4 Interactions — Взаимодействия

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Who can send me messages | `who_can_message` | `FRIENDS` | ⚖️ | DSA Art.14 · Israel PPL Sec.2 |
| Who can comment my posts | `who_can_comment` | `FRIENDS` | ⚖️ | DSA Art.14 |
| Who can react to my posts | `who_can_react` | `EVERYONE` | 💡 | — |
| Who can tag me in posts | `who_can_tag` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Tag approval required | `tag_approval_required` | `true` | ⚖️ | GDPR Art.25 — всегда требует одобрения |
| Comment moderation keywords | `comment_filter_keywords` | `[]` (пустой список) | 💡 | App Store §1.2 — фильтрация контента |
| Filter offensive comments (auto) | `auto_filter_comments` | `true` | ⚖️ | App Store §1.2 · Google Play UGC — метод фильтрации обязателен |

---

### 2.5 Discoverability — Обнаружимость

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Profile in search results | `profile_searchable` | `true` | ⚖️ | GDPR Art.17 — право на забвение (opt-out доступен) |
| SEO indexing | `seo_indexable` | **`false`** | ⚖️ | **GDPR Art.25(2) — OFF обязателен** |
| Appear in «People you may know» | `recommendations_opt_out` | `false` (в рекомендациях) | ⚖️ | GDPR Art.22 · DSA Art.29 · CCPA §1798.121 |
| Algorithm explanation | — | Ссылка/кнопка | ⚖️ | **DSA Art.27 — «Почему вас рекомендуют»** NEW |

> **⚠️ DSA Art.27**: рядом с `recommendations_opt_out` обязательна кнопка/ссылка «Почему я вижу этот контент?» с объяснением параметров алгоритма.

---

### 2.6 Blocked Accounts — Заблокированные аккаунты

| Элемент | Описание | ⚖️ | Закон |
|---|---|---|---|
| Список заблокированных | Все заблокированные аккаунты | ⚖️ | **App Store §1.2** · **Google Play UGC** — ОБЯЗАТЕЛЬНО |
| Заблокировать пользователя | Кнопка Block на профиле/в чате | ⚖️ | App Store §1.2 · Google Play UGC |
| Разблокировать | Действие в списке | ⚖️ | — |

> **🔴 App Store §1.2 + Google Play UGC**: функция блокировки пользователей — обязательное требование для соцсетей. Без нее 100% отказ модерации.

---

## 3. 🛡️ LOGIN & SECURITY — Вход и безопасность

**Обоснование:** ⚖️ GDPR Art.32 · Israel Data Security Regulations · App Store §4.8

| Настройка / Действие | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Change password** | — | Действие | — | ⚖️ | GDPR Art.32 |
| **Two-factor authentication (2FA)** | `two_fa_enabled` | Toggle + тип (Email OTP · TOTP App; SMS — только если телефон добавлен в профиль) | `OFF` → рекомендуется | ⚖️ | GDPR Art.32 |
| **Sign in with Apple** | — | Подключить/отключить | — | ⚖️ | **App Store §4.8 — ОБЯЗАТЕЛЬНО если есть Google/Facebook login** |
| **Sign in with Google** | — | Подключить/отключить + кнопка «Отключить» | — | ⚖️ | **App Store §5.1.1(v) — кнопка Disconnect ОБЯЗАТЕЛЬНА** NEW |
| **Sign in with Facebook** | — | Подключить/отключить + кнопка «Отключить» | — | ⚖️ | **App Store §5.1.1(v) — кнопка Disconnect ОБЯЗАТЕЛЬНА** NEW |
| **Active sessions** | — | Список устройств + дата/IP | — | ⚖️ | GDPR Art.32 |
| **Terminate all other sessions** | — | Действие | — | ⚖️ | GDPR Art.32 |
| **Login activity log** | — | Журнал входов | — | ⚖️ | GDPR Art.32 · Israel Data Security Regs |
| **Trusted devices** | — | Список + управление | — | 💡 | — |

> **🔴 App Store §4.8**: если в приложении есть Google / Facebook / Twitter / любой social login → **Sign in with Apple ОБЯЗАТЕЛЕН** как эквивалент.  
> **🔴 App Store §5.1.1(v)** NEW: для каждого подключённого стороннего провайдера (Google, Facebook и т.д.) должна быть отдельная кнопка отключения/отзыва доступа.

---

## 4. 🔔 NOTIFICATIONS — Уведомления

**Обоснование:** ⚖️ GDPR Art.7 · ePrivacy Art.13 · CASL · CAN-SPAM · **TCPA §227** · App Store §4.5.4

### 4.0 Каналы доставки

На экране уведомлений — 3 переключателя каналов:

| Канал | ⚖️ | Закон |
|---|---|---|
| **Push** (мобильные) | ⚖️ Требует разрешения iOS/Android | iOS: системный ATT диалог. Android: runtime permission |
| **Email** | ⚖️ Требует opt-in для маркетинга | CAN-SPAM (USA) · CASL (Canada) · ePrivacy Art.13 (EU) |
| **In-app** | 💡 Не требует разрешений | — |

> **⚠️ CASL + ePrivacy**: галочки opt-in для Email-маркетинга = **пустые по умолчанию** (pre-checked ЗАПРЕЩЕНЫ)  
> **⚠️ TCPA §227**: SMS-уведомления требуют отдельного **письменного согласия** (см. Поток 5)  
> **⚠️ CAN-SPAM**: в каждом email — физический адрес организации + рабочая ссылка отписки (≤ 10 дней)  
> **⚠️ CASL**: one-click unsubscribe в каждом marketing email

### 4.1 Account & Security (⚖️ 🚫 НЕЛЬЗЯ ВЫКЛЮЧИТЬ)

| Key | Описание | Каналы | Закон |
|---|---|---|---|
| `profile_security_login_new_device` | Вход с нового устройства | Email, Push, In-app | GDPR Art.32 |
| `profile_security_suspicious_login_attempt` | Подозрительная попытка входа | Email, Push | GDPR Art.32 |
| `profile_security_password_changed` | Пароль изменён | Email, In-app | GDPR Art.32 |
| `profile_security_contacts_changed` | Email/телефон изменены | Email, In-app | GDPR Art.32 |
| `profile_security_suspicious_activity` | Подозрительная активность | Email, Push | GDPR Art.32 |
| `profile_data_export_ready` | Файл экспорта данных готов | Email, In-app | GDPR Art.15 |
| `profile_data_export_requested` | Запрос на экспорт принят | Email, In-app | GDPR Art.15 |
| `profile_account_suspended` | Аккаунт заблокирован | Email, In-app | DSA Art.17/20 |
| `profile_account_restored` | Аккаунт восстановлен | In-app, Email | DSA Art.20 |
| `profile_account_deletion_completed` | Удаление завершено | Email, In-app | GDPR Art.12+17 |
| `profile_account_deletion_requested` | Запрос на удаление принят | Email, In-app | GDPR Art.17 |

### 4.2 System & Legal (⚖️ 🚫 НЕЛЬЗЯ ВЫКЛЮЧИТЬ)

| Key | Описание | Каналы | Закон |
|---|---|---|---|
| `system_terms_updated` | Обновлены Условия использования | Email, In-app | GDPR Art.7 |
| `system_privacy_updated` | Обновлена Политика конфиденциальности | Email, In-app | GDPR Art.13 |
| `system_accessibility_updates` | Изменения в доступности | In-app | EAA |
| `system_maintenance` | Техническое обслуживание | Push, In-app | UX-норма |

### 4.3 Content & Moderation (⚖️ 🚫 НЕЛЬЗЯ ВЫКЛЮЧИТЬ)

| Key | Описание | Каналы | Закон |
|---|---|---|---|
| `system_moderation_content_removed` | Контент удалён модерацией | Email, In-app | DSA Art.17 |
| `system_moderation_content_rejected` | Контент не прошёл | In-app | DSA Art.17 |
| `profile_complaint_received` | Жалоба на ваш контент | In-app | DSA Art.17 |
| `profile_appeal_decision` | Решение по апелляции | Email, In-app | **DSA Art.20** |

### 4.4 Social Activity (💡 можно выключить)

| Key | Описание | Default | Каналы |
|---|---|---|---|
| `profile_new_post_comment` | Комментарий к посту | ✅ ON | In-app, Push |
| `profile_reply_comment` | Ответ на комментарий | ✅ ON | In-app, Push |
| `profile_reaction_post` | Реакция на пост | ✅ ON | In-app |
| `profile_reaction_comment` | Реакция на комментарий | ✅ ON | In-app |
| `user_mention_post` | Упоминание в посте | ✅ ON | In-app, Push |
| `user_mention_comment` | Упоминание в комментарии | ✅ ON | In-app |
| `profile_friend_request` | Запрос в друзья | ✅ ON | In-app, Push |
| `profile_friend_request_accepted` | Запрос принят | ✅ ON | In-app |
| `profile_post_shared` | Поделились постом | ✅ ON | In-app |

### 4.5 Chat (💡 можно выключить)

| Key | Описание | Default | Каналы |
|---|---|---|---|
| `chat_new_message` | Новое сообщение | ✅ ON | In-app, Push |
| `chat_request` | Запрос на переписку | ✅ ON | In-app, Push |
| `chat_reacted` | Реакция на сообщение | ✅ ON | In-app |
| `chat_request_declined` | Запрос отклонён | ✅ ON | In-app |
| `chat_cannot_send_messages` | Невозможно отправить | ✅ ON | In-app |
| `chat_request_accepted` | Запрос принят | ✅ ON | In-app |

### 4.6 Email Marketing Consent (⚖️ CASL + ePrivacy) NEW

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Product news & updates | `email_marketing_product` | **`false`** (пустой чекбокс) | ⚖️ | CASL · ePrivacy Art.13 |
| Special offers & promotions | `email_marketing_promo` | **`false`** | ⚖️ | CASL · ePrivacy Art.13 |
| Tips & best practices | `email_marketing_tips` | **`false`** | ⚖️ | CASL |

> **⚠️ CASL + ePrivacy**: ВСЕ marketing email-подписки = пустые по умолчанию. Pre-checked = нарушение. Каждое письмо содержит рабочую ссылку unsubscribe.
> **⚠️ CAN-SPAM**: footer каждого email = физический адрес компании + unsubscribe link

---

## 5. 👥 FRIENDS — Друзья

**Обоснование:** 💡 UX-норма социальной сети

| Настройка / Функция | Описание | ⚖️/💡 |
|---|---|---|
| Incoming friend requests | Список входящих запросов | 💡 |
| Sent friend requests | Список исходящих | 💡 |
| Suggestions | «Вы можете знать» | ⚖️ GDPR Art.22 — opt-out должен быть |
| Find friends (contacts import) | Синхронизация контактов | ⚖️ **GDPR Art.6 + App Store §5.1.2(iv) — запрос разрешения** |
| Who can send friend requests | `who_can_friend_request` (ENUM: Everyone / FOAF / Nobody) | Default: `EVERYONE` | 💡 |

> **⚠️ App Store §5.1.2(iv)**: синхронизация контактов телефона — только с явного разрешения пользователя; нельзя «Silent upload».

---

## 6. 📝 CONTENT & MODERATION — Контент и модерация

**Обоснование:** ⚖️ DSA Art.14/17 · GDPR Art.16/21/22 · DSA Art.27 · AI Act Art.50 · App Store §1.2 · Google Play UGC Policy · GDPR Art.25

### 6.0 Feed & Content — Лента и контент

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Default feed | `default_feed` | `SMART_FEED` | ⚖️ | DSA Art.27 · AI Act Art.50 |
| Opt out from recommendations | `feed_personalization_opt_out` | `false` | ⚖️ | GDPR Art.22 · DSA Art.29 |
| **Reset Smart Feed (сброс алгоритма)** | — (Action) | — | ⚖️ | GDPR Art.16 / Art.21 |
| About recommendations | — (Link) | — | ⚖️ | DSA Art.27 · AI Act Art.50 |

#### Экран «About recommendations» — полный текст
**Закон:** DSA Art.27 (Евросоюз) + AI Act Art.50 — прозрачность алгоритмов.
*(Текст должен быть доступен по клику из настроек ленты)*:
> "Лента рекомендаций Bestme использует алгоритмы для показа контента.  
> **Главные факторы ранжирования:**  
> 1. Ваше взаимодействие (лайки, комментарии, время просмотра).  
> 2. Свежесть контента (дата публикации).  
> 3. Общие друзья и сообщества с автором.  
> Вы можете в любой момент сбросить алгоритм или полностью отключить персонализацию ленты."

#### 🔄 Reset Smart Feed — полная спецификация
**Действие:** кнопка «Сбросить настройки ленты» (Reset Smart Feed).  
**Юридическое основание:** GDPR Art.16 (право на исправление профиля) и Art.21 (право на возражение).  
**Логика бэкенда при нажатии:**
1. Очистить таблицу `user_interaction_scores` (веса лайков, интересов, dwell time).
2. Сбросить категорийные теги (interest graphs).
3. Перевести ленту в режим "Cold Start" (показывать общие популярные посты и только прямых друзей без ранжирования), пока алгоритм заново не обучится.
4. **Не удалять:** историю поиска, сохранённые посты, подписки.

### 6.1 Content Creation Settings

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Default post privacy | `default_post_privacy` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Default media privacy | `default_media_privacy` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Allow location tagging | `location_tagging_enabled` | **`false`** | ⚖️ | GDPR Art.25 · ePrivacy |
| Safe Search / Content filter | `safe_search_enabled` | **`true`** | ⚖️ | App Store §1.2 · Google Play UGC |

> **⚠️ GDPR Art.25 Privacy by Default**: геометки (location_tagging) СТРОГО выключены (`false`) по умолчанию. Перед включением — Prominent Disclosure (см. Поток 3).

### 6.2 Moderation & Reports

**Закон:** EU DSA Art.14 (Notice and Action) · DSA Art.17 (Statement of Reasons) · Apple App Store §1.2  

| Элемент | Логика / Требование |
|---|---|
| **Кнопка Report (Жалоба)** | Доступна на КАЖДОМ посте, профиле, комментарии, медиа-файле (в меню "⋮") |
| **Блокировка** | Юзер должен иметь возможность заблокировать автора контента сразу после жалобы |
| **Notice and Action (DSA)** | При отправке жалобы генерируется `report_id`. Юзер получает In-app/Email уведомление о решении. |
| **Statement of Reasons** | Если модератор удаляет контент, автор удалённого контента получает Email с объяснением причины (со ссылкой на пункт правил) и кнопкой "Апелляция". |
| **Апелляция (Appeal)** | Право на обжалование решения (DSA Art.20) — кнопка в уведомлении. |

### Категории жалоб (report categories) — ОБЯЗАТЕЛЬНЫЙ СПИСОК
*(🔴 Требуется Google Play Child Safety Policy и DSA)*

1. 🔴 **Child Safety / Exploitation (CSAE)** — *Critical, немедленный репорт в NCMEC*
2. **Violence or Gore** (Насилие)
3. **Hate Speech / Harassment** (Вражда / Травля)
4. **Adult Content / Nudity** (Порнография)
5. **Spam / Scam / Fraud** (Спам / Мошенничество)
6. 🔴 **AI-Generated / Deepfake** (Немаркированный ИИ контент) — *Новое требование Google Play*
7. **Terrorism / Extremism** (Терроризм)
8. **Self-Harm / Suicide** (Призывы к суициду)

---

## 7. 📦 YOUR DATA — Ваши данные

**Обоснование:** ⚖️ GDPR Art.15–22 · CCPA §1798.100–120 · PIPEDA · Quebec L25

### 7.1 Права субъекта данных

Все эти права должны быть реализованы в виде кнопок / действий:

| Право | Как реализовано | ⚖️ | Основание |
|---|---|---|---|
| **Right of Access** | Кнопка «Download my data». Бэкенд генерирует JSON/CSV файл. Уведомление на email при готовности. | ⚖️ | GDPR Art.15 · CCPA §1798.100 |
| **Data Portability** | Часть «Download my data» (машиночитаемый формат JSON для миграции в другие соцсети). | ⚖️ | GDPR Art.20 · Quebec L25 |
| **Right to Object** | Кнопка «Отказ от рекомендаций» и «Ad preferences (opt-out)». | ⚖️ | GDPR Art.21 |
| **Right not to be subject to AI** | Кнопка «Запрос проверки решения человеком» (Human review) — например, для автоматического бана. | ⚖️ | GDPR Art.22 · Quebec L25 Art.8.1 |
| **Restrict Processing** | Кнопка «Заморозить аккаунт / Ограничить обработку» (профиль скрыт, но данные не удаляются). | ⚖️ | GDPR Art.18 |
| **Consent History** | Ссылка «История согласий» — лог: когда, с какого IP и на что юзер давал consent (Terms, Privacy, Ads). | ⚖️ | GDPR Art.7(1) — proof of consent |
| **Right to Erasure** | Кнопка Delete Account + отдельный запрос удаления без закрытия аккаунта. | ⚖️ | GDPR Art.17 |

### 7.2 CCPA / CPRA (Калифорния)

| Настройка | variable_name | Тип | Default | ⚖️ | Основание |
|---|---|---|---|---|---|
| **Do Not Sell My Personal Information** | `ccpa_do_not_sell` | Тумблер/Кнопка | `false` | ⚖️ | **CCPA §1798.120** |
| Limit Use of Sensitive Personal Info | `ccpa_limit_sensitive` | Тумблер | `false` | ⚖️ | CPRA §1798.121 |

> **⚠️ CCPA**: Ссылка «Do Not Sell or Share My Personal Information» должна быть **явной и видимой** для пользователей из Калифорнии (США).

### 7.3 Политика хранения данных — GDPR Art.5(1)(e) Storage Limitation NEW

> *Эта информация должна отображаться текстом в разделе Your Data.*

* **Деактивированные аккаунты:** Хранятся бессрочно (или N лет по выбору), пока юзер не вернётся, НО скрыты от всех.
* **Удалённые аккаунты:** 30 дней (Grace period), затем Hard Delete.
* **Логи серверов / IP-адреса:** Удаляются или анонимизируются через 90 дней.
* **Бэкапы БД:** Удаляются в рамках цикла ротации (обычно 30 дней).

### 7.4 Прочее

| Пункт | Описание | ⚖️ | Основание |
|---|---|---|---|
| Cookie Preferences | Настройка аналитических и рекламных cookies | ⚖️ | ePrivacy Directive (EU) |
| Clear Cache | Очистка кэша приложения на устройстве | 💡 | App Store Guidelines (Resource Mgmt) |

---

## 8. ♿ ACCESSIBILITY — Доступность

**Обоснование:** ⚖️ European Accessibility Act 2019/882 (вступает 28.06.2025) · ADA · AODA · CA Unruh Civil Rights Act · **App Store §2.5.4**

| Настройка / Поддержка | variable_name | Тип | ⚖️ | Основание / Стандарт |
|---|---|---|---|---|
| **Text size / Dynamic Type** | `text_size` | Slider / System Sync | ⚖️ | EAA · ADA · WCAG 2.1 AA (1.4.4) |
| **High contrast mode** | `high_contrast` | Toggle | ⚖️ | EAA · WCAG 2.1 AA (1.4.3) |
| **Reduce motion** | `reduce_motion` | Toggle / System Sync | ⚖️ | EAA · ADA · WCAG 2.3 (Seizures) |
| **VoiceOver / TalkBack** | — | System Support | ⚖️ | **App Store §2.5.4 — ОБЯЗАТЕЛЬНО** |
| **Closed Captions (Video)** | `captions_enabled` | Toggle | ⚖️ | EAA · ADA · WCAG 2.1 AA (1.2.2) |
| **Alt text for images** | `alt_text_enabled` | Toggle (default `true`) | ⚖️ | EAA · WCAG 2.1 AA (1.1.1) |

> **🔴 App Store §2.5.4 + EAA**: Приложение обязано поддерживать системные экранные дикторы (VoiceOver на iOS / TalkBack на Android). Все кнопки и элементы интерфейса должны иметь осмысленные метки (`accessibilityLabel`). Это закон, а не просто пожелание магазинов.

---

## 9. ❓ HELP & SUPPORT — Помощь и поддержка

**Обоснование:** ⚖️ DSA Art.14/16 · GDPR Art.37 · App Store §1.5

### 9.1 Структура Help & Support

| Пункт | Тип | ⚖️ | Основание |
|---|---|---|---|
| Help Center / FAQ | Внешняя ссылка или In-app webview | 💡 | — |
| Contact Support | Форма с полем email и категорией | ⚖️ | App Store §1.5 |
| **Report a Problem (Bugs/Tech)** | Форма с логами (опционально) | 💡 | — |
| **Privacy Policy** | Ссылка | ⚖️ | App Store · Google Play · GDPR Art.13 |
| **Terms of Use** | Ссылка | ⚖️ | App Store · Google Play |
| **Contact Data Protection Officer (DPO)** | Форма или email (privacy@) | ⚖️ | Quebec L25 Art.5 · GDPR Art.37 |

### 9.2 Child Safety Section (🔴 NEW — Google Play Child Safety Standards)
**Закон:** Google Play Developer Policy — Child Safety.
Приложение 18+ (Social Media) обязано предоставлять быстрый, очевидный способ сообщить об эксплуатации детей (CSAE).
*   В разделе Help & Support должна быть кнопка или email (например, `childsafety@bestme.com`).
*   Форма репорта: «Report Child Exploitation / Safety Concern» — с приоритетной маршрутизацией.

---

## СВОДНАЯ ТАБЛИЦА ЗАКОНОВ × НАСТРОЙКИ

| Закон / Директива | Требование | Где реализовано в Settings |
|---|---|---|
| **GDPR Art. 17** | Право на удаление (Right to Erasure) | 1. Account → Delete account |
| **GDPR Art. 25** | Privacy by Default | 2. Privacy (Всё выключено / Friends Only по умолчанию) |
| **GDPR Art. 20** | Переносимость данных (Data Portability) | 7. Your Data → Download my data (JSON) |
| **GDPR Art. 32** | Безопасность данных (Security) | 3. Login & Security (2FA, Sessions) |
| **GDPR Art. 22** | Отказ от AI-решений | 6. Content → Opt out from recommendations |
| **EU DSA Art. 14** | Механизм жалоб на контент | 6. Moderation → Кнопка Report на постах |
| **EU DSA Art. 27** | Прозрачность алгоритмов | 6. Content → About recommendations |
| **EU EAA 2019/882** | Цифровая доступность | 8. Accessibility |
| **CCPA §1798.120** | Запрет продажи данных | 7. Your Data → Do Not Sell My Info (Калифорния) |
| **TCPA / CAN-SPAM** | Согласие на коммуникацию | 1. Account (SMS checkbox) + 4. Notifications |
| **Apple App Store** | Требования к публикации | Sign in with Apple, Delete Account, ATT, Block User, VoiceOver |

---

## ЧЕКЛИСТ ПУБЛИКАЦИИ — App Store + Google Play

### 🔴 БЛОКЕРЫ (без этого публикация невозможна)
- [ ] Кнопка **Delete Account** есть в приложении.
- [ ] Веб-форма **Delete Account** доступна по URL без входа в приложение (для Google Play).
- [ ] Кнопки **Block User** и **Report Content** работают на UGC контенте.
- [ ] EULA / Правила сообщества принимаются пользователем перед созданием первого поста.
- [ ] Системный диалог **ATT** (iOS) реализован перед сбором данных.
- [ ] **Prominent Disclosure** показано перед запросом геолокации и пушей.
- [ ] **Sign in with Apple** внедрён (если есть Google/FB вход).
- [ ] Для всех сторонних провайдеров входа (Google/FB) есть кнопка **Disconnect (Отключить)**.
- [ ] Раздел **Child Safety** (жалобы) добавлен в Help & Support (Google Play).

### 🟡 ВАЖНО
- [ ] Privacy Nutrition Labels заполнены в App Store Connect.
- [ ] Data Safety Form заполнена в Google Play Console.
- [ ] Политика конфиденциальности содержит контакт DPO и срок хранения данных.
- [ ] Добавлено объяснение алгоритма ленты («Почему я это вижу»).

### 🟢 РЕКОМЕНДАЦИИ
- [ ] Поддержка VoiceOver / TalkBack для всех важных кнопок.
- [ ] JSON/CSV формат для экспорта данных (Data Portability).

---

## ТЕХНИЧЕСКИЙ СЛОВАРЬ ПЕРЕМЕННЫХ (variable_names)

```json
{
  "account_private": false,
  "profile_searchable": true,
  "seo_indexable": false,
  "online_status_visible": "FRIENDS",
  "birthday_visibility": "FRIENDS_AGE",
  "relationship_visible": "FRIENDS",
  "email_visibility": "ONLY_ME",
  "phone_visibility": "ONLY_ME",
  "city_visibility": "FRIENDS",
  "website_visibility": "PUBLIC",
  "social_links_visibility": "PUBLIC",
  "default_post_privacy": "FRIENDS",
  "default_media_privacy": "FRIENDS",
  "friends_list_visibility": "FRIENDS",
  "activity_visibility": "FRIENDS",
  "likes_visibility": "FRIENDS",
  "who_can_message": "FRIENDS",
  "who_can_comment": "FRIENDS",
  "who_can_react": "EVERYONE",
  "who_can_tag": "FRIENDS",
  "tag_approval_required": true,
  "recommendations_opt_out": false,
  "two_fa_enabled": false,
  "email_marketing_product": false,
  "email_marketing_promo": false,
  "email_marketing_tips": false,
  "location_tagging_enabled": false,
  "safe_search_enabled": true,
  "ccpa_do_not_sell": false,
  "text_size": "NORMAL",
  "high_contrast": false,
  "reduce_motion": false,
  "captions_enabled": false,
  "alt_text_enabled": true
}
```
