# Bilingual UI Guidelines / Руководство по двуязычному UI
# English Interface + Russian Annotations

*Version: 1.0 | Date: 2026-02-17*

## Overview / Обзор

This document establishes the **bilingual design system** for the Bestme social network settings interface. All UI elements use **English** for interface text with **Russian annotations** for clarity and context.

Этот документ устанавливает **систему двуязычного дизайна** для интерфейса настроек социальной сети Bestme. Все элементы UI используют **английский** для текста интерфейса с **русскими аннотациями** для ясности и контекста.

---

## Core Principle / Основной принцип

```
English for UI = International standard, clean, professional
Russian annotations = Context, clarity, user understanding

Английский для UI = Международный стандарт, чисто, профессионально
Русские аннотации = Контекст, ясность, понимание пользователя
```

---

## Why This Approach? / Почему такой подход?

### Benefits / Преимущества:

1. **International Standards** / Международные стандарты
   - English UI aligns with global social network conventions
   - Easier for developers (English code/docs)
   - Professional appearance / Профессиональный вид

2. **User Understanding** / Понимание пользователя
   - Russian annotations provide context
   - No confusion about technical terms
   - Bridge between languages / Мост между языками

3. **Consistency** / Последовательность
   - One language for interface = visual consistency
   - One language for docs = maintenance simplicity
   - Bilingual = understanding / Двуязычный = понимание

4. **SEO & Accessibility** / SEO и доступность
   - English keywords recognized globally
   - Screen readers work better with English UI
   - Russian helps context / Русский помогает с контекстом

---

## Format Rules / Правила формата

### Standard Format / Стандартный формат:

```
English UI Text / Русское пояснение
```

### Examples / Примеры:

✅ **CORRECT:**
```
Profile / Профиль
Notifications / Уведомления
Privacy Settings / Настройки приватности
Edit Profile / Редактировать профиль
```

❌ **INCORRECT:**
```
Профиль / Profile  (Russian first - wrong!)
Profile (Профиль)  (Parentheses - inconsistent)
Profile-Профиль    (No separator)
```

---

## UI Element Guidelines / Руководство по элементам UI

### 1. Navigation Items / Элементы навигации

**Format:** English / Русский

```
Profile / Профиль
Privacy / Приватность
Notifications / Уведомления
Account / Аккаунт
Content & Interactions / Контент и взаимодействия
```

**Why:** Navigation needs to be scannable / Навигация должна быстро считываться

---

### 2. Section Headers / Заголовки разделов

**Format:** English
**Subtext:** (Русское пояснение)

```
Edit Profile
(Редактировать профиль)

Login & Security
(Вход и безопасность)

Privacy Settings
(Настройки приватности)
```

**Why:** Headers are larger, annotations work as subtitles

---

### 3. Field Labels / Метки полей

**Format:** English / Русский

```
Profile Photo / Фото профиля
Cover Photo / Обложка
Username / Имя пользователя
Bio / О себе
Birthday / День рождения
Location / Местоположение
```

**Why:** Fields need immediate clarity / Поля нужны с немедленной ясностью

---

### 4. Buttons / Кнопки

**Format:** English only (no space for annotations)

```
Save
Edit
Cancel
Delete
Share
Send
```

**Russian in tooltip/hover:**
```
Save (hover: Сохранить)
Delete (hover: Удалить)
```

**Why:** Buttons are small, tooltips provide translation

---

### 5. Toggles & Switches / Переключатели

**Format:** English / Русский

```
Show activity status / Показывать статус активности
Dark mode / Темная тема
Push notifications / Push-уведомления
```

**Why:** Toggles have space, need clarity

---

### 6. Dropdown Options / Опции выпадающего меню

**Format:** English / Русский (stacked in dropdown)

```
Public / Всем
Friends / Друзьям
Only Me / Только мне
```

**Why:** Dropdowns can accommodate both

---

### 7. Helper Text / Вспомогательный текст

**Format:** English (primary) with Russian (secondary)

```
Who can see your posts?
(Кто может видеть ваши посты?)

Choose who can tag you in photos
(Выберите, кто может отмечать вас на фото)
```

**Why:** Explanations need both for full understanding

---

### 8. Error Messages / Сообщения об ошибках

**Format:** English / Русский

```
Invalid email address / Неверный адрес электронной почты
Password must be 8+ characters / Пароль должен быть 8+ символов
Username already taken / Имя пользователя уже занято
```

**Why:** Errors need to be absolutely clear

---

## Typography Guidelines / Руководство по типографике

### Font Sizes / Размеры шрифта:

```
English text:    16px (base)
Russian text:    14px (annotation)
Section headers: 20px English, 16px Russian subtext
```

### Font Weights / Толщина шрифта:

```
English:  Medium (500) or Semi-Bold (600)
Russian:  Regular (400) or Medium (500)
```

### Colors / Цвета:

```
English:  Primary text color (#1A1A1A)
Russian:  Secondary text color (#666666)
```

**Why:** Visual hierarchy shows primary vs secondary information

---

## Layout Patterns / Паттерны макета

### Pattern 1: Inline (Most Common) / В линию (чаще всего)

```
┌─────────────────────────────────┐
│ Profile / Профиль               │
├─────────────────────────────────┤
│ Privacy / Приватность           │
├─────────────────────────────────┤
│ Notifications / Уведомления     │
└─────────────────────────────────┘
```

**Use for:** Navigation, lists, menu items

---

### Pattern 2: Stacked (Section Headers) / Стопкой (заголовки)

```
┌─────────────────────────────────┐
│ Edit Profile                    │
│ (Редактировать профиль)         │
│                                 │
│ Profile Photo / Фото профиля    │
│ Cover Photo / Обложка           │
└─────────────────────────────────┘
```

**Use for:** Section titles with fields below

---

### Pattern 3: Side-by-Side (Forms) / Рядом (формы)

```
┌─────────────────────────────────┐
│ Username          Bio            │
│ Имя пользователя  О себе        │
│ [___________]     [___________] │
└─────────────────────────────────┘
```

**Use for:** Form labels above inputs

---

### Pattern 4: Tooltip (Buttons) / Подсказка (кнопки)

```
┌─────────┐
│  Save   │  ← Hover shows "Сохранить"
└─────────┘
```

**Use for:** Buttons, icons

---

## Naming Conventions / Соглашения об именовании

### DO / ДЕЛАТЬ:

✅ Use common English social network terms
```
Profile, Feed, Stories, Posts, Likes, Comments, Share
```

✅ Keep English concise (1-2 words max)
```
"Edit Profile" not "Edit Your Personal Profile"
```

✅ Use Russian for full context
```
Edit Profile / Редактировать публичный профиль
```

✅ Match industry standards
```
"Notifications" (not "Alerts") / "Уведомления" (not "Оповещения")
```

### DON'T / НЕ ДЕЛАТЬ:

❌ Don't invent new English terms
```
Bad: "Post Maker" → Use: "Create Post"
```

❌ Don't use abbreviations without explanation
```
Bad: "2FA" → Use: "Two-Factor Authentication / Двухфакторная аутентификация"
```

❌ Don't mix languages in one element
```
Bad: "Редактировать Profile"
```

❌ Don't translate English brand terms
```
Keep: "Stories" not "Истории" (Stories is a product name)
```

---

## Privacy Level Naming / Названия уровней приватности

### Standard 3-Level Privacy / Стандартная 3-уровневая приватность:

```
Public / Всем
├─ Everyone can see / Видно всем
├─ Icon: 🌍
└─ Description: Visible to everyone on Bestme

Friends / Друзьям  
├─ Only your friends can see / Видно только друзьям
├─ Icon: 👥
└─ Description: Only people you follow back

Only Me / Только мне
├─ Only you can see / Видно только вам
├─ Icon: 🔒
└─ Description: Private, visible only to you
```

**Why these names:**
- Short, clear, universal / Короткие, ясные, универсальные
- Match other social networks / Совпадают с другими соцсетями
- Icon + text for clarity / Иконка + текст для ясности

---

## Category Naming / Названия категорий

### v2.0 Category Names / Названия категорий v2.0:

```
📱 Profile / Профиль
   (Your public profile and personal information)
   (Ваш публичный профиль и личная информация)

🔒 Privacy / Приватность
   (Control who can see your content)
   (Контролируйте, кто видит ваш контент)

🔔 Notifications / Уведомления
   (Manage alerts and updates)
   (Управление уведомлениями и обновлениями)

⚙️ Account / Аккаунт
   (Login, security, and preferences)
   (Вход, безопасность и настройки)

💬 Content & Interactions / Контент и взаимодействия
   (Posts, stories, and saved content)
   (Посты, истории и сохраненное)
```

**Icon Usage:**
- Icon + English name = primary
- Russian below = secondary context
- Icons help visual scanning / Иконки помогают визуальному сканированию

---

## Field Naming Reference / Справочник названий полей

### Profile Fields / Поля профиля:

| English | Russian | Notes |
|---------|---------|-------|
| Profile Photo | Фото профиля | Your main photo |
| Cover Photo | Обложка | Banner image |
| Username | Имя пользователя | @username |
| Display Name | Отображаемое имя | Full name |
| Bio | О себе | Short description |
| Website | Веб-сайт | Personal URL |
| Birthday | День рождения | Date of birth |
| Gender | Пол | Optional field |
| Location | Местоположение | City, Country |

### Privacy Fields / Поля приватности:

| English | Russian | Notes |
|---------|---------|-------|
| Account Privacy | Приватность аккаунта | Public/Private toggle |
| Who can see your profile | Кто видит профиль | Visibility setting |
| Who can see your posts | Кто видит посты | Post visibility |
| Who can message you | Кто может писать | Messaging permissions |
| Who can tag you | Кто может отмечать | Tagging permissions |
| Activity Status | Статус активности | Online indicator |
| Blocked Accounts | Заблокированные | Block list |

### Notification Fields / Поля уведомлений:

| English | Russian | Notes |
|---------|---------|-------|
| Push Notifications | Push-уведомления | Mobile alerts |
| Email Notifications | Email-уведомления | Email alerts |
| Likes and Reactions | Лайки и реакции | Engagement alerts |
| Comments | Комментарии | Comment alerts |
| New Followers | Новые подписчики | Follower alerts |
| Messages | Сообщения | Message alerts |
| Mentions | Упоминания | @mention alerts |

### Account Fields / Поля аккаунта:

| English | Russian | Notes |
|---------|---------|-------|
| Change Password | Изменить пароль | Security |
| Two-Factor Authentication | Двухфакторная аутентификация | 2FA |
| Active Sessions | Активные сессии | Login sessions |
| Login Activity | История входов | Login history |
| Language | Язык | App language |
| Theme | Тема | Light/Dark |
| Download Your Data | Скачать данные | Data export |
| Delete Account | Удалить аккаунт | Account deletion |

---

## Documentation Standards / Стандарты документации

### File Names / Названия файлов:

```
✅ English only, no Russian:
- STRUCTURE_GUIDE.md (not СТРУКТУРА.md)
- README.md (not ПРОЧИТАЙ_МЕНЯ.md)

✅ Use underscores:
- ANALYSIS_V1_TO_V2.md (not ANALYSIS-V1-TO-V2.md)
```

### Headers in Docs / Заголовки в документах:

```
✅ Bilingual headers:
# Settings Structure / Структура настроек

✅ Section headers:
## Profile Category / Категория профиль
```

### Code Comments / Комментарии в коде:

```javascript
// English only in code
// Profile photo upload handler
function uploadProfilePhoto() {
  // Implementation
}

/* Russian in documentation:
 * Profile Photo / Фото профиля
 * Upload and crop user profile photo
 * Загрузка и обрезка фото профиля пользователя
 */
```

---

## Testing Checklist / Контрольный список тестирования

When implementing bilingual UI, verify:

- [ ] All English UI text is clear and concise / Весь английский текст UI ясен и лаконичен
- [ ] All Russian annotations are accurate / Все русские аннотации точны
- [ ] Format is consistent (English / Русский) / Формат последователен
- [ ] Russian text doesn't overflow on small screens / Русский текст не переполняет на маленьких экранах
- [ ] Tooltips work for buttons / Подсказки работают для кнопок
- [ ] Icons support text where needed / Иконки поддерживают текст где нужно
- [ ] Visual hierarchy is clear (English primary) / Визуальная иерархия ясна
- [ ] Both languages are readable / Оба языка читаемы
- [ ] No text is cut off / Текст не обрезается
- [ ] Consistent across all pages / Последовательно на всех страницах

---

## Examples / Примеры

### Example 1: Navigation Menu / Меню навигации

```
┌─────────────────────────────────┐
│ ⚙️ Settings / Настройки         │
├─────────────────────────────────┤
│ 📱 Profile / Профиль            │
│ 🔒 Privacy / Приватность        │
│ 🔔 Notifications / Уведомления  │
│ ⚙️ Account / Аккаунт            │
│ 💬 Content / Контент            │
└─────────────────────────────────┘
```

### Example 2: Profile Edit Form / Форма редактирования профиля

```
┌─────────────────────────────────────────┐
│ Edit Profile                            │
│ (Редактировать профиль)                 │
├─────────────────────────────────────────┤
│                                         │
│ Profile Photo / Фото профиля            │
│ [   Change Photo   ]                    │
│                                         │
│ Username / Имя пользователя             │
│ [@username_________]                    │
│                                         │
│ Bio / О себе                            │
│ [____________________________]          │
│                                         │
│ Website / Веб-сайт                      │
│ [https://_________________]             │
│                                         │
│ [Save] [Cancel]                         │
└─────────────────────────────────────────┘
```

### Example 3: Privacy Settings / Настройки приватности

```
┌─────────────────────────────────────────┐
│ Privacy Settings                        │
│ (Настройки приватности)                 │
├─────────────────────────────────────────┤
│                                         │
│ Account Privacy / Приватность аккаунта  │
│ ○ Public / Публичный                    │
│ ● Private / Приватный                   │
│                                         │
│ Who can see your posts?                 │
│ (Кто может видеть ваши посты?)          │
│ [Friends / Друзья ▾]                    │
│                                         │
│ Who can message you?                    │
│ (Кто может вам писать?)                 │
│ [Everyone / Все ▾]                      │
│                                         │
└─────────────────────────────────────────┘
```

---

## Version History / История версий

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-02-17 | Initial bilingual guidelines / Первая версия двуязычных правил |

---

## Questions? / Вопросы?

If something is unclear, **always ask** before implementing:
Если что-то непонятно, **всегда спрашивайте** перед реализацией:

1. Is the English term correct? / Правильный ли английский термин?
2. Is the Russian translation accurate? / Точен ли русский перевод?
3. Does it match social network standards? / Соответствует ли стандартам соцсетей?
4. Is it clear to users? / Понятно ли пользователям?

---

*Document maintained by: Design Team*
*Last updated: 2026-02-17*
