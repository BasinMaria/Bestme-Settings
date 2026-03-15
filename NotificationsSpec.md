# Bestme — Notifications Specification
> **Таблица всех уведомлений** по разделам. Только для личного профиля + бизнес-профиля.
> ✅ ON по умолчанию · ❌ OFF по умолчанию · 🚫 нельзя выключить

**Колонки таблицы:**
- **Key** — код уведомления (для разработки)
- **Описание** — что происходит (RU)
- **Default** — включено/выключено по умолчанию
- **⚖️ Закон** — обязательно по закону или нет
- **Основание** — legal_basis_code
- **Канал** — Email / Push / In-app
- **Title (EN)** — заголовок уведомления
- **Subtitle (EN)** — подзаголовок уведомления

---

## 🟩 PROFILE — Аккаунт и безопасность
> ⚖️ GDPR / CPRA / DSA — все уведомления обязательны, нельзя выключить

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `profile_security_login_new_device` | Вход с нового устройства | ✅ 🚫 | ✅ | GDPR (security) | Email, Push, In-app | Sign-in from a new device | Notify when someone signs in to your account from a new device or browser |
| `profile_security_suspicious_login_attempt` | Попытка входа неуспешная / необычная | ✅ 🚫 | ✅ | GDPR Art.32 | Email, Push | Suspicious sign-in attempt | Notify when an unusual or failed sign-in attempt is detected on your account |
| `profile_security_password_changed` | Пароль изменён | ✅ 🚫 | ✅ | GDPR | Email, In-app | Password changed | Notify when the password for your account is changed |
| `profile_security_contacts_changed` | Контакты изменены (email, телефон) | ✅ 🚫 | ✅ | GDPR | Email, In-app | Contact details changed | Notify when your email, phone number or other contact details on the account are changed |
| `profile_security_suspicious_activity` | Подозрительная активность | ✅ 🚫 | ✅ | GDPR | Email, Push | Suspicious activity on account | Notify when unusual logins or other suspicious activity are detected on your account |
| `profile_data_export_ready` | Файл экспорта данных готов | ✅ 🚫 | ✅ | GDPR Art.15 | Email, In-app | Your data export is ready | Download your personal data file before it expires |
| `profile_data_export_requested` | Запрос на скачивание данных принят | ✅ 🚫 | ✅ | GDPR Art.15 | Email, In-app | Data export and download | Notify when your request to access and download a copy of your data is processed |
| `profile_account_suspended` | Аккаунт заблокирован | ✅ 🚫 | ✅ | DSA Art.20 | Email, In-app | Account blocked or suspended | Notify when your account is blocked, suspended or access is restricted |
| `profile_account_restored` | Аккаунт восстановлен | ✅ | ❌ | UX-норма | In-app, Email | Account restored | Notify when your account is restored and access is returned |
| `profile_account_deletion_completed` | Удаление аккаунта завершено | ✅ 🚫 | ✅ | GDPR Art.12 + Art.17 | Email, In-app | Account and data deleted | Receive notifications when your account and personal data have been permanently deleted and can no longer be restored |
| `profile_account_deletion_requested` | Запрос на удаление аккаунта принят | ✅ 🚫 | ✅ | GDPR Art.17 | Email, In-app | Account deletion request | Receive notifications when your account deletion request has been received and accepted for processing |

---

## 🟥 PROFILE — Системные и юридические уведомления
> ⚖️ Обязательны по GDPR Art.7 / Art.13

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `system_terms_updated` | Обновлены Условия использования | ✅ 🚫 | ✅ | GDPR Art.7 | Email, In-app | Terms of Use updated | Notify when changes to the Terms of Use affect your rights or obligations |
| `system_privacy_updated` | Обновлена Политика конфиденциальности | ✅ 🚫 | ✅ | GDPR Art.13 | Email, In-app | Privacy Policy updated | Notify when the Privacy Policy is updated about how your data is collected and used |
| `system_accessibility_updates` | Обновления, влияющие на доступность | ✅ | ❌ | UX-норма | In-app | Updates affecting accessibility | Notify when product changes may affect accessibility or how you use the app |
| `system_maintenance` | Технические уведомления (обслуживание) | ❌ | ❌ | UX-норма | Push, In-app | Technical notifications | Notify about planned maintenance, performance issues and other non-critical technical updates |

---

## 🟦 PROFILE — Контент и модерация
> ⚖️ Обязательны по DSA Art.17–20

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `system_moderation_content_removed` | Контент удалён модерацией | ✅ 🚫 | ✅ | GDPR Art.17 | Email, In-app | Content removed by moderation | Notify when your post, comment or other content is removed by moderation |
| `system_moderation_content_rejected` | Контент не прошёл модерацию | ✅ 🚫 | ✅ | GDPR Art.20 | In-app | Content not approved | Notify when content you submitted does not pass moderation and is not published |
| `profile_complaint_received` | На ваш контент поступила жалоба | ✅ 🚫 | ✅ | GDPR Art.17 | In-app | Complaint about your content | Notify when someone complains about your content or when there is an update on your complaint |
| `profile_appeal_decision` | Решение по апелляции | ✅ 🚫 | ✅ | GDPR Art.20 | Email, In-app | Decision on your appeal | Notify when a decision is made on an appeal you submitted about moderation |

---

## 🟨 PROFILE — Социальная активность (User-to-User)
> Стандарт соцсетей, не обязательны по закону

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `profile_new_post_comment` | Комментарий к вашему посту | ✅ | ❌ | UX-норма | In-app, Push | New comment on your post | Notify when someone leaves a new comment on your post |
| `profile_reply_comment` | Ответ на ваш комментарий | ✅ | ❌ | UX-норма | In-app, Push | Reply to your comment | Notify when someone replies to a comment you wrote |
| `profile_reaction_post` | Реакция на ваш пост | ✅ | ❌ | UX-норма | In-app | Reaction to your post | Notify when someone reacts to your post |
| `profile_reaction_comment` | Реакция на ваш комментарий | ✅ | ❌ | UX-норма | In-app | Reaction to your comment | Notify when someone reacts to your comment |
| `user_mention_post` | Вас упомянули в посте | ✅ | ❌ | UX-норма | In-app, Push | Mention in a post | Notify when someone mentions you in a post |
| `user_mention_comment` | Вас упомянули в комментарии | ✅ | ❌ | UX-норма | In-app | Mention in a comment | Notify when someone mentions you in a comment |
| `profile_friend_request` | Запрос на добавление в друзья | ✅ | ❌ | UX-норма | In-app, Push | Friend request received | Notify when someone sends you a friend request |
| `profile_friend_request_accepted` | Ваш запрос в друзья принят | ✅ | ❌ | UX-норма | In-app | Friend request accepted | Notify when someone accepts your friend request |
| `profile_post_shared` | Поделились вашим постом | ✅ | ❌ | UX-норма | In-app | Your post was shared | Notify when someone shares your post |

---

## 🟪 CHAT — Чат

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `chat_new_message` | Новое сообщение | ✅ | ❌ | UX-норма | In-app, Push | New chat message | Notify when you receive a new message in your chats |
| `chat_request` | Запрос на переписку | ✅ | ❌ | UX-норма | In-app, Push | New chat request | Notify when someone sends you a chat request |
| `chat_reacted` | Реакция на ваше сообщение | ✅ | ❌ | UX-норма | In-app | Reaction to your message | Notify when someone reacts to your message |
| `chat_request_declined` | Запрос на переписку отклонён | ✅ | ❌ | UX-норма | In-app | Chat request declined | Notify when your chat request is declined |
| `chat_cannot_send_messages` | Невозможно отправить сообщение (ограничения) | ✅ | ❌ | UX-норма | In-app | Messaging restricted | Notify when you can't send messages because of limits, blocks or privacy settings |
| `chat_request_accepted` | Запрос на переписку принят | ✅ | ❌ | UX-норма | In-app | Chat request accepted | Notify when someone accepts your chat request |

---

## 🎁 REWARDS — Награды и бонусы

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `reward_spent` | Бонусы списаны при обмене | ✅ | ❌ | UX-норма | In-app, Push | Rewards redeemed | Notify when your bonus points are spent on a gift or service |
| `reward_new_gift` | Новый подарок разблокирован | ✅ | ❌ | UX-норма | In-app | New gift unlocked | Notify when you unlock a new gift or reward you can claim |
| `reward_daily_bonus` | Доступен ежедневный бонус | ✅ | ❌ | UX-норма | In-app | Daily bonus available | Your daily reward is ready — don't forget to claim it! |

---

## 🟩 BLOGS — Блоги и авторы
> Уведомления о блогах, на которые подписан пользователь

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `blog_new_post_published` | Новый пост опубликован в блоге | ✅ | ❌ | DSA Art.14 | In-app, Push | New post in a blog | Notify when a new post is published in a blog you follow |
| `blog_post_updated` | Пост в блоге обновлён | ✅ | ❌ | UX-норма | In-app | Blog post updated | Notify when a post is updated in a blog you follow |
| `blog_you_follow_updated_info` | Профиль блога обновлён | ✅ | ❌ | UX-норма | In-app | Blog profile updated | Notify when a blog you follow updates its profile information |

### Blogs — Модерация и система
> ⚖️ DSA Art.17–20

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `blog_comment_removed_by_system` | Комментарий удалён модерацией | ✅ 🚫 | ✅ | DSA Art.17–20 | In-app, Email | Comment removed by the system | Notify when a comment under your blog post is removed by the system due to moderation |
| `blog_you_follow_removed` | Блог удалён системой | ✅ 🚫 | ✅ | DSA Art.20 | In-app, Push | Blog removed by system | Notify when the system removes a blog you follow |

### Blogs — Контент и взаимодействия

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `blog_comment_replied` | Ответ на ваш комментарий в блоге | ✅ | ❌ | UX-норма | In-app, Push | Comment reply in a blog post | Notify when someone replies to your comment in a blog post |
| `blog_comment_liked` | Реакция на ваш комментарий в блоге | ✅ | ❌ | UX-норма | In-app | Reaction to your blog comment | Notify when someone reacts to your comment in a blog |

---

## 🟩 COMMUNITY — Сообщества

### Community — Активность

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `community_admin_assigned` | Вас назначили главным администратором | ✅ | ❌ | UX-норма | In-app, Push | Promoted to head admin | Receive notifications when a user is promoted to the head admin role |
| `community_invitation_sent` | Вас пригласили вступить в сообщество | ✅ | ❌ | UX-норма | In-app, Push | Community invitations | Receive notifications when you are invited to join the community as a member |
| `community_join_request_approved` | Ваш запрос на вступление одобрен | ✅ | ❌ | UX-норма | In-app, Push | Approved requests | Receive notifications when join requests are approved |
| `community_join_request_rejected` | Ваш запрос на вступление отклонён | ✅ | ❌ | UX-норма | In-app | Rejected requests | Receive notifications when join requests are declined |
| `community_team_invite_sent` | Вас пригласили в команду (admin/moderator/editor) | ✅ | ❌ | UX-норма | In-app, Push | Community team invitations | Receive notifications about invitations to join a community's team |

### Community — Модерация и система

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `community_profile_updated` | Профиль сообщества обновлён | ✅ | ❌ | UX-норма | In-app | Community profile update | Receive notifications when the community's photo, description, or contact details are updated |
| `community_removed_by_moderation` | Сообщество удалено системой | ✅ 🚫 | ✅ | DSA Art.20 | In-app, Push, Email | Community removed by system | Receive notifications when the community is removed or suspended by the system for violating rules |
| `community_you_were_removed` | Вас исключили из сообщества | ✅ 🚫 | ✅ | DSA Art.17 | In-app, Push | Removed from a community | Notify when you are removed from a community |

---

## 🎯 CHALLENGE — Ежедневные задания

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `challenge_question_available` | Доступен новый вопрос | ✅ | ❌ | UX-норма | In-app, Push | New challenge question | Notify when a new question is available in your challenges |

---

## ⭐ BUSINESS PROFILE — Бизнес-профиль

### Business — Модерация и юридические (⚖️ ОБЯЗАТЕЛЬНО)
> DSA Art.17–20 — нельзя выключить

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `business_profile_removed_by_system` | Профиль удалён или заблокирован системой | ✅ 🚫 | ✅ | DSA Art.20 | In-app, Email | Business profile removed | Notify when your business profile is removed or suspended by the system |
| `business_review_removed_by_moderation` | Отзыв/оценка удалены модерацией | ✅ 🚫 | ✅ | DSA Art.17 | In-app | Review/rating removed by moderation | Notify me when a review or rating on my business profile is removed by moderation |
| `business_review_rejected` | Новый отзыв не прошёл модерацию | ✅ 🚫 | ✅ | DSA Art.20 | In-app | New review not approved | Notify me when a new review on my business profile does not pass moderation and is not published |
| `business_complaint_received` | На бизнес-профиль поступила жалоба | ✅ 🚫 | ✅ | DSA Art.17 | In-app | Complaint about business profile | Notify me when someone files a complaint about my business profile |
| `business_appeal_decision` | Решение по апелляции | ✅ 🚫 | ✅ | DSA Art.20 | In-app, Email | Appeal decision | Notify me when a decision is made on an appeal I submitted about moderation on my business profile |

### Business — Рейтинги и отзывы
> ⚖️ DSA Art.22 — публичные оценки

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `business_new_rating` | Новый рейтинг / отзыв на бизнес | ✅ | ❌ | DSA Art.22 | In-app, Push | New rating/review on business | Notify me when someone leaves a new rating or review on my business profile |
| `business_rating_updated` | Пользователь обновил свою оценку | ✅ | ❌ | UX-норма | In-app | User updated rating | Notify me when a user updates their rating on my business profile |
| `business_rating_removed` | Пользователь удалил свой отзыв | ✅ | ❌ | UX-норма | In-app | User removed their review | Notify me when a user deletes their review on my business profile |
| `business_new_review_comment` | К отзыву добавлен комментарий | ✅ | ❌ | UX-норма | In-app | Comment added to a review | Notify me when someone adds a comment to a review on my business profile |

### Business — Подписчики и взаимодействие

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `business_new_follower` | Новый подписчик | ✅ | ❌ | UX-норма | In-app | New follower | Notify me when someone follows my business profile |
| `business_follower_left` | Пользователь отписался | ✅ | ❌ | UX-норма | In-app | User unfollowed | Notify me when someone unfollows my business profile |
| `business_post_commented` | Комментарий на пост бизнес-профиля | ✅ | ❌ | UX-норма | In-app | Comment on profile post | Notify me when someone comments on a post on my business profile |
| `business_comment_replied` | Ответ на комментарий | ✅ | ❌ | UX-норма | In-app | Reply to comment | Notify me when a reply is posted to a comment on my business profile |
| `business_post_liked` | Реакция на пост | ✅ | ❌ | UX-норма | In-app | Reaction to post | Notify me when someone reacts to a post on my business profile |
| `business_comment_liked` | Реакция на комментарий | ✅ | ❌ | UX-норма | In-app | Reaction to comment | Notify me when someone reacts to a comment on my business profile |

### Business — Обновления профиля

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `business_profile_updated` | Контакты, описание, фото или категория обновлены | ✅ | ❌ | GDPR (security) | In-app, Email | Business details updated | Notify me when contact info, description, photo or category on my business profile is updated |
| `business_hours_updated` | Обновление рабочих часов | ✅ | ❌ | UX-норма | In-app | Business hours updated | Notify me when the business hours on my business profile are updated |
| `business_services_updated` | Добавлены / обновлены услуги | ✅ | ❌ | UX-норма | In-app | Services additions/updates | Notify me when services are added or updated on my business profile |

### Business — Чат

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `chat_new_message_business` | Новое сообщение в бизнес-чат | ✅ | ❌ | UX-норма | In-app, Push | New message in business chat | Notify me when I receive a new message in my business chat |
| `chat_request_business` | Запрос переписки в бизнес-чат | ✅ | ❌ | UX-норма | In-app, Push | Chat request | Notify me when someone sends a chat request to my business profile |
| `chat_reacted_business` | Реакция на сообщение в бизнес-чате | ✅ | ❌ | UX-норма | In-app | Reaction to message | Notify me when someone reacts to a message in my business chat |

### Business — Система и юридические

| Key | Описание (RU) | Default | ⚖️ Закон | Основание | Канал | Title (EN) | Subtitle (EN) |
|---|---|---|---|---|---|---|---|
| `terms_updated_business` | Обновлены Условия платформы | ✅ 🚫 | ✅ | GDPR/DSA | In-app | Terms of Use update (business) | Notify me when changes to the Terms of Use affect business profiles or my rights/obligations as a business |
| `privacy_policy_updated_business` | Обновлена Политика конфиденциальности | ✅ 🚫 | ✅ | GDPR | Email | Privacy Policy update (business) | Notify me when the Privacy Policy is updated regarding how business profile data is collected and used |
| `consent_withdrawn` | Подтверждение отзыва согласия | ✅ 🚫 | ✅ | GDPR Art.7 | Email | Consent withdrawal confirmation | Notify me when a user withdraws consent related to my business profile |
| `account_security_alert` | Подозрительная активность на бизнес-профиле | ✅ 🚫 | ✅ | GDPR | Email, In-app | Suspicious activity on business profile | Notify me when unusual activity or other suspicious behaviour is detected on my business profile |

---

## 📊 Итого по разделам

| Раздел | Кол-во уведомлений | Обязательных по закону (🚫) |
|---|---|---|
| Profile — Аккаунт и безопасность | 11 | 10 |
| Profile — Системные/юридические | 4 | 2 |
| Profile — Контент и модерация | 4 | 4 |
| Profile — Социальная активность | 9 | 0 |
| Chat | 6 | 0 |
| Rewards | 3 | 0 |
| Blogs | 5 | 2 |
| Community | 8 | 2 |
| Challenge | 1 | 0 |
| Business — Модерация/юридические | 5 | 5 |
| Business — Рейтинги и отзывы | 4 | 0 |
| Business — Подписчики | 6 | 0 |
| Business — Обновления профиля | 3 | 0 |
| Business — Чат | 3 | 0 |
| Business — Система/юридические | 4 | 4 |
| **ИТОГО** | **76** | **29** |

---

*Файл: `NotificationsSpec.md` | Версия 1.0 | Только таблицы, без лишнего текста*
