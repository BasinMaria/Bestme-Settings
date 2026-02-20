# Privacy Settings Structure / Структура настроек приватности
# Bestme Social App

*Date: 2026-02-17*

---

## 🔒 Privacy / Приватность

Complete privacy settings structure with legal compliance based on access table.

---

```
🔒 Privacy / Приватность
│
├── Account Privacy / Приватность аккаунта
│   ├── Profile Page / Страница профиля
│   │   └── Default: PUBLIC
│   │       Variable: profile_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: Minimum metadata visible (GDPR Art. 15)
│   │       Visibility:
│   │       • PUBLIC: ✅ Full profile to everyone
│   │       • FRIENDS_ONLY: ⚠️ Name + avatar only to non-friends
│   │       • PRIVATE: ⚠️ Minimal info only
│   │
│   ├── Name / Имя
│   │   └── Default: PUBLIC
│   │       Variable: name_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: Minimum "First name + Initial" must be visible (GDPR)
│   │       Visibility:
│   │       • PUBLIC: ✅ Full name to everyone
│   │       • FRIENDS_ONLY: ✅ Full name to friends, ⚠️ First+Initial to others
│   │       • PRIVATE: ⚠️ First name only to everyone
│   │
│   ├── Avatar Photo / Фото профиля
│   │   └── Default: PUBLIC
│   │       Variable: avatar_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       Visibility:
│   │       • PUBLIC: ✅ Show to everyone
│   │       • FRIENDS_ONLY: ⚠️ Placeholder to non-friends
│   │       • PRIVATE: ⚠️ Placeholder to non-friends
│   │
│   ├── Cover Photo / Обложка
│   │   └── Default: PUBLIC
│   │       Variable: cover_photo_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       Visibility:
│   │       • PUBLIC: ✅ Show to everyone
│   │       • FRIENDS_ONLY: ⚠️ Placeholder to non-friends
│   │       • PRIVATE: ⚠️ Placeholder to non-friends
│   │
│   ├── Bio / About / О себе
│   │   └── Default: PUBLIC
│   │       Variable: bio_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Description / Описание
│   │   └── Default: PUBLIC
│   │       Variable: description_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Birthday / День рождения
│   │   └── Default: PRIVATE ⚠️
│   │       Variable: birthday_visibility
│   │       Options: PUBLIC_FULL, PUBLIC_AGE, FRIENDS_FULL, FRIENDS_AGE, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Must default to PRIVATE
│   │       ⚠️ Always stored in DB for COPPA age check (13+)
│   │       Visibility:
│   │       • PUBLIC_FULL: ✅ Full date to everyone
│   │       • PUBLIC_AGE: ⚠️ Age only to everyone
│   │       • FRIENDS_FULL: ✅ Full date to friends, ❌ Hide from others
│   │       • FRIENDS_AGE: ⚠️ Age to friends, ❌ Hide from others
│   │       • PRIVATE: ❌ Hidden from everyone
│   │
│   ├── Gender / Пол
│   │   └── Default: PRIVATE ⚠️
│   │       Variable: gender_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Sensitive personal data
│   │
│   ├── Email / Электронная почта
│   │   └── Default: PRIVATE ⚠️
│   │       Variable: email_visibility
│   │       Options: FRIENDS_ONLY, PRIVATE (❌ NO PUBLIC option)
│   │       ⚠️ Legal: GDPR + CAN-SPAM (USA) + CASL (Canada)
│   │       ⚠️ FORBIDDEN to make PUBLIC
│   │
│   ├── Phone / Телефон
│   │   └── Default: PRIVATE ⚠️
│   │       Variable: phone_visibility
│   │       Options: FRIENDS_ONLY, PRIVATE (❌ NO PUBLIC option)
│   │       ⚠️ Legal: GDPR + TCPA (USA) + PIPEDA (Canada)
│   │       ⚠️ FORBIDDEN to make PUBLIC
│   │
│   ├── Location / Местоположение
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: location_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Location data
│   │
│   ├── Address / Адрес
│   │   └── Default: PRIVATE
│   │       Variable: address_visibility (implied, not in table)
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Precise location = sensitive data
│   │
│   ├── Personal Links / Личные ссылки
│   │   └── Default: PUBLIC
│   │       Variable: personal_links_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Social Media Links / Ссылки на соцсети
│   │   └── Default: PUBLIC
│   │       Variable: social_links_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Blog Link / Ссылка на блог
│   │   └── Default: PUBLIC
│   │       Variable: show_blog_link
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   └── Business Link / Ссылка на бизнес
│       └── Default: PRIVATE
│           Variable: show_business_link
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Legal: GDPR Art. 6 - Business ownership = personal data
│
├── Content Visibility / Видимость контента
│   ├── Who can see your posts / Кто видит ваши посты
│   │   └── Default: PUBLIC
│   │       Variable: default_post_visibility
│   │       ├── 🌍 Public / Всем
│   │       ├── 👥 Friends / Друзьям ✅
│   │       └── 🔒 Only Me / Только мне
│   │       ⚠️ Note: User MUST control each post individually (GDPR)
│   │
│   ├── Media Gallery / Галерея медиа
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: media_gallery_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Photos can contain faces, children, locations
│   │
│   ├── Who can see your friends list / Кто видит список друзей
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: friends_list_visibility
│   │       ├── 🌍 Public / Всем
│   │       ├── 👥 Friends / Друзьям ✅ (default)
│   │       └── 🔒 Only Me / Только мне (⚠️ Mutual friends still visible)
│   │       ⚠️ Legal: Mutual friends MUST always be visible
│   │       Visibility:
│   │       • PUBLIC: ✅ Full list to everyone
│   │       • FRIENDS_ONLY: ✅ Full list to friends, ⚠️ Mutual only to others
│   │       • PRIVATE: ⚠️ Mutual friends only to everyone
│   │
│   ├── Categories / Интересы (категории)
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: categories_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Can reveal religion, politics, orientation
│   │
│   ├── Subscribed Blogs / Подписки на блоги
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: subscribed_blogs_visibility
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Can reveal political/religious views
│   │
│   └── Subscribed Communities / Подписки на сообщества
│       └── Default: FRIENDS_ONLY
│           Variable: subscribed_communities_visibility
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Legal: GDPR Art. 9 - Can reveal sensitive interests
│
├── Interactions / Взаимодействия
│   ├── Who can send you messages / Кто может писать вам
│   │   └── Default: FRIENDS_ONLY ✅
│   │       Variable: who_can_message
│   │       ├── Everyone / Все
│   │       ├── Friends / Друзья ✅ (default)
│   │       ├── Friends of Friends / Друзья друзей
│   │       └── No one / Никто
│   │       ⚠️ Legal: ePrivacy Directive (EU) + GDPR
│   │       ⚠️ Recommended: FRIENDS_ONLY (Privacy by Default)
│   │
│   ├── Who can tag you in posts / Кто может отмечать в постах
│   │   └── Default: FRIENDS_ONLY ✅
│   │       Variable: who_can_tag (implied, not in table)
│   │       ├── Everyone / Все
│   │       ├── Friends / Друзья ✅ (default)
│   │       └── No one / Никто
│   │       └── Review tags before posting / Проверка перед публикацией ☑️
│   │
│   ├── Who can comment on your posts / Кто может комментировать
│   │   └── Default: FRIENDS_ONLY ✅
│   │       Variable: who_can_comment (implied, not in table)
│   │       ├── Everyone / Все
│   │       ├── Friends / Друзья ✅ (default)
│   │       ├── Friends of friends / Друзья друзей
│   │       └── No one / Никто
│   │
│   ├── Who can share your posts / Кто может делиться постами
│   │   └── Default: EVERYONE ✅
│   │       Variable: who_can_share (implied, not in table)
│   │       ├── Everyone / Все ✅ (default)
│   │       ├── Friends / Друзья
│   │       └── No one / Никто
│   │
│   └── Who can send friend request / Кто может отправлять запросы в друзья
│       └── Default: EVERYONE
│           Variable: who_can_send_friend_request
│           ├── Everyone / Все ✅ (default)
│           ├── Friends of Friends / Друзья друзей
│           └── No one / Никто
│
├── Activity Status / Статус активности
│   ├── Show online status / Показывать онлайн статус
│   │   └── Default: FRIENDS_ONLY
│   │       Variable: show_online_status
│   │       Options: EVERYONE, FRIENDS_ONLY, NOBODY
│   │       ⚠️ Legal: GDPR Art. 9 - Behavioral tracking data
│   │       Toggle: ON ✅ / OFF
│   │
│   └── Show last seen / Показывать когда был онлайн
│       └── Default: FRIENDS_ONLY
│           Variable: show_last_seen
│           Options: EVERYONE, FRIENDS_ONLY, NOBODY
│           ⚠️ Legal: GDPR Art. 9 - Activity tracking data
│           Toggle: ON ✅ / OFF
│
└── Blocking & Muting / Блокировка и скрытие
    ├── Blocked Accounts / Заблокированные аккаунты
    │   └── [List of blocked users]
    │       [Список заблокированных пользователей]
    │       Users you've blocked can't see your profile or contact you
    │       Заблокированные не видят профиль и не могут связаться
    │
    ├── Muted Accounts / Скрытые аккаунты
    │   └── Hide posts without unfollowing
    │       Скрыть посты без отписки
    │       You still follow them, but don't see their posts
    │       Вы подписаны, но не видите их посты
    │
    └── Restricted Accounts / Ограниченные аккаунты
        └── Limit interactions without blocking
            Ограничить взаимодействие без блокировки
            They can see public posts but with limited interaction
            Видят публичные посты но с ограниченным взаимодействием
```

---

## Privacy Levels Explanation / Объяснение уровней приватности

### Standard 3-Level Privacy / Стандартная 3-уровневая приватность:

```
🌍 PUBLIC / ВСЕМ
   └── Visible to everyone on Bestme
       Видно всем на Bestme

👥 FRIENDS_ONLY / ТОЛЬКО ДРУЗЬЯМ
   └── Visible only to your friends
       Видно только вашим друзьям

🔒 PRIVATE / ПРИВАТНО
   └── Hidden from everyone (only you can see)
       Скрыто от всех (видите только вы)
```

### Special Birthday Privacy / Специальная приватность дня рождения:

```
📅 PUBLIC_FULL / ВСЕМ (ПОЛНАЯ ДАТА)
   └── Full birthdate visible to everyone
       Полная дата рождения видна всем

📅 PUBLIC_AGE / ВСЕМ (ТОЛЬКО ВОЗРАСТ)
   └── Only age visible to everyone
       Только возраст виден всем

📅 FRIENDS_FULL / ДРУЗЬЯМ (ПОЛНАЯ ДАТА)
   └── Full birthdate visible to friends only
       Полная дата видна только друзьям

📅 FRIENDS_AGE / ДРУЗЬЯМ (ТОЛЬКО ВОЗРАСТ)
   └── Only age visible to friends
       Только возраст виден друзьям

📅 PRIVATE / ПРИВАТНО
   └── Completely hidden
       Полностью скрыто
```

### Messaging Privacy / Приватность сообщений:

```
🌍 EVERYONE / ВСЕ
   └── Anyone can send you messages
       Любой может отправить сообщение

👥 FRIENDS_ONLY / ТОЛЬКО ДРУЗЬЯ
   └── Only friends can message you
       Только друзья могут писать

👥 FRIENDS_OF_FRIENDS / ДРУЗЬЯ ДРУЗЕЙ
   └── Friends and their friends can message
       Друзья и их друзья могут писать

🔒 NOBODY / НИКТО
   └── No one can send messages
       Никто не может писать
```

---

## Legal Compliance Summary / Сводка по соответствию законам

### GDPR (EU) Requirements / Требования GDPR (ЕС):

**Article 6 - Personal Data / Статья 6 - Персональные данные:**
- Name, email, phone, location
- Business ownership information

**Article 9 - Sensitive Data / Статья 9 - Чувствительные данные:**
- Birthday (age verification)
- Gender (especially non-binary)
- Location (precise tracking)
- Photos/videos (faces, biometric data)
- Interests/Categories (religion, politics, health, orientation)
- Community memberships
- Online status and activity tracking

**Article 15 - Right to Access / Статья 15 - Право доступа:**
- Minimum metadata must remain visible

### USA Compliance / Соответствие США:

- **CAN-SPAM Act:** Email cannot be PUBLIC
- **TCPA:** Phone cannot be PUBLIC
- **COPPA:** Age verification required (13+)
- **California CCPA:** Privacy by Default

### Canada Compliance / Соответствие Канада:

- **PIPEDA:** Phone/email protection
- **CASL:** Anti-spam for email

---

## Default Settings Summary / Сводка настроек по умолчанию

### Public by Default / Публично по умолчанию:
✅ Profile Page  
✅ Name  
✅ Avatar Photo  
✅ Cover Photo  
✅ Bio / About  
✅ Description  
✅ Personal Links  
✅ Social Media Links  
✅ Blog Link  
✅ Default Post Visibility  

### Friends Only by Default / Только друзья по умолчанию:
👥 Location  
👥 Media Gallery  
👥 Friends List  
👥 Categories (Interests)  
👥 Subscribed Blogs  
👥 Subscribed Communities  
👥 Online Status  
👥 Last Seen  
👥 Who Can Send Messages  

### Private by Default / Приватно по умолчанию:
🔒 Birthday (GDPR requirement)  
🔒 Gender (GDPR requirement)  
🔒 Email (Legal requirement)  
🔒 Phone (Legal requirement)  
🔒 Address  
🔒 Business Link  

### Special Defaults / Специальные настройки:
🌍 Who Can Send Friend Request: EVERYONE

---

## Notes / Примечания:

### Cannot Be Made Public / Нельзя сделать публичными:
❌ Email (legal restriction)  
❌ Phone (legal restriction)  

### Always Visible to Both Parties / Всегда видно обеим сторонам:
⚠️ Mutual friends (transparency law)

### Must Allow Individual Control / Должен быть индивидуальный контроль:
⚠️ Each post visibility (GDPR requirement)

### Age Verification Required / Требуется проверка возраста:
⚠️ Birthday always stored in DB for COPPA (13+ years)

---

## Variable Reference / Справочник переменных

| Setting | Variable Name | Type | Default |
|---------|--------------|------|---------|
| Profile Page | `profile_visibility` | enum | PUBLIC |
| Name | `name_visibility` | enum | PUBLIC |
| Avatar | `avatar_visibility` | enum | PUBLIC |
| Cover Photo | `cover_photo_visibility` | enum | PUBLIC |
| Bio | `bio_visibility` | enum | PUBLIC |
| Description | `description_visibility` | enum | PUBLIC |
| Birthday | `birthday_visibility` | enum | PRIVATE |
| Gender | `gender_visibility` | enum | PRIVATE |
| Email | `email_visibility` | enum | PRIVATE |
| Phone | `phone_visibility` | enum | PRIVATE |
| Location | `location_visibility` | enum | FRIENDS_ONLY |
| Address | `address_visibility` | enum | PRIVATE |
| Media Gallery | `media_gallery_visibility` | enum | FRIENDS_ONLY |
| Personal Links | `personal_links_visibility` | enum | PUBLIC |
| Social Links | `social_links_visibility` | enum | PUBLIC |
| Blog Link | `show_blog_link` | enum | PUBLIC |
| Business Link | `show_business_link` | enum | PRIVATE |
| Default Posts | `default_post_visibility` | enum | PUBLIC |
| Friends List | `friends_list_visibility` | enum | FRIENDS_ONLY |
| Categories | `categories_visibility` | enum | FRIENDS_ONLY |
| Subscribed Blogs | `subscribed_blogs_visibility` | enum | FRIENDS_ONLY |
| Subscribed Communities | `subscribed_communities_visibility` | enum | FRIENDS_ONLY |
| Online Status | `show_online_status` | enum | FRIENDS_ONLY |
| Last Seen | `show_last_seen` | enum | FRIENDS_ONLY |
| Who Can Message | `who_can_message` | enum | FRIENDS_ONLY |
| Friend Requests | `who_can_send_friend_request` | enum | EVERYONE |

---

*Document created: 2026-02-17*  
*Based on privacy fields table with legal compliance*
