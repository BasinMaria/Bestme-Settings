# Bestme — ТЗ настроек личного профиля
## Полная структура L1 → L2 → L3 со всеми юридическими основаниями

> **Обозначения:**
> ⚖️ = обязательно по закону (нарушение → штраф или отказ в публикации)
> 💡 = рекомендация (UX-норма, лучшие практики)
> 🔴 = критичный блокер публикации
> 🟡 = важно до значительного роста
> 🟢 = рекомендация (улучшает доверие)

---

## РАЗДЕЛ A. ЧТО НУЖНО ДОБАВИТЬ В ПРИЛОЖЕНИЕ

### 🔴 Критично — без этого публикация невозможна

| # | Что добавить | Закон / Правило |
|---|---|---|
| 🔴 1 | **Веб-форма удаления аккаунта** (не только in-app, отдельная страница на сайте) | Google Play Developer Policy (обязательно с 2024) |
| 🔴 2 | **Блок регистрации для пользователей < 13 лет** (жёсткая возрастная верификация при signup) | COPPA (США) · DSA Art.28 (ЕС) |
| 🔴 3 | **Кнопка «Do Not Sell My Personal Information»** в разделе Your Data | CCPA/CPRA §1798.120 (Калифорния) |
| 🔴 4 | **Pre-checked boxes = пустые** во всех формах opt-in (email, push, SMS) | CASL (Канада) · ePrivacy Directive Art.13 (ЕС) |
| 🔴 5 | **Accessibility раздел** в настройках (текст, контраст, субтитры, screen reader) | EAA Directive 2019/882 (ЕС, с 28 июня 2025) · ADA (США) · Israel Disability Law 5758-1998 · AODA (Канада) · App Store 2.5.4 · Google Play |
| 🔴 6 | **Art.17(2) де-индексация**: при Delete account — автоматический запрос удаления URL в Google Search Console + Yandex.Webmaster + Bing (если был seo_indexable = ON) | GDPR Art.17(2) (ЕС) — штраф до 20 млн € |
| 🔴 7 | **Onboarding disclosure**: при регистрации взрослых (18+) — явное уведомление о том, что профиль будет публичным | GDPR Art.25(2) (ЕС) — условие законности открытого профиля по умолчанию |
| 🔴 8 | **UGC ToS acceptance**: модаль «Принять правила сообщества» при первом создании контента (пост, комментарий, загрузка фото) | Google Play UGC Policy · Apple App Store §1.2 |
| 🔴 9 | **Child Safety Standards**: (a) запрет CSAE в Terms of Use/Community Guidelines; (b) категория «Child Safety» в Report a problem; (c) публичный email childsafety@bestme.com в Help & Support | Google Play Child Safety Standards Policy (5 обязательных пунктов) · COPPA |
| 🔴 10 | **App Tracking Transparency (ATT) диалог** (iOS 14.5+) — если используются аналитические или рекламные SDK | Apple App Store §5.1.2(i) — без этого автоматический отказ в ревью |
| 🔴 11 | **Prominent Disclosure**: in-app экран объяснения сбора данных ДО запроса Push / Camera / Photos (не только в Privacy Policy) | Google Play User Data Policy — Prominent Disclosure & Consent |
| 🔴 12 | **SMS consent checkbox** (при добавлении телефона): явный текст «Я соглашаюсь получать SMS от Bestme... Для отписки ответьте STOP» | TCPA 47 U.S.C. §227 — штраф $1 500 за каждое SMS без письменного согласия |
| 🔴 13 | **Кнопка «Отключить»** для каждого 3rd-party login-провайдера (Google, Facebook и т.д.) в Login & Security | Apple App Store §5.1.1(v) |

### 🟡 Важно — до первого значительного роста аудитории

| # | Что добавить | Закон / Правило |
|---|---|---|
| 🟡 8 | **Ограничение обработки данных** (Restrict Processing) — заморозить без удаления | GDPR Art.18 (ЕС) |
| 🟡 9 | **One-click unsubscribe** в каждом email-письме (ссылка отписки работает ≤ 10 дней) | CASL (Канада) · CAN-SPAM (США) · ePrivacy Art.13(2) (ЕС) |
| 🟡 10 | **Объяснение алгоритма рекомендаций** — ссылка / поп-ап «почему я вижу этот контент» | DSA Art.27 (ЕС) |
| 🟡 11 | **Chief Privacy Officer / DPO контакт** — публично виден в приложении | Quebec Law 25 Art.5 (Канада) · GDPR Art.37–39 (ЕС) |
| 🟡 12 | **«Почему я вижу эту рекламу»** — ссылка объяснения к каждому рекламному блоку | DSA Art.26 (ЕС) |
| 🟡 13 | **Право на пересмотр автоматического решения** (human review запрос) | GDPR Art.22 · Quebec L25 Art.8.1 · CPRA §1798.185 |
| 🟡 14 | **Физический адрес организации** в footer каждого email-письма | CAN-SPAM (США) |
| 🟡 15 | **Storage period policy**: в Your Data указать срок хранения данных при деактивации и после удаления | GDPR Art.25(2) (ЕС) |
| 🟡 16 | **Delete account UX**: пояснение о де-индексации («до 30 дней») в модальном окне | GDPR Art.17(2) (ЕС) |

### 🟢 Рекомендации — до масштабирования

| # | Что добавить | Закон / Правило |
|---|---|---|
| 🟢 13 | Privacy Nutrition Labels заполнены в App Store Connect | Apple App Store Guidelines |
| 🟢 14 | Data Safety Form заполнена в Google Play Console | Google Play Developer Policy |
| 🟢 15 | Privacy Impact Assessment (PIA) для новых функций | Quebec Law 25 Art.3.2 · GDPR Art.35 |
| 🟢 16 | Регистрация базы данных в Реестре баз данных Израиля | Israel PPL Sec.8 (для >10 000 субъектов) |
| 🟢 17 | Pre-permission screen перед запросом системных разрешений | Google Play Prominent Disclosure Policy |

---

## РАЗДЕЛ B. ПОЛНАЯ СТРУКТУРА НАСТРОЕК L1 → L2 → L3

---

### 1️⃣ 👤 ACCOUNT — Аккаунт
**Обоснование:** ⚖️ App Store 5.1.1 · Google Play · GDPR Art.17 — управление аккаунтом обязательно

#### L2: Основная информация профиля

| L3 — Пункт | Тип элемента | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Profile photo | Действие (загрузить / удалить) | — | 💡 | — |
| Display name | Текстовое поле | — | 💡 | — |
| Username / @handle | Текстовое поле (уникальный) | — | 💡 | — |
| Email address | Текстовое поле | — | ⚖️ | GDPR — контактные данные |
| Phone number | Текстовое поле | — | ⚖️ | GDPR · TCPA — контактные данные |
| Date of birth | Дата | — | ⚖️ | COPPA (возраст < 13) · GDPR Art.8 · DSA Art.28 |
| Gender | Выбор (ENUM + не указывать) | Не указано | 💡 | — |
| Language | Выбор из списка | System | 💡 | — |
| Country / Region | Выбор | — | ⚖️ | GDPR — применимое право |
| Bio / About | Текстовое поле | — | 💡 | — |

#### L2: Управление аккаунтом

| L3 — Пункт | Тип элемента | ⚖️/💡 | Закон |
|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация) | ⚖️ | GDPR Art.17 |
| **Delete account** | Действие (постоянное удаление + подтверждение) | ⚖️ | GDPR Art.17 · CCPA §1798.105 · App Store 5.1.1(v) · Google Play |
| Switch to Business profile | Действие | 💡 | — |

> ⚠️ **App Store + Google Play**: ссылка на удаление аккаунта должна быть доступна ПРЯМО из настроек — без этого отказ в публикации
> ⚠️ **Google Play** (дополнительно): должна существовать **веб-форма** удаления аккаунта (не только in-app)
> ❌ **GDPR Art.17(2)** — при Delete account: необходимо автоматически запросить де-индексацию в Google Search Console + Yandex.Webmaster + Bing (если `seo_indexable` был включён). UX: модальное окно при удалении должно содержать пояснение «Ваш профиль будет удалён из поисковых систем в течение 30 дней». Подробнее → `GDPRArt25Art17AuditSpec.md` §2.2

---

### 2️⃣ 🔒 PRIVACY & VISIBILITY — Приватность и видимость
**Обоснование:** ⚖️ GDPR Art.25 — Privacy by Default (все настройки = наиболее строгие по умолчанию)

#### L2: Account Privacy — Приватность аккаунта

> Приложение **только для 18+** — единый набор дефолтов, возрастных развилок нет.

| L3 — Настройка | variable_name | Тип | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|---|
| Private account | `account_private` | Toggle On/Off | `OFF` (открытый) | ⚖️ | GDPR Art.25 — открытый профиль законен для 18+ |
| Profile in search results | `profile_searchable` | Toggle On/Off | `ON` | ⚖️ | GDPR Art.17 (право на забвение = opt-out доступен) |
| SEO indexing (Google, Yandex) | `seo_indexable` | Toggle On/Off | **`OFF`** | ⚖️ | GDPR Art.25 — **СТРОГО OFF** по умолчанию, нельзя менять |
| Activity status | `online_status_visible` | Toggle On=Friends / Off=Nobody | `ON` (= Friends) | ⚖️ | GDPR Art.25 · ePrivacy — default видят только друзья, не все |
| Show age | `birthday_visibility` | ENUM: Full date / Age only / Friends only / Only me / Hidden | `FRIENDS_AGE` | ⚖️ | GDPR Art.9 |
| Show relationship status | `relationship_visible` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

> ✅ `account_private = OFF` **законно** — открытый профиль соответствует GDPR Art.25 (подтверждено CNIL, ICO)
> ⚠️ `seo_indexable = OFF` **нельзя менять** — GDPR Art.25, штраф до 10 млн € при нарушении
> ⚠️ `online_status_visible`: тумблер ON = видят только ДРУЗЬЯ (не все) · OFF = никто не видит

#### L2: Contact Info Privacy — Видимость контактов

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Who sees email | `email_visibility` | `ONLY_ME` | ⚖️ | GDPR Art.25 · CAN-SPAM · Israel PPL |
| Who sees phone | `phone_visibility` | `ONLY_ME` | ⚖️ | GDPR Art.25 · TCPA · Israel PPL |
| Who sees city | `city_visibility` | `FRIENDS` | 💡 | — |
| Who sees website | `website_visibility` | `PUBLIC` | 💡 | — |
| Who sees social links | `social_links_visibility` | `PUBLIC` | 💡 | — |

> ⚠️ `email_visibility` и `phone_visibility` **НИКОГДА не могут быть PUBLIC** по умолчанию

#### L2: Content Visibility — Видимость контента

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Who sees my posts | `default_post_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 · Quebec L25 Art.8 |
| Who sees my photos / gallery | `photos_visibility` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Who sees my friends list | `friends_list_visibility` | `FRIENDS` | 💡 | — |
| Who sees my activity feed | `activity_visibility` | `FRIENDS` | 💡 | — |
| Who sees my likes / reactions | `likes_visibility` | `FRIENDS` | 💡 | — |
| Who sees my challenges | `challenges_visibility` | `FRIENDS` | 💡 | — |

#### L2: Interactions — Взаимодействия

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Who can send me messages | `who_can_message` | `FRIENDS` | ⚖️ | DSA Art.14 · Israel PPL Sec.2 |
| Who can comment my posts | `who_can_comment` | `FRIENDS` | ⚖️ | DSA Art.14 |
| Who can react to my posts | `who_can_react` | `EVERYONE` | 💡 | — |
| Who can tag me in posts | `who_can_tag` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Tag approval required | `tag_approval_required` | `true` | ⚖️ | GDPR Art.25 |
| Comment moderation | `comment_moderation` | `OFF` | 💡 | — |

#### L2: Discoverability — Обнаружимость

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Profile in search results | `profile_searchable` | `true` | ⚖️ | GDPR Art.17 (право на забвение = opt-out) |
| SEO indexing (Google, Bing) | `seo_indexable` | **`false`** | ⚖️ | GDPR Art.25 — **ОБЯЗАТЕЛЬНО OFF** по умолчанию |
| Content recommendations opt-out | `recommendations_opt_out` | `false` | ⚖️ | GDPR Art.22 · DSA Art.29 · CCPA §1798.121 |
| Algorithm explanation | `show_recommendation_info` | `true` | ⚖️ | DSA Art.27 (ЕС) — «почему мне рекомендуют» |

#### L2: Blocked Accounts — Заблокированные аккаунты

| L3 — Элемент | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| Список заблокированных пользователей | Список | ⚖️ | GDPR — защита от преследования |
| Разблокировать пользователя | Действие | ⚖️ | — |
| Заблокировать пользователя | Действие | ⚖️ | — |
| Ограниченный список (Restricted) | Список | 💡 | — |

---

### 3️⃣ 🛡️ LOGIN & SECURITY — Вход и безопасность
**Обоснование:** ⚖️ GDPR Art.32 — безопасность данных · App Store 5.1.3 (Sign in with Apple)

#### L2: Пароль и доступ

| L3 — Пункт | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| Change password | Действие (с подтверждением текущего) | ⚖️ | GDPR Art.32 |
| **Two-factor authentication (2FA)** | Toggle + выбор метода (Email OTP · TOTP App; SMS — только если добавлен телефон в профиль) | ⚖️ | GDPR Art.32 · Israel Data Security Regs 5777-2017 |
| Login methods | Список (Google / Apple / Email) | ⚖️ | App Store 5.1.3 — Sign in with Apple обязателен |
| **Sign in with Apple** | Метод входа | ⚖️ | **App Store 5.1.3** — обязателен если есть вход через Google/Facebook |

#### L2: Сессии и устройства

| L3 — Пункт | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| Active sessions (список устройств) | Список с датой / IP / устройством | ⚖️ | GDPR Art.32 · Israel Data Security Regs |
| Terminate selected session | Действие | ⚖️ | GDPR Art.32 |
| Terminate all other sessions | Действие | ⚖️ | GDPR Art.32 |
| Trusted devices | Список | 💡 | — |
| Login activity log | Хронология входов | ⚖️ | GDPR · Israel Data Security Regs (audit log) |

> ⚠️ **App Store**: если есть вход через Google или Facebook — Sign in with Apple **обязателен**

---

### 4️⃣ 🔔 NOTIFICATIONS — Уведомления
**Обоснование:** ⚖️ GDPR Art.6/7 · App Store · Google Play · CASL · CAN-SPAM

#### L2: Каналы уведомлений (глобальные переключатели)

| L3 — Канал | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Push notifications | `push_enabled` | `true` | ⚖️ | App Store — системный диалог iOS (не bypass) |
| Email notifications | `email_notifications_enabled` | `true` | ⚖️ | GDPR · CASL — opt-in до отправки |
| In-app notifications | `inapp_enabled` | `true` | 💡 | — |

> ⚠️ **CASL (Канада)**: push и email требуют **явного opt-in** перед первой отправкой
> ⚠️ **Каждое письмо** должно содержать ссылку **one-click unsubscribe** (CASL + CAN-SPAM)

#### L2: Account & Security ⚖️ (нельзя выключить)

| L3 — Ключ уведомления | Описание | Каналы |
|---|---|---|
| `profile_security_login_new_device` | Вход с нового устройства | Email · Push · In-app |
| `profile_security_suspicious_login_attempt` | Подозрительная попытка входа | Email · Push |
| `profile_security_password_changed` | Пароль изменён | Email · In-app |
| `profile_security_contacts_changed` | Email или телефон изменены | Email · In-app |
| `profile_security_suspicious_activity` | Подозрительная активность | Email · Push |
| `profile_data_export_ready` | Файл экспорта данных готов | Email · In-app |
| `profile_data_export_requested` | Запрос экспорта данных | Email · In-app |
| `profile_account_suspended` | Аккаунт заблокирован | Email · In-app |
| `profile_account_restored` | Аккаунт восстановлен | Email · In-app |
| `profile_account_deletion_completed` | Удаление аккаунта завершено | Email · In-app |
| `profile_security_2fa_changed` | Изменены настройки 2FA | Email · In-app |

**Юридическое основание:** GDPR Art.32/33 · Israel PPL Sec.17C · PIPEDA (breach notification)

#### L2: System & Legal ⚖️ (нельзя выключить)

| L3 — Ключ уведомления | Описание | Каналы |
|---|---|---|
| `system_terms_updated` | Обновлены Условия использования | Email · In-app |
| `system_privacy_updated` | Обновлена Политика конфиденциальности | Email · In-app |
| `system_accessibility_updates` | Обновления, влияющие на доступность | In-app |
| `system_maintenance` | Технические уведомления | Push · In-app |

#### L2: Content & Moderation ⚖️ (нельзя выключить)

| L3 — Ключ уведомления | Описание | Каналы |
|---|---|---|
| `system_moderation_content_removed` | Контент удалён модерацией | Email · In-app |
| `system_moderation_content_rejected` | Контент не прошёл модерацию | In-app |
| `profile_complaint_received` | Жалоба на ваш контент | In-app |
| `profile_appeal_decision` | Решение по апелляции | Email · In-app |

**Юридическое основание:** DSA Art.17/18 (обязательно для ЕС)

#### L2: Social Activity 💡 (можно выключить)

| L3 — Ключ уведомления | Default | Каналы |
|---|---|---|
| `profile_new_post_comment` | ✅ ON | In-app · Push |
| `profile_reply_comment` | ✅ ON | In-app · Push |
| `profile_reaction_post` | ✅ ON | In-app |
| `profile_reaction_comment` | ✅ ON | In-app |
| `user_mention_post` | ✅ ON | In-app · Push |
| `user_mention_comment` | ✅ ON | In-app |
| `profile_friend_request` | ✅ ON | In-app · Push |
| `profile_friend_request_accepted` | ✅ ON | In-app |
| `profile_post_shared` | ✅ ON | In-app |

#### L2: Chat 💡 (можно выключить)

| L3 — Ключ уведомления | Default | Каналы |
|---|---|---|
| `chat_new_message` | ✅ ON | Push · In-app |
| `chat_message_reaction` | ✅ ON | In-app |
| `chat_group_added` | ✅ ON | Push · In-app |
| `chat_group_invitation` | ✅ ON | Push · In-app |
| `chat_call_incoming` | ✅ ON | Push |
| `chat_call_missed` | ✅ ON | Push · In-app |

#### L2: Rewards, Blogs, Community, Challenge 💡 (можно выключить)

| L3 — Группа | Ключи | Default |
|---|---|---|
| Rewards (3 ключа) | `reward_badge_earned`, `reward_points_added`, `reward_challenge_completed` | ✅ ON |
| Blogs (5 ключей) | `blog_new_comment`, `blog_reply`, `blog_reaction`, `blog_published`, `blog_mentioned` | ✅ ON |
| Community (8 ключей) | `community_new_post`, `community_mention`, `community_role_changed`, `community_invite`, `community_post_approved`, `community_post_rejected`, `community_member_joined`, `community_announcement` | ✅ ON |
| Challenge (1 ключ) | `challenge_new_participant` | ✅ ON |

---

### 5️⃣ 👥 FRIENDS — Друзья
**Обоснование:** 💡 UX-норма социальной сети · ⚖️ GDPR Art.25 (видимость списка друзей)

#### L2: Список друзей

| L3 — Элемент | Тип | ⚖️/💡 |
|---|---|---|
| Friends list | Список с поиском | 💡 |
| Mutual friends count | Число | 💡 |
| Remove friend | Действие | 💡 |
| Find friends (contacts / suggestions) | Функция | 💡 |

#### L2: Запросы

| L3 — Элемент | Тип | ⚖️/💡 |
|---|---|---|
| Incoming friend requests | Список | 💡 |
| Outgoing friend requests | Список | 💡 |
| Accept / Decline request | Действие | 💡 |
| Cancel sent request | Действие | 💡 |

#### L2: Настройки дружбы

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Who can send friend requests | `who_can_add_friends` | `EVERYONE` | 💡 | — |
| Friend suggestions | `friend_suggestions_enabled` | `true` | 💡 | — |
| Mutual friends visible | `mutual_friends_visible` | `FRIENDS` | ⚖️ | GDPR Art.25 |

---

### 6️⃣ 📝 CONTENT — Контент и публикации
**Обоснование:** ⚖️ DSA Art.14 · GDPR Art.25 · 💡 UX контроль

#### L2: Настройки публикации по умолчанию

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Default post audience | `default_post_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 · Quebec L25 Art.8 |
| Default photo audience | `default_photo_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Location tagging | `location_tagging_enabled` | `false` | ⚖️ | GDPR Art.25 (Privacy by Default = OFF) |
| Allow sharing of my posts | `post_sharing_allowed` | `FRIENDS` | 💡 | — |

#### L2: Фильтрация и модерация контента

| L3 — Настройка | variable_name | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|
| Sensitive content filter | `sensitive_content_filter` | `MODERATE` | ⚖️ | DSA Art.14 |
| Muted words list | `muted_words` | [] | 💡 | — |
| Auto-moderate comments | `comment_moderation` | `OFF` | 💡 | — |
| Auto-archive old posts | `auto_archive_posts` | `OFF` | 💡 | — |
| Content language filter | `content_language_filter` | System | 💡 | — |

#### L2: История и архив

| L3 — Элемент | Тип | ⚖️/💡 |
|---|---|---|
| My posts archive | Список | 💡 |
| Archived stories | Список | 💡 |
| Liked / Saved posts | Список | 💡 |
| Download my content | Действие | ⚖️ (входит в GDPR Art.20 Data Portability) |

---

### 7️⃣ 📦 YOUR DATA — Ваши данные
**Обоснование:** ⚖️ GDPR Art.15–22 · CCPA §1798.100–120 · PIPEDA · Quebec L25 · Israel PPL

#### L2: Права субъекта данных

| L3 — Действие | Описание | ⚖️/💡 | Закон |
|---|---|---|---|
| **Download my data** | Полная копия в JSON/CSV формате | ⚖️ | GDPR Art.15 · PIPEDA Pr.9 · CCPA §1798.100 · Israel PPL Sec.11 |
| **Data portability** | Перенос данных к другому сервису | ⚖️ | GDPR Art.20 · Quebec L25 Art.27 |
| **Restrict processing** | Заморозить обработку без удаления | ⚖️ | GDPR Art.18 |
| **Withdraw consent** | Отозвать своё согласие | ⚖️ | GDPR Art.7 · CASL · PIPEDA Pr.3 |
| **View consent history** | История всех согласий (дата / IP / версия) | ⚖️ | GDPR Art.7 · CASL · PIPEDA Pr.3 |
| **Request data deletion** | Полное удаление всех данных (отдельно от удаления аккаунта) | ⚖️ | GDPR Art.17 · Quebec L25 Art.12 · CCPA §1798.105 |
| **Do Not Sell My Personal Information** | Запрет продавать / передавать данные для рекламы | ⚖️ | **CCPA/CPRA §1798.120** (Калифорния) |
| **Ad preferences** | Рекламные предпочтения + opt-out профилирования | ⚖️ | GDPR Art.21/22 · DSA Art.29 · CCPA §1798.121 |
| **Human review request** | Запрос ревью автоматизированного решения | ⚖️ | GDPR Art.22 · Quebec L25 Art.8.1 · CPRA §1798.185 |

#### L2: Управление согласиями и данными

| L3 — Элемент | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| Cookie settings | Настройки cookies (аналитика / маркетинг / функциональные) | ⚖️ | GDPR / ePrivacy Art.5(3) |
| Privacy Policy | Ссылка | ⚖️ | App Store · Google Play · GDPR Art.13 · PIPEDA Pr.8 |
| Terms of Use | Ссылка | ⚖️ | App Store · Google Play |
| **Contact Privacy Officer / DPO** | Email / форма | ⚖️ | Quebec L25 Art.5 · GDPR Art.37 |

---

### 8️⃣ ♿ ACCESSIBILITY — Доступность
**Обоснование:** ⚖️ **по закону** — EU EAA 2019/882 · ADA (США) · Israel Disability Law 5758-1998 · AODA (Канада) · California Unruh Act · **App Store 2.5.4 · Google Play**

> ⚠️ **КРИТИЧНО**: Accessibility — это НЕ только требование магазинов. Это **закон** в нескольких юрисдикциях:
>
> | Юрисдикция | Закон | Вступает в силу |
> |---|---|---|
> | 🇪🇺 ЕС / ЕЭЗ | **EAA — European Accessibility Act** (Directive 2019/882) — мобильные приложения | **28 июня 2025** |
> | 🇺🇸 США | **ADA** (Americans with Disabilities Act) + **Section 508** (WCAG 2.1 AA) | Сейчас |
> | 🇮🇱 Израиль | **Equal Rights for Persons with Disabilities Law** 5758-1998 + Regulations 5763-2003 | Сейчас |
> | 🇨🇦 Канада | **AODA** (Accessibility for Ontarians with Disabilities Act) + **Accessible Canada Act** 2019 | Сейчас |
> | 🇺🇸 Калифорния | **Unruh Civil Rights Act** (§51 Civil Code) — цифровая доступность | Сейчас |
> | 📱 App Store | Guidelines 2.5.4 — VoiceOver совместимость | Сейчас |
> | 🤖 Google Play | Accessibility guidelines | Сейчас |

#### L2: Текст и отображение

| L3 — Настройка | variable_name | Тип | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|---|
| Text size | `text_size` | Слайдер: Small / Normal / Large / XL | `NORMAL` | ⚖️ | EAA · ADA · WCAG 2.1 Success 1.4.4 |
| Bold text | `bold_text_enabled` | Toggle | `OFF` | ⚖️ | EAA · ADA |
| High contrast mode | `high_contrast_enabled` | Toggle | `OFF` | ⚖️ | EAA · ADA · WCAG 2.1 Success 1.4.3 |
| Reduce motion (animations) | `reduce_motion_enabled` | Toggle | `OFF` | ⚖️ | EAA · ADA · WCAG 2.3 (seizures) |
| Dark / Light mode | `color_theme` | ENUM: Dark / Light / System | `SYSTEM` | 💡 | — |

#### L2: Медиа и контент

| L3 — Настройка | variable_name | Тип | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|---|
| Autoplay videos | `autoplay_videos` | ENUM: Always / Wi-Fi only / Never | `WIFI_ONLY` | 💡 | — |
| Closed captions (CC) | `captions_enabled` | Toggle | `OFF` | ⚖️ | EAA · ADA · WCAG 2.1 Success 1.2.2 |
| Image descriptions (alt text) | `alt_text_enabled` | Toggle | **`ON`** | ⚖️ | EAA · ADA · WCAG 2.1 Success 1.1.1 |
| Screen reader optimization info | — | Информационный экран | — | ⚖️ | EAA · App Store 2.5.4 · ADA |

#### L2: Управление и взаимодействие

| L3 — Настройка | variable_name | Тип | Default | ⚖️/💡 | Закон |
|---|---|---|---|---|---|
| Haptic feedback | `haptic_feedback` | Toggle | `ON` | 💡 | — |
| Sound effects | `sound_effects` | Toggle | `ON` | 💡 | — |
| Keyboard navigation | `keyboard_nav_support` | Информация | — | ⚖️ | EAA · ADA · WCAG 2.1 Success 2.1.1 |
| Focus indicators | `focus_indicators` | Информация | — | ⚖️ | EAA · WCAG 2.1 Success 2.4.7 |

---

### 9️⃣ ❓ HELP & SUPPORT — Помощь и поддержка
**Обоснование:** ⚖️ App Store — обязательная ссылка на поддержку · DSA Art.14/17 · GDPR

#### L2: Основные ресурсы поддержки

| L3 — Пункт | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| Help Center / FAQ | Ссылка (внешний сайт или in-app) | ⚖️ | App Store · Google Play |
| **Contact support** | Форма / Email | ⚖️ | App Store · Google Play |
| **Report a problem** | Форма (контент / пользователь / технические) | ⚖️ | DSA Art.14 · App Store |
| Community guidelines | Ссылка | ⚖️ | DSA Art.12–14 |
| Accessibility support | Ссылка или форма | ⚖️ | EAA · ADA · Israel Disability Law |

#### L2: Юридические ссылки

| L3 — Пункт | Тип | ⚖️/💡 | Закон |
|---|---|---|---|
| **Privacy Policy** | Ссылка | ⚖️ | App Store · Google Play · GDPR Art.13 · PIPEDA Pr.8 |
| **Terms of Use** | Ссылка | ⚖️ | App Store · Google Play |
| **Cookie Policy** | Ссылка | ⚖️ | ePrivacy Directive (ЕС) |
| Licenses / Third-party libs | Список | ⚖️ | App Store |
| **Contact Privacy Officer** | Email / форма | ⚖️ | Quebec L25 Art.5 · GDPR Art.37 |

#### L2: Информация о приложении

| L3 — Пункт | Тип | ⚖️/💡 |
|---|---|---|
| App version | Текст (версия + build) | ⚖️ (App Store) |
| Open source attributions | Список | ⚖️ (App Store) |
| Feedback / Rate the app | Ссылка | 💡 |

---

## РАЗДЕЛ C. СВОДНАЯ ТАБЛИЦА — 9 РАЗДЕЛОВ × ЗАКОНЫ

| # | Раздел | Иконка | ⚖️/💡 | Основные законы |
|---|---|---|---|---|
| 1 | Account | 👤 | ⚖️ | App Store 5.1.1 · Google Play · GDPR Art.17 · CCPA §1798.105 · COPPA |
| 2 | Privacy & Visibility | 🔒 | ⚖️ | GDPR Art.25 · DSA Art.14 · Quebec L25 Art.8 · Israel PPL |
| 3 | Login & Security | 🛡️ | ⚖️ | GDPR Art.32 · App Store 5.1.3 · Israel Data Security Regs |
| 4 | Notifications | 🔔 | ⚖️ | GDPR Art.6/7 · CASL · CAN-SPAM · App Store · DSA Art.17 |
| 5 | Friends | 👥 | 💡/⚖️ | GDPR Art.25 (видимость списка) |
| 6 | Content | 📝 | ⚖️/💡 | GDPR Art.25 · DSA Art.14 · Quebec L25 Art.8 |
| 7 | Your Data | 📦 | ⚖️ | GDPR Art.15–22 · CCPA §1798.100–120 · PIPEDA · Quebec L25 · Israel PPL |
| 8 | Accessibility | ♿ | ⚖️ | **EAA 2019/882** · ADA · Israel Disability Law 5758-1998 · AODA · App Store 2.5.4 |
| 9 | Help & Support | ❓ | ⚖️ | App Store · Google Play · DSA Art.14 · GDPR · Quebec L25 (CPO) |

---

## РАЗДЕЛ D. ДЕРЕВО СТРУКТУРЫ (копируется как текст)

```
⚙️ Settings — Настройки
│
├── 1️⃣ 👤 Account ⚖️
│   ├── Profile photo
│   ├── Display name
│   ├── Username / @handle
│   ├── Email address ⚖️
│   ├── Phone number ⚖️
│   ├── Date of birth ⚖️ COPPA·DSA
│   ├── Gender
│   ├── Language
│   ├── Country / Region ⚖️ GDPR
│   ├── Bio / About
│   ├── Deactivate account ⚖️ GDPR Art.17
│   └── Delete account ⚖️ App Store·Google Play·GDPR Art.17·CCPA
│
├── 2️⃣ 🔒 Privacy & Visibility ⚖️ GDPR Art.25
│   ├── Account Privacy                         ← полный анализ → AccountPrivacySpec.md
│   │   ├── Private account [OFF — открытый] ⚖️ GDPR Art.25
│   │   ├── Profile in search [ON] ⚖️ GDPR Art.17
│   │   ├── SEO indexing [OFF строго] ⚖️ GDPR Art.25 Privacy by Default
│   │   ├── Activity status [ON=Friends / OFF=Nobody] ⚖️ GDPR Art.25
│   │   ├── Show age [Friends — age only] ⚖️ GDPR Art.9
│   │   └── Show relationship status [Friends]
│   ├── Contact Info Privacy
│   │   ├── Who sees email [ONLY ME] ⚖️
│   │   ├── Who sees phone [ONLY ME] ⚖️
│   │   ├── Who sees city [Friends]
│   │   └── Who sees website [Public]
│   ├── Content Visibility
│   │   ├── Who sees posts [Friends]
│   │   ├── Who sees photos [Friends]
│   │   ├── Who sees friends list [Friends]
│   │   ├── Who sees activity [Friends]
│   │   └── Who sees likes [Friends]
│   ├── Interactions
│   │   ├── Who can message me [Friends] ⚖️ DSA Art.14
│   │   ├── Who can comment [Friends] ⚖️ DSA Art.14
│   │   ├── Who can react [Everyone]
│   │   ├── Who can tag me [Friends] ⚖️
│   │   ├── Tag approval required [ON] ⚖️
│   │   └── Comment moderation [OFF]
│   ├── Discoverability
│   │   ├── Profile in search [ON]
│   │   ├── SEO indexing [OFF] ⚖️ GDPR Art.25 Privacy by Default
│   │   ├── Recommendations opt-out [OFF] ⚖️ GDPR Art.22·DSA Art.29
│   │   └── Algorithm explanation [ON] ⚖️ DSA Art.27
│   └── Blocked Accounts
│       ├── Blocked list
│       ├── Block user
│       └── Unblock user
│
├── 3️⃣ 🛡️ Login & Security ⚖️ GDPR Art.32
│   ├── Change password ⚖️
│   ├── Two-factor authentication (2FA) ⚖️
│   ├── Login methods (Google / Apple / Email) ⚖️ App Store 5.1.3
│   ├── Active sessions ⚖️
│   ├── Terminate all sessions ⚖️
│   ├── Trusted devices
│   └── Login activity log ⚖️
│
├── 4️⃣ 🔔 Notifications ⚖️ GDPR·CASL·DSA
│   ├── Channel settings (Push / Email / In-app)
│   ├── Account & Security 🔒 [нельзя выключить] ⚖️ GDPR Art.33
│   │   ├── New device login
│   │   ├── Suspicious activity
│   │   ├── Password changed
│   │   ├── Account suspended / restored
│   │   └── Data export ready
│   ├── System & Legal 🔒 [нельзя выключить] ⚖️ DSA
│   │   ├── Terms updated
│   │   └── Privacy Policy updated
│   ├── Content & Moderation 🔒 [нельзя выключить] ⚖️ DSA Art.17
│   │   ├── Content removed by moderation
│   │   ├── Appeal decision
│   │   └── Complaint received
│   ├── Social Activity 💡 [можно выключить]
│   │   ├── New comment / reply
│   │   ├── Reactions
│   │   ├── Mentions
│   │   ├── Friend request / accepted
│   │   └── Post shared
│   ├── Chat 💡
│   ├── Rewards 💡
│   ├── Blogs 💡
│   ├── Community 💡
│   └── Challenge 💡
│
├── 5️⃣ 👥 Friends 💡
│   ├── Friends list (с поиском)
│   ├── Incoming requests
│   ├── Outgoing requests
│   └── Settings
│       ├── Who can add me [Everyone]
│       ├── Friend suggestions [ON]
│       └── Mutual friends visible [Friends] ⚖️ GDPR
│
├── 6️⃣ 📝 Content ⚖️/💡 DSA·GDPR
│   ├── Default post audience [Friends] ⚖️ GDPR Art.25
│   ├── Default photo audience [Friends] ⚖️
│   ├── Location tagging [OFF] ⚖️ GDPR Art.25
│   ├── Allow post sharing [Friends]
│   ├── Sensitive content filter [Moderate] ⚖️ DSA Art.14
│   ├── Muted words
│   ├── Auto-moderate comments [OFF]
│   ├── Auto-archive posts [OFF]
│   └── Archive / Saved posts
│
├── 7️⃣ 📦 Your Data ⚖️ GDPR Art.15–22
│   ├── Download my data ⚖️ GDPR Art.15·CCPA
│   ├── Data portability ⚖️ GDPR Art.20
│   ├── Restrict processing ⚖️ GDPR Art.18
│   ├── Withdraw consent ⚖️ GDPR Art.7·CASL
│   ├── View consent history ⚖️ GDPR Art.7
│   ├── Request data deletion ⚖️ GDPR Art.17·CCPA
│   ├── Do Not Sell My Personal Information ⚖️ CCPA §1798.120
│   ├── Ad preferences ⚖️ GDPR Art.21/22·DSA Art.29
│   ├── Human review request ⚖️ GDPR Art.22·Quebec L25
│   ├── Cookie settings ⚖️ ePrivacy
│   ├── Privacy Policy ⚖️
│   ├── Terms of Use ⚖️
│   └── Contact Privacy Officer ⚖️ Quebec L25·GDPR
│
├── 8️⃣ ♿ Accessibility ⚖️ EAA·ADA·Israel·AODA·App Store
│   ├── Text & Display
│   │   ├── Text size [Normal] ⚖️ EAA·ADA·WCAG 1.4.4
│   │   ├── Bold text [OFF] ⚖️
│   │   ├── High contrast [OFF] ⚖️ WCAG 1.4.3
│   │   ├── Reduce motion [OFF] ⚖️ WCAG 2.3
│   │   └── Dark / Light / System theme
│   ├── Media
│   │   ├── Autoplay videos [Wi-Fi only]
│   │   ├── Closed captions [OFF] ⚖️ EAA·ADA·WCAG 1.2.2
│   │   ├── Alt text for images [ON] ⚖️ WCAG 1.1.1
│   │   └── Screen reader info ⚖️
│   └── Controls
│       ├── Haptic feedback [ON]
│       ├── Sound effects [ON]
│       ├── Keyboard navigation info ⚖️ WCAG 2.1.1
│       └── Focus indicators info ⚖️ WCAG 2.4.7
│
└── 9️⃣ ❓ Help & Support ⚖️ App Store·DSA
    ├── Help Center / FAQ ⚖️
    ├── Contact support ⚖️ App Store
    ├── Report a problem ⚖️ DSA Art.14
    ├── Community guidelines ⚖️ DSA
    ├── Accessibility support ⚖️ EAA·ADA
    ├── Privacy Policy ⚖️
    ├── Terms of Use ⚖️
    ├── Cookie Policy ⚖️ ePrivacy
    ├── Contact Privacy Officer ⚖️ Quebec L25
    ├── Licenses / Third-party ⚖️
    └── App version ⚖️
```

---

*Файл: `SettingsTZ.md` | Версия 1.0 | Юрисдикции: EU/EEA · Canada · Israel · California · USA · App Stores*
*Полный юридический анализ → `LegalComplianceSpec.md` | Настройки по разделам → `ProfileSettingsFullSpec.md`*
