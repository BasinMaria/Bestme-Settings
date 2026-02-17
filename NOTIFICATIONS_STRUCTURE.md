# 🔔 Notifications / Уведомления

## Overview / Обзор

Complete detailed structure of the Notifications settings section for Bestme, including variable names, default values, options, and legal compliance notes.

Полная детальная структура раздела настроек Уведомлений для Bestme, включая имена переменных, значения по умолчанию, опции и юридические заметки.

---

## Structure / Структура

```
🔔 Notifications / Уведомления
│
├── Push Notifications / Push-уведомления
│   ├── Enable push notifications / Включить push-уведомления
│   │   └── Master control for all push notifications
│   │       Главный переключатель для всех push-уведомлений
│   │       Default: ON ✅
│   │       Variable: push_notifications_enabled
│   │       Options: ON, OFF
│   │       ⚠️ Legal: ePrivacy Directive (EU) - User consent required
│   │       [Master toggle ON/OFF] / [Главный переключатель Вкл/Выкл]
│   │
│   ├── Likes and Reactions / Лайки и реакции
│   │   └── When someone likes or reacts to your post
│   │       Когда кто-то лайкает или реагирует на пост
│   │       Default: ON ✅
│   │       Variable: notify_likes_reactions
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Comments / Комментарии
│   │   └── When someone comments on your post
│   │       Когда кто-то комментирует ваш пост
│   │       Default: ON ✅
│   │       Variable: notify_comments
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── New Followers / Новые подписчики
│   │   └── When someone follows you
│   │       Когда кто-то подписывается на вас
│   │       Default: ON ✅
│   │       Variable: notify_new_followers
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Messages / Сообщения
│   │   └── When you receive a new message
│   │       Когда получаете новое сообщение
│   │       Default: ON ✅
│   │       Variable: notify_messages
│   │       Options: ON, OFF
│   │       ⚠️ Note: Must respect user's messaging privacy settings
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Mentions and Tags / Упоминания и отметки
│   │   └── When someone @mentions or tags you
│   │       Когда кто-то @упоминает или отмечает вас
│   │       Default: ON ✅
│   │       Variable: notify_mentions_tags
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Friend Requests / Запросы в друзья
│   │   └── When someone sends you a friend request
│   │       Когда кто-то отправляет запрос в друзья
│   │       Default: ON ✅
│   │       Variable: notify_friend_requests
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Live Videos / Прямые эфиры
│       └── When people you follow go live
│           Когда люди, на которых вы подписаны, в эфире
│           Default: OFF
│           Variable: notify_live_videos
│           Options: ON, OFF
│           ⚠️ Note: OFF by default to avoid notification overload
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
├── Email Notifications / Email-уведомления
│   ├── Activity Summary / Сводка активности
│   │   └── Daily or weekly summary of activity
│   │       Ежедневная или еженедельная сводка активности
│   │       Default: WEEKLY ✅
│   │       Variable: email_activity_summary
│   │       Options: NEVER, DAILY, WEEKLY
│   │       ⚠️ Legal: CAN-SPAM Act (USA) - Must provide unsubscribe link
│   │       [Never / Daily / Weekly] / [Никогда / Ежедневно / Еженедельно]
│   │
│   ├── Reminder Emails / Письма-напоминания
│   │   └── Reminders about posts, friends, or events
│   │       Напоминания о постах, друзьях или событиях
│   │       Default: ON ✅
│   │       Variable: email_reminders
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Product Updates / Обновления продукта
│   │   └── News about new features and updates
│   │       Новости о новых функциях и обновлениях
│   │       Default: ON ✅
│   │       Variable: email_product_updates
│   │       Options: ON, OFF
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Newsletter / Новостная рассылка
│       └── Tips and inspiration
│           Советы и вдохновение
│           Default: OFF
│           Variable: email_newsletter
│           Options: ON, OFF
│           ⚠️ Legal: GDPR (EU) - Explicit opt-in required for marketing emails
│           ⚠️ Legal: CASL (Canada) - Express consent required
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── In-App Settings / Настройки в приложении
    ├── Sound / Звук
    │   └── Play sound for notifications
    │       Воспроизводить звук для уведомлений
    │       Default: ON ✅
    │       Variable: notification_sound_enabled
    │       Options: ON, OFF
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    ├── Vibration / Вибрация
    │   └── Vibrate for notifications
    │       Вибрация для уведомлений
    │       Default: ON ✅
    │       Variable: notification_vibration_enabled
    │       Options: ON, OFF
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    └── Badge Count / Счетчик значков
        └── Show number of unread notifications on app icon
            Показывать количество непрочитанных на иконке
            Default: ON ✅
            Variable: notification_badge_count
            Options: ON, OFF
            [Toggle ON/OFF] / [Вкл/Выкл]
```

---

## Variable Names Reference / Справочник имен переменных

### Push Notifications (8 variables)
```javascript
push_notifications_enabled: boolean          // Master toggle
notify_likes_reactions: boolean              // Likes and reactions
notify_comments: boolean                     // Comments
notify_new_followers: boolean                // New followers
notify_messages: boolean                     // Messages
notify_mentions_tags: boolean                // Mentions and tags
notify_friend_requests: boolean              // Friend requests
notify_live_videos: boolean                  // Live videos
```

### Email Notifications (4 variables)
```javascript
email_activity_summary: "NEVER" | "DAILY" | "WEEKLY"  // Activity summary
email_reminders: boolean                               // Reminder emails
email_product_updates: boolean                         // Product updates
email_newsletter: boolean                              // Newsletter
```

### In-App Settings (3 variables)
```javascript
notification_sound_enabled: boolean          // Sound
notification_vibration_enabled: boolean      // Vibration
notification_badge_count: boolean            // Badge count
```

---

## Default Values Summary / Сводка значений по умолчанию

### ON by default (13 settings) ✅
**Push Notifications:**
- Master toggle: ON
- Likes and Reactions: ON
- Comments: ON
- New Followers: ON
- Messages: ON
- Mentions and Tags: ON
- Friend Requests: ON

**Email Notifications:**
- Activity Summary: WEEKLY
- Reminder Emails: ON
- Product Updates: ON

**In-App Settings:**
- Sound: ON
- Vibration: ON
- Badge Count: ON

### OFF by default (2 settings)
- **Live Videos:** OFF (to avoid notification overload)
- **Newsletter:** OFF (requires explicit opt-in per GDPR)

---

## Legal Compliance / Юридическое соответствие

### ePrivacy Directive (EU)
⚠️ **Push Notifications:**
- User consent required before enabling push notifications
- Must provide easy opt-out mechanism
- Cannot enable without explicit permission

### GDPR (EU)
⚠️ **Newsletter:**
- Explicit opt-in required (cannot be pre-checked)
- Clear purpose statement needed
- Easy unsubscribe process
- Must honor withdrawal of consent

⚠️ **Marketing Communications:**
- Separate consent for each communication type
- Cannot bundle with terms of service
- Must keep records of consent

### CAN-SPAM Act (USA)
⚠️ **All Email Notifications:**
- Must include unsubscribe link in every email
- Must honor opt-out requests within 10 business days
- Must identify sender clearly
- Subject line must not be deceptive

### CASL (Canada)
⚠️ **Marketing Emails:**
- Express consent required for marketing emails
- Cannot use implied consent
- Must identify sender clearly
- Must provide unsubscribe mechanism

---

## User Experience Notes / Заметки по пользовательскому опыту

### Best Practices / Лучшие практики

1. **Default to ON for essential notifications:**
   - Friend requests, messages, comments
   - User expects these by default

2. **Default to OFF for high-frequency notifications:**
   - Live videos can create notification fatigue
   - Better to let users opt-in

3. **Provide granular control:**
   - Master toggle for quick on/off
   - Individual toggles for fine control

4. **Email frequency options:**
   - NEVER: No emails (except critical)
   - DAILY: For active users
   - WEEKLY: Good default balance

5. **Respect privacy settings:**
   - Notification settings must respect privacy controls
   - Don't notify if content is hidden by privacy settings

### Notification Hierarchy / Иерархия уведомлений

**Priority 1 (Always notify):**
- Friend requests
- Direct messages
- Mentions/Tags

**Priority 2 (Default ON):**
- Comments
- Likes and reactions
- New followers

**Priority 3 (Default OFF or WEEKLY):**
- Live videos
- Activity summary
- Newsletter

---

## Implementation Notes / Заметки по реализации

### Database Schema Example
```sql
CREATE TABLE user_notification_settings (
    user_id BIGINT PRIMARY KEY,
    
    -- Push Notifications
    push_notifications_enabled BOOLEAN DEFAULT true,
    notify_likes_reactions BOOLEAN DEFAULT true,
    notify_comments BOOLEAN DEFAULT true,
    notify_new_followers BOOLEAN DEFAULT true,
    notify_messages BOOLEAN DEFAULT true,
    notify_mentions_tags BOOLEAN DEFAULT true,
    notify_friend_requests BOOLEAN DEFAULT true,
    notify_live_videos BOOLEAN DEFAULT false,
    
    -- Email Notifications
    email_activity_summary VARCHAR(10) DEFAULT 'WEEKLY', -- NEVER, DAILY, WEEKLY
    email_reminders BOOLEAN DEFAULT true,
    email_product_updates BOOLEAN DEFAULT true,
    email_newsletter BOOLEAN DEFAULT false,
    
    -- In-App Settings
    notification_sound_enabled BOOLEAN DEFAULT true,
    notification_vibration_enabled BOOLEAN DEFAULT true,
    notification_badge_count BOOLEAN DEFAULT true,
    
    -- Audit fields
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### API Endpoint Example
```javascript
// GET /api/v1/users/{userId}/notification-settings
// PUT /api/v1/users/{userId}/notification-settings

{
  "pushNotifications": {
    "enabled": true,
    "likesReactions": true,
    "comments": true,
    "newFollowers": true,
    "messages": true,
    "mentionsTags": true,
    "friendRequests": true,
    "liveVideos": false
  },
  "emailNotifications": {
    "activitySummary": "WEEKLY",  // "NEVER" | "DAILY" | "WEEKLY"
    "reminders": true,
    "productUpdates": true,
    "newsletter": false
  },
  "inAppSettings": {
    "sound": true,
    "vibration": true,
    "badgeCount": true
  }
}
```

---

## Testing Checklist / Чек-лист тестирования

### Functional Testing
- [ ] Master toggle disables all push notifications
- [ ] Individual toggles work independently
- [ ] Email frequency changes take effect immediately
- [ ] Unsubscribe links work in all emails
- [ ] Badge count updates correctly
- [ ] Sound and vibration settings apply immediately

### Legal Compliance Testing
- [ ] Newsletter requires explicit opt-in (not pre-checked)
- [ ] All emails include unsubscribe link
- [ ] Unsubscribe honored within required timeframe
- [ ] Consent records maintained
- [ ] Privacy policy linked and accessible

### User Experience Testing
- [ ] Settings save without page reload
- [ ] Clear feedback when settings change
- [ ] Settings persist across devices (if synced)
- [ ] Performance: Settings page loads quickly
- [ ] Accessibility: All toggles keyboard-navigable

---

## Total: 15 Notification Settings

**8** Push notification types (including master)  
**4** Email notification types  
**3** In-app settings  

All settings documented with variables, defaults, options, and legal compliance notes.

Все настройки задокументированы с переменными, значениями по умолчанию, опциями и юридическими заметками.
