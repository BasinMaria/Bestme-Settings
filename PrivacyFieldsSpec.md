# Bestme — Privacy Fields Specification
> **Только для личного профиля** (Personal Profile). Бизнес-профиль — отдельный документ.  
> Полная спецификация всех privacy-полей: variable name, type, default, legal, visibility matrix.
> **Юридический анализ Account Privacy block (defaults, возрастные развилки) → `AccountPrivacySpec.md`**

---

## Легенда / Legend

| Символ | Значение |
|---|---|
| ⚖️ | Юридическое ограничение — обязательно |
| 🇪🇺 | GDPR (EU) |
| 🇺🇸 | CCPA / US federal laws |
| 🇨🇦 | CASL / PIPEDA (Canada) |
| ✅ | Privacy by Default — это значение выставлено по умолчанию |
| ⚠️ | Частичное отображение (не полное) |
| ❌ | Скрыто / Hidden |
| 🚫 | Полностью заблокировано |

**Аудитории:**  
- **Owner** — сам владелец профиля (всегда видит всё своё)  
- **Friends** — подтверждённые друзья  
- **FoF** — Friends of Friends (друзья друзей)  
- **Everyone** — все авторизованные пользователи  
- **Unauth** — незарегистрированные / неавторизованные  
- **Blocked** — заблокированные пользователем  

---

## 1. Поля профиля — видимость

### 1.0 Private Account (закрытый аккаунт)

> Подробный юридический анализ → `AccountPrivacySpec.md`

| Атрибут | Значение |
|---|---|
| **Variable** | `account_private` |
| **Type** | boolean (Toggle On/Off) |
| **Default 18+** | `false` (открытый) — ✅ законно для взрослых |
| **Default 13–17** | `true` (закрытый) — ⚖️ обязательно по DSA Art.28(3)(g) |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.25 · DSA Art.28(3)(g) |
| **Влияние** | Если `true` — Content Visibility автоматически → FRIENDS для всех контентных полей |

| Аудитория | account_private = false | account_private = true |
|---|---|---|
| Owner | ✅ Full profile | ✅ Full profile |
| Friends | ✅ согласно настройкам | ✅ Full profile |
| Everyone | ✅ согласно настройкам | ⚠️ Name + avatar + bio only |
| Unauth | ⚠️ Limited (no contact info) | ⚠️ Name + avatar only |
| Blocked | 🚫 Hidden | 🚫 Hidden |

---

### 1.1 Profile Page (общая видимость профиля)

| Атрибут | Значение |
|---|---|
| **Variable** | `profile_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.15 — минимальные метаданные (имя + аватар) должны быть видны даже при PRIVATE |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Full profile | ✅ Full profile | ✅ Full profile |
| Friends | ✅ Full profile | ✅ Full profile | ⚠️ Basic info (name + avatar) |
| Everyone | ✅ Full profile | ⚠️ Basic info | ⚠️ Basic info (name + avatar) |
| Unauth | ⚠️ Limited (no contact info) | ⚠️ Name + avatar only | ⚠️ Name + avatar only |
| Blocked | 🚫 Hidden (except legal requests) | 🚫 Hidden | 🚫 Hidden |

---

### 1.2 Name

| Атрибут | Значение |
|---|---|
| **Variable** | `name_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR — прозрачность: минимум "Имя + первая буква фамилии" должно быть видно всегда |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Full name | ✅ Full name | ✅ Full name |
| Friends | ✅ Full name | ✅ Full name | ⚠️ First name only |
| Everyone | ✅ Full name | ⚠️ First name + initial | ⚠️ First name + initial |
| Unauth | ✅ Full name | ⚠️ First name + initial | ⚠️ First name + initial |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.3 Avatar

| Атрибут | Значение |
|---|---|
| **Variable** | `avatar_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ✅ Show |
| Everyone | ✅ Show | ⚠️ Placeholder | ⚠️ Placeholder |
| Unauth | ✅ Show | ⚠️ Placeholder | ⚠️ Placeholder |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.4 Cover Photo

| Атрибут | Значение |
|---|---|
| **Variable** | `cover_photo_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ✅ Show |
| Everyone | ✅ Show | ⚠️ Placeholder | ⚠️ Placeholder |
| Unauth | ✅ Show | ⚠️ Placeholder | ⚠️ Placeholder |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.5 Bio

| Атрибут | Значение |
|---|---|
| **Variable** | `bio_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.6 About Profile

| Атрибут | Значение |
|---|---|
| **Variable** | `about_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.7 Status / Mood

| Атрибут | Значение |
|---|---|
| **Variable** | `status_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR — контент-модерация обязательна (hate speech, violence). Рекомендуется автоистечение через 24ч (data minimization) |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.8 Life Goal

| Атрибут | Значение |
|---|---|
| **Variable** | `goal_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR — goal может раскрывать чувствительные данные (здоровье, религия) |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 1.9 Birthday

| Атрибут | Значение |
|---|---|
| **Variable** | `birthday_visibility` |
| **Type** | enum |
| **Default** | `PRIVATE` ✅ |
| **Values** | `PUBLIC_FULL`, `PUBLIC_AGE`, `FRIENDS_FULL`, `FRIENDS_AGE`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — персональные данные. ОБЯЗАТЕЛЬНО по умолчанию PRIVATE. Дата рождения ВСЕГДА хранится в БД для COPPA age check (13+). |

| Аудитория | PUBLIC_FULL | PUBLIC_AGE | FRIENDS_FULL | FRIENDS_AGE | PRIVATE |
|---|---|---|---|---|---|
| Owner | ✅ Full date | ✅ Full date | ✅ Full date | ✅ Full date | ✅ Full date |
| Friends | ✅ Full date | ⚠️ Age only | ✅ Full date | ⚠️ Age only | ❌ Hide |
| Everyone | ✅ Full date | ⚠️ Age only | ❌ Hide | ❌ Hide | ❌ Hide |
| Unauth | ✅ Full date | ⚠️ Age only | ❌ Hide | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden | ❌ Hidden | ❌ Hidden |

**UI-options для пользователя:**
- Public — full date (показывает дату рождения всем)
- Public — age only (показывает только возраст всем)
- Friends — full date
- Friends — age only
- Private ✅ (только ты)

---

### 1.10 Gender

| Атрибут | Значение |
|---|---|
| **Variable** | `gender_visibility` |
| **Type** | enum |
| **Default** | `PRIVATE` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — гендер (особенно небинарные идентичности) = чувствительные данные |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

## 2. Контактная информация

### 2.1 Email

| Атрибут | Значение |
|---|---|
| **Variable** | `email_visibility` |
| **Type** | enum |
| **Default** | `PRIVATE` ✅ |
| **Values** | `FRIENDS_ONLY`, `PRIVATE` |
| **Can User Change** | ⚠️ Ограниченно — **PUBLIC не существует в UI**, вариант PUBLIC запрещён законом |
| **Legal** | ⚖️ 🇪🇺 GDPR + 🇺🇸 CAN-SPAM + 🇨🇦 CASL — ЗАПРЕЩЕНО делать PUBLIC. В UI опция PUBLIC отсутствует. |

| Аудитория | FRIENDS_ONLY | PRIVATE |
|---|---|---|
| Owner | ✅ Show | ✅ Show |
| Friends | ✅ Show | ❌ Hide |
| Everyone | ❌ Hide | ❌ Hide |
| Unauth | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden |

---

### 2.2 Phone Number

| Атрибут | Значение |
|---|---|
| **Variable** | `phone_visibility` |
| **Type** | enum |
| **Default** | `PRIVATE` ✅ |
| **Values** | `FRIENDS_ONLY`, `PRIVATE` |
| **Can User Change** | ⚠️ Ограниченно — **PUBLIC не существует в UI** |
| **Legal** | ⚖️ 🇪🇺 GDPR + 🇺🇸 TCPA + 🇨🇦 PIPEDA — ЗАПРЕЩЕНО делать PUBLIC. В UI опция PUBLIC отсутствует. |

| Аудитория | FRIENDS_ONLY | PRIVATE |
|---|---|---|
| Owner | ✅ Show | ✅ Show |
| Friends | ✅ Show | ❌ Hide |
| Everyone | ❌ Hide | ❌ Hide |
| Unauth | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden |

---

### 2.3 Location / City

| Атрибут | Значение |
|---|---|
| **Variable** | `location_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — геолокация = чувствительные данные |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 2.4 Personal Links (website)

| Атрибут | Значение |
|---|---|
| **Variable** | `personal_links_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see, others hide / PRIVATE=только Owner

---

### 2.5 Social Media Links

| Атрибут | Значение |
|---|---|
| **Variable** | `social_links_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет — пользователь добровольно добавляет ссылки |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see, others hide / PRIVATE=только Owner

---

### 2.6 Blog Link

| Атрибут | Значение |
|---|---|
| **Variable** | `show_blog_link` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | Нет |

Аудитория: PUBLIC=Show для всех / FRIENDS_ONLY=только друзья / PRIVATE=только Owner

---

### 2.7 Business Link

| Атрибут | Значение |
|---|---|
| **Variable** | `show_business_link` |
| **Type** | enum |
| **Default** | `PRIVATE` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.6 — владение бизнесом = персональные данные, идентифицирующие человека |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see / PRIVATE=только Owner

---

## 3. Контент и активность

### 3.1 Media Gallery

| Атрибут | Значение |
|---|---|
| **Variable** | `media_gallery_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — фото/видео могут содержать: лица (биометрические данные), дети, приватные локации = чувствительные данные |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Show | ✅ Show | ✅ Show |
| Friends | ✅ Show | ✅ Show | ❌ Hide |
| Everyone | ✅ Show | ❌ Hide | ❌ Hide |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 3.2 Friends List

| Атрибут | Значение |
|---|---|
| **Variable** | `friends_list_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ Законы о прозрачности — **Взаимные (mutual) друзья ОБЯЗАНЫ быть видимы обеим сторонам** (нельзя полностью скрыть общих друзей) |

| Аудитория | PUBLIC | FRIENDS_ONLY | PRIVATE |
|---|---|---|---|
| Owner | ✅ Full list | ✅ Full list | ✅ Full list |
| Friends | ✅ Full list | ✅ Full list | ⚠️ Mutual friends only |
| Everyone | ✅ Full list | ⚠️ Mutual friends only | ⚠️ Mutual friends only |
| Unauth | ✅ Show | ❌ Hide | ❌ Hide |
| Blocked | ❌ Hidden | ❌ Hidden | ❌ Hidden |

---

### 3.3 Interest Categories

| Атрибут | Значение |
|---|---|
| **Variable** | `categories_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — интересы могут раскрывать: религию, политические взгляды, сексуальную ориентацию = чувствительные данные |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see, others hide / PRIVATE=только Owner

---

### 3.4 Subscribed Blogs

| Атрибут | Значение |
|---|---|
| **Variable** | `subscribed_blogs_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — подписки на блоги могут раскрывать интересы (политика, религия и т.д.) = чувствительные данные |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see, others hide / PRIVATE=только Owner

---

### 3.5 Subscribed Communities

| Атрибут | Значение |
|---|---|
| **Variable** | `subscribed_communities_visibility` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — членство в сообществах может раскрывать: политические взгляды, религию, здоровье, сексуальную ориентацию = чувствительные данные |

Аудитория: PUBLIC=Show / FRIENDS_ONLY=Friends see, others hide / PRIVATE=только Owner

---

### 3.6 Default Post Visibility

| Атрибут | Значение |
|---|---|
| **Variable** | `default_post_visibility` |
| **Type** | enum |
| **Default** | `PUBLIC` |
| **Values** | `PUBLIC`, `FRIENDS_ONLY`, `PRIVATE` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.25 — Privacy by Default. **ВАЖНО:** пользователь ОБЯЗАН иметь возможность изменить видимость каждого конкретного поста индивидуально (GDPR Art.25) |

Аудитория: аудитория каждого поста определяется индивидуально или по этому умолчанию.

---

## 4. Взаимодействия (Interactions)

### 4.1 Who Can Send Messages

| Атрибут | Значение |
|---|---|
| **Variable** | `who_can_message` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `FRIENDS_OF_FRIENDS`, `NOBODY` |
| **Legal** | ⚖️ 🇪🇺 ePrivacy Directive + GDPR — нежелательные сообщения = спам. Рекомендуемый default: FRIENDS_ONLY (Privacy by Default) |

---

### 4.2 Who Can Send Friend Requests

| Атрибут | Значение |
|---|---|
| **Variable** | `who_can_send_friend_request` |
| **Type** | enum |
| **Default** | `EVERYONE` |
| **Values** | `EVERYONE`, `FRIENDS_OF_FRIENDS`, `NOBODY` |
| **Legal** | Нет |

---

### 4.3 Who Can Tag Me

| Атрибут | Значение |
|---|---|
| **Variable** | `who_can_tag` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `NOBODY` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.4/9 — отметки на фото могут содержать биометрические данные |

---

### 4.4 Tag Approval (одобрение отметок)

| Атрибут | Значение |
|---|---|
| **Variable** | `tag_approval_required` |
| **Type** | boolean |
| **Default** | `false` |
| **Values** | `true` (одобрять вручную), `false` (автоматически) |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.7/9 — рекомендуется включить по умолчанию если `who_can_tag = EVERYONE`. Если биометрические данные (фото с лицами) — одобрение критично |
| **Note** | Если `tag_approval_required = true` → отметки не появляются на профиле без одобрения владельца |

---

### 4.5 Who Can Comment on Posts

| Атрибут | Значение |
|---|---|
| **Variable** | `who_can_comment` |
| **Type** | enum |
| **Default** | `EVERYONE` |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `FRIENDS_OF_FRIENDS`, `NOBODY` |
| **Legal** | Нет (но обязательна модерация контента по EU DSA) |

---

### 4.6 Comment Moderation

| Атрибут | Значение |
|---|---|
| **Variable** | `comment_moderation` |
| **Type** | enum |
| **Default** | `AUTO_FILTER` |
| **Values** | `DISABLED`, `AUTO_FILTER`, `MANUAL_APPROVE` |
| **Legal** | ⚖️ 🇪🇺 EU DSA Art.14 — платформы обязаны иметь механизм модерации противоправного контента |
| **Note** | `AUTO_FILTER` — скрывает очевидный спам/hate speech автоматически. `MANUAL_APPROVE` — владелец одобряет каждый комментарий |

---

### 4.7 Who Can Share / Repost

| Атрибут | Значение |
|---|---|
| **Variable** | `who_can_share` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `NOBODY` |
| **Legal** | Нет (контент-политика) |

---

## 5. Активность (Activity)

### 5.1 Online Status

| Атрибут | Значение |
|---|---|
| **Variable** | `show_online_status` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `NOBODY` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — статус онлайн = поведенческие данные (behavioral tracking) |

---

### 5.2 Last Seen

| Атрибут | Значение |
|---|---|
| **Variable** | `show_last_seen` |
| **Type** | enum |
| **Default** | `FRIENDS_ONLY` ✅ |
| **Values** | `EVERYONE`, `FRIENDS_ONLY`, `NOBODY` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.9 — активность = поведенческие данные |

---

## 6. Обнаружение (Discoverability)

> Эта группа критична для GDPR Art.17 (право на забвение) и GDPR Art.22 (автоматизированные решения)

### 6.1 Profile in Search Results

| Атрибут | Значение |
|---|---|
| **Variable** | `profile_searchable` |
| **Type** | enum |
| **Default** | `EVERYONE` |
| **Values** | `EVERYONE`, `FRIENDS_OF_FRIENDS`, `NOBODY` |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.17 — право на забвение: пользователь вправе убрать себя из поиска |
| **Note** | При `NOBODY` — профиль не появляется во внутреннем поиске платформы, доступен только по прямой ссылке |

---

### 6.2 SEO Indexing (индексация профиля в Google/Bing)

| Атрибут | Значение |
|---|---|
| **Variable** | `seo_indexable` |
| **Type** | boolean |
| **Default** | `false` ✅ (ВЫКЛЮЧЕНО по умолчанию) |
| **Values** | `true` (разрешить индексацию поисковиками), `false` (запретить) |
| **Legal** | ⚖️ 🇪🇺 GDPR — должен быть **выключен по умолчанию** (Privacy by Default, GDPR Art.25). Пользователь должен явно включить. При `profile_visibility = PRIVATE` — SEO индексация ОБЯЗАНА быть отключена независимо от настройки. |

---

### 6.3 Content & People Recommendations

| Атрибут | Значение |
|---|---|
| **Variable** | `recommendations_opt_out` |
| **Type** | boolean |
| **Default** | `false` (включено — рекомендации работают) |
| **Can User Change** | Да — **opt-out** (пользователь может отказаться) |
| **Legal** | ⚖️ 🇪🇺 GDPR Art.22 — автоматизированное принятие решений: **пользователь ОБЯЗАН иметь право отказаться** от алгоритмических рекомендаций. При opt-out — показывать хронологическую ленту. |
| **Note** | Это затрагивает: рекомендации людей (People you may know), рекомендации контента (For You), таргетированная реклама |

---

## 7. Сводная таблица всех переменных

| # | Field (UI) | Variable | Default | Legal | Примечание |
|---|---|---|---|---|---|
| 1 | Profile Page | `profile_visibility` | PUBLIC | ⚖️ GDPR Art.15 | Мин. имя+аватар видны при PRIVATE |
| 2 | Name | `name_visibility` | PUBLIC | ⚖️ GDPR (прозрачность) | Мин. имя+инициал всегда виден |
| 3 | Avatar | `avatar_visibility` | PUBLIC | — | Плейсхолдер при скрытии |
| 4 | Cover Photo | `cover_photo_visibility` | PUBLIC | — | Плейсхолдер при скрытии |
| 5 | Bio | `bio_visibility` | PUBLIC | — | |
| 6 | About Profile | `about_visibility` | PUBLIC | — | |
| 7 | Status / Mood | `status_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR (data minimization) | Рекомендуется авто-истечение 24ч |
| 8 | Life Goal | `goal_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 9 | Birthday | `birthday_visibility` | **PRIVATE** ✅ | ⚖️ GDPR Art.9, COPPA | 5 вариантов (full/age × public/friends/private) |
| 10 | Gender | `gender_visibility` | **PRIVATE** ✅ | ⚖️ GDPR Art.9 | |
| 11 | Email | `email_visibility` | **PRIVATE** ✅ | ⚖️ GDPR+CAN-SPAM+CASL | PUBLIC вариант ЗАПРЕЩЁН в UI |
| 12 | Phone | `phone_visibility` | **PRIVATE** ✅ | ⚖️ GDPR+TCPA+PIPEDA | PUBLIC вариант ЗАПРЕЩЁН в UI |
| 13 | Location / City | `location_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 14 | Personal Links | `personal_links_visibility` | PUBLIC | — | |
| 15 | Social Media Links | `social_links_visibility` | PUBLIC | — | Добровольные ссылки |
| 16 | Blog Link | `show_blog_link` | PUBLIC | — | |
| 17 | Business Link | `show_business_link` | **PRIVATE** ✅ | ⚖️ GDPR Art.6 | |
| 18 | Media Gallery | `media_gallery_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | Биометрия, дети, локации |
| 19 | Friends List | `friends_list_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ Прозрачность | Mutual друзья видны всегда |
| 20 | Interest Categories | `categories_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 21 | Subscribed Blogs | `subscribed_blogs_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 22 | Subscribed Communities | `subscribed_communities_visibility` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 23 | Default Post Visibility | `default_post_visibility` | PUBLIC | ⚖️ GDPR Art.25 | Per-post override обязателен |
| 24 | Who Can Message | `who_can_message` | **FRIENDS_ONLY** ✅ | ⚖️ ePrivacy+GDPR | |
| 25 | Who Can Send Friend Request | `who_can_send_friend_request` | EVERYONE | — | |
| 26 | Who Can Tag Me | `who_can_tag` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.4/9 | |
| 27 | Tag Approval | `tag_approval_required` | false | ⚖️ GDPR Art.7/9 | |
| 28 | Who Can Comment | `who_can_comment` | EVERYONE | ⚖️ EU DSA Art.14 | |
| 29 | Comment Moderation | `comment_moderation` | AUTO_FILTER | ⚖️ EU DSA Art.14 | |
| 30 | Who Can Share / Repost | `who_can_share` | **FRIENDS_ONLY** ✅ | — | |
| 31 | Online Status | `show_online_status` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 32 | Last Seen | `show_last_seen` | **FRIENDS_ONLY** ✅ | ⚖️ GDPR Art.9 | |
| 33 | Profile in Search | `profile_searchable` | EVERYONE | ⚖️ GDPR Art.17 | Opt-out = исчезает из поиска |
| 34 | SEO Indexing | `seo_indexable` | **false** ✅ | ⚖️ GDPR Art.25 | Off по умолчанию |
| 35 | Recommendations Opt-out | `recommendations_opt_out` | false (on) | ⚖️ GDPR Art.22 | Opt-out обязателен |

---

## 8. Юридический чеклист — что обязательно для публикации

### 8.1 Обязательно для App Store (Apple)
- [ ] Sign in with Apple (если есть любой другой OAuth)
- [ ] App Tracking Transparency dialog (ATT) — iOS 14.5+
- [ ] Dynamic Type поддержка (Accessibility)
- [ ] VoiceOver поддержка (Accessibility)
- [ ] Все IAP через Apple Pay (30% комиссия)
- [ ] Privacy Policy ссылка в App Store Connect
- [ ] Фильтр контента 17+ (для sensitive content)
- [ ] NSPhotoLibraryUsageDescription, NSCameraUsageDescription и т.д.

### 8.2 Обязательно для Google Play
- [ ] Data Safety Declaration (заполнить в Google Play Console)
- [ ] Фильтр sensitive content
- [ ] Privacy Policy URL
- [ ] Для приложений с пользователями до 13 лет — families policy

### 8.3 Обязательно по GDPR (EU)
- [ ] Email PRIVACY_ONLY — PUBLIC вариант запрещён
- [ ] Phone PRIVACY_ONLY — PUBLIC вариант запрещён
- [ ] Birthday default = PRIVATE
- [ ] Gender default = PRIVATE
- [ ] Media gallery default = FRIENDS_ONLY
- [ ] SEO indexing default = OFF
- [ ] GDPR Art.22 — opt-out от алгоритмических рекомендаций
- [ ] GDPR Art.17 — удаление аккаунта (30-day grace period)
- [ ] GDPR Art.20 — экспорт данных
- [ ] GDPR Art.15 — просмотр своих данных
- [ ] GDPR Art.25 — Privacy by Default (закрытые поля по умолчанию)
- [ ] Механизм жалоб EU DSA Art.16
- [ ] Cookie Policy + consent dialog
- [ ] "Mutual friends always visible" — не позволять полностью скрыть общих друзей

### 8.4 Обязательно по US/Canada
- [ ] Email opt-in для маркетинговых рассылок (CAN-SPAM, CASL)
- [ ] Unsubscribe link в каждом письме (CAN-SPAM)
- [ ] Do Not Sell My Data (CCPA — для пользователей из CA/США)
- [ ] COPPA: age verification при регистрации (дату рождения хранить в БД всегда)
- [ ] TCPA: телефонный номер не делать публичным

### 8.5 Поля, требующие специального UI
- [ ] **Birthday** — 5 вариантов в UI (не 3): PUBLIC_FULL / PUBLIC_AGE / FRIENDS_FULL / FRIENDS_AGE / PRIVATE
- [ ] **Email** — в UI только 2 варианта: Friends / Private (PUBLIC вариант не показывать)
- [ ] **Phone** — в UI только 2 варианта: Friends / Private (PUBLIC вариант не показывать)
- [ ] **Tag Approval** — отдельный toggle + очередь одобрения отметок
- [ ] **Comment Moderation** — 3 режима: Disabled / Auto-filter / Manual approve
- [ ] **SEO Indexing** — toggle, по умолчанию OFF
- [ ] **Recommendations Opt-out** — toggle с объяснением что изменится
- [ ] **Profile Search** — возможность полностью убрать из поиска

---

## 9. Специальные случаи и бизнес-правила

### 9.1 Взаимозависимости полей

| Если... | То... |
|---|---|
| `profile_visibility = PRIVATE` | `seo_indexable` = принудительно false (независимо от настройки) |
| `profile_visibility = PRIVATE` | Профиль не показывается в поиске (даже если `profile_searchable = EVERYONE`) |
| `who_can_tag = EVERYONE` | Рекомендуется показать предупреждение о `tag_approval_required` |
| `email` не верифицирован | Заблокировать изменение `email_visibility` |
| Пользователь < 18 лет | `media_gallery_visibility` принудительно FRIENDS_ONLY или PRIVATE |
| Пользователь < 13 лет | Регистрация заблокирована (COPPA) |

### 9.2 Уведомления при изменении настроек

| Изменение | Уведомление |
|---|---|
| Email address изменён | Email-подтверждение на новый + уведомление на старый ⚖️ |
| Password изменён | Email-уведомление ⚖️ GDPR Art.33 |
| Вход с нового устройства | Push + Email ⚖️ |
| Аккаунт заблокирован | Email с объяснением ⚖️ |
| Delete account запрошен | Email подтверждение + 30-day warning ⚖️ |

---

*Файл: `PrivacyFieldsSpec.md` | Версия 1.0 | Только для личного профиля | Бизнес-профиль — отдельный документ*
