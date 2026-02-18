# Business Profile UX Architecture / UX-архитектура бизнес-профиля

## Project Context / Контекст проекта

**Bestme** — это социальная сеть в сфере wellness и саморазвития, где бизнесы создают профили внутри соцсети (не просто маркетплейс). Бизнес-профиль должен быть адаптивным и понятным с первого взгляда.

**Key Principle / Ключевой принцип:**
Система должна динамически адаптироваться под тип бизнеса, показывая только релевантную информацию и действия.

---

## 1. Information Architecture / Информационная архитектура

### Structure / Структура профиля:

```
Business Profile / Бизнес-профиль
│
├── UNIVERSAL SECTION / УНИВЕРСАЛЬНАЯ СЕКЦИЯ
│   └── 8 common blocks for ALL business types
│       8 общих блоков для ВСЕХ типов бизнеса
│
└── IDENTITY SECTION / СЕКЦИЯ ИДЕНТИЧНОСТИ  
    └── Unique blocks based on Business Type (3-5 blocks)
        Уникальные блоки в зависимости от типа (3-5 блоков)
```

---

## 2. Universal Section / Универсальная секция

**Эти блоки есть у ВСЕХ бизнес-профилей (нельзя менять):**

### 2.1 Header / Шапка профиля
- Business Name / Название бизнеса
- Business Type Badge / Бейдж типа бизнеса
- Avatar / Аватар
- Cover Photo / Обложка
- CTA Buttons / Кнопки действий (2-4, адаптивные)

### 2.2 About / О нас
- Description / Описание
- Specializations / Специализации
- Founded / Год основания (optional)

### 2.3 Format / Формат работы
- Online / Онлайн
- Offline / Офлайн  
- Hybrid / Гибрид

### 2.4 Location / Address / Локация
- Physical address / Физический адрес (if offline/hybrid)
- Map / Карта
- Get Directions button / Кнопка "Маршрут"

### 2.5 Opening Hours / Часы работы
- Schedule / Расписание (if provided)
- Timezone / Часовой пояс

### 2.6 Contact / Контакты
- Phone / Телефон
- Email / Email
- Website / Веб-сайт
- Social Links / Соцсети

### 2.7 Posts / Посты
- Business posts / Посты бизнеса
- Announcements / Объявления
- Updates / Обновления

### 2.8 Media Gallery / Медиа галерея
- Photos / Фото
- Videos / Видео
- Portfolio / Портфолио

### 2.9 Reviews / Отзывы
- Rating / Рейтинг
- Reviews list / Список отзывов
- Write a review / Написать отзыв

**⚠️ Important / Важно:**
- If a block has no data → hide it / Если блок пустой → скрыть
- Universal blocks are NOT duplicated in Identity Section / Универсальные блоки НЕ дублируются в уникальных

---

## 3. Business Types / Типы бизнеса

### 3.1 Specialist / Специалист

**Identity Description / Описание идентичности:**
Индивидуальные специалисты, предоставляющие персональные услуги: психологи, коучи, тренеры, консультанты, мастера красоты, массажисты, диетологи. Пользователь приходит, чтобы **записаться на консультацию или сессию**.

**Primary CTA:**
- **Book / Записаться** ⭐

**Secondary CTAs (2-3):**
- Contact / Связаться
- View Schedule / Расписание
- Call / Позвонить

**Unique Blocks / Уникальные блоки:**

1. **Services Menu / Меню услуг**
   - Service Name / Название услуги
   - Duration / Длительность
   - Price / Цена
   - Description / Описание
   - Variable: `services_catalog`

2. **Certifications & Credentials / Сертификаты и квалификация**
   - Diplomas / Дипломы
   - Certificates / Сертификаты
   - Professional memberships / Членство в ассоциациях
   - Variable: `certifications_list`

3. **Availability Calendar / Календарь доступности**
   - Available time slots / Доступные слоты
   - Booking interface / Интерфейс записи
   - Timezone / Часовой пояс
   - Variable: `availability_calendar`

4. **Specialization Tags / Теги специализации**
   - Areas of expertise / Области экспертизы
   - Methods / Методы
   - Variable: `specialization_tags`

**Optional Blocks / Опциональные блоки:**
- Client Success Stories / Истории успеха клиентов (if provided)
- Education & Training / Образование (if provided)
- Years of Experience / Опыт работы

**Onboarding Hint / Подсказка при выборе:**
```
Specialist Profile / Профиль специалиста
Perfect for: Coaches, therapists, consultants, personal trainers
Идеально для: Коучи, терапевты, консультанты, тренеры

You'll be able to:
• Showcase your services and expertise
• Let clients book appointments
• Display certifications and credentials
• Manage your availability calendar

Вы сможете:
• Показать свои услуги и экспертизу
• Принимать записи клиентов
• Отображать сертификаты
• Управлять календарем доступности
```

---

### 3.2 Place / Место

**Identity Description / Описание идентичности:**
Физические места и заведения: студии йоги, фитнес-центры, wellness-центры, спа, кафе здорового питания, коворкинги. Пользователь приходит, чтобы **посетить место** или **забронировать визит**.

**Primary CTA:**
- **Visit / Посетить** ⭐

**Secondary CTAs (2-3):**
- Book / Забронировать
- Get Directions / Маршрут
- Call / Позвонить

**Unique Blocks / Уникальные блоки:**

1. **Menu / Amenities / Меню / Удобства**
   - Services list / Список услуг
   - Facilities / Оборудование
   - Menu items / Позиции меню (for cafes)
   - Variable: `amenities_list`

2. **Capacity & Space Info / Вместимость**
   - Max capacity / Максимальная вместимость
   - Space description / Описание пространства
   - Room types / Типы помещений
   - Variable: `capacity_info`

3. **Atmosphere & Vibe / Атмосфера**
   - Style tags / Теги стиля
   - Music / Музыка
   - Ambiance / Обстановка
   - Variable: `atmosphere_tags`

4. **Parking & Accessibility / Парковка и доступность**
   - Parking availability / Наличие парковки
   - Public transport / Общественный транспорт
   - Accessibility features / Доступность для людей с ограниченными возможностями
   - Variable: `accessibility_info`

**Optional Blocks / Опциональные блоки:**
- Events Calendar / Календарь мероприятий (if has events)
- Membership Options / Варианты членства (if applicable)
- Class Schedule / Расписание занятий (if applicable)

**Onboarding Hint / Подсказка при выборе:**
```
Place Profile / Профиль места
Perfect for: Studios, wellness centers, gyms, healthy cafes
Идеально для: Студии, wellness-центры, фитнес-залы, кафе

You'll be able to:
• Showcase your physical space
• Display amenities and facilities
• Help visitors find and contact you
• Share your atmosphere and vibe

Вы сможете:
• Показать ваше пространство
• Отобразить удобства и оборудование
• Помочь найти и связаться с вами
• Передать атмосферу места
```

---

### 3.3 Education / Образование

**Identity Description / Описание идентичности:**
Образовательные проекты: онлайн-курсы, школы, мастер-классы, тренинги, программы сертификации, образовательные платформы. Может быть онлайн, офлайн или гибрид. Пользователь приходит, чтобы **записаться на курс или программу**.

**Primary CTA:**
- **Enroll / Записаться** ⭐

**Secondary CTAs (2-3):**
- View Courses / Курсы
- Contact / Связаться
- Download Syllabus / Программа

**Unique Blocks / Уникальные блоки:**

1. **Courses Catalog / Каталог курсов**
   - Course title / Название курса
   - Duration / Длительность
   - Price / Цена
   - Level / Уровень (beginner, intermediate, advanced)
   - Format / Формат (online, offline, hybrid)
   - Variable: `courses_catalog`

2. **Course Schedule / Расписание курсов**
   - Start dates / Даты начала
   - Time / Время
   - Frequency / Частота занятий
   - Variable: `course_schedule`

3. **Certification Programs / Программы сертификации**
   - Certificate types / Типы сертификатов
   - Requirements / Требования
   - Recognition / Признание
   - Variable: `certification_programs`

4. **Instructors / Преподаватели**
   - Teacher profiles / Профили преподавателей
   - Qualifications / Квалификация
   - Bio / Биография
   - Variable: `instructors_list`

**Optional Blocks / Опциональные блоки:**
- Student Success Stories / Истории успеха студентов
- Free Trial / Бесплатный пробный урок
- Course Materials / Материалы курса (preview)

**Onboarding Hint / Подсказка при выборе:**
```
Education Profile / Образовательный профиль
Perfect for: Online courses, schools, workshops, training programs
Идеально для: Онлайн-курсы, школы, мастер-классы, тренинги

You'll be able to:
• Showcase your courses and programs
• Display course schedules and pricing
• Feature your instructors
• Offer certifications

Вы сможете:
• Показать курсы и программы
• Отобразить расписание и цены
• Представить преподавателей
• Предлагать сертификацию
```

---

### 3.4 Services / Сервисы

**Identity Description / Описание идентичности:**
Сервисные компании, предоставляющие различные услуги: дизайн, разработка, консалтинг, маркетинг, event-организация, wellness-услуги для компаний. Пользователь приходит, чтобы **получить расчет** или **заказать услугу**.

**Primary CTA:**
- **Get Quote / Получить расчет** ⭐

**Secondary CTAs (2-3):**
- Contact / Связаться
- View Services / Услуги
- Schedule Call / Созвон

**Unique Blocks / Уникальные блоки:**

1. **Services Catalog / Каталог услуг**
   - Service categories / Категории услуг
   - Service description / Описание
   - Deliverables / Результаты
   - Timeline / Сроки
   - Variable: `services_catalog`

2. **Pricing Models / Модели ценообразования**
   - Hourly rate / Почасовая ставка
   - Project-based / За проект
   - Retainer / Абонемент
   - Packages / Пакеты
   - Variable: `pricing_models`

3. **Portfolio / Портфолио**
   - Case studies / Кейсы
   - Before/After / До/После
   - Results / Результаты
   - Testimonials / Отзывы клиентов
   - Variable: `portfolio_items`

4. **Process / Workflow / Процесс работы**
   - Steps / Этапы
   - Timeline / Временные рамки
   - What to expect / Чего ожидать
   - Variable: `workflow_steps`

**Optional Blocks / Опциональные блоки:**
- Team Members / Команда
- Industry Expertise / Отраслевая экспертиза
- Awards & Recognition / Награды

**Onboarding Hint / Подсказка при выборе:**
```
Services Profile / Профиль сервисов
Perfect for: Agencies, consultants, service providers
Идеально для: Агентства, консультанты, поставщики услуг

You'll be able to:
• Showcase your service offerings
• Display pricing and packages
• Share your portfolio and results
• Explain your process

Вы сможете:
• Показать услуги
• Отобразить цены и пакеты
• Поделиться портфолио
• Объяснить процесс работы
```

---

### 3.5 Products / Товары

**Identity Description / Описание идентичности:**
E-commerce бизнесы, продающие физические или цифровые товары: wellness-продукты, добавки, экипировка, книги, оборудование для йоги. Пользователь приходит, чтобы **купить товары**.

**Primary CTA:**
- **Shop / Магазин** ⭐

**Secondary CTAs (2-3):**
- View Catalog / Каталог
- Contact / Связаться
- Track Order / Отследить заказ

**Unique Blocks / Уникальные блоки:**

1. **Product Catalog / Каталог товаров**
   - Product cards / Карточки товаров
   - Categories / Категории
   - Filters / Фильтры (price, type, etc.)
   - Sorting / Сортировка
   - Variable: `product_catalog`

2. **Product Details / Детали товара**
   - Photos / Фото
   - Description / Описание
   - Specifications / Характеристики
   - Price / Цена
   - In stock / В наличии
   - Variable: `product_details`

3. **Shipping & Delivery / Доставка**
   - Shipping methods / Способы доставки
   - Delivery time / Сроки доставки
   - Shipping costs / Стоимость доставки
   - International shipping / Международная доставка
   - Variable: `shipping_info`

4. **Return Policy / Политика возврата**
   - Return period / Срок возврата
   - Conditions / Условия
   - Refund process / Процесс возврата
   - Variable: `return_policy`

**Optional Blocks / Опциональные блоки:**
- Featured Products / Популярные товары
- Bundles & Deals / Наборы и акции
- Loyalty Program / Программа лояльности

**Onboarding Hint / Подсказка при выборе:**
```
Products Profile / Профиль магазина
Perfect for: E-commerce, retail, wellness products
Идеально для: E-commerce, розница, wellness-продукты

You'll be able to:
• Create product catalog
• Manage inventory and pricing
• Set up shipping and delivery
• Handle orders and returns

Вы сможете:
• Создать каталог товаров
• Управлять складом и ценами
• Настроить доставку
• Обрабатывать заказы и возвраты
```

---

### 3.6 Activities & Travel / Активности и путешествия

**Identity Description / Описание идентичности:**
Организаторы активностей, туров и путешествий: wellness-ретриты, йога-туры, походы, экскурсии, активности на природе, приключенческий туризм. Пользователь приходит, чтобы **посмотреть активности и забронировать участие**.

**Primary CTA:**
- **Activities / Активности** ⭐

**Secondary CTAs (2-3):**
- Book / Забронировать
- View Calendar / Календарь
- Contact / Связаться

**Unique Blocks / Уникальные блоки:**

1. **Activities Catalog / Каталог активностей**
   - Activity name / Название
   - Type / Тип (retreat, tour, hike, etc.)
   - Duration / Длительность
   - Price / Цена
   - Group size / Размер группы
   - Variable: `activities_catalog`

2. **Dates & Availability / Даты и доступность**
   - Upcoming dates / Ближайшие даты
   - Calendar / Календарь
   - Booking status / Статус бронирования
   - Variable: `dates_availability`

3. **Difficulty Levels & Requirements / Уровень сложности**
   - Physical fitness required / Требования к физподготовке
   - Experience level / Уровень опыта
   - Age restrictions / Возрастные ограничения
   - Equipment needed / Необходимое снаряжение
   - Variable: `difficulty_requirements`

4. **Itinerary / Маршрут**
   - Daily schedule / Расписание по дням
   - Locations / Локации
   - Activities breakdown / Разбивка активностей
   - Meals included / Питание
   - Variable: `itinerary_details`

**Optional Blocks / Опциональные блоки:**
- Past Trips Gallery / Галерея прошлых поездок
- Participant Reviews / Отзывы участников
- Packing List / Список вещей

**Onboarding Hint / Подсказка при выборе:**
```
Activities & Travel Profile / Профиль активностей
Perfect for: Retreats, tours, outdoor activities, adventure travel
Идеально для: Ретриты, туры, активности на природе

You'll be able to:
• Showcase your activities and tours
• Display dates and availability
• Share itineraries and details
• Manage bookings and groups

Вы сможете:
• Показать активности и туры
• Отобразить даты и доступность
• Поделиться маршрутами
• Управлять бронированиями
```

---

### 3.7 B2B Services / B2B сервисы

**Identity Description / Описание идентичности:**
Услуги для бизнеса: корпоративный wellness, B2B SaaS, бизнес-консалтинг, корпоративные программы здоровья, оптовые поставки wellness-продуктов. Пользователь приходит, чтобы **запросить демо** или **получить коммерческое предложение**.

**Primary CTA:**
- **Request Demo / Запросить демо** ⭐

**Secondary CTAs (2-3):**
- Contact Sales / Отдел продаж
- View Solutions / Решения
- Download Deck / Презентация

**Unique Blocks / Уникальные блоки:**

1. **Solutions / Решения**
   - Solution categories / Категории решений
   - Features / Функционал
   - Benefits / Преимущества
   - Use cases / Кейсы использования
   - Variable: `solutions_catalog`

2. **Case Studies / Кейсы клиентов**
   - Client stories / Истории клиентов
   - Results & metrics / Результаты и метрики
   - Industry / Индустрия
   - Company size / Размер компании
   - Variable: `case_studies`

3. **Pricing Tiers / Ценовые планы**
   - Plan names / Названия планов
   - Features per tier / Функции в каждом плане
   - Pricing / Цены
   - Custom enterprise / Индивидуальный план
   - Variable: `pricing_tiers`

4. **Integrations & Tech Stack / Интеграции**
   - Compatible systems / Совместимые системы
   - API documentation / API документация
   - Technical requirements / Технические требования
   - Variable: `integrations_list`

**Optional Blocks / Опциональные блоки:**
- Client Logos / Логотипы клиентов
- ROI Calculator / Калькулятор ROI
- Certifications & Compliance / Сертификации

**Onboarding Hint / Подсказка при выборе:**
```
B2B Services Profile / B2B профиль
Perfect for: Corporate wellness, B2B SaaS, business consulting
Идеально для: Корпоративный wellness, B2B SaaS, бизнес-консалтинг

You'll be able to:
• Showcase solutions for businesses
• Display case studies and results
• Offer pricing tiers
• Generate leads and demos

Вы сможете:
• Показать решения для бизнеса
• Отобразить кейсы и результаты
• Предлагать ценовые планы
• Генерировать лиды и демо
```

---

## 4. CTA Logic System / Система CTA кнопок

### CTA Priority Rules / Правила приоритета:

**Primary CTA (1 button):**
- Most important action for this business type
- Always visible in header
- Highest visual priority (primary button style)

**Secondary CTAs (2-3 buttons):**
- Supporting actions
- Visible in header or quick actions section
- Secondary button style

**Tertiary actions:**
- Available in content blocks
- Lower priority
- Text links or tertiary buttons

### CTA Mapping Table / Таблица CTA:

| Business Type | Primary CTA | Secondary CTA 1 | Secondary CTA 2 | Secondary CTA 3 |
|---------------|-------------|-----------------|-----------------|-----------------|
| **Specialist** | Book / Записаться | Contact / Связаться | View Schedule / Расписание | Call / Позвонить |
| **Place** | Visit / Посетить | Book / Забронировать | Get Directions / Маршрут | Call / Позвонить |
| **Education** | Enroll / Записаться | View Courses / Курсы | Contact / Связаться | Download Syllabus / Программа |
| **Services** | Get Quote / Получить расчет | Contact / Связаться | View Services / Услуги | Schedule Call / Созвон |
| **Products** | Shop / Магазин | View Catalog / Каталог | Contact / Связаться | Track Order / Заказ |
| **Activities & Travel** | Activities / Активности | Book / Забронировать | View Calendar / Календарь | Contact / Связаться |
| **B2B Services** | Request Demo / Запросить демо | Contact Sales / Продажи | View Solutions / Решения | Download Deck / Презентация |

### CTA Behavior Rules / Правила поведения:

1. **Mobile:** Show maximum 2 CTAs in header, rest in overflow menu
2. **Empty State:** If action not available (e.g., no booking system) → hide button
3. **Logged In Users:** May see different CTAs based on relationship with business
4. **Load Order:** Primary CTA loads first, secondaries load progressively

---

## 5. Summary Comparison Table / Итоговая таблица сравнения

| Business Type | Primary CTA | Unique Blocks | Identity Focus | Best For |
|---------------|-------------|---------------|----------------|----------|
| **Specialist** | Book / Записаться | Services, Certifications, Calendar | Personal expertise & appointments | Coaches, therapists, consultants |
| **Place** | Visit / Посетить | Amenities, Capacity, Atmosphere | Physical space & experience | Studios, wellness centers, cafes |
| **Education** | Enroll / Записаться | Courses, Schedule, Certifications | Learning programs & development | Online courses, schools, trainings |
| **Services** | Get Quote / Расчет | Services, Pricing, Portfolio | Professional services & results | Agencies, consulting, B2C services |
| **Products** | Shop / Магазин | Catalog, Shipping, Returns | E-commerce & product sales | Wellness products, retail, equipment |
| **Activities** | Activities / Активности | Catalog, Dates, Itinerary | Experiences & adventures | Retreats, tours, outdoor activities |
| **B2B** | Request Demo / Демо | Solutions, Case Studies, Tiers | Business solutions & enterprise | Corporate wellness, SaaS, B2B |

---

## 6. Implementation Notes / Заметки по реализации

### 6.1 Technical Requirements / Технические требования

**Database Structure:**
```javascript
BusinessProfile {
  // Universal fields
  id: string
  business_name: string
  business_type: enum (7 types)
  description: text
  avatar: url
  cover: url
  format: enum (online, offline, hybrid)
  
  // Identity fields (JSON, type-specific)
  identity_blocks: {
    // Different structure per business_type
  }
  
  // CTA configuration
  primary_cta: string
  secondary_ctas: array
}
```

**Block Visibility Logic:**
```javascript
function shouldShowBlock(block, data) {
  // Hide if no data
  if (!data || data.length === 0) return false;
  
  // Hide if not applicable for business type
  if (!isBlockApplicable(block, businessType)) return false;
  
  return true;
}
```

### 6.2 Scalability Considerations / Масштабируемость

**Future Features:**
- Booking system integration
- Payment processing
- Subscription management
- Crypto rewards
- NFT certifications
- AI recommendations

**New Business Types:**
Can be added by:
1. Defining Identity blocks
2. Setting CTA priority
3. Creating onboarding hints
4. No changes to Universal blocks

### 6.3 Legal & Privacy / Юридические аспекты

**GDPR Compliance:**
- Business contact info requires consent
- User reviews need moderation
- Data export available
- Right to be forgotten

**Business Verification:**
- Optional verification badge
- Document verification process
- Trust & safety measures

---

## 7. User Flows / Пользовательские сценарии

### 7.1 Business Owner Flow / Сценарий владельца

1. **Choose Business Type** → See onboarding hint → Understand what to expect
2. **Fill Universal Info** → Name, description, contact, location
3. **Fill Identity Info** → Type-specific blocks (e.g., services for Specialist)
4. **Configure CTAs** → Select primary and secondary actions
5. **Publish Profile** → Profile goes live with adaptive UI

### 7.2 User (Visitor) Flow / Сценарий посетителя

1. **Land on Profile** → See business type, name, primary CTA
2. **Understand Instantly** → Type badge + primary CTA = clear intent
3. **Explore Identity Blocks** → See unique info relevant to this type
4. **Take Action** → Click primary CTA (book, buy, enroll, etc.)
5. **Check Universal Info** → Reviews, contact, posts if needed

---

## 8. Design System Integration / Интеграция дизайн-системы

### 8.1 Components / Компоненты

**Universal Components:**
- ProfileHeader
- AboutBlock
- ContactBlock
- ReviewsBlock
- PostsBlock
- MediaGallery

**Identity Components (lazy loaded):**
- ServicesBlock (Specialist, Services)
- CoursesBlock (Education)
- ProductCatalog (Products)
- ActivitiesCatalog (Activities & Travel)
- SolutionsBlock (B2B)
- etc.

### 8.2 Adaptive Layout / Адаптивная верстка

**Desktop:**
```
[Header with 2-4 CTAs]
[About + Identity Blocks in 2 columns]
[Universal Blocks below]
```

**Mobile:**
```
[Header with max 2 CTAs]
[Identity Blocks (stacked)]
[Universal Blocks (stacked)]
```

### 8.3 Loading Strategy / Стратегия загрузки

1. **Critical:** Header, primary CTA, business name (instant)
2. **Above Fold:** About, first identity block (fast)
3. **Progressive:** Other identity blocks, universal blocks (lazy)
4. **Deferred:** Reviews, media gallery (on scroll)

---

## 9. Success Metrics / Метрики успеха

### For Users / Для пользователей:
- **Time to Action** < 5 seconds (from landing to CTA click)
- **Profile Completion Rate** > 80% understand business instantly
- **CTA Click Rate** > 15% of visitors

### For Businesses / Для бизнесов:
- **Profile Completion** > 90% fill all identity blocks
- **Lead Generation** increased by 30% vs generic profiles
- **User Engagement** +50% time spent on profile

---

## 10. Conclusion / Заключение

Эта архитектура создает **адаптивную, масштабируемую и понятную систему** бизнес-профилей для Bestme. Каждый тип бизнеса получает уникальную идентичность, сохраняя при этом целостность платформы через универсальные блоки.

**Key Achievements / Ключевые достижения:**
- ✅ 7 business types supported / 7 типов бизнеса
- ✅ Clear identity per type / Четкая идентичность
- ✅ No duplication / Нет дублирования
- ✅ Scalable architecture / Масштабируемая архитектура
- ✅ User-centric design / Фокус на пользователе
- ✅ Social network context / Контекст соцсети

**Ready for:** Design, Development, and Implementation
**Готово к:** Дизайну, разработке и внедрению

