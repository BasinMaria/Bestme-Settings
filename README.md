# Bestme Settings — Индекс всех файлов репозитория

> **Репозиторий:** BasinMaria/Bestme-Settings  
> **Последнее обновление:** март 2026  
> **Что здесь:** полная спецификация настроек личного профиля Bestme с юридическим анализом по 21 закону и 2 магазинам (App Store + Google Play).

---

## 🗂 ЧТО ЗДЕСЬ ЕСТЬ — ПОЛНЫЙ СПИСОК ФАЙЛОВ

| Файл | Что внутри | Объём |
|---|---|---|
| **[ProfileSettingsFullSpec.md](ProfileSettingsFullSpec.md)** ← **ГЛАВНЫЙ** | Полная структура настроек профиля v2.0. 9 разделов L1→L2→L3, 6 обязательных потоков, таблица законов × настройки, чеклист публикации (34 пункта) | 843 строки |
| [SettingsTZ.md](SettingsTZ.md) | ТЗ настроек: таблицы 🔴/🟡/🟢, секции 1–9 с variable_names, defaults, законами. ASCII-дерево структуры | 631 строка |
| [MasterComplianceAnalysis.md](MasterComplianceAnalysis.md) | Итоговый анализ: что работает (78%), 9 критических пробелов, что нужно добавить | 529 строк |
| [LegalComplianceSpec.md](LegalComplianceSpec.md) | Юридическая спецификация: 21 закон + 2 магазина, матрица 22×12, чеклист | 539 строк |
| [PrivacyFieldsSpec.md](PrivacyFieldsSpec.md) | 35 privacy-полей: variable names, defaults, матрица видимости (Owner/Friends/Everyone/Unauth/Blocked), правовые основания | 757 строк |
| [NotificationsSpec.md](NotificationsSpec.md) | 76 ключей уведомлений в 15 группах, 29 обязательных по закону (нельзя выключить), Title/Subtitle (EN) | 240 строк |
| [AccountPrivacySpec.md](AccountPrivacySpec.md) | Юридический анализ блока Account Privacy: defaults по возрасту, законность открытого профиля 18+ | 245 строк |
| [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md) | Аудит GDPR Art.25 + Art.17 пункт за пунктом, 2 критических пробела (де-индексация + onboarding) | 301 строка |
| [AppStoreAuditSpec.md](AppStoreAuditSpec.md) | Аудит Apple App Store Review Guidelines (02.2026) пункт за пунктом | 315 строк |
| [SettingsMapping.md](SettingsMapping.md) | Маппинг дизайнерских экранов к уровням L1/L2/L3, связи между разделами | 441 строка |
| [PersonalProfileSettings.drawio.html](PersonalProfileSettings.drawio.html) | Draw.io диаграмма: 260 ячеек, 9 L1, иерархия L1→L2→L3 только для личного профиля | HTML-диаграмма |
| [SettingsArchitecture.drawio.html](SettingsArchitecture.drawio.html) | Draw.io диаграмма: 242 ячейки, 4 дизайнерских экрана Privacy & Visibility | HTML-диаграмма |
| [ProfileSettings.drawio.html](ProfileSettings.drawio.html) | Draw.io диаграмма: исходная архитектура настроек | HTML-диаграмма |

---

## 📄 ЧТО НАХОДИТСЯ В ГЛАВНОМ ФАЙЛЕ — ProfileSettingsFullSpec.md

> Это итоговый документ с **полной структурой всех настроек профиля**, собранной на основе всех остальных файлов.

### Структура файла

```
ProfileSettingsFullSpec.md
│
├── GDPR Art.5 — 7 принципов обработки данных (фундамент)
│
├── ПЕРВЫЙ ЭКРАН — 9 пунктов главного меню Settings
│
├── ОБЯЗАТЕЛЬНЫЕ ПОТОКИ (6 NEW-потоков)
│   ├── Поток 1: Onboarding Disclosure — регистрация 18+ (GDPR Art.25)
│   ├── Поток 2: UGC Terms Acceptance — первый контент (App Store §1.2)
│   ├── Поток 3: Prominent Disclosure — перед Push/Camera (Google Play)
│   ├── Поток 4: ATT диалог iOS (App Store §5.1.2)
│   ├── Поток 5: TCPA SMS Consent — при добавлении телефона
│   └── Поток 6: Delete Account Modal — с де-индексацией (GDPR Art.17)
│
├── 1. 👤 ACCOUNT — профиль + управление аккаунтом
├── 2. 🔒 PRIVACY & VISIBILITY — 6 подразделов
│   ├── 2.1 Account Privacy (приватный/открытый аккаунт)
│   ├── 2.2 Contact Info Privacy (email, телефон, город)
│   ├── 2.3 Content Visibility (посты, фото, активность)
│   ├── 2.4 Interactions (сообщения, комментарии, теги)
│   ├── 2.5 Discoverability (поиск, SEO, рекомендации)
│   └── 2.6 Blocked Accounts
├── 3. 🛡️ LOGIN & SECURITY — 2FA, сессии, 3rd-party login
├── 4. 🔔 NOTIFICATIONS — 6 групп + каналы доставки
├── 5. 👥 FRIENDS — запросы, синхронизация контактов
├── 6. 📝 CONTENT & MODERATION — настройки + категории жалоб
├── 7. 📦 YOUR DATA — 9 прав GDPR + CCPA + хранение
├── 8. ♿ ACCESSIBILITY — 8 настроек + WCAG-матрица
├── 9. ❓ HELP & SUPPORT — Child Safety + поддержка
│
├── СВОДНАЯ ТАБЛИЦА: 40+ законов × настройки
├── ЧЕКЛИСТ ПУБЛИКАЦИИ: 20 блокеров + 9 важных + 5 рекомендаций
└── ТЕХНИЧЕСКИЙ СЛОВАРЬ: все variable_names + defaults
```

---

## ✅ ЧТО БЫЛО СДЕЛАНО В ЭТОМ PR

### ProfileSettingsFullSpec.md — полная перезапись до v2.0

**Добавлено (чего не было в v1.0):**

| # | Что добавлено | Закон / Правило |
|---|---|---|
| 1 | Секция GDPR Art.5 — 7 принципов как фундамент всей архитектуры | GDPR Art.5 |
| 2 | **Поток 1**: Onboarding Disclosure при регистрации 18+ (UI-макет) | GDPR Art.25(2) |
| 3 | **Поток 2**: UGC Terms Acceptance при первом посте (UI-макет) | App Store §1.2 · Google Play UGC |
| 4 | **Поток 3**: Prominent Disclosure перед Push/Camera/Photos (UI-макет) | Google Play User Data Policy |
| 5 | **Поток 4**: ATT диалог iOS + NSUserTrackingUsageDescription текст | App Store §5.1.2(i) |
| 6 | **Поток 5**: TCPA SMS Consent checkbox при добавлении телефона (UI-макет) | TCPA 47 U.S.C. §227 |
| 7 | **Поток 6**: Delete Account Modal с объяснением де-индексации (UI-макет) | GDPR Art.17(2) |
| 8 | Кнопка «Disconnect» для каждого 3rd-party логина (Google, Facebook) | App Store §5.1.1(v) |
| 9 | Child Safety Section в Help & Support (childsafety@bestme.com + NCMEC) | Google Play Child Safety Standards |
| 10 | Категория «Child Safety / CSAE» в форме жалоб | Google Play Child Safety Standards |
| 11 | Кнопка «Do Not Sell My Personal Information» в Your Data | CCPA §1798.120 · CPRA |
| 12 | Таблица политики хранения данных (активный / деактивированный / удалённый) | GDPR Art.5(1)(e) |
| 13 | Email Marketing Consent: пустые чекбоксы по умолчанию | CASL · ePrivacy Art.13 |
| 14 | DSA Art.27 — объяснение алгоритма рекомендаций | DSA Art.27 |
| 15 | auto_filter_comments = true | App Store §1.2 |
| 16 | Сводная таблица 40+ законов × все настройки | — |
| 17 | Чеклист публикации: 20 блокеров + 9 важных + 5 рекомендаций | — |
| 18 | Полный технический словарь variable_names + типы + defaults | — |

---

## 📋 ЧЕКЛИСТ ПУБЛИКАЦИИ (краткая версия)

### 🔴 Блокеры — без них App Store / Google Play не опубликует

- [ ] Веб-форма удаления: `bestme.com/account/delete` + URL в Play Console
- [ ] Кнопка «Disconnect» для Google/Facebook login
- [ ] Категория «Child Safety» в форме жалоб
- [ ] Email `childsafety@bestme.com` публично в Help & Support
- [ ] UGC ToS acceptance при первом контенте (Поток 2)
- [ ] ATT диалог iOS (Поток 4)
- [ ] Prominent Disclosure перед Push/Camera (Поток 3)
- [ ] Блок регистрации < 13 лет (возрастная верификация)
- [ ] TCPA SMS consent checkbox (Поток 5) при добавлении телефона
- [ ] Onboarding Disclosure для 18+ (Поток 1)
- [ ] «Do Not Sell My Personal Information» кнопка в Your Data
- [ ] Пустые чекбоксы email marketing по умолчанию
- ✅ Delete account в настройках
- ✅ Sign in with Apple
- ✅ Block / Report user
- ✅ Accessibility раздел
- ✅ Privacy Policy ссылка
- ✅ seo_indexable = false по умолчанию
- ✅ phone_visibility = ONLY_ME по умолчанию

### 🟡 Важно — до первого значительного роста

- [ ] One-click unsubscribe в каждом email
- [ ] Физический адрес компании в footer email
- [ ] DSA Art.27 — объяснение алгоритма рекомендаций
- [ ] DPO контакт публично виден (Help & Support)
- [ ] GDPR Art.17(2) — де-индексация при удалении (backend задача)
- [ ] Storage period policy в Your Data + Privacy Policy
- ✅ GDPR Art.18 — Restrict Processing
- ✅ GDPR Art.22 — Human review request

---

## 🔑 КЛЮЧЕВЫЕ DEFAULTS (самое важное)

| Variable | Default | Почему именно так |
|---|---|---|
| `seo_indexable` | `false` | GDPR Art.25 — СТРОГО OFF, штраф до 10 млн € |
| `phone_visibility` | `ONLY_ME` | TCPA §227 — телефон никогда не публичен |
| `email_visibility` | `ONLY_ME` | GDPR Art.25 + CAN-SPAM |
| `account_private` | `false` (18+) / `true` (13–17) | GDPR Art.25 + DSA Art.28(3)(g) |
| `online_status_visible` | `true` = Friends only | GDPR Art.25 — не «все», только друзья |
| `tag_approval_required` | `true` | GDPR Art.25 |
| `location_tagging_enabled` | `false` | GDPR Art.25 + ePrivacy |
| `sms_consent` | `false` (пустой чекбокс) | TCPA 47 U.S.C. §227 |
| `email_marketing_*` | `false` (пустые чекбоксы) | CASL + ePrivacy Art.13 |
| `captions_enabled` | `true` | EAA 2019/882 + ADA |
| `alt_text_auto_enabled` | `true` | EAA 2019/882 + ADA + WCAG 1.1.1 |

---

## ⚖️ ОХВАТ ЗАКОНОВ

> Все настройки в этом репозитории покрывают **21 закон + 2 магазина**:

| Юрисдикция | Законы |
|---|---|
| 🇪🇺 Европейский союз | GDPR · DSA · ePrivacy Directive |
| 🇺�� США (федеральный) | TCPA · CAN-SPAM · COPPA · ADA |
| 🇨🇦 Канада | PIPEDA · CASL · Quebec Law 25 · AODA |
| 🇮🇱 Израиль | PPL · Data Security Regulations · Disability Law 5758-1998 |
| 🇺🇸 Калифорния | CCPA/CPRA · Unruh Civil Rights Act |
| 📱 App Store | Apple App Store Review Guidelines (02.2026) |
| 📱 Google Play | Google Play Developer Policy (2024) · Child Safety Standards |
| 🌐 Стандарты | WCAG 2.1 AA |

---

*README.md | Bestme Settings Repository | март 2026*
