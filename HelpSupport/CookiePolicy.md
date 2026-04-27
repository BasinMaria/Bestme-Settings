# Cookie Policy — Экранная спецификация

**Раздел:** Settings → Help & Support → Cookie Policy  
**Обязательно:** ⚖️ ePrivacy Directive 2002/58/EC · GDPR Art.7 · CCPA §1798.120

---

## Требования к публикации

| Требование | Источник |
|---|---|
| Cookie Policy обязательна при использовании cookie или аналогичных технологий | ePrivacy Directive (ЕС) |
| Пользователь должен дать согласие до установки нессессарных cookie | ePrivacy Art.5(3) |
| Pre-checked boxes недопустимы для необязательных cookie | GDPR Art.7 · ePrivacy |
| Пользователь должен иметь возможность отозвать согласие так же легко, как дал | GDPR Art.7(3) |
| «Do Not Sell» для аналитических / рекламных cookie (Калифорния) | CCPA §1798.120 |

---

## Структура экрана (Cookie Policy — текстовый документ)

```
Cookie Policy
├── Заголовок: «Cookie Policy»
├── Версия + дата
├── Содержание:
│   ├── 1. What are cookies
│   ├── 2. Types of cookies we use
│   ├── 3. Third-party cookies
│   ├── 4. Your choices
│   └── 5. Contact
└── Кнопка: «Manage Cookie Preferences» → открывает Cookie Settings
```

---

## Таблица типов cookie (обязательна в тексте)

| Тип | Примеры | Согласие |
|---|---|---|
| **Strictly necessary** | Сессия, CSRF-токен, auth | Не требуется |
| **Functional** | Язык, тема, предпочтения | Требуется |
| **Analytics** | Firebase Analytics, Amplitude | Требуется |
| **Advertising / Tracking** | Facebook Pixel, AppsFlyer | Требуется (ATT на iOS) |

---

## Экран Cookie Settings (управление согласием)

```
Cookie Preferences
├── Заголовок: «Manage Cookies»
├── Strictly Necessary [всегда ON, нельзя выключить]
│   └── «Required for the app to work»
├── Functional Cookies [Toggle, default: ON]
│   └── «Remember your language and preferences»
├── Analytics Cookies [Toggle, default: OFF]  ← OFF по умолчанию (GDPR Art.25)
│   └── «Help us understand how you use the app»
├── Advertising Cookies [Toggle, default: OFF] ← OFF по умолчанию
│   └── «Personalised ads. iOS: managed by system ATT prompt»
├── Кнопка: «Save Preferences»
└── Кнопка: «Reject All» (кроме Strictly Necessary)
```

---

## Точки входа в приложении

| Экран | Момент | Обязательно |
|---|---|---|
| Cookie banner при первом запуске | До установки нессессарных cookie | ⚖️ ePrivacy (ЕС) |
| Settings → Your Data → Cookie Settings | Управление в любое время | ⚖️ GDPR Art.7(3) |
| Settings → Help & Support → Cookie Policy | Ссылка на документ | ⚖️ ePrivacy |

---

## Cookie Banner (первый запуск — только для ЕС)

```
Cookie Banner (bottom sheet)
├── Текст: «We use cookies to improve your experience.»
│          «[Read our Cookie Policy]»
├── Кнопка: «Accept All»
├── Кнопка: «Reject Non-Essential»  ← обязательна (GDPR)
└── Кнопка: «Manage Preferences»   → открывает Cookie Settings
```

> ⚠️ **Важно:** Кнопка «Reject» должна быть такой же заметной, как «Accept». Прятать её — нарушение GDPR Art.7 (тёмные паттерны).
