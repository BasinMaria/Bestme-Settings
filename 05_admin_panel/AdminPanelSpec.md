# Admin Panel — Спецификация бэкофиса BestMe

**Версия:** 1.0 · **Дата:** май 2026  
**Кому:** Бэкенд-разработчик, Фронтенд-разработчик (веб), DevOps, Команда модерации  
**Статус:** 🔴 Часть функций является блокером публикации (DSA Art.14 · Google Play Child Safety)

> **Смежные документы:**  
> [../04_moderation/ModerationAdminGuide.md](../04_moderation/ModerationAdminGuide.md) — бизнес-процессы модерации  
> [../06_database/DatabaseSchema.md](../06_database/DatabaseSchema.md) — схема базы данных  
> [../01_legal/TermsOfService.md](../01_legal/TermsOfService.md) — правила платформы  
> [../02_compliance/LegalComplianceSpec.md](../02_compliance/LegalComplianceSpec.md) — правовые требования

---

## Содержание

1. [Роли и права доступа](#1-роли-и-права-доступа)
2. [Moderation Dashboard — Очередь жалоб](#2-moderation-dashboard)
3. [Карточка тикета](#3-карточка-тикета)
4. [User Management — управление аккаунтами](#4-user-management)
5. [Appeals Queue — очередь апелляций](#5-appeals-queue)
6. [CSAE Queue — экстренная очередь](#6-csae-queue)
7. [Statistics Dashboard](#7-statistics-dashboard)
8. [Audit Log — журнал действий модератора](#8-audit-log)
9. [Settings — настройки платформы](#9-settings)
10. [Технические требования](#10-технические-требования)

---

## 1. Роли и права доступа

### 1.1 Таблица ролей

| Роль | Кто | Права |
|---|---|---|
| **Moderator** | Рядовой модератор | Просмотр тикетов · Dismiss · Remove content · Warn user |
| **Senior Moderator** | Старший модератор | Всё Moderator + Suspend account (≤30 дней) · Рассмотрение апелляций |
| **Admin** | Администратор платформы | Всё Senior + Permanent ban · Снятие страйков · Настройки платформы · Экспорт данных |
| **Safety Officer** | Офицер безопасности | Доступ к CSAE очереди · Подача репортов в NCMEC · Координация с правоохранителями |
| **DPO** | Data Protection Officer | Только чтение: Consent History · Audit Log · запросы GDPR Art.15–22 |
| **SuperAdmin** | CTO / основатель | Полный доступ + управление ролями пользователей |

### 1.2 Матрица прав

| Действие | Moderator | Senior | Admin | Safety Officer | DPO | SuperAdmin |
|---|---|---|---|---|---|---|
| Просмотр тикетов | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| Dismiss (закрыть без действий) | ✅ | ✅ | ✅ | ❌ | ❌ | ✅ |
| Remove content | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| Warn user (+страйк) | ✅ | ✅ | ✅ | ❌ | ❌ | ✅ |
| Suspend account ≤30 дней | ❌ | ✅ | ✅ | ❌ | ❌ | ✅ |
| Suspend account >30 дней | ❌ | ❌ | ✅ | ❌ | ❌ | ✅ |
| Permanent ban | ❌ | ❌ | ✅ | ✅ (CSAE only) | ❌ | ✅ |
| Рассмотрение апелляций | ❌ | ✅ | ✅ | ❌ | ❌ | ✅ |
| Доступ к CSAE очереди | ❌ | ❌ | ✅ | ✅ | ❌ | ✅ |
| Репорт в NCMEC | ❌ | ❌ | ❌ | ✅ | ❌ | ✅ |
| Снятие страйка | ❌ | ❌ | ✅ | ❌ | ❌ | ✅ |
| Просмотр Audit Log | ❌ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Просмотр Consent History | ❌ | ❌ | ✅ | ❌ | ✅ | ✅ |
| Настройки платформы | ❌ | ❌ | ✅ | ❌ | ❌ | ✅ |
| Управление ролями | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |
| Экспорт данных | ❌ | ❌ | ✅ | ❌ | ✅ (только GDPR) | ✅ |

> ⚖️ **GDPR Art.32:** Доступ к личным данным пользователей — только у ролей с явным служебным основанием. Логируется каждый просмотр.

---

## 2. Moderation Dashboard

**URL:** `/admin/moderation`  
**Кто видит:** Moderator, Senior, Admin, Safety Officer, SuperAdmin

### 2.1 Структура экрана

```
┌─────────────────────────────────────────────────────────────┐
│ MODERATION DASHBOARD                          [👤 Admin ▾]  │
├──────────────────┬──────────────────────────────────────────┤
│ 🔴 CSAE          │  Queue                                    │
│ 📋 All Reports   │  ┌─────────────────────────────────────┐ │
│ ⏳ Pending       │  │ Filters: [Status ▾] [Category ▾]    │ │
│ ✅ Resolved      │  │         [Date ▾] [Priority ▾]       │ │
│ 🔁 Appeals       │  ├─────────────────────────────────────┤ │
│ ──────────────── │  │ #1042 | 🔴 Child Safety | OPEN      │ │
│ 👤 Users         │  │ @reporter → @offender | 2 min ago   │ │
│ 📊 Statistics    │  ├─────────────────────────────────────┤ │
│ 🔒 Audit Log     │  │ #1041 | Harassment | OPEN           │ │
│ ⚙️ Settings      │  │ @user_a → @user_b | 15 min ago      │ │
│                  │  ├─────────────────────────────────────┤ │
│                  │  │ #1040 | Spam | OPEN                  │ │
│                  │  │ @user_c → @user_d | 1 hr ago        │ │
│                  │  └─────────────────────────────────────┘ │
└──────────────────┴──────────────────────────────────────────┘
```

### 2.2 Счётчики в шапке

| Счётчик | Что показывает |
|---|---|
| 🔴 CSAE | Тикеты с категорией Child Safety — требуют ответа ≤1 ч |
| ⏳ Pending | Все открытые тикеты (не CSAE) |
| 🔁 Appeals | Поданные апелляции, ожидающие рассмотрения |
| ⚠️ Overdue | Тикеты просрочены (>24 ч CSAE или >5 дней стандарт) |

### 2.3 Строка тикета в списке

| Поле | Значение |
|---|---|
| Номер тикета | `#1042` |
| Приоритет | 🔴 CSAE / 🟠 Illegal / 🟡 Standard |
| Категория | Child Safety / Harassment / Spam / Hate Speech / Misinformation / Other |
| Статус | OPEN / IN_REVIEW / RESOLVED / APPEAL_OPEN / CLOSED |
| Reporter trust score | ⭐⭐⭐ (скрыт от нарушителя, виден модератору) |
| Время поступления | Относительное ("2 min ago") |

---

## 3. Карточка тикета

**URL:** `/admin/moderation/{ticket_id}`

### 3.1 Структура

```
┌─────────────────────────────────────────────────────────────┐
│ Ticket #1042                         Status: 🔴 OPEN (CSAE) │
├─────────────────────────────────────────────────────────────┤
│ REPORTER            │ OFFENDER                              │
│ @anna_k (ID: 9821)  │ @user_xyz (ID: 4521)                  │
│ Trust Score: ⭐⭐⭐  │ Strikes: 0 | Joined: Jan 2026         │
│ Reports filed: 3    │ Reports received: 1                   │
├─────────────────────────────────────────────────────────────┤
│ REPORTED CONTENT                                            │
│ Type: Post | Post ID: p_88712                               │
│ [Превью контента — размыт до нажатия "View"]               │
│ [🔍 View Content]                                           │
├─────────────────────────────────────────────────────────────┤
│ REPORT REASON: Child Safety                                  │
│ Reporter note: "Это изображение эксплуатирует ребёнка"      │
├─────────────────────────────────────────────────────────────┤
│ OFFENDER HISTORY                                            │
│ Prior violations: 0 | Prior reports received: 0             │
├─────────────────────────────────────────────────────────────┤
│ ACTIONS                                                     │
│ [✅ Dismiss — No violation]  [🗑 Remove content]            │
│ [⚠️ Warn user]  [⏸ Suspend]  [🚫 Permanent ban]            │
│ [🔴 Escalate to CSAE team]  [📋 Report to NCMEC]           │
│                                                             │
│ Internal note (not visible to users):                       │
│ [_________________________________]  [Save note]            │
└─────────────────────────────────────────────────────────────┘
```

### 3.2 Действия модератора и их последствия

| Действие | Кто может | Что происходит | Уведомление |
|---|---|---|---|
| **Dismiss** | Moderator+ | Тикет → CLOSED · Нарушений не найдено | Репортёру: `report_outcome_no_violation` |
| **Remove content** | Moderator+ | Контент скрыт для всех · Страйк +1 · Кнопка Appeal у нарушителя | Репортёру: `report_outcome_action_taken` · Нарушителю: Statement of Reasons + Appeal |
| **Warn user** | Moderator+ | Предупреждение · Страйк +1 · Контент остаётся | Нарушителю: `moderation_warning_issued` |
| **Suspend (≤30d)** | Senior+ | Аккаунт заморожен · Нарушитель не может логиниться | Нарушителю: `account_suspended` + срок |
| **Permanent ban** | Admin+ | Аккаунт удалён навсегда | Нарушителю: `account_permanently_banned` |
| **Escalate CSAE** | Safety Officer+ | Тикет → CSAE очередь · Контент немедленно скрыт | Нарушителю — ничего до проверки |
| **Report to NCMEC** | Safety Officer+ | CyberTipline форма отправлена | Внутренний аудит-лог |

---

## 4. User Management

**URL:** `/admin/users`  
**Кто видит:** Admin, Safety Officer, DPO (только чтение), SuperAdmin

### 4.1 Поиск пользователя

```
Search: [_________________________] [Search by ID / email / username]

Filters: [Status ▾] [Registration date ▾] [Strikes ▾]
```

### 4.2 Карточка пользователя `/admin/users/{user_id}`

```
┌─────────────────────────────────────────────────────────────┐
│ User: @username (ID: 12345)                                  │
├─────────────────────────────────────────────────────────────┤
│ Email: user@email.com    | Joined: 12 Jan 2026              │
│ Status: Active           | Country: DE (IP)                 │
│ Age verified: No         | Login method: Google              │
├─────────────────────────────────────────────────────────────┤
│ MODERATION HISTORY                                          │
│ Strikes: 1               | Suspensions: 0                   │
│ Reports received: 3      | Reports filed: 12                │
│ Trust Score: ⭐⭐ (medio) | Abuse flag: No                  │
├─────────────────────────────────────────────────────────────┤
│ GDPR / DATA                                                 │
│ Consent given: ✅ 12 Jan 2026                               │
│ Marketing opt-in: ❌     | Data export requested: No        │
│ Account deletion: Not requested                             │
├─────────────────────────────────────────────────────────────┤
│ ACTIONS (Admin only)                                        │
│ [⚠️ Warn]  [⏸ Suspend]  [🚫 Ban]  [🔓 Restore]            │
│ [✂️ Remove strike]  [📦 Export user data]  [🗑 Delete data] │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. Appeals Queue

**URL:** `/admin/appeals`  
**Кто видит:** Senior Moderator, Admin, SuperAdmin

> ⚖️ **DSA Art.20:** Апелляцию рассматривает **другой** модератор, не тот кто принял первоначальное решение.

### 5.1 Структура

```
Appeals Queue

Filters: [Pending ▾] [Date ▾]

┌─────────────────────────────────────────────────────────────┐
│ Appeal #A-201                          Submitted: 2 hrs ago  │
│ For: Ticket #1038 (Remove content — Harassment)             │
│ User: @offender_username               Deadline: 3 days 22h │
│ [Review Appeal →]                                           │
└─────────────────────────────────────────────────────────────┘
```

### 5.2 Карточка апелляции `/admin/appeals/{appeal_id}`

```
APPEAL #A-201

Original decision: Remove content
Original moderator: @mod_user (NOT visible to appellant)
Original reason: "Harassment — targeted personal attack"

Appellant's statement:
"This was a joke between friends, not harassment."

Original content: [View — requires confirmation click]

──────────────────────────────────────────────
DECISION (must be a DIFFERENT moderator)

[✅ Grant appeal — restore content + remove strike]
[❌ Deny appeal — uphold removal]

Reasoning (обязательное поле, DSA Art.20):
[____________________________________________]

[Submit decision]
```

---

## 6. CSAE Queue

**URL:** `/admin/csae`  
**Кто видит:** Safety Officer, Admin, SuperAdmin (двухфакторная аутентификация обязательна)

> 🔴 **Протокол:** Весь контент в этой очереди автоматически скрыт. Обработка ≤1 час с момента поступления.

```
🔴 CSAE QUEUE — PRIORITY: CRITICAL

┌─────────────────────────────────────────────────────────────┐
│ #CSAE-044              Received: 14 min ago   ⏱️ 0:46 left  │
│ Content type: Image    User: @suspect_user                   │
│ Auto-hidden: ✅        NCMEC reported: ❌                    │
│ [Review →]                                                   │
└─────────────────────────────────────────────────────────────┘
```

### Действия в CSAE тикете

| Шаг | Действие | Обязателен |
|---|---|---|
| 1 | Просмотр контента (требует PIN-подтверждения) | ✅ |
| 2 | Подтвердить: CSAE / Not CSAE | ✅ |
| 3 | Если CSAE: Permanent ban пользователя | ✅ |
| 4 | Отправить репорт в NCMEC CyberTipline | ✅ по закону США ≤24 ч |
| 5 | Сохранить контент + метаданные для правоохранителей | ✅ |
| 6 | Закрыть тикет с пометкой CSAE_CONFIRMED или NOT_CSAE | ✅ |

---

## 7. Statistics Dashboard

**URL:** `/admin/statistics`  
**Кто видит:** Admin, SuperAdmin

```
┌────────────────┬────────────────┬────────────────┬────────────────┐
│  Total reports │  Resolved      │  Avg resolution│  Appeal rate   │
│  this month    │  today         │  time          │                │
│    1 284        │    47           │    3.2 h        │    8.4%         │
└────────────────┴────────────────┴────────────────┴────────────────┘

Reports by category (last 30 days):
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  Spam           (42%)
▓▓▓▓▓▓▓▓            Harassment     (21%)
▓▓▓▓▓               Hate Speech    (14%)
▓▓▓                 Misinformation (9%)
▓▓                  Child Safety   (6%)
▓▓                  Other          (8%)

Resolution outcomes:
✅ Action taken:  54%
❌ No violation:  46%

Appeal outcomes:
✅ Granted: 23%  ❌ Denied: 77%

Active users: 12,450 | New today: 134 | Banned this month: 7
```

---

## 8. Audit Log

**URL:** `/admin/audit`  
**Кто видит:** Senior Moderator, Admin, DPO, SuperAdmin  
**Хранение:** 3 года (GDPR Art.5(1)(e) · DSA)

### 8.1 Каждая запись содержит

| Поле | Пример |
|---|---|
| Timestamp | 2026-05-12 14:32:05 UTC |
| Actor (модератор) | @mod_alice (ID: 501) |
| Action | REMOVE_CONTENT |
| Target user | @offender (ID: 4521) |
| Target content | post_id: p_88712 |
| Ticket ID | #1042 |
| IP адрес модератора | 192.168.x.x |
| Reason | "Child Safety — CSAM confirmed" |

### 8.2 Фильтры

```
Filters: [Moderator ▾] [Action type ▾] [Date range ▾] [User ID]

[Export CSV]  [Export JSON]
```

---

## 9. Settings

**URL:** `/admin/settings`  
**Кто видит:** Admin, SuperAdmin

### 9.1 Настройки модерации

| Параметр | Значение по умолчанию | Описание |
|---|---|---|
| `strike_limit_warn` | 1 | Страйков до предупреждения |
| `strike_limit_suspend` | 2 | Страйков до временной блокировки |
| `strike_limit_ban` | 3 | Страйков до постоянного бана |
| `suspend_default_days` | 7 | Дней блокировки по умолчанию |
| `csae_auto_hide` | true | Автоматически скрыть контент при CSAE репорте |
| `csae_sla_hours` | 1 | Максимальное время ответа на CSAE (часы) |
| `standard_sla_days` | 5 | Максимальное время ответа на обычный тикет (рабочих дней) |
| `appeal_sla_days` | 5 | Максимальное время рассмотрения апелляции |
| `trust_score_spam_threshold` | 10 | Жалоб за 24 ч — автофлаг «possible abuse» |
| `trust_score_no_violation_threshold` | 0.8 | Доля закрытых без нарушений — снижение Trust Score |

### 9.2 Управление ролями (SuperAdmin only)

```
/admin/settings/roles

[+ Add moderator]

┌─────────────────────────────────────────────────────────────┐
│ @mod_alice    Role: Moderator        Last active: 2 hrs ago  │
│                                 [Edit role ▾]  [Revoke]     │
└─────────────────────────────────────────────────────────────┘
```

---

## 10. Технические требования

### 10.1 Аутентификация

| Требование | Обязательность |
|---|---|
| 2FA обязательна для всех ролей | ⚖️ GDPR Art.32 |
| CSAE очередь — дополнительный PIN при каждом открытии | ⚖️ Лучшая практика |
| Сессия истекает через 30 минут бездействия | ⚖️ GDPR Art.32 |
| Все действия логируются даже при ошибке | ⚖️ DSA Art.15 |

### 10.2 Защита данных

| Требование | Обязательность |
|---|---|
| HTTPS/TLS 1.3 для всех запросов | ⚖️ GDPR Art.5(1)(f) |
| IP-белый список для доступа к Admin Panel (VPN или офисная сеть) | 💡 Лучшая практика |
| Reporter ID никогда не передаётся нарушителю через API | ⚖️ DSA Art.16 (анонимность) |
| Контент из CSAE очереди хранится изолированно | ⚖️ CVAA |

### 10.3 API endpoints (внутренние)

| Endpoint | Метод | Роль |
|---|---|---|
| `/api/admin/tickets` | GET | Moderator+ |
| `/api/admin/tickets/{id}` | GET | Moderator+ |
| `/api/admin/tickets/{id}/dismiss` | POST | Moderator+ |
| `/api/admin/tickets/{id}/remove-content` | POST | Moderator+ |
| `/api/admin/tickets/{id}/warn` | POST | Moderator+ |
| `/api/admin/tickets/{id}/suspend` | POST | Senior+ |
| `/api/admin/tickets/{id}/ban` | POST | Admin+ |
| `/api/admin/appeals` | GET | Senior+ |
| `/api/admin/appeals/{id}/decide` | POST | Senior+ |
| `/api/admin/users/{id}` | GET | Admin+, DPO (GET only) |
| `/api/admin/users/{id}/strikes` | DELETE | Admin+ |
| `/api/admin/audit` | GET | Senior+, DPO |
| `/api/admin/ncmec-report` | POST | Safety Officer+ |

---

*AdminPanelSpec.md · BestMe · май 2026*
