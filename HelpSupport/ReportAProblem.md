# UGC Moderation — Report a Problem: Полная спецификация

**Разделы в приложении:**
- Кнопка Report — на каждом посте, профиле, комментарии, DM
- Settings → My Reports (история жалоб)
- Settings → Help & Support → Report a Problem (точка входа из настроек)

**Обязательно:**
⚖️ DSA Art.14 (механизм жалоб на незаконный контент) · DSA Art.16 (уведомление репортёра о результате) · DSA Art.17 (Statement of Reasons)

---

## Обзор системы

| Компонент | Кто участвует | Где |
|---|---|---|
| 🚩 Report Button + Report Menu | Репортёр | Везде: пост, профиль, комментарий, DM |
| 🚫 Block User Button | Репортёр | Профиль, после Report |
| Alert — Submit report | Репортёр | Перед отправкой жалобы |
| Статусы жалобы | Репортёр | Settings → My Reports |
| Уведомление о жалобе | Нарушитель | In-app (до решения) |
| Content Moderation (AI + Human) | Нарушитель | In-app |
| Statement of Reasons (DSA Art.17) | Нарушитель | In-app + Email |
| Appeal — DSA Art.20 | Нарушитель | In-app |
| Appeal при AI-удалении — GDPR Art.22 | Нарушитель | In-app |
| Модерация DM/чатов | Участники чата | In-app |
| Anti-Spam — автоматика | Система | Фон |
| My Reports (история) | Любой пользователь | Settings → My Reports |

---

## 1. 🚩 Report Button — Кнопка «Пожаловаться»

> ⚖️ **Apple §1.2 · DSA Art.14 · Google Play:** кнопка Report обязательна на всём пользовательском контенте.  
> Кнопка должна быть доступна **на каждом посте, профиле, комментарии и в личных сообщениях.**

### 1.1 Расположение кнопки

| Контекст | Доступ | Иконка / метка |
|---|---|---|
| Пост / фото в ленте | Кнопка ⋯ (три точки) под постом | 🚩 «Report» |
| Страница поста (detail view) | Кнопка ⋯ вверху справа | 🚩 «Report» |
| Профиль другого пользователя | Кнопка ⋯ на странице профиля | 🚩 «Report» |
| Комментарий | Long press на комментарии | 🚩 «Report» |
| Личное сообщение (DM) | Long press на сообщении | 🚩 «Report» |
| Чат (беседа целиком) | Кнопка ⋯ в шапке чата | 🚩 «Report conversation» |
| Settings → Help & Support | Строка «Report a problem» | 🚩 «Report a problem» |

> Кнопка не показывается на **собственном** контенте пользователя.

---

## 2. 🚫 Block User Button — Кнопка «Заблокировать»

> Блокировка — немедленное действие, не требует проверки модератором.  
> Может использоваться **вместе** с жалобой или **без неё**.

### 2.1 Расположение

| Контекст | Действие |
|---|---|
| Профиль пользователя → ⋯ | «Block» (отдельный пункт, рядом с «Report») |
| После подачи жалобы (экран подтверждения) | Предложение «Also block @username?» |
| Settings → Privacy & Visibility → Blocked Accounts | Добавить вручную |

### 2.2 Поведение после блокировки

| Что меняется | Для кого |
|---|---|
| Заблокированный не видит профиль блокирующего | Заблокированный |
| Заблокированный не может написать сообщение | Заблокированный |
| Заблокированный не отображается в поиске (для блокирующего) | Оба |
| Уведомление о блокировке | ❌ Не отправляется (защита блокирующего) |

---

## 3. Report Menu — Список причин жалобы

> Открывается сразу после нажатия 🚩 Report.  
> Тип: bottom sheet или full-screen modal.

```
[Bottom sheet]

Заголовок: «Why are you reporting this?»
Подзаголовок: «Your report is anonymous.»

Список причин (radio, одиночный выбор):
  ○ Spam
  ○ Harassment or bullying
  ○ Hate speech
  ○ Violence or dangerous content
  ○ Nudity or sexual content
  ○ Fraud or scam
  ○ Misinformation / False information
  ○ 🔴 Child Safety (CSAE)            ← обязательно (Google Play Child Safety)
  ○ Intellectual property violation
  ○ Other

[Кнопка: «Next»  — активна только после выбора]
[Кнопка: «Cancel»]
```

> ⚖️ **Google Play Child Safety Standards:** категория «Child Safety» обязательна.  
> ⚖️ **DSA Art.14:** категории незаконного контента (hate speech, CSAE, violence, fraud) обязательны для платформ ЕС.  
> ⚖️ **Apple §1.2:** механизм жалоб на оскорбительный UGC обязателен.

### 3.1 Экран деталей (после выбора причины)

> Показывается для всех причин, кроме Spam.

```
Заголовок: «Add more details (optional)»
Подзаголовок: «Help us understand the issue.»

Текстовое поле: «Describe the problem...» (max 500 chars)
Прикрепить скриншот: [+] (опционально)

[Кнопка: «Next»]
[Кнопка: «Back»]
```

> ⚖️ **DSA Art.14(2):** пользователь должен иметь возможность объяснить суть жалобы.

---

## 4. Alert — Submit Report (Подтверждение перед отправкой)

> Системный алерт перед финальной отправкой — защита от случайных жалоб.

```
[System Alert]

Заголовок: «Submit report?»
Текст:
  «You're reporting this [post / comment / profile] for [Reason].
   This report is anonymous.»

[Кнопка: «Submit»]    ← основное действие
[Кнопка: «Cancel»]
```

---

## 5. Подтверждение отправки (Success Screen)

```
Заголовок: «Report submitted»
Иконка: ✅

Текст: «Thanks for letting us know. We will review your report and take action if it violates our Community Guidelines. You will be notified of the outcome.»

Текст (конфиденциальность): «Your identity is kept confidential — the reported user will NOT know who reported them.»

────────────────────────────

Вопрос: «Want to block @username?»
Текст: «They will no longer be able to view your content or interact with you.»

[Кнопка: «Block @username»]
[Кнопка: «No thanks»]

[Кнопка: «Done»]
```

> ⚖️ **DSA Art.16(5):** платформа обязана уведомить репортёра о результате.  
> Предложение заблокировать — лучшая практика (снижает вред для репортёра).

---

## 6. Уведомление заявителю о результате жалобы

> ⚖️ **DSA Art.16 — обязательно.** Платформа обязана уведомить репортёра о результате.

| Канал | Ключ | Текст |
|---|---|---|
| In-app | `report_outcome_action_taken` | «Update on your report: We reviewed the content you reported and took action.» |
| In-app | `report_outcome_no_violation` | «Update on your report: We reviewed the content and found it doesn't violate our guidelines.» |

> Имя нарушителя в уведомлении **не раскрывается**.

---

## 7. Content Moderation — Уведомление нарушителю

### 7.1 Уведомление о жалобе (до решения)

> Отправляется сразу после получения жалобы — до того как модератор принял решение.  
> Ключ: `profile_complaint_received`

```
[In-app notification]

Заголовок: «Complaint about your content»
Текст: «Someone reported content on your profile.
        We're reviewing it. No action has been taken yet.»
```

> Кто пожаловался — **не раскрывается**. Защищает репортёра от мести.

### 7.2 Контент удалён — Statement of Reasons (DSA Art.17)

> Отправляется, когда **модератор (или AI)** принял решение удалить контент.  
> Ключ: `system_moderation_content_removed`  
> Каналы: Email + In-app

```
[In-app / Email]

Заголовок: «Your content was removed»
Текст:
  «We removed your [post / photo / comment] posted on [дата].

   Reason: [Violation category — например: Hate Speech]

   This content violated our Community Guidelines:
   [Ссылка: Read Community Guidelines →]

   If you believe this was a mistake, you can appeal this decision.»

[Кнопка: «Appeal this decision»]   ← обязательна (DSA Art.20)
[Кнопка: «OK»]
```

> ⚖️ **DSA Art.17(1):** Statement of Reasons обязателен — нужно указать конкретное правило, которое нарушено.  
> ⚖️ **DSA Art.20:** пользователь должен иметь возможность обжаловать любое решение.

### 7.3 Контент не прошёл модерацию (при публикации)

> Контент заблокирован до публикации (pre-moderation).  
> Ключ: `system_moderation_content_rejected`

```
[In-app]

Заголовок: «Content not approved»
Текст: «Your [post / photo] was not published because it doesn't meet
        our Community Guidelines.
        Reason: [категория]»

[Кнопка: «Appeal»]
[Кнопка: «Edit and repost»]
[Кнопка: «OK»]
```

### 7.4 Placeholder удалённого контента (в ленте автора)

> Другие пользователи удалённый пост **не видят вообще**.  
> Автор видит placeholder на месте своего поста.

```
┌─────────────────────────────┐
│  ⚠️ Content removed         │
│  This post was removed for  │
│  violating Community        │
│  Guidelines.                │
│  Reason: [Hate Speech]      │
│  [Appeal →]                 │
└─────────────────────────────┘
```

---

## 8. Обжалование (Appeal) — DSA Art.20

> ⚖️ **DSA Art.20:** право на апелляцию обязательно для **каждого** решения об удалении контента.  
> Апелляция всегда рассматривается **живым модератором** (не AI).

### 8.1 Экран 1 — Форма апелляции

```
Заголовок: «Appeal content removal»

Информация об удалённом контенте:
  Тип: Post / Photo / Comment
  Дата удаления: [дата]
  Причина удаления: [Hate Speech]

Текст: «Tell us why you think this was a mistake.»
Поле: «Explain your appeal...» (обязательное, max 1000 chars)

[Кнопка: «Submit Appeal»]
[Кнопка: «Cancel»]
```

### 8.2 Экран 2 — Подтверждение апелляции

```
Заголовок: «Appeal submitted»
Иконка: ✅

Текст: «We've received your appeal. A human moderator will review
        your case within 5 business days.
        We'll notify you of the outcome by email and in-app.»

[Кнопка: «Done»]
```

### 8.3 Уведомление о решении по апелляции

> Ключ: `profile_appeal_decision`  
> Каналы: Email + In-app

| Решение | Текст уведомления |
|---|---|
| Апелляция удовлетворена | «Your appeal was approved. Your content has been restored.» |
| Апелляция отклонена | «Your appeal was reviewed. The removal decision was upheld. [Reason].» |

> ⚖️ **DSA Art.20(4):** решение по апелляции должно быть мотивировано.

---

## 9. Кнопка «Appeal» при AI-удалении (GDPR Art.22 + DSA Art.20)

> Если контент удалён **автоматически (AI)** — пользователь имеет право потребовать проверки **человеком**.  
> ⚖️ **GDPR Art.22:** запрещено принимать юридически значимые решения исключительно автоматически без возможности оспаривания.
> ⚖️ **DSA Art.20:** апелляция на любое решение о модерации.

### Отличие от стандартной апелляции

| Параметр | Стандартная апелляция | AI-удаление |
|---|---|---|
| Инициатор удаления | Модератор (человек) | AI / автоматика |
| Метка в уведомлении | — | «Removed automatically» |
| Текст кнопки | «Appeal» | «Request human review» |
| Срок рассмотрения | 5 рабочих дней | 5 рабочих дней |
| Кто рассматривает апелляцию | Модератор 2 | Модератор (всегда человек) |

### Уведомление об AI-удалении

```
[In-app]

Заголовок: «Your content was removed automatically»
Текст:
  «Your [post / photo] was automatically removed on [дата]
   because it may violate our guidelines on [причина].

   If you believe this was a mistake, you can request
   a review by a human moderator.»

[Кнопка: «Request human review»]   ← GDPR Art.22
[Кнопка: «OK»]
```

---

## 10. Сроки рассмотрения

> ⚖️ **DSA Art.14–20:** сроки обязательны для платформ ЕС.

| Тип | Срок | Кто рассматривает |
|---|---|---|
| CSAE / незаконный контент | ≤ 24 ч | Специальная CSAE-команда |
| Стандартная жалоба (Spam, Harassment и др.) | ≤ 5 рабочих дней | Модератор |
| Апелляция (стандартная) | ≤ 5 рабочих дней | Модератор 2 (не тот, кто удалял) |
| Апелляция при AI-удалении | ≤ 5 рабочих дней | Модератор-человек |
| Ответ на GDPR-запрос | ≤ 30 дней | DPO / Privacy Officer |

---

## 11. Проверка достоверности информации (Misinformation)

> Жалоба с причиной **«Misinformation / False information»** обрабатывается отдельным флоу.

| Шаг | Действие |
|---|---|
| 1 | Жалоба поступает → тег `fact_check_required` |
| 2 | AI делает предварительную оценку + добавляет метку «Disputed» на контент |
| 3 | Модератор проверяет + при необходимости привлекает fact-check партнёра |
| 4 | Решения: Verified / Disputed (остаётся с меткой) / Removed |

**Метка «Disputed» (на контенте, видна всем):**
```
┌─────────────────────────────────────┐
│  ⚠️ This post contains disputed    │
│  information.                        │
│  [Learn more →]                      │
└─────────────────────────────────────┘
```

> Автор видит ту же метку и может подать апелляцию через стандартный флоу (п. 8).

---

## 12. 💬 Модерация личных сообщений (DM / Чаты)

> ⚖️ **DSA Art.14 · Apple §1.2:** механизм жалоб обязателен в том числе в личных сообщениях.

### 12.1 Точки входа для Report в чате

| Действие | Результат |
|---|---|
| Long press на конкретном сообщении → «Report» | Жалоба на одно сообщение |
| ⋯ в шапке чата → «Report conversation» | Жалоба на весь диалог |
| ⋯ в шапке чата → «Block user» | Блокировка + закрытие чата |

### 12.2 Report Menu в чате (дополнительные категории)

```
Список причин для DM:
  ○ Spam or unwanted messages
  ○ Harassment or threats
  ○ Sending harmful content (images / links)
  ○ Fraud or scam attempt
  ○ 🔴 Child Safety (CSAE)
  ○ Other
```

### 12.3 Поведение после блокировки в чате

- Чат остаётся в истории (только для заблокировавшего).
- Заблокированный не может написать новые сообщения.
- Уведомление заблокированному **не отправляется**.

### 12.4 Конфиденциальность при модерации DM

> Содержание личных сообщений модератор **не читает** без веских оснований.  
> При жалобе: модератор видит только **флаг жалобы + категорию + конкретное сообщение**, на которое пожаловались.
> При CSAE: полный доступ к чату + обязательный репорт в NCMEC.

---

## 13. Автоматическая система защиты (Anti-Spam)

> Работает в фоне, пользователю не видна. Снижает нагрузку на модераторов.

| Триггер | Автодействие |
|---|---|
| Одинаковый текст/ссылки в N постах за короткое время | Временный hold (задержка публикации) |
| Новый аккаунт рассылает DM сразу нескольким пользователям | Капча / временный лимит на DM |
| Ссылка из блэклиста (фишинг, malware) | Автоблокировка ссылки + уведомление пользователю |
| Одинаковые комментарии на разных постах | Автоскрытие + флаг для модератора |
| > 10 жалоб «Spam» на одного пользователя за 24 ч | Временная приостановка аккаунта + review |

**Уведомление пользователю при автоматическом ограничении:**
```
[In-app]

Текст: «Your account has been temporarily limited due to
        unusual activity. This may have been a mistake.
        If you believe this is an error, please contact support.»

[Кнопка: «Contact Support»]
[Кнопка: «OK»]
```

---

## 14. Settings → My Reports (История жалоб)

**Расположение:** `Settings → My Reports`  
*(также доступно через Settings → Help & Support → Report a problem)*

> Экран снижает нагрузку на поддержку: пользователь сам отслеживает статус своих жалоб и нарушений.

### 14.1 Структура экрана

```
My Reports
├── Вкладка: «Submitted» (жалобы, которые я подал)
└── Вкладка: «My content» (мой удалённый / оспариваемый контент)
```

### 14.2 Вкладка «Submitted» — Жалобы репортёра

```
Submitted Reports

┌─────────────────────────────────────┐
│  Report #1042                        │
│  Type: Post                          │
│  Reason: Harassment                  │
│  Submitted: 12 Apr 2026              │
│  Status: ● Under review             │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Report #1038                        │
│  Type: User profile                  │
│  Reason: Spam                        │
│  Submitted: 5 Apr 2026               │
│  Status: ✅ Action taken            │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Report #1021                        │
│  Type: Comment                       │
│  Reason: Hate Speech                 │
│  Submitted: 28 Mar 2026              │
│  Status: ℹ️ No violation found      │
└─────────────────────────────────────┘
```

**Статусы жалобы (DSA Art.17 — уведомление о результате):**

| Статус | Значение |
|---|---|
| `● Under review` | Жалоба принята, рассматривается |
| `✅ Action taken` | Контент удалён / аккаунт ограничен |
| `ℹ️ No violation found` | Нарушений не найдено |

> Имя пользователя, на которого подана жалоба, **не показывается** — только тип контента.

### 14.3 Вкладка «My content» — Мои нарушения

```
My Content

Предупреждение (если есть активные страйки):
┌─────────────────────────────────────┐
│  ⚠️ 1 active strike on your account│
│  3 strikes may result in account    │
│  suspension.                         │
└─────────────────────────────────────┘

[Список удалённого/оспариваемого контента]

┌─────────────────────────────────────┐
│  Post removed                        │
│  Date: 12 Apr 2026                   │
│  Reason: Hate Speech                 │
│  Removed by: Moderator              │
│  Appeal: Not submitted               │
│  [Submit Appeal →]                   │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Photo removed automatically        │
│  Date: 8 Apr 2026                   │
│  Reason: Nudity                      │
│  Removed by: AI (automatic)         │
│  Appeal: Requested human review ↻  │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Comment removed                     │
│  Date: 1 Mar 2026                    │
│  Reason: Spam                        │
│  Removed by: Moderator              │
│  Appeal: ✅ Upheld — Removal stands │
└─────────────────────────────────────┘
```

---

## 15. Уведомления — Сводная таблица

> Все уведомления из `NotificationsSpec.md`, связанные с модерацией.  
> Нельзя выключить (🚫).

| Ключ | Кому | Закон | Канал | Title (EN) |
|---|---|---|---|---|
| `profile_complaint_received` | Нарушителю | ⚖️ DSA Art.17 | In-app | «Complaint about your content» |
| `system_moderation_content_removed` | Нарушителю | ⚖️ DSA Art.17 | Email, In-app | «Content removed by moderation» |
| `system_moderation_content_rejected` | Нарушителю | ⚖️ GDPR Art.20 | In-app | «Content not approved» |
| `profile_appeal_decision` | Нарушителю (апеллянту) | ⚖️ DSA Art.20 / GDPR Art.22 | Email, In-app | «Decision on your appeal» |
| `report_outcome_action_taken` | Репортёру | ⚖️ DSA Art.16 | In-app | «Update on your report» |
| `report_outcome_no_violation` | Репортёру | ⚖️ DSA Art.16 | In-app | «Update on your report» |
| `profile_account_suspended` | Нарушителю | ⚖️ DSA Art.20 | Email, In-app | «Account blocked or suspended» |

---

## 16. Список экранов для дизайнера

| # | Экран | Тип |
|---|---|---|
| 1 | Report Menu — выбор причины | Bottom sheet |
| 2 | Детали жалобы (текст + скриншот) | Full screen |
| 3 | Alert — «Submit report?» | System alert |
| 4 | Подтверждение жалобы + предложение Block | Full screen |
| 5 | In-app: жалоба получена (до решения) | Push / In-app banner |
| 6 | In-app + Email: контент удалён (Statement of Reasons) | In-app modal |
| 7 | In-app: контент удалён AI («Request human review») | In-app modal |
| 8 | Placeholder удалённого поста в ленте автора | Card (inline) |
| 9 | Метка «Disputed» на посте (misinformation) | Card overlay |
| 10 | Форма апелляции (standard) | Full screen |
| 11 | Форма «Request human review» (AI-removal) | Full screen |
| 12 | Подтверждение апелляции | Full screen |
| 13 | Settings → My Reports → «Submitted» | Full screen |
| 14 | Settings → My Reports → «My content» | Full screen |

---

## 17. Структура БД (Таблица Reports)

| Поле / Колонка | Тип данных | Обязательно | Описание |
| :--- | :--- | :---: | :--- |
| `id` | UUID / BigInt | Да | Первичный ключ (например, Report #1042). |
| `reporter_id` | UUID (FK) | Да | Кто отправил жалобу (нужно для отправки результата по DSA Art.16). |
| `reported_user_id` | UUID (FK) | Да | На кого пожаловались. |
| `target_type` | Enum | Да | Тип контента: `post`, `comment`, `profile`, `dm`, `chat`. |
| `target_id` | UUID (FK) | Да | ID конкретного поста, комментария или сообщения. |
| `reason` | Enum | Да | Причина (Spam, Harassment, Hate Speech, CSAE и т.д.). |
| `details` | Text | Нет | Текст от пользователя (макс 500 символов). |
| `status` | Enum | Да | `under_review`, `action_taken`, `no_violation`. |
| `created_at` | Timestamp | Да | Дата создания (отсчет 24ч или 5 дней для SLA). |
| `updated_at` | Timestamp | Да | Дата последнего изменения статуса. |
| `resolved_at` | Timestamp | Нет | Дата и время, когда модератор принял решение. От нее идет отсчет хранения. |
| `retention_expires_at` | Timestamp | Нет | Точная дата, когда скрипт должен навсегда удалить этот репорт (например, `resolved_at` + 6 месяцев). |
| `legal_hold` | Boolean | Да (по умолчанию `false`) | Замок для тяжелых нарушений (CSAE, терроризм). Если `true`, скрипт игнорирует жалобу и хранит ее до 7 лет. |

---

## 18. Сроки хранения данных (Data Retention)

> Все удаленные данные переходят в состояние **Soft Delete** (скрыты от пользователей). Физическое удаление (Hard Delete) делает скрипт (Cron) по истечении срока.

### 1. Если жалоба отклонена (No Violation)
* **Ситуация:** Кто-то кинул репорт, но модератор проверил и нарушений нет. Контент остается публичным.
* **Срок хранения репорта:** **90 дней**.
* **Действие:** Запись о жалобе хранится 3 месяца для аналитики ложных репортов, затем удаляется навсегда из базы.

### 2. Обычное нарушение (Spam, Harassment, Nudity)
* **Ситуация:** Модератор подтвердил нарушение, удалил контент и закрыл жалобу.
* **Срок хранения репорта и контента:** **Строго 6 месяцев**.
* **Действие:** По закону DSA у нарушителя есть полгода на апелляцию. Пост скрывается, но хранится в базе вместе с логом модератора. Через 6 месяцев скрипт удаляет всё навсегда. Удаленный медиафайл перемещается в скрытый защищенный бакет.

### 3. Тяжелые нарушения и Криминал (CSAE, Угрозы жизни, Fraud, Терроризм)
* **Ситуация:** Обнаружен нелегальный контент (потенциальное уголовное дело).
* **Срок хранения репорта и контента:** **До 7 лет (Бессрочная заморозка / Legal Hold)**.
* **Действие:** Контент немедленно скрывается от пользователей. На саму жалобу, на удаленный контент (фото/видео) и на переписку вешается железная метка `legal_hold`. Скрипт автоматического удаления всегда обходит этот репорт стороной. Данные сохраняются для передачи в полицию/суд по официальному запросу.

---

## 19. Требования к Terms of Service (ToS) и Privacy Policy
Для соответствия законам (ЕС, США, Канада, Израиль) необходимо добавить следующие пункты:

### В Privacy Policy (Раздел Data Retention):
1. **Срок апелляций:** Указать, что удаленный за нарушения контент и логи жалоб хранятся до 6 месяцев для обеспечения права пользователя на апелляцию (согласно DSA).
2. **Legal Hold (Заморозка данных):** Платформа оставляет за собой право сохранять данные (включая IP, переписку и медиа), несмотря на запросы пользователя на удаление профиля, если аккаунт или контент вовлечен в мошенничество, угрозы жизни, распространение CSAE или другие уголовные преступления. Данные могут храниться до 7 лет или до завершения расследования правоохранительными органами.

### В Terms of Service (Раздел Safety & Moderation):
1. Уведомить пользователей о праве платформы скрывать или удалять контент, нарушающий правила.
2. Указать право пользователя на апелляцию в установленные сроки.
3. Четко прописать, что удаление пользователем своего аккаунта с целью сокрытия нарушения или незаконной деятельности не приведет к немедленному физическому уничтожению этих данных на серверах платформы.

---

## Связанные файлы

- [ModerationAdminGuide.md](ModerationAdminGuide.md) — процессы модератора, страйки, Trust Score, CSAE-протокол
- [ChildSafety.md](ChildSafety.md) — отдельный экран Child Safety
- [ContactSupport.md](ContactSupport.md) — контакты поддержки, сроки ответа
- `NotificationsSpec.md` — все ключи уведомлений с каналами
- `TermsOfService.md` → раздел 9 «Safety, Blocking, and Reporting»
