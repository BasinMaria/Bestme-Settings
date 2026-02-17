# Settings Structure v2.1 for Bestme / Структура настроек v2.1 для Bestme
# Personal Profile / Личный профиль

*Version: 2.1 | Date: 2026-02-17*

## About Bestme / О Bestme

**Bestme** - это социальное приложение про саморазвитие и благополучие (self-development and wellbeing), где пользователи:
- ставят **еженедельные цели** (weekly goals)
- читают контент в **блогах**
- общаются в **сообществах**
- ведут **личный профиль** или **бизнес-профиль**

**Фокус:** мягкая поддержка, привычки и ощущение прогресса (не жёсткая продуктивность).

---

## Product Structure / Структура продукта

### Main Sections / Основные разделы:
1. **Home** - главный hub с weekly goal и прогрессом
2. **Weekly Goals** - центральная фича с daily check-in
3. **Blogs** - контент по темам развития
4. **Categories** - 6 категорий здорового образа жизни
5. **Community/Friends** - друзья и сообщества
6. **Profile** - личный профиль
7. **Business Profile** - для экспертов и коучей (отдельно)
8. **Notifications** - уведомления и напоминания
9. **Settings** - настройки (этот документ)

### 6 Health Categories / 6 Категорий здорового образа жизни:
1. Healthy Eating / Здоровое питание
2. Physical Activity / Физическая нагрузка
3. Mental Balance / Душевное равновесие
4. Aesthetics & Hygiene / Эстетика и гигиена
5. Environment / Окружающая среда
6. Daily Routine / Режим дня

---

## Settings Structure Philosophy / Философия структуры настроек

### Core Principles / Основные принципы:

1. **User-Centric** / Ориентация на пользователя
   - Организовано по задачам пользователя
   - Простой и понятный интерфейс

2. **Bilingual Support** / Двуязычная поддержка
   - English for UI / Английский для интерфейса
   - Russian annotations / Русские пояснения

3. **Privacy First** / Приватность прежде всего
   - Четкие настройки видимости
   - Контроль над данными

4. **Community Focus** / Фокус на сообщество
   - Настройки для взаимодействия с друзьями
   - Управление сообществами

5. **Legal Compliance** / Соответствие законам
   - EU, Canada, USA, Israel, California

---

## Settings Categories / Категории настроек

Total: **6 main categories** for Personal Profile
Всего: **6 основных категорий** для личного профиля

---

## 👤 1. Profile / Профиль

**Purpose / Цель:**  
Edit your personal profile and preferences  
Редактировать личный профиль и настройки

**Icon:** 👤  
**Color:** Purple #9B59B6

### Structure / Структура:

```
👤 Profile / Профиль
│
├── Basic Info / Основная информация
│   ├── Profile Photo / Фото профиля
│   │   └── Upload, crop, remove photo
│   │       Загрузить, обрезать, удалить фото
│   │
│   ├── Name / Имя
│   │   └── Your display name
│   │       Ваше отображаемое имя
│   │
│   ├── Username / Имя пользователя
│   │   └── @username (unique)
│   │       @имяпользователя (уникальное)
│   │
│   ├── Bio / О себе
│   │   └── Short description about you (150 characters)
│   │       Краткое описание о вас (150 символов)
│   │
│   └── Links / Ссылки
│       └── Social media links, website, etc.
│           Ссылки на соцсети, сайт и т.д.
│
├── Weekly Goals Preferences / Настройки еженедельных целей
│   ├── Default Goal Category / Категория цели по умолчанию
│   │   └── Choose your preferred category for goals
│   │       Выберите предпочитаемую категорию для целей
│   │
│   ├── Daily Check-in Time / Время ежедневной проверки
│   │   └── When to remind you about daily check-in
│   │       Когда напоминать о ежедневной проверке
│   │       [Time picker: 20:00 default]
│   │
│   └── Week Start Day / День начала недели
│       └── Monday or Sunday
│           Понедельник или воскресенье
│           [Monday ✅ default / Sunday]
│
├── Categories & Interests / Категории и интересы
│   └── Select Your Health Categories / Выберите категории здоровья
│       ├── ☑ Healthy Eating / Здоровое питание
│       ├── ☑ Physical Activity / Физическая нагрузка
│       ├── ☑ Mental Balance / Душевное равновесие
│       ├── ☐ Aesthetics & Hygiene / Эстетика и гигиена
│       ├── ☐ Environment / Окружающая среда
│       └── ☐ Daily Routine / Режим дня
│       
│       These categories help personalize your content and goals
│       Эти категории помогают персонализировать контент и цели
│
└── Contact Info / Контактная информация
    ├── Email / Электронная почта
    │   └── Primary email (required for login)
    │       Основная почта (нужна для входа)
    │
    └── Phone / Телефон (optional)
        └── Optional phone number
            Необязательный номер телефона
```

### Key Features / Ключевые функции:
- ✅ Edit profile information
- ✅ Set weekly goals preferences
- ✅ Choose health categories
- ✅ Add social links

---

## 🔒 2. Privacy / Приватность

**Purpose / Цель:**  
Control who can see your content and activity  
Контролировать, кто видит ваш контент и активность

**Icon:** 🔒  
**Color:** Red #E74C3C

### Structure / Структура:

```
🔒 Privacy / Приватность
│
├── Profile Visibility / Видимость профиля
│   ├── Profile Type / Тип профиля
│   │   ├── ● Public Profile / Публичный профиль ✅ (default)
│   │   │   Anyone can see your profile
│   │   │   Любой может видеть ваш профиль
│   │   │
│   │   └── ○ Private Profile / Приватный профиль
│   │       Only approved friends can see your profile
│   │       Только одобренные друзья видят профиль
│   │
│   └── Profile Info Visibility / Видимость информации профиля
│       Who can see your profile photo, bio, and links
│       Кто видит ваше фото, описание и ссылки
│       ├── 🌍 Everyone / Все ✅ (default)
│       ├── 👥 Friends Only / Только друзья
│       └── 🔒 Only Me / Только я
│
├── Weekly Goals Visibility / Видимость еженедельных целей
│   ├── Show My Goals / Показывать мои цели
│   │   └── Who can see your weekly goals
│   │       Кто видит ваши еженедельные цели
│   │       ├── 🌍 Everyone / Все
│   │       ├── 👥 Friends Only / Только друзья ✅ (default)
│   │       └── 🔒 Only Me / Только я
│   │
│   └── Show My Progress / Показывать мой прогресс
│       └── Who can see your daily check-ins and progress
│           Кто видит ваши ежедневные проверки и прогресс
│           ├── 🌍 Everyone / Все
│           ├── 👥 Friends Only / Только друзья ✅ (default)
│           └── 🔒 Only Me / Только я
│
├── Blog & Posts Visibility / Видимость блога и постов
│   ├── Blog Posts / Посты в блоге
│   │   └── Who can see your blog posts
│   │       Кто видит посты в вашем блоге
│   │       ├── 🌍 Everyone / Все ✅ (default)
│   │       ├── 👥 Friends Only / Только друзья
│   │       └── 🔒 Only Me / Только я
│   │
│   └── Comments on My Posts / Комментарии к моим постам
│       └── Who can comment on your posts
│           Кто может комментировать ваши посты
│           ├── Everyone / Все ✅ (default)
│           ├── Friends Only / Только друзья
│           └── No One / Никто
│
├── Activity Visibility / Видимость активности
│   ├── Friends List / Список друзей
│   │   └── Who can see your friends list
│   │       Кто видит ваш список друзей
│   │       ├── 🌍 Everyone / Все
│   │       ├── 👥 Friends Only / Только друзья ✅ (default)
│   │       └── 🔒 Only Me / Только я
│   │
│   ├── Community Memberships / Членство в сообществах
│   │   └── Who can see which communities you joined
│   │       Кто видит, в какие сообщества вы вступили
│   │       ├── 🌍 Everyone / Все ✅ (default)
│   │       ├── 👥 Friends Only / Только друзья
│   │       └── 🔒 Only Me / Только я
│   │
│   └── Online Status / Онлайн статус
│       └── Show when you're online
│           Показывать, когда вы онлайн
│           [Toggle ON/OFF] ✅ ON (default)
│
└── Blocking / Блокировка
    ├── Blocked Users / Заблокированные пользователи
    │   └── Users you've blocked can't see your profile or contact you
    │       Заблокированные пользователи не видят профиль и не могут связаться
    │       [List of blocked users]
    │
    └── Muted Users / Скрытые пользователи
        └── Hide posts from specific users without unfollowing
            Скрыть посты от определенных пользователей
            [List of muted users]
```

### Key Features / Ключевые функции:
- ✅ Control profile visibility
- ✅ Manage goals and progress visibility
- ✅ Set blog posts visibility
- ✅ Block/mute users

---

## 👥 3. Friends & Community / Друзья и сообщество

**Purpose / Цель:**  
Manage your social connections and community memberships  
Управление социальными связями и членством в сообществах

**Icon:** 👥  
**Color:** Blue #3498DB

### Structure / Структура:

```
👥 Friends & Community / Друзья и сообщество
│
├── Friends Management / Управление друзьями
│   ├── My Friends / Мои друзья
│   │   └── View and manage your friends list
│   │       Просмотр и управление списком друзей
│   │       └── 245 friends, 23 online
│   │           245 друзей, 23 онлайн
│   │
│   ├── Friend Requests / Запросы в друзья
│   │   ├── Pending requests (sent by you)
│   │   │   Ожидающие запросы (отправлены вами)
│   │   │
│   │   └── Incoming requests (from others)
│   │       Входящие запросы (от других)
│   │
│   └── Friend Settings / Настройки друзей
│       ├── Who can send you friend requests / Кто может отправлять запросы
│       │   ├── Everyone / Все ✅ (default)
│       │   ├── Friends of friends / Друзья друзей
│       │   └── No one / Никто
│       │
│       └── Auto-accept from / Автоматически принимать от
│           └── Automatically accept friend requests from specific groups
│               Автоматически принимать запросы от определенных групп
│
├── Communities / Сообщества
│   ├── My Communities / Мои сообщества
│   │   └── Communities you've joined or created
│   │       Сообщества, в которые вы вступили или создали
│   │       [List of communities]
│   │
│   ├── Community Invitations / Приглашения в сообщества
│   │   └── Pending invitations to join communities
│   │       Ожидающие приглашения в сообщества
│   │
│   └── Community Settings / Настройки сообществ
│       ├── Who can invite you to communities / Кто может приглашать
│       │   ├── Everyone / Все
│       │   ├── Friends Only / Только друзья ✅ (default)
│       │   └── No one / Никто
│       │
│       └── Community Notifications / Уведомления сообществ
│           └── Get notified about community activity
│               Получать уведомления об активности сообществ
│               [Toggle ON/OFF] ✅ ON (default)
│
├── Subscriptions / Подписки
│   ├── Blog Subscriptions / Подписки на блоги
│   │   └── Blogs you're subscribed to
│   │       Блоги, на которые вы подписаны
│   │       [List of blog subscriptions]
│   │
│   ├── Business Account Subscriptions / Подписки на бизнес-аккаунты
│   │   └── Business accounts you follow
│   │       Бизнес-аккаунты, на которые вы подписаны
│   │       [List of business subscriptions]
│   │
│   └── Subscription Settings / Настройки подписок
│       └── Manage how you receive updates from subscriptions
│           Управление получением обновлений от подписок
│
└── Activity Feed / Лента активности
    ├── Feed Preferences / Настройки ленты
    │   ├── Show friends' goals / Показывать цели друзей
    │   │   [Toggle ON/OFF] ✅ ON (default)
    │   │
    │   ├── Show friends' achievements / Показывать достижения друзей
    │   │   [Toggle ON/OFF] ✅ ON (default)
    │   │
    │   └── Show community posts / Показывать посты сообществ
    │       [Toggle ON/OFF] ✅ ON (default)
    │
    └── Share Settings / Настройки публикации
        ├── Auto-share my goals / Автоматически делиться целями
        │   └── Share your weekly goals with friends automatically
        │       Автоматически делиться еженедельными целями с друзьями
        │       [Toggle ON/OFF] ☐ OFF (default)
        │
        └── Auto-share achievements / Автоматически делиться достижениями
            └── Share your achievements when you complete goals
                Делиться достижениями при выполнении целей
                [Toggle ON/OFF] ✅ ON (default)
```

### Key Features / Ключевые функции:
- ✅ Manage 245 friends, see 23 online
- ✅ Join/create communities
- ✅ Subscribe to blogs and business accounts
- ✅ Control activity feed

---

## 🔔 4. Notifications / Уведомления

**Purpose / Цель:**  
Manage all alerts and reminders  
Управление всеми уведомлениями и напоминаниями

**Icon:** 🔔  
**Color:** Orange #F39C12

### Structure / Структура:

```
🔔 Notifications / Уведомления
│
├── Weekly Goals Reminders / Напоминания о еженедельных целях
│   ├── Daily Check-in Reminder / Напоминание о ежедневной проверке
│   │   └── Remind me to complete my daily check-in
│   │       Напомнить о ежедневной проверке
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │       Time: [20:00] ✅
│   │
│   ├── Weekly Goal Start / Начало еженедельной цели
│   │   └── Remind me when a new week starts
│   │       Напомнить, когда начинается новая неделя
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │       Day: Monday, Time: 08:00
│   │
│   └── Goal Progress Updates / Обновления прогресса цели
│       └── Notify me about my weekly progress
│           Уведомлять о еженедельном прогрессе
│           [Toggle ON/OFF] ✅ ON (default)
│
├── Social Notifications / Социальные уведомления
│   ├── Friend Requests / Запросы в друзья
│   │   └── When someone sends you a friend request
│   │       Когда кто-то отправляет запрос в друзья
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   ├── Friend Activity / Активность друзей
│   │   ├── Friend completes a goal / Друг выполняет цель
│   │   │   [Toggle ON/OFF] ✅ ON (default)
│   │   │
│   │   └── Friend achieves milestone / Друг достигает вехи
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   └── Comments & Mentions / Комментарии и упоминания
│       ├── Someone comments on your post / Кто-то комментирует пост
│       │   [Toggle ON/OFF] ✅ ON (default)
│       │
│       └── Someone mentions you / Кто-то упоминает вас
│           [Toggle ON/OFF] ✅ ON (default)
│
├── Community Notifications / Уведомления сообществ
│   ├── Community Invitations / Приглашения в сообщества
│   │   └── When someone invites you to a community
│   │       Когда кто-то приглашает в сообщество
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   ├── New Posts in Communities / Новые посты в сообществах
│   │   └── When there are new posts in your communities
│   │       Когда появляются новые посты в ваших сообществах
│   │       [Toggle ON/OFF] ☐ OFF (default - can be noisy)
│   │
│   └── Community Discussions / Дискуссии сообществ
│       └── Updates on discussions you participate in
│           Обновления дискуссий, в которых вы участвуете
│           [Toggle ON/OFF] ✅ ON (default)
│
├── Content Notifications / Уведомления о контенте
│   ├── New Blog Posts / Новые посты в блогах
│   │   └── From blogs you're subscribed to
│   │       От блогов, на которые вы подписаны
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   ├── New Content in Categories / Новый контент в категориях
│   │   └── Content related to your selected categories
│   │       Контент, связанный с вашими категориями
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   └── Recommended Content / Рекомендованный контент
│       └── Personalized content recommendations
│           Персонализированные рекомендации контента
│           [Toggle ON/OFF] ☐ OFF (default)
│
├── Chat Notifications / Уведомления чата
│   ├── New Messages / Новые сообщения
│   │   └── When you receive a new chat message
│   │       Когда получаете новое сообщение в чате
│   │       [Toggle ON/OFF] ✅ ON (default)
│   │
│   └── Message Previews / Превью сообщений
│       └── Show message content in notifications
│           Показывать содержимое сообщений в уведомлениях
│           [Toggle ON/OFF] ✅ ON (default)
│
└── Notification Settings / Настройки уведомлений
    ├── Push Notifications / Push-уведомления
    │   └── Enable push notifications on mobile
    │       Включить push-уведомления на мобильном
    │       [Toggle ON/OFF] ✅ ON (default)
    │
    ├── Email Notifications / Email-уведомления
    │   ├── Daily Summary / Ежедневная сводка
    │   │   └── Receive daily summary of activity
    │   │       Получать ежедневную сводку активности
    │   │       [Toggle ON/OFF] ☐ OFF (default)
    │   │
    │   └── Weekly Summary / Еженедельная сводка
    │       └── Receive weekly summary and insights
    │           Получать еженедельную сводку и аналитику
    │           [Toggle ON/OFF] ✅ ON (default)
    │
    ├── In-App Notifications / Уведомления в приложении
    │   ├── Sound / Звук
    │   │   [Toggle ON/OFF] ✅ ON (default)
    │   │
    │   └── Badge Count / Счетчик значков
    │       [Toggle ON/OFF] ✅ ON (default)
    │
    └── Quiet Hours / Тихие часы
        └── Don't send notifications during these hours
            Не отправлять уведомления в эти часы
            From: [22:00] To: [08:00]
            С: [22:00] До: [08:00]
```

### Key Features / Ключевые функции:
- ✅ Daily check-in reminders (центральная фича!)
- ✅ Friends activity notifications
- ✅ Community updates
- ✅ Chat notifications
- ✅ Quiet hours setting

---

## 📝 5. Content / Контент

**Purpose / Цель:**  
Manage your blog and saved content  
Управление вашим блогом и сохраненным контентом

**Icon:** 📝  
**Color:** Green #27AE60

### Structure / Структура:

```
📝 Content / Контент
│
├── My Personal Blog / Мой личный блог
│   ├── Blog Settings / Настройки блога
│   │   ├── Blog Name / Название блога
│   │   │   └── Name of your personal blog
│   │   │       Название вашего личного блога
│   │   │       [Text input]
│   │   │
│   │   ├── Blog Description / Описание блога
│   │   │   └── Short description of your blog
│   │   │       Краткое описание вашего блога
│   │   │       [Text area, 300 characters]
│   │   │
│   │   └── Blog Visibility / Видимость блога
│   │       └── Who can see your blog
│   │           Кто может видеть ваш блог
│   │           ├── 🌍 Everyone / Все ✅ (default)
│   │           ├── 👥 Friends Only / Только друзья
│   │           └── 🔒 Only Me / Только я
│   │
│   ├── Post Settings / Настройки постов
│   │   ├── Default Post Visibility / Видимость постов по умолчанию
│   │   │   └── Default audience for new posts
│   │   │       Аудитория по умолчанию для новых постов
│   │   │       ├── 🌍 Everyone / Все ✅ (default)
│   │   │       ├── 👥 Friends Only / Только друзья
│   │   │       └── 🔒 Only Me / Только я (draft)
│   │   │
│   │   ├── Comments / Комментарии
│   │   │   └── Allow comments on your posts by default
│   │   │       Разрешить комментарии к постам по умолчанию
│   │   │       [Toggle ON/OFF] ✅ ON (default)
│   │   │
│   │   └── Post Categories / Категории постов
│   │       └── Tag your posts with health categories
│   │           Отмечать посты категориями здоровья
│   │           [Select multiple categories]
│   │
│   └── Blog Statistics / Статистика блога
│       └── View stats about your blog (views, subscribers)
│           Просмотр статистики блога (просмотры, подписчики)
│           [View Statistics]
│
├── Saved Content / Сохраненный контент
│   ├── Saved Posts / Сохраненные посты
│   │   └── Posts you've bookmarked for later
│   │       Посты, сохраненные на потом
│   │       [View Saved Posts]
│   │
│   ├── Saved Goals / Сохраненные цели
│   │   └── Goal ideas you want to try
│   │       Идеи целей, которые хотите попробовать
│   │       [View Saved Goals]
│   │
│   └── Organize Saved Content / Организация сохраненного
│       └── Create folders or tags for your saved content
│           Создать папки или теги для сохраненного контента
│           [Manage Organization]
│
├── Discussions / Дискуссии
│   ├── My Discussions / Мои дискуссии
│   │   └── Discussions you've started in categories
│   │       Дискуссии, которые вы начали в категориях
│   │       [View My Discussions]
│   │
│   ├── Participating In / Участвую в
│   │   └── Discussions you're participating in
│   │       Дискуссии, в которых вы участвуете
│   │       [View Active Discussions]
│   │
│   └── Discussion Preferences / Настройки дискуссий
│       ├── Who can reply to your discussions / Кто может отвечать
│       │   ├── Everyone / Все ✅ (default)
│       │   ├── Friends Only / Только друзья
│       │   └── No one / Никто
│       │
│       └── Notify about replies / Уведомлять об ответах
│           [Toggle ON/OFF] ✅ ON (default)
│
└── Content Preferences / Настройки контента
    ├── Content Language / Язык контента
    │   └── Preferred language for content recommendations
    │       Предпочитаемый язык для рекомендаций контента
    │       [English / Русский / Both]
    │
    └── Content Filters / Фильтры контента
        └── Hide content with specific topics or triggers
            Скрыть контент с определенными темами или триггерами
            [Manage Filters]
```

### Key Features / Ключевые функции:
- ✅ Personal blog management (one blog per user)
- ✅ Saved content organization
- ✅ Discussions in categories
- ✅ Content preferences

---

## ⚙️ 6. Account / Аккаунт

**Purpose / Цель:**  
Manage your account, security, and app preferences  
Управление аккаунтом, безопасностью и настройками приложения

**Icon:** ⚙️  
**Color:** Gray #7F8C8D

### Structure / Структура:

```
⚙️ Account / Аккаунт
│
├── Login & Security / Вход и безопасность
│   ├── Email / Электронная почта
│   │   └── Change your login email
│   │       Изменить email для входа
│   │       [Current: user@example.com]
│   │
│   ├── Password / Пароль
│   │   └── Change your password
│   │       Изменить пароль
│   │       [Change Password]
│   │
│   ├── Two-Factor Authentication / Двухфакторная аутентификация
│   │   └── Add extra security to your account
│   │       Добавить дополнительную защиту аккаунта
│   │       [Setup 2FA]
│   │       Status: ☐ Not enabled / Не включена
│   │
│   ├── Active Sessions / Активные сессии
│   │   └── Devices where you're currently logged in
│   │       Устройства, на которых вы вошли в систему
│   │       [View Sessions]
│   │
│   └── Login Activity / История входов
│       └── Recent login attempts and locations
│           Недавние попытки входа и местоположения
│           [View Activity]
│
├── App Preferences / Настройки приложения
│   ├── Language / Язык
│   │   └── Choose your app language
│   │       Выберите язык приложения
│   │       ├── ○ English
│   │       ├── ● Русский ✅ (your selection)
│   │       └── ○ Auto (system)
│   │
│   ├── Theme / Тема
│   │   └── Choose app appearance
│   │       Выберите внешний вид приложения
│   │       ├── ○ Light Mode / Светлая
│   │       ├── ● Dark Mode / Темная ✅
│   │       └── ○ Auto (system) / Авто
│   │
│   ├── Timezone / Часовой пояс
│   │   └── Your local timezone for reminders
│   │       Ваш часовой пояс для напоминаний
│   │       [Select timezone]
│   │
│   └── Accessibility / Доступность
│       ├── Larger Text / Увеличенный текст
│       │   [Toggle ON/OFF] ☐ OFF (default)
│       │
│       ├── High Contrast / Высокий контраст
│       │   [Toggle ON/OFF] ☐ OFF (default)
│       │
│       └── Reduce Motion / Уменьшить анимацию
│           [Toggle ON/OFF] ☐ OFF (default)
│
├── Data & Privacy / Данные и конфиденциальность
│   ├── Download Your Data / Скачать ваши данные
│   │   └── Request a copy of your data
│   │       Запросить копию ваших данных
│   │       [Request Download]
│   │
│   ├── Data Sharing / Обмен данными
│   │   └── Control what data you share with Bestme
│   │       Контроль данных, которыми вы делитесь с Bestme
│   │       [Manage Data Sharing]
│   │
│   ├── Privacy Policy / Политика конфиденциальности
│   │   └── Read our privacy policy (EU, USA, Canada, Israel compliant)
│   │       Ознакомиться с политикой конфиденциальности
│   │       [View Policy]
│   │
│   └── Legal Compliance / Соответствие законам
│       └── Information about data protection
│           Информация о защите данных
│           Compliant with: EU GDPR, California CCPA, Canada PIPEDA
│           Соответствует: EU GDPR, California CCPA, Canada PIPEDA
│
├── Business Profile / Бизнес-профиль
│   ├── Create Business Profile / Создать бизнес-профиль
│   │   └── Switch to or create a business profile
│   │       Переключиться или создать бизнес-профиль
│   │       [Create Business Profile]
│   │       
│   │   Note: Business profiles have separate settings
│   │   Примечание: У бизнес-профилей отдельные настройки
│   │
│   └── Switch to Business Profile / Переключиться на бизнес-профиль
│       └── If you already have a business profile
│           Если у вас уже есть бизнес-профиль
│           [Switch Profile]
│
└── Account Management / Управление аккаунтом
    ├── Deactivate Account / Деактивировать аккаунт
    │   └── Temporarily disable your account
    │       Временно отключить аккаунт
    │       [Deactivate]
    │
    ├── Delete Account / Удалить аккаунт
    │   └── Permanently delete your account and all data
    │       Навсегда удалить аккаунт и все данные
    │       [Delete Account]
    │       
    │       ⚠️ This action cannot be undone
    │       ⚠️ Это действие нельзя отменить
    │
    └── Help & Support / Помощь и поддержка
        ├── Help Center / Центр помощи
        ├── Contact Support / Связаться с поддержкой
        └── Terms of Service / Условия использования
```

### Key Features / Ключевые функции:
- ✅ Login security and 2FA
- ✅ App language and theme
- ✅ Data download and privacy
- ✅ Business profile creation
- ✅ Legal compliance (EU, USA, Canada, Israel, California)

---

## Privacy Level Visual System / Визуальная система уровней приватности

### Icons & Colors / Иконки и цвета:

```
🌍 Everyone / Все
   Color: Green #27AE60
   Meaning: Visible to all Bestme users
   Значение: Видно всем пользователям Bestme

👥 Friends Only / Только друзья
   Color: Blue #3498DB
   Meaning: Only visible to your friends
   Значение: Видно только вашим друзьям

🔒 Only Me / Только я
   Color: Red #E74C3C
   Meaning: Private, visible only to you
   Значение: Приватно, видно только вам
```

---

## Default Settings Summary / Сводка настроек по умолчанию

### Profile / Профиль:
- Weekly check-in time: 20:00
- Week starts: Monday
- Default categories: Healthy Eating, Physical Activity, Mental Balance

### Privacy / Приватность:
- Profile type: Public
- Profile info: Everyone
- Goals visibility: Friends Only
- Progress visibility: Friends Only
- Blog posts: Everyone
- Friends list: Friends Only

### Friends & Community / Друзья и сообщество:
- Friend requests: Everyone can send
- Community invitations: Friends only
- Auto-share achievements: ON
- Auto-share goals: OFF

### Notifications / Уведомления:
- Daily check-in reminder: ON at 20:00
- Friend activity: ON
- Chat messages: ON
- Email weekly summary: ON
- Quiet hours: 22:00 - 08:00

### Content / Контент:
- Blog visibility: Everyone
- Default post visibility: Everyone
- Comments allowed: Yes
- Discussion replies: Everyone

### Account / Аккаунт:
- Language: Русский
- Theme: Dark Mode
- 2FA: Not enabled

---

## Key Differences from v2.0 / Ключевые отличия от v2.0

### ❌ Removed (doesn't exist in Bestme):
- Stories Settings
- Collections (replaced with "Saved Content")

### ✅ Added (actual Bestme features):
- Weekly Goals settings and daily check-in reminders
- Friends management (245 friends, 23 online)
- Communities (join, create, manage)
- Personal Blog (one per user)
- Discussions in categories
- Chat (1-on-1 messaging)
- Subscriptions (blogs, business accounts)
- Business Profile creation

### ✅ Updated:
- 6 health categories as framework
- Social focus (friends, community, sharing)
- Achievement sharing
- Legal compliance noted

---

## Business Profile Settings / Настройки бизнес-профиля

**Note / Примечание:**  
Business Profile has **separate settings** with additional features for experts, coaches, psychologists, content creators, and brands.

Бизнес-профиль имеет **отдельные настройки** с дополнительными функциями для экспертов, коучей, психологов, создателей контента и брендов.

See: `BUSINESS_PROFILE_SETTINGS.md` (to be created)  
Смотрите: `BUSINESS_PROFILE_SETTINGS.md` (будет создан)

---

## Legal Compliance / Соответствие законам

Bestme complies with data protection and privacy laws in:
Bestme соответствует законам о защите данных и конфиденциальности:

- 🇪🇺 **European Union** - GDPR (General Data Protection Regulation)
- 🇨🇦 **Canada** - PIPEDA (Personal Information Protection and Electronic Documents Act)
- 🇺🇸 **United States** - Various state and federal laws
- 🇮🇱 **Israel** - Privacy Protection Law
- 🏴󠁵󠁳󠁣󠁡󠁿 **California** - CCPA (California Consumer Privacy Act)

All settings respect user rights to:
Все настройки уважают права пользователя на:
- Access their data / Доступ к данным
- Delete their data / Удаление данных
- Export their data / Экспорт данных
- Control how data is used / Контроль использования данных

---

## Implementation Notes / Заметки по реализации

### For Developers / Для разработчиков:

1. **Weekly Goals Integration**
   - Daily check-in notifications are critical
   - Track 7-day progress (Mon-Sun or Sun-Sat)
   - Emotional screens at week end

2. **Social Features**
   - Friends count real-time (245 friends, 23 online)
   - Community join/create flow
   - 1-on-1 chat only (no group chat yet)

3. **One Blog Per User**
   - Each user has ONE personal blog
   - Can subscribe to other users' blogs
   - Can subscribe to business account blogs

4. **Categories Framework**
   - 6 categories structure all content
   - Goals, blogs, challenges use categories
   - Discussions happen within categories

5. **Legal Compliance**
   - Data export functionality required
   - Cookie consent (EU)
   - Opt-out mechanisms (California)
   - Data retention policies

---

## Recommendations for Future / Рекомендации на будущее

### Suggested Features (not yet in v2.1):

1. **Group Chat / Групповой чат**
   - Currently 1-on-1 only
   - Consider adding community group chats

2. **Advanced Goal Tracking / Расширенное отслеживание целей**
   - Habit streaks / Серии привычек
   - Long-term goals (monthly, yearly)
   - Goal templates

3. **Challenges / Челленджи**
   - Weekly/monthly challenges
   - Group challenges in communities
   - Challenge leaderboards

4. **Badges & Achievements / Значки и достижения**
   - Visual achievement system
   - Profile badges
   - Milestone celebrations

5. **Analytics / Аналитика**
   - Personal insights dashboard
   - Progress over time
   - Category-based analytics

6. **Premium Features / Премиум функции**
   - Advanced analytics
   - Priority support
   - Custom themes

---

## Next Steps / Следующие шаги

1. ✅ Create this structure document (v2.1)
2. ⏳ Create BUSINESS_PROFILE_SETTINGS.md
3. ⏳ Update BILINGUAL_UI_GUIDELINES.md with Bestme context
4. ⏳ Create visual draw.io diagram for v2.1
5. ⏳ User testing and feedback
6. ⏳ Implementation by development team

---

*Document Version: 2.1*  
*Created: 2026-02-17*  
*For: Bestme Personal Profile Settings*  
*Next Review: After user feedback*
