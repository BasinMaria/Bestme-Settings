# Settings First Screen Structure / Структура первого экрана настроек
# Bestme Social App

*Date: 2026-02-17*

---

## First Screen Menu / Главное меню первого экрана

Это главный экран Settings, который видит пользователь при входе в настройки.

---

### Menu Items / Пункты меню:

```
⚙️ SETTINGS / НАСТРОЙКИ
│
├── 👤 Profile / Профиль
│   └── Edit your profile information
│       Редактировать информацию профиля
│
├── 🔒 Privacy / Приватность
│   └── Control who can see your content
│       Контролировать, кто видит ваш контент
│
├── 👥 Friends & Community / Друзья и сообщество
│   └── Manage friends and communities
│       Управление друзьями и сообществами
│
├── 🔔 Notifications / Уведомления
│   └── Manage alerts and reminders
│       Управление уведомлениями и напоминаниями
│
├── 📝 Content / Контент
│   └── Blog and saved content
│       Блог и сохраненный контент
│
├── ⚙️ Account / Аккаунт
│   └── Security and preferences
│       Безопасность и настройки
│
└── 🏢 Business Profile / Бизнес-профиль
    └── Create or switch to business
        Создать или переключиться на бизнес
```

---

## Detailed First Screen / Детальный первый экран

### Header / Шапка:
```
┌─────────────────────────────────────┐
│  [← Back]    SETTINGS / НАСТРОЙКИ   │
└─────────────────────────────────────┘
```

### Main Menu Items / Основные пункты:

#### 1. 👤 Profile / Профиль
**Icon:** User avatar or profile icon  
**Label:** Profile / Профиль  
**Subtitle:** Edit your profile information / Редактировать информацию профиля  
**Action:** Navigate to Profile settings →

---

#### 2. 🔒 Privacy / Приватность  
**Icon:** Lock icon  
**Label:** Privacy / Приватность  
**Subtitle:** Control who can see your content / Контролировать, кто видит ваш контент  
**Action:** Navigate to Privacy settings →

---

#### 3. 👥 Friends & Community / Друзья и сообщество
**Icon:** People/group icon  
**Label:** Friends & Community / Друзья и сообщество  
**Subtitle:** Manage friends and communities / Управление друзьями и сообществами  
**Badge:** 245 friends, 23 online  
**Action:** Navigate to Friends & Community settings →

---

#### 4. 🔔 Notifications / Уведомления
**Icon:** Bell icon  
**Label:** Notifications / Уведомления  
**Subtitle:** Manage alerts and reminders / Управление уведомлениями и напоминаниями  
**Badge:** 3 new (if applicable)  
**Action:** Navigate to Notifications settings →

---

#### 5. 📝 Content / Контент
**Icon:** Document/blog icon  
**Label:** Content / Контент  
**Subtitle:** Blog and saved content / Блог и сохраненный контент  
**Action:** Navigate to Content settings →

---

#### 6. ⚙️ Account / Аккаунт
**Icon:** Gear/settings icon  
**Label:** Account / Аккаунт  
**Subtitle:** Security and preferences / Безопасность и настройки  
**Action:** Navigate to Account settings →

---

#### 7. 🏢 Business Profile / Бизнес-профиль
**Icon:** Briefcase icon  
**Label:** Business Profile / Бизнес-профиль  
**Subtitle:** Create or switch to business / Создать или переключиться на бизнес  
**Note:** Only show if user doesn't have business profile  
**Action:** Navigate to Business Profile creation/switch →

---

### Bottom Section / Нижняя секция:

```
├── ℹ️ Help & Support / Помощь и поддержка
├── 📋 Terms of Service / Условия использования
└── 🔓 Log Out / Выйти
```

---

## Visual Layout / Визуальный макет

```
┌─────────────────────────────────────────┐
│  [←]        Settings / Настройки        │
├─────────────────────────────────────────┤
│                                         │
│  👤  Profile / Профиль             →   │
│      Edit your profile information      │
│                                         │
├─────────────────────────────────────────┤
│  🔒  Privacy / Приватность         →   │
│      Control who can see your content   │
│                                         │
├─────────────────────────────────────────┤
│  👥  Friends & Community           →   │
│      245 friends, 23 online             │
│                                         │
├─────────────────────────────────────────┤
│  🔔  Notifications              [3] →   │
│      Manage alerts and reminders        │
│                                         │
├─────────────────────────────────────────┤
│  📝  Content / Контент             →   │
│      Blog and saved content             │
│                                         │
├─────────────────────────────────────────┤
│  ⚙️  Account / Аккаунт             →   │
│      Security and preferences           │
│                                         │
├─────────────────────────────────────────┤
│  🏢  Business Profile              →   │
│      Create or switch to business       │
│                                         │
├─────────────────────────────────────────┤
│                                         │
│  ℹ️   Help & Support                   │
│  📋  Terms of Service                  │
│  🔓  Log Out                            │
│                                         │
└─────────────────────────────────────────┘
```

---

## Notes / Примечания:

### For Personal Profile / Для личного профиля:
- Show all 7 main menu items
- Business Profile item shows "Create Business Profile"
- Friends count shows real-time (245 friends, 23 online)
- Notification badge shows unread count

### For Business Profile / Для бизнес-профиля:
- Business Profile item shows "Switch to Personal Profile"
- Additional business-specific items may appear

### Design Considerations / Соображения дизайна:
- Each item is tappable/clickable
- Clear visual hierarchy
- Icons help quick scanning
- Subtitles provide context
- Right arrow (→) indicates navigation
- Bilingual labels for clarity

---

## Interaction Flow / Поток взаимодействия:

```
Home Screen → Settings Icon → FIRST SCREEN (this) → Specific Settings
Главный экран → Иконка настроек → ПЕРВЫЙ ЭКРАН (этот) → Конкретные настройки
```

---

---

## Detailed Structures / Детальные структуры

### 👤 Profile Structure / Структура профиля

```
👤 Profile / Профиль
│
├── Edit Profile / Редактировать профиль
│   ├── Avatar Photo / Фото профиля
│   ├── Status
│   ├── Cover Photo / Обложка
│   ├── Name (нельзя менять / cannot change)
│   ├── Last Name
│   ├── Bio / About
│   ├── Birthday / День рождения [Privacy toggle]
│   └── Gender / Пол [Privacy toggle]
│
├── Contact Info / Контактная информация
│   ├── Phone / Телефон [Privacy toggle]
│   ├── Email / Электронная почта [Privacy toggle]
│   ├── Location / Местоположение [Privacy toggle]
│   └── Address [Privacy toggle]
│
└── Interests / Интересы
    ├── Categories / Категории интересов
    └── Goals / Цели
```

**See detailed Privacy structure in:** `PRIVACY_STRUCTURE.md`

---

*This is the simple first screen structure as requested.*  
*Это простая структура первого экрана, как было запрошено.*
