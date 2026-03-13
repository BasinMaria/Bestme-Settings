# Bestme — Settings Structure & Law Mapping
> Структура всех 9 вкладок настроек: что внутри, что по закону, что опционально.  
> Маппинг дизайнерских экранов к вкладкам.

---

## Обзор: 9 вкладок

| # | Вкладка | Что внутри (кратко) | Почему / Закон |
|---|---|---|---|
| 1️⃣ | **Account & Profile** | Avatar, bio, birthday, contact info, personal links, interests, profile switch | Identity |
| 2️⃣ | **Privacy & Visibility ⚖️** | Who sees what — profile, content, network, activity, blocking | GDPR Art.25 |
| 3️⃣ | **Security & Login ⚖️** | Password, 2FA, sessions, biometrics, Sign in with Apple | GDPR + App Store |
| 4️⃣ | **Data & Privacy ⚖️** | Download/view/delete data, GDPR all rights, CCPA, consents, app permissions | GDPR + CCPA + App Store |
| 5️⃣ | **Notifications** | Push, email, in-app, quiet hours, security alerts | CAN-SPAM / CASL |
| 6️⃣ | **Content & Blog** | Feed algorithm, post defaults, blog settings, site/page, media | Social network |
| 7️⃣ | **Business Profile 💼** | Business info, verification, analytics, monetization (IAP), tools | Business law + App Store |
| 8️⃣ | **App Preferences** | Theme, language, accessibility (required by App Store), storage | UX + App Store |
| 9️⃣ | **Help & Legal ⚖️** | Privacy Policy, ToS, Cookies, ATT framework, Google Play Data Safety | All stores + law |

---

## 1️⃣ Account & Profile — Аккаунт и профиль

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Аватар / Фото профиля | Опционально | — |
| Обложка профиля | Опционально | — |
| Полное имя | Нужно для функции | — |
| @хендл / Username | Нужно для функции | — |
| Биография / О себе | Опционально | — |
| Статус (текст / эмодзи) | Опционально | — |
| Дата рождения | **Обязательно** (верификация возраста) | ⚖️ GDPR Art.8 — 13+ / 16+ |
| Пол | Опционально (Private по умолчанию) | ⚖️ GDPR — чувствительная категория |
| Местоположение / Город | Опционально | — |
| Вебсайт / Personal links | Опционально | — |
| Интересы / Категории | Опционально | — |
| Жизненная цель | Опционально | — |
| Переключение профиля (обычный / бизнес) | Нужно для функции | — |

---

## 2️⃣ Privacy & Visibility ⚖️ — Приватность и видимость

> **Все 4 дизайнерских экрана находятся здесь ↓**

### 📌 Экран 1: Account Privacy (из дизайна)

| Пункт | Опции | По закону ⚖️ |
|---|---|---|
| Profile page | Public / Friends only / **Private** ✅ | ⚖️ GDPR Art.25 — Privacy by Default |
| Full name | Public / Friends only / **Private** ✅ | ⚖️ GDPR Art.25 |
| Avatar photo | Public / Friends only / **Private** ✅ | — |
| Cover photo | Public / Friends only / **Private** ✅ | — |
| Bio / About | Public / Friends only / **Private** ✅ | — |
| Birthday | Public / Friends only / **Private** ✅ | ⚖️ GDPR — чувствительная дата |
| Gender | Public / Friends only / **Private** ✅ | ⚖️ GDPR — чувствительная категория |
| Interests | Public / Friends only / **Private** ✅ | — |

### 📌 Экран 2: Contact Info Privacy (из дизайна)

| Пункт | Опции | По закону ⚖️ |
|---|---|---|
| Email | Friends only / **Private** ✅ (не может быть Public) | ⚖️ GDPR Art.5 — минимизация данных; **юридическое ограничение** |
| Phone | Friends only / **Private** ✅ | ⚖️ GDPR Art.5 |
| Location / City | Friends only / **Private** ✅ | ⚖️ GDPR — геоданные чувствительные |
| Address | Friends only / **Private** ✅ | ⚖️ GDPR Art.5 |
| Personal links | Public / Friends only / **Private** ✅ | — |
| Blog link | Public / Friends only / **Private** ✅ | — |
| Business link | Public / Friends only / **Private** ✅ | — |

### 📌 Экран 3: Interactions (из дизайна)

| Пункт | Опции | По закону ⚖️ |
|---|---|---|
| Who can message you | Everyone / Friends of friends / **Friends only** ✅ / Nobody | — |
| Who can tag you | Everyone / Friends of friends / **Friends only** ✅ | — |
| Who can comment on your posts | Everyone / Friends of friends / **Friends only** ✅ / Nobody | — |
| Who can share your posts | Everyone / Friends only / **Nobody** ✅ | — |
| Who can send friend requests | Everyone / **Friends of friends** ✅ | — |

### 📌 Экран 4: Content Visibility (из дизайна)

| Пункт | Опции | По закону ⚖️ |
|---|---|---|
| Default post visibility | **Public** / Friends only / Private | ⚖️ GDPR Art.25 — нужен выбор по умолчанию |
| Media gallery | Public / Friends only / **Private** ✅ | — |
| Friends list | Public / Friends only / **Private** ✅ | — |
| Categories (followed) | Public / Friends only / **Private** ✅ | — |
| Subscribed blogs | Public / Friends only / **Private** ✅ | — |
| Subscribed communities | Public / Friends only / **Private** ✅ | — |

### Остальные пункты Privacy & Visibility

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Видимость профиля (публичный / приватный) | **Обязательно** | ⚖️ GDPR Art.25 — Private by Default |
| Профиль в поиске | **Обязательно** | ⚖️ GDPR Art.17 — право на забвение |
| SEO-индексация профиля | Нужно (выкл по умолчанию) | ⚖️ GDPR |
| Активный статус (онлайн) | Опционально | — |
| Последний раз в сети | Опционально | — |
| Заблокированные аккаунты | Нужно для функции | — |
| Ограниченные / Заглушённые | Нужно для функции | — |

---

## 3️⃣ Security & Login ⚖️ — Безопасность и вход

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Изменить email | **Обязательно** | ⚖️ GDPR Art.32 |
| Изменить пароль | **Обязательно** | ⚖️ GDPR Art.32 |
| Двухфакторная аутентификация (2FA) | Настоятельно рекомендуется | ⚖️ GDPR Art.32 |
| Активные сессии / устройства | Нужно для функции | ⚖️ GDPR Art.32 |
| Журнал входов | Нужно для функции | ⚖️ GDPR Art.30 |
| Выйти со всех устройств | **Обязательно** | ⚖️ GDPR Art.32 |
| Face ID / Touch ID | Опционально | 📱 App Store — только через системный API |
| Sign in with Apple | **Обязательно** (если есть Google/FB-вход) | 📱 App Store — обязательное требование |
| Revoke third-party access (Google, FB) | **Обязательно** | ⚖️ GDPR Art.7 — право отозвать согласие |
| Оповещения безопасности (email) | **Обязательно** | ⚖️ GDPR Art.33/34 |

---

## 4️⃣ Data & Privacy ⚖️ — Данные и права

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Скачать мои данные | **Обязательно** | ⚖️ GDPR Art.20 — право на портируемость |
| Просмотреть мои данные | **Обязательно** | ⚖️ GDPR Art.15 — право доступа |
| Исправить данные | **Обязательно** | ⚖️ GDPR Art.16 — право на исправление |
| 🗑️ Удалить аккаунт | **Обязательно** | ⚖️ GDPR Art.17 — право на удаление |
| Деактивировать профиль | Опционально | — |
| Согласие на аналитику | **Обязательно** (opt-in) | ⚖️ GDPR — только с явного согласия |
| Согласие на рекламу | **Обязательно** (opt-in) | ⚖️ GDPR — только с явного согласия |
| Cookie-настройки | **Обязательно** для ЕС | ⚖️ ePrivacy / GDPR |
| Не продавать мои данные | **Обязательно** для США/CA | ⚖️ CCPA |
| Разрешения приложения (геолокация, камера, контакты) | **Обязательно** | 📱 App Store / Google Play |

---

## 5️⃣ Notifications — Уведомления

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Push-уведомления (вкл/выкл) | **Обязательно** (системный диалог iOS/Android) | 📱 App Store |
| Новые сообщения | Опционально | — |
| Лайки / Комментарии | Опционально | — |
| Новые подписчики / запросы в друзья | Опционально | — |
| Теги и упоминания | Опционально | — |
| Обновления бизнеса | Опционально (только бизнес-аккаунт) | — |
| Оповещения безопасности | **Обязательно** | ⚖️ GDPR Art.33 |
| Тихие часы | Опционально | — |
| Email-рассылка / дайджест | Нужно с opt-in | ⚖️ CAN-SPAM / CASL |
| Email-оповещения безопасности | **Обязательно** | ⚖️ GDPR Art.33/34 |
| Звук / вибрация | Опционально | — |

---

## 6️⃣ Content & Blog — Контент и блог

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Аудитория постов по умолчанию | **Обязательно** | ⚖️ GDPR Art.25 — Privacy by Default |
| Алгоритм ленты (хронологически / рекомендации) | Нужно с opt-out | ⚖️ GDPR Art.22 — право отказа от алгоритма |
| Фильтр чувствительного контента | **Обязательно** | 📱 App Store / Google Play — для 17+ |
| Разрешить репосты моих публикаций | Опционально | — |
| Настройки блога (заголовок, описание, URL) | Нужно для функции | — |
| Сайт / Страница | Нужно для функции | — |
| Медиа (качество загрузки, авто-теги) | Опционально | — |
| Геолокация в постах | Опционально (выкл по умолчанию) | ⚖️ GDPR — геоданные |
| Модерация комментариев | Нужно для функции | — |
| Заглушённые ключевые слова | Опционально | — |
| Фильтр языка контента | Опционально | — |
| Автовоспроизведение видео | Опционально | — |

---

## 7️⃣ Business Profile 💼 — Бизнес-профиль

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Создать / переключиться на бизнес-профиль | Опционально | — |
| Название и категория бизнеса | Нужно для функции | ⚖️ Торговое право |
| Юридический адрес | **Обязательно** | ⚖️ EU DSA / местное законодательство |
| Верификация бизнеса | **Обязательно** для ЕС | ⚖️ EU DSA Art.13 |
| Аналитика | Опционально | — |
| Монетизация / IAP | **Обязательно** через Apple/Google если есть | 📱 App Store / Google Play — 30% комиссия |
| Рекламные инструменты | Опционально | — |

---

## 8️⃣ App Preferences — Настройки приложения

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Тема (светлая / тёмная / авто) | Опционально | — |
| Язык / Регион / Формат даты | Нужно для функции | — |
| Доступность (VoiceOver, Dynamic Type, контрастность) | **Обязательно** | 📱 App Store — обязательное требование |
| Кэш / Управление хранилищем | Опционально | — |
| Разрешения (push, геолокация, камера, контакты) | **Обязательно** | 📱 App Store / Google Play |

---

## 9️⃣ Help & Legal ⚖️ — Помощь и правовые документы

| Пункт | Обязательно / Опционально | По закону ⚖️ |
|---|---|---|
| Центр помощи / Связь с поддержкой | Нужно для функции | — |
| Пожаловаться на нарушение / контент | **Обязательно** | ⚖️ EU DSA Art.16 |
| Политика конфиденциальности | **Обязательно** | ⚖️ GDPR + App Store + Google Play |
| Условия использования | **Обязательно** | 📱 App Store + Google Play |
| Cookie Policy | **Обязательно** для ЕС | ⚖️ ePrivacy |
| App Tracking Transparency (ATT) | **Обязательно** | 📱 Apple — с iOS 14.5 |
| Google Play Data Safety | **Обязательно** | 🔴 Google Play |
| Лицензии open-source | Нужно | 📱 App Store |
| Версия приложения | Нужно для поддержки | — |
| Оценить приложение | Опционально | — |

---

## Итого по закону — обязательные пункты

| Закон / Требование | Что обязательно реализовать |
|---|---|
| **GDPR Art.6/7** | Согласие на обработку, право отозвать |
| **GDPR Art.8** | Верификация возраста (13+ / 16+) |
| **GDPR Art.13/14** | Privacy Policy при регистрации |
| **GDPR Art.15/16** | Доступ и исправление своих данных |
| **GDPR Art.17** | Кнопка "Удалить аккаунт" |
| **GDPR Art.20** | Скачать свои данные |
| **GDPR Art.22** | Opt-out от алгоритмической ленты |
| **GDPR Art.25** | Privacy by Default (закрытый профиль по умолчанию) |
| **GDPR Art.32** | 2FA, сессии, защита данных |
| **GDPR Art.33/34** | Email при взломе аккаунта |
| **CCPA** | "Do Not Sell My Data" |
| **CAN-SPAM / CASL** | Opt-in на email + кнопка отписки |
| **ePrivacy** | Cookie-согласие |
| **EU DSA Art.13/16** | Верификация бизнеса + механизм жалоб |
| **Apple App Store** | Sign in with Apple, ATT-диалог, Accessibility, IAP через Apple |
| **Google Play** | Data Safety декларация |
