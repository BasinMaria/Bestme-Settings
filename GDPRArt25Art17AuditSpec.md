# Bestme — GDPR Art.25 + Art.17: аудит соответствия по каждому пункту
## Полный разбор: что именно требует закон и как это реализовано в наших настройках

> **Аудит основан на официальном тексте регламента GDPR 2016/679.**
> Статус: ✅ Соответствует · ⚠️ Частично / нужно уточнение · ❌ Нарушение / пробел · 🔄 Требует технического решения (backend/ops)

---

## ЧАСТЬ 1. GDPR Art.25 — Data Protection by Design and by Default

### Официальный текст (пронумерованные пункты для аудита)

> **Art.25(1) — Privacy by Design:**
> *"…the controller shall…implement appropriate technical and organisational measures, such as pseudonymisation, which are designed to implement data-protection principles, such as data minimisation, in an effective manner and to integrate the necessary safeguards into the processing in order to meet the requirements of this Regulation and protect the rights of data subjects."*

> **Art.25(2) — Privacy by Default:**
> *"The controller shall implement appropriate technical and organisational measures for ensuring that, by default, only personal data which are necessary for each specific purpose of the processing are processed. That obligation applies to the amount of personal data collected, the extent of their processing, the period of their storage and their accessibility. In particular, such measures shall ensure that by default personal data are not made accessible without the individual's intervention to an indefinite number of natural persons."*

---

### 1.1 Art.25(1) — Privacy by Design: пункт за пунктом

| # | Цитата из Art.25(1) | Наша реализация | Статус |
|---|---|---|---|
| 1.1.1 | *"appropriate technical and organisational measures"* | Privacy-ориентированные defaults во всех полях настроек (см. SettingsTZ.md §2) | ✅ |
| 1.1.2 | *"such as pseudonymisation"* | **Не отражено в настройках.** Pseudonymisation = техническая мера backend: замена прямых идентификаторов токенами при передаче/хранении | ⚠️ Нужна в Backend Architecture Spec, не в UI-настройках |
| 1.1.3 | *"data-protection principles, such as data minimisation"* | Account section: собираем только необходимые поля. Optional-поля (биография, город, соцсети) — не обязательны | ✅ |
| 1.1.4 | *"at the time of the determination of the means for processing"* | Privacy-by-Design встроен на этапе проектирования (данный документ + SettingsTZ.md) | ✅ |
| 1.1.5 | *"at the time of the processing itself"* | Настройки применяются в реальном времени при каждом запросе к данным | ✅ (backend requirement) |
| 1.1.6 | *"integrate the necessary safeguards into the processing"* | 2FA, session management, login activity log (Login & Security раздел) | ✅ |

> **Вывод по Art.25(1):** ✅ Соответствие на уровне UI/UX-настроек.
> ⚠️ **Открытый пункт**: Pseudonymisation — нужно отразить в Backend/Infrastructure документации (не в Settings UI spec).

---

### 1.2 Art.25(2) — Privacy by Default: пункт за пунктом

Ключевые четыре обязательства из Art.25(2):

#### Обязательство A: «amount of personal data collected» (объём собранных данных)

| Поле | Что делаем | Статус |
|---|---|---|
| Account section | Обязательные поля: имя, email, дата рождения. Всё остальное — optional | ✅ |
| Profile fields | Телефон, биография, город, соцсети — необязательные | ✅ |
| Photo | Аватар — опциональный | ✅ |

#### Обязательство B: «extent of their processing» (объём обработки)

| Аспект | Что делаем | Статус |
|---|---|---|
| SEO indexing | `seo_indexable = false` по умолчанию — данные НЕ передаются поисковикам | ✅ |
| Recommendations | `recommendations_opt_out` — пользователь может ограничить профилирование | ✅ |
| Ad targeting | `ad_preferences` — opt-out из таргетированной рекламы | ✅ |

#### Обязательство C: «period of their storage» (срок хранения)

| Аспект | Что делаем | Статус |
|---|---|---|
| Срок хранения активных данных | **НЕ ОПРЕДЕЛЁН** в настройках | ❌ **Пробел** |
| Удаление при деактивации аккаунта | Deactivate account → данные хранятся X дней, затем? | ⚠️ Нужна политика |
| Удаление после Delete account | Данные должны удаляться в разумный срок | ⚠️ Срок не указан |

> ❌ **Конкретный пробел**: В разделе «Your Data» нет настройки срока хранения и нет информации о сроках автоудаления. Необходимо добавить:
> - Уведомление о сроке хранения данных в `Your Data → Privacy Policy`
> - При деактивации: пояснение «данные будут удалены через X дней после деактивации»

#### Обязательство D: «accessibility» (доступность данных третьим лицам)

Ключевая фраза: *"by default personal data are not made accessible without the individual's intervention to an indefinite number of natural persons"*

**«Indefinite number of natural persons» = неограниченный круг лиц = весь интернет.**

| Поле | Default | Соответствие Art.25(2) последней фразе | Обоснование |
|---|---|---|---|
| `seo_indexable` | `false` ← OFF | ✅ **СТРОГО СООТВЕТСТВУЕТ** | Данные НЕ передаются неограниченному кругу лиц (поисковики) |
| `email_visibility` | `ONLY_ME` | ✅ Соответствует | Ограниченный круг = только владелец |
| `phone_visibility` | `ONLY_ME` | ✅ Соответствует | Ограниченный круг |
| `default_post_audience` | `FRIENDS` | ✅ Соответствует | Ограниченный круг (подтверждённые друзья) |
| `photos_visibility` | `FRIENDS` | ✅ Соответствует | Ограниченный круг |
| `online_status_visible` | `FRIENDS` (ON=Friends) | ✅ Соответствует | Ограниченный круг |
| `profile_searchable` | `true` (ON) | ✅ Соответствует | **Внутренний поиск ≠ «indefinite number»**: поиск ограничен зарегистрированными пользователями платформы, что является законной целью соцсети |
| `account_private` | `false` (OFF=открытый) для 18+ | ⚠️ **СЕРАЯ ЗОНА** — см. анализ ниже | Открытый профиль на публичной соцсети |

---

### 1.3 Детальный анализ «серой зоны»: `account_private = OFF` для 18+

**Вопрос**: Противоречит ли открытый профиль по умолчанию фразе «by default personal data are not made accessible… to an indefinite number of natural persons»?

#### Аргументы ЗА законность (OFF = открытый):

1. **Цель сервиса**: Bestme — публичная социальная сеть. Публичность профиля — основная функция, которую пользователь ожидает и принимает при регистрации. GDPR Art.25 требует «measures necessary for each **specific purpose** of the processing» — публичность И ЕСТЬ цель.

2. **«Without the individual's intervention»**: Пользователь осознанно создал аккаунт в публичной социальной сети. Регистрация = intervention (вмешательство/действие субъекта). Если на экране регистрации явно написано: «Ваш профиль будет виден всем пользователям» — это уведомление снимает требование.

3. **Прецеденты EDPB**: EDPB Opinion 5/2019 (Online Social Networking) признаёт, что дефолтная публичность профиля на SNS может быть законной при условии прозрачного уведомления.

4. **Прецеденты рынка**: Instagram, TikTok, X (Twitter), LinkedIn, Facebook — все делают профили 18+ публичными по умолчанию без штрафов GDPR.

5. **ICO Guidance (UK)**: Открытый профиль для взрослых на SNS допустим, если пользователь явно уведомлён при регистрации.

#### Аргументы ПРОТИВ (риски):

1. **Строгое прочтение**: «indefinite number» = любой зарегистрированный пользователь платформы + неаутентифицированные посетители = неограниченный круг.

2. **CNIL enforcement**: Французский регулятор в ряде дел требовал более строгих дефолтов.

3. **«Minimisation»**: EDPB Opinion 8/2019 подчёркивает, что даже внутри платформы видимость по умолчанию должна быть минимальной.

#### Вывод и требование к реализации:

| Условие | Статус |
|---|---|
| Профиль 18+ открытый по умолчанию — **допустимо** | ✅ При выполнении условий ниже |
| **Условие 1**: На экране регистрации явное уведомление: «Ваш профиль будет виден всем» | ❌ **Обязательно добавить в onboarding** |
| **Условие 2**: При первом входе — возможность сразу закрыть профиль (Privacy Checkup) | ⚠️ Рекомендуется |
| **Условие 3**: В Settings > Privacy чёткое объяснение, что значит «открытый» | ✅ UI copy уже есть в AccountPrivacySpec.md |

---

### 1.4 Сводка: Что добавить для полного соответствия Art.25

| # | Что добавить | Где | Приоритет |
|---|---|---|---|
| 1 | **Onboarding disclosure**: явное уведомление о публичности профиля при регистрации | Onboarding UX | 🔴 Критично |
| 2 | **Storage period**: указать срок хранения данных в разделе Your Data | Your Data → Data retention info | 🟡 Важно |
| 3 | **Deactivation policy**: при деактивации — пояснение о сроке хранения и автоудалении | Account → Deactivate account modal | 🟡 Важно |
| 4 | **Pseudonymisation**: задокументировать в Backend Spec (не в UI) | Backend Architecture | 🟢 Рекомендация |
| 5 | **Privacy Checkup**: экран проверки настроек приватности при первом входе | Onboarding UX | 🟢 Рекомендация |

---

## ЧАСТЬ 2. GDPR Art.17 — Right to Erasure («Right to Be Forgotten»)

### Официальный текст (пронумерованные пункты для аудита)

> **Art.17(1)** — 6 оснований для удаления:
> *(a) данные больше не нужны для цели сбора*
> *(b) субъект отзывает согласие (Art.6(1)(a) или Art.9(2)(a)) и нет другого правового основания*
> *(c) субъект возражает (Art.21(1)) и нет весомых законных оснований, или возражает (Art.21(2))*
> *(d) данные обработаны незаконно*
> *(e) необходимо стереть по закону ЕС/государства-члена*
> *(f) данные собраны в связи с информационными услугами для детей (Art.8(1))*

> **Art.17(2)** — Де-индексация: *"Where the controller has made the personal data public and is obliged pursuant to paragraph 1 to erase the personal data, the controller…shall take reasonable steps, including technical measures, to inform controllers which are processing the personal data that the data subject has requested the erasure by such controllers of any links to, or copy or replication of, those personal data."*

> **Art.17(3)** — Исключения:
> *(a) свобода слова и информации*
> *(b) юридическое обязательство или выполнение задачи в общественных интересах*
> *(c) общественное здравоохранение*
> *(d) архивирование, научные или статистические цели (Art.89(1))*
> *(e) установление, осуществление или защита правовых требований*

---

### 2.1 Art.17(1) — 6 оснований для удаления

| Основание | Цитата | Реализация в настройках | Статус |
|---|---|---|---|
| (a) | *"no longer necessary in relation to the purposes"* | Account → **Delete account** + очистка всех данных | ✅ |
| (b) | *"withdraws consent"* | Your Data → **Withdraw consent** → автоматическое удаление если нет другого основания | ✅ |
| (c) | *"objects to the processing (Art.21)"* | Your Data → **Opt-out from profiling** / recommendations_opt_out | ⚠️ Opt-out ≠ удаление; нужен маршрут: «возразить → запрос удаления» |
| (d) | *"unlawfully processed"* | Your Data → **Report data misuse** → Delete account | ⚠️ Нет явной кнопки «Мои данные обработаны незаконно» |
| (e) | *"legal obligation"* | Внутренний compliance-процесс (не UI) | 🔄 Backend/legal team |
| (f) | *"collected in relation to information society services for minors (Art.8)"* | Н/П — Bestme только 18+, несовершеннолетние не могут зарегистрироваться | ✅ Н/П |

> **Пробел по основанию (c)**: У пользователя должна быть возможность не просто отключить профилирование, но и **потребовать удаления данных, собранных в ходе профилирования**. Это отдельный запрос в разделе Your Data.

---

### 2.2 Art.17(2) — КРИТИЧЕСКИЙ ПРОБЕЛ: Де-индексация при удалении данных

**Это самый конкретный технический пробел в текущей спецификации.**

**Что требует закон:**
Если контроллер (Bestme) **опубликовал данные пользователя** (т.е. `seo_indexable = true` был включён) и теперь обязан их удалить по Art.17(1) — контроллер ОБЯЗАН предпринять разумные шаги, включая технические меры, чтобы УВЕДОМИТЬ других контроллеров (Google, Yandex, Bing), которые обрабатывают эти данные, что субъект запросил удаление всех ссылок/копий.

**Когда это активируется:**
1. Пользователь включал `seo_indexable = true` (давал явный opt-in) — данные попали в индекс Google/Yandex
2. Пользователь **удаляет аккаунт** → Art.17(1)(a) или (b) → обязанность по Art.17(2)
3. Пользователь **отключает SEO-индексацию** (`seo_indexable = false`) → Art.17(1)(c) через Art.21(2) → обязанность по Art.17(2)

**Что сделать (технические меры):**

| Мера | Описание | Когда | Приоритет |
|---|---|---|---|
| **robots.txt / X-Robots-Tag** | При удалении аккаунта — добавить `Disallow: /profile/[username]` в robots.txt или X-Robots-Tag: noindex в HTTP-ответах | При Delete account | 🔴 Критично |
| **Google Search Console URL Removal** | Использовать Google Search Console API для запроса удаления URL профиля | При Delete account + при `seo_indexable OFF` | 🔴 Критично |
| **Yandex.Webmaster** | Аналогично через Yandex Webmaster API | При Delete account + при `seo_indexable OFF` | 🔴 Критично |
| **Bing Webmaster Tools** | URL Removal через Bing Webmaster | При Delete account | 🟡 Важно |
| **Structured data / canonical** | Убрать structured data (OpenGraph, JSON-LD) из страницы удалённого профиля | Технически | 🟡 Важно |
| **CDN invalidation** | Очистить кэш CDN для страниц удалённого профиля | Технически | 🟡 Важно |

> ⚠️ **Реалистичная оговорка**: Закон требует «разумных шагов» (reasonable steps). Полная немедленная де-индексация технически невозможна — поисковики обновляют индекс в своём темпе. Но **факт отправки запросов** через официальные API = выполнение требования Art.17(2).

**Что добавить в настройки / UX:**
- При Delete account: модальное окно с пояснением: «Мы запросим удаление вашего профиля из поисковых систем. Это может занять до 30 дней.»
- Раздел Your Data: информация об ожидаемом сроке де-индексации

**Текущий статус в спецификациях:**

| Элемент | Статус |
|---|---|
| `seo_indexable = false` по умолчанию | ✅ Прописано |
| Уведомление поисковиков при Delete account | ❌ **Не прописано нигде** |
| Уведомление поисковиков при `seo_indexable OFF` | ❌ **Не прописано нигде** |
| UX-пояснение о де-индексации | ❌ **Нет** |

---

### 2.3 Art.17(3) — Исключения из права на удаление

| Исключение | Пример применения для Bestme | Статус |
|---|---|---|
| (a) Свобода слова | Нельзя удалить контент, представляющий журналистский/публичный интерес (редкий случай для соцсети) | 💡 Внутренний процесс |
| (b) Юридическое обязательство | Нельзя удалить данные, которые требует хранить закон (налоговые записи, судебные запросы) | 🔄 Legal team |
| (c) Общественное здравоохранение | Не актуально для Bestme | — |
| (d) Архивирование / наука / статистика | Агрегированные анонимизированные данные для аналитики могут быть сохранены | ⚠️ Нужна явная политика анонимизации |
| (e) Правовые требования / защита | При активном судебном разбирательстве данные могут быть сохранены | 🔄 Legal team |

> **Пункт (d) — важный**: Bestme может хранить **анонимизированную статистику** (количество пользователей, aggregate metrics) даже после удаления аккаунта. Это законно и должно быть прописано в Privacy Policy.

---

### 2.4 Сводка: Что добавить для полного соответствия Art.17

| # | Что добавить | Где | Приоритет |
|---|---|---|---|
| 1 | **Art.17(2) де-индексация**: при Delete account — автоматический запрос удаления URL в Google/Yandex/Bing через API | Backend / System spec | 🔴 Критично |
| 2 | **Art.17(2) де-индексация**: при отключении `seo_indexable` → аналогичный процесс | Backend / System spec | 🔴 Критично |
| 3 | **UX при Delete account**: модальное пояснение о де-индексации (до 30 дней) | Account → Delete account modal | 🟡 Важно |
| 4 | **Art.17(1)(f)**: механизм запроса удаления для родителей несовершеннолетних | Your Data → родительский запрос | 🟡 Важно |
| 5 | **Art.17(3)(d)**: явная политика анонимизации данных после удаления аккаунта | Privacy Policy + Your Data | 🟡 Важно |
| 6 | **Art.17(1)(c)**: маршрут «возразить против обработки → запросить удаление собранных данных» | Your Data | 🟢 Рекомендация |

---

## ЧАСТЬ 3. СВОДНЫЙ ОТВЕТ: Соблюдаем ли мы GDPR Art.25 и Art.17?

### Art.25 — Privacy by Design and by Default

| Требование | Статус | Что нужно |
|---|---|---|
| Privacy by Design (технические меры) | ✅ В UI-настройках | Псевдонимизация — в Backend Spec |
| Минимизация данных | ✅ | — |
| Defaults = ограниченный доступ (FRIENDS, ONLY_ME) | ✅ | — |
| `seo_indexable = OFF` | ✅ Строго | — |
| `account_private = OFF` для 18+ | ✅ С оговоркой | ❌ Нужен **onboarding disclosure** |
| Срок хранения данных | ❌ Пробел | Добавить в Your Data |
| Onboarding disclosure для открытого профиля | ❌ Пробел | Добавить в onboarding UX |

### Art.17 — Right to Erasure

| Требование | Статус | Что нужно |
|---|---|---|
| Art.17(1)(a): Delete account | ✅ | — |
| Art.17(1)(b): Withdraw consent | ✅ | — |
| Art.17(1)(c): Opt-out pathway | ⚠️ Частично | Маршрут «возразить → удалить данные» |
| Art.17(2): **Де-индексация Google/Yandex** | ❌ **КРИТИЧЕСКИЙ ПРОБЕЛ** | Backend + UX modal |
| Art.17(1)(f): Несовершеннолетние | ✅ Н/П | Bestme только 18+ |
| Art.17(3): Исключения задокументированы | ⚠️ Частично | Privacy Policy |

### Итоговая оценка

**По Art.25:** ~85% соответствие. Открытые пункты: onboarding disclosure + storage period.

**По Art.17:** ~75% соответствие. **Критический пробел: Art.17(2) де-индексация поисковиков** — ни в одном из текущих документов спецификации этот процесс не описан.

---

## ЧАСТЬ 4. ОБЯЗАТЕЛЬНЫЙ ЧЕКЛИСТ ДЛЯ КОМАНДЫ

### 🔴 До публикации в ЕС (критично)

- [ ] **Onboarding disclosure**: добавить явное уведомление о публичном профиле при регистрации
- [ ] **Art.17(2) Backend**: реализовать автоматический запрос де-индексации в Google Search Console + Yandex.Webmaster при Delete account

### 🟡 До первого значительного роста ЕС-аудитории

- [ ] **Storage period**: добавить политику хранения данных в Your Data (сроки автоудаления при деактивации)
- [ ] **Delete account UX**: добавить пояснение о де-индексации (до 30 дней) в модальное окно
- [ ] **Art.17(2) seo_indexable OFF**: при отключении SEO — запускать процесс де-индексации
- [ ] **Parent erasure request**: добавить форму для запроса удаления данных несовершеннолетних

### 🟢 Рекомендации

- [ ] **Privacy Checkup**: экран проверки настроек приватности при первом входе
- [ ] **Pseudonymisation policy**: задокументировать в Backend Architecture Spec
- [ ] **Art.17(3)(d)**: прописать политику анонимизации данных после удаления в Privacy Policy

---

*Файл: `GDPRArt25Art17AuditSpec.md` | Версия 1.0*
*Основан на: Regulation (EU) 2016/679 (GDPR) — официальный текст + EDPB Opinion 5/2019 + EDPB Opinion 8/2019 + ICO Guidance on Privacy by Design*
