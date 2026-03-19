# PrivacyVisibilitySpec.md — Полная спецификация: Account + Privacy & Visibility

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик  
**Статус:** 🔴 Часть блокирует публикацию (App Store + Google Play) · 🟡 Часть критична для GDPR

> **Этот документ** формализует структуру, описанную автором приложения, с дополнением переменных,
> дефолтов и правовых оснований. Смежные документы:
> [AccountDeletionSpec.md](AccountDeletionSpec.md), [AccountPrivacySpec.md](AccountPrivacySpec.md),
> [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md)

---

## Содержание

1. [Раздел 1: Account (Аккаунт)](#1-account)
2. [Раздел 2: Privacy & Visibility (Приватность и видимость)](#2-privacy--visibility)
   - [2.1 Account Privacy](#21-account-privacy)
   - [2.2 Profile Visibility](#22-profile-visibility)
   - [2.3 Contact Info Privacy](#23-contact-info-privacy)
   - [2.4 Content Visibility](#24-content-visibility)
   - [2.5 Interactions](#25-interactions)
   - [2.6 Discoverability](#26-discoverability)
   - [2.7 Blocked Accounts](#27-blocked-accounts)
3. [🔴 Обязательно для публикации](#3-обязательно-для-публикации)
4. [Карта пропущенных полей](#4-карта-пропущенных-полей)
5. [Вопрос: куда поместить Subscribed Communities?](#5-subscribed-communities)
6. [Итоговая ASCII-структура](#6-ascii-структура)

---

## 1. Account

**Путь в приложении:** Settings → Account  
**Правовое основание:** ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17

### 1.1 User Info — Информация пользователя

| Поле | variable_name | Тип | Редактируемость | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Avatar (фото профиля)** | `avatar_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **Cover image (обложка)** | `cover_image_url` | Изображение (загрузить / удалить) | ✏️ | 💡 | — |
| **First name (имя)** | `first_name` | Текст | ❌ **не меняется** после регистрации | ⚖️ | GDPR Art.17 |
| **Last name (фамилия)** | `last_name` | Текст | ✏️ (добавить если нет) | ⚖️ | GDPR Art.17 |
| **Date of birth** | `date_of_birth` | Дата | ❌ не меняется | ⚖️ | COPPA · GDPR Art.8 · DSA Art.28 |
| **Gender** | `gender` | ENUM: Male / Female / Other / Prefer not to say | ✏️ | 💡 | — |
| **Interests / Categories** | `interest_tags` | Multi-select (теги) | ✏️ | 💡 | — |

> ⚠️ **First name не редактируется:** под полем показать подсказку  
> _«Чтобы изменить имя, напишите в поддержку»_ — с прямой кнопкой «Написать в поддержку».  
> Это стандартная практика (как в Instagram, TikTok) для защиты от спуфинга.

### 1.2 Profile Info — Информация профиля

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Bio / About** | `bio` | Текст (≤ 300 символов) | пусто | 💡 | — |
| **Status** | `status_text` | Текст (≤ 80 символов) | пусто | 💡 | — |
| **Goals** | `goals` | Multi-select (цели: «пить больше воды», «больше ходить», …) | пусто | 💡 | — |
| **Category** | `profile_category` | ENUM (список категорий: Creator, Athlete, Artist, Business…) | пусто | 💡 | — |
| **Language** | `app_language` | ENUM (список языков) | System locale | 💡 | — |

### 1.3 Contact Info — Контактная информация

| Поле | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| **Email address** | `email` | Текст | обязательный | ⚖️ | GDPR Art.5 — минимизация |
| **Phone number** | `phone_number` | Текст | необязательный | ⚖️ | GDPR · TCPA |
| **Location / Country / Region** | `location_country` | ENUM (страны) | пусто | ⚖️ | GDPR — применимое право |
| **Address** | `address_text` | Текст | пусто | ⚖️ | GDPR — чувствительные данные |
| **Personal link (профильная ссылка)** | `profile_link_url` | URL | пусто | 💡 | — |
| **Blog link (ссылка на блог)** | `blog_link_url` | URL | пусто | 💡 | — |
| **Business link** | `business_link_url` | URL | пусто | 💡 | — |

> ⚠️ Телефон не является обязательным при регистрации — это влияет на 2FA  
> (подробнее → [GDPRArt5SecuritySpec.md §1.1](GDPRArt5SecuritySpec.md))

### 1.4 Account Management — Управление аккаунтом

**Путь в приложении:** Settings → Account → Account Management

| Пункт | Тип | ⚖️ | Закон |
|---|---|---|---|
| **Deactivate account** | Действие (временная деактивация) | ⚖️ | GDPR Art.17 |
| **Delete account** | Действие (постоянное удаление + 2-step confirmation) | ⚖️ | GDPR Art.17 · CCPA §1798.105 · **App Store §5.1.1(v)** · **Google Play** |
| **Switch to Business profile** | Действие (переключение на бизнес-режим) | 💡 | — |
| **Create Business account** | Действие (создать дополнительный бизнес-аккаунт) | 💡 | — |

> ⚠️ **App Store + Google Play**: кнопка Delete account должна быть доступна **прямо** из настроек.  
> Полный путь: **Settings → Account → Account Management → Delete account**  
> ⚠️ **Google Play** (дополнительно): веб-форма `bestme.app/account/delete` (отдельно от in-app)  
> Подробнее → [AccountDeletionSpec.md](AccountDeletionSpec.md)

---

## 2. Privacy & Visibility

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
| **Subscribed blogs visibility** | `subscribed_blogs_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |
| **Subscribed communities** | `subscribed_communities_visibility` | ENUM: Everyone / Friends / Only me | `EVERYONE` | 💡 | — |
| **Discussions visibility** | `discussions_visibility` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

> ℹ️ **Categories (`categories_visibility`):** категория профиля (Creator, Artist и т.д.) — публичная
> информация, аналог "профессия" в LinkedIn. Default `EVERYONE` допустим.

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

> 💬 **Activity status (online) — `online_status_visible`**  
> Зелёная точка (или надпись «В сети») рядом с аватаром пользователя, которая показывает, что человек **прямо сейчас** открыл приложение. Как в WhatsApp или Instagram Stories — ты видишь, что друг онлайн, и можешь написать. Если выключить — никто не увидит, когда ты в приложении.  
> ⚠️ **Юридически:** ON = видят только ДРУЗЬЯ (не «все»). «Онлайн для всех» без явного согласия = нарушение ePrivacy Directive Art.5(3).

> 💬 **Read receipts — `read_receipts_visible`**  
> Уведомление о прочтении сообщения — синие галочки / «Прочитано», которые получает отправитель, когда ты открыл его сообщение. Как в Telegram (два синих флажка) или iMessage (слово «Read»). Если выключить — люди не увидят, читал ли ты их сообщения.  
> 💡 Обе функции (онлайн-статус и прочитал/не прочитал) должны быть взаимными: если ты скрываешь свой статус, ты не видишь чужой (стандарт UX мессенджеров).

> ⚠️ **`last_seen_visible`:** Default `FRIENDS` (не `EVERYONE`) — по GDPR Art.25 данные о времени активности = персональные данные.  
> ⚠️ **`share_permission`:** кто может делиться твоими постами вовне. Default `FRIENDS` — Privacy by Default (GDPR Art.25). Пользователь может ослабить до `EVERYONE`.

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

### 2.7 Blocked Accounts

**Путь:** Settings → Privacy & Visibility → Blocked Accounts

> Управляет списком заблокированных и ограниченных пользователей.  
> **Не требует переменных на бэкенде в этом разделе** — это UI для управления существующей таблицей `blocks`.

| Элемент UI | Тип | ⚖️ | Закон |
|---|---|---|---|
| **Список заблокированных пользователей** | Список (Blocked users list) | ⚖️ | GDPR — защита от преследования |
| **Разблокировать пользователя** | Действие (Unblock) | ⚖️ | — |
| **Заблокировать пользователя** | Действие (Block, через профиль) | ⚖️ | — |
| **Ограниченный список (Restricted)** | Список (видят публичный контент, но не Stories, не личные посты) | 💡 | — |

> 💬 **Block vs Restrict:**  
> — **Block** = полная блокировка: человек не видит профиль, не может написать, не появляется в поиске.  
> — **Restrict** = мягкое ограничение: человек видит публичные посты, но его комментарии видны только ему самому (незаметно для него). Как в Instagram. Полезно против троллей без эскалации конфликта.  
> ⚠️ GDPR требует, чтобы заблокированный пользователь **не мог определить, что его заблокировали** (нейтральный ответ системы — "профиль не найден"). Это снижает риск преследования (harassment).

---

## 3. Обязательно для публикации

> 🔴 **Этот раздел для тебя** — здесь собраны ТОЛЬКО те настройки и поведения, которые **блокируют App Store / Google Play** или грозят **крупным штрафом GDPR**. Всё остальное — рекомендации.

### 🔴 БЛОКЕРЫ App Store + Google Play

| # | Что обязательно | Где в спеке | Почему |
|---|---|---|---|
| 1 | **Кнопка «Delete account»** доступна прямо из Settings | §1.4 Account Management | App Store §5.1.1(v) + Google Play — обязательно иначе отказ в публикации |
| 2 | **Веб-форма удаления** `bestme.app/account/delete` (отдельно) | §1.4 + AccountDeletionSpec.md | Google Play — требует веб-форму независимо от in-app |
| 3 | **`seo_indexable = false` по умолчанию** — нельзя менять | §2.1 + §2.6 | GDPR Art.25 — штраф до 10 млн € |
| 4 | **Согласие на UGC Terms of Service** при публикации | ProfileSettingsFullSpec.md | Google Play — обязательная acceptance при создании контента |
| 5 | **ATT (App Tracking Transparency)** prompt на iOS | ProfileSettingsFullSpec.md | App Store §5.1.2 — обязательно перед сбором IDFA |
| 6 | **Prominent Disclosure** перед запросом разрешений | ProfileSettingsFullSpec.md | App Store + Google Play — объяснить ДО запроса разрешений |

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

> 💡 Всё, что помечено ⚖️ в таблицах спеки — это закон. Всё, что 💡 — это лучшая практика, но не штраф.

---

## 4. Карта пропущенных полей

Поля, описанные пользователем, которых **не было** в предыдущих спецификациях и которые добавлены в этом документе:

| Поле | variable_name | Новый? | Где было раньше |
|---|---|---|---|
| Last name | `last_name` | ✅ Уточнено | SettingsTZ: только `Display name` без разделения |
| Status | `status_text` | 🆕 Новое | Не было ни в одной спеке |
| Status visibility | `status_visibility` | 🆕 Новое | Не было ни в одной спеке |
| Goals | `goals` | 🆕 Новое | Не было ни в одной спеке |
| Goals visibility | `goals_visibility` | 🆕 Новое | Не было ни в одной спеке |
| Category (profile) | `profile_category` | 🆕 Новое | Не было |
| Address | `address_text` | ✅ Подтверждено | Упоминалось, но без поля |
| Address visibility | `address_visibility` | 🆕 **Новое** | **Отсутствовало** в SettingsTZ Contact Info Privacy |
| Personal link visibility | `personal_link_visibility` | 🆕 **Новое** | Только `website_visibility` в SettingsTZ |
| Business link visibility | `business_link_visibility` | 🆕 **Новое** | Отсутствовало |
| Blog link | `blog_link_url` | 🆕 Новое | Не было ни в одной спеке |
| Blog link visibility | `blog_link_visibility` | 🆕 Новое | Не было ни в одной спеке |
| Categories visibility | `categories_visibility` | 🆕 **Новое** | **Отсутствовало** в Content Visibility |
| Subscribed blogs visibility | `subscribed_blogs_visibility` | 🆕 **Новое** | **Отсутствовало** |
| Discussions visibility | `discussions_visibility` | 🆕 **Новое** | **Отсутствовало** |
| Share permission | `share_permission` | 🆕 **Новое** | **Отсутствовало** в Interactions |
| Friend request permission | `friend_request_permission` | 🆕 **Новое** | **Отсутствовало** |
| Last seen | `last_seen_visible` | 🆕 **Новое** | **Отсутствовало** |
| Read receipts | `read_receipts_visible` | 🆕 **Новое** | **Отсутствовало** |
| Relationship visible | `relationship_visible` | 🆕 **Новое** | **Отсутствовало** в Account Privacy |
| Who can react | `who_can_react` | 🆕 **Новое** | **Отсутствовало** в Interactions |
| Subscribed communities visibility | `subscribed_communities_visibility` | 🆕 **Новое** | **Отсутствовало** в Content Visibility |
| Recommendations opt-out | `recommendations_opt_out` | 🆕 **Новое** | **Отсутствовало** — новый §2.6 Discoverability |
| Show recommendation info | `show_recommendation_info` | 🆕 **Новое** | **Отсутствовало** — новый §2.6 Discoverability |
| Blocked Accounts UI | — | 🆕 **Новое** | **Отсутствовал** целый раздел §2.7 |

---

## 5. Subscribed Communities

### Вопрос: куда поместить «Подписанные сообщества»?

Пользователь разместил «Subscribed communities» в разделе **Account → Account Management**.  
Это нестандартное расположение — рассмотрим варианты:

| Вариант | Где | Плюсы | Минусы |
|---|---|---|---|
| **A: В Account Management** (как предложила пользователь) | Settings → Account → Account Management | Логично как «управление членством» | Смешивает deletion/deactivation с подписками |
| **B: В Friends & Community (отдельный L1 раздел)** | Settings → Friends & Community | Стандартная практика (Discord, Reddit, Telegram) | Требует отдельный раздел |
| **C: В отдельном L2 под Account** | Settings → Account → My Communities | Компромисс | Нестандартно |

**Рекомендация:**

Если в приложении есть раздел **Friends & Community** (L1) — вынести туда:
```
Settings
└── Friends & Community
    ├── My Friends (список друзей)
    ├── Friend Requests
    ├── Subscribed Communities   ← сюда
    └── Subscribed Blogs
```

Если отдельного раздела нет (или он называется иначе) — оставить в Account как подраздел:
```
Settings → Account → Account Management
├── Deactivate account
├── Delete account
├── Switch to Business profile
├── Create Business account
└── Subscribed communities   ← если нет другого места
```

> ℹ️ «Подписанные сообщества» — это не операция управления аккаунтом, а список членств.  
> Логически ближе к Friend/Social разделу. Но финальное решение за дизайнером/продуктом.

---

## 6. ASCII-структура

Полная структура двух разделов с учётом всех уточнений:

```
⚙️ Settings
│
├── 1️⃣ 👤 Account  ⚖️ App Store §5.1.1 · Google Play · GDPR Art.17
│   ├── User Info
│   │   ├── Avatar (upload / delete)
│   │   ├── Cover image (upload / delete)
│   │   ├── First name  [❌ не меняется — показать: «Написать в поддержку»]
│   │   ├── Last name   [✏️ добавить если нет]
│   │   ├── Date of birth  ⚖️ COPPA · GDPR Art.8 · DSA Art.28
│   │   ├── Gender
│   │   └── Interests
│   │
│   ├── Profile Info
│   │   ├── Bio / About
│   │   ├── Status
│   │   ├── Goals  (multi-select: пить воду, ходить, …)
│   │   ├── Category (Creator / Artist / Athlete / Business…)
│   │   └── Language
│   │
│   ├── Contact Info
│   │   ├── Email  ⚖️ GDPR
│   │   ├── Phone  ⚖️ GDPR · TCPA  [необязательный]
│   │   ├── Location / Country  ⚖️ GDPR
│   │   ├── Address  ⚖️ GDPR (чувствительные)
│   │   ├── Personal link
│   │   ├── Blog link
│   │   └── Business link
│   │
│   └── Account Management  ⚖️
│       ├── Deactivate account          ⚖️ GDPR Art.17
│       ├── Delete account              ⚖️ GDPR Art.17 · CCPA · App Store · Google Play
│       ├── Switch to Business profile  💡
│       └── Create Business account     💡
│
└── 2️⃣ (или 3️⃣) 🔒 Privacy & Visibility  ⚖️ GDPR Art.25
    │
    ├── Account Privacy  ⚖️
    │   ├── Private account         [OFF — открытый]  ⚖️ GDPR Art.25
    │   ├── Profile in search       [ON]  ⚖️ GDPR Art.17
    │   ├── SEO indexing            [OFF строго]  ⚖️ GDPR Art.25
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
    │   ├── Email                   [ONLY_ME]  ⚖️ GDPR Art.5 · CAN-SPAM
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
    │   ├── Categories              [EVERYONE]
    │   ├── Subscribed blogs        [FRIENDS]
    │   ├── Subscribed communities  [EVERYONE]
    │   └── Discussions             [FRIENDS]
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
    │   └── Read receipts           [ON]
    │
    ├── Discoverability  ⚖️ GDPR Art.22 · DSA Art.27 · DSA Art.29
    │   ├── Profile in search       [ON]  ⚖️ GDPR Art.17
    │   ├── SEO indexing            [OFF строго]  ⚖️ GDPR Art.25
    │   ├── Opt-out recommendations [OFF]  ⚖️ GDPR Art.22 · DSA Art.29
    │   └── Why recommended?        [ON]  ⚖️ DSA Art.27
    │
    └── Blocked Accounts  ⚖️
        ├── Blocked users list      ⚖️ GDPR (защита от преследования)
        ├── Block user (action)     ⚖️
        ├── Unblock user (action)   ⚖️
        └── Restricted list         💡
```

---

*PrivacyVisibilitySpec.md v2.0 · Bestme · март 2026*  
*Смежные документы: [AccountPrivacySpec.md](AccountPrivacySpec.md), [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md), [AccountDeletionSpec.md](AccountDeletionSpec.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)*
