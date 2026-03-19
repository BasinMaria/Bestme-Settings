# SettingsOverview.md — Общая структура настроек профиля BestMe

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик, PM  
**Статус:** Мастер-документ — обзор всех 9 разделов настроек

> **Этот документ** — главный обзор всех 9 разделов настроек приложения BestMe.  
> Каждый раздел ссылается на отдельный подробный документ (spec).  
> Используйте его как **карту навигации** по всему ТЗ настроек.

---

## Обозначения

| Символ | Значение |
|---|---|
| ⚖️ | Обязательно по закону — нарушение ведёт к штрафу или отказу в публикации |
| 💡 | Рекомендация — UX-норма, лучшая практика |
| 🔴 | Критичный блокер публикации |
| 🟡 | Важно до значительного роста аудитории |
| 🟢 | Рекомендуется для улучшения доверия |

---

## Первый экран Settings — что видит пользователь

Когда пользователь нажимает на «Settings» (⚙️), он видит список из 9 основных разделов.  
Это **L1 (первый уровень)** навигации.

```
⚙️ Settings
│
├── 1️⃣  👤  Account
├── 2️⃣  🔒  Privacy & Visibility
├── 3️⃣  🛡️  Login & Security
├── 4️⃣  🔔  Notifications
├── 5️⃣  👥  Friends & Community
├── 6️⃣  📝  Content
├── 7️⃣  📦  Your Data
├── 8️⃣  ♿  Accessibility
└── 9️⃣  ❓  Help & Support
```

> 💡 **UX-стандарт порядка разделов:**  
> — Личное и управление аккаунтом (1) → приватность (2) → безопасность (3) → коммуникации (4) → социальное (5) → контент (6) → данные (7) → доступность (8) → поддержка (9)  
> — Такой порядок принят в Instagram, Facebook, TikTok, LinkedIn.

---

## 9 разделов — полное описание

---

### 1️⃣ 👤 ACCOUNT

**Путь:** Settings → Account  
**Правовое основание:** ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17  
**Подробный документ:** [AccountSpec.md](AccountSpec.md)

**Что включает:**
- **User Info** — аватар, статус (на аватарке), обложка, имя, дата рождения, пол, **Interests** (6 категорий)
- **Profile Info** — Bio, Goals, Language
- **Contact Info** — Email, Phone, Location, Address, Personal link, Blog link, Business link
- **Account Management** — Deactivate, Delete account, Switch to Business, Create Business account

**6 категорий Interests (одновременно Category):**  
Sport · Nutrition · Environment · Aesthetics & Hygiene · Mental Health · Daily Routine

**Блокеры публикации:**
- 🔴 Кнопка «Delete account» — прямо из Settings → Account → Account Management (App Store §5.1.1(v), Google Play)
- 🔴 Веб-форма `bestme.app/account/delete` (Google Play — отдельно от in-app)

---

### 2️⃣ 🔒 PRIVACY & VISIBILITY

**Путь:** Settings → Privacy & Visibility  
**Правовое основание:** ⚖️ GDPR Art.25 (Privacy by Default) · DSA Art.14 · ePrivacy · Israel PPL  
**Подробный документ:** [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md)

**Что включает:**
- **Account Privacy** — Private account, Profile in search, SEO indexing, Relationship status
- **Profile Visibility** — кто видит имя, аватар, обложку, bio, статус, день рождения, пол, интересы, цели
- **Contact Info Privacy** — кто видит email, phone, location, address, ссылки
- **Content Visibility** — видимость постов, галереи, списка друзей, подписок, ленты, лайков, сохранений
- **Interactions** — кто может писать, тегировать, комментировать, делиться постами; онлайн-статус, прочитано
- **Discoverability** — поиск, SEO, алгоритм рекомендаций
- **Safety & Blocked Accounts** — блокировки, жалобы (Report user / Report content)

**Блокеры публикации:**
- 🔴 `seo_indexable = false` строго по умолчанию (GDPR Art.25 — штраф до 10 млн €)
- 🔴 Кнопка **Report user** на каждом профиле (DSA Art.16 — обязательно для ЕС)
- 🔴 Кнопка **Report content** на каждом посте/фото/комменте (DSA Art.16)

---

### 3️⃣ 🛡️ LOGIN & SECURITY

**Путь:** Settings → Login & Security  
**Правовое основание:** ⚖️ GDPR Art.32 · App Store §5.1.3 (Sign in with Apple) · Google Play  
**Подробный документ:** [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)

**Что включает:**
- **Change password** — смена пароля
- **Two-factor authentication (2FA)** — SMS-код (если телефон добавлен в профиль)
- **Sign in with Apple / Google / Facebook** — 3rd-party login
- **Disconnect 3rd-party login** — 🔴 кнопка отключения (App Store §5.1.1(v))
- **Active sessions** — список устройств, выход из сессий
- **Login history** — журнал входов

**Блокеры публикации:**
- 🔴 Кнопка **Disconnect** для каждого 3rd-party login-провайдера (App Store §5.1.1(v))
- 🔴 Sign in with Apple — обязателен если есть другие 3rd-party login (App Store §5.1.3)

> 💬 **2FA:** SMS доступна только если телефон добавлен в профиле (Account → Contact Info).  
> Регистрация использует email. 2FA не обязательна для MVP по GDPR.

---

### 4️⃣ 🔔 NOTIFICATIONS

**Путь:** Settings → Notifications  
**Правовое основание:** ⚖️ GDPR Art.6/7 (согласие) · App Store · Google Play · CASL · CAN-SPAM  
**Подробный документ:** [NotificationsSpec.md](NotificationsSpec.md)

**Что включает:**

| Категория уведомлений | UI-название | Default |
|---|---|---|
| Push-уведомления | Push notifications | ON (с согласия) |
| Email-уведомления | Email notifications | ON (с согласия) |
| SMS-уведомления | SMS notifications | OFF ⚖️ TCPA |
| Уведомления о сообщениях | Messages | ON |
| Уведомления о друзьях | Friends & requests | ON |
| Уведомления о реакциях | Reactions & comments | ON |
| Уведомления о контенте в ленте | Feed recommendations | ON (можно отключить) |
| Уведомления о дискуссиях | Discussions & community | ON |
| Системные уведомления | System & security | ON (нельзя отключить) |

**Блокеры публикации:**
- 🔴 **Pre-checked boxes = пустые** для email/SMS opt-in (CASL Канада · ePrivacy ЕС)
- 🔴 **One-click unsubscribe** в каждом email (CAN-SPAM США · CASL · ePrivacy)
- 🔴 **SMS consent checkbox** при добавлении телефона (TCPA — штраф $1 500 за SMS без согласия)

---

### 5️⃣ 👥 FRIENDS & COMMUNITY

**Путь:** Settings → Friends & Community  
**Правовое основание:** ⚖️ GDPR Art.25 (видимость списка друзей) · DSA Art.14  
**UX-норма:** 💡 Стандарт соцсети (Instagram, Facebook, Discord)

**Что включает:**

```
Settings → Friends & Community
├── My Friends              — список друзей
├── Friend Requests         — входящие/исходящие запросы в друзья
├── Subscribed Blogs        — блоги, на которые подписан пользователь
│                             (подписаться можно на любое количество)
├── My Blog                 — управление собственным блогом
│                             (создать можно только 1 блог)
├── Subscribed Communities  — сообщества, в которых состоит пользователь
│                             (присоединиться можно к любому количеству)
├── My Communities          — сообщества, созданные пользователем
│                             (создать можно любое количество)
├── Followed Business Profiles — бизнес-профили, на которые подписан
│                             (можно оставлять комментарии и рейтинг)
└── Suggestions             — рекомендации (алгоритм)
```

**Правила платформы BestMe:**
- Блог: пользователь может создать **только 1** собственный блог, но подписаться на **любое количество** чужих блогов
- Сообщества: пользователь может создать **любое количество** сообществ и вступить в **любое количество** сообществ
- Бизнес-профили: можно подписаться, оставить комментарий и рейтинг (rating)

> 💡 **Visibility этого раздела управляется в Privacy & Visibility:**  
> — Список друзей: `friends_list_visibility`  
> — Подписки на блоги: `subscribed_blogs_visibility`  
> — Подписки на сообщества: `subscribed_communities_visibility`

---

### 6️⃣ 📝 CONTENT

**Путь:** Settings → Content  
**Правовое основание:** ⚖️ DSA Art.14 · GDPR Art.25 · Google Play UGC Policy · App Store §1.2  
**Подробный документ:** [ProfileSettingsFullSpec.md](ProfileSettingsFullSpec.md)

**Что включает:**

| Блок | UI-название | Описание |
|---|---|---|
| **Saved content** | Saved / Bookmarks | Контент, который пользователь сохранил («закладки») |
| **Posted content** | My Posts | Управление опубликованным контентом |
| **Content sharing** | Sharing | Настройки шеринга (внутри платформы и вовне) |
| **Feed preferences** | Feed | Настройки алгоритма ленты (какой контент показывать) |
| **Discussion settings** | Discussions | Участие в тематических дискуссиях по категориям |
| **UGC Terms acceptance** | Community Guidelines | Принятие правил публикации контента |
| **Archived posts** | Archive | Архив скрытых постов |

**Типы контента в BestMe:**
- **Посты** в профиле с лайками, комментариями, оценками
- **Шеринг** — поделиться контентом внутри системы и за её пределами
- **Сохранение** — сохранить контент, чтобы не потерять
- **Лента (Feed)** — алгоритм подбирает актуальный контент по Interests пользователя
- **Дискуссии** — тематические страницы по каждой категории, где люди открывают публичные обсуждения, задают вопросы, делятся материалами; контент тематически отбирается по категории

**Блокеры публикации:**
- 🔴 **UGC ToS acceptance** при первом создании контента (Google Play UGC Policy · App Store §1.2)

---

### 7️⃣ 📦 YOUR DATA

**Путь:** Settings → Your Data  
**Правовое основание:** ⚖️ GDPR Art.15–22 · CCPA §1798.100–120 · PIPEDA · Quebec L25 · Israel PPL  
**Подробный документ:** [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md)

**Что включает:**

| Пункт | UI-название | ⚖️ | Закон |
|---|---|---|---|
| Скачать мои данные | Download my data | ⚖️ | GDPR Art.15 (право на доступ) · CCPA §1798.100 |
| Что мы знаем о вас | See what we know | ⚖️ | GDPR Art.15 |
| Исправить данные | Correct my data | ⚖️ | GDPR Art.16 (право на исправление) |
| Ограничить обработку | Restrict processing | ⚖️ | GDPR Art.18 |
| Не продавать мои данные | Do Not Sell My Personal Information | ⚖️ | CCPA/CPRA §1798.120 🔴 |
| История согласий | Consent history | ⚖️ | GDPR Art.7(3) |
| Удаление данных | Delete my data | ⚖️ | GDPR Art.17 · CCPA §1798.105 |
| Контакт с DPO | Contact our DPO / Privacy Officer | ⚖️ | Quebec L25 Art.5 · GDPR Art.37 |

**Блокеры публикации:**
- 🔴 **«Do Not Sell My Personal Information»** — CCPA/CPRA §1798.120 (Калифорния)
- 🔴 Кнопка «Download my data» — GDPR Art.15 (право на доступ)

---

### 8️⃣ ♿ ACCESSIBILITY

**Путь:** Settings → Accessibility  
**Правовое основание:** ⚖️ EU EAA 2019/882 · ADA (США) · Israel Disability Law 5758-1998 · AODA (Канада) · California Unruh Act · App Store §2.5.4 · Google Play  
**Подробный документ:** [AccessibilitySpec.md](AccessibilitySpec.md)

**Что включает:**

| Настройка | variable_name | Default | ⚖️ |
|---|---|---|---|
| **Text size** (размер текста) | `text_size_scale` | System (1.0x) | ⚖️ EAA · ADA |
| **Bold text** (жирный текст) | `bold_text_enabled` | System | ⚖️ EAA · ADA |
| **High contrast mode** | `high_contrast_enabled` | false | ⚖️ EAA · ADA (WCAG 2.1 AA) |
| **Reduce motion** (уменьшить анимации) | `reduce_motion_enabled` | false | ⚖️ EAA · ADA |
| **Captions / Subtitles** | `captions_enabled` | **true** (включены по умолчанию) | ⚖️ EAA Art.13 |
| **Screen reader support** | `screen_reader_hint` | — | ⚖️ EAA · ADA |
| **Color blind mode** | `color_blind_mode` | none | ⚖️ EAA · ADA |
| **Contact DPO / Privacy Officer** | — (кнопка-ссылка) | — | ⚖️ Quebec L25 · GDPR Art.37 |

**Блокеры публикации:**
- 🔴 Раздел Accessibility обязателен (EAA с 28 июня 2025 · ADA · App Store §2.5.4 · Google Play)
- 🔴 `captions_enabled = true` по умолчанию — охватывает видео приложения (UGC субтитры не требуются)

---

### 9️⃣ ❓ HELP & SUPPORT

**Путь:** Settings → Help & Support  
**Правовое основание:** ⚖️ App Store (обязательная ссылка на поддержку) · DSA Art.14/17 · GDPR

**Что включает:**

| Пункт | UI-название | ⚖️ | Закон |
|---|---|---|---|
| Помощь / FAQ | Help Center / FAQ | ⚖️ | App Store — обязательна ссылка на поддержку |
| Написать в поддержку | Contact Support | ⚖️ | App Store · DSA Art.17 |
| Политика конфиденциальности | Privacy Policy | ⚖️ | GDPR Art.13 · App Store · Google Play |
| Условия использования | Terms of Service | ⚖️ | App Store · Google Play |
| Политика cookies | Cookie Policy | ⚖️ | ePrivacy · GDPR |
| Пожаловаться на контент | Report a problem | ⚖️ | DSA Art.16/17 |
| Child Safety | Child Safety | ⚖️ | Google Play Child Safety Standards 🔴 |
| Лицензии / open source | Open Source Licenses | 💡 | — |
| Версия приложения | App version | 💡 | — |

**Блокеры публикации:**
- 🔴 **Child Safety** раздел с email `childsafety@bestme.com` (Google Play Child Safety Standards)
- 🔴 Ссылки на Privacy Policy и Terms of Service (App Store · Google Play — обязательно)
- 🔴 Механизм **Report a problem** (DSA Art.16/17)

---

## Полная ASCII-структура всех 9 разделов

```
⚙️ Settings
│
├── 1️⃣  👤  Account  ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17
│   ├── User Info
│   │   ├── Avatar (upload / delete)
│   │   ├── Status  ← отображается на аватарке
│   │   ├── Cover image
│   │   ├── First name  [❌ не меняется]  ⚖️ GDPR Art.17
│   │   ├── Last name
│   │   ├── Date of birth  ⚖️ COPPA · GDPR Art.8
│   │   ├── Gender
│   │   └── Interests  (6 категорий: Sport / Nutrition / Environment /
│   │                                Aesthetics & Hygiene / Mental Health / Daily Routine)
│   ├── Profile Info
│   │   ├── Bio / About
│   │   ├── Goals
│   │   └── Language
│   ├── Contact Info  ⚖️ GDPR Art.5
│   │   ├── Email  [обязательный]
│   │   ├── Phone  [необязательный]  ⚖️ TCPA
│   │   ├── Location / Country
│   │   ├── Address  ⚖️ GDPR Art.9
│   │   ├── Personal link
│   │   ├── Blog link
│   │   └── Business link  ← внешний URL (≠ Switch to Business profile)
│   └── Account Management  ⚖️ GDPR Art.17
│       ├── Deactivate account  🔴
│       ├── Delete account  🔴 App Store · Google Play
│       ├── Switch to Business profile
│       └── Create Business account
│
├── 2️⃣  🔒  Privacy & Visibility  ⚖️ GDPR Art.25
│   ├── Account Privacy  (Private / Search / SEO / Relationship)
│   ├── Profile Visibility  (Name / Avatar / Cover / Bio / Status / Birthday / Gender / Interests / Goals)
│   ├── Contact Info Privacy  (Email / Phone / Location / Address / Links)
│   ├── Content Visibility  (Posts / Gallery / Friends list / Subscriptions / Discussions / Saves)
│   ├── Interactions  (Messages / Tags / Comments / Reactions / Shares / Online status / Last seen)
│   ├── Discoverability  (Search / SEO / Recommendations)
│   └── Safety & Blocked Accounts  🔴 DSA Art.16
│       ├── Blocked users list
│       ├── Restricted list
│       ├── Report user  🔴 DSA Art.16
│       └── Report content  🔴 DSA Art.16
│
├── 3️⃣  🛡️  Login & Security  ⚖️ GDPR Art.32 · App Store §5.1.3
│   ├── Change password
│   ├── Two-factor authentication (2FA)
│   ├── Sign in with Apple / Google / Facebook
│   ├── Disconnect 3rd-party  🔴 App Store §5.1.1(v)
│   ├── Active sessions
│   └── Login history
│
├── 4️⃣  🔔  Notifications  ⚖️ GDPR Art.6/7 · CASL · CAN-SPAM · TCPA
│   ├── Push notifications
│   ├── Email notifications
│   ├── SMS notifications  ⚖️ TCPA
│   ├── Messages
│   ├── Friends & requests
│   ├── Reactions & comments
│   ├── Feed recommendations
│   ├── Discussions & community
│   └── System & security
│
├── 5️⃣  👥  Friends & Community  💡 UX-норма соцсети · ⚖️ GDPR Art.25
│   ├── My Friends
│   ├── Friend Requests
│   ├── Subscribed Blogs
│   ├── My Blog  (только 1 собственный)
│   ├── Subscribed Communities
│   ├── My Communities  (создать можно неограниченно)
│   └── Followed Business Profiles
│
├── 6️⃣  📝  Content  ⚖️ DSA Art.14 · GDPR Art.25
│   ├── Saved  (Bookmarks)
│   ├── My Posts
│   ├── Sharing settings
│   ├── Feed preferences
│   ├── Discussions
│   ├── Community Guidelines (UGC ToS)  🔴 Google Play · App Store
│   └── Archive
│
├── 7️⃣  📦  Your Data  ⚖️ GDPR Art.15–22 · CCPA · PIPEDA · Quebec L25 · Israel PPL
│   ├── Download my data  🔴 GDPR Art.15
│   ├── See what we know
│   ├── Correct my data  ⚖️ GDPR Art.16
│   ├── Restrict processing  ⚖️ GDPR Art.18
│   ├── Do Not Sell My Personal Information  🔴 CCPA §1798.120
│   ├── Consent history
│   ├── Delete my data  ⚖️ GDPR Art.17
│   └── Contact our DPO  ⚖️ Quebec L25 · GDPR Art.37
│
├── 8️⃣  ♿  Accessibility  ⚖️ EAA 2019/882 · ADA · Israel · AODA · CA Unruh · App Store · Google Play
│   ├── Text size
│   ├── Bold text
│   ├── High contrast mode  ⚖️ WCAG 2.1 AA
│   ├── Reduce motion
│   ├── Captions / Subtitles  [ON по умолчанию]  🔴 EAA
│   ├── Screen reader support
│   ├── Color blind mode
│   └── Contact DPO  ⚖️ Quebec L25 · GDPR Art.37
│
└── 9️⃣  ❓  Help & Support  ⚖️ App Store · DSA Art.14/17 · GDPR
    ├── Help Center / FAQ  🔴 App Store
    ├── Contact Support  🔴 App Store · DSA Art.17
    ├── Privacy Policy  🔴 GDPR Art.13 · App Store · Google Play
    ├── Terms of Service  🔴 App Store · Google Play
    ├── Cookie Policy  ⚖️ ePrivacy
    ├── Report a problem  🔴 DSA Art.16/17
    ├── Child Safety  🔴 Google Play Child Safety Standards
    ├── Open Source Licenses
    └── App version
```

---

## Таблица разделов — документы и правовые основания

| # | Раздел | UI-иконка | Закон / Правила | Документ ТЗ |
|---|---|---|---|---|
| 1 | **Account** | 👤 | App Store §5.1.1 · Google Play · GDPR Art.17 | [AccountSpec.md](AccountSpec.md) |
| 2 | **Privacy & Visibility** | 🔒 | GDPR Art.25 · DSA Art.14 · ePrivacy · Israel PPL | [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md) |
| 3 | **Login & Security** | 🛡️ | GDPR Art.32 · App Store §5.1.3 | [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md) |
| 4 | **Notifications** | 🔔 | GDPR Art.6/7 · App Store · Google Play · CASL · CAN-SPAM · TCPA | [NotificationsSpec.md](NotificationsSpec.md) |
| 5 | **Friends & Community** | 👥 | GDPR Art.25 · DSA Art.14 | *(этот документ, §5)* |
| 6 | **Content** | 📝 | DSA Art.14 · GDPR Art.25 · Google Play UGC · App Store §1.2 | [ProfileSettingsFullSpec.md](ProfileSettingsFullSpec.md) |
| 7 | **Your Data** | 📦 | GDPR Art.15–22 · CCPA §1798.100–120 · PIPEDA · Quebec L25 · Israel PPL | [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md) |
| 8 | **Accessibility** | ♿ | EAA 2019/882 · ADA · Israel Disability Law · AODA · CA Unruh · App Store §2.5.4 · Google Play | [AccessibilitySpec.md](AccessibilitySpec.md) |
| 9 | **Help & Support** | ❓ | App Store · Google Play · DSA Art.14/17 · GDPR Art.13 | *(этот документ, §9)* |

---

## Сводная таблица блокеров публикации (все разделы)

> 🔴 **Эти пункты должны быть реализованы ДО первой публикации в App Store и Google Play.**

| # | Раздел | Что обязательно | Закон |
|---|---|---|---|
| 1 | Account | **Delete account** кнопка в Settings → Account → Account Management | App Store §5.1.1(v) · Google Play |
| 2 | Account | **Веб-форма** `bestme.app/account/delete` | Google Play |
| 3 | Privacy | **`seo_indexable = false`** строго по умолчанию | GDPR Art.25 |
| 4 | Privacy | **Report user** на каждом профиле | DSA Art.16 |
| 5 | Privacy | **Report content** на каждом посте/фото/комменте | DSA Art.16 |
| 6 | Login & Security | **Disconnect** для каждого 3rd-party login | App Store §5.1.1(v) |
| 7 | Login & Security | **Sign in with Apple** (если есть другие 3rd-party) | App Store §5.1.3 |
| 8 | Notifications | **Pre-checked = пустые** для email/SMS opt-in | CASL · ePrivacy |
| 9 | Notifications | **SMS consent checkbox** при добавлении телефона | TCPA |
| 10 | Content | **UGC ToS acceptance** при первом создании контента | Google Play · App Store §1.2 |
| 11 | Content | **ATT prompt** на iOS (если используется IDFA) | App Store §5.1.2 |
| 12 | Content | **Prominent Disclosure** перед запросом разрешений | Google Play · App Store |
| 13 | Your Data | **Do Not Sell My Personal Information** кнопка | CCPA §1798.120 |
| 14 | Your Data | **Download my data** / GDPR export | GDPR Art.15 |
| 15 | Accessibility | **Раздел Accessibility** в Settings | EAA 2019/882 (с 28.06.2025) · ADA · App Store §2.5.4 |
| 16 | Accessibility | **`captions_enabled = true`** по умолчанию | EAA Art.13 |
| 17 | Help & Support | **Privacy Policy** и **Terms of Service** ссылки | App Store · Google Play · GDPR Art.13 |
| 18 | Help & Support | **Child Safety** раздел с childsafety@ email | Google Play Child Safety Standards |
| 19 | Help & Support | **Contact Support** / Report a problem | App Store · DSA Art.17 |

---

## Что добавлено в SettingsOverview.md v1.0

> 📋 **Для разработчиков:** это первая версия мастер-документа.

### ✅ ЧТО ДОБАВЛЕНО / УТОЧНЕНО

| # | Что | Куда | Причина |
|---|---|---|---|
| 1 | **Friends & Community полностью расписан** | §5 Friends & Community | Раздел существовал, но не был описан. Добавлены: My Blog (только 1), Subscribed Blogs (неограниченно), My Communities (неограниченно), Subscribed Communities (неограниченно), Followed Business Profiles (с комментариями и рейтингом). |
| 2 | **Content раздел** | §6 Content | Уточнены типы контента: посты, шеринг, сохранение, лента (Feed с алгоритмом), дискуссии по категориям (публичные обсуждения по Interests). |
| 3 | **Дискуссии по категориям** | §6 Content | Тематические страницы дискуссий: пользователи открывают публичное обсуждение, делятся вопросами, отвечают. Контент отбирается алгоритмом по категории (Interests). |
| 4 | **Бизнес-профили в Friends & Community** | §5 Friends & Community | Followed Business Profiles: пользователь может подписаться на бизнес-профили, оставить комментарий и рейтинг. |
| 5 | **Алгоритм ленты** | §6 Content → Feed preferences | Feed personalization: алгоритм подбирает наиболее актуальный контент по Interests пользователя. |
| 6 | **Сводная таблица 19 блокеров** | Конец документа | Все критичные требования всех 9 разделов в одном месте. |
| 7 | **Таблица разделов с документами** | Перед ASCII-структурой | Ссылки на все spec-файлы для быстрой навигации. |

---

*SettingsOverview.md v1.0 · Bestme · март 2026*  
*Документы по разделам: [AccountSpec.md](AccountSpec.md) · [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md) · [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md) · [NotificationsSpec.md](NotificationsSpec.md) · [AccessibilitySpec.md](AccessibilitySpec.md) · [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md) · [ProfileSettingsFullSpec.md](ProfileSettingsFullSpec.md)*
