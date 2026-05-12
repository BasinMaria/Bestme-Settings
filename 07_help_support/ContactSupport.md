# Contact Support

**Раздел:** Settings → Help & Support → Contact Support  
**Обязательно:** ⚖️ App Store (Support URL) · DSA Art.17 (пользователь должен иметь возможность оспорить решение модерации)

---

## Требования к публикации

| Требование | Источник |
|---|---|
| Механизм обращения в поддержку обязателен | App Store Connect — Support URL |
| Механизм обращения обязателен | Google Play Policy |
| Пользователь должен иметь возможность обратиться по поводу удалённого контента | DSA Art.17(3) |
| Физический адрес компании должен быть в footer каждого email | CAN-SPAM (США) |
| Контакт DPO / Privacy Officer должен быть публично доступен | GDPR Art.37 · Quebec L25 Art.5 |

---

## Структура экрана

```
Contact Support
├── Заголовок: «How can we help?»
├── Категории обращения (обязательный выбор):
│   ├── 🔴 Report illegal content (DSA Art.14)
│   ├── My content was removed — I want to appeal  (DSA Art.17)
│   ├── Account issue (login, suspension)
│   ├── Privacy / data request (GDPR)
│   ├── Technical problem
│   ├── Billing / subscription
│   └── Other
├── Текстовое поле: «Describe your issue» (обязательное)
├── Прикрепить файл (опционально)
├── Email для ответа (предзаполнен из аккаунта, редактируемый)
└── Кнопка: «Send» → экран подтверждения
```

### Экран подтверждения после отправки

```
Confirmation
├── Иконка ✅
├── Заголовок: «Request received»
├── Текст: «We will reply to [email] within 3 business days.
│          For urgent child safety issues, email childsafety@bestme.app»
├── Номер тикета: #XXXXX (показывается пользователю)
└── Кнопка: «Done»
```

---

## Контакты (публичные)

| Назначение | Контакт | Обязательно |
|---|---|---|
| Общая поддержка | support@bestme.app | ⚖️ App Store |
| Детская безопасность / CSAE | childsafety@bestme.app | ⚖️ Google Play Child Safety |
| Privacy Officer / DPO | privacy@bestme.app | ⚖️ GDPR Art.37 · Quebec L25 |
| Юридические запросы | legal@bestme.app | 💡 |

---

## Сроки ответа (обязательны для DSA)

| Тип обращения | Срок | Источник |
|---|---|---|
| Незаконный контент (DSA категории) | 24 часа | DSA Art.14 |
| Жалоба на удалённый контент / апелляция | 5 рабочих дней | DSA Art.17 |
| Запрос GDPR (копия данных, удаление) | 30 дней | GDPR Art.12 |
| Общее обращение | 3 рабочих дня | App Store (рекомендация) |
