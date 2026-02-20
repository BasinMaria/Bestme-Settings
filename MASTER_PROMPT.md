# Master Prompt: Bestme Settings & Business Profile System

## Project Overview / Обзор проекта

**Project Name:** Bestme Settings & Business Profile System  
**Platform:** Bestme - Social network for self-development and wellness  
**Focus:** User settings architecture & Business profile system  

**Bestme** - это социальная сеть про саморазвитие и благополучие, где люди:
- Ставят еженедельные цели (goals)
- Читают контент (блоги)
- Общаются в сообществе
- Ведут личный профиль или бизнес-профиль

**6 Wellness Categories / 6 категорий здорового образа жизни:**
1. 🍎 Healthy Eating / Здоровое питание
2. 💪 Physical Activity / Физическая нагрузка
3. 🧘 Mental Balance / Душевное равновесие
4. ✨ Aesthetics & Hygiene / Эстетика и гигиена
5. 🌍 Environment / Окружающая среда
6. ⏰ Daily Routine / Режим дня

---

## Complete Deliverables / Все документы (24 files)

### 1. Settings Structures (6 files) / Структуры настроек

**Core Settings Documentation:**

1. **SETTINGS_FIRST_SCREEN.md** - First screen with 7 main menu items
2. **PRIVACY_STRUCTURE.md** - Complete privacy settings (28 settings)
3. **NOTIFICATIONS_STRUCTURE.md** - Notifications system (17 controls)
4. **ACCOUNT_STRUCTURE.md** - Account management (17 features)
5. **CONTENT_STRUCTURE.md** - Content & interactions (16 settings)
6. **FRIENDS_COMMUNITY_STRUCTURE.md** - Social networking (23 features)

**Total: 116+ individual settings documented**

### 2. Business Profile System (3 files) / Система бизнес-профилей

**Business Architecture:**

1. **BUSINESS_PROFILE_ARCHITECTURE.md** - 7 business types architecture
2. **BUSINESS_ACCOUNT_CREATION_FLOW.md** - 6-step creation process
3. **BUSINESS_TYPE_CATEGORY_MATRIX.md** - 42 adaptive combinations

### 3. Supporting Documentation (15 files) / Поддерживающая документация

**Guidelines & References:**
- README.md - Project overview
- BILINGUAL_UI_GUIDELINES.md - UI text format rules
- STRUCTURE_GUIDE.md - Structure breakdown
- UPDATE_GUIDE.md - Maintenance instructions
- VALIDATION.md - Validation checklist
- CHANGELOG.md - Version tracking
- INDEX.md - Navigation guide
- SUMMARY.md - Quick overview
- QUICK_REFERENCE.md - Quick reference
- COMPARISON_V1_V2.md - Version comparison
- ANALYSIS_V1_TO_V2.md - Evolution analysis
- STRUCTURE_V2.md - v2.0 structure
- PROJECT_SUMMARY_V2.md - v2.0 summary
- ProfileSettings.drawio.html - Visual diagram (draw.io)
- .gitignore - Repository management

---

## Settings Structure Summary / Сводка по настройкам

### 6 Main Sections (116 settings total):

#### 1. 📱 Profile / Профиль (15 fields)
**Sections:**
- Edit Profile (8 fields): Avatar, Status, Cover, Name, Last Name, Bio, Birthday, Gender
- Contact Info (4 fields): Phone, Email, Location, Address
- Personal Links (1 field): Blog Link
- Interests (2 fields): Categories, Goals

**Format:**
All contact fields have privacy toggles (PUBLIC/FRIENDS_ONLY/PRIVATE)

#### 2. 🔒 Privacy / Приватность (28 settings)
**Sections:**
- Account Privacy (15 fields): Profile page, Name, Avatar, Cover, Bio, Birthday, Gender, Email, Phone, Location, Address, Personal Links, Blog Link, Business Link
- Content Visibility (6 fields): Posts, Media Gallery, Friends List, Categories, Subscribed Blogs, Subscribed Communities
- Interactions (5 fields): Messages, Tags, Comments, Sharing, Friend Requests
- Activity Status (2 fields): Online Status, Last Seen
- Blocking & Muting (3 sections): Blocked, Muted, Restricted

**Legal Compliance:**
- GDPR (EU): Articles 6, 9, 15, 17, 20
- CCPA (California, USA)
- PIPEDA (Canada)
- CAN-SPAM Act (USA)
- TCPA (USA)
- COPPA (USA)

#### 3. 👥 Friends & Community / Друзья и сообщество (23 features)
**Sections:**
- Friends Management (5): Friends List (245 friends), Add, Remove, Requests, Close Friends
- Followers & Subscriptions (4): Your Followers, Your Following, Manage, Follow Requests
- Subscriptions (3): Blogs, Business Accounts, Unsubscribe
- Communities (5): My Communities, Create, Invitations, Manage, Leave
- Network Search & Discovery (4): Find Friends, Discover People, Suggested Communities, Suggested Blogs
- Suggestions (2): Friend Suggestions, Hide Suggestions

#### 4. 🔔 Notifications / Уведомления (17 controls)
**Sections:**
- Push Notifications (1 master + 7 types): Likes, Comments, Followers, Messages, Mentions, Friend Requests, Live Videos
- Email Notifications (4 types): Activity Summary (Never/Daily/Weekly), Reminders, Product Updates, Newsletter
- In-App Settings (3): Sound, Vibration, Badge Count

**Defaults:**
- Most ON by default (13 settings)
- OFF: Live Videos, Newsletter

#### 5. 💬 Content & Interactions / Контент (16 settings)
**Sections:**
- Posts Settings (3): Default Audience, Auto-Archive, Hide Likes
- Stories Settings (4): Allow Sharing, Hide From, Save to Archive, Duration
- Saved & Collections (3): Saved Posts, Collections, Saved Stories
- Media Settings (3): Upload Quality (High/Data Saver), Auto-Play Videos, HD Video
- Feed Preferences (3): Suggested Posts, Sensitive Content, Favorite Accounts

#### 6. ⚙️ Account / Аккаунт (17 features)
**Sections:**
- Login & Security (5): Change Password, 2FA, Active Sessions, Login Activity, Authorized Apps
- App Preferences (4): Language (English/Русский), Theme (Light/Dark/Auto), Accessibility (3 options), Data Saver
- Data Management (4): Download Your Data, Data Permissions, Account Status (Deactivate/Delete), Help & Support
- Business Account (2): Switch to Business, Create Business Account
- Log Out (1): Log out (everywhere/this device)

---

## Business Profile System / Система бизнес-профилей

### 7 Business Types / 7 типов бизнеса

1. **🎯 Specialist / Специалист**
   - Primary CTA: Book / Записаться
   - Identity: Personal services, consultations
   - Examples: Psychologist, Coach, Nutritionist, Trainer

2. **📍 Place / Место**
   - Primary CTA: Visit / Посетить
   - Identity: Physical location, venue
   - Examples: Restaurant, Gym, Studio, Cafe, Salon

3. **🎓 Education / Образование**
   - Primary CTA: Enroll / Записаться на курс
   - Identity: Courses, learning programs
   - Examples: School, Courses, Training, Workshops

4. **🔧 Services / Сервисы**
   - Primary CTA: Get Quote / Получить расчет
   - Identity: Professional services
   - Examples: Design, Consulting, Repair

5. **🛍️ Products / Товары**
   - Primary CTA: Shop / Магазин
   - Identity: E-commerce, catalog
   - Examples: Healthy products, Supplements, Cosmetics

6. **✈️ Activities & Travel / Активности и путешествия**
   - Primary CTA: Activities / Активности
   - Identity: Tours, retreats, experiences
   - Examples: Retreats, Tours, Excursions, Workshops

7. **💼 B2B Services / B2B Сервисы**
   - Primary CTA: Request Demo / Запросить демо
   - Identity: Business solutions
   - Examples: SaaS, Corporate Wellness, Consulting

### Universal Blocks (for ALL business types):
- Reviews / Отзывы
- Contact / Контакты
- Posts / Посты
- Media Gallery / Медиа галерея
- Location/Address (optional)
- Online/Offline/Hybrid format
- Opening Hours (if provided)
- About / О нас

### Adaptive System: Type × Category

**42 Combinations = 7 Business Types × 6 Categories**

**Example Combinations:**

**Place × Healthy Eating = Restaurant:**
- Menu / Меню
- Dietary Options / Диетические опции
- Cuisine Type / Тип кухни
- NOT Portfolio, NOT Equipment

**Place × Physical Activity = Gym:**
- Equipment List / Оборудование
- Classes Schedule / Расписание
- Membership Plans / Тарифы
- NOT Menu, NOT Cuisine

**Specialist × Mental Balance = Therapist:**
- Therapy Approaches / Подходы
- Specializations / Специализации
- Session Types / Типы сессий
- NOT Products, NOT Menu

**Products × Aesthetics = Beauty Products:**
- Product Catalog / Каталог
- Ingredients / Состав
- Skin Types / Типы кожи
- NOT Services, NOT Classes

---

## Business Account Creation Flow / Флоу создания

### 6-Step Process:

**Step 1: Entry Point / Точка входа**
- From: Personal Account → Settings → Account → "Create Business Account"

**Step 2: Introduction Screen / Введение**
- Welcome message
- Benefits explanation
- "Continue" button

**Step 3: Business Type Selection / Выбор типа** ⭐
- 7 cards with business types
- Each card: Icon + Name + Description + Example
- User selects ONE type
- Cannot be changed after creation

**Step 4: Primary Information / Основная информация** ⭐
**REQUIRED fields:**
- Business Name / Название (3-100 chars, unique)
- Description / Описание (100-500 chars)
- Format / Формат (Online/Offline/Hybrid)
- Contact / Контакт (Phone OR Email)
- Location (if Offline/Hybrid)

**OPTIONAL:**
- Avatar / Аватар
- Cover Photo / Обложка

**Step 5: Identity Information / Уникальная информация** ⭐
**Type-specific optional fields:**
- Specialist: Services, Certifications, Calendar
- Place: Amenities, Capacity, Menu
- Education: Courses, Schedule, Certifications
- Services: Services, Pricing, Portfolio
- Products: Catalog, Shipping, Returns
- Activities: Activities, Dates, Difficulty
- B2B: Solutions, Case Studies, Pricing Tiers

**Can skip all and add later**

**Step 6: Review & Publish / Проверка**
- Preview profile
- Edit any section
- "Publish" button
- Profile goes live immediately

### Business Type Badge / Бейдж

**What:** Visual indicator (icon + text) like 🎯 Specialist  
**Where:** Profile header, next to business name  
**When:** AFTER publishing (not during creation)  
**Why:** Quick category recognition, sets user expectations  

### Information Hierarchy:

**PRIMARY (required for publishing):**
- Business Name
- Business Type
- Description
- Format
- Contact

**SECONDARY (optional, recommended):**
- Avatar, Cover Photo
- Location (if Offline/Hybrid)
- Opening Hours
- Social Links

**TERTIARY (add anytime):**
- Identity blocks (type-specific)
- Media Gallery
- Posts
- Reviews (user-generated)

---

## Working Rules / Правила работы

### 1. Ask First, Don't Assume / Сначала спроси
✅ If something is unclear, ask questions  
✅ Don't just do things without understanding  
✅ Always confirm before making changes  

### 2. Bilingual Approach / Двуязычный подход
✅ Interface text in **English**  
✅ Russian annotations for context and clarity  
✅ Format: `English Text / Русское пояснение`  
✅ Examples: `Profile / Профиль`, `Settings / Настройки`  

### 3. No Unauthorized Changes / Никаких несанкционированных изменений
✅ **Don't delete** anything without permission  
✅ **Don't add** anything without permission  
✅ If something seems unnecessary → **ask first**  
✅ If something needs to be added → **ask for approval first**  

### 4. Focus on Naming and UI / Фокус на названиях и UI
✅ Clear, consistent naming is critical  
✅ UI/UX is primary concern  
✅ Professional English interface + user-friendly Russian context  

### 5. Legal Compliance / Соответствие законам
✅ Must comply with laws: EU (GDPR), USA (COPPA, CAN-SPAM, TCPA), Canada (PIPEDA, CASL), Israel, California (CCPA)  
✅ Privacy by default  
✅ User control over data  
✅ Transparency in data usage  

### 6. Social Network Context / Контекст соцсети
✅ This is a social network, not a marketplace  
✅ Focus on regular user profiles first  
✅ Business features are extensions, not core  
✅ User-generated content is important  
✅ Community and connection matter  

---

## Usage Instructions / Инструкции по использованию

### How to Use This Prompt:

**1. For New Features:**
```
Context: Working on Bestme Settings project
Reference: MASTER_PROMPT.md
Task: [Describe new feature]
Requirements: Follow working rules, maintain bilingual format
```

**2. For Updates:**
```
Context: Updating [specific section] in Bestme Settings
Reference: See [relevant .md file]
Changes needed: [List changes]
Approval: [Yes/No - waiting for approval]
```

**3. For Onboarding:**
- Read MASTER_PROMPT.md (this file)
- Review SUMMARY.md for quick overview
- Check INDEX.md for navigation
- Read specific structure files as needed

**4. For Design:**
- Use structures as wireframe reference
- Follow bilingual UI guidelines
- Implement adaptive business system
- Validate against VALIDATION.md

**5. For Development:**
- Reference variable names in structures
- Implement validation rules
- Follow database schema examples
- Test against legal requirements

---

## Key Statistics / Ключевая статистика

### Documentation:
- **Total Files:** 24 documents
- **Total Size:** ~420KB
- **Settings Documented:** 116+
- **Business Combinations:** 42 (7 types × 6 categories)
- **Languages:** 100% bilingual (English / Russian)

### Coverage:
- ✅ 6 Settings sections complete
- ✅ 7 Business types documented
- ✅ 6 Wellness categories integrated
- ✅ Legal compliance (5 jurisdictions)
- ✅ Creation flow (6 steps)
- ✅ Validation rules
- ✅ Implementation examples

### Quality:
- ✅ Professional UX language
- ✅ Structured documentation
- ✅ Scannable format
- ✅ Actionable information
- ✅ Consistent formatting
- ✅ Ready for implementation

---

## Next Steps / Следующие шаги

### For Design Team:
1. Create visual mockups based on structures
2. Design 7 business type templates
3. Prototype 6-step creation flow
4. Design badge variations
5. Create adaptive UI components

### For UX Team:
1. Conduct user testing on structures
2. Test business type selection flow
3. Validate information hierarchy
4. Test Category × Type combinations
5. Measure task completion times

### For Development Team:
1. Implement database schema
2. Build settings API endpoints
3. Create business profile system
4. Implement validation rules
5. Build adaptive UI logic
6. Integrate legal compliance

### For Product Team:
1. Plan rollout strategy
2. Create marketing materials
3. Prepare onboarding content
4. Define success metrics
5. Plan A/B tests

### For Legal Team:
1. Review privacy settings
2. Validate GDPR compliance
3. Check COPPA requirements
4. Verify data handling
5. Approve legal disclaimers

---

## File Structure / Структура файлов

```
Bestme-Settings/
│
├── Settings Structures (6 files)
│   ├── SETTINGS_FIRST_SCREEN.md
│   ├── PRIVACY_STRUCTURE.md
│   ├── NOTIFICATIONS_STRUCTURE.md
│   ├── ACCOUNT_STRUCTURE.md
│   ├── CONTENT_STRUCTURE.md
│   └── FRIENDS_COMMUNITY_STRUCTURE.md
│
├── Business Profile (3 files)
│   ├── BUSINESS_PROFILE_ARCHITECTURE.md
│   ├── BUSINESS_ACCOUNT_CREATION_FLOW.md
│   └── BUSINESS_TYPE_CATEGORY_MATRIX.md
│
├── Guidelines & Support (15 files)
│   ├── README.md
│   ├── MASTER_PROMPT.md (this file)
│   ├── BILINGUAL_UI_GUIDELINES.md
│   ├── STRUCTURE_GUIDE.md
│   ├── UPDATE_GUIDE.md
│   ├── VALIDATION.md
│   ├── CHANGELOG.md
│   ├── INDEX.md
│   ├── SUMMARY.md
│   ├── QUICK_REFERENCE.md
│   ├── COMPARISON_V1_V2.md
│   ├── ANALYSIS_V1_TO_V2.md
│   ├── STRUCTURE_V2.md
│   ├── PROJECT_SUMMARY_V2.md
│   └── ProfileSettings.drawio.html
│
└── Repository Files
    └── .gitignore
```

---

## Success Criteria / Критерии успеха

### For Users:
✅ Find any setting in under 30 seconds  
✅ Understand privacy options clearly  
✅ Complete business profile in under 10 minutes  
✅ Feel confident about data control  

### For Business:
✅ 95%+ profile completion rate  
✅ 50% reduction in support tickets  
✅ 4.5+ star user satisfaction  
✅ Legal compliance verified  

### For Platform:
✅ Scalable architecture  
✅ Easy to maintain  
✅ Extensible for new features  
✅ Well-documented  

---

## Contact & Contribution / Контакт и вклад

**Project Repository:** BasinMaria/Bestme-Settings  
**Branch:** copilot/progressive-settings-structure  

**For Questions:**
- Review relevant .md file first
- Check INDEX.md for navigation
- Read SUMMARY.md for quick overview

**For Changes:**
- Follow working rules
- Get approval before major changes
- Update CHANGELOG.md
- Maintain bilingual format

---

**Last Updated:** 2026-02-20  
**Version:** 2.0  
**Status:** Production-ready documentation  

---

## Quick Reference / Быстрая справка

**Settings:**
- Profile (15) + Privacy (28) + Friends (23) + Notifications (17) + Content (16) + Account (17) = **116 settings**

**Business:**
- 7 Types × 6 Categories = **42 combinations**

**Files:**
- 6 Settings + 3 Business + 15 Support = **24 files**

**Languages:**
- English (Interface) + Russian (Context) = **100% bilingual**

**Compliance:**
- EU + USA + Canada + Israel + California = **5 jurisdictions**

---

**🎉 Complete documentation ready for implementation!**  
**🎉 Полная документация готова к внедрению!**
