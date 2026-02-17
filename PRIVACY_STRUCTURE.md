# Privacy Settings Structure / Структура настроек приватности
# Bestme Social App

*Date: 2026-02-17*

---

## 🔒 Privacy / Приватность

Complete privacy settings structure with legal compliance.

---

```
🔒 Privacy / Приватность
│
├── Profile Visibility / Видимость профиля
│   ├── Profile Page / Страница профиля
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: Minimum metadata visible (GDPR Art. 15)
│   │
│   ├── Name / Имя
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: Minimum "First name + Initial" must be visible (GDPR transparency)
│   │       Visibility:
│   │       • PUBLIC: Full name to everyone
│   │       • FRIENDS_ONLY: Full name to friends, First+Initial to others
│   │       • PRIVATE: First name only to everyone
│   │
│   ├── Avatar Photo / Фото профиля
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       Visibility:
│   │       • PUBLIC: Show to everyone
│   │       • FRIENDS_ONLY: Placeholder to non-friends
│   │       • PRIVATE: Placeholder to non-friends
│   │
│   ├── Cover Photo / Обложка
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       Visibility:
│   │       • PUBLIC: Show to everyone
│   │       • FRIENDS_ONLY: Placeholder to non-friends
│   │       • PRIVATE: Placeholder to non-friends
│   │
│   ├── Bio / About / О себе
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Description / Описание
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Birthday / День рождения
│   │   └── Default: PRIVATE
│   │       Options: PUBLIC_FULL, PUBLIC_AGE, FRIENDS_FULL, FRIENDS_AGE, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Must default to PRIVATE
│   │       ⚠️ Always stored in DB for COPPA age check (13+)
│   │       Visibility:
│   │       • PUBLIC_FULL: Full date to everyone
│   │       • PUBLIC_AGE: Age only to everyone
│   │       • FRIENDS_FULL: Full date to friends only
│   │       • FRIENDS_AGE: Age only to friends
│   │       • PRIVATE: Hidden from everyone
│   │
│   └── Gender / Пол
│       └── Default: PRIVATE
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Legal: GDPR Art. 9 - Sensitive personal data
│
├── Contact Visibility / Видимость контактов
│   ├── Email / Электронная почта
│   │   └── Default: PRIVATE
│   │       Options: FRIENDS_ONLY, PRIVATE (NO PUBLIC option)
│   │       ⚠️ Legal: GDPR + CAN-SPAM (USA) + CASL (Canada)
│   │       ⚠️ FORBIDDEN to make PUBLIC
│   │
│   ├── Phone / Телефон
│   │   └── Default: PRIVATE
│   │       Options: FRIENDS_ONLY, PRIVATE (NO PUBLIC option)
│   │       ⚠️ Legal: GDPR + TCPA (USA) + PIPEDA (Canada)
│   │       ⚠️ FORBIDDEN to make PUBLIC
│   │
│   ├── Location / Местоположение
│   │   └── Default: FRIENDS_ONLY
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Location data
│   │
│   └── Address / Адрес
│       └── Default: PRIVATE
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Legal: GDPR Art. 9 - Precise location = sensitive data
│
├── Content & Links Visibility / Видимость контента и ссылок
│   ├── Media Gallery / Галерея медиа
│   │   └── Default: FRIENDS_ONLY
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Photos can contain faces, children, locations
│   │
│   ├── Personal Links / Личные ссылки
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Social Media Links / Ссылки на соцсети
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Blog Link / Ссылка на блог
│   │   └── Default: PUBLIC
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │
│   ├── Business Link / Ссылка на бизнес
│   │   └── Default: PRIVATE
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 6 - Business ownership = personal data
│   │
│   └── Default Post Visibility / Видимость постов по умолчанию
│       └── Default: PUBLIC
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Note: User MUST control each post individually (GDPR)
│
├── Friends & Community / Друзья и сообщество
│   ├── Friends List / Список друзей
│   │   └── Default: FRIENDS_ONLY
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: Mutual friends MUST always be visible
│   │       Visibility:
│   │       • PUBLIC: Full list to everyone
│   │       • FRIENDS_ONLY: Full list to friends, Mutual only to others
│   │       • PRIVATE: Mutual friends only to everyone
│   │
│   ├── Categories / Интересы (категории)
│   │   └── Default: FRIENDS_ONLY
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Can reveal religion, politics, orientation
│   │
│   ├── Subscribed Blogs / Подписки на блоги
│   │   └── Default: FRIENDS_ONLY
│   │       Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│   │       ⚠️ Legal: GDPR Art. 9 - Can reveal political/religious views
│   │
│   └── Subscribed Communities / Подписки на сообщества
│       └── Default: FRIENDS_ONLY
│           Options: PUBLIC, FRIENDS_ONLY, PRIVATE
│           ⚠️ Legal: GDPR Art. 9 - Can reveal sensitive interests
│
├── Activity & Status / Активность и статус
│   ├── Online Status / Онлайн статус
│   │   └── Default: FRIENDS_ONLY
│   │       Options: EVERYONE, FRIENDS_ONLY, NOBODY
│   │       ⚠️ Legal: GDPR Art. 9 - Behavioral tracking data
│   │
│   └── Last Seen / Последний раз в сети
│       └── Default: FRIENDS_ONLY
│           Options: EVERYONE, FRIENDS_ONLY, NOBODY
│           ⚠️ Legal: GDPR Art. 9 - Activity tracking data
│
└── Interactions / Взаимодействия
    ├── Who Can Send Messages / Кто может писать сообщения
    │   └── Default: FRIENDS_ONLY
    │       Options: EVERYONE, FRIENDS_ONLY, FRIENDS_OF_FRIENDS, NOBODY
    │       ⚠️ Legal: ePrivacy Directive + GDPR
    │       ⚠️ Recommended: FRIENDS_ONLY (Privacy by Default)
    │
    └── Who Can Send Friend Request / Кто может отправлять запросы в друзья
        └── Default: EVERYONE
            Options: EVERYONE, FRIENDS_OF_FRIENDS, NOBODY
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
