# PrivacyVisibilitySpec.md — Спецификация раздела: 2️⃣ PRIVACY & VISIBILITY

**Версия:** 2.4 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик  
**Правовое основание:** ⚖️ GDPR Art.25 (Privacy by Default) · DSA Art.14 · ePrivacy · Israel PPL  
**Статус:** 🔴 Часть блокирует публикацию · ⚖️ GDPR Art.25

> **Этот документ** описывает только раздел **2️⃣ Privacy & Visibility**.  
> Смежные документы:  
> [AccountSpec.md](AccountSpec.md) — §1 Account  
> [SettingsOverview.md](SettingsOverview.md) — общая структура всех 9 разделов  
> [AccountPrivacySpec.md](AccountPrivacySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md),  
> [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)

---

## Содержание

1. [2.1 Account Privacy](#21-account-privacy)
2. [2.2 Profile Visibility](#22-profile-visibility)
3. [2.3 Contact Info Privacy](#23-contact-info-privacy)
4. [2.4 Content Visibility](#24-content-visibility)
5. [2.5 Interactions](#25-interactions)
6. [2.6 Discoverability](#26-discoverability)
7. [2.7 Safety & Blocked Accounts](#27-safety--blocked-accounts)
8. [🔴 Обязательно для публикации](#обязательно-для-публикации)
9. [ASCII-структура раздела](#ascii-структура)
10. [Что добавлено в v2.4](#changelog-v24)

---

> 📌 **Принцип Privacy by Default (GDPR Art.25):**  
> Все настройки по умолчанию должны быть максимально строгими.  
> Пользователь сам ослабляет ограничения — но не наоборот.

---

## Privacy & Visibility

**Путь в приложении:** Settings → Privacy & Visibility  
**Правовое основание:** ⚖️ GDPR Art.25 (Privacy by Default) · DSA Art.14 · ePrivacy · Israel PPL

> 📌 **Принцип Privacy by Default (GDPR Art.25):**  
> Все настройки по умолчанию должны быть максимально строгими.  
> Пользователь сам ослабляет ограничения — но не наоборот.

---

### 2.1 Account Privacy

**Путь:** Settings → Privacy & Visibility → Account Privacy

> Настройки, управляющие тем, **как аккаунт находят и индексируют**.

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Private account** | `account_private` | Toggle | `false` (открытый) | ⚖️ | GDPR Art.25 — открытый профиль законен для 18+ |
| **Profile in search results** | `profile_searchable` | Toggle | `true` | ⚖️ | GDPR Art.17 — право на забвение (opt-out доступен) |
| **SEO indexing** | `seo_indexable` | Toggle | **`false`** | ⚖️ | **GDPR Art.25 — СТРОГО OFF, нельзя делать ON по умолчанию** |
| **Show relationship status** | `relationship_visible` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

> ✅ `account_private = false` — **законно** для 18+, открытый профиль соответствует GDPR Art.25 (подтверждено CNIL, ICO)  
> ❌ `seo_indexable` нельзя делать `true` по умолчанию — штраф до 10 млн € (GDPR Art.25)  
> 💬 **`relationship_visible`** — статус отношений («В отношениях», «Женат/замужем» и т.д.). Не является обязательным полем; по умолчанию видят только друзья. Пользователь может скрыть полностью (`Only me`).

---

### 2.2 Profile Visibility

**Путь:** Settings → Privacy & Visibility → Profile Visibility

> Кто видит конкретные поля на странице профиля пользователя.

| Поле профиля | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Full name** | `name_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Имя = публичное (как в соцсети) |
| **Avatar** | `avatar_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Аватар = публичный |
| **Cover** | `cover_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Обложка = публичная |
| **Bio** | `bio_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Открытый профиль → bio публичный |
| **Status** | `status_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Короткий статус профиля — публичный |
| **Birthday** | `birthday_visibility` | ENUM: Full date / Age only / Friends only / Only me / Hidden | `FRIENDS_AGE_ONLY` | ⚖️ | GDPR Art.9 — только возраст друзьям (не полная дата) |
| **Gender** | `gender_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Interests** | `interests_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |
| **Goals** | `goals_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | Личные цели пользователя (пить воду, ходить…) |

> ⚠️ `birthday_visibility`: по умолчанию показывать **только возраст** друзьям — полная дата рождения = чувствительные данные (GDPR Art.9).

---

### 2.3 Contact Info Privacy

**Путь:** Settings → Privacy & Visibility → Contact Info Privacy

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Email** | `email_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.5** — минимизация данных; **никогда не PUBLIC** |
| **Phone** | `phone_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.5 · TCPA** — никогда не PUBLIC |
| **Location** | `location_visibility` | ENUM: Only me / Friends / Everyone | `FRIENDS` | ⚖️ | GDPR — локационные данные |
| **Address** | `address_visibility` | ENUM: Only me / Friends / Everyone | `ONLY_ME` | ⚖️ | **GDPR Art.9** — адрес = чувствительные данные, строго ONLY_ME |
| **Personal link** | `personal_link_visibility` | ENUM: Only me / Friends / Everyone | `EVERYONE` | 💡 | — |
| **Blog link** | `blog_link_visibility` | ENUM: Only me / Friends / Everyone | `EVERYONE` | 💡 | — |
| **Business link** | `business_link_visibility` | ENUM: Only me / Friends / Everyone | `EVERYONE` | 💡 | — |

> ⚠️ **`email_visibility` и `phone_visibility` НИКОГДА не могут быть `EVERYONE` по умолчанию**  
> ⚠️ **`address_visibility`** — адрес является чувствительными данными категории "местоположение",
> по умолчанию строго `ONLY_ME`. Не должен быть публичным даже для 18+.

---

### 2.4 Content Visibility

**Путь:** Settings → Privacy & Visibility → Content Visibility

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Default post visibility** | `default_post_audience` | ENUM: Everyone / Friends / Friends of Friends / Only me | `FRIENDS` | ⚖️ | GDPR Art.25 · Quebec L25 Art.8 |
| **Media gallery visibility** | `gallery_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | ⚖️ | GDPR Art.25 |
| **Friends list visibility** | `friends_list_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |
| **Categories visibility** | `categories_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | Категории профиля — публичная информация |
| **Subscribed blogs visibility** | `subscribed_blogs_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Subscribed communities** | `subscribed_communities_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Discussions visibility** | `discussions_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Activity feed visibility** | `activity_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Likes & reactions visibility** | `likes_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Challenges visibility** | `challenges_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |

> ℹ️ **Categories (`categories_visibility`):** категория профиля (Creator, Artist и т.д.) — публичная
> информация, аналог "профессия" в LinkedIn. Default `EVERYONE` допустим.  
> ℹ️ **Subscribed blogs / Subscribed communities / Discussions** — публичный контент (подписки, публичные дискуссии),
> поэтому дефолт `EVERYONE` допустим по GDPR Art.25 (публичное взаимодействие осознанно).  
> ℹ️ **Activity feed (`activity_visibility`)** — это публичный лог действий пользователя: какие посты он лайкнул,
> какие челленджи начал, какие цели поставил. **Это НЕ лента контента, которую видит сам пользователь** (его собственный
> feed — это отдельная фича приложения, не настройка). Дефолт `EVERYONE` — делает активность видимой
> всем, что стимулирует социальное взаимодействие и открытость (wellness-платформа).  
> ℹ️ **Likes & reactions / Challenges** — социальная активность пользователя. Дефолт `EVERYONE` усиливает
> вирусность и вовлечённость. Правового требования ставить `FRIENDS` нет.  
> ℹ️ **Friends list (`friends_list_visibility`)** — дефолт `FRIENDS` оставлен: список друзей раскрывает
> социальный граф пользователя, это более чувствительные данные.  
> ℹ️ **Saved content** — список сохранённых материалов доступен пользователю **только в его личном меню**
> (Menu → Saved) и никогда не показывается другим пользователям. Настройка видимости не нужна: поле
> `saved_content_visibility` **удалено** из спецификации. Дублировать ссылку на «Saved» в настройках не нужно —
> доступ через меню является достаточным и стандартным паттерном (как в Instagram, TikTok).
>
> ℹ️ **UX-правило: меню vs настройки.** Настройки §2.4 управляют тем, **кто из других пользователей может видеть**
> тот или иной раздел на публичном профиле (например, список обсуждений или челленджей пользователя). Сам
> пользователь всегда видит свои собственные списки через навигацию приложения (Menu / Profile). Добавлять в
> Settings → Privacy & Visibility ссылку на личные разделы меню не требуется.

---

### 2.5 Interactions

**Путь:** Settings → Privacy & Visibility → Interactions

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Who can send messages** | `who_can_message` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | DSA Art.14 · Israel PPL §2 |
| **Who can tag me** | `who_can_tag` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 — тег = обработка данных |
| **Tag approval required** | `tag_approval_required` | Toggle | `true` | ⚖️ | GDPR Art.25 (Privacy by Default) |
| **Who can comment my posts** | `who_can_comment` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | DSA Art.14 |
| **Who can react to my posts** | `who_can_react` | ENUM: Everyone / Friends / No one | `EVERYONE` | 💡 | — |
| **Who can share my posts** | `share_permission` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 — шеринг = распространение данных |
| **Who can send friend requests** | `friend_request_permission` | ENUM: Everyone / Friends of Friends / No one | `EVERYONE` | 💡 | — |
| **Activity status (online)** | `online_status_visible` | Toggle | `true` → только друзья | ⚖️ | GDPR Art.25 · ePrivacy |
| **Last seen** | `last_seen_visible` | ENUM: Everyone / Friends / No one | `FRIENDS` | ⚖️ | GDPR Art.25 · ePrivacy — метаданные активности |
| **Read receipts** | `read_receipts_visible` | Toggle | `true` | 💡 | — |
| **Comment moderation** | `comment_moderation` | Toggle | `false` (OFF) | 💡 | — |

> 💬 **Activity status (online) — `online_status_visible`**  
> Зелёная точка (или надпись «В сети») рядом с аватаром пользователя, которая показывает, что человек **прямо сейчас** открыл приложение. Как в WhatsApp или Instagram Stories — ты видишь, что друг онлайн, и можешь написать. Если выключить — никто не увидит, когда ты в приложении.  
> ⚠️ **Юридически:** ON = видят только ДРУЗЬЯ (не «все»). «Онлайн для всех» без явного согласия = нарушение ePrivacy Directive Art.5(3).

> 💬 **Read receipts — `read_receipts_visible`**  
> Уведомление о прочтении сообщения — синие галочки / «Прочитано», которые получает отправитель, когда ты открыл его сообщение. Как в Telegram (два синих флажка) или iMessage (слово «Read»). Если выключить — люди не увидят, читал ли ты их сообщения.  
> 💡 Обе функции (онлайн-статус и прочитал/не прочитал) должны быть взаимными: если ты скрываешь свой статус, ты не видишь чужой (стандарт UX мессенджеров).

> ⚠️ **`last_seen_visible`:** Default `FRIENDS` (не `EVERYONE`) — по GDPR Art.25 данные о времени активности = персональные данные.  
> ⚠️ **`share_permission`:** кто может делиться твоими постами вовне. Default `FRIENDS` — Privacy by Default (GDPR Art.25). Пользователь может ослабить до `EVERYONE`.

> 💬 **Comment moderation — `comment_moderation`**  
> Автоматическая фильтрация оскорбительных комментариев под постами пользователя (как в Instagram — «Hidden words»). По умолчанию `false` (OFF) — пользователь сам решает. Рекомендуется предложить заготовленный список стоп-слов при включении.

---

### 2.6 Discoverability

**Путь:** Settings → Privacy & Visibility → Discoverability

> Управляет тем, **как алгоритм и поиск находят профиль** пользователя.  
> `profile_searchable` и `seo_indexable` задаются также в §2.1 Account Privacy —  
> здесь они отображаются в едином «блоке обнаружимости» для удобства пользователя.

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Profile in search results** | `profile_searchable` | Toggle | `true` | ⚖️ | GDPR Art.17 — право на забвение (opt-out доступен) |
| **SEO indexing (Google, Yandex, Bing)** | `seo_indexable` | Toggle | **`false`** | ⚖️ | **GDPR Art.25 — ОБЯЗАТЕЛЬНО OFF, нельзя менять на ON** |
| **Opt-out from recommendations** | `recommendations_opt_out` | Toggle | `false` | ⚖️ | GDPR Art.22 · DSA Art.29 · CCPA §1798.121 |
| **Why am I recommended this?** | `show_recommendation_info` | Toggle | `true` | ⚖️ | DSA Art.27 (ЕС) — алгоритмическая прозрачность |

> 💬 **`recommendations_opt_out`** — кнопка/тумблер «Не использовать мой профиль для алгоритмических рекомендаций». По GDPR Art.22 и DSA Art.29 пользователь имеет право отказаться от полностью автоматизированных решений, влияющих на него. По умолчанию `false` = участвует в рекомендациях (стандартная практика). Пользователь может отключить.  
> 💬 **`show_recommendation_info`** — кнопка «Почему мне рекомендуют этого пользователя / этот контент?». По DSA Art.27 (ЕС) это **обязательно** для крупных платформ. Для стартапа: включить заранее, чтобы не переделывать при росте. По умолчанию `true`.  
> ⚠️ **`seo_indexable`:** СТРОГО `false` — штраф до 10 млн € при нарушении GDPR Art.25. Никогда не включать по умолчанию.

---

### 2.7 Safety & Blocked Accounts

**Путь:** Settings → Privacy & Visibility → Safety & Blocked Accounts

> Управляет списком заблокированных / ограниченных пользователей, а также жалобами на контент и пользователей.  
> **Не требует переменных на бэкенде в этом разделе** — это UI для управления существующими таблицами `blocks` и `reports`.

| Элемент UI | Тип | ⚖️ | Закон |
|---|---|---|---|
| **Blocked users list** | Список (заблокированные пользователи) | ⚖️ | GDPR — защита от преследования |
| **Unblock user** | Действие (разблокировать) | ⚖️ | — |
| **Block user** | Действие (заблокировать, через профиль) | ⚖️ | — |
| **Restricted list** | Список (мягкое ограничение — видят публичный контент, но не личные посты) | 💡 | — |
| **Report user** | Действие (пожаловаться на пользователя) | ⚖️ | **DSA Art.16 · DSA Art.14** — механизм уведомления и принятия мер |
| **Report content** | Действие (пожаловаться на контент: пост, комментарий, фото) | ⚖️ | **DSA Art.16** — обязателен для платформ, работающих в ЕС |

> 💬 **Block vs Restrict:**  
> — **Block** = полная блокировка: человек не видит профиль, не может написать, не появляется в поиске.  
> — **Restrict** = мягкое ограничение: человек видит публичные посты, но его комментарии видны только ему самому (незаметно для него). Как в Instagram. Полезно против троллей без эскалации конфликта.  
> ⚠️ GDPR требует, чтобы заблокированный пользователь **не мог определить, что его заблокировали** (нейтральный ответ системы — "профиль не найден"). Это снижает риск преследования (harassment).

> 💬 **Report user / Report content — обязательно для публикации в ЕС:**  
> По **DSA Art.16** (Digital Services Act) любая платформа, доступная в ЕС, **обязана** предоставить механизм жалоб на незаконный контент и пользователей. Кнопка «Report» должна быть доступна:  
> 1. На странице профиля любого пользователя (три точки → Report)  
> 2. Под каждым постом, комментарием, фото (три точки → Report)  
> 3. В этом разделе — для жалоб на уже заблокированных пользователей  
> ⚠️ **Без механизма жалоб — нарушение DSA, недопустимо при публикации в App Store (EU) и Google Play (EU).**

---

## Обязательно для публикации

> 🔴 **Этот раздел** — только те настройки §2 Privacy & Visibility, которые **блокируют App Store / Google Play** или грозят **крупным штрафом GDPR**.

### 🔴 БЛОКЕРЫ (Privacy & Visibility)

| # | Что обязательно | Где | Почему |
|---|---|---|---|
| 1 | **`seo_indexable = false` по умолчанию** — нельзя менять | §2.1 + §2.6 | GDPR Art.25 — штраф до 10 млн € |
| 2 | **Механизм жалоб (Report user / Report content)** | §2.7 | **DSA Art.16** — обязателен для ЕС; без него — нарушение DSA + отказ в App Store EU |

### ⚖️ ОБЯЗАТЕЛЬНЫЕ настройки (без них — нарушение GDPR)

| # | Настройка | variable_name | Дефолт | Закон |
|---|---|---|---|---|
| 1 | **`seo_indexable`** | `seo_indexable` | **СТРОГО `false`** | GDPR Art.25 |
| 2 | **`email_visibility`** | `email_visibility` | **СТРОГО `ONLY_ME`** | GDPR Art.5 |
| 3 | **`phone_visibility`** | `phone_visibility` | **СТРОГО `ONLY_ME`** | GDPR Art.5 · TCPA |
| 4 | **`address_visibility`** | `address_visibility` | **СТРОГО `ONLY_ME`** | GDPR Art.9 |
| 5 | **`birthday_visibility`** | `birthday_visibility` | **`FRIENDS_AGE_ONLY`** (не полная дата) | GDPR Art.9 |
| 6 | **`tag_approval_required`** | `tag_approval_required` | **`true`** | GDPR Art.25 |
| 7 | **`online_status_visible`** ON | `online_status_visible` | Видят только **ДРУЗЬЯ** (не все) | ePrivacy |
| 8 | **`show_recommendation_info`** | `show_recommendation_info` | `true` | DSA Art.27 (ЕС) |

> 💡 Всё, что помечено ⚖️ в таблицах — это закон. 💡 — лучшая практика, не штраф.

---

## ASCII-структура

```
⚙️ Settings
│
└── 2️⃣ 🔒 Privacy & Visibility  ⚖️ GDPR Art.25 (Privacy by Default)
    │
    ├── Account Privacy  ⚖️ GDPR Art.25 · Art.17
    │   ├── Private account         [OFF — открытый]  ⚖️ GDPR Art.25
    │   ├── Profile in search       [ON]  ⚖️ GDPR Art.17
    │   ├── SEO indexing            [OFF строго]  ⚖️ GDPR Art.25  🔴 БЛОКЕР
    │   └── Relationship status     [FRIENDS]  💡
    │
    ├── Profile Visibility  💡
    │   ├── Full name               [EVERYONE]
    │   ├── Avatar                  [EVERYONE]
    │   ├── Cover                   [EVERYONE]
    │   ├── Bio                     [EVERYONE]
    │   ├── Status                  [EVERYONE]
    │   ├── Birthday                [FRIENDS_AGE_ONLY]  ⚖️ GDPR Art.9
    │   ├── Gender                  [EVERYONE]
    │   ├── Interests               [FRIENDS]
    │   └── Goals                   [FRIENDS]
    │
    ├── Contact Info Privacy  ⚖️ GDPR Art.5 — минимизация данных
    │   ├── Email                   [ONLY_ME]  ⚖️ GDPR Art.5
    │   ├── Phone                   [ONLY_ME]  ⚖️ GDPR Art.5 · TCPA
    │   ├── Location                [FRIENDS]  ⚖️ GDPR
    │   ├── Address                 [ONLY_ME]  ⚖️ GDPR Art.9
    │   ├── Personal link           [EVERYONE]
    │   ├── Blog link               [EVERYONE]
    │   └── Business link           [EVERYONE]
    │
    ├── Content Visibility  ⚖️ GDPR Art.25
    │   ├── Default post audience   [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Media gallery           [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Friends list            [FRIENDS]
    │   ├── Interests               [EVERYONE]
    │   ├── Subscribed blogs        [EVERYONE]
    │   ├── Subscribed communities  [EVERYONE]
    │   ├── Discussions             [EVERYONE]
    │   ├── Activity feed           [EVERYONE]
    │   ├── Likes & reactions       [EVERYONE]
    │   └── Challenges              [EVERYONE]
    │
    ├── Interactions  ⚖️ DSA Art.14 · GDPR Art.25 · ePrivacy
    │   ├── Who can message         [FRIENDS]  ⚖️ DSA Art.14
    │   ├── Who can tag me          [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Tag approval required   [ON]  ⚖️ GDPR Art.25
    │   ├── Who can comment         [FRIENDS]  ⚖️ DSA Art.14
    │   ├── Who can react           [EVERYONE]
    │   ├── Who can share my posts  [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Who can send friend req [EVERYONE]
    │   ├── Activity status (online)[ON = только друзья]  ⚖️ ePrivacy
    │   ├── Last seen               [FRIENDS]  ⚖️ GDPR Art.25
    │   ├── Read receipts           [ON]
    │   └── Comment moderation      [OFF]
    │
    ├── Discoverability  ⚖️ GDPR Art.22 · DSA Art.27 · DSA Art.29
    │   ├── Profile in search       [ON]  ⚖️ GDPR Art.17
    │   ├── SEO indexing            [OFF строго]  ⚖️ GDPR Art.25
    │   ├── Opt-out recommendations [OFF]  ⚖️ GDPR Art.22 · DSA Art.29
    │   └── Why recommended?        [ON]  ⚖️ DSA Art.27
    │
    └── Safety & Blocked Accounts  ⚖️ GDPR · DSA Art.16
        ├── Blocked users list      ⚖️ GDPR (защита от преследования)
        ├── Block user (action)     ⚖️
        ├── Unblock user (action)   ⚖️
        ├── Restricted list         💡
        ├── Report user (action)    ⚖️ DSA Art.16  🔴 БЛОКЕР
        └── Report content (action) ⚖️ DSA Art.16  🔴 БЛОКЕР
```

---

## Changelog v2.4

<a name="changelog-v24"></a>

> 📋 **Для разработчиков:** изменения относительно v2.3.

### ✅ ЧТО ДОБАВЛЕНО / ИЗМЕНЕНО в v2.4

| # | Что | Куда | Причина |
|---|---|---|---|
| 1 | **ASCII-дерево исправлено** — `activity_visibility`, `likes_visibility`, `challenges_visibility` обновлены с `[FRIENDS]` → `[EVERYONE]` | §8 Architecture tree | Дерево отставало от таблицы §2.4 (регрессия в v2.3) |
| 2 | **`Saved content [ONLY_ME]`** удалено из ASCII-дерева | §8 Architecture tree | Поле `saved_content_visibility` было удалено из таблицы в v2.3, но строка осталась в дереве |
| 3 | **UX-примечание «меню vs настройки»** добавлено | §2.4 примечания | Поясняет: Settings §2.4 = кто *другие* видят на профиле; Menu → Saved/Discussions/Challenges = личный доступ самого пользователя; дублировать ссылки на личные разделы в настройках не нужно |

---



<a name="changelog-v23"></a>

> 📋 **Для разработчиков:** изменения относительно v2.2.

### ✅ ЧТО ДОБАВЛЕНО / ИЗМЕНЕНО в v2.3

| # | Что | Куда | Причина |
|---|---|---|---|
| 1 | **Дефолт `activity_visibility`** изменён с `FRIENDS` → `EVERYONE` | §2.4 Content Visibility | Нет правового требования ограничивать; открытый дефолт усиливает вовлечённость |
| 2 | **Дефолт `likes_visibility`** изменён с `FRIENDS` → `EVERYONE` | §2.4 Content Visibility | Аналогично: лайки — социальная активность, не чувствительные данные |
| 3 | **Дефолт `challenges_visibility`** изменён с `FRIENDS` → `EVERYONE` | §2.4 Content Visibility | Аналогично: публичные челленджи = вирусность |
| 4 | **`saved_content_visibility` удалено** полностью | §2.4 Content Visibility | Сохранённый контент видит только сам пользователь в своём меню; функции «поделиться списком» нет |
| 5 | **Примечание к `activity_visibility`** добавлено | §2.4 примечания | Уточнено: это лог действий пользователя, а НЕ его личная лента контента |

---

## Changelog v2.2

> 📋 **Для разработчиков:** изменения относительно v2.1.

### ✅ ЧТО ДОБАВЛЕНО / ИЗМЕНЕНО в v2.2

| # | Что | Куда | UX-название | Причина |
|---|---|---|---|---|
| 1 | **Документ разделён** | AccountSpec.md (отдельный) | — | Account (§1) вынесен в отдельный файл. Этот документ теперь содержит ТОЛЬКО §2 Privacy & Visibility. |
| 2 | **Убраны ссылки на §1.x** в блокерах | Обязательно для публикации | — | Блокеры из Account (Delete account, веб-форма) перенесены в AccountSpec.md |
| 3 | **ASCII-структура** обновлена | — | — | Показывает только раздел 2️⃣ Privacy & Visibility (без Account) |
| 4 | **«Interests» в Content Visibility** | §2.4 Content Visibility | "Interests" | Переименована строка `categories_visibility` → показывается как «Interests» (соответствует AccountSpec §1.1) |

### 📋 Сводная таблица — что нужно добавить в ТЗ (Privacy & Visibility)

| Приоритет | Что добавить | Путь в приложении | Закон / Почему важно |
|---|---|---|---|
| 🔴 **БЛОКЕР** | Кнопка **Report user** на профиле | Profile → ⋯ → Report | DSA Art.16 — без этого нельзя публиковаться в ЕС |
| 🔴 **БЛОКЕР** | Кнопка **Report content** на каждом посте/фото/комменте | Post / Photo / Comment → ⋯ → Report | DSA Art.16 |
| 🟡 **ВАЖНО** | **Activity Feed visibility** | Settings → Privacy & Visibility → Content Visibility | Дефолт изменён на EVERYONE (социальная активность открыта) |
| 🟡 **ВАЖНО** | **Likes & Reactions visibility** | Settings → Privacy & Visibility → Content Visibility | Дефолт изменён на EVERYONE |
| 🟡 **ВАЖНО** | **Challenges visibility** | Settings → Privacy & Visibility → Content Visibility | Дефолт изменён на EVERYONE |
| 🟢 **РЕКОМЕНДУЕТСЯ** | **Comment moderation** | Settings → Privacy & Visibility → Interactions | UX-стандарт (Instagram Hidden words) |

---

*PrivacyVisibilitySpec.md v2.4 · Bestme · март 2026*  
*Смежные документы: [AccountSpec.md](AccountSpec.md), [SettingsOverview.md](SettingsOverview.md), [AccountPrivacySpec.md](AccountPrivacySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md), [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)*
