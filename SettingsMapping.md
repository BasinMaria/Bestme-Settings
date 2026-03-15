# Bestme — Settings Structure & Law Mapping
> Полная структура настроек **личного профиля** (бизнес-профиль — отдельный документ).  
> Уровни: L1 = главный экран настроек · L2 = подраздел · L3 = конкретный пункт.  
> Маппинг дизайнерских экранов к вкладкам.  
> ⚖️ = по закону обязательно · ✅ = Privacy by Default · 📱 = требование App Store

> **Диаграмма v2:** `PersonalProfileSettings.drawio.html` — полная 3-уровневая иерархия L1→L2→L3 (260 cells, 9 L1, 46 L2, 182 L3)  
> **Полная спецификация полей:** `PrivacyFieldsSpec.md` — все 35 privacy-полей с variable names, defaults, visibility matrix, legal

---

## Обзор: 9 вкладок (L1 главного экрана)

| # | Вкладка (L1) | Что внутри (кратко) | Почему / Закон |
|---|---|---|---|
| 1️⃣ | **👤 Account** | Avatar, bio, about, status, goal, birthday, gender, contacts, links, interests | Identity |
| 2️⃣ | **👥 Friends** | Friends management, people you may know, recommendations opt-out | GDPR Art.22 |
| 3️⃣ | **🔒 Privacy** | Account Privacy, Contact Info, Content Visibility, Interactions, Discoverability, Activity, Blocked | GDPR Art.25 |
| 4️⃣ | **🔐 Login & Security** | Password, 2FA, sessions, login activity, authorized apps | GDPR + App Store |
| 5️⃣ | **🔔 Notifications** | Push, email (+ In-App settings), quiet hours | CAN-SPAM / CASL |
| 6️⃣ | **📝 Content** | Feed, post defaults, sensitive content, blog, muted keywords, autoplay | GDPR Art.22/25 |
| 7️⃣ | **📊 Your Data** | Download/view/correct/delete data, consents, app permissions | GDPR + CCPA + App Store |
| 8️⃣ | **♿ Accessibility** | Theme, language, motion, screen reader, storage | App Store required |
| 9️⃣ | **❓ Help & Support** | Help centre, report a problem, terms & privacy policy | EU DSA Art.16 + Stores |

---

## 1️⃣ Account — Аккаунт и профиль

| Пункт | Variable | Default | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|---|---|
| Аватар / Фото профиля | `avatar_visibility` | PUBLIC | Опционально | — |
| Обложка профиля | `cover_photo_visibility` | PUBLIC | Опционально | — |
| Полное имя | `name_visibility` | PUBLIC | Нужно для функции | ⚖️ GDPR — мин. имя+инициал всегда виден |
| @хендл / Username | — | — | Нужно для функции | — |
| Bio (биография) | `bio_visibility` | PUBLIC | Опционально | — |
| About Profile (о себе) | `about_visibility` | PUBLIC | Опционально | — |
| Status / Mood (статус) | `status_visibility` | **FRIENDS_ONLY** ✅ | Опционально | ⚖️ GDPR data minimization |
| Life Goal (жизненная цель) | `goal_visibility` | **FRIENDS_ONLY** ✅ | Опционально | ⚖️ GDPR Art.9 |
| Дата рождения | `birthday_visibility` | **PRIVATE** ✅ | **Обязательно** (age check) | ⚖️ GDPR Art.9, COPPA |
| Пол | `gender_visibility` | **PRIVATE** ✅ | Опционально | ⚖️ GDPR Art.9 — чувствительная категория |
| Местоположение / Город | `location_visibility` | **FRIENDS_ONLY** ✅ | Опционально | ⚖️ GDPR Art.9 — геоданные |
| Personal links (вебсайт) | `personal_links_visibility` | PUBLIC | Опционально | — |
| Social media links | `social_links_visibility` | PUBLIC | Опционально | — |
| Blog link | `show_blog_link` | PUBLIC | Опционально | — |
| Business link | `show_business_link` | **PRIVATE** ✅ | Опционально | ⚖️ GDPR Art.6 |
| Интересы / Категории | `categories_visibility` | **FRIENDS_ONLY** ✅ | Опционально | ⚖️ GDPR Art.9 |
| Переключение в бизнес-профиль | — | — | Опционально | — |

---

## 2️⃣ Friends — Друзья и сообщество

> **Из дизайнерского экрана:** Friends & Community → Friends management

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Friends list (список друзей) | Нужно для функции | — |
| Add friends (добавить) | Нужно для функции | — |
| Remove friends (удалить) | **Обязательно** | ⚖️ GDPR — право прекратить связь |
| Friend requests (заявки) | Нужно для функции | — |
| Friend suggestions (People you may know) | Опционально | — |
| Opt-out от рекомендаций | **Обязательно** | ⚖️ GDPR Art.22 — право отказаться от алгоритмических решений |

---

## 3️⃣ Privacy — Приватность и видимость ⚖️

> **Все 4 дизайнерских экрана + новый Discoverability ↓**

### 📌 Account Privacy (Экран 1 дизайна)

| Пункт | Variable | Default | Опции | По закону ⚖️ |
|---|---|---|---|---|
| Profile page | `profile_visibility` | PUBLIC | Public / Friends / **Private** ✅ | ⚖️ GDPR Art.15 — мин. имя+аватар видны |
| Full name | `name_visibility` | PUBLIC | Public / Friends / Private | ⚖️ GDPR — мин. имя+инициал всегда виден |
| Avatar | `avatar_visibility` | PUBLIC | Public / Friends / Private | — |
| Cover photo | `cover_photo_visibility` | PUBLIC | Public / Friends / Private | — |
| Bio | `bio_visibility` | PUBLIC | Public / Friends / Private | — |
| About Profile | `about_visibility` | PUBLIC | Public / Friends / Private | — |
| Status / Mood | `status_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR data minimization; авто-истечение 24ч |
| Life Goal | `goal_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 |
| Birthday | `birthday_visibility` | **PRIVATE** ✅ | PUBLIC_FULL / PUBLIC_AGE / FRIENDS_FULL / FRIENDS_AGE / **PRIVATE** | ⚖️ GDPR Art.9, COPPA |
| Gender | `gender_visibility` | **PRIVATE** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 — чувствительная категория |

### 📌 Contact Info Privacy (Экран 2 дизайна)

| Пункт | Variable | Default | Опции в UI | По закону ⚖️ |
|---|---|---|---|---|
| Email | `email_visibility` | **PRIVATE** ✅ | Friends / **Private** (PUBLIC запрещён!) | ⚖️ GDPR+CAN-SPAM+CASL |
| Phone | `phone_visibility` | **PRIVATE** ✅ | Friends / **Private** (PUBLIC запрещён!) | ⚖️ GDPR+TCPA+PIPEDA |
| Location / City | `location_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 — геоданные |
| Address | — | PRIVATE | Private only | ⚖️ GDPR Art.5 |
| Personal links | `personal_links_visibility` | PUBLIC | Public / Friends / Private | — |
| Social media links | `social_links_visibility` | PUBLIC | Public / Friends / Private | — |
| Blog link | `show_blog_link` | PUBLIC | Public / Friends / Private | — |
| Business link | `show_business_link` | **PRIVATE** ✅ | Public / Friends / Private | ⚖️ GDPR Art.6 |

### 📌 Interactions (Экран 3 дизайна) + дополнения

| Пункт | Variable | Default | Опции | По закону ⚖️ |
|---|---|---|---|---|
| Who can message | `who_can_message` | **FRIENDS_ONLY** ✅ | Everyone / FoF / Friends / Nobody | ⚖️ ePrivacy+GDPR — нежелательные сообщения |
| Who can send friend request | `who_can_send_friend_request` | EVERYONE | Everyone / FoF / Nobody | — |
| Who can tag me | `who_can_tag` | **FRIENDS_ONLY** ✅ | Everyone / Friends / Nobody | ⚖️ GDPR Art.4/9 — биометрия |
| Tag approval | `tag_approval_required` | false | true (manual) / false (auto) | ⚖️ GDPR Art.7/9 — рекомендуется если `who_can_tag=EVERYONE` |
| Who can comment | `who_can_comment` | EVERYONE | Everyone / FoF / Friends / Nobody | ⚖️ EU DSA Art.14 |
| Comment moderation | `comment_moderation` | AUTO_FILTER | Disabled / **Auto-filter** ✅ / Manual | ⚖️ EU DSA Art.14 |
| Who can share/repost | `who_can_share` | **FRIENDS_ONLY** ✅ | Everyone / Friends / Nobody | — |

### 📌 Content Visibility (Экран 4 дизайна)

| Пункт | Variable | Default | Опции | По закону ⚖️ |
|---|---|---|---|---|
| Default post visibility | `default_post_visibility` | PUBLIC | Public / Friends / Private | ⚖️ GDPR Art.25 — per-post override обязателен |
| Media gallery | `media_gallery_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 — биометрия, дети |
| Friends list | `friends_list_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ Mutual friends ОБЯЗАНЫ быть видимы |
| Interest categories | `categories_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 |
| Subscribed blogs | `subscribed_blogs_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 |
| Subscribed communities | `subscribed_communities_visibility` | **FRIENDS_ONLY** ✅ | Public / Friends / Private | ⚖️ GDPR Art.9 |

### 📌 Discoverability (НОВЫЙ — требуется по GDPR)

| Пункт | Variable | Default | Опции | По закону ⚖️ |
|---|---|---|---|---|
| Profile in search results | `profile_searchable` | EVERYONE | Everyone / FoF / **Nobody** | ⚖️ GDPR Art.17 — право на забвение |
| SEO indexing | `seo_indexable` | **false** ✅ | On / **Off** | ⚖️ GDPR Art.25 — выключен по умолчанию |
| Content recommendations opt-out | `recommendations_opt_out` | false (on) | On / Off (opt-out) | ⚖️ GDPR Art.22 — право отказа от алгоритма |

### 📌 Activity Status

| Пункт | Variable | Default | Опции | По закону ⚖️ |
|---|---|---|---|---|
| Online / active status | `show_online_status` | **FRIENDS_ONLY** ✅ | Everyone / Friends / Nobody | ⚖️ GDPR Art.9 — поведенческие данные |
| Last seen | `show_last_seen` | **FRIENDS_ONLY** ✅ | Everyone / Friends / Nobody | ⚖️ GDPR Art.9 |
| Read receipts | — | on | On / Off | — |
| Typing indicators | — | on | On / Off | — |

---

## 3️⃣ Login & Security ⚖️ — Безопасность и вход

> **Название в соц сетях:** "Login & Security" (Facebook, Instagram, Bestme из дизайна)  
> **Что это:** Всё связанное с безопасностью аккаунта — пароль, 2FA, сессии, история входов, сторонние приложения.  
> **Из дизайнерского экрана (9ec16a4a):** Change password · Two-Factor Authentication · Active sessions · Login activity · Authorized apps

### 📌 Дизайнерский экран: Login & Security (из Account settings)

**L2: Change Password**

| L3 пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Current password (верификация) | **Обязательно** | ⚖️ GDPR Art.32 |
| New password (min 8 chars) | **Обязательно** | ⚖️ GDPR Art.32 |
| Confirm new password | **Обязательно** | — |
| Email-уведомление о смене пароля | **Обязательно** | ⚖️ GDPR Art.33 |

**L2: Two-Factor Authentication (2FA)**

| L3 пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Authenticator app (TOTP — Google Auth, Authy) | Настоятельно рекомендуется | ⚖️ GDPR Art.32 |
| SMS verification (резервный метод) | Настоятельно рекомендуется | ⚖️ GDPR Art.32 |
| Backup codes (10 одноразовых кодов) | Нужно для функции | — |
| Trusted devices (не спрашивать 30 дней) | Опционально | — |

**L2: Active Sessions** *(называется "Where You're Logged In" в Facebook)*

| L3 пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Список устройств (тип, ОС, локация, время входа) | **Обязательно** | ⚖️ GDPR Art.32 |
| Выйти с выбранного устройства | **Обязательно** | ⚖️ GDPR Art.32 |
| Выйти со всех устройств ⚠️ | **Обязательно** | ⚖️ GDPR Art.32 |

**L2: Login Activity** *(называется "Security Log" / "Login Activity" в Facebook/LinkedIn)*

| L3 пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| История входов (дата, устройство, локация) | Нужно для функции | ⚖️ GDPR Art.30 |
| Оповещения о подозрительном входе | **Обязательно** | ⚖️ GDPR Art.33 |

**L2: Authorized Apps** *(называется "Apps and Websites" в Facebook, "Connected Apps" в Twitter)*

| L3 пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Список подключённых приложений | **Обязательно** | ⚖️ GDPR Art.7 |
| Отозвать доступ (Revoke access) | **Обязательно** | ⚖️ GDPR Art.7 — право отозвать согласие |

### Дополнительно в Login & Security (не в дизайне, но нужно по закону / стандарту)

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Sign in with Apple | **Обязательно** (если есть Google/FB-вход) | 📱 App Store — обязательное требование |
| Sign in with Google / Disconnect | **Обязательно** (revoke) | ⚖️ GDPR Art.7 |
| Изменить email адрес | **Обязательно** | ⚖️ GDPR Art.32 |
| Изменить номер телефона | Нужно для функции | — |
| Email-оповещения безопасности (always on) | **Обязательно** | ⚖️ GDPR Art.33/34 |

---

## 4️⃣ Data & Privacy ⚖️ — Данные и права

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Скачать мои данные | **Обязательно** | ⚖️ GDPR Art.20 — право на портируемость |
| Просмотреть мои данные | **Обязательно** | ⚖️ GDPR Art.15 — право доступа |
| Исправить данные | **Обязательно** | ⚖️ GDPR Art.16 — право на исправление |
| 🗑️ Удалить аккаунт | **Обязательно** | ⚖️ GDPR Art.17 — право на удаление |
| Деактивировать профиль | Опционально | — |
| Согласие на аналитику | **Обязательно** (opt-in) | ⚖️ GDPR — только с явного согласия |
| Согласие на рекламу | **Обязательно** (opt-in) | ⚖️ GDPR — только с явного согласия |
| Cookie-настройки | **Обязательно** для ЕС | ⚖️ ePrivacy / GDPR |
| Не продавать мои данные | **Обязательно** для США/CA | ⚖️ CCPA |
| Разрешения приложения (геолокация, камера, контакты) | **Обязательно** | 📱 App Store / Google Play |

---

## 5️⃣ Notifications — Уведомления

> **Из дизайнерского экрана (6d404521):** 3 вкладки — Push notifications / Email notifications / In-App settings

### Push Notifications (из дизайна)

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Enable push notifications  (toggle) | **Обязательно** (системный диалог iOS/Android) | 📱 App Store / Google Play |
| Likes and Reactions | Опционально | — |
| Comments | Опционально | — |
| New followers | Опционально | — |
| Messages | Опционально | — |
| Mentions and tags | Опционально | — |
| Friend requests | Опционально | — |
| Live videos | Опционально | — |
| Security & account alerts | **Обязательно (always on)** | ⚖️ GDPR Art.33 |

### Email Notifications (из дизайна)

| Пункт | Default | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|---|
| Activity summary | Weekly | Опционально (opt-in) | ⚖️ CAN-SPAM / CASL |
| Reminder emails | On | Опционально | — |
| Product updates | On | Опционально | — |
| Newsletter | **Off** ✅ | Нужно с явным opt-in | ⚖️ CAN-SPAM / CASL |
| Security alerts | **On (always)** | **Обязательно** | ⚖️ GDPR Art.33 |
| Unsubscribe link в каждом письме | — | **Обязательно** | ⚖️ CAN-SPAM |

### In-App Settings (из дизайна)

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Sound | Опционально | — |
| Vibration | Опционально | — |
| Badge count | Опционально | — |

### Quiet Hours (дополнение к дизайну)

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Enable quiet hours | Опционально | — |
| From / To (time picker) | Опционально | — |
| Allow urgent security alerts (always on) | **Обязательно** | ⚖️ GDPR Art.33 |

---

## 6️⃣ Content & Blog — Контент и блог

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Аудитория постов по умолчанию | **Обязательно** | ⚖️ GDPR Art.25 — Privacy by Default |
| Алгоритм ленты (хронологически / рекомендации) | Нужно с opt-out | ⚖️ GDPR Art.22 — право отказа от алгоритма |
| Фильтр чувствительного контента | **Обязательно** | 📱 App Store / Google Play — для 17+ |
| Разрешить репосты моих публикаций | Опционально | — |
| Настройки блога (заголовок, описание, URL) | Нужно для функции | — |
| Сайт / Страница | Нужно для функции | — |
| Медиа (качество загрузки, авто-теги) | Опционально | — |
| Геолокация в постах | Опционально (выкл по умолчанию) | ⚖️ GDPR — геоданные |
| Модерация комментариев | Нужно для функции | — |
| Заглушённые ключевые слова | Опционально | — |
| Фильтр языка контента | Опционально | — |
| Автовоспроизведение видео | Опционально | — |

---

## 7️⃣ Business Profile 💼 — Бизнес-профиль

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Создать / переключиться на бизнес-профиль | Опционально | — |
| Название и категория бизнеса | Нужно для функции | ⚖️ Торговое право |
| Юридический адрес | **Обязательно** | ⚖️ EU DSA / местное законодательство |
| Верификация бизнеса | **Обязательно** для ЕС | ⚖️ EU DSA Art.13 |
| Аналитика | Опционально | — |
| Монетизация / IAP | **Обязательно** через Apple/Google если есть | 📱 App Store / Google Play — 30% комиссия |
| Рекламные инструменты | Опционально | — |

---

## 8️⃣ App Preferences — Настройки приложения

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Тема (светлая / тёмная / авто) | Опционально | — |
| Язык / Регион / Формат даты | Нужно для функции | — |
| Доступность (VoiceOver, Dynamic Type, контрастность) | **Обязательно** | 📱 App Store — обязательное требование |
| Кэш / Управление хранилищем | Опционально | — |
| Разрешения (push, геолокация, камера, контакты) | **Обязательно** | 📱 App Store / Google Play |

---

## 9️⃣ Help & Legal ⚖️ — Помощь и правовые документы

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Центр помощи / Связь с поддержкой | Нужно для функции | — |
| Пожаловаться на нарушение / контент | **Обязательно** | ⚖️ EU DSA Art.16 |
| Политика конфиденциальности | **Обязательно** | ⚖️ GDPR + App Store + Google Play |
| Условия использования | **Обязательно** | 📱 App Store + Google Play |
| Cookie Policy | **Обязательно** для ЕС | ⚖️ ePrivacy |
| App Tracking Transparency (ATT) | **Обязательно** | 📱 Apple — с iOS 14.5 |
| Google Play Data Safety | **Обязательно** | 🔴 Google Play |
| Лицензии open-source | Нужно | 📱 App Store |
| Версия приложения | Нужно для поддержки | — |
| Оценить приложение | Опционально | — |

---

## Итого по закону — обязательные пункты

| Закон / Требование | Что обязательно реализовать |
|---|---|
| **GDPR Art.6/7** | Согласие на обработку, право отозвать |
| **GDPR Art.8** | Верификация возраста (13+ / 16+) |
| **GDPR Art.13/14** | Privacy Policy при регистрации |
| **GDPR Art.15/16** | Доступ и исправление своих данных |
| **GDPR Art.17** | Кнопка "Удалить аккаунт" |
| **GDPR Art.20** | Скачать свои данные |
| **GDPR Art.22** | Opt-out от алгоритмической ленты |
| **GDPR Art.25** | Privacy by Default (закрытый профиль по умолчанию) |
| **GDPR Art.32** | 2FA, сессии, защита данных |
| **GDPR Art.33/34** | Email при взломе аккаунта |
| **CCPA** | "Do Not Sell My Data" |
| **CAN-SPAM / CASL** | Opt-in на email + кнопка отписки |
| **ePrivacy** | Cookie-согласие |
| **EU DSA Art.13/16** | Верификация бизнеса + механизм жалоб |
| **Apple App Store** | Sign in with Apple, ATT-диалог, Accessibility, IAP через Apple |
| **Google Play** | Data Safety декларация |

---

## 🗂️ L1 → L2 → L3: Полная 3-уровневая иерархия личного профиля

> Именно так называются экраны в соц сетях (Instagram / Facebook / Twitter / TikTok).  
> Полная интерактивная диаграмма: **`PersonalProfileSettings.drawio.html`**

### L1: Главный экран Settings — что видит пользователь

| # | L1 (главный экран) | Подзаголовок (subtitle) | Как в других соц сетях |
|---|---|---|---|
| 1 | 👤 **Account** | Manage your profile & account | Account — Instagram, Twitter |
| 2 | 🔒 **Privacy** | Control who sees your content | Privacy — Instagram, TikTok, Facebook |
| 3 | 🔐 **Login & Security** | Password, 2FA, sessions | Login & Security — Facebook, Instagram |
| 4 | 🔔 **Notifications** | Manage your alerts | Notifications — все соц сети |
| 5 | 📝 **Content** | Feed, posts, blog settings | Content Preferences — Twitter, TikTok |
| 6 | 📊 **Your Data** | Access, download, delete | Your Information — Facebook; Data & Privacy — Instagram |
| 7 | ♿ **Accessibility** | Display, language, accessibility | Accessibility — App Store required |
| 8 | ❓ **Help & Support** | Get help, report a problem | Help & Support — все соц сети |
| 9 | 📋 **About** | App info, legal documents | About — все соц сети |
| — | 🚪 **Log Out** | Sign out (красная кнопка) | Log Out — все |
| — | 🗑️ **Delete Account** | Permanent deletion ⚖️ | Delete Account / Deactivate — все |

---

### L2: Подразделы каждой L1-вкладки

#### 👤 Account → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| ✏️ Edit Profile | Avatar, cover, name, @handle, bio, status, birthday, gender, pronouns, location | Edit Profile — Instagram, Twitter |
| 📞 Contact Information | Email (verified), phone, address | Contact Info — Facebook |
| 🔗 Personal Links | Website, social links, blog link | Links — Instagram |
| 🎯 Interests & Goals | Categories (up to 10), life goal | Interests — TikTok, Pinterest |
| 🔄 Profile Type | Switch to Business Profile | Account type — Instagram |

#### 🔒 Privacy → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 🛡️ Account Privacy | Profile page, name, avatar, cover, bio, birthday, gender, interests — Public/Friends/Private | Account Privacy — Instagram |
| 📞 Contact Info Privacy | Email (Private only⚖️), phone, location, address, links | Contact Info Privacy — из дизайна Bestme |
| 💬 Interactions | Who can message, tag, comment, share, send requests | Interactions — из дизайна Bestme |
| 👁️ Content Visibility | Default posts, media, friends list, categories, blogs, communities | Content Visibility — из дизайна Bestme |
| ⚡ Activity Status | Online status, last seen, read receipts, typing | Activity Status — Telegram, WhatsApp |
| 🚫 Blocked Accounts | Blocked, restricted, muted users | Blocking — Instagram, Twitter |

#### 🔐 Login & Security → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 🔑 Change Password | Current + new password + email notification | Change Password — все |
| 🛡️ Two-Factor Authentication | Authenticator app, SMS, backup codes | 2-Step Verification — Google; 2FA — Twitter |
| 📱 Active Sessions | Device list, log out from device/all | Where You're Logged In — Facebook |
| 📋 Login Activity | Login history log, security alerts | Login Activity — Facebook |
| 🔌 Authorized Apps | Third-party apps list, revoke access ⚖️ | Apps and Websites — Facebook |
| 🔗 Connected Accounts | Sign in with Apple⚖️📱, Google, connect/disconnect | Linked Accounts — Instagram |
| 📧 Change Email/Phone | Verify new email flow | Account Settings — Twitter |

#### 🔔 Notifications → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 📲 Push Notifications | Messages, requests, tags, likes, comments, followers, blogs, communities, security⚖️ | Push Notifications — все |
| 📧 Email Notifications | Digest, newsletter(opt-in⚖️), security alerts(always on⚖️) | Email — все |
| 🔕 Quiet Hours | Schedule from/to, urgent exceptions | Focus / DND — Instagram, TikTok |
| 🔊 Sound & Vibration | Sound on/off, vibration, badge count | Sounds — Telegram, WhatsApp |

#### 📝 Content → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 📰 Feed Settings | Algorithm: Recommended/Chronological⚖️, show from, language | Feed — Twitter, TikTok |
| ✍️ Post Defaults | Default audience⚖️, location off✅, comments, sharing | Sharing defaults — Facebook |
| ⚠️ Sensitive Content | Filter graphic/adult content📱, safe search | Sensitive Content — Instagram, Twitter |
| 📖 Blog Settings | Title, description, URL slug, visibility | Blog — Substack, Medium |
| 🔇 Muted Keywords | Add keywords/hashtags, duration | Muted Words — Twitter |
| ▶️ Autoplay | Videos on WiFi/always/never, sound off✅ | Autoplay — Instagram, YouTube |

#### 📊 Your Data → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| ⬇️ Download Your Data | Request export, JSON/HTML, email link ⚖️ GDPR Art.20 | Download Your Information — Facebook |
| 👁️ View Your Data | Posts, comments, login history ⚖️ GDPR Art.15 | Access Your Data — Google |
| ✏️ Correct Your Data | Correction request ⚖️ GDPR Art.16 | — |
| ✅ Consents & Analytics | Analytics opt-in, ads opt-in, cookies⚖️, Do Not Sell⚖️ CCPA | Ad Preferences — Facebook |
| 📱 App Permissions | Notifications, camera, mic, photos, contacts (opt-in!), location (off✅) | Permissions — iOS/Android |
| ⏸️ Deactivate Account | Temporarily hide profile | Deactivate — Instagram, Facebook |
| 🗑️ Delete Account | Permanent deletion ⚖️ GDPR Art.17, 30-day grace | Delete Account — все |

#### ♿ Accessibility → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 🎨 Display & Appearance | Theme (light/dark/system), text size📱, bold, contrast | Display — Twitter, Instagram |
| 🌍 Language & Region | Language, region, date format, units | Language — все |
| 🌀 Motion & Animation | Reduce motion, autoplay animations off | Reduce Motion — iOS |
| 🔊 Screen Reader Support | VoiceOver/TalkBack📱 (обязательно), accessibility labels | Accessibility — App Store required |
| 💾 Storage & Data | Clear cache, downloads, mobile data usage | Storage — Telegram, Instagram |

#### ❓ Help & Support → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 📚 Help Center | FAQ, knowledge base | Help Center — Instagram, Twitter |
| 💬 Contact Support | Open ticket, in-app chat | Contact Us — все |
| 🐛 Report a Problem | Bug report, feedback | Report a Problem — Apple |
| ⚠️ Report Content or User | Report harmful content⚖️ EU DSA Art.16, appeal⚖️ EU DSA Art.20 | Report — все (обязательно ЕС) |

#### 📋 About → L2
| L2 Подраздел | Что включает | Как в соц сетях |
|---|---|---|
| 📄 Legal Documents | Privacy Policy⚖️📱, Terms⚖️📱, Cookie Policy⚖️, Community Guidelines | About / Legal — все |
| 📡 Platform & Tracking | ATT⚖️📱 (Apple iOS 14.5+), Data Safety🔴 (Google Play), OSS licenses📱 | — (обязательно) |
| ℹ️ App Info | Version & build number, rate the app | About — все |
