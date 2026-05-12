# Database Schema — Схема базы данных BestMe

**Версия:** 1.0 · **Дата:** май 2026  
**Кому:** Бэкенд-разработчик, DevOps, DPO  
**База данных:** PostgreSQL 15+  
**Статус:** 🔴 Таблицы `users`, `reports`, `moderation_tickets` — блокеры публикации

> **Смежные документы:**  
> [../05_admin_panel/AdminPanelSpec.md](../05_admin_panel/AdminPanelSpec.md) — интерфейс бэкофиса  
> [../04_moderation/ModerationAdminGuide.md](../04_moderation/ModerationAdminGuide.md) — бизнес-процессы  
> [../01_legal/PrivacyPolicy.md](../01_legal/PrivacyPolicy.md) — правила хранения данных  
> [../02_compliance/GDPRArt25Art17AuditSpec.md](../02_compliance/GDPRArt25Art17AuditSpec.md) — GDPR требования к данным

---

## Содержание

1. [users — аккаунты пользователей](#1-users)
2. [user_profiles — данные профиля](#2-user_profiles)
3. [user_sessions — активные сессии](#3-user_sessions)
4. [consent_history — история согласий](#4-consent_history)
5. [reports — жалобы пользователей](#5-reports)
6. [moderation_tickets — тикеты модерации](#6-moderation_tickets)
7. [moderation_log — журнал действий модераторов](#7-moderation_log)
8. [strikes — система страйков](#8-strikes)
9. [appeals — апелляции](#9-appeals)
10. [blocked_users — блокировки между пользователями](#10-blocked_users)
11. [notifications_log — журнал уведомлений](#11-notifications_log)
12. [data_deletion_requests — запросы на удаление данных](#12-data_deletion_requests)
13. [Индексы](#13-индексы)
14. [Политика хранения данных (GDPR Art.5(1)(e))](#14-политика-хранения-данных)

---

## 1. users

Основная таблица аккаунтов. Содержит только данные, необходимые для аутентификации и идентификации.

```sql
CREATE TABLE users (
    id                  BIGSERIAL PRIMARY KEY,
    uuid                UUID NOT NULL UNIQUE DEFAULT gen_random_uuid(),
    email               VARCHAR(255) UNIQUE,           -- NULL если только phone/OAuth
    email_verified      BOOLEAN NOT NULL DEFAULT FALSE,
    phone               VARCHAR(20) UNIQUE,             -- NULL если только email/OAuth
    phone_verified      BOOLEAN NOT NULL DEFAULT FALSE,
    password_hash       VARCHAR(255),                   -- bcrypt, NULL для OAuth-only
    status              VARCHAR(20) NOT NULL DEFAULT 'active',
                        -- active | suspended | banned | deactivated | pending_deletion
    role                VARCHAR(20) NOT NULL DEFAULT 'user',
                        -- user | moderator | senior_moderator | admin | safety_officer | dpo | superadmin
    age_verified        BOOLEAN NOT NULL DEFAULT FALSE,
    birth_year          SMALLINT,                       -- только год, не полная дата (минимизация данных)
    country_code        VARCHAR(2),                     -- определяется при регистрации по IP (ISO 3166-1 alpha-2)
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    suspended_until     TIMESTAMPTZ,                    -- NULL если не на паузе
    deletion_requested_at TIMESTAMPTZ,                  -- NULL если не запрошено
    deletion_scheduled_at TIMESTAMPTZ,                  -- удалить через 30 дней после deactivation
    CONSTRAINT status_check CHECK (status IN ('active','suspended','banned','deactivated','pending_deletion')),
    CONSTRAINT role_check CHECK (role IN ('user','moderator','senior_moderator','admin','safety_officer','dpo','superadmin'))
);

COMMENT ON TABLE users IS 'Основные аккаунты. Минимальные данные — GDPR Art.5(1)(c) минимизация.';
COMMENT ON COLUMN users.birth_year IS 'Только год для проверки возраста ≥13 / ≥18. Не хранится полная дата рождения.';
COMMENT ON COLUMN users.deletion_scheduled_at IS 'GDPR Art.17: данные удаляются в этот момент. 30 дней grace period.';
```

---

## 2. user_profiles

Публичные и приватные данные профиля пользователя. Отдельная таблица — можно удалить независимо.

```sql
CREATE TABLE user_profiles (
    user_id             BIGINT PRIMARY KEY REFERENCES users(id) ON DELETE CASCADE,

    -- Отображаемые данные
    display_name        VARCHAR(100),
    username            VARCHAR(50) UNIQUE NOT NULL,
    bio                 TEXT,
    avatar_url          VARCHAR(500),
    website_url         VARCHAR(500),

    -- Настройки приватности (см. PrivacyVisibilitySpec.md)
    account_privacy     VARCHAR(10) NOT NULL DEFAULT 'public',
                        -- public | private
    show_online_status  BOOLEAN NOT NULL DEFAULT TRUE,
    show_last_seen      BOOLEAN NOT NULL DEFAULT TRUE,
    seo_indexable       BOOLEAN NOT NULL DEFAULT TRUE,  -- GDPR Art.17(2) де-индексация

    -- Локализация
    language_code       VARCHAR(10) NOT NULL DEFAULT 'en',
    timezone            VARCHAR(50),

    -- Маркетинг (всё OFF по умолчанию — CASL / ePrivacy)
    email_marketing_opt_in   BOOLEAN NOT NULL DEFAULT FALSE,
    push_marketing_opt_in    BOOLEAN NOT NULL DEFAULT FALSE,
    sms_marketing_opt_in     BOOLEAN NOT NULL DEFAULT FALSE,

    updated_at          TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

COMMENT ON TABLE user_profiles IS 'Данные профиля. Отдельная таблица для удобства GDPR Art.17 удаления.';
COMMENT ON COLUMN user_profiles.seo_indexable IS 'FALSE = запрос де-индексации в Google/Bing при удалении аккаунта (GDPR Art.17(2))';
COMMENT ON COLUMN user_profiles.email_marketing_opt_in IS 'CASL / ePrivacy: обязательно FALSE по умолчанию, явный opt-in.';
```

---

## 3. user_sessions

Активные сессии. Хранятся для управления через Settings → Login & Security → Active Sessions.

```sql
CREATE TABLE user_sessions (
    id                  BIGSERIAL PRIMARY KEY,
    user_id             BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    session_token_hash  VARCHAR(255) NOT NULL UNIQUE,  -- хэш токена, не сам токен
    device_name         VARCHAR(100),                   -- "iPhone 15 Pro", "Chrome on Windows"
    device_type         VARCHAR(20),                    -- ios | android | web
    ip_address          INET,
    country_code        VARCHAR(2),
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    last_active_at      TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    expires_at          TIMESTAMPTZ NOT NULL,
    revoked_at          TIMESTAMPTZ,                    -- NULL = активна
    revoked_by          VARCHAR(20)                     -- user | admin | system
);

COMMENT ON TABLE user_sessions IS 'GDPR Art.5(1)(f): управление сессиями для безопасности. Хранится хэш токена, не сам токен.';
```

---

## 4. consent_history

История всех согласий пользователя. Обязательно для GDPR Art.7 (доказательство согласия).

```sql
CREATE TABLE consent_history (
    id                  BIGSERIAL PRIMARY KEY,
    user_id             BIGINT NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    consent_type        VARCHAR(50) NOT NULL,
                        -- terms_of_service | privacy_policy | marketing_email |
                        --   marketing_push | marketing_sms | analytics | advertising |
                        --   att_ios | age_verification | ugc_terms
    action              VARCHAR(10) NOT NULL,   -- granted | revoked
    version             VARCHAR(20),            -- версия документа, напр. "1.0"
    ip_address          INET,
    user_agent          TEXT,
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    CONSTRAINT consent_type_check CHECK (consent_type IN (
        'terms_of_service','privacy_policy','marketing_email',
        'marketing_push','marketing_sms','analytics','advertising',
        'att_ios','age_verification','ugc_terms'
    )),
    CONSTRAINT action_check CHECK (action IN ('granted','revoked'))
);

COMMENT ON TABLE consent_history IS 'GDPR Art.7: неизменяемый журнал согласий. Хранится 5 лет.';
COMMENT ON COLUMN consent_history.user_id IS 'SET NULL при удалении пользователя — запись остаётся для аудита без привязки к личности.';
```

---

## 5. reports

Жалобы, поданные пользователями. Основа системы модерации.

```sql
CREATE TABLE reports (
    id                  BIGSERIAL PRIMARY KEY,
    reporter_id         BIGINT REFERENCES users(id) ON DELETE SET NULL,
                        -- SET NULL: анонимность после удаления, тикет остаётся
    reported_user_id    BIGINT REFERENCES users(id) ON DELETE SET NULL,
    content_type        VARCHAR(20),            -- post | comment | profile | dm | conversation
    content_id          BIGINT,                 -- ID поста, комментария, DM и т.д.
    category            VARCHAR(30) NOT NULL,
                        -- spam | harassment | hate_speech | child_safety |
                        --   misinformation | nudity | violence | illegal | other
    subcategory         VARCHAR(50),
    reporter_note       TEXT,                   -- необязательный текст от репортёра
    screenshot_url      VARCHAR(500),           -- если приложен скриншот
    status              VARCHAR(20) NOT NULL DEFAULT 'pending',
                        -- pending | in_review | resolved_action | resolved_no_violation | escalated_csae
    trust_score_at_report SMALLINT,             -- Trust Score репортёра на момент подачи
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    CONSTRAINT category_check CHECK (category IN (
        'spam','harassment','hate_speech','child_safety',
        'misinformation','nudity','violence','illegal','other'
    )),
    CONSTRAINT status_check CHECK (status IN (
        'pending','in_review','resolved_action','resolved_no_violation','escalated_csae'
    ))
);

COMMENT ON TABLE reports IS 'DSA Art.14/16: жалобы пользователей. reporter_id скрыт от нарушителя.';
COMMENT ON COLUMN reports.reporter_id IS 'НИКОГДА не передавать нарушителю — DSA Art.16 анонимность репортёра.';
```

---

## 6. moderation_tickets

Тикеты модерации — основная рабочая единица для модераторов.

```sql
CREATE TABLE moderation_tickets (
    id                  BIGSERIAL PRIMARY KEY,
    report_id           BIGINT UNIQUE REFERENCES reports(id) ON DELETE CASCADE,
    assigned_to         BIGINT REFERENCES users(id) ON DELETE SET NULL,  -- модератор
    priority            VARCHAR(10) NOT NULL DEFAULT 'standard',
                        -- critical (CSAE) | high (illegal) | standard
    status              VARCHAR(20) NOT NULL DEFAULT 'open',
                        -- open | in_review | closed | appeal_open | appeal_closed
    decision            VARCHAR(30),
                        -- no_violation | content_removed | user_warned |
                        --   user_suspended | user_banned | escalated_csae
    decision_reason     TEXT,                   -- внутреннее обоснование (не для пользователя)
    statement_of_reasons TEXT,                  -- DSA Art.17: текст для нарушителя
    moderator_note      TEXT,                   -- внутренняя заметка
    resolved_at         TIMESTAMPTZ,
    sla_deadline        TIMESTAMPTZ NOT NULL,   -- рассчитывается: CSAE = +1h, standard = +5 рабочих дней
    ncmec_reported      BOOLEAN NOT NULL DEFAULT FALSE,
    ncmec_report_id     VARCHAR(100),           -- ID репорта в CyberTipline
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    CONSTRAINT priority_check CHECK (priority IN ('critical','high','standard')),
    CONSTRAINT status_check CHECK (status IN ('open','in_review','closed','appeal_open','appeal_closed')),
    CONSTRAINT decision_check CHECK (decision IS NULL OR decision IN (
        'no_violation','content_removed','user_warned',
        'user_suspended','user_banned','escalated_csae'
    ))
);

COMMENT ON TABLE moderation_tickets IS 'DSA Art.14: основная единица модерации. sla_deadline контролирует соблюдение сроков.';
COMMENT ON COLUMN moderation_tickets.statement_of_reasons IS 'DSA Art.17: обязательный текст объяснения, отправляется нарушителю.';
```

---

## 7. moderation_log

Неизменяемый журнал всех действий модераторов. Используется DPO и для аудитов DSA.

```sql
CREATE TABLE moderation_log (
    id                  BIGSERIAL PRIMARY KEY,
    ticket_id           BIGINT REFERENCES moderation_tickets(id) ON DELETE SET NULL,
    actor_id            BIGINT REFERENCES users(id) ON DELETE SET NULL,  -- модератор
    actor_role          VARCHAR(20) NOT NULL,
    action              VARCHAR(50) NOT NULL,
                        -- ticket_opened | content_viewed | content_removed | user_warned |
                        --   user_suspended | user_banned | ticket_dismissed |
                        --   appeal_granted | appeal_denied | ncmec_report_sent |
                        --   strike_added | strike_removed | note_added
    target_user_id      BIGINT,                 -- пользователь, которого касается действие
    target_content_id   BIGINT,
    target_content_type VARCHAR(20),
    details             JSONB,                  -- дополнительные данные (срок бана, текст заметки и т.д.)
    ip_address          INET,
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

COMMENT ON TABLE moderation_log IS 'DSA Art.15 · GDPR Art.5(2): неизменяемый аудит-лог. Хранить 3 года минимум. INSERT ONLY.';
```

---

## 8. strikes

Страйки пользователей. Накапливаются, не сбрасываются автоматически.

```sql
CREATE TABLE strikes (
    id                  BIGSERIAL PRIMARY KEY,
    user_id             BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    ticket_id           BIGINT REFERENCES moderation_tickets(id) ON DELETE SET NULL,
    issued_by           BIGINT REFERENCES users(id) ON DELETE SET NULL,  -- модератор
    reason              TEXT NOT NULL,
    active              BOOLEAN NOT NULL DEFAULT TRUE,  -- FALSE = снят после апелляции
    issued_at           TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    removed_at          TIMESTAMPTZ,
    removed_by          BIGINT REFERENCES users(id) ON DELETE SET NULL
);

COMMENT ON TABLE strikes IS 'Система страйков: 1=warn, 2=suspend, 3=ban. Снять может только Admin+.';
COMMENT ON COLUMN strikes.active IS 'FALSE если страйк снят после успешной апелляции или Admin решения.';
```

---

## 9. appeals

Апелляции пользователей против решений модерации.

```sql
CREATE TABLE appeals (
    id                  BIGSERIAL PRIMARY KEY,
    ticket_id           BIGINT NOT NULL REFERENCES moderation_tickets(id) ON DELETE CASCADE,
    appellant_id        BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    statement           TEXT NOT NULL,          -- текст апелляции от пользователя
    status              VARCHAR(20) NOT NULL DEFAULT 'pending',
                        -- pending | in_review | granted | denied
    reviewed_by         BIGINT REFERENCES users(id) ON DELETE SET NULL,
                        -- ДОЛЖЕН отличаться от moderator который принял исходное решение
    decision_reason     TEXT,                   -- DSA Art.20: обязательное обоснование
    submitted_at        TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    deadline_at         TIMESTAMPTZ NOT NULL,   -- submitted_at + 5 рабочих дней
    resolved_at         TIMESTAMPTZ,
    CONSTRAINT status_check CHECK (status IN ('pending','in_review','granted','denied'))
);

COMMENT ON TABLE appeals IS 'DSA Art.20: право на апелляцию. reviewed_by ≠ исходный модератор — проверяется на уровне приложения.';
COMMENT ON COLUMN appeals.decision_reason IS 'DSA Art.20: обязательное поле. Не может быть NULL при resolved_at IS NOT NULL.';
```

---

## 10. blocked_users

Блокировки между пользователями (пользовательское действие, не модерация).

```sql
CREATE TABLE blocked_users (
    id                  BIGSERIAL PRIMARY KEY,
    blocker_id          BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    blocked_id          BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    created_at          TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    CONSTRAINT unique_block UNIQUE (blocker_id, blocked_id),
    CONSTRAINT no_self_block CHECK (blocker_id != blocked_id)
);

COMMENT ON TABLE blocked_users IS 'Пользовательская блокировка. blocked_id никогда не должен знать, что его заблокировали.';
```

---

## 11. notifications_log

Журнал отправленных уведомлений (push, email, in-app). Используется для дедупликации и GDPR доказательств.

```sql
CREATE TABLE notifications_log (
    id                  BIGSERIAL PRIMARY KEY,
    user_id             BIGINT NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    notification_key    VARCHAR(100) NOT NULL,  -- см. NotificationsSpec.md для полного списка ключей
    channel             VARCHAR(10) NOT NULL,   -- push | email | in_app | sms
    status              VARCHAR(15) NOT NULL DEFAULT 'sent',
                        -- sent | delivered | failed | bounced | unsubscribed
    payload             JSONB,                  -- параметры уведомления (без PII)
    related_entity_type VARCHAR(20),            -- ticket | appeal | report | post | user
    related_entity_id   BIGINT,
    sent_at             TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    delivered_at        TIMESTAMPTZ,
    CONSTRAINT channel_check CHECK (channel IN ('push','email','in_app','sms')),
    CONSTRAINT status_check CHECK (status IN ('sent','delivered','failed','bounced','unsubscribed'))
);

COMMENT ON TABLE notifications_log IS 'GDPR Art.7 / CASL: доказательство отправки согласия и уведомлений. payload не должен содержать PII.';
COMMENT ON COLUMN notifications_log.notification_key IS 'Полный список ключей — NotificationsSpec.md. Примеры: report_outcome_action_taken, account_suspended.';
```

---

## 12. data_deletion_requests

GDPR Art.17 / CCPA — запросы на удаление данных.

```sql
CREATE TABLE data_deletion_requests (
    id                  BIGSERIAL PRIMARY KEY,
    user_id             BIGINT REFERENCES users(id) ON DELETE SET NULL,
    request_channel     VARCHAR(20) NOT NULL,   -- in_app | web_form | email | support_ticket
    status              VARCHAR(20) NOT NULL DEFAULT 'pending',
                        -- pending | processing | completed | rejected_legal_hold
    requester_email     VARCHAR(255),           -- если через web-форму без аккаунта
    identity_verified   BOOLEAN NOT NULL DEFAULT FALSE,
    verification_method VARCHAR(30),            -- email_link | phone_otp | manual_review
    deindex_requested   BOOLEAN NOT NULL DEFAULT FALSE,  -- GDPR Art.17(2) де-индексация
    deindex_completed   BOOLEAN NOT NULL DEFAULT FALSE,
    deletion_scope      VARCHAR(20) NOT NULL DEFAULT 'full',
                        -- full | partial (только контент, аккаунт остаётся)
    requested_at        TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    processing_started_at TIMESTAMPTZ,
    completed_at        TIMESTAMPTZ,
    rejected_reason     TEXT,
    CONSTRAINT status_check CHECK (status IN ('pending','processing','completed','rejected_legal_hold')),
    CONSTRAINT scope_check CHECK (deletion_scope IN ('full','partial'))
);

COMMENT ON TABLE data_deletion_requests IS 'GDPR Art.17 / CCPA §1798.105: запросы на удаление. Выполнить в течение 30 дней.';
COMMENT ON COLUMN data_deletion_requests.deindex_requested IS 'TRUE = отправить запрос на де-индексацию в Google Search Console и Bing при удалении.';
```

---

## 13. Индексы

```sql
-- users — часто ищем по email, phone, uuid, status
CREATE INDEX idx_users_email ON users(email) WHERE email IS NOT NULL;
CREATE INDEX idx_users_phone ON users(phone) WHERE phone IS NOT NULL;
CREATE INDEX idx_users_uuid ON users(uuid);
CREATE INDEX idx_users_status ON users(status);
CREATE INDEX idx_users_deletion_scheduled ON users(deletion_scheduled_at) WHERE deletion_scheduled_at IS NOT NULL;

-- user_sessions — ищем по user_id и токену
CREATE INDEX idx_sessions_user_id ON user_sessions(user_id);
CREATE INDEX idx_sessions_expires ON user_sessions(expires_at) WHERE revoked_at IS NULL;

-- consent_history — ищем по user_id и типу
CREATE INDEX idx_consent_user_id ON consent_history(user_id);
CREATE INDEX idx_consent_type ON consent_history(consent_type, action);

-- reports — очередь модерации
CREATE INDEX idx_reports_status ON reports(status);
CREATE INDEX idx_reports_category ON reports(category);
CREATE INDEX idx_reports_reported_user ON reports(reported_user_id);
CREATE INDEX idx_reports_created_at ON reports(created_at DESC);

-- moderation_tickets — приоритизация и SLA
CREATE INDEX idx_tickets_status ON moderation_tickets(status);
CREATE INDEX idx_tickets_priority ON moderation_tickets(priority);
CREATE INDEX idx_tickets_sla ON moderation_tickets(sla_deadline) WHERE status IN ('open','in_review');
CREATE INDEX idx_tickets_assigned ON moderation_tickets(assigned_to) WHERE assigned_to IS NOT NULL;

-- moderation_log — аудит
CREATE INDEX idx_moderation_log_actor ON moderation_log(actor_id);
CREATE INDEX idx_moderation_log_ticket ON moderation_log(ticket_id);
CREATE INDEX idx_moderation_log_target_user ON moderation_log(target_user_id);
CREATE INDEX idx_moderation_log_created_at ON moderation_log(created_at DESC);

-- strikes
CREATE INDEX idx_strikes_user_id ON strikes(user_id) WHERE active = TRUE;

-- appeals
CREATE INDEX idx_appeals_ticket ON appeals(ticket_id);
CREATE INDEX idx_appeals_status ON appeals(status);
CREATE INDEX idx_appeals_deadline ON appeals(deadline_at) WHERE status IN ('pending','in_review');

-- blocked_users — проверка блокировки в реальном времени
CREATE INDEX idx_blocked_blocker ON blocked_users(blocker_id);
CREATE INDEX idx_blocked_blocked ON blocked_users(blocked_id);

-- notifications_log
CREATE INDEX idx_notifications_user ON notifications_log(user_id);
CREATE INDEX idx_notifications_key ON notifications_log(notification_key);
CREATE INDEX idx_notifications_sent_at ON notifications_log(sent_at DESC);

-- data_deletion_requests
CREATE INDEX idx_deletion_requests_user ON data_deletion_requests(user_id);
CREATE INDEX idx_deletion_requests_status ON data_deletion_requests(status) WHERE status IN ('pending','processing');
```

---

## 14. Политика хранения данных

> ⚖️ **GDPR Art.5(1)(e):** данные хранятся не дольше, чем необходимо для цели обработки.

| Таблица / данные | Срок хранения | Основание | Автоматическое удаление |
|---|---|---|---|
| `users` (активный) | Пока активен аккаунт | GDPR Art.5(1)(e) | ❌ |
| `users` (deactivated) | 30 дней → полное удаление | GDPR Art.17 · App Store §5.1.1 | ✅ cronjob |
| `user_profiles` | Вместе с users | — | ✅ CASCADE |
| `user_sessions` | 90 дней после истечения / отзыва | GDPR Art.5(1)(e) | ✅ cronjob |
| `consent_history` | 5 лет | GDPR Art.7 (доказательство согласия) | ❌ вручную |
| `reports` | 3 года с даты закрытия | GDPR Art.5 · DSA | ✅ cronjob |
| `moderation_tickets` | 3 года с даты закрытия | DSA Art.24 (прозрачность) | ✅ cronjob |
| `moderation_log` | 3 года | DSA Art.15 · GDPR Art.5(2) подотчётность | ❌ вручную (аудит) |
| Удалённый контент (копия) | 6 месяцев | DSA Art.17 (для апелляций) | ✅ cronjob |
| CSAE контент | До закрытия дела / запроса NCMEC | CVAA · PROTECT Our Children Act | ❌ только Safety Officer |
| `strikes` | Бессрочно | Защита платформы | ❌ |
| `blocked_users` | До разблокировки | Пользовательское действие | ❌ |
| `notifications_log` | 1 год | CASL / ePrivacy (доказательство) | ✅ cronjob |
| `data_deletion_requests` | 5 лет | GDPR Art.12(5) (журнал запросов) | ❌ |

### Cronjob задачи

```
# Каждую ночь в 02:00 UTC
0 2 * * * delete_expired_sessions          -- user_sessions старше 90 дней после revoked/expired
0 2 * * * process_pending_deletions        -- users с deletion_scheduled_at < NOW()
0 2 * * * archive_old_reports              -- reports/tickets старше 3 лет
0 2 * * * cleanup_notifications_log       -- notifications_log старше 1 года
0 2 * * * delete_removed_content_copies   -- удалённый контент старше 6 месяцев (не CSAE)
```

---

*DatabaseSchema.md · BestMe · май 2026*
