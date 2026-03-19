# AccountSpec.md — Спецификация раздела: 1️⃣ ACCOUNT

**Версия:** 1.1 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик  
**Правовое основание:** ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17 — управление аккаунтом обязательно  
**Статус:** 🔴 Часть блокирует публикацию (App Store + Google Play) · ⚖️ GDPR Art.17

> **Этот документ** описывает только раздел **1️⃣ Account** (первый экран настроек).  
> Смежные документы:  
> [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md) — §2 Privacy & Visibility  
> [SettingsOverview.md](SettingsOverview.md) — общая структура всех 9 разделов  
> [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)

---

## Содержание

1. [1.1 User Info — Информация пользователя](#11-user-info)
2. [1.2 Profile Info — Информация профиля](#12-profile-info)
3. [1.3 Contact Info — Контактная информация](#13-contact-info)
4. [1.4 Account Management — Управление аккаунтом](#14-account-management)
5. [ASCII-структура раздела](#ascii-структура)
6. [Обязательно для публикации](#обязательно-для-публикации)
7. [Что изменено в v1.0 — сводка для разработчиков](#changelog-v10)

---

## 1.1 User Info

**Путь в приложении:** Settings → Account → User Info

> Базовые данные профиля — видны на карточке пользователя.  
> **Status** отображается **на аватарке** (поверх фото профиля), поэтому он находится здесь — рядом с Avatar.

| Поле | variable_name | Тип | Редактируемость | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Avatar (фото профиля)** | `avatar_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **Status** | `status_text` | Текст (≤ 80 символов) | ✏️ | 💡 | — |
| **Cover image (обложка)** | `cover_image_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **First name (имя)** | `first_name` | Текст | ❌ **не меняется** после регистрации | ⚖️ | GDPR Art.17 |
| **Last name (фамилия)** | `last_name` | Текст | ✏️ (добавить если нет) | ⚖️ | GDPR Art.17 |
| **Date of birth** | `date_of_birth` | Дата | ❌ **значение не меняется** после регистрации (изменить — только через поддержку) · ✏️ **формат отображения** задаётся отдельно в Privacy & Visibility → `birthday_visibility` | ⚖️ | COPPA · GDPR Art.8 · DSA Art.28 |
| **Gender** | `gender` | ENUM: Male / Female / Other / Prefer not to say | ✏️ | 💡 | — |
| **Interests** | `interest_category` | Multi-select (6 категорий — см. ниже) | ✏️ | 💡 | — |

### Поле «Interests» (Категории интересов) — 6 категорий

> ⚠️ **«Interests» и «Category» — это одно и то же в BestMe.**  
> Пользователь выбирает одну или несколько из **6 категорий оздоровления**, которые определяют его профиль и контент в ленте.  
> Название в UI: **Interests** (или «Your focus areas»).  
> Переменная: `interest_category` (multi-select, можно выбрать несколько).

| # | Категория (EN) | Категория (RU) | icon |
|---|---|---|---|
| 1 | **Sport** | Спорт | 🏃 |
| 2 | **Nutrition** | Питание | 🥗 |
| 3 | **Environment** | Окружающая среда | 🌿 |
| 4 | **Aesthetics & Hygiene** | Эстетика и гигиена | ✨ |
| 5 | **Mental Health** | Ментальное здоровье | 🧠 |
| 6 | **Daily Routine** | Режим жизни | ⏰ |

> 💡 Эти категории определяют:  
> — алгоритм фида (какой контент показывать пользователю)  
> — тематические страницы (куда попадают посты пользователя)  
> — поиск и рекомендации (какие сообщества / блоги рекомендовать)  
> 
> **Важно для разработчиков:** поле `interest_category` заменяет оба поля из предыдущих спецификаций:  
> — `interest_tags` (Interests в User Info)  
> — `profile_category` (Category в Profile Info — Creator / Artist / Business)  
> Они объединены в одно поле с 6 фиксированными значениями.

> ⚠️ **First name не редактируется:** под полем показать подсказку  
> _«Чтобы изменить имя, напишите в поддержку»_ — с прямой кнопкой «Написать в поддержку».  
> Стандартная практика Instagram, TikTok — защита от спуфинга.

> ⚠️ **Date of birth — два разных поля, не путать:**
>
> | Что | Переменная | Редактируемость | Где |
> |---|---|---|---|
> | **Сама дата рождения** (значение) | `date_of_birth` | ❌ **заблокировано** — устанавливается при регистрации, изменить нельзя. Это возрастная верификация (18+). При ошибке — только через поддержку. | Этот экран (User Info) |
> | **Формат отображения** (как дата видна другим) | `birthday_visibility` | ✏️ **редактируется** — пользователь выбирает: показывать **полную дату** или только **возраст**, и кому (всем / друзьям / только мне / скрыть). | **Privacy & Visibility → §2.2 Profile Visibility** |
>
> **Итого:** пользователь не может изменить саму дату, но может настроить, как она отображается — в полном виде (день.месяц.год) или только в виде возраста (например, «28 лет»).  
> По умолчанию: `birthday_visibility = FRIENDS_AGE_ONLY` — только возраст, только друзьям (GDPR Art.9 — полная дата рождения = чувствительные данные).

---

## 1.2 Profile Info

**Путь в приложении:** Settings → Account → Profile Info

> Дополнительная информация, которую пользователь добавляет о себе.  
> Status перемещён в §1.1 User Info (отображается на аватарке).

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Bio / About** | `bio` | Текст (≤ 300 символов) | пусто | 💡 | — |
| **Goals** | `goals` | Multi-select (цели: «пить больше воды», «больше ходить», «медитировать», …) | пусто | 💡 | — |
| **Language** | `app_language` | ENUM (список языков приложения) | System locale | 💡 | — |

> 💡 **Goals (цели)** — это личные цели пользователя внутри каждой категории (Interests).  
> Например, в категории «Nutrition» цели: «Пить 2 л воды в день», «Есть меньше сахара».  
> Goals отличаются от Interests: Interests = категория (что тебя интересует), Goals = конкретное намерение.

---

## 1.3 Contact Info

**Путь в приложении:** Settings → Account → Contact Info

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Email address** | `email` | Текст | обязательный | ⚖️ | GDPR Art.5 — минимизация |
| **Phone number** | `phone_number` | Текст | необязательный | ⚖️ | GDPR · TCPA |
| **Location / Country / Region** | `location_country` | ENUM (страны) | пусто | ⚖️ | GDPR — применимое право |
| **Address** | `address_text` | Текст | пусто | ⚖️ | GDPR — чувствительные данные |
| **Personal link** | `profile_link_url` | URL | пусто | 💡 | — |
| **Blog link** | `blog_link_url` | URL | пусто | 💡 | — |
| **Business link** | `business_link_url` | URL | пусто | 💡 | — |

> ⚠️ **Телефон не является обязательным при регистрации** — это влияет на 2FA  
> (подробнее → [GDPRArt5SecuritySpec.md §1.1](GDPRArt5SecuritySpec.md))

> ⚠️ **«Business link» vs «Switch to Business profile» — в чём разница:**
>
> | Поле | Где | Что делает |
> |---|---|---|
> | **Business link** (Contact Info) | Settings → Account → Contact Info | URL-адрес внешнего бизнес-сайта или страницы (например, `instagram.com/mybrand`). Это просто ссылка — как «Personal link», но для бизнеса. Отображается на профиле как кликабельная иконка. |
> | **Switch to Business profile** (Account Management) | Settings → Account → Account Management | Переключает **режим аккаунта** внутри BestMe — с личного на бизнес-профиль. Это не просто ссылка — это смена типа аккаунта, которая открывает аналитику, бизнес-инструменты и т.д. |
>
> Рекомендация UX: переименовать «Business link» в Contact Info в **«Website / Business page»** (`website_url`) — чтобы не путать с кнопкой переключения профиля.

---

## 1.4 Account Management

**Путь в приложении:** Settings → Account → Account Management

| Пункт | Тип | ⚖️ | Закон |
|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация — аккаунт скрыт, но не удалён) | ⚖️ | GDPR Art.17 |
| **Delete account** | Действие (постоянное удаление + 2-step confirmation) | ⚖️ | GDPR Art.17 · CCPA §1798.105 · **App Store §5.1.1(v)** · **Google Play** |
| **Switch to Business profile** | Действие (переключение текущего аккаунта в бизнес-режим) | 💡 | — |
| **Create Business account** | Действие (создать отдельный бизнес-аккаунт в дополнение к личному) | 💡 | — |

> ⚠️ **App Store + Google Play:** кнопка **Delete account** должна быть доступна **прямо** из настроек.  
> Полный путь: **Settings → Account → Account Management → Delete account**  
> ⚠️ **Google Play** (дополнительно): веб-форма `bestme.app/account/delete` (независимо от in-app).  
> Подробнее → [AccountDeletionSpec.md](AccountDeletionSpec.md)

> 💡 **Switch to Business profile** — переключает тип аккаунта (не создаёт новый, а меняет текущий).  
> **Create Business account** — создаёт отдельный бизнес-аккаунт, привязанный к тому же пользователю.  
> Оба пункта отличаются от поля **Business link** в Contact Info (см. §1.3).

---

## ASCII-структура

```
⚙️ Settings
│
└── 1️⃣ 👤 Account  ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17
    │
    ├── User Info
    │   ├── Avatar (upload / delete)
    │   ├── Status  ← отображается на аватарке
    │   ├── Cover image (upload / delete)
    │   ├── First name  [❌ не меняется — «Написать в поддержку»]  ⚖️ GDPR Art.17
    │   ├── Last name   [✏️ добавить если нет]  ⚖️ GDPR Art.17
    │   ├── Date of birth  [❌ значение заблокировано · ✏️ формат → Privacy §2.2 birthday_visibility]  ⚖️ COPPA · GDPR Art.8
    │   ├── Gender
    │   └── Interests (6 категорий: Sport / Nutrition / Environment /
    │                              Aesthetics & Hygiene / Mental Health / Daily Routine)
    │
    ├── Profile Info
    │   ├── Bio / About
    │   ├── Goals  (multi-select цели внутри категорий)
    │   └── Language
    │
    ├── Contact Info  ⚖️ GDPR Art.5
    │   ├── Email  ⚖️ GDPR (обязательный)
    │   ├── Phone  ⚖️ GDPR · TCPA  [необязательный]
    │   ├── Location / Country  ⚖️ GDPR
    │   ├── Address  ⚖️ GDPR Art.9 (чувствительные данные)
    │   ├── Personal link
    │   ├── Blog link
    │   └── Business link  ← внешний URL бизнес-страницы
    │                         (≠ «Switch to Business profile» в Account Management)
    │
    └── Account Management  ⚖️ GDPR Art.17 · App Store §5.1.1 · Google Play
        ├── Deactivate account   ⚖️ GDPR Art.17
        ├── Delete account       ⚖️ GDPR Art.17 · CCPA · App Store · Google Play  [🔴 БЛОКЕР]
        ├── Switch to Business profile  💡  ← меняет режим аккаунта
        └── Create Business account     💡  ← создаёт отдельный бизнес-аккаунт
```

---

## Обязательно для публикации

### 🔴 БЛОКЕРЫ App Store + Google Play

| # | Что обязательно | Где | Почему |
|---|---|---|---|
| 1 | **Кнопка «Delete account»** доступна прямо из Settings | §1.4 Account Management | App Store §5.1.1(v) + Google Play — отказ в публикации без этого |
| 2 | **Веб-форма удаления** `bestme.app/account/delete` | §1.4 + AccountDeletionSpec.md | Google Play — требует веб-форму независимо от in-app |
| 3 | **First name не редактируется** — показать кнопку «Написать в поддержку» | §1.1 User Info | UX-стандарт + защита от спуфинга |

### ⚖️ ОБЯЗАТЕЛЬНЫЕ настройки (без них — нарушение GDPR)

| # | Настройка | variable_name | Требование | Закон |
|---|---|---|---|---|
| 1 | **Email** — обязателен при регистрации | `email` | Поле обязательное | GDPR Art.5 |
| 2 | **Date of birth** — значение не редактируется после регистрации; формат отображения (`birthday_visibility`) — в Privacy & Visibility | `date_of_birth` · `birthday_visibility` | ❌ заблокировать изменение значения · ✏️ формат — в Privacy §2.2 | COPPA · GDPR Art.8 |
| 3 | **Phone** — не обязателен, влияет на 2FA | `phone_number` | Поле необязательное | GDPR · TCPA |

---

## Changelog v1.0 → v1.1

> 📋 **Для разработчиков:** все изменения относительно предыдущей версии (PrivacyVisibilitySpec.md v2.1 §1).

---

### ✅ ЧТО ДОБАВЛЕНО / ИЗМЕНЕНО

| # | Что | Куда | UX-название | Причина |
|---|---|---|---|---|
| 1 | **Status перемещён в User Info** | §1.1 User Info (рядом с Avatar) | "Status" | Status отображается **на аватарке** пользователя — логически он должен быть рядом с аватаром, а не в Profile Info. Как в WhatsApp, Instagram (статус/настроение виден на фото). |
| 2 | **Interests = Category — унифицированы** | §1.1 User Info | "Interests" | В BestMe «Interests» и «Category» — одно и то же: 6 wellness-категорий (Sport, Nutrition, Environment, Aesthetics & Hygiene, Mental Health, Daily Routine). Единое поле `interest_category` вместо двух разных (`interest_tags` + `profile_category`). |
| 3 | **6 категорий Interests явно прописаны** | §1.1 User Info | Sport · Nutrition · Environment · Aesthetics & Hygiene · Mental Health · Daily Routine | Ранее категории не были явно перечислены в спеке. |
| 4 | **Убран `profile_category` (Creator/Artist/Business) из Profile Info** | §1.2 Profile Info | — | Поле было некорректно — в BestMe нет деления на «Creator / Artist». Категории = 6 wellness-направлений. Удалено во избежание путаницы. |
| 5 | **«Business link» в Contact Info разъяснён** | §1.3 Contact Info | "Business link" / "Website / Business page" | Пользователи путали «Business link» (внешний URL) с «Switch to Business profile» (смена режима аккаунта). Добавлена таблица-сравнение. Рекомендовано переименовать в «Website / Business page». |
| 6 | **Документ разделён** | AccountSpec.md (этот файл) | — | Ранее Account + Privacy & Visibility были в одном файле (PrivacyVisibilitySpec.md). Разделены в отдельные документы для ясности ТЗ. |
| 7 | **`date_of_birth` разъяснён** (v1.1) | §1.1 User Info + §Changelog | "Date of birth" | Уточнено различие: **значение** даты рождения (`date_of_birth`) — заблокировано после регистрации (для возрастной верификации 18+, COPPA/GDPR Art.8). **Формат отображения** (`birthday_visibility`) — редактируется отдельно в Privacy & Visibility §2.2: выбор «показывать полную дату» или «только возраст» (и кому). По умолчанию: `FRIENDS_AGE_ONLY` (GDPR Art.9). |

---

*AccountSpec.md v1.1 · Bestme · март 2026*  
*Смежные документы: [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md), [SettingsOverview.md](SettingsOverview.md), [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)*
