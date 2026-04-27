# Report a Problem — Полная спецификация экранов

**Раздел:** Settings → Help & Support → Report a Problem  
**Обязательно:** ⚖️ DSA Art.14 (механизм жалоб) · DSA Art.16 (уведомление репортёра) · DSA Art.17 (апелляция) · App Store · Google Play Child Safety

---

## Обзор флоу

Система жалоб состоит из **четырёх независимых флоу:**

| Флоу | Кто участвует | Экраны |
|---|---|---|
| A. Подача жалобы | Пользователь-репортёр | 3 экрана |
| B. Уведомление нарушителя | Нарушитель | In-app сообщение + placeholder |
| C. Апелляция | Нарушитель | 2 экрана |
| D. Account Status | Любой пользователь | 1 экран (история) |

---

## A. Флоу репортёра — Подача жалобы

### A-1. Точки входа (откуда открывается Report)

| Контекст | Действие |
|---|---|
| Профиль другого пользователя | Кнопка ⋯ → «Report» |
| Пост / фото | Кнопка ⋯ под постом → «Report» |
| Комментарий | Long press → «Report» |
| Settings → Help & Support | «Report a problem» |

---

### A-2. Экран 1 — Выбор причины (Report Reason)

```
[Bottom sheet или отдельный экран]

Заголовок: «Why are you reporting this?»
Подзаголовок: «Your report is anonymous.»

Список причин (одиночный выбор, radio):
  ○ Spam
  ○ Harassment or bullying
  ○ Hate speech
  ○ Violence or dangerous content
  ○ Nudity or sexual content
  ○ Fraud or scam
  ○ Misinformation
  ○ 🔴 Child Safety (CSAE)          ← обязательная категория (Google Play)
  ○ Intellectual property violation
  ○ Other

[Кнопка: «Next»]
[Кнопка: «Cancel»]
```

> ⚖️ **Обязательно (Google Play Child Safety Standards):** категория «Child Safety» должна присутствовать в списке.  
> ⚖️ **DSA Art.14:** категория незаконного контента (hate speech, CSAE, fraud) обязательна для платформ ЕС.

---

### A-3. Экран 2 — Детали (опциональный)

> Показывается после выбора любой причины, кроме Spam.

```
Заголовок: «Add more details (optional)»
Подзаголовок: «Help us understand the issue.»

Текстовое поле: «Describe the problem...» (max 500 chars)
Прикрепить скриншот: [+] (опционально)

[Кнопка: «Submit Report»]
[Кнопка: «Back»]
```

> ⚖️ **DSA Art.14(2):** пользователь должен иметь возможность объяснить суть жалобы.

---

### A-4. Экран 3 — Подтверждение (Confirmation)

```
Заголовок: «Report submitted»
Иконка: ✅

Текст: «Thanks for letting us know. We'll review this and take action
        if it violates our Community Guidelines.
        We'll notify you of the outcome.»

Разделитель: ─────

Вопрос: «Do you also want to block @username?»
Текст: «They won't be able to see your profile or contact you.»

[Кнопка: «Block @username»]   ← рекомендуется (снижает вред для репортёра)
[Кнопка: «No thanks»]

[Кнопка: «Done»]
```

> ⚖️ **DSA Art.16(5):** платформа обязана уведомить репортёра о результате рассмотрения жалобы.  
> Предложение заблокировать пользователя — лучшая практика (Instagram, TikTok, YouTube).

---

### A-5. Уведомление репортёра о результате

Когда модератор принимает решение, репортёр получает:

| Канал | Ключ уведомления | Текст |
|---|---|---|
| In-app | `report_outcome_action_taken` | «Update on your report: We reviewed the content you reported and took action.» |
| In-app | `report_outcome_no_violation` | «Update on your report: We reviewed the content and found it doesn't violate our guidelines.» |

> ⚖️ **DSA Art.16(5):** уведомление обязательно для платформ ЕС. Содержание решения сообщается без раскрытия личности нарушителя.

---

## B. Флоу нарушителя — Уведомление об удалении контента

### B-1. In-app сообщение (Statement of Reasons)

> Отправляется автоматически, когда модератор удаляет контент.  
> Канал: In-app notification + Email.  
> Ключ: `system_moderation_content_removed`

```
[In-app notification]

Заголовок: «Your content was removed»
Текст:
  «We removed your [post / photo / comment] posted on [date].

   Reason: [Violation category, например: Hate Speech]

   This content violated our Community Guidelines.
   [Read Community Guidelines →]

   If you believe this was a mistake, you can appeal below.»

[Кнопка: «Appeal this decision»]   ← обязательна (DSA Art.17)
[Кнопка: «OK»]
```

> ⚖️ **DSA Art.17(1):** платформа обязана предоставить Statement of Reasons — объяснение, какое правило нарушено.  
> ⚖️ **DSA Art.17(3):** пользователь должен иметь возможность подать апелляцию.

---

### B-2. Placeholder удалённого контента (в ленте автора)

> Другие пользователи не видят удалённый пост вообще.  
> Автор видит placeholder вместо своего поста.

```
[Карточка поста — только для автора]

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

### B-3. Уведомление о жалобе (до решения)

> Отправляется сразу после получения жалобы, до принятия решения.  
> Ключ: `profile_complaint_received`

```
[In-app notification]

Текст: «Someone reported content on your profile.
        We're reviewing it. No action has been taken yet.»
```

> Кто пожаловался — не раскрывается. Это защищает репортёра от преследования.

---

## C. Флоу апелляции

### C-1. Экран 1 — Форма апелляции

```
Заголовок: «Appeal content removal»

Текст: «Tell us why you think this was a mistake.»

Информация об удалённом контенте:
  Тип: Post / Photo / Comment
  Дата удаления: [дата]
  Причина удаления: [Hate Speech]

Текстовое поле: «Explain your appeal...» (обязательное, max 1000 chars)

[Кнопка: «Submit Appeal»]
[Кнопка: «Cancel»]
```

> ⚖️ **DSA Art.17(3)(c):** пользователь должен иметь возможность объяснить, почему считает решение ошибкой.

---

### C-2. Экран 2 — Подтверждение апелляции

```
Заголовок: «Appeal submitted»
Иконка: ✅

Текст: «We've received your appeal. A human moderator will review
        your case within 5 business days.
        We'll notify you of the outcome by email and in-app.»

[Кнопка: «Done»]
```

---

### C-3. Уведомление о решении по апелляции

| Канал | Ключ | Текст |
|---|---|---|
| In-app + Email | `profile_appeal_decision` | «Your appeal has been reviewed. [Решение: Content restored / Removal upheld]. [Reason].» |

> ⚖️ **DSA Art.17(4):** решение по апелляции должно быть мотивировано.

---

## D. Account Status — История жалоб и нарушений

**Раздел:** Settings → Help & Support → Account Status  
*(или: Settings → Help & Support → My Reports & Violations)*

> Этот экран снижает нагрузку на поддержку: пользователь сам видит, что происходит с его жалобами и контентом.

### D-1. Структура экрана

```
Account Status
├── Вкладка: «My Reports» (жалобы, которые я подал)
└── Вкладка: «My Violations» (удалённый мой контент)
```

---

### D-2. Вкладка «My Reports» (жалобы репортёра)

```
My Reports

[Список жалоб]

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

**Статусы:**
- `● Under review` — на рассмотрении
- `✅ Action taken` — контент удалён / пользователь заблокирован
- `ℹ️ No violation found` — нарушений не найдено

> Имя пользователя, на которого подана жалоба, **не показывается** — только тип контента.  
> Это защищает анонимность: если репортёр видит «action taken» или «no violation», этого достаточно.

---

### D-3. Вкладка «My Violations» (нарушения пользователя)

```
My Violations

Предупреждение (если есть страйки):
┌─────────────────────────────────────┐
│  ⚠️ 1 strike on your account       │
│  3 strikes may result in account    │
│  suspension.                         │
└─────────────────────────────────────┘

[Список удалённого контента]

┌─────────────────────────────────────┐
│  Post removed                        │
│  Date: 12 Apr 2026                   │
│  Reason: Hate Speech                 │
│  Appeal status: Not submitted        │
│  [Submit Appeal →]                   │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Comment removed                     │
│  Date: 1 Mar 2026                    │
│  Reason: Spam                        │
│  Appeal status: ✅ Upheld — Removed │
└─────────────────────────────────────┘
```

---

## Уведомления, связанные с жалобами (сводка)

| Ключ | Кому | Нельзя выключить | Канал |
|---|---|---|---|
| `profile_complaint_received` | Нарушителю | ⚖️ DSA Art.17 | In-app |
| `system_moderation_content_removed` | Нарушителю | ⚖️ DSA Art.17 | Email · In-app |
| `profile_appeal_decision` | Нарушителю (апеллянту) | ⚖️ DSA Art.17 | Email · In-app |
| `report_outcome_action_taken` | Репортёру | ⚖️ DSA Art.16 | In-app |
| `report_outcome_no_violation` | Репортёру | ⚖️ DSA Art.16 | In-app |

---

## Что нужно дизайнеру — список экранов

| # | Экран | Тип |
|---|---|---|
| 1 | Выбор причины жалобы | Bottom sheet / Full screen |
| 2 | Детали жалобы (текст + скриншот) | Full screen |
| 3 | Подтверждение жалобы + предложение Block | Full screen |
| 4 | In-app уведомление: контент удалён (Statement of Reasons) | In-app notification |
| 5 | Placeholder удалённого поста в ленте автора | Card (inline в ленте) |
| 6 | Форма апелляции | Full screen |
| 7 | Подтверждение апелляции | Full screen |
| 8 | Account Status → My Reports | Full screen |
| 9 | Account Status → My Violations | Full screen |
