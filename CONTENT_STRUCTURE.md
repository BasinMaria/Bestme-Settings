# 💬 Content & Interactions / Контент и взаимодействия

Complete structure for Content & Interactions settings section in Bestme.

Полная структура раздела настроек Контента и взаимодействий в Bestme.

---

## Structure / Структура

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
├── Stories Settings / Настройки историй
│   ├── Allow Story Sharing / Разрешить делиться историями
│   │   └── Let others share your stories to their stories
│   │       Позволить другим делиться вашими историями
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Hide Stories From / Скрыть истории от
│   │   └── Choose specific people who won't see your stories
│   │       Выбрать людей, которые не увидят ваши истории
│   │       [Select users] / [Выбрать пользователей]
│   │
│   ├── Save to Archive / Сохранять в архив
│   │   └── Automatically save stories to your private archive
│   │       Автоматически сохранять истории в личный архив
│   │       [Toggle ON/OFF] ✅ (default ON)
│   │
│   └── Story Duration / Длительность истории
│       └── How long stories stay visible (24 hours default)
│           Как долго видны истории (24 часа по умолчанию)
│
├── Saved & Collections / Сохраненное и коллекции
│   ├── Saved Posts / Сохраненные посты
│   │   └── Posts you've bookmarked
│   │       Посты, которые вы сохранили
│   │       [View saved] / [Просмотреть сохраненное]
│   │
│   ├── Collections / Коллекции
│   │   └── Organize saved posts into collections
│   │       Организовать сохраненное в коллекции
│   │       [Manage collections] / [Управлять коллекциями]
│   │
│   └── Saved Stories / Сохраненные истории
│       └── Stories you've saved from others
│           Истории, которые вы сохранили от других
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

---

## Detailed Breakdown / Детальная разбивка

### 1. Posts Settings / Настройки постов

Settings that control how your posts behave and appear.

Настройки, которые контролируют поведение и отображение постов.

#### Default Audience / Аудитория по умолчанию
- **Type:** Selection (3 options)
- **Options:** Public, Friends, Only Me
- **Default:** Public or Friends (user's choice)
- **Variable:** `default_post_visibility`
- **Description:** Choose who can see your posts by default. You can still change this for each individual post.
- **Описание:** Выберите, кто видит ваши посты по умолчанию. Вы всё равно можете менять это для каждого поста отдельно.

#### Auto-Archive Posts / Автоархивация постов
- **Type:** Toggle (ON/OFF)
- **Default:** OFF
- **Variable:** `auto_archive_posts`
- **Description:** Automatically move posts to archive after 30 days. Archived posts are hidden from your profile but you can view them anytime.
- **Описание:** Автоматически переносить посты в архив через 30 дней. Архивные посты скрыты из профиля, но вы можете просмотреть их в любое время.

#### Hide Likes Count / Скрыть счетчик лайков
- **Type:** Toggle (ON/OFF)
- **Default:** OFF
- **Variable:** `hide_likes_count`
- **Description:** Hide the number of likes on your posts from others. You'll still see the count.
- **Описание:** Скрыть количество лайков на ваших постах от других. Вы по-прежнему будете видеть счётчик.

---

### 2. Stories Settings / Настройки историй

Control how your stories are shared, viewed, and saved.

Контроль того, как ваши истории публикуются, просматриваются и сохраняются.

#### Allow Story Sharing / Разрешить делиться историями
- **Type:** Toggle (ON/OFF)
- **Default:** ON
- **Variable:** `allow_story_sharing`
- **Description:** Let others share your stories to their own stories.
- **Описание:** Разрешить другим делиться вашими историями в своих историях.

#### Hide Stories From / Скрыть истории от
- **Type:** User selection
- **Default:** None (empty list)
- **Variable:** `hide_stories_from`
- **Description:** Select specific people who won't be able to see your stories.
- **Описание:** Выберите конкретных людей, которые не смогут видеть ваши истории.

#### Save to Archive / Сохранять в архив
- **Type:** Toggle (ON/OFF)
- **Default:** ON ✅
- **Variable:** `save_stories_to_archive`
- **Description:** Automatically save all your stories to a private archive after they expire (24 hours).
- **Описание:** Автоматически сохранять все ваши истории в личный архив после истечения срока (24 часа).

#### Story Duration / Длительность истории
- **Type:** Display info (not changeable in v1)
- **Default:** 24 hours
- **Description:** Stories are visible for 24 hours before they disappear (standard across social networks).
- **Описание:** Истории видны в течение 24 часов, прежде чем исчезнут (стандарт для соцсетей).

---

### 3. Saved & Collections / Сохраненное и коллекции

Manage your saved content and organize it into collections.

Управляйте сохранённым контентом и организуйте его в коллекции.

#### Saved Posts / Сохраненные посты
- **Type:** View/Management
- **Action:** [View saved] / [Просмотреть сохраненное]
- **Description:** View all posts you've bookmarked for later.
- **Описание:** Просмотреть все посты, которые вы сохранили на потом.

#### Collections / Коллекции
- **Type:** Management interface
- **Action:** [Manage collections] / [Управлять коллекциями]
- **Description:** Create themed collections to organize your saved posts (e.g., "Recipes", "Workouts", "Travel").
- **Описание:** Создавайте тематические коллекции для организации сохранённых постов (напр., "Рецепты", "Тренировки", "Путешествия").

#### Saved Stories / Сохраненные истории
- **Type:** View/Management
- **Action:** [View saved stories] / [Просмотреть сохранённые истории]
- **Description:** Stories you've saved from other users before they expired.
- **Описание:** Истории, которые вы сохранили от других пользователей до их истечения.

---

### 4. Media Settings / Настройки медиа

Control how photos and videos are uploaded and played.

Контроль загрузки и воспроизведения фото и видео.

#### Upload Quality / Качество загрузки
- **Type:** Selection (2 options)
- **Options:**
  - High Quality (uses more data) / Высокое качество (больше данных)
  - Data Saver ✅ (compressed, faster) / Экономия данных (сжато, быстрее)
- **Default:** Data Saver ✅
- **Variable:** `upload_quality`
- **Description:** Choose between high quality uploads or compressed uploads that save mobile data.
- **Описание:** Выберите между высоким качеством загрузки или сжатыми загрузками, которые экономят мобильные данные.

#### Auto-Play Videos / Автовоспроизведение видео
- **Type:** Selection (3 options)
- **Options:**
  - Always / Всегда
  - Wi-Fi Only ✅ (default) / Только Wi-Fi
  - Never / Никогда
- **Default:** Wi-Fi Only ✅
- **Variable:** `auto_play_videos`
- **Description:** Control when videos automatically start playing in your feed.
- **Описание:** Контролируйте, когда видео автоматически начинают воспроизводиться в ленте.

#### HD Video / HD-видео
- **Type:** Toggle (ON/OFF)
- **Default:** OFF
- **Variable:** `upload_hd_video`
- **Description:** Upload videos in high definition. Uses more storage and data.
- **Описание:** Загружать видео в высоком разрешении. Использует больше места и данных.
- **Note:** May require additional storage permissions.

---

### 5. Feed Preferences / Настройки ленты

Customize what you see in your main feed.

Настройте, что вы видите в основной ленте.

#### Show Suggested Posts / Показывать рекомендации
- **Type:** Toggle (ON/OFF)
- **Default:** ON ✅
- **Variable:** `show_suggested_posts`
- **Description:** See posts from accounts you don't follow, based on your interests.
- **Описание:** Видеть посты от аккаунтов, на которые вы не подписаны, на основе ваших интересов.

#### Sensitive Content / Чувствительный контент
- **Type:** Selection (3 options)
- **Options:**
  - Allow / Разрешить - See all content
  - Limit / Ограничить - Filter some sensitive content ✅ (default)
  - Hide / Скрыть - Hide all sensitive content
- **Default:** Limit ✅
- **Variable:** `sensitive_content_filter`
- **Description:** Control how much sensitive or potentially disturbing content you see.
- **Описание:** Контролируйте, сколько чувствительного или потенциально беспокоящего контента вы видите.
- **Legal Note:** Required by many jurisdictions to protect users from harmful content.

#### Favorite Accounts / Избранные аккаунты
- **Type:** User selection list
- **Action:** [Add favorites] / [Добавить избранных]
- **Variable:** `favorite_accounts`
- **Description:** Mark specific accounts as favorites to see their posts first in your feed.
- **Описание:** Отметьте конкретные аккаунты как избранные, чтобы видеть их посты первыми в ленте.

---

## User Flow / Пользовательский поток

### Accessing Content Settings / Доступ к настройкам контента

1. Open Settings / Открыть настройки
2. Tap "Content & Interactions" / Нажать "Контент и взаимодействия"
3. Choose subsection (Posts, Stories, Saved, Media, Feed)
4. Adjust settings as needed
5. Changes save automatically

### Typical Use Cases / Типичные случаи использования

**Privacy-conscious user / Приватный пользователь:**
- Set default audience to "Friends"
- Hide likes count
- Disable suggested posts
- Filter sensitive content

**Content creator / Создатель контента:**
- Keep audience on "Public"
- Enable story sharing
- Use high quality uploads
- Show suggested posts for discovery

**Data-conscious user / Экономный пользователь:**
- Use Data Saver upload quality
- Set auto-play to "Wi-Fi Only" or "Never"
- Disable HD video uploads

---

## Default Settings Summary / Сводка настроек по умолчанию

| Setting / Настройка | Default / По умолчанию | Reason / Причина |
|---------------------|------------------------|------------------|
| Default Audience | Public/Friends (user choice) | User preference |
| Auto-Archive Posts | OFF | User control |
| Hide Likes Count | OFF | Social engagement |
| Allow Story Sharing | ON | Viral content spread |
| Save Stories to Archive | ON ✅ | Memory preservation |
| Upload Quality | Data Saver ✅ | Mobile data saving |
| Auto-Play Videos | Wi-Fi Only ✅ | Data savings |
| HD Video | OFF | Storage/data savings |
| Show Suggested Posts | ON ✅ | Content discovery |
| Sensitive Content | Limit ✅ | User protection |

---

## Developer Reference / Справочник разработчика

### Variable Names / Имена переменных

```javascript
// Posts Settings
default_post_visibility: "PUBLIC" | "FRIENDS" | "ONLY_ME"
auto_archive_posts: boolean
hide_likes_count: boolean

// Stories Settings
allow_story_sharing: boolean
hide_stories_from: string[] // array of user IDs
save_stories_to_archive: boolean
story_duration: number // hours (fixed at 24)

// Saved & Collections
saved_posts: string[] // array of post IDs
collections: Collection[] // array of collection objects
saved_stories: string[] // array of story IDs

// Media Settings
upload_quality: "HIGH" | "DATA_SAVER"
auto_play_videos: "ALWAYS" | "WIFI_ONLY" | "NEVER"
upload_hd_video: boolean

// Feed Preferences
show_suggested_posts: boolean
sensitive_content_filter: "ALLOW" | "LIMIT" | "HIDE"
favorite_accounts: string[] // array of user IDs
```

### Storage Considerations / Соображения хранения

- **Collections:** Store as separate table with user_id, collection_name, post_ids[]
- **Favorites:** Index for fast feed sorting
- **Hide Stories From:** Efficient lookup for story visibility checks
- **Saved Content:** Archive old saved posts after 1 year (user notification)

---

## Legal & Compliance / Юридические вопросы

### Data Protection / Защита данных

**GDPR Compliance:**
- ✅ User controls their content visibility (Article 6)
- ✅ Saved content is exportable (Article 20)
- ✅ Can delete saved content (Article 17)

**Child Safety:**
- ⚠️ Sensitive content filter required for users under 18
- ⚠️ Default to "Hide" for minors

### Content Moderation / Модерация контента

**Required Features:**
- Sensitive content filtering
- Ability to hide stories from specific users
- Report mechanisms (linked from Help & Support)

---

## Related Settings / Связанные настройки

**Also see / См. также:**
- Privacy > Content Visibility - Control who sees your content
- Privacy > Interactions - Control who can interact with your content
- Notifications > Push Notifications - Get notified about content interactions
- Account > Data Management - Download your content

---

## Future Enhancements / Будущие улучшения

**Potential additions (not in v1):**
- Post scheduling
- Story highlights (permanent story collections)
- Advanced analytics for posts
- Content moderation preferences
- Custom story duration options
- Collaborative collections
- Cross-posting to other platforms

---

**Last Updated:** 2026-02-17  
**Version:** 1.0  
**Status:** Production Ready / Готово к продакшену
