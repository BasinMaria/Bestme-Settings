# Bestme — Юридическое соответствие настроек профиля
## Все применимые законы: Европа · Канада · Израиль · Калифорния · США · Магазины

> ⚖️ = обязательное требование (нарушение → штраф / отказ в публикации)
> 💡 = рекомендация (несоответствие не штрафуется, но влияет на рейтинг/доверие)
> 🚫 = запрет (делать нельзя ни при каких условиях)
> ✅ = уже реализовано в ProfileSettingsFullSpec.md
> ❌ = ещё НЕ реализовано — требует добавления

---

## ЧАСТЬ 1. ОБЗОР ВСЕХ ПРИМЕНИМЫХ ЗАКОНОВ

| # | Закон / Правило | Юрисдикция | Что регулирует | Макс. штраф |
|---|---|---|---|---|
| 1 | **GDPR** — General Data Protection Regulation 2016/679 | 🇪🇺 ЕС + ЕЭЗ (Норвегия, Исландия, Лихтенштейн) | Обработка персональных данных | 20 млн € или 4% оборота |
| 2 | **DSA** — Digital Services Act 2022/2065 | 🇪🇺 ЕС (с 2024) | Ответственность платформ, модерация, прозрачность рекламы | 6% глобального оборота |
| 3 | **ePrivacy Directive** 2002/58/EC (обновление) | 🇪🇺 ЕС | Cookies, email, SMS, push-уведомления | по нац. законам |
| 4 | **PIPEDA** — Personal Information Protection and Electronic Documents Act | 🇨🇦 Канада (федерально) | Персональные данные коммерческих организаций | 100 000 CAD |
| 5 | **CASL** — Canada's Anti-Spam Legislation | 🇨🇦 Канада | Email, SMS, push — коммерческие сообщения | до 10 млн CAD |
| 6 | **Quebec Law 25** (Bill 64 / Loi 25) | 🇨🇦 Канада, провинция Квебек | Конфиденциальность (строже PIPEDA) | 25 млн CAD или 4% оборота |
| 7 | **Protection of Privacy Law** 5741-1981 + Amendment 2007 | 🇮🇱 Израиль | Базы данных, персональные данные | до 5 лет лишения свободы |
| 8 | **Data Security Regulations** 5777-2017 | 🇮🇱 Израиль | Технические требования к защите БД | Административные |
| 9 | **ILITA Guidelines** 2023 | 🇮🇱 Израиль | Рекомендации по обработке данных в интернет-сервисах | — |
| 10 | **CCPA** — California Consumer Privacy Act (2020) | 🇺🇸 Калифорния | Права потребителей на данные | $7 500 за намеренное нарушение |
| 11 | **CPRA** — California Privacy Rights Act (2023, заменяет CCPA) | 🇺🇸 Калифорния | Расширяет CCPA: новые права, CPPA-агентство | $7 500 за намеренное нарушение |
| 12 | **CAN-SPAM Act** (2003) | 🇺🇸 США (федерально) | Email-маркетинг | $51 744 за письмо |
| 13 | **TCPA** — Telephone Consumer Protection Act | 🇺🇸 США (федерально) | SMS, звонки, push | $1 500 за сообщение |
| 14 | **COPPA** — Children's Online Privacy Protection Act | 🇺🇸 США (федерально) | Дети до 13 лет | $51 744 за нарушение |
| 15 | **Apple App Store Guidelines** 5.1.x + 2.5.4 | 🌍 Везде (iOS) | Конфиденциальность, данные, удаление аккаунта, доступность | Удаление из магазина |
| 16 | **Google Play Developer Policy** | 🌍 Везде (Android) | Конфиденциальность, данные, доступность | Удаление из магазина |
| 17 | **EAA** — European Accessibility Act (Directive 2019/882) | 🇪🇺 ЕС + ЕЭЗ (с 28 июня 2025) | Доступность мобильных приложений (WCAG 2.1 AA) | по нац. законам ЕС |
| 18 | **ADA** — Americans with Disabilities Act + Section 508 | 🇺🇸 США | Цифровая доступность (WCAG 2.1 AA) | Судебные иски |
| 19 | **Israel Disability Law** 5758-1998 + Regulations 5763-2003 | 🇮🇱 Израиль | Равные права, доступность цифровых услуг | Административные + иски |
| 20 | **AODA** (Accessibility for Ontarians) + **Accessible Canada Act** 2019 | 🇨🇦 Канада | Доступность цифровых продуктов | до 100 000 CAD |
| 21 | **California Unruh Civil Rights Act** §51 Civil Code | 🇺🇸 Калифорния | Цифровая доступность как гражданское право | до $4 000 за нарушение |

---

## ЧАСТЬ 2. ЧТО ТРЕБУЕТ КАЖДЫЙ ЗАКОН — по разделам настроек

---

### 2.1 🇪🇺 GDPR (Европа)

> **Детальный аудит GDPR Art.25 и Art.17 (пункт за пунктом)** → `GDPRArt25Art17AuditSpec.md`

| Статья GDPR | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Art. 5 | Принцип минимизации данных — собирать только нужное | Account | ✅ |
| Art. 6 | Правовое основание для обработки (согласие или легитимный интерес) | Your Data → Consent | ✅ |
| Art. 7 | Согласие: добровольное, конкретное, информированное, отзываемое | Your Data → Withdraw consent | ✅ |
| Art. 12–14 | Уведомление об обработке данных (Privacy Notice) | Help → Privacy Policy | ✅ |
| Art. 15 | Право на доступ к своим данным | Your Data → Download my data | ✅ |
| Art. 16 | Право на исправление неточных данных | Account → Edit fields | ✅ |
| Art. 17(1) | Право на удаление: основания (a)–(d) | Account → Delete account | ✅ |
| Art. 17(2) | **Де-индексация**: при публичных данных — уведомить Google/Yandex/Bing об удалении | Backend: Search Console API при Delete account + при `seo_indexable OFF` | ❌ **КРИТИЧЕСКИЙ ПРОБЕЛ — нужен backend-процесс** |
| Art. 17(1)(f) | Удаление данных несовершеннолетних (Art.8) | Your Data → родительский запрос | ❌ **нужен механизм для родителей** |
| Art. 18 | Право на ограничение обработки | Your Data → Restrict processing | ❌ **нужно добавить** |
| Art. 20 | Право на переносимость данных (JSON/CSV) | Your Data → Data portability | ✅ |
| Art. 21 | Право на возражение против обработки (opt-out from profiling) | Your Data → Ad preferences | ✅ |
| Art. 22 | Право на отказ от автоматизированных решений / профилирования | Privacy → Discoverability → recommendations_opt_out | ✅ |
| Art. 25(1) | Privacy by Design: технические меры, псевдонимизация, минимизация | Privacy defaults + Login & Security | ✅ (псевдонимизация → Backend Spec) |
| Art. 25(2) | Privacy by Default: `seo_indexable=OFF`, `email/phone=ONLY_ME`, posts=`FRIENDS` | Privacy → все defaults | ✅ |
| Art. 25(2) | Privacy by Default: **onboarding disclosure** для открытого профиля 18+ | Onboarding UX | ❌ **нужно добавить уведомление при регистрации** |
| Art. 25(2) | Privacy by Default: **storage period** — срок хранения данных | Your Data | ❌ **нужна политика хранения** |
| Art. 32 | Технические меры безопасности | Login & Security → 2FA, sessions | ✅ |
| Art. 33 | Уведомление об утечке (72 часа) | Notifications → security (non-disable) | ✅ |
| Art. 37–39 | DPO (Data Protection Officer) — если >250 сотрудников или >5000 субъектов | Внутренний процесс | 💡 |

**Ключевые требования GDPR к настройкам:**
- `seo_indexable` = **OFF** по умолчанию (Art. 25)
- `recommendations_opt_out` должен быть доступен (Art. 22)
- Удаление аккаунта + удаление данных — отдельные действия (Art. 17)
- **Art.17(2) де-индексация** — ❌ при Delete account → автоматический запрос в Google/Yandex Search Console API
- **Ограничение обработки** (Art. 18) — ❌ нет в текущей спеке → нужно добавить в Your Data
- **Onboarding disclosure** — ❌ явное уведомление о публичном профиле при регистрации взрослых

---

### 2.2 🇪🇺 DSA — Digital Services Act (Европа)

| Статья DSA | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Art. 14 | Механизм жалоб на незаконный контент | Help → Report a problem | ✅ |
| Art. 17 | Уведомление пользователя о решении по модерации | Notifications → Content & Moderation | ✅ |
| Art. 18 | Внутренняя апелляционная система (не менее 6 мес.) | Notifications → profile_appeal_decision | ✅ |
| Art. 20 | Приоритет для доверенных сигнальщиков | Внутренний процесс | 💡 |
| Art. 26 | Прозрачность рекламы — кто таргетирует и почему | Your Data → Ad preferences | ❌ **нужно добавить метку "почему я вижу эту рекламу"** |
| Art. 27 | Объяснение алгоритмов рекомендаций | Privacy → Discoverability | ❌ **нужно добавить описание алгоритма** |
| Art. 28 | Запрет таргетированной рекламы на несовершеннолетних | Account → Date of birth | ✅ (возраст) |
| Art. 29 | Право отключить профилирование для рекламы без штрафа для пользователя | Your Data → Ad preferences | ❌ **opt-out без последствий** |
| Art. 42 | Ежегодный отчёт о прозрачности (для VLOP > 45 млн пользователей) | Внутренний процесс | 💡 |

---

### 2.3 🇪🇺 ePrivacy Directive (Европа)

| Статья | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Art. 5(3) | Cookies: opt-in согласие до установки нетехнических cookies | Your Data → Cookie settings | ✅ |
| Art. 13 | Email/SMS-маркетинг: opt-in обязателен | Notifications → Email channel | ✅ |
| Art. 13(2) | Возможность отписаться от каждого email (one-click unsubscribe) | Notifications (unsubscribe link в каждом письме) | ❌ **проверить наличие** |
| Art. 6 | Метаданные трафика — удалять или анонимизировать | Внутренний процесс | 💡 |

---

### 2.4 🇨🇦 PIPEDA (Канада, федерально)

| Принцип PIPEDA | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Принцип 1 | Accountability: назначить Privacy Officer | Внутренний | 💡 |
| Принцип 2 | Identifying Purposes: объяснить зачем собираем данные | Your Data → Privacy Policy | ✅ |
| Принцип 3 | Consent: явное согласие до сбора | Your Data → Consent history | ✅ |
| Принцип 4 | Limiting Collection: только нужные данные | Account | ✅ |
| Принцип 5 | Limiting Use, Disclosure: не передавать без согласия | Your Data → Ad preferences | ✅ |
| Принцип 7 | Safeguards: технические меры защиты | Login & Security → 2FA | ✅ |
| Принцип 8 | Openness: доступная Privacy Policy | Help → Privacy Policy | ✅ |
| Принцип 9 | **Individual Access**: право запросить свои данные | Your Data → Download | ✅ |
| Принцип 10 | **Challenging Compliance**: механизм жалоб | Help → Contact support | ✅ |
| **Breach notification** | Уведомление OPC и пользователей при утечке «real risk of significant harm» | Notifications → security | ✅ |

**Ключевые отличия PIPEDA от GDPR:**
- PIPEDA допускает **implied consent** (подразумеваемое согласие) в некоторых случаях, GDPR — нет
- Нет права на «забвение» в явном виде, но есть право на уточнение данных
- Штрафы значительно меньше, но репутационные риски высокие

---

### 2.5 🇨🇦 CASL — Canada's Anti-Spam Legislation

| Требование CASL | Раздел настроек | Статус |
|---|---|---|
| **Express consent** до отправки любого коммерческого email / push | Notifications → Email / Push opt-in | ✅ |
| **Unsubscribe mechanism**: одно действие, работает ≤ 10 рабочих дней | Notifications → каждая группа | ❌ **проверить unsubscribe из email** |
| Обязательный **sender identification** в каждом письме | Email-шаблоны | 💡 |
| Хранить **доказательство согласия** (дата, IP, версия формы) | Your Data → Consent history | ✅ |
| Запрет на pre-checked boxes при сборе email | Onboarding / форма | ❌ **UX: флажки должны быть пустыми** |

---

### 2.6 🇨🇦 Quebec Law 25 / Loi 25 (Bill 64) — строже PIPEDA

| Статья | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Art. 8 | **Privacy by Default** (как GDPR Art. 25) | Privacy (все defaults = самые строгие) | ✅ |
| Art. 12 | **Право на уничтожение** данных (= GDPR Art. 17) | Account → Delete account | ✅ |
| Art. 27 | **Право на переносимость** данных | Your Data → Data portability | ✅ |
| Art. 8.1 | **Автоматические решения**: уведомлять + право на человека | Your Data → ❌ **нужно «Право на пересмотр автоматического решения»** |
| Art. 3.2 | **Privacy Impact Assessment** при новых технологиях | Внутренний процесс | 💡 |
| Art. 5 | Назначить **Chief Privacy Officer** (публично указан) | Help → Contact | ❌ **нужна ссылка на CPO** |
| Art. 12.1 | **Конфиденциальность по умолчанию** с момента сбора | Account (date of birth, phone) | ✅ |

---

### 2.7 🇮🇱 Israel — Protection of Privacy Law 5741-1981 + Amendments

| Статья | Требование | Раздел настроек | Статус |
|---|---|---|---|
| Sec. 1 | Определение «sensitive information» (здоровье, сексуальная ориентация, вероисповедание) — строгая защита | Privacy → Contact Info + Account | ✅ (ONLY_ME) |
| Sec. 2 | Запрет передачи данных без согласия | Your Data → Ad preferences | ✅ |
| Sec. 8 | **Регистрация базы данных** в Реестре баз данных Израиля (обязательно для > 10 000 субъектов или чувствительных данных) | Внутренний | ❌ **юридический процесс, не UI** |
| Sec. 11 | Право субъекта **просмотреть свои данные** | Your Data → Download | ✅ |
| Sec. 14 | Право на **исправление** данных | Account → Edit | ✅ |
| Sec. 17C | Уведомление об **утечке** данных (Attorney General + субъект) | Notifications → security | ✅ |
| Sec. 2A | Запрет на **нежелательную рассылку** без согласия | Notifications → Email opt-in | ✅ |

**Israel Data Security Regulations 5777-2017 (технические):**

| Уровень безопасности | Требование | Статус |
|---|---|---|
| Базовый | Шифрование при передаче (HTTPS/TLS) | ✅ |
| Средний (чувствительные данные) | Шифрование хранения + контроль доступа | ⚠️ зависит от backend |
| Средний | Двухфакторная аутентификация для admins | Login & Security → 2FA | ✅ |
| Средний | Журнал доступа к данным (audit log) | Login & Security → Login activity | ✅ |

---

### 2.8 🇺🇸 CCPA / CPRA (Калифорния)

> Применяется если: ≥ $25M дохода, ИЛИ ≥ 100 000 California residents, ИЛИ ≥ 50% дохода от продажи данных

| Право / Требование | CCPA/CPRA Статья | Раздел настроек | Статус |
|---|---|---|---|
| **Right to Know** — какие данные собраны | § 1798.100 | Your Data → Download | ✅ |
| **Right to Delete** — удалить данные | § 1798.105 | Account → Delete account | ✅ |
| **Right to Opt-Out of Sale** — не продавать данные | § 1798.120 | Your Data → ❌ **нужна кнопка "Do Not Sell My Personal Information"** |
| **Right to Non-Discrimination** — не ухудшать сервис за opt-out | § 1798.125 | UX-принцип | 💡 |
| **Right to Correct** (CPRA) | § 1798.106 | Account → Edit fields | ✅ |
| **Right to Limit Use of Sensitive Info** (CPRA) | § 1798.121 | Privacy → Contact Info | ✅ |
| **Right to Know about Automated Decision** (CPRA) | § 1798.185 | Your Data → ❌ **нужно объяснение автоматических решений** |
| **"Do Not Share" for cross-context behavioral ads** (CPRA) | § 1798.120 | Your Data → Ad preferences | ❌ **нужна отдельная настройка** |
| **Privacy Policy** должна содержать полный список категорий данных | — | Help → Privacy Policy | ✅ |
| **Contact method** для California requests | — | Help → Contact support | ✅ |

**Ключевые отличия CPRA (2023) от CCPA:**
- Новое агентство CPPA вместо AG
- "Sensitive personal information" — отдельная категория с правом ограничения
- "Share" = передача данных для таргетированной рекламы — теперь регулируется отдельно

---

### 2.9 🇺🇸 CAN-SPAM (США, email)

| Требование | Раздел настроек | Статус |
|---|---|---|
| Правдивый заголовок "From" | Email-шаблоны | 💡 |
| Не вводящий в заблуждение subject line | Email-шаблоны | 💡 |
| Указание физического адреса организации в каждом письме | Email-шаблоны | ❌ **проверить footer** |
| **Opt-out механизм** в каждом коммерческом письме | Notifications → Email unsubscribe | ❌ **проверить** |
| Выполнить opt-out **в течение 10 дней** | Система | 💡 |
| Email / phone не отображать PUBLIC | Privacy → Contact Info → `email_visibility` = ONLY_ME default | ✅ |

---

### 2.10 🇺🇸 TCPA (США, SMS/телефон)

| Требование | Раздел настроек | Статус |
|---|---|---|
| **Prior Express Written Consent** для SMS-маркетинга | Onboarding → SMS opt-in | ❌ **если есть SMS — проверить** |
| Opt-out через STOP | SMS-система | 💡 |
| `phone_visibility` не может быть PUBLIC | Privacy → Contact Info | ✅ |
| Запрет automated calls без согласия | Не актуально для соцсети | — |

---

### 2.11 🇺🇸 COPPA (США, дети < 13)

| Требование | Раздел настроек | Статус |
|---|---|---|
| **Возрастная проверка** при регистрации | Account → Date of birth | ✅ |
| Запрет регистрации < 13 лет (или согласие родителей) | Onboarding | ❌ **явный блок < 13 при регистрации** |
| Не собирать данные от < 13 без согласия родителей | Account | ⚠️ зависит от onboarding |
| Удалять данные детей по запросу родителей | Your Data → Delete | ✅ |
| Не показывать таргетированную рекламу < 13 | Content + DSA Art.28 | ✅ (возраст) |

---

### 2.12 📱 Apple App Store Guidelines

> **Детальный аудит всех применимых пунктов App Store Review Guidelines (Feb 2026)** → `AppStoreAuditSpec.md`

| Правило | Требование | Раздел в Bestme | Статус |
|---|---|---|---|
| **§1.2** | UGC: фильтрация неприемлемого контента до публикации | Content moderation | ⚠️ Нужна документация в App Review Notes |
| **§1.2** | UGC: механизм жалоб на контент + своевременный ответ | Help → Report a problem | ✅ |
| **§1.2** | UGC: **блокировка агрессивных пользователей** | Privacy → Blocked Accounts | ✅ |
| **§1.2** | UGC: опубликованные контакты для пользователей | Help & Support → Contact | ✅ |
| **§1.3 / §5.1.4** | Дети: нет 3rd-party analytics/ads для несовершеннолетних | Age-gated routing по date of birth | ⚠️ SDK audit нужен |
| **§2.3.6** | Честный возрастной рейтинг (UGC → скорее 17+) | App Store Connect metadata | 🔄 При подаче |
| **§4.5.4** | Push: opt-in только, не обязательны для работы | Notifications settings | ✅ |
| **§4.8** | Если есть Google/Facebook login → **Sign in with Apple обязателен** | Login & Security | ✅ |
| **§5.1.1(i)** | Privacy Policy: data **retention/deletion** policy обязательна | Your Data + Privacy Policy | ❌ **ПРОБЕЛ** |
| **§5.1.1(i)** | Privacy Policy: список всех 3rd-party получателей данных | Privacy Policy | ⚠️ Проверить полноту |
| **§5.1.1(ii)** | **Pre-permission screen** перед запросом разрешений iOS | Onboarding | ❌ **ПРОБЕЛ** |
| **§5.1.1(iii)** | Data minimization: только необходимые permissions | iOS implementation | ⚠️ Проверить |
| **§5.1.1(v)** | Удаление аккаунта **изнутри приложения** обязательно | Account → Delete account | ✅ |
| **§5.1.1(v)** | **Кнопка отключения каждого 3rd-party login** (Google/Facebook) | Login & Security | ❌ **ПРОБЕЛ** |
| **§5.1.2(i) ATT** | **App Tracking Transparency** dialog (iOS 14.5+) — если любая аналитика/реклама | iOS codebase | ❌ **Нужна проверка** |
| **§5.1.2(i)** | Согласие перед передачей данных в **3rd-party AI** | Your Data / onboarding | ❌ **ПРОБЕЛ если используется AI** |
| **§5.1.5** | Location Services — только если напрямую нужно | N/A | — |
| **Privacy Nutrition Labels** | Заполнить все Data Types в App Store Connect | App Store Connect | 🔄 Административный |

**Ключевые требования App Store к настройкам:**
- **§1.2 (4 пункта)** — все 4 обязательны для UGC/соцсети: filter + report + block + contact
- **§4.8** — Sign in with Apple при наличии любого 3rd-party login ✅
- **§5.1.1(i)** — Privacy Policy обязана содержать data retention policy ❌ нет
- **§5.1.1(ii)** — Pre-permission screen перед каждым iOS-разрешением ❌ нет
- **§5.1.1(v)** — Кнопка отключения Google/Facebook login ❌ нет
- **§5.1.2(i) ATT** — App Tracking Transparency если используется tracking ❌ проверить

---

### 2.13 🤖 Google Play Developer Policy

| Правило | Требование | Раздел настроек | Статус |
|---|---|---|---|
| **Data Safety section** | Заполнить Data Safety Form в Play Console | Play Console | ❌ **административный процесс** |
| **Prominent Disclosure** | Объяснить сбор данных до запроса разрешений | Onboarding / Privacy Notice | ❌ **нужен pre-permission screen** |
| **Account Deletion** | Удаление аккаунта из настроек + из web (не только в app) | Account → Delete + веб-форма | ❌ **нужна веб-форма удаления** |
| **Sensitive Permissions** | Доступ к контактам, микрофону, камере — только когда нужно | Системные диалоги | 💡 |
| **Accessibility** | AccessibilityService только с явным обоснованием | — | 💡 |

---

### 2.14 ♿ Законы о доступности (Accessibility)

> ⚠️ Accessibility — это НЕ только требование магазинов. В ЕС это закон с 28 июня 2025 года.

| Закон | Юрисдикция | Требование | Раздел настроек | Статус |
|---|---|---|---|---|
| **EAA** Directive 2019/882, Art.4 | 🇪🇺 ЕС + ЕЭЗ (с 28.06.2025) | WCAG 2.1 AA: текст масштабируемый, контраст ≥4.5:1, субтитры, screen reader | Accessibility (8.1–8.3) | ✅ |
| **EAA** Art.4(2) | 🇪🇺 ЕС | Alt-text для изображений | Accessibility → alt_text_enabled = ON | ✅ |
| **EAA** Art.4(3) | 🇪🇺 ЕС | Возможность отключить анимации (reduce motion) | Accessibility → reduce_motion | ✅ |
| **ADA** + **Section 508** | 🇺🇸 США | WCAG 2.1 AA для веб/мобильных сервисов, субтитры, keyboard nav | Accessibility (все настройки) | ✅ |
| **Israel Disability Law** 5758-1998 + Reg. 5763-2003, § 19i | 🇮🇱 Израиль | Интернет-сервисы: WCAG 2.0 AA (обязательно для бизнесов > 5 сотрудников) | Accessibility | ✅ |
| **AODA** IASR + **Accessible Canada Act** S.C. 2019 | 🇨🇦 Канада | WCAG 2.0 AA (организации > 50 сотрудников) | Accessibility | ✅ |
| **California Unruh Civil Rights Act** §51 | 🇺🇸 Калифорния | Цифровые продукты = места общественного пользования (судебная практика: ADA WCAG) | Accessibility | ✅ |
| **Apple App Store** 2.5.4 | 📱 iOS | VoiceOver совместимость, масштаб текста | Accessibility → Screen reader info | ✅ |
| **Google Play** Accessibility | 🤖 Android | TalkBack совместимость, минимальный размер tappable area (48×48 dp) | Accessibility | ✅ |

**WCAG 2.1 AA — основные критерии, влияющие на настройки:**

| WCAG Критерий | Описание | Настройка в приложении | Закон |
|---|---|---|---|
| 1.1.1 Non-text Content | Alt-text для всех изображений | `alt_text_enabled` = ON | EAA · ADA · Israel |
| 1.2.2 Captions | Субтитры для видео | `captions_enabled` | EAA · ADA · AODA |
| 1.4.3 Contrast | Минимум 4.5:1 для текста | `high_contrast_enabled` | EAA · ADA |
| 1.4.4 Resize Text | До 200% без потери контента | `text_size` slider | EAA · ADA |
| 2.1.1 Keyboard | Вся функциональность через клавиатуру | Keyboard navigation info | EAA · ADA |
| 2.3.1 Seizures | Нет контента > 3 вспышки/сек | `reduce_motion_enabled` | EAA · ADA |
| 2.4.7 Focus Visible | Видимый фокус при навигации | Focus indicators info | EAA · ADA |

---

## ЧАСТЬ 3. СВОДНАЯ ТАБЛИЦА — настройка × закон

| Настройка / Экран | GDPR | DSA | ePrivacy | PIPEDA | CASL | Quebec L25 | Israel PPL | CCPA/CPRA | CAN-SPAM | COPPA | App Store | Google Play |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Delete account | Art.17(1) | — | — | Pr.9 | — | Art.12 | Sec.14 | §1798.105 | — | — | 5.1.1(v) | ⚖️ |
| **De-indexing on delete** ❌ | **Art.17(2)** | — | — | — | — | Art.12 | — | — | — | — | — | — |
| Download my data | Art.15 | — | — | Pr.9 | — | Art.27 | Sec.11 | §1798.100 | — | — | — | ⚖️ |
| Data portability | Art.20 | — | — | — | — | Art.27 | — | — | — | — | — | — |
| Withdraw consent | Art.7 | — | — | Pr.3 | ⚖️ | Art.3.2 | — | — | — | — | — | — |
| Cookie settings | — | — | Art.5(3) | — | — | — | — | — | — | — | — | — |
| Ad preferences / opt-out | Art.21/22 | Art.29 | — | Pr.5 | — | — | — | §1798.120 | — | — | — | — |
| **Do Not Sell** button | — | — | — | — | — | — | — | §1798.120 ❌ | — | — | — | — |
| Consent history | Art.7 | — | — | Pr.3 | ⚖️ | — | — | — | — | — | — | — |
| Privacy Policy link | Art.13 | — | — | Pr.8 | — | — | — | ⚖️ | — | — | 5.1.1 | ⚖️ |
| email_visibility = ONLY_ME | Art.25(2) | — | Art.13 | — | — | Art.8 | — | — | ⚖️ | — | — | — |
| phone_visibility = ONLY_ME | Art.25(2) | — | — | — | — | Art.8 | — | — | — | ⚖️ TCPA | — | — |
| seo_indexable = false | Art.25(2)/17(2) | — | — | — | — | Art.8 | — | — | — | — | — | — |
| **Onboarding disclosure (open profile)** ❌ | **Art.25(2)** | — | — | — | — | Art.8 | — | — | — | — | — | — |
| **Storage period policy** ❌ | **Art.25(2)** | — | — | — | — | — | — | — | — | — | — | — |
| recommendations_opt_out | Art.22 | Art.27/29 | — | — | — | Art.8.1 | — | §1798.121 | — | — | — | — |
| Date of birth (age gate) | Art.8 | Art.28 | — | — | — | — | — | — | — | ⚖️ COPPA | — | — |
| 2FA | Art.32 | — | — | Pr.7 | — | — | Data Sec. | — | — | — | — | — |
| Active sessions / terminate | Art.32 | — | — | Pr.7 | — | — | Data Sec. | — | — | — | — | — |
| Login activity log | Art.32 | — | — | Pr.7 | — | — | Data Sec. | — | — | — | — | — |
| Sign in with Apple | — | — | — | — | — | — | — | — | — | — | 5.1.3 ⚖️ | — |
| Notifications: security (non-disable) | Art.33 | Art.17 | — | Breach notif. | — | — | Sec.17C | — | — | — | — | — |
| Notifications: moderation (non-disable) | — | Art.17/18 | — | — | — | — | — | — | — | — | — | — |
| Report a problem | — | Art.14 | — | Pr.10 | — | — | — | — | — | — | ⚖️ | ⚖️ |
| Help & Support contact | — | Art.14 | — | Pr.10 | — | Art.5 CPO | — | ⚖️ | — | — | ⚖️ | ⚖️ |
| Accessibility section (text size, contrast, captions, alt-text) | — | — | — | — | — | — | Israel Dis.Law | — | — | — | ⚖️ 2.5.4 | ⚖️ |
| Accessibility (EAA — мобильные приложения) | — | — | — | — | AODA | — | ⚖️ Dis.5758 | — | ⚖️ ADA | — | — | — |
| Terms of Use link | — | — | — | — | — | — | — | — | — | — | ⚖️ | ⚖️ |

---

## ЧАСТЬ 4. ЧТО НУЖНО ДОБАВИТЬ ИЛИ ИЗМЕНИТЬ

### ❌ Критично для публикации (без этого → отказ)

| # | Что добавить | Где | Закон |
|---|---|---|---|
| 1 | Кнопка **«Do Not Sell My Personal Information»** (или «Do Not Share») | Your Data | CCPA/CPRA §1798.120 |
| 2 | Веб-форма удаления аккаунта (не только in-app) | Сайт / веб-версия | Google Play Policy |
| 3 | Блок регистрации для < 13 лет (возрастная верификация) | Onboarding | COPPA |
| 4 | Pre-permission screen перед запросом системных разрешений | Onboarding | Google Play Prominent Disclosure |
| 5 | **Право на ограничение обработки** (Restrict Processing) | Your Data | GDPR Art.18 |
| 6 | Объяснение алгоритма рекомендаций (краткое описание) | Privacy → Discoverability | DSA Art.27 |
| 7 | **Opt-out from profiling for ads** без штрафа для пользователя | Your Data → Ad preferences | DSA Art.29 |
| 8 | **Art.17(2) де-индексация**: при Delete account — автоматический запрос удаления URL в Google Search Console API + Yandex.Webmaster API + Bing | Backend | GDPR Art.17(2) |
| 9 | **Art.17(2) де-индексация**: при `seo_indexable OFF` — аналогичный процесс | Backend | GDPR Art.17(2) |
| 10 | **Onboarding disclosure**: явное уведомление о публичном профиле при регистрации взрослых (18+) | Onboarding UX | GDPR Art.25(2) |

### ⚠️ Важно для соответствия (может привести к штрафам)

| # | Что добавить | Где | Закон |
|---|---|---|---|
| 11 | **Unsubscribe (one-click)** из каждого email-уведомления | Email-шаблоны + Notifications | ePrivacy Art.13(2) + CASL |
| 12 | **«Почему я вижу эту рекламу»** — ссылка/объяснение | Your Data + Ad preferences | DSA Art.26 |
| 13 | **Chief Privacy Officer** контакт публично виден | Help & Support | Quebec Law 25 Art.5 |
| 14 | **Право на пересмотр автоматического решения** (human review) | Your Data | GDPR Art.22 + Quebec Art.8.1 + CPRA |
| 15 | Pre-checked boxes = запрещены для opt-in | Onboarding + Notifications | CASL |
| 16 | Физический адрес организации в footer каждого email | Email-шаблоны | CAN-SPAM |
| 17 | Регистрация базы данных в Израиле | Юридический отдел | Israel PPL Sec.8 |
| 18 | **Storage period policy**: срок хранения данных при деактивации / после удаления | Your Data + Privacy Policy | GDPR Art.25(2) |
| 19 | **Delete account UX**: пояснение о де-индексации в модальном окне («до 30 дней») | Account → Delete account modal | GDPR Art.17(2) |

### 💡 Рекомендации (не обязательно, но повышают доверие)

| # | Что добавить | Где | Закон |
|---|---|---|---|
| 20 | Privacy Nutrition Labels заполнены в App Store Connect | App Store Connect | Apple Guidelines |
| 21 | Data Safety Form заполнена в Google Play Console | Google Play Console | Google Play Policy |
| 22 | DPO (Data Protection Officer) назначен | Внутренний | GDPR Art.37 |
| 23 | Privacy Impact Assessment для новых функций | Внутренний | Quebec Art.3.2 |
| 24 | Audit log доступа к данным | Login & Security | Israel Data Security |
| 25 | Ссылка на Privacy Policy в каждом email-письме | Email-шаблоны | PIPEDA + GDPR |

---

## ЧАСТЬ 5. СВОДНЫЙ ЧЕКЛИСТ ДЛЯ ПУБЛИКАЦИИ

### ✅ App Store (Apple)
- [x] Delete account в настройках (5.1.1v)
- [x] Privacy Policy ссылка
- [x] Sign in with Apple (если есть Google/Facebook)
- [x] Push: системный диалог iOS
- [x] Accessibility раздел
- [ ] ❌ Privacy Nutrition Labels в App Store Connect

### ✅ Google Play (Android)
- [x] Delete account в настройках
- [ ] ❌ Веб-форма удаления аккаунта (отдельно от app)
- [ ] ❌ Data Safety Form в Play Console
- [ ] ❌ Pre-permission screen (Prominent Disclosure)
- [x] Privacy Policy ссылка
- [x] Accessibility раздел

### ✅ Европа (GDPR + DSA + ePrivacy)
- [x] Согласие (consent) и отзыв согласия
- [x] Экспорт данных (Art.15)
- [x] Удаление данных (Art.17(1))
- [x] Переносимость (Art.20)
- [x] Opt-out от рекомендаций (Art.22)
- [x] Privacy by Default (Art.25) — все defaults = FRIENDS/PRIVATE
- [x] seo_indexable = OFF (Art.25(2))
- [x] 2FA и безопасность (Art.32)
- [x] Cookie consent
- [ ] ❌ **Art.17(2) де-индексация Google/Yandex при Delete account** (backend)
- [ ] ❌ **Art.25(2) onboarding disclosure** (открытый профиль 18+)
- [ ] ❌ **Art.25(2) storage period** — политика хранения данных
- [ ] ❌ Ограничение обработки (Art.18)
- [ ] ❌ Объяснение алгоритма рекомендаций (DSA Art.27)
- [ ] ❌ «Do Not Share» для рекламы (DSA Art.29)

### ✅ Канада (PIPEDA + CASL + Quebec Law 25)
- [x] Download my data
- [x] Consent history
- [x] Email opt-in
- [ ] ❌ One-click unsubscribe в каждом письме (CASL)
- [ ] ❌ CPO контакт публичный (Quebec Art.5)
- [ ] ❌ Human review права (Quebec Art.8.1)
- [ ] ❌ Pre-checked boxes = пустые (CASL)

### ✅ Израиль (PPL + Data Security Regs + Disability Law)
- [x] email_visibility = ONLY_ME
- [x] Уведомления об утечке
- [x] 2FA
- [x] Login activity log
- [x] Accessibility раздел (Israel Disability Law 5758-1998 + Regs 5763-2003)
- [ ] ❌ Регистрация БД в реестре (юридический процесс)

### ✅ Калифорния (CCPA / CPRA + Unruh Civil Rights Act)
- [x] Download my data (Right to Know)
- [x] Delete account (Right to Delete)
- [x] Correct data (Right to Correct)
- [x] Accessibility раздел (California Unruh Civil Rights Act §51)
- [ ] ❌ «Do Not Sell My Personal Information» кнопка
- [ ] ❌ Объяснение автоматических решений

### ✅ США (CAN-SPAM + TCPA + COPPA + ADA)
- [x] email_visibility = ONLY_ME default
- [x] phone_visibility = ONLY_ME default
- [x] Date of birth field
- [x] Accessibility раздел (ADA — WCAG 2.1 AA)
- [ ] ❌ Блок регистрации < 13 лет (COPPA)
- [ ] ❌ Opt-out из каждого email (CAN-SPAM)

### ✅ Канада (PIPEDA + CASL + Quebec L25 + AODA)
- [x] Download my data
- [x] Consent history
- [x] Email opt-in
- [x] Accessibility раздел (AODA + Accessible Canada Act)
- [ ] ❌ One-click unsubscribe в каждом письме (CASL)
- [ ] ❌ CPO контакт публичный (Quebec Art.5)
- [ ] ❌ Human review права (Quebec Art.8.1)
- [ ] ❌ Pre-checked boxes = пустые (CASL)

---

## ЧАСТЬ 6. ПРИОРИТИЗАЦИЯ ИЗМЕНЕНИЙ

### 🔴 БЛОКЕРЫ публикации (сделать ДО релиза)

1. **Веб-форма удаления аккаунта** — Google Play требует не только in-app
2. **Блок регистрации для < 13** — COPPA, отказ App Store без этого
3. **«Do Not Sell My Personal Information»** — CCPA/CPRA (если аудитория Калифорния)
4. **Pre-checked boxes = пустые** во всех формах opt-in
5. **Accessibility раздел** — EAA (с 28.06.2025 ЕС), ADA (США), Israel Disability Law, AODA (Канада) + App Store + Google Play

### 🟡 ВАЖНО (сделать до первого значительного роста)

6. **Ограничение обработки** (Restrict Processing) — GDPR Art.18
7. **One-click unsubscribe** в каждом email — CASL + ePrivacy
8. **Объяснение алгоритма рекомендаций** — DSA Art.27
9. **CPO контакт** публично — Quebec Law 25
10. **Физический адрес** в footer emails — CAN-SPAM

### 🟢 РЕКОМЕНДАЦИИ (до масштабирования)

11. Privacy Nutrition Labels (App Store Connect)
12. Data Safety Form (Google Play Console)
13. Privacy Impact Assessment процесс
14. DPO назначение
15. Регистрация БД Израиль

---

*Файл: `LegalComplianceSpec.md` | Версия 2.0 | Юрисдикции: EU/EEA · Canada · Israel · California · USA · App Stores | 21 закон*
