# Settings Structure v2.0 / Структура настроек v2.0
# For Regular Social Network Users / Для обычных пользователей социальной сети

*Version: 2.0 | Date: 2026-02-17*

## Overview / Обзор

This document defines the **new, simplified settings structure** for Bestme social network, optimized for regular users with a bilingual interface (English UI + Russian annotations).

Этот документ определяет **новую, упрощенную структуру настроек** для социальной сети Bestme, оптимизированную для обычных пользователей с двуязычным интерфейсом (английский UI + русские аннотации).

---

## Structure Philosophy v2.0 / Философия структуры v2.0

### Core Principles / Основные принципы:

1. **User Tasks First** / Задачи пользователя на первом месте
   - Organized by what users want to do, not system architecture
   - Организовано по тому, что хотят делать пользователи, а не по системной архитектуре

2. **Progressive Disclosure** / Прогрессивное раскрытие
   - Common settings visible, advanced hidden
   - Частые настройки видны, сложные скрыты

3. **Simplified Privacy** / Упрощенная приватность
   - 3 levels: Public, Friends, Only Me
   - 3 уровня: Всем, Друзьям, Только мне

4. **Bilingual Clarity** / Двуязычная ясность
   - English for UI, Russian for context
   - Английский для UI, русский для контекста

5. **Mobile-First** / Сначала мобильные
   - Optimized for touch and small screens
   - Оптимизировано для нажатий и маленьких экранов

---

## Category Structure / Структура категорий

Total: **5 main categories** (reduced from 8 in v1.0)
Всего: **5 основных категорий** (сокращено с 8 в v1.0)

---

## 📱 1. Profile / Профиль

**Purpose / Цель:**  
Edit your public profile and personal information  
Редактировать публичный профиль и личную информацию

**Icon:** 📱  
**Color:** Purple #9B59B6 / Фиолетовый

### Structure / Структура:

```
📱 Profile / Профиль
│
├── Edit Profile / Редактировать профиль
│   ├── Profile Photo / Фото профиля
│   │   └── Change, crop, remove photo
│   │
│   ├── Cover Photo / Обложка
│   │   └── Change, reposition, remove cover
│   │
│   ├── Name / Имя
│   │   └── Your display name (visible to everyone)
│   │       Ваше отображаемое имя (видно всем)
│   │
│   ├── Username / Имя пользователя
│   │   └── @username (unique identifier)
│   │       @имяпользователя (уникальный идентификатор)
│   │
│   ├── Bio / О себе
│   │   └── Short description (150 characters)
│   │       Краткое описание (150 символов)
│   │
│   ├── Website / Веб-сайт
│   │   └── Your personal website or blog
│   │       Ваш личный сайт или блог
│   │
│   ├── Birthday / День рождения
│   │   ├── Date selector / Выбор даты
│   │   └── Privacy toggle: 🌍 Show to everyone / Friends / Only me
│   │       Приватность: Показать всем / Друзьям / Только мне
│   │
│   └── Gender / Пол
│       ├── Selection: Male, Female, Other, Prefer not to say
│       │   Выбор: Мужской, Женский, Другой, Предпочитаю не указывать
│       └── Privacy toggle: Show / Hide
│           Приватность: Показать / Скрыть
│
├── Contact Info / Контактная информация
│   ├── Phone / Телефон
│   │   ├── Add/Edit phone number
│   │   │   Добавить/изменить номер телефона
│   │   └── Privacy: Friends / Only me (default: Only me)
│   │       Приватность: Друзьям / Только мне (по умолчанию: Только мне)
│   │
│   ├── Email / Электронная почта
│   │   ├── Primary email (required for login)
│   │   │   Основная почта (нужна для входа)
│   │   └── Privacy: Friends / Only me (default: Only me)
│   │       Приватность: Друзьям / Только мне (по умолчанию: Только мне)
│   │
│   └── Location / Местоположение
│       ├── City, Country / Город, Страна
│       └── Privacy: Public / Friends / Only me (default: Public)
│           Приватность: Всем / Друзьям / Только мне (по умолчанию: Всем)
│
└── Interests / Интересы
    ├── Categories / Категории интересов
    │   └── Select from predefined list (Sports, Music, Tech, etc.)
    │       Выбор из списка (Спорт, Музыка, Технологии, и т.д.)
    │
    └── Goals / Цели
        └── Personal goals (Fitness, Learning, Career, etc.)
            Личные цели (Фитнес, Обучение, Карьера, и т.д.)
```

### Key Changes from v1.0 / Ключевые изменения с v1.0:

✅ All profile info in ONE category (was split across multiple)  
✅ Inline privacy toggles (not separate "Visibility" page)  
✅ Simplified contact info (removed "Address" - too sensitive)  
✅ Interests integrated here (not separate category)

---

## 🔒 2. Privacy / Приватность

**Purpose / Цель:**  
Control who can see your content and interact with you  
Контролировать, кто видит контент и может взаимодействовать

**Icon:** 🔒  
**Color:** Red #E74C3C / Красный

### Structure / Структура:

```
🔒 Privacy / Приватность
│
├── Account Privacy / Приватность аккаунта
│   ├── Account Type / Тип аккаунта
│   │   ├── ○ Public Account / Публичный аккаунт
│   │   │   Everyone can see your profile and posts
│   │   │   Все видят ваш профиль и посты
│   │   │
│   │   └── ● Private Account / Приватный аккаунт ✅ (default)
│   │       Only followers you approve can see your posts
│   │       Только подтвержденные подписчики видят посты
│   │
│   └── Profile Visibility / Видимость профиля
│       Who can see your profile photo, bio, and follower count
│       Кто видит ваше фото, описание и счетчик подписчиков
│
├── Content Visibility / Видимость контента
│   ├── Who can see your posts / Кто видит ваши посты
│   │   ├── 🌍 Public / Всем
│   │   ├── 👥 Friends / Друзьям ✅ (default)
│   │   └── 🔒 Only Me / Только мне
│   │
│   └── Who can see your friends list / Кто видит список друзей
│       ├── 🌍 Public / Всем
│       ├── 👥 Friends / Друзьям ✅ (default)
│       └── 🔒 Only Me / Только мне
│
├── Interactions / Взаимодействия
│   ├── Who can send you messages / Кто может писать вам
│   │   ├── Everyone / Все
│   │   ├── Friends / Друзья ✅ (default)
│   │   └── No one / Никто
│   │
│   ├── Who can tag you in posts / Кто может отмечать в постах
│   │   ├── Everyone / Все
│   │   ├── Friends / Друзья ✅ (default)
│   │   └── No one / Никто
│   │   └── Review tags before posting / Проверка перед публикацией ☑️
│   │
│   ├── Who can comment on your posts / Кто может комментировать
│   │   ├── Everyone / Все
│   │   ├── Friends / Друзья ✅ (default)
│   │   ├── Friends of friends / Друзья друзей
│   │   └── No one / Никто
│   │
│   └── Who can share your posts / Кто может делиться постами
│       ├── Everyone / Все ✅ (default)
│       ├── Friends / Друзья
│       └── No one / Никто
│
├── Activity Status / Статус активности
│   ├── Show activity status / Показывать статус активности
│   │   └── Let friends see when you're active
│   │       Друзья видят, когда вы активны
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Show online status / Показывать онлайн статус
│       └── Show green dot when you're online
│           Показывать зеленую точку, когда вы онлайн
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── Blocking & Muting / Блокировка и скрытие
    ├── Blocked Accounts / Заблокированные аккаунты
    │   └── [List of blocked users]
    │       [Список заблокированных пользователей]
    │
    ├── Muted Accounts / Скрытые аккаунты
    │   └── Hide posts without unfollowing
    │       Скрыть посты без отписки
    │
    └── Restricted Accounts / Ограниченные аккаунты
        └── Limit interactions without blocking
            Ограничить взаимодействие без блокировки
```

### Key Changes from v1.0 / Ключевые изменения с v1.0:

✅ ALL privacy in ONE category (was scattered across 13+ settings)  
✅ Simplified to 3 levels everywhere (was 5+ for some fields)  
✅ Grouped by action type (Content, Interactions, Status)  
✅ Clear defaults indicated with ✅  
✅ Icons for each privacy level (visual clarity)

---

## 🔔 3. Notifications / Уведомления

**Purpose / Цель:**  
Manage what alerts you receive  
Управлять уведомлениями, которые получаете

**Icon:** 🔔  
**Color:** Orange #F39C12 / Оранжевый

### Structure / Структура:

```
🔔 Notifications / Уведомления
│
├── Push Notifications / Push-уведомления
│   ├── Enable push notifications / Включить push-уведомления
│   │   [Master toggle ON/OFF] / [Главный переключатель Вкл/Выкл]
│   │
│   ├── Likes and Reactions / Лайки и реакции
│   │   └── When someone likes or reacts to your post
│   │       Когда кто-то лайкает или реагирует на пост
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Comments / Комментарии
│   │   └── When someone comments on your post
│   │       Когда кто-то комментирует ваш пост
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── New Followers / Новые подписчики
│   │   └── When someone follows you
│   │       Когда кто-то подписывается на вас
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Messages / Сообщения
│   │   └── When you receive a new message
│   │       Когда получаете новое сообщение
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Mentions and Tags / Упоминания и отметки
│   │   └── When someone @mentions or tags you
│   │       Когда кто-то @упоминает или отмечает вас
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Friend Requests / Запросы в друзья
│   │   └── When someone sends you a friend request
│   │       Когда кто-то отправляет запрос в друзья
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Live Videos / Прямые эфиры
│       └── When people you follow go live
│           Когда люди, на которых вы подписаны, в эфире
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
├── Email Notifications / Email-уведомления
│   ├── Activity Summary / Сводка активности
│   │   └── Daily or weekly summary of activity
│   │       Ежедневная или еженедельная сводка активности
│   │       [Never / Daily / Weekly] / [Никогда / Ежедневно / Еженедельно]
│   │
│   ├── Reminder Emails / Письма-напоминания
│   │   └── Reminders about posts, friends, or events
│   │       Напоминания о постах, друзьях или событиях
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Product Updates / Обновления продукта
│   │   └── News about new features and updates
│   │       Новости о новых функциях и обновлениях
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Newsletter / Новостная рассылка
│       └── Tips and inspiration
│           Советы и вдохновение
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── In-App Settings / Настройки в приложении
    ├── Sound / Звук
    │   └── Play sound for notifications
    │       Воспроизводить звук для уведомлений
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    ├── Vibration / Вибрация
    │   └── Vibrate for notifications
    │       Вибрация для уведомлений
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    └── Badge Count / Счетчик значков
        └── Show number of unread notifications on app icon
            Показывать количество непрочитанных на иконке
            [Toggle ON/OFF] / [Вкл/Выкл]
```

### Key Changes from v1.0 / Ключевые изменения с v1.0:

✅ NEW CATEGORY (was completely missing in v1.0!)  
✅ Grouped by notification type (Push, Email, In-App)  
✅ Granular control for each type of notification  
✅ Clear descriptions for each option  
✅ Essential for social network engagement

---

## ⚙️ 4. Account / Аккаунт

**Purpose / Цель:**  
Manage your account settings and preferences  
Управление настройками аккаунта и предпочтениями

**Icon:** ⚙️  
**Color:** Blue #3498DB / Синий

### Structure / Структура:

```
⚙️ Account / Аккаунт
│
├── Login & Security / Вход и безопасность
│   ├── Change Password / Изменить пароль
│   │   └── Update your login password
│   │       Обновить пароль для входа
│   │
│   ├── Two-Factor Authentication / Двухфакторная аутентификация
│   │   ├── Enable 2FA for extra security
│   │   │   Включить 2FA для дополнительной защиты
│   │   └── [Setup 2FA] / [Настроить 2FA]
│   │
│   ├── Active Sessions / Активные сессии
│   │   └── See devices where you're logged in
│   │       Устройства, на которых вы вошли в систему
│   │       [View sessions] / [Просмотреть сессии]
│   │
│   ├── Login Activity / История входов
│   │   └── Recent login attempts and locations
│   │       Недавние попытки входа и местоположения
│   │       [View activity] / [Просмотреть активность]
│   │
│   └── Authorized Apps / Авторизованные приложения
│       └── Third-party apps with access to your account
│           Сторонние приложения с доступом к аккаунту
│           [Manage apps] / [Управлять приложениями]
│
├── App Preferences / Настройки приложения
│   ├── Language / Язык
│   │   └── Choose your display language
│   │       Выберите язык отображения
│   │       [English / Русский / Other]
│   │
│   ├── Theme / Тема
│   │   ├── ○ Light Mode / Светлая тема
│   │   ├── ● Dark Mode / Темная тема
│   │   └── ○ Auto (System) / Авто (системная)
│   │
│   ├── Accessibility / Доступность
│   │   ├── Larger Text / Увеличенный текст
│   │   │   [Toggle ON/OFF] / [Вкл/Выкл]
│   │   │
│   │   ├── High Contrast / Высокий контраст
│   │   │   [Toggle ON/OFF] / [Вкл/Выкл]
│   │   │
│   │   └── Reduce Motion / Уменьшить анимацию
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Data Saver / Экономия трафика
│       └── Reduce data usage on mobile
│           Снизить расход данных на мобильном
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── Data Management / Управление данными
    ├── Download Your Data / Скачать ваши данные
    │   └── Request a copy of your posts, photos, and information
    │       Запросить копию постов, фото и информации
    │       [Request download] / [Запросить скачивание]
    │
    ├── Data Permissions / Разрешения на данные
    │   └── Manage what data you've shared with Bestme
    │       Управлять данными, которыми поделились с Bestme
    │       [View permissions] / [Просмотреть разрешения]
    │
    ├── Account Status / Статус аккаунта
    │   ├── Deactivate Account / Деактивировать аккаунт
    │   │   └── Temporarily disable your account
    │   │       Временно отключить аккаунт
    │   │
    │   └── Delete Account / Удалить аккаунт
    │       └── Permanently remove your account and data
    │           Навсегда удалить аккаунт и данные
    │           [Delete permanently] / [Удалить навсегда]
    │
    └── Help & Support / Помощь и поддержка
        ├── Help Center / Центр помощи
        ├── Report a Problem / Сообщить о проблеме
        └── Terms & Privacy Policy / Условия и политика конфиденциальности
```

### Key Changes from v1.0 / Ключевые изменения с v1.0:

✅ Consolidated "Security & Login" + "Data & Privacy" + "Preferences"  
✅ Grouped by logical sections (Login, Preferences, Data)  
✅ Destructive actions (Delete) at bottom with warning  
✅ Help & Support integrated here (one-stop for account stuff)

---

## 💬 5. Content & Interactions / Контент и взаимодействия

**Purpose / Цель:**  
Manage your posts and saved content  
Управление постами и сохраненным контентом

**Icon:** 💬  
**Color:** Green #27AE60 / Зеленый

### Structure / Структура:

```
💬 Content & Interactions / Контент и взаимодействия
│
├── Posts Settings / Настройки постов
│   ├── Default Audience / Аудитория по умолчанию
│   │   └── Who can see your posts by default
│   │       Кто видит ваши посты по умолчанию
│   │       [Public / Friends / Only Me]
│   │       [Всем / Друзьям / Только мне]
│   │
│   ├── Auto-Archive Posts / Автоархивация постов
│   │   └── Automatically archive posts after 30 days
│   │       Автоматически архивировать посты через 30 дней
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Hide Likes Count / Скрыть счетчик лайков
│       └── Hide the number of likes on your posts
│           Скрыть количество лайков на ваших постах
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
├── Saved Content / Сохраненный контент
│   └── Saved Posts / Сохраненные посты
│       └── Posts you've bookmarked for later
│           Посты, которые вы сохранили на потом
│           [View saved] / [Просмотреть сохраненное]
│
├── Media Settings / Настройки медиа
│   ├── Upload Quality / Качество загрузки
│   │   ├── High Quality / Высокое качество
│   │   │   Uses more data / Использует больше данных
│   │   └── Data Saver / Экономия данных ✅ (default)
│   │       Compressed for faster upload
│   │       Сжато для быстрой загрузки
│   │
│   ├── Auto-Play Videos / Автовоспроизведение видео
│   │   ├── Always / Всегда
│   │   ├── Wi-Fi Only / Только Wi-Fi ✅ (default)
│   │   └── Never / Никогда
│   │
│   └── HD Video / HD-видео
│       └── Upload videos in HD (uses more storage)
│           Загружать видео в HD (больше места)
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── Feed Preferences / Настройки ленты
    ├── Show Suggested Posts / Показывать рекомендации
    │   └── See posts from accounts you don't follow
    │       Видеть посты от аккаунтов, на которые не подписаны
    │       [Toggle ON/OFF] ✅ (default ON)
    │
    ├── Sensitive Content / Чувствительный контент
    │   └── Control what sensitive content you see
    │       Контроль чувствительного контента
    │       [Allow / Limit / Hide]
    │       [Разрешить / Ограничить / Скрыть]
    │
    └── Favorite Accounts / Избранные аккаунты
        └── See posts from favorite accounts first
            Сначала видеть посты избранных аккаунтов
            [Add favorites] / [Добавить избранных]
```

### Key Changes from v1.0 / Ключевые изменения с v1.0:

✅ Feed preferences added (control what you see)  
✅ Media settings for data usage  
✅ Saved content organized here (was scattered)  
✅ More user control over content experience

---

## Privacy Level Visual System / Визуальная система уровней приватности

### Icons & Colors / Иконки и цвета:

```
🌍 Public / Всем
   Color: Green #27AE60
   Meaning: Visible to everyone on Bestme
   Значение: Видно всем на Bestme

👥 Friends / Друзьям
   Color: Blue #3498DB
   Meaning: Only visible to people you follow back
   Значение: Видно только тем, на кого подписаны взаимно

🔒 Only Me / Только мне
   Color: Red #E74C3C
   Meaning: Private, visible only to you
   Значение: Приватно, видно только вам
```

### Usage Pattern / Паттерн использования:

```
┌─────────────────────────────────────────┐
│ Who can see your posts?                 │
│ (Кто может видеть ваши посты?)          │
├─────────────────────────────────────────┤
│ ○ 🌍 Public / Всем                      │
│   Everyone on Bestme                    │
│                                         │
│ ● 👥 Friends / Друзьям ✅               │
│   Only people you follow back           │
│                                         │
│ ○ 🔒 Only Me / Только мне               │
│   Just you                              │
└─────────────────────────────────────────┘
```

---

## Comparison: v1.0 vs v2.0 / Сравнение

| Feature | v1.0 | v2.0 | Impact |
|---------|------|------|--------|
| **Categories** | 8 | 5 | -38% cognitive load |
| **Privacy Settings** | 13+ scattered | 1 consolidated | -92% complexity |
| **Privacy Levels** | 3-5+ levels | 3 levels everywhere | 40% simpler |
| **Notifications** | None | Dedicated category | Essential feature added |
| **Business Features** | Always visible | Removed | 95% users benefit |
| **Language** | English only | English + Russian | Better understanding |
| **Organization** | System-centric | User task-centric | More intuitive |
| **Mobile UX** | Not prioritized | Mobile-first | Better on phones |
| **Feed Control** | Limited | Full control | Better UX |

---

## Implementation Notes / Заметки по реализации

### Default Settings / Настройки по умолчанию:

```
Privacy defaults:
- Account: Private ✅
- Posts: Friends ✅
- Messages: Friends ✅
- Comments: Friends ✅
- Sharing: Everyone ✅
- Activity Status: ON ✅
- Online Status: ON ✅

Notification defaults:
- Push: ON ✅ (all types)
- Email: Weekly summary ✅
- Sound: ON ✅
- Vibration: ON ✅

Content defaults:
- Story Archive: ON ✅
- Upload Quality: Data Saver ✅
- Auto-Play: Wi-Fi Only ✅
- Suggested Posts: ON ✅
```

### Progressive Disclosure / Прогрессивное раскрытие:

1. **Level 1:** Most common settings visible by default
2. **Level 2:** "Advanced" link shows more options
3. **Level 3:** "Manage custom list" for granular control

Example / Пример:
```
Privacy → Who can message you
├─ [Dropdown] Everyone / Friends / No one
└─ [Link] Advanced message filters →
    ├─ Block message requests
    ├─ Filter unknown senders
    └─ Custom allowed list
```

---

## Migration from v1.0 / Миграция с v1.0

### Mapping / Соответствие:

| v1.0 Category | v2.0 Category | Notes |
|---------------|---------------|-------|
| Account & Profile → Profile details | Profile / Профиль | Direct mapping |
| Account & Profile → Contact info | Profile / Профиль | Direct mapping |
| Account & Profile → Personal links | Profile / Профиль | Under Contact Info |
| Interests & Goals | Profile / Профиль | Under Interests |
| Content & Activity | Content / Контент | Enhanced features |
| Visibility (all 13 settings) | Privacy / Приватность | Consolidated |
| Preferences | Account / Аккаунт | Under App Preferences |
| Security & Login | Account / Аккаунт | Under Login & Security |
| Data & Privacy | Account / Аккаунт | Under Data Management |
| Professional/Business | (Removed) | Opt-in feature |
| (New) | Notifications / Уведомления | Added |

### Data Migration / Миграция данных:

All existing user settings should map as follows:
```
v1.0 birthday privacy (5 levels) → v2.0 birthday privacy (3 levels):
  - "Everyone full date" → "Public" 🌍
  - "Everyone age only" → "Public" 🌍
  - "Friends full date" → "Friends" 👥
  - "Friends age only" → "Friends" 👥
  - "Private" → "Only Me" 🔒

v1.0 visibility settings → v2.0 privacy category:
  - All 13 settings consolidated into logical groups
  - Defaults applied where user never changed v1.0 setting
```

---

## Success Metrics / Метрики успеха

### Target Improvements / Целевые улучшения:

1. **Findability** / Находимость
   - 30% faster to find any setting
   - 50% fewer support tickets about "can't find setting"

2. **Engagement** / Вовлеченность
   - 40% more users customize at least one setting
   - 60% more users adjust privacy settings

3. **Satisfaction** / Удовлетворенность
   - 4.5+ stars in settings usability rating
   - 70% of users report settings are "easy to use"

4. **Privacy** / Приватность
   - 80% of users understand their privacy settings
   - 50% reduction in accidental public posts

5. **Performance** / Производительность
   - Settings load 2x faster (simpler structure)
   - 50% fewer clicks to complete common tasks

---

## Next Steps / Следующие шаги

1. ✅ Create this structure document
2. ⏳ Create v2.0 draw.io diagram
3. ⏳ User testing with prototype
4. ⏳ Iterate based on feedback
5. ⏳ Developer implementation
6. ⏳ Gradual rollout with A/B testing
7. ⏳ Monitor metrics and iterate

---

*Document Version: 2.0*  
*Created: 2026-02-17*  
*Next Review: After user testing*
