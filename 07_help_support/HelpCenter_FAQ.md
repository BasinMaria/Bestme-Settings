# Help Center / FAQ

**Раздел:** Settings → Help & Support → Help Center / FAQ  
**Обязательно:** ⚖️ App Store (Support URL обязателен) · Google Play (поддержка пользователей)

---

## Требования к публикации

| Требование | Источник |
|---|---|
| Наличие URL страницы поддержки (может быть FAQ) | App Store Connect — Support URL |
| Страница должна открываться (HTTP 200) | App Store Review |
| Рекомендуется иметь раздел Help в приложении или на сайте | Google Play Policy |

**Минимальный вариант:** одна страница `bestme.app/help` со ссылкой на `support@bestme.app` — этого достаточно для публикации.

---

## Структура экрана

```
Help Center / FAQ
├── Поиск (строка поиска вверху)
├── Раздел: Getting Started
│   ├── How to create an account
│   ├── How to set up your profile
│   └── How to find friends
├── Раздел: Privacy & Safety
│   ├── How to make your profile private
│   ├── How to block a user
│   ├── How to report content or a user  →  ведёт на ReportAProblem
│   └── Child Safety                     →  ведёт на ChildSafety
├── Раздел: Account & Data
│   ├── How to download your data
│   ├── How to delete your account
│   └── How to manage notifications
├── Раздел: Technical Issues
│   ├── App crashes / doesn't load
│   └── Can't log in
└── Кнопка: Contact Support             →  ведёт на ContactSupport
```

---

## Элементы экрана

| Элемент | Тип | Обязательно |
|---|---|---|
| Строка поиска по FAQ | Input | 💡 |
| Список разделов (accordion) | Список | ⚖️ (хотя бы 1 раздел) |
| Ответы на вопросы | Текст / WebView | ⚖️ |
| Кнопка «Contact Support» | CTA | ⚖️ App Store |
| Кнопка «Report a problem» | CTA | ⚖️ DSA Art.14 |
| Email childsafety@bestme.app (видим) | Текст / ссылка | ⚖️ Google Play Child Safety |

---

## Минимальный контент для публикации

Три обязательных пункта FAQ:

1. **How to delete my account** — Settings → Your Data → Delete Account. Alternatively use the web form at bestme.app/delete-account.
2. **How to report harmful content** — Tap (⋯) under any post or on a profile → Report. Select a reason. We will review within 24 hours.
3. **Child Safety / CSAE** — To report child sexual abuse material, email childsafety@bestme.app immediately.

---

## Ссылки из раздела

- [Contact Support](ContactSupport.md)
- [Report a Problem](../04_moderation/ReportAProblem.md)
- [Child Safety](../04_moderation/ChildSafety.md)
- [Privacy Policy](../01_legal/PrivacyPolicy.md)
- [Terms of Service](../01_legal/TermsOfService.md)
