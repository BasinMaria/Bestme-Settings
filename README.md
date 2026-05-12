# Bestme Settings — Карта репозитория

> **Репозиторий:** BasinMaria/Bestme-Settings  
> **Принцип:** каждый документ живёт **ровно в одном месте**. Везде остальное — только ссылка.

---

## 📁 Структура папок

```
Bestme-Settings/
├── 01_legal/          ← Юридические тексты (Terms, Privacy, Cookies)
├── 02_compliance/     ← Аудиты, анализы, чеклисты публикации
├── 03_settings/       ← ТЗ всех 9 разделов настроек приложения
├── 04_moderation/     ← UGC модерация: экраны для пользователей + инструкция модератора
├── 05_admin_panel/    ← Интерфейс бэкофиса: роли, экраны, API
├── 06_database/       ← Схема БД: таблицы, индексы, политика хранения
├── 07_help_support/   ← Экраны Help & Support (только то, что видит пользователь)
└── diagrams/          ← draw.io схемы
```

---

## 01_legal — Юридические тексты

> Полные тексты документов. Нигде не дублируются — везде только ссылки сюда.

| Файл | Что внутри |
|---|---|
| [TermsOfService.md](01_legal/TermsOfService.md) | Terms of Service v1.0 — полный юридический текст |
| [PrivacyPolicy.md](01_legal/PrivacyPolicy.md) | Privacy Policy v1.0 — полный юридический текст (GDPR · CCPA · PIPEDA) |
| [CookiePolicy.md](01_legal/CookiePolicy.md) | Cookie Policy — типы cookie, экран Cookie Settings, Banner |

---

## 02_compliance — Аудиты и анализы

> Проверки соответствия законам, чеклисты блокеров публикации.

| Файл | Что внутри |
|---|---|
| [LegalComplianceSpec.md](02_compliance/LegalComplianceSpec.md) | 21 закон + 2 магазина, матрица 22×12, приоритеты |
| [MasterComplianceAnalysis.md](02_compliance/MasterComplianceAnalysis.md) | Итоговый анализ: готовность, 9 критических пробелов |
| [GDPRArt25Art17AuditSpec.md](02_compliance/GDPRArt25Art17AuditSpec.md) | Аудит GDPR Art.25 (Privacy by Default) + Art.17 (право на удаление) |
| [AppStoreAuditSpec.md](02_compliance/AppStoreAuditSpec.md) | Аудит Apple App Store Review Guidelines (02.2026) |
| [ComplianceClarifications.md](02_compliance/ComplianceClarifications.md) | Ответы на вопросы: возраст 18+ vs COPPA, субтитры, 13 критичных пунктов |
| [PublicationPriorityPlan.md](02_compliance/PublicationPriorityPlan.md) | Что блокирует публикацию, 2-sprint план, статус 6 потоков |

---

## 03_settings — ТЗ настроек приложения

> Технические задания для дизайнеров и разработчиков по всем 9 разделам Settings.

| Файл | Что внутри |
|---|---|
| [SettingsOverview.md](03_settings/SettingsOverview.md) | **КАРТА:** обзор всех 9 разделов, структура L1 |
| [ProfileSettingsFullSpec.md](03_settings/ProfileSettingsFullSpec.md) | **ГЛАВНЫЙ:** полная спецификация v2.0, 6 обязательных потоков, 40+ законов |
| [SettingsTZ.md](03_settings/SettingsTZ.md) | ТЗ: таблицы 🔴/🟡/🟢, L1→L2→L3, variable names |
| [SettingsMapping.md](03_settings/SettingsMapping.md) | Маппинг дизайнерских экранов к L1/L2/L3 |
| [AccountSpec.md](03_settings/AccountSpec.md) | Раздел 1️⃣ Account: редактирование профиля |
| [AccountDeletionSpec.md](03_settings/AccountDeletionSpec.md) | Удаление аккаунта: 4 сценария, 15 экранов, де-индексация, App Store чеклист |
| [AccountPrivacySpec.md](03_settings/AccountPrivacySpec.md) | Юридический анализ блока Account Privacy, defaults по возрасту |
| [PrivacyVisibilitySpec.md](03_settings/PrivacyVisibilitySpec.md) | Раздел 2️⃣ Privacy & Visibility: полная спецификация |
| [PrivacyFieldsSpec.md](03_settings/PrivacyFieldsSpec.md) | 35 privacy-полей: defaults, матрица видимости, правовые основания |
| [GDPRArt5SecuritySpec.md](03_settings/GDPRArt5SecuritySpec.md) | Раздел 3️⃣ Login & Security: 2FA, сессии, OAuth, GDPR Art.5 |
| [NotificationsSpec.md](03_settings/NotificationsSpec.md) | Раздел 4️⃣ Notifications: 76 уведомлений в 15 группах |
| [FriendsAndCommunitySpec.md](03_settings/FriendsAndCommunitySpec.md) | Раздел 5️⃣ Friends & Community |
| [AccessibilitySpec.md](03_settings/AccessibilitySpec.md) | Раздел 8️⃣ Accessibility: 8 настроек, WCAG, EAA, кнопка Contact DPO |
| [UserManualGuide.md](03_settings/UserManualGuide.md) | Нужно ли руководство пользователя: Help Center, Accessibility Statement |

---

## 04_moderation — Модерация UGC

> Всё про жалобы и модерацию: и что видит пользователь, и что делает модератор.

| Файл | Что внутри |
|---|---|
| [ReportAProblem.md](04_moderation/ReportAProblem.md) | Полная спецификация Report flow: 14 экранов, все категории, DM, AI-модерация |
| [ModerationAdminGuide.md](04_moderation/ModerationAdminGuide.md) | Инструкция модератора: жизненный цикл тикета, страйки, CSAE протокол |
| [ChildSafety.md](04_moderation/ChildSafety.md) | Экран Child Safety в приложении, NCMEC, требования Google Play |

---

## 05_admin_panel — Интерфейс бэкофиса

> Спецификация веб-панели для команды модерации.

| Файл | Что внутри |
|---|---|
| [AdminPanelSpec.md](05_admin_panel/AdminPanelSpec.md) | Роли (Moderator/Senior/Admin/Safety Officer/DPO), экраны Dashboard/Tickets/Appeals/CSAE/Statistics/Audit Log, матрица прав, API endpoints |

---

## 06_database — Схема базы данных

> SQL-схемы всех таблиц с комментариями, индексы, политика хранения данных.

| Файл | Что внутри |
|---|---|
| [DatabaseSchema.md](06_database/DatabaseSchema.md) | Таблицы: `users`, `user_profiles`, `user_sessions`, `consent_history`, `reports`, `moderation_tickets`, `moderation_log`, `strikes`, `appeals`, `blocked_users`, `notifications_log`, `data_deletion_requests` |

---

## 07_help_support — Help & Support (пользовательские экраны)

> Только то, что видит пользователь в Settings → Help & Support.  
> Terms и Privacy не дублируются — ссылки на `01_legal/`.

| Файл | Что внутри |
|---|---|
| [HelpCenter_FAQ.md](07_help_support/HelpCenter_FAQ.md) | FAQ: частые вопросы и ответы |
| [ContactSupport.md](07_help_support/ContactSupport.md) | Контакты поддержки: email, сроки ответа |
| [OpenSourceLicenses.md](07_help_support/OpenSourceLicenses.md) | Лицензии open-source компонентов |
| [AppVersion.md](07_help_support/AppVersion.md) | Экран версии приложения |

---

## diagrams — Схемы draw.io

| Файл | Что внутри |
|---|---|
| [PersonalProfileSettings.drawio.html](diagrams/PersonalProfileSettings.drawio.html) | 260 ячеек, иерархия L1→L2→L3 настроек |
| [SettingsArchitecture.drawio.html](diagrams/SettingsArchitecture.drawio.html) | 242 ячейки, архитектура Privacy & Visibility |
| [ProfileSettings.drawio.html](diagrams/ProfileSettings.drawio.html) | Исходная архитектура настроек |

---

## Правило «один раз — одно место»

| Что | Где живёт | Везде остальное |
|---|---|---|
| Terms of Service (текст) | `01_legal/TermsOfService.md` | Ссылка |
| Privacy Policy (текст) | `01_legal/PrivacyPolicy.md` | Ссылка |
| Cookie Policy | `01_legal/CookiePolicy.md` | Ссылка |
| Все 76 ключей уведомлений | `03_settings/NotificationsSpec.md` | Ссылка |
| Report flow (пользователь) | `04_moderation/ReportAProblem.md` | Ссылка |
| Инструкция модератора | `04_moderation/ModerationAdminGuide.md` | Ссылка |
| DB схемы | `06_database/DatabaseSchema.md` | Ссылка |

---

*README.md · Bestme Settings · май 2026*
