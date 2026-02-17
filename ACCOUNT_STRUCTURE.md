# ⚙️ Account / Аккаунт

## Overview / Обзор

This document describes the complete structure of the Account settings section in Bestme.

Этот документ описывает полную структуру раздела настроек Аккаунта в Bestme.

---

## Structure / Структура

```
⚙️ Account / Аккаунт
│
├── Login & Security / Вход и безопасность
│   ├── Change Password / Изменить пароль
│   │   └── Update your login password
│   │       Обновить пароль для входа
│   │
│   ├── Two-Factor Authentication / Двухфакторная аутентификация
│   │   ├── Enable 2FA for extra security
│   │   │   Включить 2FA для дополнительной защиты
│   │   └── [Setup 2FA] / [Настроить 2FA]
│   │
│   ├── Active Sessions / Активные сессии
│   │   └── See devices where you're logged in
│   │       Устройства, на которых вы вошли в систему
│   │       [View sessions] / [Просмотреть сессии]
│   │
│   ├── Login Activity / История входов
│   │   └── Recent login attempts and locations
│   │       Недавние попытки входа и местоположения
│   │       [View activity] / [Просмотреть активность]
│   │
│   └── Authorized Apps / Авторизованные приложения
│       └── Third-party apps with access to your account
│           Сторонние приложения с доступом к аккаунту
│           [Manage apps] / [Управлять приложениями]
│
├── App Preferences / Настройки приложения
│   ├── Language / Язык
│   │   └── Choose your display language
│   │       Выберите язык отображения
│   │       [English / Русский / Other]
│   │
│   ├── Theme / Тема
│   │   ├── ○ Light Mode / Светлая тема
│   │   ├── ● Dark Mode / Темная тема
│   │   └── ○ Auto (System) / Авто (системная)
│   │
│   ├── Accessibility / Доступность
│   │   ├── Larger Text / Увеличенный текст
│   │   │   [Toggle ON/OFF] / [Вкл/Выкл]
│   │   │
│   │   ├── High Contrast / Высокий контраст
│   │   │   [Toggle ON/OFF] / [Вкл/Выкл]
│   │   │
│   │   └── Reduce Motion / Уменьшить анимацию
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Data Saver / Экономия трафика
│       └── Reduce data usage on mobile
│           Снизить расход данных на мобильном
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
├── Data Management / Управление данными
│   ├── Download Your Data / Скачать ваши данные
│   │   └── Request a copy of your posts, photos, and information
│   │       Запросить копию постов, фото и информации
│   │       [Request download] / [Запросить скачивание]
│   │
│   ├── Data Permissions / Разрешения на данные
│   │   └── Manage what data you've shared with Bestme
│   │       Управлять данными, которыми поделились с Bestme
│   │       [View permissions] / [Просмотреть разрешения]
│   │
│   ├── Account Status / Статус аккаунта
│   │   ├── Deactivate Account / Деактивировать аккаунт
│   │   │   └── Temporarily disable your account
│   │   │       Временно отключить аккаунт
│   │   │
│   │   └── Delete Account / Удалить аккаунт
│   │       └── Permanently remove your account and data
│   │           Навсегда удалить аккаунт и данные
│   │           [Delete permanently] / [Удалить навсегда]
│   │
│   └── Help & Support / Помощь и поддержка
│       ├── Help Center / Центр помощи
│       ├── Report a Problem / Сообщить о проблеме
│       └── Terms & Privacy Policy / Условия и политика конфиденциальности
│
├── Business Account / Бизнес-аккаунт
│   ├── Switch to Business Account / Переключиться на бизнес-аккаунт
│   │   └── Toggle between Personal and Business profiles
│   │       Переключение между личным и бизнес профилями
│   │       [Switch account] / [Переключить аккаунт]
│   │       Condition: Shows only if business account exists
│   │       Условие: Показывается только если бизнес-аккаунт существует
│   │
│   └── Create Business Account / Создать бизнес-аккаунт
│       └── Set up a business profile for your brand
│           Создать бизнес-профиль для вашего бренда
│           [Create business account] / [Создать бизнес-аккаунт]
│           Condition: Shows only if no business account exists
│           Условие: Показывается только если бизнес-аккаунта нет
│
└── Log Out / Выйти
    └── Sign out of your account
        Выйти из аккаунта
        Options / Опции:
        • Log out everywhere / Выйти везде (all devices)
        • Log out this device / Выйти с этого устройства
        [Log out] / [Выйти]
```

---

## Detailed Breakdown / Детальное описание

### 1. Login & Security / Вход и безопасность

**Location:** First section in Account  
**Расположение:** Первая секция в Аккаунте

**5 Security Features / 5 функций безопасности:**

#### 1.1 Change Password / Изменить пароль
- **Description:** Update your login password
- **Описание:** Обновить пароль для входа
- **Action:** Opens password change form
- **Действие:** Открывает форму изменения пароля

#### 1.2 Two-Factor Authentication / Двухфакторная аутентификация
- **Description:** Enable 2FA for extra security
- **Описание:** Включить 2FA для дополнительной защиты
- **Action:** [Setup 2FA] button
- **Действие:** Кнопка [Настроить 2FA]
- **Methods:** SMS, Authenticator app, Email
- **Методы:** SMS, Приложение-аутентификатор, Email

#### 1.3 Active Sessions / Активные сессии
- **Description:** See devices where you're logged in
- **Описание:** Устройства, на которых вы вошли в систему
- **Action:** [View sessions] - Shows list of devices
- **Действие:** [Просмотреть сессии] - Показывает список устройств
- **Info shown:** Device type, location, last active time
- **Показывает:** Тип устройства, местоположение, время последней активности

#### 1.4 Login Activity / История входов
- **Description:** Recent login attempts and locations
- **Описание:** Недавние попытки входа и местоположения
- **Action:** [View activity] - Shows login history
- **Действие:** [Просмотреть активность] - Показывает историю входов
- **Info shown:** Date, time, location, device, IP address
- **Показывает:** Дата, время, местоположение, устройство, IP адрес

#### 1.5 Authorized Apps / Авторизованные приложения
- **Description:** Third-party apps with access to your account
- **Описание:** Сторонние приложения с доступом к аккаунту
- **Action:** [Manage apps] - List of connected apps
- **Действие:** [Управлять приложениями] - Список подключенных приложений
- **Can:** Revoke access to any app
- **Можно:** Отозвать доступ любого приложения

---

### 2. App Preferences / Настройки приложения

**Location:** Second section in Account  
**Расположение:** Вторая секция в Аккаунте

**4 Preference Categories / 4 категории настроек:**

#### 2.1 Language / Язык
- **Description:** Choose your display language
- **Описание:** Выберите язык отображения
- **Options:** 
  - English
  - Русский
  - Other languages
- **Default:** Based on device/system settings
- **По умолчанию:** На основе настроек устройства/системы

#### 2.2 Theme / Тема
- **Description:** Choose app appearance
- **Описание:** Выберите внешний вид приложения
- **3 Options / 3 опции:**
  - ○ Light Mode / Светлая тема
  - ● Dark Mode / Темная тема (example selection)
  - ○ Auto (System) / Авто (системная)
- **Default:** Auto (follows system settings)
- **По умолчанию:** Авто (следует системным настройкам)

#### 2.3 Accessibility / Доступность
- **Description:** Features to improve app accessibility
- **Описание:** Функции для улучшения доступности приложения

**3 Accessibility Options / 3 опции доступности:**

1. **Larger Text / Увеличенный текст**
   - Increases text size throughout the app
   - Увеличивает размер текста во всем приложении
   - Control: Toggle ON/OFF

2. **High Contrast / Высокий контраст**
   - Enhances color contrast for better visibility
   - Усиливает цветовой контраст для лучшей видимости
   - Control: Toggle ON/OFF

3. **Reduce Motion / Уменьшить анимацию**
   - Reduces animations and transitions
   - Уменьшает анимации и переходы
   - Control: Toggle ON/OFF

#### 2.4 Data Saver / Экономия трафика
- **Description:** Reduce data usage on mobile
- **Описание:** Снизить расход данных на мобильном
- **Control:** Toggle ON/OFF
- **Effect:** Reduces image quality, disables auto-play
- **Эффект:** Снижает качество изображений, отключает авто-воспроизведение

---

### 3. Data Management / Управление данными

**Location:** Third section in Account  
**Расположение:** Третья секция в Аккаунте

**4 Data Management Features / 4 функции управления данными:**

#### 3.1 Download Your Data / Скачать ваши данные
- **Description:** Request a copy of your posts, photos, and information
- **Описание:** Запросить копию постов, фото и информации
- **Action:** [Request download] button
- **Действие:** Кнопка [Запросить скачивание]
- **Legal:** GDPR Article 15 - Right to data portability
- **Юридически:** GDPR Статья 15 - Право на переносимость данных
- **Process:** Request → Processing (24-48h) → Email with download link
- **Процесс:** Запрос → Обработка (24-48ч) → Email со ссылкой на скачивание

#### 3.2 Data Permissions / Разрешения на данные
- **Description:** Manage what data you've shared with Bestme
- **Описание:** Управлять данными, которыми поделились с Bestme
- **Action:** [View permissions] - Opens permissions list
- **Действие:** [Просмотреть разрешения] - Открывает список разрешений
- **Includes:** Camera, Photos, Location, Contacts, Microphone, Notifications
- **Включает:** Камера, Фото, Местоположение, Контакты, Микрофон, Уведомления

#### 3.3 Account Status / Статус аккаунта
- **Description:** Manage your account status
- **Описание:** Управление статусом аккаунта

**2 Options / 2 опции:**

1. **Deactivate Account / Деактивировать аккаунт**
   - Description: Temporarily disable your account
   - Описание: Временно отключить аккаунт
   - Effect: Account hidden, can reactivate anytime
   - Эффект: Аккаунт скрыт, можно восстановить в любое время
   - Data: Preserved / Сохранены

2. **Delete Account / Удалить аккаунт**
   - Description: Permanently remove your account and data
   - Описание: Навсегда удалить аккаунт и данные
   - Action: [Delete permanently]
   - Действие: [Удалить навсегда]
   - Effect: Irreversible, all data deleted after 30 days
   - Эффект: Необратимо, все данные удалены через 30 дней
   - Legal: GDPR Article 17 - Right to be forgotten
   - Юридически: GDPR Статья 17 - Право быть забытым

#### 3.4 Help & Support / Помощь и поддержка
- **Description:** Get help and support
- **Описание:** Получить помощь и поддержку

**3 Support Options / 3 опции поддержки:**

1. **Help Center / Центр помощи**
   - Opens help articles and FAQs
   - Открывает справочные статьи и FAQ

2. **Report a Problem / Сообщить о проблеме**
   - Submit bug reports or issues
   - Отправить отчеты об ошибках или проблемах

3. **Terms & Privacy Policy / Условия и политика конфиденциальности**
   - View legal documents
   - Просмотр юридических документов
   - Includes: Terms of Service, Privacy Policy, Community Guidelines
   - Включает: Условия использования, Политика конфиденциальности, Правила сообщества

---

### 4. Business Account / Бизнес-аккаунт

**Location:** Fourth section in Account (before Log Out)  
**Расположение:** Четвертая секция в Аккаунте (перед Выйти)

**2 Business Account Features / 2 функции бизнес-аккаунта:**

#### 4.1 Switch to Business Account / Переключиться на бизнес-аккаунт
- **Description:** Toggle between Personal and Business profiles
- **Описание:** Переключение между личным и бизнес профилями
- **Variable:** `switch_to_business_account`
- **Default:** N/A (action button)
- **Action:** [Switch account] button
- **Действие:** Кнопка [Переключить аккаунт]
- **Condition:** Shows only if business account already exists
- **Условие:** Показывается только если бизнес-аккаунт существует
- **Effect:** Switches active profile without logging out
- **Эффект:** Переключает активный профиль без выхода

#### 4.2 Create Business Account / Создать бизнес-аккаунт
- **Description:** Set up a business profile for your brand
- **Описание:** Создать бизнес-профиль для вашего бренда
- **Variable:** `create_business_account_action`
- **Default:** N/A (action button)
- **Action:** [Create business account] button
- **Действие:** Кнопка [Создать бизнес-аккаунт]
- **Condition:** Shows only if no business account exists yet
- **Условие:** Показывается только если бизнес-аккаунта нет
- **Required Information / Требуется:**
  - Business name / Название бизнеса
  - Business category / Категория бизнеса
  - Contact information / Контактная информация
  - Business verification (optional) / Верификация бизнеса (опционально)
- **Legal:** GDPR Article 6 - Business ownership = personal data
- **Юридически:** GDPR Статья 6 - Владение бизнесом = личные данные
- **Note:** Can have both Personal and Business accounts
- **Примечание:** Можно иметь и личный, и бизнес аккаунт

---

### 5. Log Out / Выйти

**Location:** Last item in Account (at very bottom)  
**Расположение:** Последний пункт в Аккаунте (в самом низу)

#### Log Out from Account / Выйти из аккаунта
- **Description:** Sign out of your account
- **Описание:** Выйти из аккаунта
- **Variable:** `logout_action`
- **Default:** N/A (action button)
- **Action:** [Log out] button
- **Действие:** Кнопка [Выйти]
- **2 Options / 2 опции:**
  1. **Log out everywhere / Выйти везде**
     - Signs out from all devices
     - Выход со всех устройств
     - Requires re-login on all devices
     - Требует повторного входа на всех устройствах
  
  2. **Log out this device / Выйти с этого устройства**
     - Signs out only from current device
     - Выход только с этого устройства
     - Other sessions remain active
     - Другие сессии остаются активными

- **Confirmation:** Required before logout
- **Подтверждение:** Требуется перед выходом
- **Warning:** "Unsaved changes will be lost"
- **Предупреждение:** "Несохраненные изменения будут потеряны"
- **Effect:** Returns to login/welcome screen
- **Эффект:** Возвращает на экран входа/приветствия

---

## User Flow / Пользовательский процесс

**From Settings First Screen:**

```
Settings / Настройки
  ↓ [Tap / Нажать]
⚙️ Account / Аккаунт
  ↓ [Opens / Открывается]
Account Screen with 3 sections:
  1. Login & Security
  2. App Preferences
  3. Data Management
```

**Example Navigation:**

```
Settings → Account → Login & Security → Two-Factor Authentication → [Setup 2FA]
Настройки → Аккаунт → Вход и безопасность → Двухфакторная аутентификация → [Настроить 2FA]
```

---

## Security & Legal Compliance / Безопасность и соответствие законам

### GDPR Compliance / Соответствие GDPR:
- ✅ **Article 15:** Right to data access (Download Your Data)
- ✅ **Article 17:** Right to be forgotten (Delete Account)
- ✅ **Article 20:** Right to data portability (Download Your Data)

### USA Compliance / Соответствие США:
- ✅ **COPPA:** Age verification, parental controls
- ✅ **CCPA:** Data download, deletion rights (California)

### Canada Compliance / Соответствие Канады:
- ✅ **PIPEDA:** Data access and deletion rights

---

## Summary / Итого

**Total Settings:**
- **5 main sections** / **5 основных секций**
- **5 security features** / **5 функций безопасности**
- **4 preference categories** / **4 категории настроек**
- **4 data management features** / **4 функции управления данными**
- **2 business account features** / **2 функции бизнес-аккаунта**
- **1 logout action** / **1 действие выхода**

**Total: 17 account management settings**  
**Всего: 17 настроек управления аккаунтом**

**Key Features / Ключевые функции:**
- 🔐 Security: Password, 2FA, Sessions, Login history, Authorized apps
- 🎨 Preferences: Language, Theme (3 modes), Accessibility (3 options), Data saver
- 📊 Data: Download, Permissions, Account status (Deactivate/Delete)
- 🏢 Business: Switch/Create business account
- 🚪 Log Out: Everywhere or this device
- 💬 Support: Help center, Report problem, Terms/Privacy
