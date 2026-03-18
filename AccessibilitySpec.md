# AccessibilitySpec.md — Полное ТЗ раздела «Accessibility» (Доступность)

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Дизайнер, iOS-разработчик, Android-разработчик, Backend-разработчик  
**Статус:** 🔴 Обязательно для публикации (App Store §2.5.4 + Google Play + EAA с 28.06.2025)

> **Главный принцип:** Все настройки Accessibility — это **UI-уровень** (размер шрифта, контраст, подписи). Автоматические субтитры к видео пользователей (UGC) **НЕ требуются** ни одним из перечисленных законов.

---

## Содержание

1. [Зачем это нужно (законы и магазины)](#1-зачем-это-нужно)
2. [Где находится в навигации](#2-где-находится-в-навигации)
3. [Полный список настроек — ТЗ на каждую](#3-полный-список-настроек)
4. [Кнопка Contact DPO](#4-кнопка-contact-dpo)
5. [Технические требования для разработчика](#5-технические-требования)
6. [Чеклист публикации](#6-чеклист-публикации)

---

## 1. Зачем это нужно

| Закон / Правило | Требование | Штраф / Последствие |
|---|---|---|
| **EAA 2019/882** (ЕС, с 28.06.2025) | Приложения должны обеспечивать доступность по WCAG 2.1 уровня AA | До €10 млн или запрет продаж в ЕС |
| **ADA** (США, Закон об инвалидах) | Цифровые продукты, открытые для публики, должны быть доступны | Судебный иск, от $4 000 за нарушение |
| **Israel Disability Law 5758-1998** | Равный доступ для людей с инвалидностью к цифровым услугам | Административный штраф |
| **AODA (Канада)** | Стандарт доступности для онтарийских организаций, WCAG 2.0 AA | Штраф до $100 000/день |
| **California Unruh Civil Rights Act §51** | Запрет дискриминации в публичных заведениях (включает приложения) | Штраф $4 000 за нарушение + ущерб |
| **App Store §2.5.4** | Приложения должны корректно работать с VoiceOver и Dynamic Type | Отклонение при ревью |
| **Google Play** | Accessibility Best Practices — рекомендует поддержку TalkBack и крупного текста | Может стать причиной отклонения |

**Итог:** Accessibility Settings нужен для прохождения ревью App Store + защиты от исков в США, Израиле, Канаде и соблюдения EAA в ЕС с июня 2025.

---

## 2. Где находится в навигации

```
Settings (главный экран)
└── Accessibility (L1 — 8-й раздел)
    ├── Text size                    (переключатель)
    ├── Bold text                    (toggle)
    ├── High contrast mode           (toggle)
    ├── Reduce motion                (toggle)
    ├── Closed captions (videos)     (toggle)
    ├── Auto-generate alt text       (toggle)
    ├── Screen reader information    (ссылка/информация)
    ├── Keyboard navigation info     (ссылка/информация)
    └── Contact DPO                  (кнопка — см. §4)
```

**Путь в приложении:** Settings → Accessibility  
**Иконка раздела:** ♿ или глаз / человечек с коляской  

---

## 3. Полный список настроек

---

### 3.1 Text Size — Размер текста

| Параметр | Значение |
|---|---|
| **variable_name** | `text_size` |
| **Тип** | ENUM (сегментированный контрол или слайдер) |
| **Значения** | `small` · `normal` · `large` · `xl` |
| **Default** | `normal` |
| **WCAG** | 1.4.4 Resize Text (уровень AA) |
| **Законы** | EAA · ADA · Israel Disability Law · AODA |

**Что это:** Пользователь выбирает базовый размер шрифта в приложении. Это отдельная настройка **внутри приложения** — она работает независимо от системного размера шрифта (iOS Dynamic Type / Android Font Scale), но **должна также уважать системный размер**.

**Почему нужно:**  
- WCAG 1.4.4 требует, чтобы текст можно было увеличить до 200% без потери контента или функциональности.  
- App Store §2.5.4 проверяет поддержку Dynamic Type — если крупный шрифт ломает верстку, приложение могут отклонить.

**Что делает разработчик:**
- iOS: читать `UIApplication.shared.preferredContentSizeCategory` и дополнительно предоставлять собственный слайдер. Хранить `text_size` в UserDefaults + синхронизировать с сервером.
- Android: читать `Configuration.fontScale` + собственный регулятор. Хранить в SharedPreferences.
- Сервер: хранить в `user_settings.text_size`. Синхронизировать при смене устройства.

**UI-поведение:** При изменении значения — немедленное применение ко всем текстам в приложении (без перезагрузки). Все шрифты в приложении должны использовать относительные единицы (sp на Android, Dynamic Type на iOS).

---

### 3.2 Bold Text — Жирный текст

| Параметр | Значение |
|---|---|
| **variable_name** | `bold_text_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `false` |
| **WCAG** | 1.4.3 Contrast (Minimum) — жирный текст улучшает читаемость |
| **Законы** | EAA · ADA · Israel Disability Law |

**Что это:** Когда включено — весь основной текст в приложении переключается на жирное начертание (font-weight: bold / 700). Помогает пользователям со слабым зрением.

**Почему нужно:**  
- Жирный текст при том же размере имеет лучший воспринимаемый контраст.
- iOS имеет системную настройку «Bold Text» — приложение должно её уважать (`UIAccessibility.isBoldTextEnabled`).

**Что делает разработчик:**
- iOS: подписаться на `UIAccessibility.boldTextStatusDidChangeNotification`. Если системная настройка включена — применять независимо от настройки приложения.
- Android: применять `Typeface.DEFAULT_BOLD` к основным текстовым стилям через Theme.
- Сервер: хранить в `user_settings.bold_text_enabled`.

**UI-поведение:** Немедленное применение при переключении.

---

### 3.3 High Contrast Mode — Высокий контраст

| Параметр | Значение |
|---|---|
| **variable_name** | `high_contrast_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `false` |
| **WCAG** | 1.4.3 Contrast Minimum — 4.5:1 для обычного текста, 3:1 для крупного (≥18pt) |
| **Законы** | EAA · ADA · Israel Disability Law |

**Что это:** Когда включено — приложение переключается на высококонтрастную цветовую схему. Например, фон #FFFFFF, текст #000000, акцентный цвет меняется на более тёмный.

**Почему нужно:**  
- WCAG 1.4.3 требует минимальный контраст 4.5:1 для нормального текста. Многие дизайн-системы используют пастельные цвета, которые не соответствуют этому требованию.  
- EAA с 28.06.2025 требует соответствия WCAG 2.1 AA — это одно из первых, что проверяет аудитор.

**Что делает разработчик:**
- Создать отдельный `HighContrastTheme` / `ColorScheme` с проверенными цветами (контраст ≥4.5:1).
- iOS: уважать `UIAccessibility.isDarkerSystemColorsEnabled` системную настройку.
- Android: уважать `Configuration.UI_MODE_NIGHT_NO` + проверять `AccessibilityManager`.
- При включении — применять `HighContrastTheme` к корневому View.

**Что проверить:** Использовать инструмент [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/) или встроенный Accessibility Inspector (Xcode) для проверки 4.5:1.

---

### 3.4 Reduce Motion — Уменьшить движение

| Параметр | Значение |
|---|---|
| **variable_name** | `reduce_motion_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `false` |
| **WCAG** | 2.3.1 Three Flashes or Below Threshold · 2.3.3 Animation from Interactions |
| **Законы** | EAA · ADA |

**Что это:** Когда включено — все анимации в приложении (переходы между экранами, появление элементов, параллакс-эффекты, пульсация) упрощаются или отключаются. Для людей с вестибулярными расстройствами, эпилепсией и фоточувствительностью.

**Почему нужно:**  
- WCAG 2.3.3 (WCAG 2.1, уровень AAA, но EAA требует AA+) запрещает интерфейсные анимации без возможности отключения.
- WCAG 2.3.1 прямо запрещает содержимое, мигающее более 3 раз в секунду.

**Что делает разработчик:**
- iOS: читать `UIAccessibility.isReduceMotionEnabled` и уважать его **до** проверки настройки приложения.
- Android: читать `Settings.Global.ANIMATOR_DURATION_SCALE` и устанавливать его в 0 при включении.
- Конкретно: отключить Lottie-анимации, заменить `push/pop` анимации на fade, убрать parallax scroll.

---

### 3.5 Closed Captions (Videos) — Субтитры к видео

| Параметр | Значение |
|---|---|
| **variable_name** | `captions_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `true` |
| **WCAG** | 1.2.2 Captions (Prerecorded) |
| **Законы** | EAA · ADA · AODA |

**Что это:** Переключатель, который управляет отображением субтитров в **системных/обучающих видео приложения** (onboarding-видео, туториалы, Help-видео). При включении — субтитры показываются поверх видеоплеера.

### ❗ ВАЖНО: Что включает, а что нет

| Что | Субтитры нужны? |
|---|---|
| Onboarding-видео (ваш контент) | ✅ **Да** — нужны субтитры |
| Help & Support видео (ваш контент) | ✅ **Да** — нужны субтитры |
| Видео от пользователей (UGC) | ❌ **Нет** — вы не обязаны автоматически добавлять субтитры к видео, которые загрузили пользователи. TikTok делает это как маркетинговую фичу, не как требование закона |
| Видео в новостной ленте (UGC) | ❌ **Нет** |

**Почему значение по умолчанию `true`:**  
По WCAG 1.2.2 субтитры к записанным видео **обязательны** (уровень A). Если у вас есть хоть одно обучающее видео в приложении — субтитры должны быть доступны и включены по умолчанию.

**Что делает разработчик:**
- Для каждого системного видео в приложении: добавить VTT/SRT файл субтитров.
- Видеоплеер должен читать `captions_enabled` и показывать/скрывать треки субтитров.
- iOS: использовать `AVPlayer` + `AVMediaSelectionGroup` для subtitle tracks.
- Android: использовать `ExoPlayer` + `CueGroup` для subtitle tracks.
- Для UGC видео: добавить возможность для создателя контента загрузить свои субтитры (опционально, не обязательно).

---

### 3.6 Auto-Generate Alt Text — Автоматический alt-текст для фото

| Параметр | Значение |
|---|---|
| **variable_name** | `alt_text_auto_enabled` |
| **Тип** | Boolean (toggle) |
| **Default** | `true` |
| **WCAG** | 1.1.1 Non-text Content |
| **Законы** | EAA · ADA · Israel Disability Law |

**Что это:** Когда включено и пользователь загружает фото — приложение **автоматически генерирует описание** изображения (alt text) с помощью ML/AI, которое читает screen reader. Когда выключено — пользователь может добавить alt text вручную или не добавлять.

**Почему нужно:**  
- WCAG 1.1.1 требует, чтобы все нетекстовые элементы (изображения) имели текстовую альтернативу.
- Screen readers (VoiceOver, TalkBack) зачитывают alt text для незрячих пользователей.
- Это **особенно важно** для соцсети, где пользователи публикуют фото.

**Что делает разработчик:**
- При загрузке фото: вызвать Vision API / ML-модель для генерации описания.
- iOS: `VNGenerateImageFeaturePrintRequest` или Apple's Vision framework.
- Android: Google ML Kit `ImageLabeling` или Cloud Vision API.
- Хранить alt text в `media.alt_text` в базе данных.
- При рендеринге фото: передавать `contentDescription` (Android) / `accessibilityLabel` (iOS).
- Разрешить пользователю отредактировать или удалить автоматически сгенерированный alt text.

---

### 3.7 Screen Reader Information — Информация для скринридеров

| Параметр | Значение |
|---|---|
| **variable_name** | — (информационная ссылка, не настройка) |
| **Тип** | Статичная строка + иконка "i" или кнопка «Подробнее» |
| **Default** | — |
| **WCAG** | 4.1.3 Status Messages |
| **Законы** | EAA · ADA · App Store §2.5.4 |

**Что это:** Информационный блок в разделе Accessibility, который объясняет, что приложение поддерживает VoiceOver (iOS) и TalkBack (Android), и даёт ссылки на руководства по использованию этих технологий.

**Почему нужно:**  
- App Store §2.5.4 проверяет, что приложение работает с VoiceOver. Наличие явной секции Screen Reader в настройках — хороший сигнал для ревьюера.
- Пользователи со скринридером должны знать, что приложение поддерживается.

**Что отображать:**
```
📱 Screen Reader Support
This app is compatible with VoiceOver (iOS) and TalkBack (Android).
All buttons, images, and form fields have accessibility labels.

[Learn how to use VoiceOver →]   (ссылка на support.apple.com)
[Learn how to use TalkBack →]    (ссылка на support.google.com)
```

**Что делает разработчик:**
- Добавить `accessibilityLabel` ко **всем** кнопкам-иконкам, изображениям, переключателям, полям ввода.
- Для иконок без текста: обязательный `accessibilityLabel` (iOS) / `contentDescription` (Android).
- Для декоративных изображений: `accessibilityElementsHidden = true` (iOS) / `importantForAccessibility="no"` (Android).
- Протестировать весь основной поток в приложении с включённым VoiceOver/TalkBack.

---

### 3.8 Keyboard Navigation Info — Информация о клавиатурной навигации

| Параметр | Значение |
|---|---|
| **variable_name** | — (информационная ссылка, не настройка) |
| **Тип** | Статичная строка + иконка "i" |
| **Default** | — |
| **WCAG** | 2.1.1 Keyboard · 2.1.2 No Keyboard Trap |
| **Законы** | EAA · ADA |

**Что это:** Информационный блок для пользователей, которые используют внешнюю клавиатуру (подключённую к iPad или Android-планшету) или Switch Control. Объясняет, что все функции доступны без тачскрина.

**Почему нужно:**  
- WCAG 2.1.1 требует, чтобы ВСЯ функциональность была доступна с клавиатуры.
- EAA требует поддержку внешних устройств ввода.

**Что отображать:**
```
⌨️ Keyboard & External Device Navigation
All features are accessible using an external keyboard or switch control.
Use Tab to navigate, Enter/Space to activate, Escape to close dialogs.
```

**Что делает разработчик:**
- iOS: убедиться, что все `UIControl`-элементы focusable через UIFocusEnvironment (для iPad + внешняя клавиатура).
- Android: убедиться, что все интерактивные элементы имеют `focusable="true"` и правильный tab order (`nextFocusDown`, `nextFocusRight`).
- Проверить, что нет «ловушек фокуса» (WCAG 2.1.2) — модальные окна должны держать фокус внутри себя, но при закрытии возвращать фокус на элемент, который их открыл.

---

## 4. Кнопка Contact DPO

### Что это и зачем

**DPO (Data Protection Officer)** — Ответственный за защиту данных. По GDPR Art.37 организации, обрабатывающие данные в большом масштабе, обязаны назначить DPO и сделать его контакт доступным для пользователей.

**Почему это в Accessibility:** DPO контакт размещают в разных местах — в Privacy Policy, в разделе «Your Data», иногда в Accessibility (поскольку EAA тоже требует контактной точки для жалоб на доступность). Оптимальное размещение — в разделе **Help & Support** ИЛИ **Your Data**, но ссылка должна быть и в Privacy Policy.

**Рекомендация:** Разместить кнопку Contact DPO в двух местах:
1. Settings → Help & Support → Contact DPO ✅ (основное)
2. Settings → Your Data → Contact DPO ✅ (дублирование для GDPR)

### ТЗ для кнопки Contact DPO

| Параметр | Значение |
|---|---|
| **Путь** | Settings → Help & Support → Contact DPO |
| **Тип** | Кнопка → открывает email-клиент или in-app форму |
| **Действие** | `mailto:dpo@bestme.app` или форма с полями: тема, сообщение |
| **Закон** | GDPR Art.37(7) — контакт DPO должен быть опубликован |
| **Quebec L25** | Art.5 — требует назначить Privacy Officer с публичным контактом |

**Что показать при нажатии:**
```
📧 Contact our Data Protection Officer

Your message goes directly to our Data Protection Officer.
You can contact us regarding:
• Requests to access, correct, or delete your data
• Questions about how we use your data
• Concerns about data privacy practices
• Accessibility-related complaints

Email: dpo@bestme.app
Response time: within 30 days (as required by GDPR Art.12)

[Send Email]    [Open Form]
```

**Что делает разработчик:**
- Кнопка «Send Email» → `UIApplication.shared.open(URL(string: "mailto:dpo@bestme.app")!)`
- Кнопка «Open Form» → WebView с формой на сайте (bestme.app/contact-dpo)
- Или in-app форма с полями: Имя (optional), Email, Тема (dropdown), Сообщение.
- Backend: отправлять на dpo@bestme.app + логировать запрос в compliance-журнале.

### Важно: нужен ли ФИЗИЧЕСКИЙ DPO?

| Ситуация | Требование |
|---|---|
| Компания в ЕС или обрабатывает данные граждан ЕС в большом масштабе | ✅ DPO обязателен (GDPR Art.37(1)(b)) |
| Стартап / малый бизнес, не основная деятельность — обработка данных | ⚠️ DPO рекомендован, но не всегда обязателен |
| Quebec L25 (Канада) | ✅ Privacy Officer обязателен для организаций любого размера |

**Минимальный вариант для стартапа:** Назначить основателя/CEO как Privacy Officer → указать его email → зарегистрировать в реестре GDPR (если применимо).

---

## 5. Технические требования для разработчика

### Хранение настроек

```
Таблица: user_settings
Поля:
  text_size             ENUM('small','normal','large','xl')   DEFAULT 'normal'
  bold_text_enabled     BOOLEAN                               DEFAULT false
  high_contrast_enabled BOOLEAN                               DEFAULT false
  reduce_motion_enabled BOOLEAN                               DEFAULT false
  captions_enabled      BOOLEAN                               DEFAULT true
  alt_text_auto_enabled BOOLEAN                               DEFAULT true
```

### Синхронизация

- Все настройки хранятся на сервере и синхронизируются при входе на новом устройстве.
- Локальный кэш в UserDefaults (iOS) / SharedPreferences (Android) для работы оффлайн.
- При первом запуске: загрузить с сервера → применить локально.

### Приоритет системных настроек

Системные настройки **всегда имеют приоритет** над настройками приложения:

```
Итоговый text_size = max(system_font_scale, app_text_size)
Итоговый bold_text = system_bold_text OR app_bold_text
Итоговый reduce_motion = system_reduce_motion OR app_reduce_motion
Итоговый high_contrast = system_high_contrast OR app_high_contrast
```

### Тестирование

Перед сдачей в ревью обязательно проверить:
1. ✅ Включить VoiceOver (iOS) / TalkBack (Android) — все кнопки и поля должны зачитываться
2. ✅ Установить системный шрифт XL — верстка не должна ломаться
3. ✅ Включить Bold Text (системная настройка iOS) — приложение должно реагировать
4. ✅ Включить Reduce Motion (системная настройка) — анимации должны отключаться
5. ✅ Проверить контраст цветов в приложении инструментом Accessibility Inspector (Xcode)

---

## 6. Чеклист публикации

### App Store §2.5.4 — обязательно

- [ ] Все кнопки-иконки имеют `accessibilityLabel`
- [ ] Все изображения (не декоративные) имеют `accessibilityLabel`
- [ ] Приложение работает с включённым VoiceOver (все основные сценарии)
- [ ] Поддержка Dynamic Type: весь текст масштабируется без ошибок верстки
- [ ] Раздел Accessibility Settings существует и содержит все 8 пунктов

### Google Play — обязательно

- [ ] Приложение работает с включённым TalkBack
- [ ] Все интерактивные элементы имеют `contentDescription`
- [ ] Поддержка Android Font Scale

### EAA (обязательно с 28.06.2025 для рынка ЕС)

- [ ] Контраст текста ≥ 4.5:1 для обычного текста (проверить Accessibility Inspector)
- [ ] Контраст UI-компонентов ≥ 3:1
- [ ] Весь функционал доступен без тачскрина (keyboard/switch navigation)
- [ ] Субтитры для всех обучающих видео приложения
- [ ] Alt text для всех значимых изображений

---

*AccessibilitySpec.md v1.0 · Bestme · март 2026*  
*Смежные документы: [SettingsTZ.md](SettingsTZ.md), [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md)*
