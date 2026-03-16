# Bestme — Полная структура настроек личного профиля v2.0
> **Версия:** 2.0 — полная перезапись с учётом ВСЕХ законов
> **Дата:** март 2026
> **Юрисдикции:** ЕС · США · Канада · Израиль · Калифорния
> **Законы:** GDPR Art.5/7/8/13/15-22/25/32/33/37 · DSA Art.14/17/18/20/25-29 · ePrivacy · Apple App Store (02.2026) · Google Play (2024) · TCPA 47 U.S.C. §227 · CAN-SPAM · CASL · COPPA · CCPA/CPRA · Quebec L25 · Israel PPL · EAA 2019/882 · ADA · AODA
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
| **Ограничение целей** | Art.5(1)(b) | Данные собираются только для указанных целей; запрет повторного использования без согласия |
| **Минимизация данных** | Art.5(1)(c) | Собираем только то, что нужно (имя, email, dob); телефон опционален |
| **Точность** | Art.5(1)(d) | Пользователь может редактировать все данные своего профиля |
| **Ограничение хранения** | Art.5(1)(e) | Политика хранения данных: 30 дней на восстановление после деактивации; немедленное удаление по запросу |
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

> Эти экраны НЕ являются частью меню Settings, но обязательны по закону и должны быть задокументированы здесь для разработки.

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

> **⚖️ Date of birth**: если пользователь указал возраст < 13 → **заблокировать регистрацию** с сообщением «К сожалению, Bestme доступен только с 13 лет». Перенаправить на helpline (**COPPA § 312.5**)

### L2: Управление аккаунтом

| L3 — Пункт | Тип | ⚖️/💡 | Закон | Примечание |
|---|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация) | ⚖️ | GDPR Art.17 | Данные сохраняются; доступ заморожен на срок до 30 дней; затем постоянное удаление |
| **Delete account** *(🔴 ОБЯЗАТЕЛЬНО)* | Действие (постоянное удаление) | ⚖️ 🔴 | GDPR Art.17 · CCPA §1798.105 · **App Store §5.1.1(v)** · **Google Play** | Открывает Поток 6 (Delete Account Modal) |

> **🔴 App Store §5.1.1(v)**: кнопка Delete account ОБЯЗАНА быть в настройках — без этого Apple отклонит приложение  
> **🔴 Google Play**: кнопка Delete account в приложении + отдельная веб-форма `https://bestme.com/account/delete` (URL вносится в Play Console)  
> **⚖️ GDPR Art.17(2)**: при удалении — backend автоматически вызывает Google Search Console API + Yandex.Webmaster API + Bing для де-индексации страницы профиля

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

> **⚠️ Возрастные дефолты**: для 13–17 лет — строгие defaults по **DSA Art.28(3)(g)**

| Настройка | variable_name | Тип | Default 18+ | Default 13–17 | ⚖️ | Закон |
|---|---|---|---|---|---|---|
| Private account | `account_private` | Toggle ON/OFF | `OFF` (открытый) | **`ON`** (закрытый) | ⚖️ | GDPR Art.25 · **DSA Art.28(3)(g)** — закрытый для 13–17 ОБЯЗАТЕЛЕН |
| Profile in search results | `profile_searchable` | Toggle ON/OFF | `ON` | `ON` | ⚖️ | GDPR Art.17 — право на забвение (opt-out) |
| SEO indexing (Google/Yandex/Bing) | `seo_indexable` | Toggle ON/OFF | **`OFF`** | **`OFF`** | ⚖️ | **GDPR Art.25(2) — СТРОГО OFF, штраф до 10 млн €** |
| Activity status / online status | `online_status_visible` | Toggle ON=Friends / OFF=Nobody | `ON` (=Friends) | `OFF` (=Nobody) | ⚖️ | GDPR Art.25 · ePrivacy |
| Show age | `birthday_visibility` | ENUM: Full date / Age only / Friends only / Only me / Hidden | `FRIENDS_AGE` | `ONLY_ME` | ⚖️ | COPPA · GDPR Art.9 · DSA Art.28 |
| Show relationship status | `relationship_visible` | ENUM: Everyone / Friends / Only me | `FRIENDS` | `ONLY_ME` | 💡 | — |

**Важные примечания:**
> ✅ `account_private = OFF` для 18+ **законно** (открытый профиль для взрослых, CNIL/ICO подтвердили)  
> ⚖️ `account_private = ON` для 13–17 **обязателен** по DSA Art.28(3)(g)  
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

> **⚠️ TCPA §227**: телефон пользователя НИКОГДА не должен быть публично виден другим пользователям или третьим лицам без явного письменного согласия. `phone_visibility = ONLY_ME` строго обязателен и не может быть изменён на PUBLIC.  
> **⚠️ CAN-SPAM + GDPR**: email пользователя аналогично НИКОГДА не отображается публично.

---

### 2.3 Content Visibility — Видимость контента

| Настройка | variable_name | Default 18+ | Default 13–17 | ⚖️ | Закон |
|---|---|---|---|---|---|
| Default post audience | `default_post_audience` | `FRIENDS` | `FRIENDS` | ⚖️ | GDPR Art.25 Privacy by Default |
| Who sees my photos/gallery | `photos_visibility` | `FRIENDS` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Who sees my friends list | `friends_list_visibility` | `FRIENDS` | `ONLY_ME` | 💡 | — |
| Who sees my activity feed | `activity_visibility` | `FRIENDS` | `ONLY_ME` | 💡 | — |
| Who sees my likes/reactions | `likes_visibility` | `FRIENDS` | `ONLY_ME` | 💡 | — |
| Who sees my challenges | `challenges_visibility` | `FRIENDS` | `ONLY_ME` | 💡 | — |
| Who sees my rewards/badges | `rewards_visibility` | `FRIENDS` | `ONLY_ME` | 💡 | — |

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

> **⚠️ DSA Art.27**: рядом с `recommendations_opt_out` обязательна кнопка/ссылка «Почему я вижу этот контент?» с объяснением критериев рекомендательного алгоритма.

---

### 2.6 Blocked Accounts — Заблокированные аккаунты

| Элемент | Описание | ⚖️ | Закон |
|---|---|---|---|
| Список заблокированных | Все заблокированные аккаунты | ⚖️ | **App Store §1.2** · **Google Play UGC** — ОБЯЗАТЕЛЬНО |
| Заблокировать пользователя | Кнопка Block на профиле/в чате | ⚖️ | App Store §1.2 · Google Play UGC |
| Разблокировать | Действие в списке | ⚖️ | — |

> **🔴 App Store §1.2 + Google Play UGC**: функция блокировки пользователей — обязательное требование для соцсетей. Без неё — автоматический отказ в публикации.

---

## 3. 🛡️ LOGIN & SECURITY — Вход и безопасность

**Обоснование:** ⚖️ GDPR Art.32 · Israel Data Security Regulations · App Store §4.8

| Настройка / Действие | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Change password** | — | Действие | — | ⚖️ | GDPR Art.32 |
| **Two-factor authentication (2FA)** | `two_fa_enabled` | Toggle + тип (SMS/Authenticator/Email) | `OFF` → рекомендовать включить | ⚖️ | GDPR Art.32 · Israel Data Security Regs |
| **Sign in with Apple** | — | Подключить/отключить | — | ⚖️ | **App Store §4.8 — ОБЯЗАТЕЛЬНО если есть Google/Facebook login** |
| **Sign in with Google** | — | Подключить/отключить + кнопка «Отключить» | — | ⚖️ | **App Store §5.1.1(v) — кнопка Disconnect ОБЯЗАТЕЛЬНА** NEW |
| **Sign in with Facebook** | — | Подключить/отключить + кнопка «Отключить» | — | ⚖️ | **App Store §5.1.1(v) — кнопка Disconnect ОБЯЗАТЕЛЬНА** NEW |
| **Active sessions** | — | Список устройств + дата/IP | — | ⚖️ | GDPR Art.32 |
| **Terminate all other sessions** | — | Действие | — | ⚖️ | GDPR Art.32 |
| **Login activity log** | — | Журнал входов | — | ⚖️ | GDPR Art.32 · Israel Data Security Regs |
| **Trusted devices** | — | Список + управление | — | 💡 | — |

> **🔴 App Store §4.8**: если в приложении есть Google / Facebook / Twitter / любой social login → **Sign in with Apple ОБЯЗАТЕЛЕН** как эквивалентный вариант.  
> **🔴 App Store §5.1.1(v)** NEW: для каждого подключённого стороннего провайдера (Google, Facebook и т.д.) должна быть отдельная кнопка **«Disconnect» / «Отключить»**, которая отзывает токен и разрывает связь с аккаунтом.

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

> **⚠️ CASL + ePrivacy**: ВСЕ marketing email-подписки = пустые по умолчанию. Pre-checked = нарушение. Каждое письмо содержит рабочую ссылку отписки.  
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

> **⚠️ App Store §5.1.2(iv)**: синхронизация контактов телефона — только с явного разрешения пользователя; нельзя «Select All» по умолчанию.

---

## 6. 📝 CONTENT & MODERATION — Контент и модерация

**Обоснование:** ⚖️ DSA Art.14/17 · App Store §1.2 · Google Play UGC Policy · GDPR Art.25

### 6.1 Content Creation Settings

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Default post audience | `default_post_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Default photo audience | `default_photo_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Allow location tagging | `location_tagging_enabled` | **`false`** | ⚖️ | GDPR Art.25 · ePrivacy |
| Safe Search / Content filter | `safe_search_enabled` | **`true`** | ⚖️ | App Store §1.2 · Google Play UGC |

### 6.2 Moderation & Reports

| Функция | Описание | ⚖️ | Закон |
|---|---|---|---|
| **Report a post** | Кнопка «...» на каждом посте | ⚖️ 🔴 | **App Store §1.2** · **Google Play UGC** |
| **Report a user** | Кнопка на профиле каждого пользователя | ⚖️ 🔴 | **App Store §1.2** · **Google Play UGC** |
| **Report child exploitation (CSAE)** *(NEW)* | Отдельная категория в Report | ⚖️ 🔴 | **Google Play Child Safety Standards** · COPPA |
| **Report AI-generated offensive content** *(NEW)* | Кнопка «Report AI content» | ⚖️ | **Google Play AI-Generated Content Policy** |
| **Appeal moderation decision** | Форма апелляции | ⚖️ | DSA Art.20 |
| **Moderation decision log** | История решений | ⚖️ | DSA Art.17 |

> **🔴 App Store §1.2**: 4 ОБЯЗАТЕЛЬНЫХ элемента: (1) фильтр контента, (2) механизм жалоб, (3) блокировка, (4) контактная информация. Без каждого из них — отказ.  
> **🔴 Google Play Child Safety Standards**: отдельная категория «Child Safety / Exploitation» в форме жалоб — обязательна для соцсетей и dating-приложений.

### Категории жалоб (report categories) — ОБЯЗАТЕЛЬНЫЙ СПИСОК

```
Report content:
├── Spam or fake content
├── Hate speech or discrimination
├── Violence or graphic content
├── Nudity or sexual content
├── Harassment or bullying
├── Misinformation
├── Intellectual property violation
├── [🔴 NEW] Child Safety / Exploitation (CSAE)
└── Other

Report user:
├── Fake account or impersonation
├── Spam
├── Harassment
├── Hate speech
├── [🔴 NEW] Exploiting a child (CSAE)
└── Other
```

---

## 7. 📦 YOUR DATA — Ваши данные

**Обоснование:** ⚖️ GDPR Art.15–22 · CCPA/CPRA §1798.100–120 · Quebec L25 · Israel PPL · GDPR Art.5(2) Accountability

### 7.1 Права субъекта данных

| Право | Функция | variable_name/action | ⚖️ | Закон |
|---|---|---|---|---|
| **Right to Access (Art.15)** | Download my data | `download_data_json` / `download_data_csv` | ⚖️ | GDPR Art.15 · PIPEDA · CCPA §1798.100 |
| **Right to Portability (Art.20)** | Export data (portable format) | `export_data_portable` | ⚖️ | GDPR Art.20 · Quebec L25 Art.27 |
| **Right to Erasure (Art.17)** | Request data deletion | → Поток 6 (Delete account) | ⚖️ | GDPR Art.17 · CCPA §1798.105 |
| **Right to Rectification (Art.16)** | Edit profile / correct data | → Account Settings | ⚖️ | GDPR Art.16 · GDPR Art.5(1)(d) Accuracy |
| **Right to Restriction (Art.18)** | Restrict processing | `restrict_processing` (freeze w/o delete) | ⚖️ | GDPR Art.18 |
| **Right to Object (Art.21)** | Opt-out from profiling | `profiling_opt_out` | ⚖️ | GDPR Art.21 · DSA Art.29 |
| **Right not to be subject to automated decisions (Art.22)** | Request human review | `request_human_review` | ⚖️ | GDPR Art.22 · Quebec L25 Art.8.1 · CPRA |
| **Withdraw consent (Art.7)** | Withdraw consent | `withdraw_consent` | ⚖️ | GDPR Art.7 · CASL |
| **View consent history** | Consent log | `view_consent_history` | ⚖️ | GDPR Art.7 · CASL |

### 7.2 CCPA / CPRA (Калифорния)

| Функция | Описание | ⚖️ | Закон |
|---|---|---|---|
| **Do Not Sell My Personal Information** *(NEW)* | Кнопка «Do Not Sell or Share» | ⚖️ 🔴 | **CCPA §1798.120 · CPRA** — ОБЯЗАТЕЛЬНА |
| Right to Know categories | Список категорий данных, которые мы собираем | ⚖️ | CCPA §1798.100 |
| Right to Correct | Редактирование данных | ⚖️ | CPRA §1798.106 |
| Opt-out of targeted ads | Связан с «Do Not Sell» | ⚖️ | CCPA/CPRA |

> **🔴 CCPA §1798.120**: кнопка «Do Not Sell My Personal Information» (или «Do Not Share») обязательна для приложений с аудиторией в Калифорнии. Должна быть заметной и легко доступной.

### 7.3 Политика хранения данных — GDPR Art.5(1)(e) Storage Limitation NEW

| Состояние аккаунта | Срок хранения | Основание |
|---|---|---|
| Активный аккаунт | Пока аккаунт активен | GDPR Art.5(1)(e) |
| Деактивированный аккаунт | 30 дней (восстановление) → затем удаление | GDPR Art.5(1)(e) |
| После запроса на удаление | Немедленное удаление + 90 дней на anti-fraud/legal данные | GDPR Art.17 · Art.5(1)(e) |
| После удаления (anti-fraud данные) | 90 дней | GDPR Art.17(3)(e) · CCPA |
| Email для unsubscribe list | 3 года | CAN-SPAM · CASL (доказательство отписки) |

> **⚠️ GDPR Art.5(1)(e)**: политика хранения должна быть явно указана в разделе «Your Data» и в Privacy Policy. Пользователь должен видеть, сколько хранятся его данные.

### 7.4 Прочее

| Функция | ⚖️ | Закон |
|---|---|---|
| Cookie settings | ⚖️ | GDPR · ePrivacy Art.5(3) |
| Ad preferences & opt-out | ⚖️ | GDPR Art.21/22 · DSA Art.29 |
| Contact DPO / Privacy Officer | ⚖️ | Quebec L25 Art.5 · GDPR Art.37 |
| Privacy Policy link | ⚖️ | GDPR Art.13 · **App Store §5.1.1(i)** · **Google Play** |
| Terms of Use link | ⚖️ | App Store · Google Play |

---

## 8. ♿ ACCESSIBILITY — Доступность

**Обоснование:** ⚖️ **EAA 2019/882** (ЕС, с 28.06.2025) · **ADA** (США) · **Israel Disability Law 5758-1998** · **AODA** (Канада) · **California Unruh Civil Rights Act §51** · App Store §2.5.4 · Google Play

| Настройка | variable_name | Default | WCAG | Закон |
|---|---|---|---|---|
| Text size | `text_size` | `NORMAL` (ENUM: Small/Normal/Large/XL) | 1.4.4 | EAA · ADA · Israel |
| Bold text | `bold_text_enabled` | `false` | 1.4.3 | EAA · ADA |
| High contrast mode | `high_contrast_enabled` | `false` | 1.4.3 (4.5:1) | EAA · ADA |
| Reduce motion | `reduce_motion_enabled` | `false` | 2.3.1 | EAA · ADA |
| Closed captions (videos) | `captions_enabled` | **`true`** | 1.2.2 | EAA · ADA · AODA |
| Auto-generate alt text | `alt_text_auto_enabled` | **`true`** | 1.1.1 | EAA · ADA · Israel |
| Screen reader information | — | Ссылка/инфо | 4.1.3 | EAA · ADA · App Store §2.5.4 |
| Keyboard navigation info | — | Ссылка/инфо | 2.1.1 | EAA · ADA |

---

## 9. ❓ HELP & SUPPORT — Помощь и поддержка

**Обоснование:** ⚖️ App Store §1.5 · Google Play · DSA Art.14 · **Google Play Child Safety Standards Policy**

### 9.1 Структура Help & Support

| Пункт | Описание | ⚖️ | Закон |
|---|---|---|---|
| Help Center / FAQ | Часто задаваемые вопросы | 💡 | — |
| Report a problem | Жалоба на контент/пользователя | ⚖️ 🔴 | **App Store §1.2** · **Google Play UGC** |
| **Child Safety** *(NEW)* | Отчёт о безопасности детей + контакт | ⚖️ 🔴 | **Google Play Child Safety Standards** |
| Privacy & Legal | Ссылки на Privacy Policy, Terms, Cookie Policy | ⚖️ | GDPR Art.13 · App Store |
| Contact support | Форма/email поддержки | ⚖️ | App Store §1.5 · DSA Art.14 |
| Contact DPO | Данные защиты персональных данных | ⚖️ | GDPR Art.37 · Quebec L25 Art.5 |
| Delete account (web) *(NEW)* | Ссылка `https://bestme.com/account/delete` | ⚖️ 🔴 | **Google Play (URL в Play Console)** |
| About Bestme | Версия, лицензии | 💡 | — |

### 9.2 Child Safety Section (🔴 NEW — Google Play Child Safety Standards)

```
Help & Support → Child Safety

Bestme строго запрещает контент, связанный
с сексуальной эксплуатацией детей (CSAE/CSAM).

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Сообщить о небезопасном контенте:
[Сообщить о нарушении — Child Safety]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Child Safety Point of Contact:
childsafety@bestme.com

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Если ребёнок в опасности — обратитесь
в местные правоохранительные органы:

USA: NCMEC — www.missingkids.org
EU:  Missing Children Europe — www.missingchildreneurope.eu
IL:  Police 100
RU:  МВД 102

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Правила сообщества]  [Terms of Service]
```

> **🔴 Google Play Child Safety Standards Policy** (5 обязательных пунктов для соцсетей):
> 1. ✅ **Published standards**: явный запрет CSAE в Terms of Service / Community Guidelines
> 2. ✅ **In-app feedback mechanism**: категория «Child Safety» в форме жалоб
> 3. ⚖️ **Address CSAM**: backend SLA — удалить CSAM в течение 24 часов + уведомить NCMEC/региональный орган
> 4. ⚖️ **Comply with child safety laws**: процесс отчётности в NCMEC (USA) / соответствующий орган
> 5. ✅ **Child Safety Point of Contact**: `childsafety@bestme.com` публично указан

---

## СВОДНАЯ ТАБЛИЦА ЗАКОНОВ × НАСТРОЙКИ

| Закон | Основные требования | Где реализовано |
|---|---|---|
| **GDPR Art.5** | 7 принципов обработки данных | Все разделы (Privacy by Default) |
| **GDPR Art.7** | Явное согласие + отзыв | Notifications · Your Data → Consent |
| **GDPR Art.8/DSA Art.28** | Возраст 13+ · несовершеннолетние | Date of birth · age-specific defaults |
| **GDPR Art.13** | Информирование при сборе данных | Onboarding Disclosure (Поток 1) |
| **GDPR Art.15** | Право на доступ | Your Data → Download |
| **GDPR Art.16** | Право на исправление | Account → Edit fields |
| **GDPR Art.17(1)** | Право на удаление | Account → Delete account (Поток 6) |
| **GDPR Art.17(2)** | Де-индексация при удалении | Backend API (Google/Yandex/Bing) + Поток 6 modal |
| **GDPR Art.18** | Право на ограничение | Your Data → Restrict Processing |
| **GDPR Art.20** | Право на переносимость | Your Data → Export |
| **GDPR Art.21/22** | Возражение/автоматические решения | Your Data → Opt-out + Human review |
| **GDPR Art.25** | Privacy by Default | Privacy → все defaults |
| **GDPR Art.32** | Безопасность данных | Login & Security |
| **GDPR Art.37** | DPO | Help & Support → Contact DPO |
| **DSA Art.14** | Жалобы на контент | Content & Moderation → Report |
| **DSA Art.17–20** | Модерация + апелляции | Notifications (non-disable) · Content & Moderation |
| **DSA Art.25–26** | Запрет на профилирование рекламы несовершеннолетних | age gate + Ad preferences |
| **DSA Art.27** | Объяснение рекомендательного алгоритма | Privacy → Discoverability + label |
| **DSA Art.28(3)(g)** | Закрытый профиль для 13–17 | `account_private=ON` для 13–17 |
| **DSA Art.29** | Opt-out от рекомендаций | Privacy → Discoverability |
| **ePrivacy Art.5(3)** | Cookies | Your Data → Cookie settings |
| **ePrivacy Art.13** | Согласие на коммерческие сообщения | Notifications → Email Marketing (empty checkboxes) |
| **TCPA 47 U.S.C. §227** | Prior express written consent для SMS | Поток 5 (SMS consent checkbox) · `phone_visibility=ONLY_ME` |
| **CAN-SPAM** | Физ. адрес + unsubscribe в email | Email templates · Notifications footer |
| **CASL** | Opt-in для marketing emails · пустые чекбоксы | Notifications → Email Marketing |
| **COPPA** | Блок регистрации < 13 | Date of birth age gate |
| **CCPA/CPRA §1798.100–120** | Права: знать/удалить/исправить/не продавать | Your Data → все права + «Do Not Sell» button |
| **Quebec L25** | DPO контакт · PIA · portability | Help & Support + Your Data |
| **Israel PPL** | email/phone скрыты · безопасность | Contact Info Privacy · Login & Security |
| **EAA 2019/882** | WCAG 2.1 AA · мобильные приложения | Accessibility раздел |
| **ADA / AODA** | Доступность | Accessibility раздел |
| **App Store §1.2** | UGC: фильтр + жалобы + блокировка + контакт | Content & Moderation · Privacy → Blocked |
| **App Store §4.5.4** | Push: opt-in · opt-out внутри | Notifications |
| **App Store §4.8** | Sign in with Apple обязателен | Login & Security |
| **App Store §5.1.1(i)** | Privacy Policy в приложении | Help & Support → Legal |
| **App Store §5.1.1(v)** | Delete account + Disconnect 3rd-party | Account · Login & Security |
| **App Store §5.1.2(i) ATT** | ATT диалог iOS | Поток 4 (ATT) |
| **Google Play UGC** | Report + Block обязательны | Content & Moderation · Privacy → Blocked |
| **Google Play Child Safety** | 5 обязательных пунктов | Help & Support → Child Safety |
| **Google Play Account Deletion** | In-app + web URL | Account → Delete + `bestme.com/account/delete` |
| **Google Play Prominent Disclosure** | Экран до запроса разрешений | Поток 3 (Prominent Disclosure) |

---

## ЧЕКЛИСТ ПУБЛИКАЦИИ — App Store + Google Play

### 🔴 БЛОКЕРЫ (без этого публикация невозможна)

| # | Требование | Статус | Где |
|---|---|---|---|
| 1 | Delete account — in-app | ✅ | Account → Delete account |
| 2 | Delete account — веб-форма `bestme.com/account/delete` | ⚠️ Нужно создать | Google Play Console → URL |
| 3 | Sign in with Apple (если есть Google/Facebook) | ✅ | Login & Security |
| 4 | Disconnect button для каждого 3rd-party login | ⚠️ Добавить | Login & Security |
| 5 | Block user — функция | ✅ | Privacy → Blocked Accounts |
| 6 | Report content / user — функция | ✅ | Content & Moderation |
| 7 | Report: категория «Child Safety / CSAE» | ⚠️ Добавить | Content & Moderation → Report |
| 8 | childsafety@bestme.com публично | ⚠️ Добавить | Help & Support → Child Safety |
| 9 | UGC ToS acceptance при первом контенте | ⚠️ Добавить | Поток 2 |
| 10 | ATT диалог iOS | ⚠️ Подтвердить SDK | Поток 4 |
| 11 | Prominent Disclosure перед Push/Camera | ⚠️ Добавить | Поток 3 |
| 12 | Блок регистрации < 13 лет | ⚠️ Добавить | Onboarding age gate |
| 13 | SMS consent checkbox (TCPA) | ⚠️ Добавить | Поток 5 |
| 14 | Onboarding Disclosure для 18+ (открытый профиль) | ⚠️ Добавить | Поток 1 |
| 15 | «Do Not Sell My Personal Information» button | ⚠️ Добавить | Your Data |
| 16 | Empty checkboxes для email opt-in (CASL) | ⚠️ Проверить | Notifications |
| 17 | Accessibility раздел | ✅ | Accessibility |
| 18 | Privacy Policy ссылка в приложении | ✅ | Help & Support → Legal |
| 19 | `seo_indexable = false` по умолчанию | ✅ | Privacy → Discoverability |
| 20 | `phone_visibility = ONLY_ME` по умолчанию | ✅ | Privacy → Contact Info |

### 🟡 ВАЖНО

| # | Требование | Статус | Где |
|---|---|---|---|
| 21 | One-click unsubscribe в каждом email | ⚠️ В email templates | Email backend |
| 22 | Физический адрес компании в footer email | ⚠️ В email templates | Email backend |
| 23 | DSA Art.27 — объяснение алгоритма | ⚠️ Добавить | Privacy → Discoverability |
| 24 | DPO контакт публично виден | ⚠️ Проверить | Help & Support |
| 25 | GDPR Art.18 — Restrict Processing | ✅ | Your Data |
| 26 | GDPR Art.17(2) — де-индексация при Delete (backend) | ⚠️ Backend задача | Backend API |
| 27 | GDPR Art.25(2) — Storage period policy | ⚠️ Добавить | Your Data + Privacy Policy |
| 28 | GDPR Art.22 — Human review request | ✅ | Your Data |
| 29 | Quebec L25 Art.5 — CPO контакт | ⚠️ Проверить | Help & Support |

### 🟢 РЕКОМЕНДАЦИИ

| # | Требование |
|---|---|
| 30 | Privacy Nutrition Labels в App Store Connect |
| 31 | Data Safety Form в Google Play Console |
| 32 | DPO назначен официально |
| 33 | Privacy Impact Assessment (PIA) для новых функций |
| 34 | Регистрация базы данных в Израиле (Israel PPL Sec.8) |

---

## ТЕХНИЧЕСКИЙ СЛОВАРЬ ПЕРЕМЕННЫХ (variable_names)

```
ENUM visibility:
  EVERYONE          — все пользователи и неавторизованные
  FRIENDS           — только друзья
  FRIENDS_OF_FRIENDS — друзья друзей
  ONLY_ME           — только я
  NOBODY            — никто

ENUM post audience:
  EVERYONE / FRIENDS / FRIENDS_OF_FRIENDS / ONLY_ME

Profile:
  account_private           bool   false (18+) / true (13–17)
  seo_indexable             bool   false (СТРОГО)
  profile_searchable        bool   true
  online_status_visible     bool   true → Friends only / false → Nobody
  email_visibility          ENUM   ONLY_ME
  phone_visibility          ENUM   ONLY_ME
  city_visibility           ENUM   FRIENDS
  website_visibility        ENUM   PUBLIC
  social_links_visibility   ENUM   PUBLIC
  birthday_visibility       ENUM   FRIENDS_AGE (18+) / ONLY_ME (13–17)
  relationship_visible      ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  default_post_audience     ENUM   FRIENDS
  default_photo_audience    ENUM   FRIENDS
  photos_visibility         ENUM   FRIENDS
  friends_list_visibility   ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  activity_visibility       ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  likes_visibility          ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  challenges_visibility     ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  rewards_visibility        ENUM   FRIENDS (18+) / ONLY_ME (13–17)
  who_can_message           ENUM   FRIENDS
  who_can_comment           ENUM   FRIENDS
  who_can_react             ENUM   EVERYONE
  who_can_tag               ENUM   FRIENDS
  tag_approval_required     bool   true
  auto_filter_comments      bool   true
  location_tagging_enabled  bool   false
  recommendations_opt_out   bool   false (в рекомендациях по умолчанию)

Security:
  two_fa_enabled            bool   false (рекомендовать включить)

Notifications:
  email_marketing_product   bool   false (пустой чекбокс)
  email_marketing_promo     bool   false
  email_marketing_tips      bool   false
  sms_consent               bool   false (пустой чекбокс при добавлении телефона)

Accessibility:
  text_size                 ENUM   NORMAL
  bold_text_enabled         bool   false
  high_contrast_enabled     bool   false
  reduce_motion_enabled     bool   false
  captions_enabled          bool   true
  alt_text_auto_enabled     bool   true
```

---

*Файл: `ProfileSettingsFullSpec.md` | Версия 2.0 | Дата: март 2026*  
*Юрисдикции: EU/EEA · USA · Canada · Israel · California*  
*Законы: GDPR · DSA · ePrivacy · TCPA · CAN-SPAM · CASL · COPPA · CCPA/CPRA · Quebec L25 · Israel PPL · EAA · ADA · AODA · App Store (02.2026) · Google Play (2024)*
