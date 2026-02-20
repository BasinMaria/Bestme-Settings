# Friends & Community Structure / Структура Друзья и сообщество

Complete social networking features for Bestme platform.

Полные функции социальных сетей для платформы Bestme.

---

## 👥 Friends & Community / Друзья и сообщество

### 1. Friends Management / Управление друзьями

#### Friends List / Список друзей
```
View all your friends
Посмотреть всех ваших друзей

Default: Shows all friends (245 friends example)
Variable: friends_list_view
Options: View, Search, Filter (Recent, Alphabetical)
Action: [View friends] / [Просмотреть друзей]
```

#### Add Friends / Добавить друзей
```
Search and send friend requests
Поиск и отправка запросов в друзья

Variable: friend_request_sent
Action: Search → Send Request → Pending
Options: Search by name, username, email
[Add friend] / [Добавить в друзья]
```

#### Remove Friends / Удалить из друзей
```
Remove someone from your friends list
Удалить кого-то из списка друзей

Variable: friend_removed
Action: Remove → Confirmation → Removed
Warning: They won't be notified
[Remove] / [Удалить]
```

#### Friend Requests / Запросы в друзья
```
Pending incoming friend requests
Входящие запросы в друзья

Variable: pending_friend_requests
Default: Shows pending requests
Actions: Accept, Decline, Ignore
[View requests] / [Просмотреть запросы]
```

#### Close Friends / Близкие друзья
```
Special list for sharing exclusive content
Особый список для эксклюзивного контента

Default: Empty list
Variable: close_friends_list
Options: Add to list, Remove from list
Note: Share exclusive content only with close friends
[Manage close friends] / [Управлять близкими друзьями]
```

---

### 2. Followers & Subscriptions / Подписчики и подписки

#### Your Followers / Ваши подписчики
```
People who follow you
Люди, которые подписаны на вас

Variable: followers_list
Shows: List of all followers
Default: Public count visible
Action: [View followers] / [Просмотреть подписчиков]
```

#### Your Following / Ваши подписки
```
People and accounts you follow
Люди и аккаунты, на которые вы подписаны

Variable: following_list
Shows: Users, Blogs, Business accounts you follow
Default: Shows all following
Action: [View following] / [Просмотреть подписки]
```

#### Manage Followers / Управление подписчиками
```
Remove or block followers
Удалить или заблокировать подписчиков

Variable: manage_followers
Actions:
  - Remove follower (soft removal)
  - Block follower (hard removal)
Note: Removed followers can follow again unless blocked
[Manage] / [Управлять]
```

#### Follow Requests / Запросы на подписку
```
Pending follow requests (for private accounts)
Ожидающие запросы на подписку (для приватных аккаунтов)

Variable: follow_requests_pending
Default: Empty if account is public
Actions: Approve, Decline
Note: Only relevant for private accounts
[View requests] / [Просмотреть запросы]
```

---

### 3. Subscriptions / Подписки

#### Blog Subscriptions / Подписки на блоги
```
All blogs you subscribe to
Все блоги, на которые вы подписаны

Default: Empty list
Variable: subscribed_blogs_list
Shows: Blog name, author, subscription date
Action: [View subscribed blogs] / [Просмотреть подписки на блоги]
```

#### Business Account Subscriptions / Подписки на бизнес-аккаунты
```
Business accounts you follow
Бизнес-аккаунты, на которые вы подписаны

Default: Empty list
Variable: subscribed_business_accounts
Shows: Business name, category, subscription date
Action: [View business subscriptions] / [Просмотреть бизнес-подписки]
```

#### Unsubscribe Management / Управление отписками
```
Unsubscribe from blogs or business accounts
Отписаться от блогов или бизнес-аккаунтов

Variable: unsubscribe_action
Action: Select → Confirm → Unsubscribed
Note: You can always re-subscribe later
[Unsubscribe] / [Отписаться]
```

---

### 4. Communities / Сообщества

#### My Communities / Мои сообщества
```
Communities you have joined
Сообщества, к которым вы присоединились

Default: Empty list
Variable: my_communities_list
Shows: Community name, type (Open/Closed/Private), members count
Action: [View my communities] / [Просмотреть мои сообщества]
```

#### Create Community / Создать сообщество
```
Create a new community
Создать новое сообщество

Variable: create_community_action
Action: Create new community
Options:
  - Open Community / Открытое (anyone can join)
  - Closed Community / Закрытое (request to join)
  - Private Community / Приватное (invite only)
Required: Name, Description, Category, Rules
[Create community] / [Создать сообщество]
```

#### Community Invitations / Приглашения в сообщества
```
Pending community invitations
Ожидающие приглашения в сообщества

Default: Empty
Variable: community_invitations_pending
Shows: Community name, who invited you, date
Actions: Accept, Decline
[View invitations] / [Просмотреть приглашения]
```

#### Manage Communities / Управление сообществами
```
Admin tools for communities you own or moderate
Инструменты администратора для ваших сообществ

Variable: manage_community_settings
Available for: Community owners and moderators
Actions:
  - Edit community info
  - Invite members
  - Remove members
  - Moderate content
  - Delete community
[Manage] / [Управлять]
```

#### Leave Community / Покинуть сообщество
```
Leave a community you joined
Покинуть сообщество

Variable: leave_community_action
Action: Select community → Confirm → Leave
Warning: You will lose access to community content
Note: Can rejoin if community allows
[Leave] / [Покинуть]
```

---

### 5. Network Search & Discovery / Поиск и открытие

#### Find Friends / Найти друзей
```
Search for people to connect with
Поиск людей для общения

Variable: find_friends_search
Search by:
  - Name / Имя
  - Username / Имя пользователя
  - Email / Email (if shared)
Action: [Search] / [Поиск]
```

#### Discover People / Открыть для себя людей
```
AI-powered suggestions based on your network
Предложения на основе AI и вашей сети

Default: Enabled ✅
Variable: discover_people_suggestions
Based on:
  - Mutual friends
  - Shared interests (categories)
  - Similar communities
  - Location (if shared)
Action: [Discover] / [Открыть]
```

#### Suggested Communities / Рекомендуемые сообщества
```
Communities based on your interests
Сообщества на основе ваших интересов

Default: Enabled ✅
Variable: suggested_communities
Based on:
  - Categories you follow
  - Friends' communities
  - Popular communities in your region
Action: [View suggestions] / [Просмотреть рекомендации]
```

#### Suggested Blogs / Рекомендуемые блоги
```
Blogs based on your reading history
Блоги на основе вашей истории чтения

Default: Enabled ✅
Variable: suggested_blogs
Based on:
  - Reading history
  - Categories you follow
  - Similar users' subscriptions
Action: [View suggestions] / [Просмотреть рекомендации]
```

---

### 6. Suggestions & Recommendations / Предложения и рекомендации

#### Friend Suggestions / Предложения в друзья
```
Suggestions for people you might know
Предложения людей, которых вы можете знать

Default: ON ✅
Variable: friend_suggestions_enabled
Options: ON, OFF
Based on:
  - Mutual friends
  - Network connections
  - Shared communities
  - Contact sync (if allowed)
[Toggle ON/OFF] / [Вкл/Выкл]
```

#### Hide Suggestions / Скрыть предложения
```
Turn off all suggestions and recommendations
Отключить все предложения и рекомендации

Default: OFF
Variable: hide_suggestions
Options: ON, OFF
Note: When ON, disables all discovery features
Warning: You won't see friend/community/blog suggestions
[Toggle ON/OFF] / [Вкл/Выкл]
```

---

## Variable Names Reference / Справочник переменных

### Friends Management (5 variables)
```javascript
friends_list_view: string // "all" | "recent" | "alphabetical"
friend_request_sent: boolean
friend_removed: boolean
pending_friend_requests: number
close_friends_list: string[] // Array of user IDs
```

### Followers & Subscriptions (4 variables)
```javascript
followers_list: string[] // Array of user IDs
following_list: string[] // Array of user/account IDs
manage_followers: string // "remove" | "block"
follow_requests_pending: string[] // Array of user IDs (private accounts only)
```

### Subscriptions (3 variables)
```javascript
subscribed_blogs_list: string[] // Array of blog IDs
subscribed_business_accounts: string[] // Array of business account IDs
unsubscribe_action: string // blog_id or business_id to unsubscribe
```

### Communities (5 variables)
```javascript
my_communities_list: string[] // Array of community IDs
create_community_action: object // {name, description, type, category, rules}
community_invitations_pending: string[] // Array of community IDs
manage_community_settings: string // community_id to manage
leave_community_action: string // community_id to leave
```

### Network Search & Discovery (4 variables)
```javascript
find_friends_search: string // Search query
discover_people_suggestions: boolean // Default: true
suggested_communities: boolean // Default: true
suggested_blogs: boolean // Default: true
```

### Suggestions (2 variables)
```javascript
friend_suggestions_enabled: boolean // Default: true
hide_suggestions: boolean // Default: false
```

---

## Default Values Summary / Сводка значений по умолчанию

### Enabled by Default (5 settings)
- `discover_people_suggestions`: true ✅
- `suggested_communities`: true ✅
- `suggested_blogs`: true ✅
- `friend_suggestions_enabled`: true ✅

### Disabled by Default (1 setting)
- `hide_suggestions`: false

### Empty by Default (Lists)
- `close_friends_list`: []
- `subscribed_blogs_list`: []
- `subscribed_business_accounts`: []
- `my_communities_list`: []
- `community_invitations_pending`: []

---

## User Flow Examples / Примеры пользовательского потока

### Adding a Friend
```
1. Settings → Friends & Community
2. Friends Management → Add Friends
3. Search by name/username
4. Click "Add Friend"
5. Request sent → Pending
6. When accepted → Appears in Friends List
```

### Subscribing to a Blog
```
1. Discover blog (in Blogs section or Suggested Blogs)
2. Click "Subscribe"
3. Blog added to Subscribed Blogs list
4. Receive notifications (if enabled)
```

### Creating a Community
```
1. Settings → Friends & Community
2. Communities → Create Community
3. Fill: Name, Description, Category
4. Choose type: Open/Closed/Private
5. Set rules
6. Click "Create"
7. Community created → You're admin
```

### Managing Followers
```
1. Settings → Friends & Community
2. Followers & Subscriptions → Your Followers
3. Select follower
4. Options: Remove or Block
5. Confirm action
```

---

## Legal & Privacy Notes / Юридические заметки

### GDPR Compliance
- ⚠️ Social connections = personal data (GDPR Art. 6)
- Users must be able to export friend lists
- Users must be able to delete all connections
- Clear explanation of how suggestions work

### Privacy Considerations
- Mutual friends always visible (transparency law)
- Users control who sees their friends list
- Users control who can send friend requests
- Clear opt-out for all suggestions

### Data Retention
- Removed friends: Connection history retained for 30 days (undo option)
- Deleted connections: Permanent deletion after 30 days
- Community memberships: History retained while member

---

## Implementation Notes / Заметки по реализации

### Database Schema Suggestion
```sql
-- Friends relationships
friends (user_id, friend_id, status, created_at)
-- Followers
followers (user_id, follower_id, created_at)
-- Following (users, blogs, business)
following (user_id, target_id, target_type, created_at)
-- Communities
community_members (community_id, user_id, role, joined_at)
-- Subscriptions
subscriptions (user_id, target_id, type, subscribed_at)
```

### API Endpoints Suggestion
```
GET /api/friends
POST /api/friends/request
DELETE /api/friends/{friend_id}
GET /api/followers
GET /api/following
POST /api/subscribe/{target_id}
DELETE /api/unsubscribe/{target_id}
GET /api/communities/mine
POST /api/communities/create
POST /api/communities/{id}/join
DELETE /api/communities/{id}/leave
```

---

## Total Features Summary / Общая сводка функций

**Friends & Community includes:**
- 23 distinct features
- 23 variables for developers
- 6 main feature groups
- Full bilingual support (English / Russian)
- Legal compliance notes
- Default values specified
- User flows documented
- Implementation suggestions

All social networking features for Bestme are now documented!
Все функции социальных сетей для Bestme теперь задокументированы!
