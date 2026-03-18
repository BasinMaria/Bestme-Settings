# PrivacyVisibilitySpec.md — Полная спецификация: Account + Privacy & Visibility

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик  
**Статус:** 🔴 Часть блокирует публикацию (App Store + Google Play) · 🟡 Часть критична для GDPR

> **Этот документ** формализует структуру, описанную автором приложения, с дополнением переменных,
> дефолтов и правовых оснований. Смежные документы:
> [AccountDeletionSpec.md](AccountDeletionSpec.md), [AccountPrivacySpec.md](AccountPrivacySpec.md),
> [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md)

---

## Содержание

1. [Раздел 1: Account (Аккаунт)](#1-account)
2. [Раздел 2: Privacy & Visibility (Приватность и видимость)](#2-privacy--visibility)
   - [2.1 Account Privacy](#21-account-privacy)
   - [2.2 Contact Info Privacy](#22-contact-info-privacy)
   - [2.3 Content Visibility](#23-content-visibility)
   - [2.4 Interactions](#24-interactions)
3. [Карта пропущенных полей](#3-карта-пропущенных-полей)
4. [Вопрос: куда поместить Subscribed Communities?](#4-subscribed-communities)
5. [Итоговая ASCII-структура](#5-ascii-структура)

---

## 1. Account

**Путь в приложении:** Settings → Account  
**Правовое основание:** ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17

### 1.1 User Info — Информация пользователя

| Поле | variable_name | Тип | Редактируемость | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Avatar (фото профиля)** | `avatar_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **Cover image (обложка)** | `cover_image_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **First name (имя)** | `first_name` | Текст | ❌ **не меняется** после регистрации | ⚖️ | GDPR Art.17 |
| **Last name (фамилия)** | `last_name` | Текст | ✏️ (добавить если нет) | ⚖️ | GDPR Art.17 |
| **Date of birth** | `date_of_birth` | Дата | ❌ не меняется | ⚖️ | COPPA · GDPR Art.8 · DSA Art.28 |
| **Gender** | `gender` | ENUM: Male / Female / Other / Prefer not to say | ✏️ | 💡 | — |
| **Interests / Categories** | `interest_tags` | Multi-select (теги) | ✏️ | 💡 | — |

> ⚠️ **First name не редактируется:** под полем показать подсказку  
> _«Чтобы изменить имя, напишите в поддержку»_ — с прямой кнопкой «Написать в поддержку».  
> Это стандартная практика (как в Instagram, TikTok) для защиты от спуфинга.

### 1.2 Profile Info — Информация профиля

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Bio / About** | `bio` | Текст (≤ 300 символов) | пусто | 💡 | — |
| **Status** | `status_text` | Текст (≤ 80 символов) | пусто | 💡 | — |
| **Category** | `profile_category` | ENUM (список категорий: Creator, Athlete, Artist, Business…) | пусто | 💡 | — |
| **Language** | `app_language` | ENUM (список языков) | System locale | 💡 | — |

### 1.3 Contact Info — Контактная информация

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Email address** | `email` | Текст | обязательный | ⚖️ | GDPR Art.5 — минимизация |
| **Phone number** | `phone_number` | Текст | необязательный | ⚖️ | GDPR · TCPA |
| **Location / Country / Region** | `location_country` | ENUM (страны) | пусто | ⚖️ | GDPR — применимое право |
| **Address** | `address_text` | Текст | пусто | ⚖️ | GDPR — чувствительные данные |
| **Personal link (профильная ссылка)** | `profile_link_url` | URL | пусто | 💡 | — |
| **Business link** | `business_link_url` | URL | пусто | 💡 | — |

> ⚠️ Телефон не является обязательным при регистрации — это влияет на 2FA  
> (подробнее → [GDPRArt5SecuritySpec.md §1.1](GDPRArt5SecuritySpec.md))

### 1.4 Account Management — Управление аккаунтом

**Путь в приложении:** Settings → Account → Account Management

| Пункт | Тип | ⚖️ | Закон |
|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация) | ⚖️ | GDPR Art.17 |
| **Delete account** | Действие (постоянное удаление + 2-step confirmation) | ⚖️ | GDPR Art.17 · CCPA §1798.105 · **App Store §5.1.1(v)** · **Google Play** |
| **Switch to Business profile** | Действие (переключение на бизнес-режим) | 💡 | — |
| **Create Business account** | Действие (создать дополнительный бизнес-аккаунт) | 💡 | — |

> ⚠️ **App Store + Google Play**: кнопка Delete account должна быть доступна **прямо** из настроек.  
> Полный путь: **Settings → Account → Account Management → Delete account**  
> ⚠️ **Google Play** (дополнительно): веб-форма `bestme.app/account/delete` (отдельно от in-app)  
> Подробнее → [AccountDeletionSpec.md](AccountDeletionSpec.md)

---

## 2. Privacy & Visibility

**Путь в приложении:** Settings → Privacy & Visibility  
**Правовое основание:** ⚖️ GDPR Art.25 (Privacy by Default) · DSA Art.14 · ePrivacy · Israel PPL

> 📌 **Принцип Privacy by Default (GDPR Art.25):**  
> Все настройки по умолчанию должны быть максимально строгими.  
> Пользователь сам ослабляет ограничения — но не наоборот.

---

### 2.1 Account Privacy

**Путь:** Settings → Privacy & Visibility → Account Privacy

> Полный юридический анализ с возрастными развилками → [AccountPrivacySpec.md](AccountPrivacySpec.md)

| Настройка | variable_name | Тип | Default 18+ | Default 13–17 | ⚖️ | Закон |
|---|---|---|---|---|---|---|
| **Private account** | `account_private` | Toggle | `false` (открытый) | `true` (закрытый) | ⚖️ | GDPR Art.25 · **DSA Art.28(3)(g)** |
| **Profile in search results** | `profile_searchable` | Toggle | `true` | `true` | ⚖️ | GDPR Art.17 — право на забвение (opt-out доступен) |
| **SEO indexing** | `seo_indexable` | Toggle | **`false`** | **`false`** | ⚖️ | **GDPR Art.25 — СТРОГО OFF, нельзя делать ON по умолчанию** |
| **Activity status (online)** | `online_status_visible` | Toggle | `true` → показывать только друзьям | `false` | ⚖️ | GDPR Art.25 · ePrivacy |
| **Show age / birthday** | `birthday_visibility` | ENUM: Full date / Age only / Friends only / Only me / Hidden | `FRIENDS_AGE_ONLY` | `ONLY_ME` | ⚖️ | GDPR Art.9 · COPPA · DSA Art.28 |
| **Show gender** | `gender_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | `FRIENDS` | 💡 | — |
| **Show interests** | `interests_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | `FRIENDS` | 💡 | — |

#### Видимость полей Profile Page (Account Privacy → Profile Page)

| Поле профиля | variable_name | Default | ⚖️ | Комментарий |
|---|---|---|---|---|
| **Full name** | `name_visibility` | `EVERYONE` | 💡 | Имя = публичное (как в соцсети) |
| **Avatar** | `avatar_visibility` | `EVERYONE` | 💡 | Аватар = публичный |
| **Cover** | `cover_visibility` | `EVERYONE` | 💡 | Обложка = публичная |
| **Bio** | `bio_visibility` | `EVERYONE` | 💡 | Открытый профиль → bio публичный |
| **Birthday** | `birthday_visibility` | `FRIENDS_AGE_ONLY` | ⚖️ | Только возраст друзьям (не дата) |
| **Gender** | `gender_visibility` | `EVERYONE` | 💡 | — |
| **Interests** | `interests_visibility` | `FRIENDS` | 💡 | — |

> ✅ `account_private = false` для 18+ — **законно**, открытый профиль допустим по GDPR Art.25  
> ⚖️ `account_private = true` для 13–17 — **обязательно** по DSA Art.28(3)(g)  
> ❌ `seo_indexable` нельзя делать `true` по умолчанию — штраф до 10 млн € (GDPR Art.25)  
> ⚠️ `online_status_visible = true` → видят только ДРУЗЬЯ (не все пользователи!)

---

### 2.2 Contact Info Privacy

**Путь:** Settings → Privacy & Visibility → Contact Info Privacy

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Who sees email** | `email_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.5** — минимизация данных; **никогда не PUBLIC** |
| **Who sees phone** | `phone_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.5 · TCPA** — никогда не PUBLIC |
| **Who sees location/country** | `location_visibility` | ENUM: Only me / Friends / Everyone | `FRIENDS` | ⚖️ | GDPR — локационные данные |
| **Who sees address** | `address_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.9** — адрес = чувствительные данные, строго ONLY_ME |
| **Who sees personal link** | `personal_link_visibility` | ENUM: Only me / Friends / Everyone | `EVERYONE` | 💡 | — |
| **Who sees business link** | `business_link_visibility` | ENUM: Only me / Friends / Everyone | `EVERYONE` | 💡 | — |

> ⚠️ **`email_visibility` и `phone_visibility` НИКОГДА не могут быть `EVERYONE` по умолчанию**  
> ⚠️ **`address_visibility`** — адрес является чувствительными данными категории "местоположение",
> по умолчанию строго `ONLY_ME`. Не должен быть публичным даже для 18+.

---

### 2.3 Content Visibility

**Путь:** Settings → Privacy & Visibility → Content Visibility

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Default post visibility** | `default_post_audience` | ENUM: Everyone / Friends / Friends of Friends / Only me | `FRIENDS` | ⚖️ | GDPR Art.25 · Quebec L25 Art.8 |
| **Media gallery visibility** | `gallery_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | ⚖️ | GDPR Art.25 |
| **Friends list visibility** | `friends_list_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |
| **Categories visibility** | `categories_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Категории профиля — публичная информация |
| **Subscribed blogs visibility** | `subscribed_blogs_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |
| **Discussions visibility** | `discussions_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

> ℹ️ **Categories (`categories_visibility`):** категория профиля (Creator, Artist и т.д.) — публичная
> информация, аналог "профессия" в LinkedIn. Default `EVERYONE` допустим.

---

### 2.4 Interactions

**Путь:** Settings → Privacy & Visibility → Interactions

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Who can send messages** | `who_can_message` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | DSA Art.14 · Israel PPL §2 |
| **Who can tag me** | `who_can_tag` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 — тег = обработка данных |
| **Tag approval required** | `tag_approval_required` | Toggle | `true` | ⚖️ | GDPR Art.25 (Privacy by Default) |
| **Who can comment my posts** | `who_can_comment` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | DSA Art.14 |
| **Who can share my posts** | `share_permission` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 — шеринг = распространение данных |
| **Who can send friend requests** | `friend_request_permission` | ENUM: Everyone / Friends of Friends / No one | `EVERYONE` | 💡 | — |
| **Active status (online indicator)** | `online_status_visible` | Toggle | `true` → только друзья | ⚖️ | GDPR Art.25 · ePrivacy |
| **Last seen** | `last_seen_visible` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 · ePrivacy — метаданные активности |
| **Read receipts** | `read_receipts_visible` | Toggle | `true` | 💡 | — |

> ⚠️ **`active_status` (online indicator):** ON = видят только ДРУЗЬЯ (не «все»). Это важно —  
> «онлайн для всех» без согласия = нарушение ePrivacy Directive.
>
> ⚠️ **`last_seen_visible`:** Default `FRIENDS` (не `EVERYONE`) — по GDPR Art.25 данные о  
> времени активности = персональные данные.
>
> ⚠️ **`share_permission`:** кто может делиться твоими постами вовне. Default `FRIENDS` —  
> это Privacy by Default (GDPR Art.25). Пользователь может ослабить до `EVERYONE`.

---

## 3. Карта пропущенных полей

Поля, описанные пользователем, которых **не было** в предыдущих спецификациях и которые добавлены в этом документе:

| Поле | variable_name | Новый? | Где было раньше |
|---|---|---|---|
| Last name | `last_name` | ✅ Уточнено | SettingsTZ: только `Display name` без разделения |
| Status | `status_text` | 🆕 Новое | Не было ни в одной спеке |
| Category (profile) | `profile_category` | 🆕 Новое | Не было |
| Address | `address_text` | ✅ Подтверждено | Упоминалось, но без поля |
| Address visibility | `address_visibility` | 🆕 **Новое** | **Отсутствовало** в SettingsTZ Contact Info Privacy |
| Personal link visibility | `personal_link_visibility` | 🆕 **Новое** | Только `website_visibility` в SettingsTZ |
| Business link visibility | `business_link_visibility` | 🆕 **Новое** | Отсутствовало |
| Categories visibility | `categories_visibility` | 🆕 **Новое** | **Отсутствовало** в Content Visibility |
| Subscribed blogs visibility | `subscribed_blogs_visibility` | 🆕 **Новое** | **Отсутствовало** |
| Discussions visibility | `discussions_visibility` | 🆕 **Новое** | **Отсутствовало** |
| Share permission | `share_permission` | 🆕 **Новое** | **Отсутствовало** в Interactions |
| Friend request permission | `friend_request_permission` | 🆕 **Новое** | **Отсутствовало** |
| Last seen | `last_seen_visible` | 🆕 **Новое** | **Отсутствовало** |
| Read receipts | `read_receipts_visible` | 🆕 **Новое** | **Отсутствовало** |

---

## 4. Subscribed Communities

### Вопрос: куда поместить «Подписанные сообщества»?

Пользователь разместил «Subscribed communities» в разделе **Account → Account Management**.  
Это нестандартное расположение — рассмотрим варианты:

| Вариант | Где | Плюсы | Минусы |
|---|---|---|---|
| **A: В Account Management** (как предложила пользователь) | Settings → Account → Account Management | Логично как «управление членством» | Смешивает deletion/deactivation с подписками |
| **B: В Friends & Community (отдельный L1 раздел)** | Settings → Friends & Community | Стандартная практика (Discord, Reddit, Telegram) | Требует отдельный раздел |
| **C: В отдельном L2 под Account** | Settings → Account → My Communities | Компромисс | Нестандартно |

**Рекомендация:**

Если в приложении есть раздел **Friends & Community** (L1) — вынести туда:
```
Settings
└── Friends & Community
    ├── My Friends (список друзей)
    ├── Friend Requests
    ├── Subscribed Communities   ← сюда
    └── Subscribed Blogs
```

Если отдельного раздела нет (или он называется иначе) — оставить в Account как подраздел:
```
Settings → Account → Account Management
├── Deactivate account
├── Delete account
├── Switch to Business profile
├── Create Business account
└── Subscribed communities   ← если нет другого места
```

> ℹ️ «Подписанные сообщества» — это не операция управления аккаунтом, а список членств.  
> Логически ближе к Friend/Social разделу. Но финальное решение за дизайнером/продуктом.

---

## 5. ASCII-структура

Полная структура двух разделов с учётом всех уточнений:

```
⚙️ Settings
│
├── 1️⃣ 👤 Account  ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17
│   ├── User Info
│   │   ├── Avatar (upload / delete)
│   │   ├── Cover image (upload / delete)
│   │   ├── First name  [❌ не меняется — показать: «Написать в поддержку»]
│   │   ├── Last name   [✏️ добавить если нет]
│   │   ├── Date of birth  ⚖️ COPPA · GDPR Art.8 · DSA Art.28
│   │   ├── Gender
│   │   └── Interests
│   │
│   ├── Profile Info
│   │   ├── Bio / About
│   │   ├── Status
│   │   ├── Category (Creator / Artist / Athlete / Business…)
│   │   └── Language
│   │
│   ├── Contact Info
│   │   ├── Email  ⚖️ GDPR
│   │   ├── Phone  ⚖️ GDPR · TCPA  [необязательный]
│   │   ├── Location / Country  ⚖️ GDPR
│   │   ├── Address  ⚖️ GDPR (чувствительные)
│   │   ├── Personal link
│   │   └── Business link
│   │
│   └── Account Management  ⚖️
│       ├── Deactivate account          ⚖️ GDPR Art.17
│       ├── Delete account              ⚖️ GDPR Art.17 · CCPA · App Store · Google Play
│       ├── Switch to Business profile  💡
│       └── Create Business account     💡
│
└── 2️⃣ (или 3️⃣) 🔒 Privacy & Visibility  ⚖️ GDPR Art.25
    │
    ├── Account Privacy  ⚖️
    │   ├── Private account         [18+: OFF · 13-17: ON]  ⚖️ GDPR Art.25 · DSA Art.28
    │   ├── Profile in search       [ON]  ⚖️ GDPR Art.17
    │   ├── SEO indexing            [OFF строго]  ⚖️ GDPR Art.25
    │   ├── Activity status         [ON = только друзья]  ⚖️ ePrivacy
    │   ├── Show birthday           [FRIENDS_AGE_ONLY]  ⚖️ GDPR Art.9
    │   ├── Show gender             [EVERYONE]
    │   ├── Show interests          [FRIENDS]
    │   └── Profile page fields:
    │       ├── Full name           [EVERYONE]
    │       ├── Avatar              [EVERYONE]
    │       ├── Cover               [EVERYONE]
    │       ├── Bio                 [EVERYONE]
    │       ├── Birthday            [FRIENDS_AGE_ONLY]
    │       ├── Gender              [EVERYONE]
    │       └── Interests           [FRIENDS]
    │
    ├── Contact Info Privacy  ⚖️ GDPR Art.5 — минимизация данных
    │   ├── Who sees email          [ONLY_ME]  ⚖️ GDPR Art.5 · CAN-SPAM
    │   ├── Who sees phone          [ONLY_ME]  ⚖️ GDPR Art.5 · TCPA
    │   ├── Who sees location       [FRIENDS]  ⚖️ GDPR
    │   ├── Who sees address        [ONLY_ME]  ⚖️ GDPR Art.9
    │   ├── Who sees personal link  [EVERYONE]
    │   └── Who sees business link  [EVERYONE]
    │
    ├── Content Visibility  ⚖️ GDPR Art.25
    │   ├── Default post audience   [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Media gallery           [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Friends list            [FRIENDS]
    │   ├── Categories              [EVERYONE]
    │   ├── Subscribed blogs        [FRIENDS]
    │   └── Discussions             [FRIENDS]
    │
    └── Interactions  ⚖️ DSA Art.14 · GDPR Art.25
        ├── Who can message         [FRIENDS]  ⚖️ DSA Art.14
        ├── Who can tag me          [FRIENDS]  ⚖️ GDPR Art.25
        ├── Tag approval required   [ON]  ⚖️ GDPR Art.25
        ├── Who can comment         [FRIENDS]  ⚖️ DSA Art.14
        ├── Who can share my posts  [FRIENDS]  ⚖️ GDPR Art.25
        ├── Who can send friend req [EVERYONE]
        ├── Activity status (online)[ON = только друзья]  ⚖️ ePrivacy
        ├── Last seen               [FRIENDS]  ⚖️ GDPR Art.25
        └── Read receipts           [ON]
```

---

*PrivacyVisibilitySpec.md v1.0 · Bestme · март 2026*  
*Смежные документы: [AccountPrivacySpec.md](AccountPrivacySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md), [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)*
