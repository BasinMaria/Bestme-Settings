# Business Account Creation Flow / Флоу создания бизнес-аккаунта

## Overview / Обзор

Этот документ описывает полный процесс создания бизнес-аккаунта в Bestme, включая объяснение Business Type Badge и пошаговый флоу с четким определением главной и вторичной информации.

---

## 1. Business Type Badge / Бейдж типа бизнеса

### Что это такое / What It Is

**Business Type Badge** — это визуальный индикатор типа бизнеса, который отображается в шапке бизнес-профиля.

**Visual Indicator:** Small badge with icon + text
**Визуальный индикатор:** Небольшой бейдж с иконкой + текстом

### Примеры / Examples:

- 🎯 **Specialist** / Специалист
- 📍 **Place** / Место
- 🎓 **Education** / Образование
- 🔧 **Services** / Сервисы
- 🛍️ **Products** / Товары
- ✈️ **Activities** / Активности
- 💼 **B2B** / B2B

### Где показывается / Where It Appears

```
┌────────────────────────────────────────┐
│  [Avatar]  Business Name              │
│            🎯 Specialist              │ ← Badge here!
│  [Book] [Contact] [Schedule]         │
│                                        │
│  Description...                        │
└────────────────────────────────────────┘
```

**Location / Расположение:**
- В шапке (header) бизнес-профиля
- Прямо под названием бизнеса
- Рядом с аватаром

**Visibility / Видимость:**
- Видно всем посетителям профиля
- На всех устройствах (desktop, mobile, tablet)
- В превью профиля (если показывается в списках)

### Когда появляется / When It Appears

**ВАЖНО / IMPORTANT:**

Бейдж появляется **ПОСЛЕ** создания и публикации профиля, НЕ во время процесса создания.

**When badge appears / Когда бейдж появляется:**
- ✅ После завершения Step 6 (Review & Publish)
- ✅ Когда профиль опубликован и стал публичным
- ✅ В готовом бизнес-профиле

**When badge does NOT appear / Когда бейдж НЕ появляется:**
- ❌ Во время процесса создания (Steps 1-6)
- ❌ В черновике профиля
- ❌ В личном профиле пользователя

### Что делает / What It Does

**Purpose / Назначение:**

1. **Quick Category Recognition / Быстрое распознавание категории**
   - Пользователь сразу понимает тип бизнеса
   - Не нужно читать описание

2. **Sets Expectations / Устанавливает ожидания**
   - Specialist → можно записаться
   - Place → можно посетить
   - Products → можно купить
   - Education → можно записаться на курс

3. **Visual Differentiation / Визуальное различие**
   - Помогает отличить разные типы бизнеса
   - Делает профили более читаемыми
   - Улучшает навигацию по платформе

4. **Brand Identity / Идентичность бренда**
   - Подчеркивает специализацию
   - Помогает в категоризации
   - Упрощает поиск нужного типа бизнеса

### Техническая реализация / Technical Implementation

**Variable:** `business_type_badge`  
**Type:** String (one of 7 values)  
**Values:**
- `"specialist"`
- `"place"`
- `"education"`
- `"services"`
- `"products"`
- `"activities"`
- `"b2b"`

**Display Logic:**
```javascript
if (businessProfile.isPublished && businessProfile.businessType) {
  showBadge(businessProfile.businessType);
}
```

---

## 2. Complete Creation Flow / Полный флоу создания

### Flow Overview / Обзор флоу

```
Entry Point → Introduction → Business Type Selection → 
Primary Info → Identity Info → Review & Publish → ✅ Live Profile
```

**Total Steps / Всего шагов:** 6  
**Estimated Time / Примерное время:** 5-10 минут  
**Can Save Draft / Можно сохранить черновик:** Да, на любом шаге

---

### Step 1: Entry Point / Точка входа

**Where / Откуда:**

Personal Account → Settings / Настройки → Account / Аккаунт → Business Account section

**What User Sees / Что видит пользователь:**

```
┌─────────────────────────────────────────┐
│  Business Account / Бизнес-аккаунт     │
│                                         │
│  Create Business Account               │
│  Создать бизнес-аккаунт                │
│                                         │
│  [Create / Создать]  ←──── Button      │
└─────────────────────────────────────────┘
```

**Button Label:**
- English: "Create Business Account"
- Russian: "Создать бизнес-аккаунт"

**Action:** Opens Step 2 (Introduction Screen)

---

### Step 2: Introduction Screen / Экран введения

**Purpose / Назначение:**
- Приветствовать пользователя
- Объяснить преимущества бизнес-профиля
- Настроить ожидания

**Screen Content / Содержимое экрана:**

**Title / Заголовок:**
```
Create Your Business Profile
Создайте свой бизнес-профиль
```

**Description / Описание:**
```
Welcome to Bestme Business! Create a professional profile to:
Добро пожаловать в Bestme Business! Создайте профессиональный профиль, чтобы:

✓ Reach wellness-focused audience
  Достичь аудитории, интересующейся wellness

✓ Get bookings and orders
  Получать записи и заказы

✓ Share your expertise
  Делиться своей экспертизой

✓ Build your community
  Создавать сообщество

✓ Track analytics
  Отслеживать аналитику
```

**CTA Button:**
```
Continue / Продолжить
```

**Secondary Action:**
```
← Back / Назад
```

---

### Step 3: Business Type Selection / Выбор типа бизнеса ⭐

**Purpose / Назначение:**
Выбор типа бизнеса определяет:
- Какие блоки будут в профиле
- Какие CTA кнопки показывать
- Какие поля предложить заполнить

**Title / Заголовок:**
```
Select Your Business Type
Выберите тип вашего бизнеса
```

**Helper Text / Подсказка:**
```
This helps us create the perfect profile for your business.
You can't change this later.

Это поможет нам создать идеальный профиль для вашего бизнеса.
Изменить это позже нельзя.
```

**7 Business Type Cards / 7 карточек типов:**

#### Card 1: Specialist / Специалист
```
┌──────────────────────────────────┐
│  🎯 Specialist / Специалист      │
│                                  │
│  Personal services and           │
│  consultations                   │
│  Персональные услуги и           │
│  консультации                    │
│                                  │
│  Example: Coach, Therapist,      │
│  Trainer                         │
│  Пример: Коуч, Психолог, Тренер  │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 2: Place / Место
```
┌──────────────────────────────────┐
│  📍 Place / Место                │
│                                  │
│  Physical location to visit      │
│  Физическое место для посещения  │
│                                  │
│  Example: Cafe, Studio, Gym      │
│  Пример: Кафе, Студия, Зал       │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 3: Education / Образование
```
┌──────────────────────────────────┐
│  🎓 Education / Образование      │
│                                  │
│  Courses and learning programs   │
│  Курсы и образовательные         │
│  программы                       │
│                                  │
│  Example: School, Courses        │
│  Пример: Школа, Курсы            │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 4: Services / Сервисы
```
┌──────────────────────────────────┐
│  🔧 Services / Сервисы           │
│                                  │
│  Professional services           │
│  Профессиональные услуги         │
│                                  │
│  Example: Design, Repair,        │
│  Consulting                      │
│  Пример: Дизайн, Ремонт,         │
│  Консалтинг                      │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 5: Products / Товары
```
┌──────────────────────────────────┐
│  🛍️ Products / Товары            │
│                                  │
│  Selling products                │
│  Продажа товаров                 │
│                                  │
│  Example: Shop, Brand,           │
│  Manufacturer                    │
│  Пример: Магазин, Бренд,         │
│  Производитель                   │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 6: Activities & Travel / Активности
```
┌──────────────────────────────────┐
│  ✈️ Activities & Travel /        │
│     Активности                   │
│                                  │
│  Tours, retreats, experiences    │
│  Туры, ретриты, мероприятия      │
│                                  │
│  Example: Tours, Retreats,       │
│  Excursions                      │
│  Пример: Туры, Ретриты,          │
│  Экскурсии                       │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

#### Card 7: B2B Services / B2B Сервисы
```
┌──────────────────────────────────┐
│  💼 B2B Services / B2B           │
│                                  │
│  Solutions for businesses        │
│  Решения для бизнеса             │
│                                  │
│  Example: SaaS, Consulting,      │
│  Platforms                       │
│  Пример: SaaS, Консалтинг,       │
│  Платформы                       │
│                                  │
│  [Select / Выбрать]              │
└──────────────────────────────────┘
```

**Action:** User selects ONE type → Goes to Step 4

**Progress Indicator:**
```
Step 3 of 6 / Шаг 3 из 6
```

---

### Step 4: Primary Information / Основная информация ⭐

**Purpose / Назначение:**
Сбор обязательной информации для публикации профиля.

**Title / Заголовок:**
```
Tell Us About Your Business
Расскажите о вашем бизнесе
```

**Required Fields / Обязательные поля:**

#### 1. Business Name / Название бизнеса
```
Business Name / Название бизнеса *
[________________________]

Helper: This will be your public business name
Подсказка: Это будет ваше публичное название

Validation: 3-100 characters, must be unique
Валидация: 3-100 символов, должно быть уникальным
```

#### 2. Description / Описание
```
Description / Описание *
[________________________]
[________________________]
[________________________]

100-500 characters / 100-500 символов
Current: 0 / 500

Helper: Describe what you do in 1-2 sentences
Подсказка: Опишите, чем вы занимаетесь в 1-2 предложениях

Validation: 100-500 characters required
Валидация: Требуется 100-500 символов
```

#### 3. Business Format / Формат работы
```
Business Format / Формат работы *

○ Online / Онлайн
  Services provided remotely
  Услуги предоставляются удаленно

○ Offline / Офлайн
  Services at physical location
  Услуги в физическом месте

○ Hybrid / Гибрид
  Both online and offline
  И онлайн, и офлайн

Validation: Must select one
Валидация: Нужно выбрать один
```

#### 4. Contact Information / Контактная информация
```
Contact Information / Контактная информация *

Phone / Телефон
[________________________]

OR / ИЛИ

Email / Email
[________________________]

Helper: At least one contact method required
Подсказка: Требуется хотя бы один способ связи

Validation: Valid phone OR email format
Валидация: Валидный формат телефона ИЛИ email
```

#### 5. Location / Местоположение (Conditional)
```
Location / Местоположение *
[________________________]

Helper: Required if format is Offline or Hybrid
Подсказка: Требуется, если формат Офлайн или Гибрид

Validation: Required only for Offline/Hybrid
Валидация: Обязательно только для Офлайн/Гибрид
```

**Optional but Recommended / Опционально, но рекомендуется:**

#### 6. Avatar / Аватар
```
Avatar / Аватар

[Upload Image / Загрузить изображение]

Helper: Add a profile picture to build trust
Подсказка: Добавьте фото профиля для доверия

Format: JPG, PNG (max 5MB, 400x400px recommended)
Формат: JPG, PNG (макс 5МБ, рекомендуется 400x400px)
```

**Actions:**

Primary Button:
```
Continue / Продолжить
```

Secondary Actions:
```
← Back / Назад
Save Draft / Сохранить черновик
```

**Progress Indicator:**
```
Step 4 of 6 / Шаг 4 из 6
```

**Auto-Save:**
```
Draft saved / Черновик сохранен ✓
Last saved: 2 minutes ago
Последнее сохранение: 2 минуты назад
```

---

### Step 5: Identity Information / Уникальная информация ⭐

**Purpose / Назначение:**
Сбор информации, специфичной для выбранного типа бизнеса. ВСЕ поля опциональны.

**Title / Заголовок:**
```
Add Your [Business Type] Details
Добавьте детали [Тип бизнеса]

Optional - You can add this later
Опционально - можно добавить позже
```

**Fields vary by Business Type / Поля зависят от типа бизнеса:**

#### For Specialist / Для Специалиста:
```
Services / Услуги
[+ Add Service / Добавить услугу]

Certifications / Сертификаты
[+ Add Certification / Добавить сертификат]

Availability Calendar / Календарь доступности
[Set up calendar / Настроить календарь]
```

#### For Place / Для Места:
```
Amenities / Удобства
☐ WiFi
☐ Parking / Парковка
☐ Wheelchair Access / Доступ для инвалидов

Capacity / Вместимость
[__] people / человек

Opening Hours / Часы работы
[Set schedule / Установить расписание]
```

#### For Education / Для Образования:
```
First Course / Первый курс
[+ Add Course / Добавить курс]

Schedule / Расписание
[Set schedule / Установить расписание]

Certification Programs / Программы сертификации
[+ Add Program / Добавить программу]
```

#### For Services / Для Сервисов:
```
Services Catalog / Каталог услуг
[+ Add Service / Добавить услугу]

Pricing / Цены
[Add pricing / Добавить цены]

Portfolio / Портфолио
[Upload work samples / Загрузить примеры работ]
```

#### For Products / Для Товаров:
```
First Product / Первый товар
[+ Add Product / Добавить товар]

Shipping Information / Информация о доставке
[Add shipping details / Добавить детали доставки]

Return Policy / Политика возврата
[Add return policy / Добавить политику возврата]
```

#### For Activities & Travel / Для Активностей:
```
First Activity / Первая активность
[+ Add Activity / Добавить активность]

Dates & Availability / Даты и доступность
[Set dates / Установить даты]

Difficulty Levels / Уровни сложности
○ Beginner / Начальный
○ Intermediate / Средний
○ Advanced / Продвинутый
```

#### For B2B Services / Для B2B:
```
Solutions / Решения
[+ Add Solution / Добавить решение]

Case Studies / Кейсы
[+ Add Case Study / Добавить кейс]

Pricing Tiers / Ценовые уровни
[Add pricing / Добавить цены]
```

**Actions:**

Primary Button:
```
Continue / Продолжить
```

Secondary Actions:
```
Skip This Step / Пропустить этот шаг
← Back / Назад
Save Draft / Сохранить черновик
```

**Helper Text:**
```
💡 You can add more details after publishing
💡 Вы сможете добавить больше деталей после публикации
```

**Progress Indicator:**
```
Step 5 of 6 / Шаг 5 из 6
```

---

### Step 6: Review & Publish / Проверка и публикация

**Purpose / Назначение:**
- Показать превью профиля
- Дать возможность отредактировать
- Опубликовать профиль

**Title / Заголовок:**
```
Review Your Profile
Проверьте ваш профиль
```

**Preview Section / Секция превью:**

```
┌────────────────────────────────────────┐
│  PREVIEW / ПРЕДПРОСМОТР               │
│                                        │
│  [Avatar] Business Name                │
│           🎯 Specialist ← Badge shown! │
│  [Book] [Contact] [Call]              │
│                                        │
│  📍 Location                          │
│  🌐 Format: Online                    │
│  📞 Phone: +1234567890                │
│                                        │
│  About / О нас:                       │
│  Description text here...             │
│                                        │
│  Services / Услуги: (if added)        │
│  - Service 1                          │
│  - Service 2                          │
│                                        │
│  [Edit / Редактировать]               │
└────────────────────────────────────────┘
```

**Edit Options / Опции редактирования:**
```
✏️ Edit Business Type (can't change)
✏️ Edit Primary Information
✏️ Edit Identity Information
✏️ Add Cover Photo
✏️ Add Opening Hours
✏️ Add Social Links
```

**Privacy Settings / Настройки приватности:**
```
Profile Visibility / Видимость профиля

○ Public / Публичный
  Anyone can find and view your profile
  Любой может найти и посмотреть ваш профиль

○ Private / Приватный
  Only people you approve can see your profile
  Только одобренные люди могут видеть профиль

Default: Public / По умолчанию: Публичный
```

**Terms & Conditions:**
```
☐ I agree to Bestme Business Terms
  Я согласен с условиями Bestme Business

☐ I confirm all information is accurate
  Я подтверждаю, что вся информация точна
```

**Actions:**

Primary Button (BIG!):
```
🎉 Publish Profile / Опубликовать профиль
```

Secondary Actions:
```
← Back to Edit / Назад к редактированию
Save as Draft / Сохранить как черновик
```

**Progress Indicator:**
```
Step 6 of 6 / Шаг 6 из 6
```

---

### Success Screen / Экран успеха

**After Clicking "Publish" / После нажатия "Опубликовать":**

```
┌────────────────────────────────────────┐
│           🎉 Congratulations! 🎉       │
│                                        │
│  Your Business Profile is Live!       │
│  Ваш бизнес-профиль опубликован!      │
│                                        │
│  [Preview Image of Profile]           │
│                                        │
│  What's Next? / Что дальше?           │
│                                        │
│  ✓ Share your profile                │
│    Поделитесь профилем                │
│                                        │
│  ✓ Add more content                  │
│    Добавьте больше контента           │
│                                        │
│  ✓ Start getting bookings            │
│    Начните получать записи            │
│                                        │
│  [View Profile / Посмотреть профиль]  │
│  [Share / Поделиться]                 │
│                                        │
│  [Close / Закрыть]                    │
└────────────────────────────────────────┘
```

**Notification Sent:**
```
✉️ Email confirmation sent
✉️ Подтверждение отправлено на email

📱 Push notification sent
📱 Push-уведомление отправлено
```

---

## 3. Information Hierarchy / Иерархия информации

### PRIMARY INFORMATION / ГЛАВНАЯ ИНФОРМАЦИЯ ⭐

**Required for publishing / Требуется для публикации:**

1. **Business Name / Название бизнеса**
   - Required: Yes / Обязательно: Да
   - Validation: 3-100 characters, unique
   - Валидация: 3-100 символов, уникальное
   - Can edit later: Yes / Можно изменить: Да

2. **Business Type / Тип бизнеса**
   - Required: Yes / Обязательно: Да
   - Validation: Must select one of 7 types
   - Валидация: Нужно выбрать один из 7 типов
   - Can edit later: **NO** / Можно изменить: **НЕТ**

3. **Description / Описание**
   - Required: Yes / Обязательно: Да
   - Validation: 100-500 characters
   - Валидация: 100-500 символов
   - Can edit later: Yes / Можно изменить: Да

4. **Business Format / Формат работы**
   - Required: Yes / Обязательно: Да
   - Options: Online, Offline, Hybrid
   - Варианты: Онлайн, Офлайн, Гибрид
   - Can edit later: Yes / Можно изменить: Да

5. **Contact Information / Контактная информация**
   - Required: At least ONE (phone OR email)
   - Обязательно: Хотя бы ОДИН (телефон ИЛИ email)
   - Validation: Valid format
   - Валидация: Валидный формат
   - Can edit later: Yes / Можно изменить: Да

6. **Location / Местоположение** (Conditional)
   - Required: If format is Offline or Hybrid
   - Обязательно: Если формат Офлайн или Гибрид
   - Can edit later: Yes / Можно изменить: Да

**Summary / Резюме:**
```
PRIMARY = Must have to publish
PRIMARY = Нужно иметь для публикации

Variable: can_publish
Value: true if ALL primary fields filled
```

---

### SECONDARY INFORMATION / ВТОРИЧНАЯ ИНФОРМАЦИЯ

**Optional but recommended / Опционально, но рекомендуется:**

1. **Avatar / Аватар**
   - Recommended: Yes / Рекомендуется: Да
   - Format: JPG, PNG (max 5MB)
   - Impact: +80% trust / Влияние: +80% доверие
   - Can add later: Yes / Можно добавить: Да

2. **Cover Photo / Обложка**
   - Recommended: Yes / Рекомендуется: Да
   - Format: JPG, PNG (max 10MB)
   - Size: 1200x400px recommended
   - Can add later: Yes / Можно добавить: Да

3. **Opening Hours / Часы работы**
   - Recommended: For Place, Offline businesses
   - Рекомендуется: Для Места, Офлайн бизнесов
   - Impact: +50% bookings / Влияние: +50% записей
   - Can add later: Yes / Можно добавить: Да

4. **Social Links / Соцсети**
   - Recommended: Yes / Рекомендуется: Да
   - Platforms: Instagram, Facebook, LinkedIn, etc.
   - Impact: +30% engagement / Влияние: +30% вовлечение
   - Can add later: Yes / Можно добавить: Да

5. **Website / Веб-сайт**
   - Optional: Yes / Опционально: Да
   - Format: Valid URL
   - Can add later: Yes / Можно добавить: Да

**Summary / Резюме:**
```
SECONDARY = Makes profile more complete
SECONDARY = Делает профиль более полным

Impact: Better trust, more bookings
Влияние: Больше доверия, больше записей
```

---

### TERTIARY INFORMATION / ТРЕТИЧНАЯ ИНФОРМАЦИЯ

**Can add anytime after publishing / Можно добавить когда угодно после публикации:**

1. **Identity Blocks / Уникальные блоки**
   - Services, Products, Courses, Activities, etc.
   - Услуги, Товары, Курсы, Активности и т.д.
   - Can add anytime: Yes / Можно добавить: Да
   - Progressive enhancement / Прогрессивное улучшение

2. **Media Gallery / Медиа галерея**
   - Photos, Videos / Фото, Видео
   - Recommended: 5-10 photos minimum
   - Рекомендуется: Минимум 5-10 фото
   - Can add anytime: Yes / Можно добавить: Да

3. **Posts / Посты**
   - Business updates, news, announcements
   - Обновления бизнеса, новости, объявления
   - Can add anytime: Yes / Можно добавить: Да

4. **Reviews / Отзывы**
   - User-generated content
   - Контент от пользователей
   - Can't add yourself: User must leave review
   - Нельзя добавить самостоятельно: Пользователь должен оставить отзыв

5. **Certifications / Сертификаты**
   - Professional certifications
   - Профессиональные сертификаты
   - Can add anytime: Yes / Можно добавить: Да

6. **Portfolio / Портфолио**
   - Work samples, case studies
   - Примеры работ, кейсы
   - Can add anytime: Yes / Можно добавить: Да

**Summary / Резюме:**
```
TERTIARY = Enhances profile over time
TERTIARY = Улучшает профиль со временем

Approach: Progressive enhancement
Подход: Прогрессивное улучшение
```

---

## 4. User Journey Example / Пример пользовательского пути

### Scenario / Сценарий

**Maria wants to create a profile for her coaching business**
**Мария хочет создать профиль для своего коучинг-бизнеса**

### Step-by-Step Journey:

**Step 1: Entry**
```
Maria → Personal Account → Settings → Account
Sees: "Create Business Account" button
Clicks: "Create"
```

**Step 2: Introduction**
```
Sees: Welcome screen with benefits
Reads: About Bestme Business
Clicks: "Continue"
```

**Step 3: Business Type**
```
Sees: 7 business type cards
Thinks: "I'm a coach, so Specialist"
Selects: 🎯 Specialist card
Clicks: "Next"
```

**Step 4: Primary Info**
```
Fills:
- Name: "Dr. Maria Wellness Coach"
- Description: "Professional life coach helping you achieve balance and wellness through personalized coaching sessions"
- Format: ○ Online (selected)
- Contact: maria@example.com
- Avatar: Uploads photo ✓

Clicks: "Continue"
```

**Step 5: Identity Info**
```
Optionally adds:
- Services: "Life Coaching" (60 min, $100)
- Services: "Career Coaching" (90 min, $150)
- Certifications: "ICF Certified Coach"
- Skips: Availability Calendar (will add later)

Clicks: "Continue"
```

**Step 6: Review**
```
Sees: Preview of profile with 🎯 Specialist badge
Checks: Everything looks good!
Sets: Public visibility
Accepts: Terms & Conditions ✓
Clicks: "🎉 Publish Profile"
```

**Success!**
```
Sees: Congratulations screen!
Gets: Email confirmation
Gets: Push notification
Clicks: "View Profile"
```

**Result:**
```
Maria's profile is now live with:
✓ 🎯 Specialist badge visible
✓ "Book / Записаться" primary CTA
✓ All info displayed correctly
✓ Can start getting bookings!
```

---

## 5. Validation Rules / Правила валидации

### Business Name / Название бизнеса

**Rules:**
- Minimum: 3 characters / Минимум: 3 символа
- Maximum: 100 characters / Максимум: 100 символов
- Must be unique / Должно быть уникальным
- No special characters except: - _ & '
- Нет спецсимволов кроме: - _ & '

**Error Messages:**
```
❌ "Business name is too short (min 3 characters)"
❌ "Название слишком короткое (мин 3 символа)"

❌ "This business name is already taken"
❌ "Это название уже занято"

❌ "Business name contains invalid characters"
❌ "Название содержит недопустимые символы"
```

### Description / Описание

**Rules:**
- Minimum: 100 characters / Минимум: 100 символов
- Maximum: 500 characters / Максимум: 500 символов
- Required / Обязательно

**Character Counter:**
```
Current: 0 / 500
Текущее: 0 / 500

(turns red if < 100 or > 500)
```

**Error Messages:**
```
❌ "Description is too short (min 100 characters)"
❌ "Описание слишком короткое (мин 100 символов)"

❌ "Description is too long (max 500 characters)"
❌ "Описание слишком длинное (макс 500 символов)"
```

### Contact Information / Контактная информация

**Rules:**
- At least ONE required (phone OR email)
- Хотя бы ОДИН обязателен (телефон ИЛИ email)
- Phone: Valid international format
- Телефон: Валидный международный формат
- Email: Valid email format
- Email: Валидный формат email

**Error Messages:**
```
❌ "Please provide at least one contact method"
❌ "Пожалуйста, укажите хотя бы один способ связи"

❌ "Invalid phone number format"
❌ "Неверный формат номера телефона"

❌ "Invalid email format"
❌ "Неверный формат email"
```

### Location / Местоположение

**Rules:**
- Required IF format is Offline or Hybrid
- Обязательно ЕСЛИ формат Офлайн или Гибрид
- Must be valid address
- Должен быть валидным адресом

**Error Messages:**
```
❌ "Location is required for Offline businesses"
❌ "Местоположение обязательно для Офлайн бизнесов"

❌ "Please enter a valid address"
❌ "Пожалуйста, введите валидный адрес"
```

### Avatar / Аватар

**Rules (if uploaded):**
- Format: JPG, PNG / Формат: JPG, PNG
- Max size: 5MB / Макс размер: 5МБ
- Recommended: 400x400px / Рекомендуется: 400x400px
- Min resolution: 200x200px / Мин разрешение: 200x200px

**Error Messages:**
```
❌ "Image file is too large (max 5MB)"
❌ "Файл изображения слишком большой (макс 5МБ)"

❌ "Invalid image format (use JPG or PNG)"
❌ "Неверный формат изображения (используйте JPG или PNG)"

❌ "Image resolution is too low (min 200x200px)"
❌ "Разрешение изображения слишком низкое (мин 200x200px)"
```

---

## 6. UX Best Practices / Лучшие практики UX

### Progress Indicator / Индикатор прогресса

**Always show current step:**
```
Step 3 of 6 / Шаг 3 из 6
[===-----]  50%
```

### Auto-Save / Автосохранение

**Save draft every 30 seconds:**
```
💾 Draft saved / Черновик сохранен ✓
Last saved: 2 minutes ago
Последнее сохранение: 2 минуты назад
```

### Helper Text / Подсказки

**Provide context for every field:**
```
💡 Helper: This will be your public business name
💡 Подсказка: Это будет ваше публичное название
```

### Validation Feedback / Обратная связь по валидации

**Real-time validation:**
```
✓ Business name available
✓ Название доступно

✗ Email format invalid
✗ Формат email неверный
```

### Skip Option / Опция пропуска

**Allow skipping optional steps:**
```
Skip This Step / Пропустить этот шаг
You can add this later
Вы можете добавить это позже
```

### Edit After Publishing / Редактирование после публикации

**Make it easy to edit:**
```
All fields can be edited after publishing
Все поля можно редактировать после публикации

Exception: Business Type (can't change)
Исключение: Тип бизнеса (нельзя изменить)
```

### Success Celebration / Празднование успеха

**Make publishing feel rewarding:**
```
🎉 Congratulations!
🎉 Поздравляем!

Your profile is live!
Ваш профиль опубликован!
```

### Mobile Optimization / Оптимизация для мобильных

**Ensure mobile-friendly:**
- Large touch targets / Большие области касания
- Easy scrolling / Легкая прокрутка
- Simplified layouts / Упрощенные макеты
- No horizontal scroll / Нет горизонтальной прокрутки

---

## 7. After Profile is Published / После публикации профиля

### What Happens / Что происходит

**Immediate Actions:**
1. ✅ Profile goes live instantly
   Профиль публикуется мгновенно

2. ✅ Badge appears in header
   Бейдж появляется в шапке

3. ✅ Profile URL created
   URL профиля создан: bestme.com/business/username

4. ✅ Indexed for search
   Индексирован для поиска

5. ✅ Notifications sent
   Уведомления отправлены:
   - Email confirmation / Email подтверждение
   - Push notification / Push уведомление

### User Can Now / Пользователь теперь может

**Profile Management:**
- ✏️ Edit all fields (except Business Type)
- ✏️ Редактировать все поля (кроме Типа бизнеса)

- 📸 Add more photos to gallery
- 📸 Добавить больше фото в галерею

- 📝 Create posts
- 📝 Создавать посты

- 📊 View analytics
- 📊 Просматривать аналитику

- 💬 Respond to reviews
- 💬 Отвечать на отзывы

**Business Operations:**
- 📅 Manage bookings (if applicable)
- 📅 Управлять записями (если применимо)

- 🛒 Manage orders (if applicable)
- 🛒 Управлять заказами (если применимо)

- 💳 Set up payments (if needed)
- 💳 Настроить платежи (если нужно)

- 📧 Message customers
- 📧 Писать клиентам

**Profile Switching:**
- 🔄 Switch between Personal ↔ Business profile
- 🔄 Переключаться между Личным ↔ Бизнес профилем

- 👤 Maintain both profiles simultaneously
- 👤 Поддерживать оба профиля одновременно

### Badge in Action / Бейдж в действии

**How it appears on published profile:**

```
┌────────────────────────────────────────┐
│  [Avatar]  Dr. Maria                  │
│            Wellness Coach              │
│            🎯 Specialist              │ ← Badge!
│                                        │
│  [Book / Записаться]                  │
│  [Contact / Связаться]                │
│  [Schedule / Расписание]              │
│                                        │
│  📍 Online                            │
│  📧 maria@example.com                 │
│                                        │
│  About / О нас:                       │
│  Professional life coach helping      │
│  you achieve balance and wellness...  │
│                                        │
│  ⭐⭐⭐⭐⭐ 4.9 (127 reviews)            │
└────────────────────────────────────────┘
```

**Badge benefits:**
- ✅ Instant category recognition
- ✅ Мгновенное распознавание категории

- ✅ Sets user expectations
- ✅ Устанавливает ожидания пользователя

- ✅ Professional appearance
- ✅ Профессиональный вид

- ✅ Helps in search/filtering
- ✅ Помогает в поиске/фильтрации

---

## 8. Technical Implementation Notes / Технические заметки

### Database Schema / Схема базы данных

```javascript
BusinessProfile {
  id: UUID
  user_id: UUID (FK to Users)
  business_type: ENUM ['specialist', 'place', 'education', 'services', 'products', 'activities', 'b2b']
  business_name: STRING (3-100 chars)
  description: TEXT (100-500 chars)
  format: ENUM ['online', 'offline', 'hybrid']
  
  // Contact
  phone: STRING (optional)
  email: STRING (optional, but phone OR email required)
  website: STRING (optional)
  
  // Location (required if offline/hybrid)
  address: TEXT (optional)
  latitude: DECIMAL (optional)
  longitude: DECIMAL (optional)
  
  // Media
  avatar_url: STRING (optional)
  cover_url: STRING (optional)
  
  // Status
  is_published: BOOLEAN (default: false)
  is_verified: BOOLEAN (default: false)
  visibility: ENUM ['public', 'private'] (default: 'public')
  
  // Timestamps
  created_at: TIMESTAMP
  updated_at: TIMESTAMP
  published_at: TIMESTAMP (nullable)
}
```

### Business Type Badge Logic / Логика бейджа

```javascript
function getBadge(businessType) {
  const badges = {
    'specialist': { icon: '🎯', label: 'Specialist / Специалист' },
    'place': { icon: '📍', label: 'Place / Место' },
    'education': { icon: '🎓', label: 'Education / Образование' },
    'services': { icon: '🔧', label: 'Services / Сервисы' },
    'products': { icon: '🛍️', label: 'Products / Товары' },
    'activities': { icon: '✈️', label: 'Activities / Активности' },
    'b2b': { icon: '💼', label: 'B2B / B2B' }
  };
  
  return badges[businessType];
}

function shouldShowBadge(profile) {
  return profile.is_published && profile.business_type;
}
```

### Validation Logic / Логика валидации

```javascript
function canPublish(profile) {
  // Primary fields required
  if (!profile.business_name || profile.business_name.length < 3) return false;
  if (!profile.business_type) return false;
  if (!profile.description || profile.description.length < 100) return false;
  if (!profile.format) return false;
  
  // At least one contact method
  if (!profile.phone && !profile.email) return false;
  
  // Location required for offline/hybrid
  if ((profile.format === 'offline' || profile.format === 'hybrid') && !profile.address) {
    return false;
  }
  
  return true;
}
```

---

## 9. Summary / Резюме

### Key Takeaways / Ключевые выводы

**Business Type Badge:**
- ✅ Shows AFTER publishing in profile header
- ✅ Visual indicator with icon + text
- ✅ Helps users quickly understand business category
- ✅ Can't be changed after selection

**Creation Flow:**
- ✅ 6 clear steps from entry to published
- ✅ Progress indicator always visible
- ✅ Auto-save drafts every 30 seconds
- ✅ Can skip optional fields
- ✅ Can edit everything after publishing (except type)

**Information Priority:**
- ✅ PRIMARY (required): Name, Type, Description, Format, Contact
- ✅ SECONDARY (optional): Avatar, Cover, Hours, Social
- ✅ TERTIARY (add anytime): Identity blocks, Gallery, Posts

**User Experience:**
- ✅ Simple, guided process
- ✅ Clear helper text at every step
- ✅ Real-time validation
- ✅ Success celebration
- ✅ Mobile-optimized

### Next Steps / Следующие шаги

**For Design Team / Для дизайн-команды:**
1. Create high-fidelity mockups for all 6 steps
2. Design badge variations for all 7 types
3. Create mobile layouts
4. Design error states
5. Create success celebration animation

**For Development Team / Для команды разработки:**
1. Implement database schema
2. Build step-by-step wizard
3. Implement validation logic
4. Build auto-save functionality
5. Implement badge display logic
6. Create analytics tracking

**For UX Testing / Для UX тестирования:**
1. Test with real users
2. Measure completion rate
3. Identify drop-off points
4. Gather feedback
5. Iterate based on data

---

## Questions? / Вопросы?

Этот документ отвечает на вопросы:
- ✅ Что такое Business Type Badge?
- ✅ Где он показывается?
- ✅ Когда он появляется?
- ✅ Какой флоу создания?
- ✅ Что главная информация, что вторичная?
- ✅ После нажатия "Создать бизнес аккаунт" что происходит?

**All documented with bilingual interface text!**
**Всё задокументировано с двуязычными текстами интерфейса!**
