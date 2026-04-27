# Terms of Service — Экранная спецификация

**Раздел:** Settings → Help & Support → Terms of Service  
**Обязательно:** ⚖️ App Store · Google Play  
**Полный юридический текст:** [TermsOfService.md](../TermsOfService.md)

---

## Требования к публикации

| Требование | Источник |
|---|---|
| Terms of Service обязательны и должны быть доступны | App Store · Google Play |
| Пользователь должен явно принять Terms при регистрации | App Store 5.1.1 · Google Play |
| Terms должны запрещать CSAE контент | Google Play Child Safety Standards |
| Terms должны описывать правила модерации и последствия нарушений | DSA Art.12–14 |
| Terms должны содержать механизм апелляции | DSA Art.17 |

---

## Структура экрана

```
Terms of Service
├── Заголовок: «Terms of Service»
├── Версия + дата: «Version 1.0 — March 2026»
├── Язык: [English ▾]
├── Содержание (якорные ссылки):
│   ├── 1. Who Can Use BestMe
│   ├── 2. Your Account
│   ├── 3. Content You Post
│   ├── 4. Prohibited Conduct
│   ├── 5. Safety & Reporting
│   ├── 6. Moderation & Appeals
│   ├── 7. Termination
│   └── 8. Contact
├── Текст Terms (WebView или native scroll)
└── Footer:
    └── Ссылка: «Questions? Contact legal@bestme.app»
```

---

## Обязательные разделы (минимум для публикации)

| Раздел | Ключевой контент | Закон |
|---|---|---|
| Who can use | Минимальный возраст 13 лет (18 для взрослого контента) | COPPA · DSA Art.28 |
| Prohibited conduct | Список запрещённого контента, включая CSAE явным текстом | Google Play Child Safety |
| Moderation | Как удаляется контент, сроки, кто принимает решение | DSA Art.14 |
| Appeals | Право оспорить удаление, срок ответа | DSA Art.17 |
| Termination | Условия блокировки аккаунта, право на appeal | DSA Art.17 |
| Governing law | Применимое право | App Store · Google Play |
| Contact | Контакт для юридических вопросов | — |

---

## Точки принятия Terms пользователем (обязательны)

| Момент | Механизм | Обязательно |
|---|---|---|
| Регистрация | Чекбокс + ссылка на Terms | ⚖️ App Store · Google Play |
| Первое создание контента (пост, фото) | Модаль «Принять правила» | ⚖️ Google Play UGC Policy |
| Обновление Terms | In-app баннер + кнопка «Принять» | ⚖️ DSA |

---

> Полный юридический текст: [TermsOfService.md](../TermsOfService.md)
