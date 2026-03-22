# FriendsAndCommunitySpec.md — 5️⃣ 👥 Friends & Community

**Версия:** 3.0 · **Дата:** Март 2026
**Раздел:** Settings → Friends & Community
**Статус:** Черновик — на проверке
**Тип спецификации:** Комплексная (UX + Юридическое соответствие + Требования к публикации)

> **Соглашение по языку:** все названия элементов интерфейса (разделы, кнопки, поля, навигационные пути) указаны на **английском языке** — именно так они будут отображаться в приложении. Описания, пояснения и юридические заметки написаны на **русском языке**.

---

## Содержание

1. [Обзор — Что такое Friends & Community?](#1-обзор)
2. [Правовые требования и требования к публикации](#2-правовые-требования)
3. [1. Friends](#3-1-friends)
4. [2. Subscriptions](#4-2-subscriptions)
5. [3. Communities](#5-3-communities)
6. [Схема базы данных](#6-схема-базы-данных)
7. [Структура Settings (дерево UI)](#7-структура-settings)
8. [Журнал аудита](#8-журнал-аудита)
9. [Блокираторы публикации](#9-блокираторы-публикации)
10. [История изменений](#10-история-изменений)

---

## 1. Обзор

**Friends & Community** — это раздел 5️⃣ в Settings приложения BestMe. Он объединяет все социальные функции:
управление контактами, подписки на контент и участие в сообществах.

### Структура раздела

| Раздел (UI) | Подраздел (UI) | Описание |
|---|---|---|
| **1. Friends** [>] | My Friends | Список взаимных друзей, поиск, удаление |
| | Requests | Входящие и исходящие запросы на дружбу |
| | Recommendations | Предложения «Кого добавить» по алгоритму |
| **2. Subscriptions** [>] | Blogs | Блоги пользователей, на которые вы подписаны |
| | Business Profiles | Бизнес-аккаунты, на которые вы подписаны |
| **3. Communities** [>] | My Groups | Группы, которые вы создали (вы — администратор) |
| | Subscriptions | Группы, в которых вы участвуете как участник |

### Что НЕ относится к этому разделу

| Функция | Где находится |
|---|---|
| Кто может отправлять вам запросы на дружбу | Settings → Privacy → Interactions |
| Кто видит ваш список друзей | Settings → Privacy → Content Visibility |
| Заблокировать пользователя | Settings → Privacy → Safety & Blocked Accounts |
| Уведомления о запросах на дружбу | Settings → Notifications |

---

## 2. Правовые требования

### Применимые законы

| Закон | Статья | Применимость |
|---|---|---|
| **GDPR** | Ст.6(1)(b) | Законное основание: исполнение договора (социальные функции, предоставляемые сервисом) |
| **GDPR** | Ст.17 | Право на удаление: пользователь может покинуть сообщества, удалить связи, отписаться |
| **GDPR** | Ст.25 | Конфиденциальность по умолчанию: списки участников сообществ могут содержать чувствительные данные |
| **GDPR** | Ст.6(1)(f) | Законный интерес: алгоритмические рекомендации друзей и сообществ |
| **DSA** | Ст.14 | Незаконный контент в блогах / сообществах — требуется механизм уведомлений и действий |
| **DSA** | Ст.16 | Простой доступ к механизму жалоб на контент |
| **DSA** | Ст.27 | Алгоритмические рекомендации сообществ должны быть объяснимы |
| **CCPA** | §1798.100 | Пользователи могут запросить удаление данных о подписках и участии в сообществах |
| **App Store** | §5.1.1 | Раскрытие информации: членство в сообществе = сбор данных пользователя |
| **App Store** | §1.2 | UGC (пользовательский контент) без механизма модерации запрещён |
| **Google Play** | Политика данных | Посты в блогах и сообществах = UGC — требуется модерация |
| **Закон Израиля о защите частной жизни** | §2 | Запрет несанкционированного сбора данных о социальных связях |

### Блокираторы публикации (🔴 = блокирует релиз в App Store / Google Play)

| № | Блокиратор | Закон / Политика | Статус |
|---|---|---|---|
| 1 | 🔴 **Нет механизма жалоб на записи в блогах** | DSA Ст.16 · App Store §1.2 | Обязательно до релиза |
| 2 | 🔴 **Нет механизма жалоб на посты в сообществах** | DSA Ст.16 · App Store §1.2 | Обязательно до релиза |
| 3 | 🔴 **Нет кнопки Leave Community** | GDPR Ст.17 | Обязательно до релиза |
| 4 | 🔴 **Нет возможности удалить запись в блоге** | GDPR Ст.17 | Обязательно до релиза |
| 5 | 🔴 **Контент сообщества без раскрытия сбора данных** | App Store §5.1.1 | Требуется раскрытие до релиза |
| 6 | ⚠️ **Оценки Business Profiles без модерации** | DSA Ст.14 | Реализовать или отключить до релиза |

---

## 3. 1. Friends

Раздел **Friends** управляет взаимными связями между пользователями BestMe.
Дружба **взаимна**: она устанавливается, когда один пользователь отправляет запрос, а другой его принимает.

> **Важно:** Кто видит ваш список друзей — настраивается в **Settings → Privacy → Content Visibility → Friend List** (по умолчанию: только друзья).

### 3.1 My Friends

**Settings → Friends & Community → Friends → My Friends**

| Действие (UI) | Описание | Требуется подтверждение? |
|---|---|---|
| View list | Все текущие друзья | Нет |
| Remove Friend | Удаляет взаимную связь; другой пользователь **не уведомляется** | Нет (обратимо: можно снова добавить) |
| View Mutual Friends | Нажать на друга → увидеть общих знакомых | Нет |
| Search | Фильтр по имени | Нет |

**Правовая заметка (GDPR Ст.25):** Удаление из друзей не удаляет историю переписки — только разрывает социальную связь. Другой пользователь не получает уведомление (конфиденциальность по умолчанию).

#### UX-каркас — My Friends

```
┌──────────────────────────────────────┐
│  ←  Friends & Community              │
│  My Friends                          │
│  ──────────────────────────────────  │
│  🔍  Search friends...               │
│  ──────────────────────────────────  │
│  👤 Anna Ivanova          [Remove]   │
│  👤 Dmitry Kozlov         [Remove]   │
│  👤 Olga Petrova          [Remove]   │
│  ...                                 │
└──────────────────────────────────────┘
```

### 3.2 Requests

**Settings → Friends & Community → Friends → Requests**

#### Incoming Requests (входящие заявки)

| Действие (UI) | Описание |
|---|---|
| Accept | Устанавливает взаимную дружбу; обе стороны получают уведомление |
| Decline | Отклоняет заявку; отправитель **не уведомляется** об отклонении (GDPR Ст.25) |
| Block | Отклоняет + блокирует отправителя (перенаправляет в Settings → Privacy → Safety) |

#### Outgoing Requests (исходящие заявки)

| Действие (UI) | Описание |
|---|---|
| View | Список ожидающих ответа заявок |
| Cancel | Отзывает вашу заявку |

#### UX-каркас — Requests

```
┌──────────────────────────────────────┐
│  ←  Friends                          │
│  Requests                            │
│  ──────────────────────────────────  │
│  INCOMING (3)                        │
│  👤 Michael Sokolov  [Accept] [Decline]  │
│  👤 Svetlana Novak   [Accept] [Decline]  │
│  👤 Alex Brown       [Accept] [Decline]  │
│  ──────────────────────────────────  │
│  OUTGOING (1)                        │
│  👤 Elena Smirnova        [Cancel]   │
└──────────────────────────────────────┘
```

### 3.3 Recommendations

**Settings → Friends & Community → Friends → Recommendations**

Алгоритм предлагает пользователей, которых вы можете знать, на основе:
- Общих друзей
- Общих сообществ
- Похожих интересов (если настройки конфиденциальности позволяют)

| Действие (UI) | Описание |
|---|---|
| Add Friend | Отправляет заявку рекомендованному пользователю |
| Hide | Убирает конкретного пользователя из списка рекомендаций |
| Turn Off Recommendations | Переходит в Settings → Privacy → Discoverability → Recommendations |

**Правовая заметка (DSA Ст.27 · GDPR Ст.6(1)(f)):** Пользователь может в любой момент отключить алгоритмические рекомендации. Настройка находится в **Settings → Privacy → Discoverability → Recommendations**.

#### UX-каркас — Recommendations

```
┌──────────────────────────────────────┐
│  ←  Friends                          │
│  Recommendations                     │
│  ──────────────────────────────────  │
│  👤 Natalia Borisova                 │
│     2 mutual friends  [Add Friend] [Hide]  │
│  👤 Sergey Volkov                    │
│     Community: Yoga   [Add Friend] [Hide]  │
│  ──────────────────────────────────  │
│  ℹ️  Why am I seeing this?           │
│  [Turn Off Recommendations]          │
└──────────────────────────────────────┘
```

---

## 4. 2. Subscriptions

Раздел **Subscriptions** управляет **односторонними** подписками: на блоги других пользователей и на бизнес-профили.

> В отличие от Friends, подписки **не требуют взаимности**: вы следите за контентом, не запрашивая согласия автора.

### 4.1 Blogs

**Settings → Friends & Community → Subscriptions → Blogs**

Здесь показаны все личные блоги пользователей BestMe, на которые вы подписаны.

Каждый пользователь BestMe может вести **один личный блог**. Управление содержимым блога (посты, настройки видимости) выполняется из профиля, а не из раздела Settings.

| Действие (UI) | Описание |
|---|---|
| View list | Все блоги, на которые вы подписаны |
| Unsubscribe | Прекращает получение обновлений; автор не уведомляется |
| Open Blog | Открывает ленту автора |

#### UX-каркас — Blogs

```
┌──────────────────────────────────────┐
│  ←  Subscriptions                    │
│  Blogs                               │
│  ──────────────────────────────────  │
│  📝 Anna Ivanova's Blog  [Unsubscribe]│
│  📝 Wellness Journal     [Unsubscribe]│
│  📝 Health Diary         [Unsubscribe]│
└──────────────────────────────────────┘
```

### 4.2 Business Profiles

**Settings → Friends & Community → Subscriptions → Business Profiles**

Здесь показаны все бизнес-аккаунты (клиники, студии, тренеры, коучи), на которые вы подписаны.

| Действие (UI) | Описание |
|---|---|
| View list | Все Business Profiles, на которые вы подписаны |
| Unsubscribe | Прекращает получение обновлений |
| Open Profile | Открывает страницу бизнеса |
| Leave a Rating | Оценить бизнес (1–5 звёзд + комментарий) |

**Правовая заметка (DSA Ст.14 · ⚠️ блокиратор):** Оценки и отзывы — это пользовательский контент (UGC). До выхода в релиз необходимо реализовать механизм модерации / жалоб на отзывы.

#### UX-каркас — Business Profiles

```
┌──────────────────────────────────────┐
│  ←  Subscriptions                    │
│  Business Profiles                   │
│  ──────────────────────────────────  │
│  🏢 Yoga Studio «Lotus» [Unsubscribe]│
│     ⭐⭐⭐⭐☆  My rating: 4           │
│  🏢 Clinic «Health»     [Unsubscribe]│
│     ☆☆☆☆☆  [Leave a Rating]         │
└──────────────────────────────────────┘
```

---

## 5. 3. Communities

Раздел **Communities** управляет членством в группах: группами, которые вы создали, и группами, в которых вы состоите как участник.

> Пользователь может создавать **неограниченное количество** сообществ и вступать в любое количество групп.

### 5.1 My Groups

**Settings → Friends & Community → Communities → My Groups**

Здесь показаны все сообщества, которые **вы создали** (вы — администратор).

| Действие (UI) | Описание | Требуется подтверждение? |
|---|---|---|
| Open Group | Переходит на страницу сообщества | Нет |
| Manage Group | Редактировать название, описание, правила, обложку | Нет |
| Manage Members | Принять/отклонить заявки, назначить модераторов, удалить участника | Нет (принять), Да (удалить) |
| Delete Group | Навсегда удаляет сообщество и весь его контент | Да — модальное подтверждение |

**Правовая заметка (GDPR Ст.17):** При удалении группы весь пользовательский контент внутри неё (посты, медиа, комментарии) удаляется с серверов в течение **30 дней**.

#### UX-каркас — My Groups

```
┌──────────────────────────────────────┐
│  ←  Communities                      │
│  My Groups                           │
│  ──────────────────────────────────  │
│  🏠 Healthy Eating Club              │
│     32 members          [Manage]     │
│  🏠 Morning Running                  │
│     15 members          [Manage]     │
│  ──────────────────────────────────  │
│         [+ Create Community]         │
└──────────────────────────────────────┘
```

#### UX-каркас — Delete Group (подтверждение)

```
┌──────────────────────────────────────┐
│  ⚠️  Delete Community?               │
│                                      │
│  This action cannot be undone.       │
│  All posts, media and members        │
│  will be permanently deleted.        │
│                                      │
│  [Cancel]         [Delete Forever]   │
└──────────────────────────────────────┘
```

### 5.2 Subscriptions (Communities)

**Settings → Friends & Community → Communities → Subscriptions**

Здесь показаны все сообщества, в которых вы состоите **как участник** (не как администратор).

| Действие (UI) | Описание | Требуется подтверждение? |
|---|---|---|
| Open Group | Переходит на страницу сообщества | Нет |
| Leave Community | Выходит из сообщества | Да — модальное подтверждение |
| Report | Сообщить о нарушении правил / DSA | Нет (встроенный механизм) |

**Правовая заметка (GDPR Ст.17 · 🔴 блокиратор):** Пользователь должен иметь возможность в любой момент покинуть сообщество. Функция **Leave Community** является обязательной для релиза.

#### UX-каркас — Communities → Subscriptions

```
┌──────────────────────────────────────┐
│  ←  Communities                      │
│  Subscriptions                       │
│  ──────────────────────────────────  │
│  🏘️ Daily Meditation                 │
│     128 members    [Leave Community] │
│  🏘️ Yoga for Beginners               │
│     64 members     [Leave Community] │
└──────────────────────────────────────┘
```

#### UX-каркас — Leave Community (подтверждение)

```
┌──────────────────────────────────────┐
│  Leave «Daily Meditation»?           │
│                                      │
│  You will exit the group.            │
│  Your posts will remain visible      │
│  (delete them manually if needed).   │
│                                      │
│  [Cancel]            [Leave]         │
└──────────────────────────────────────┘
```

---

## 6. Схема базы данных

```sql
-- Связи между пользователями (дружба)
CREATE TABLE friendships (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id      UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  friend_id    UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  status       TEXT NOT NULL CHECK (status IN ('pending', 'accepted', 'declined', 'cancelled')),
  initiated_by UUID NOT NULL REFERENCES auth.users(id),
  created_at   TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at   TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE(user_id, friend_id)
);

-- Личные блоги (один на пользователя)
CREATE TABLE blogs (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID NOT NULL UNIQUE REFERENCES auth.users(id) ON DELETE CASCADE,
  title       TEXT NOT NULL,
  description TEXT,
  visibility  TEXT NOT NULL DEFAULT 'everyone'
              CHECK (visibility IN ('everyone', 'friends', 'private')),
  created_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Подписки на блоги
CREATE TABLE blog_subscriptions (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subscriber_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  blog_id       UUID NOT NULL REFERENCES blogs(id) ON DELETE CASCADE,
  created_at    TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE(subscriber_id, blog_id)
);

-- Сообщества
CREATE TABLE communities (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name        TEXT NOT NULL,
  description TEXT,
  creator_id  UUID REFERENCES auth.users(id) ON DELETE SET NULL,
  is_private  BOOLEAN NOT NULL DEFAULT false,
  created_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Членство в сообществах
CREATE TABLE community_memberships (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  community_id UUID NOT NULL REFERENCES communities(id) ON DELETE CASCADE,
  user_id      UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  role         TEXT NOT NULL DEFAULT 'member'
               CHECK (role IN ('admin', 'moderator', 'member')),
  status       TEXT NOT NULL DEFAULT 'active'
               CHECK (status IN ('pending', 'active', 'banned')),
  joined_at    TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE(community_id, user_id)
);

-- Бизнес-профили
CREATE TABLE business_profiles (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  owner_id    UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  name        TEXT NOT NULL,
  category    TEXT,
  description TEXT,
  created_at  TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Подписки на бизнес-профили
CREATE TABLE business_subscriptions (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subscriber_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  business_id   UUID NOT NULL REFERENCES business_profiles(id) ON DELETE CASCADE,
  created_at    TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE(subscriber_id, business_id)
);

-- Оценки бизнес-профилей
CREATE TABLE business_ratings (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  business_id UUID NOT NULL REFERENCES business_profiles(id) ON DELETE CASCADE,
  rating      SMALLINT NOT NULL CHECK (rating BETWEEN 1 AND 5),
  comment     TEXT,
  created_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
  UNIQUE(user_id, business_id)
);
```

---

## 7. Структура Settings

```
5️⃣ Friends & Community
│
├── 1. Friends                             [>]
│   ├── My Friends          (просмотр · поиск · Remove Friend)
│   ├── Requests            (Incoming: Accept/Decline · Outgoing: Cancel)
│   └── Recommendations     (Add Friend · Hide · Turn Off Recommendations)
│
├── 2. Subscriptions                       [>]
│   ├── Blogs               (просмотр · Unsubscribe · Open Blog)
│   └── Business Profiles   (просмотр · Unsubscribe · Leave a Rating)
│
└── 3. Communities                         [>]
    ├── My Groups           (Create Community · Manage Group · Delete Group)
    └── Subscriptions       (Open Group · Leave Community · Report)
```

---

## 8. Журнал аудита

| Событие | Когда записывается | Данные |
|---|---|---|
| `friendship_request_sent` | Отправлена заявка в Friends | user_id, target_id, timestamp |
| `friendship_request_accepted` | Заявка в Friends принята | user_id, requester_id, timestamp |
| `friendship_request_declined` | Заявка в Friends отклонена | user_id, requester_id, timestamp |
| `friendship_request_cancelled` | Заявка в Friends отозвана | user_id, target_id, timestamp |
| `friendship_removed` | Remove Friend | user_id, ex_friend_id, timestamp |
| `blog_subscribed` | Подписка в Blogs | user_id, blog_id, timestamp |
| `blog_unsubscribed` | Unsubscribe из Blogs | user_id, blog_id, timestamp |
| `business_subscribed` | Подписка в Business Profiles | user_id, business_id, timestamp |
| `business_unsubscribed` | Unsubscribe из Business Profiles | user_id, business_id, timestamp |
| `business_rated` | Leave a Rating | user_id, business_id, rating, timestamp |
| `community_created` | Create Community | user_id, community_id, timestamp |
| `community_joined` | Вступление в Communities | user_id, community_id, timestamp |
| `community_left` | Leave Community | user_id, community_id, timestamp |
| `community_deleted` | Delete Group | user_id, community_id, timestamp |
| `community_member_removed` | Участник удалён администратором из My Groups | admin_id, user_id, community_id, timestamp |

---

## 9. Блокираторы публикации

### Что нужно сделать до релиза

| № | Блокиратор | Закон / Политика | Приоритет |
|---|---|---|---|
| 1 | 🔴 Механизм жалоб на записи в Blogs | DSA Ст.16 · App Store §1.2 | Спринт до релиза |
| 2 | 🔴 Механизм жалоб на посты в Communities | DSA Ст.16 · App Store §1.2 | Спринт до релиза |
| 3 | 🔴 Кнопка **Leave Community** | GDPR Ст.17 | Спринт до релиза |
| 4 | 🔴 Удаление записи в Blogs (Delete Post) | GDPR Ст.17 | Спринт до релиза |
| 5 | 🔴 Раскрытие сбора данных Communities | App Store §5.1.1 | Спринт до релиза |
| 6 | ⚠️ Модерация рейтингов в Business Profiles | DSA Ст.14 | До или сразу после релиза |

---

## 10. История изменений

| Версия | Дата | Изменение |
|---|---|---|
| 3.0 | Март 2026 | Все названия элементов интерфейса переведены на английский язык (Friends, My Friends, Requests, Recommendations, Subscriptions, Blogs, Business Profiles, Communities, My Groups, Leave Community, Add Friend, Remove Friend, Unsubscribe и др.). Навигационные пути, wireframes и кнопки — на английском. Описания и пояснения — на русском. |
| 2.0 | Март 2026 | Полный рефакторинг на русский язык. Новая структура навигации: 1. Друзья · 2. Подписки · 3. Сообщества. SQL расширен таблицей `business_ratings`. |
| 1.0 | Март 2026 | Первоначальная версия (английский язык) |

---

*Этот документ является частью набора спецификаций BestMe. Любые изменения в функциях требуют обновления этого файла, а также соответствующих разделов в `TermsOfService.md`, `PrivacyPolicy.md` и `UserManualGuide.md`.*
