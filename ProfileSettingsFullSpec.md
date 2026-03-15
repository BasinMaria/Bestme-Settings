# Bestme — Полная структура настроек личного профиля
> **Что на первом экране → что внутри каждого раздела**
> ⚖️ = обязательно по закону (GDPR / DSA / App Store / Google Play)
> 💡 = рекомендация (UX-норма, лучшие практики)

---

## ПЕРВЫЙ ЭКРАН — Settings (главное меню)

| # | Иконка | Пункт меню (EN) | Пункт меню (RU) | ⚖️ / 💡 | Причина |
|---|---|---|---|---|---|
| 1 | 👤 | Account | Аккаунт | ⚖️ | App Store / GDPR — управление аккаунтом обязательно |
| 2 | 🔒 | Privacy & Visibility | Приватность и видимость | ⚖️ | GDPR Art.25 — Privacy by Default |
| 3 | 🛡️ | Login & Security | Вход и безопасность | ⚖️ | GDPR Art.32 — безопасность данных |
| 4 | 🔔 | Notifications | Уведомления | ⚖️ | GDPR + App Store / Google Play |
| 5 | 👥 | Friends | Друзья | 💡 | UX-норма соцсети |
| 6 | 📝 | Content | Контент | ⚖️/💡 | DSA Art.14 — GDPR Art.25 |
| 7 | 📦 | Your Data | Ваши данные | ⚖️ | GDPR Art.15–17 — право доступа и удаления |
| 8 | ♿ | Accessibility | Доступность | ⚖️ | **EAA** Directive 2019/882 (ЕС, с 28.06.2025) · **ADA** (США) · **Israel Disability Law** 5758-1998 · **AODA** (Канада) · California Unruh Act · App Store 2.5.4 · Google Play |
| 9 | ❓ | Help & Support | Помощь | ⚖️ | App Store — обязательная ссылка на поддержку |

---

## 1. 👤 ACCOUNT — Аккаунт

**Что на экране раздела:**

| Пункт | Тип | Описание | ⚖️ / 💡 | Закон |
|---|---|---|---|---|
| Profile photo | Действие | Изменить фото | 💡 | — |
| Display name | Поле | Имя, отображаемое публично | 💡 | — |
| Username / @handle | Поле | Уникальный никнейм | 💡 | — |
| Email address | Поле | Основной email | ⚖️ | GDPR — контактные данные |
| Phone number | Поле | Номер телефона | ⚖️ | GDPR — контактные данные |
| Date of birth | Поле | Дата рождения | ⚖️ | COPPA (возраст < 13) + GDPR |
| Language | Выбор | Язык интерфейса | 💡 | — |
| Country / Region | Выбор | Регион пользователя | ⚖️ | GDPR — применимое право |
| **Deactivate account** | Действие | Временная деактивация | ⚖️ | GDPR Art.17 |
| **Delete account** | Действие | Постоянное удаление | ⚖️ | GDPR Art.17 — право на удаление |

> ⚠️ **App Store / Google Play требование**: ссылка на удаление аккаунта должна быть доступна прямо из настроек. Без этого — отказ в публикации.

---

## 2. 🔒 PRIVACY & VISIBILITY — Приватность и видимость

### 2.1 Экран выбора подраздела

| Подраздел | Описание | ⚖️ / 💡 |
|---|---|---|
| Account Privacy | Кто видит профиль | ⚖️ GDPR Art.25 |
| Contact Info Privacy | Кто видит email/телефон | ⚖️ GDPR |
| Content Visibility | Кто видит посты, фото, активность | ⚖️ GDPR Art.25 |
| Interactions | Кто может писать, комментировать, отмечать | ⚖️ DSA Art.14 |
| Discoverability | Поиск, SEO, рекомендации | ⚖️ GDPR Art.17 + Art.22 |
| Blocked Accounts | Список заблокированных | ⚖️ GDPR |

---

### 2.2 Account Privacy (Приватность аккаунта)

| Настройка | variable_name | Тип | Default | ⚖️ | Закон |
|---|---|---|---|---|---|
| Profile visibility | `profile_visibility` | ENUM: Public / Friends / Private | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Show online status | `online_status_visible` | ENUM: Everyone / Friends / Nobody | `FRIENDS` | 💡 | — |
| Show last seen | `last_seen_visible` | ENUM: Everyone / Friends / Nobody | `FRIENDS` | 💡 | — |
| Show age | `birthday_visibility` | ENUM: 5 значений | `FRIENDS_AGE` | ⚖️ | COPPA + GDPR |
| Show relationship status | `relationship_visible` | ENUM: Everyone / Friends / Only me | `FRIENDS` | 💡 | — |

---

### 2.3 Contact Info Privacy (Видимость контактов)

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Who sees email | `email_visibility` | `ONLY_ME` | ⚖️ | GDPR + CAN-SPAM (нельзя PUBLIC) |
| Who sees phone | `phone_visibility` | `ONLY_ME` | ⚖️ | GDPR + TCPA (нельзя PUBLIC) |
| Who sees city | `city_visibility` | `FRIENDS` | 💡 | — |
| Who sees website | `website_visibility` | `PUBLIC` | 💡 | — |

---

### 2.4 Content Visibility (Видимость контента)

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Who sees my posts | `default_post_audience` | `FRIENDS` | ⚖️ | GDPR Art.25 Privacy by Default |
| Who sees my photos | `photos_visibility` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Who sees my friends list | `friends_list_visibility` | `FRIENDS` | 💡 | — |
| Who sees my activity | `activity_visibility` | `FRIENDS` | 💡 | — |
| Who sees my likes/reactions | `likes_visibility` | `FRIENDS` | 💡 | — |

---

### 2.5 Interactions (Взаимодействия)

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Who can send me messages | `who_can_message` | `FRIENDS` | ⚖️ | DSA Art.14 |
| Who can comment my posts | `who_can_comment` | `FRIENDS` | ⚖️ | DSA Art.14 |
| Who can react to my posts | `who_can_react` | `EVERYONE` | 💡 | — |
| Who can tag me in posts | `who_can_tag` | `FRIENDS` | ⚖️ | GDPR Art.25 |
| Tag approval required | `tag_approval_required` | `true` | ⚖️ | GDPR Art.25 |
| Comment moderation | `comment_moderation` | `OFF` | 💡 | — |

---

### 2.6 Discoverability (Обнаружимость)

| Настройка | variable_name | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Profile in search results | `profile_searchable` | `true` | ⚖️ | GDPR Art.17 — право на забвение (opt-out) |
| SEO indexing (Google) | `seo_indexable` | **`false`** | ⚖️ | GDPR Art.25 — выключен по умолчанию |
| Content recommendations | `recommendations_opt_out` | `false` (opt-in) | ⚖️ | GDPR Art.22 · DSA Art.29 · CCPA §1798.121 |
| Algorithm explanation link | `show_recommendation_info` | `true` | ⚖️ | DSA Art.27 — объяснение принципов рекомендаций |

> ⚠️ `seo_indexable` **ОБЯЗАН быть OFF по умолчанию** (GDPR Art.25 Privacy by Default)
> ⚠️ `recommendations_opt_out` = пользователь должен иметь возможность **отказаться** от рекомендаций (GDPR Art.22, DSA Art.29)
> ⚠️ `show_recommendation_info` = ссылка / поп-ап «почему мне рекомендуют этот контент» обязательна по DSA Art.27 (ЕС)

---

### 2.7 Blocked Accounts (Заблокированные)

| Элемент | Описание | ⚖️ | Закон |
|---|---|---|---|
| Список заблокированных | Все аккаунты | ⚖️ | GDPR — право не быть преследуемым |
| Разблокировать | Действие | ⚖️ | — |
| Заблокировать аккаунт | Действие | ⚖️ | — |

---

## 3. 🛡️ LOGIN & SECURITY — Вход и безопасность

| Настройка / Действие | Тип | ⚖️ | Закон |
|---|---|---|---|
| Change password | Действие | ⚖️ | GDPR Art.32 |
| Two-factor authentication (2FA) | Toggle + настройка | ⚖️ | GDPR Art.32 |
| Login methods (Google, Apple, email) | Список | ⚖️ | App Store (Sign in with Apple — обязательно) |
| Active sessions | Список устройств | ⚖️ | GDPR Art.32 |
| Terminate all other sessions | Действие | ⚖️ | GDPR Art.32 |
| Login activity log | Список | ⚖️ | GDPR |
| Trusted devices | Список | 💡 | — |

> ⚠️ **App Store требование**: если есть вход через Google/Facebook, **обязан быть Sign in with Apple**

---

## 4. 🔔 NOTIFICATIONS — Уведомления

### 4.1 Экран выбора подраздела

| Подраздел | Описание | Кол-во уведомлений |
|---|---|---|
| Account & Security | Безопасность аккаунта | 11 |
| System & Legal | Юридические уведомления | 4 |
| Content & Moderation | Контент и модерация | 4 |
| Social Activity | Социальные взаимодействия | 9 |
| Chat | Чат | 6 |
| Rewards | Награды | 3 |
| Blogs | Блоги | 5 |
| Community | Сообщества | 8 |
| Challenge | Задания | 1 |

---

### 4.2 Account & Security (⚖️ нельзя выключить)

| Key | Описание | Каналы |
|---|---|---|
| `profile_security_login_new_device` | Вход с нового устройства | Email, Push, In-app |
| `profile_security_suspicious_login_attempt` | Подозрительная попытка входа | Email, Push |
| `profile_security_password_changed` | Пароль изменён | Email, In-app |
| `profile_security_contacts_changed` | Контакты изменены | Email, In-app |
| `profile_security_suspicious_activity` | Подозрительная активность | Email, Push |
| `profile_data_export_ready` | Файл экспорта данных готов | Email, In-app |
| `profile_data_export_requested` | Запрос на скачивание данных | Email, In-app |
| `profile_account_suspended` | Аккаунт заблокирован | Email, In-app |
| `profile_account_restored` | Аккаунт восстановлен | In-app, Email |
| `profile_account_deletion_completed` | Удаление завершено | Email, In-app |
| `profile_account_deletion_requested` | Запрос на удаление принят | Email, In-app |

---

### 4.3 System & Legal (⚖️ нельзя выключить)

| Key | Описание | Каналы |
|---|---|---|
| `system_terms_updated` | Обновлены Условия использования | Email, In-app |
| `system_privacy_updated` | Обновлена Политика конфиденциальности | Email, In-app |
| `system_accessibility_updates` | Обновления, влияющие на доступность | In-app |
| `system_maintenance` | Технические уведомления | Push, In-app |

---

### 4.4 Content & Moderation (⚖️ нельзя выключить)

| Key | Описание | Каналы |
|---|---|---|
| `system_moderation_content_removed` | Контент удалён модерацией | Email, In-app |
| `system_moderation_content_rejected` | Контент не прошёл модерацию | In-app |
| `profile_complaint_received` | Жалоба на ваш контент | In-app |
| `profile_appeal_decision` | Решение по апелляции | Email, In-app |

---

### 4.5 Social Activity (💡 можно выключить)

| Key | Описание | Default | Каналы |
|---|---|---|---|
| `profile_new_post_comment` | Комментарий к посту | ✅ ON | In-app, Push |
| `profile_reply_comment` | Ответ на комментарий | ✅ ON | In-app, Push |
| `profile_reaction_post` | Реакция на пост | ✅ ON | In-app |
| `profile_reaction_comment` | Реакция на комментарий | ✅ ON | In-app |
| `user_mention_post` | Упоминание в посте | ✅ ON | In-app, Push |
| `user_mention_comment` | Упоминание в комментарии | ✅ ON | In-app |
| `profile_friend_request` | Запрос в друзья | ✅ ON | In-app, Push |
| `profile_friend_request_accepted` | Запрос принят | ✅ ON | In-app |
| `profile_post_shared` | Поделились постом | ✅ ON | In-app |

---

### 4.6 Настройка каналов доставки

На экране уведомлений должны быть 3 вкладки или переключатели:

| Канал | Описание | ⚖️ |
|---|---|---|
| **Push** | Мобильные push-уведомления | ⚖️ Требует разрешения пользователя (iOS/Android) |
| **Email** | Email-уведомления | ⚖️ Требует opt-in (CAN-SPAM / CASL) |
| **In-app** | Внутри приложения | 💡 Не требует разрешения |

> ⚠️ **iOS**: запрос на Push-уведомления — системный диалог, нельзя пропустить
> ⚠️ **Email-маркетинг**: нужен отдельный opt-in (не путать с транзакционными письмами)

---

## 5. 👥 FRIENDS — Друзья

| Настройка | Тип | Default | ⚖️ |
|---|---|---|---|
| Friend requests | Список входящих | — | 💡 |
| Who can send friend requests | ENUM: Everyone / Friends of friends / Nobody | `EVERYONE` | 💡 |
| Friend suggestions | Toggle | ON | 💡 |
| Mutual friends visibility | Toggle | ON | 💡 |

---

## 6. 📝 CONTENT — Контент

| Настройка | Описание | Default | ⚖️ | Закон |
|---|---|---|---|---|
| Default post audience | Аудитория постов по умолчанию | `FRIENDS` | ⚖️ | GDPR Art.25 Privacy by Default |
| Sensitive content filter | Фильтр чувствительного контента | ON | ⚖️ | DSA Art.14 |
| Adult content (18+) | Показывать взрослый контент | OFF | ⚖️ | App Store / GDPR (возраст) |
| Language filter | Фильтр языка | ON | 💡 | — |
| Muted words | Список заглушённых слов | — | 💡 | — |
| Comment moderation | Авто-модерация комментариев | OFF | 💡 | — |
| Auto-archive posts | Автоархивирование постов | OFF | 💡 | — |

---

## 7. 📦 YOUR DATA — Ваши данные

| Пункт | Описание | ⚖️ | Закон |
|---|---|---|---|
| **Download my data** | Скачать копию всех данных (JSON/CSV) | ⚖️ | GDPR Art.15 · PIPEDA Pr.9 · CCPA §1798.100 |
| **Request data deletion** | Удалить все данные | ⚖️ | GDPR Art.17 · Quebec L25 Art.12 · CCPA §1798.105 |
| **Data portability** | Перенос данных | ⚖️ | GDPR Art.20 · Quebec L25 Art.27 |
| **Restrict processing** | Ограничить обработку данных (не удалять, но заморозить) | ⚖️ | GDPR Art.18 |
| **View consent history** | История согласий (дата, что согласовано, версия) | ⚖️ | GDPR Art.7 · CASL · PIPEDA Pr.3 |
| **Withdraw consent** | Отозвать согласие | ⚖️ | GDPR Art.7 · CASL |
| **Do Not Sell My Personal Information** | Запрет продавать / передавать данные для рекламы | ⚖️ | CCPA/CPRA §1798.120 |
| **Ad preferences** | Рекламные предпочтения + opt-out профилирования | ⚖️ | GDPR Art.21/22 · DSA Art.29 · CCPA §1798.121 |
| **Privacy Policy** | Ссылка на политику конфиденциальности | ⚖️ | App Store · Google Play · GDPR Art.13 |
| **Terms of Use** | Ссылка на условия использования | ⚖️ | App Store · Google Play |
| **Cookie settings** | Управление cookies и трекерами | ⚖️ | GDPR / ePrivacy Art.5(3) |
| **Contact Privacy Officer** | Связаться с DPO / CPO | ⚖️ | Quebec L25 Art.5 · GDPR Art.38 |

> ⚠️ **App Store**: ссылки на Privacy Policy и Terms обязательны в настройках
> ⚠️ **GDPR**: экспорт данных и удаление аккаунта — юридическое требование
> ⚠️ **CCPA/CPRA**: кнопка «Do Not Sell My Personal Information» обязательна для аудитории Калифорнии
> ⚠️ **Google Play**: удаление аккаунта должно быть доступно также через **веб-сайт** (не только in-app)
> ⚠️ **Quebec Law 25**: контакт Privacy Officer должен быть публично виден

---

## 8. ♿ ACCESSIBILITY — Доступность

> ⚠️ **Accessibility — это не только требование магазинов, это ЗАКОН:**
> - 🇪🇺 **EAA** (European Accessibility Act, Directive 2019/882) — мобильные приложения, **вступает в силу 28 июня 2025**
> - 🇺🇸 **ADA** (Americans with Disabilities Act) + **Section 508** — применяется сейчас
> - 🇮🇱 **Israel Equal Rights for Persons with Disabilities Law** 5758-1998 + Regulations 5763-2003
> - 🇨🇦 **AODA** (Accessibility for Ontarians with Disabilities Act) + **Accessible Canada Act** 2019
> - 🇺🇸 **California Unruh Civil Rights Act** §51 — цифровая доступность
> - 📱 **App Store** Guidelines 2.5.4 · **Google Play** Accessibility guidelines

### 8.1 Текст и отображение

| Настройка | Тип | Default | ⚖️ |
|---|---|---|---|
| Text size | Слайдер (Small / Normal / Large / Extra Large) | Normal | ⚖️ |
| Bold text | Toggle | OFF | ⚖️ |
| High contrast | Toggle | OFF | ⚖️ |
| Reduce motion | Toggle | OFF | ⚖️ |
| Dark / Light mode | Выбор | System | 💡 |

### 8.2 Медиа и контент

| Настройка | Тип | Default | ⚖️ |
|---|---|---|---|
| Autoplay videos | ENUM: Always / Wi-Fi only / Never | Wi-Fi only | 💡 |
| Closed captions (CC) | Toggle | OFF | ⚖️ |
| Image descriptions (alt text) | Toggle | ON | ⚖️ |
| Screen reader optimization | Информация | — | ⚖️ |

### 8.3 Управление

| Настройка | Тип | Default | ⚖️ |
|---|---|---|---|
| Haptic feedback | Toggle | ON | 💡 |
| Sound effects | Toggle | ON | 💡 |

---

## 9. ❓ HELP & SUPPORT — Помощь

> ⚠️ **App Store / Google Play**: раздел поддержки обязателен, должна быть ссылка на контактную форму

| Пункт | Тип | ⚖️ |
|---|---|---|
| Help Center / FAQ | Ссылка | ⚖️ App Store |
| Contact support | Форма / Email | ⚖️ App Store |
| Report a problem | Форма | ⚖️ DSA Art.17 |
| Community guidelines | Ссылка | ⚖️ DSA |
| Privacy Policy | Ссылка | ⚖️ App Store |
| Terms of Use | Ссылка | ⚖️ App Store |
| Licenses / Third-party | Список | ⚖️ App Store |
| App version | Текст | ⚖️ App Store |

---

## СВОДНАЯ ТАБЛИЦА: Что обязательно для публикации

> Полный юридический анализ по всем юрисдикциям — см. `LegalComplianceSpec.md`

| Требование | Где в настройках | Закон / Правило |
|---|---|---|
| Удаление аккаунта | Account → Delete account | App Store 5.1.1 · GDPR Art.17 · CCPA §1798.105 |
| Веб-форма удаления аккаунта | Сайт / веб-версия | Google Play (обязательно отдельно от app) |
| Ссылка Privacy Policy | Your Data + Help | App Store · Google Play · GDPR Art.13 |
| Ссылка Terms of Use | Your Data + Help | App Store · Google Play |
| Sign in with Apple | Login & Security | App Store 5.1.3 (обязательно если есть Google/Facebook) |
| Push: системный запрос | Notifications | iOS App Store |
| Accessibility раздел (текст, контраст, субтитры, screen reader) | Раздел 8 | **EAA 2019/882** (ЕС, с 28.06.2025) · **ADA** (США) · **Israel Disability Law** 5758-1998 · **AODA** (Канада) · App Store 2.5.4 · Google Play |
| Форма поддержки | Help & Support | App Store |
| SEO indexing = OFF по умолчанию | Privacy → Discoverability | GDPR Art.25 · Quebec L25 Art.8 |
| Opt-out от рекомендаций | Privacy → Discoverability | GDPR Art.22 · DSA Art.29 · CCPA §1798.121 |
| Объяснение алгоритма рекомендаций | Privacy → Discoverability | DSA Art.27 (ЕС) |
| Экспорт данных | Your Data | GDPR Art.15 · PIPEDA Pr.9 · CCPA §1798.100 |
| Ограничение обработки | Your Data | GDPR Art.18 |
| «Do Not Sell My Personal Information» | Your Data | CCPA/CPRA §1798.120 (Калифорния) |
| Управление согласием (cookies) | Your Data | GDPR / ePrivacy Art.5(3) |
| Opt-out от профилирования для рекламы | Your Data → Ad preferences | DSA Art.29 · GDPR Art.21 |
| Контакт Privacy Officer | Your Data + Help | Quebec Law 25 Art.5 · GDPR Art.38 |
| Уведомления о безопасности (нельзя выключить) | Notifications → Account & Security | GDPR Art.33 · Israel PPL Sec.17C · PIPEDA |
| Уведомления о модерации (нельзя выключить) | Notifications → Content & Moderation | DSA Art.17–20 |
| Email/телефон не PUBLIC по умолчанию | Privacy → Contact Info | GDPR Art.25 · CAN-SPAM · TCPA · Israel PPL |
| 2FA доступна | Login & Security | GDPR Art.32 · Israel Data Security Regs |
| Возраст проверяется · блок < 13 | Account → Date of birth + Onboarding | COPPA · DSA Art.28 |
| Pre-checked boxes = пустые | Onboarding / Notifications | CASL · ePrivacy |

---

## ИТОГО: Структура первого экрана

```
⚙️ Settings
│
├── 1. 👤 Account                    ← управление аккаунтом + удаление
├── 2. 🔒 Privacy & Visibility       ← кто видит, SEO, рекомендации
├── 3. 🛡️ Login & Security          ← пароль, 2FA, сессии
├── 4. 🔔 Notifications              ← уведомления (76 ключей)
├── 5. 👥 Friends                    ← друзья, запросы
├── 6. 📝 Content                    ← аудитория постов, фильтры
├── 7. 📦 Your Data                  ← экспорт, удаление, GDPR права
├── 8. ♿ Accessibility              ← текст, контраст, субтитры
└── 9. ❓ Help & Support             ← поддержка, ссылки, версия
```

---

*Файл: `ProfileSettingsFullSpec.md` | Версия 2.0 | Юрисдикции: EU/EEA · Canada · Israel · California · USA · App Stores | Полный анализ → `LegalComplianceSpec.md`*
