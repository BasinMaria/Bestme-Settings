# ComplianceClarifications.md — Ответы на вопросы по 13 критичным пунктам

**Версия:** 1.0 · **Дата:** март 2026  
**Статус:** Справочный документ — существующие файлы не изменяются  
**Кому:** Продакт-менеджер, дизайнер, разработчик

> **Важно:** Этот документ не изменяет AccountDeletionSpec.md или другие уже созданные документы. Он отвечает на два конкретных вопроса из обсуждения и даёт практический план действий по каждому из 13 критичных пунктов.

---

## Содержание

1. [Вопрос 1 — Возраст: нам 18+, нужен ли блок «младше 13»?](#1-вопрос-о-возрасте-нам-18-нужен-ли-блок-младше-13)
2. [Вопрос 2 — Доступность и субтитры: как это работает в соцсети?](#2-вопрос-о-доступности-и-субтитрах)
3. [Статус всех 13 критичных пунктов](#3-статус-всех-13-критичных-пунктов)
4. [Что уже сделано в документах](#4-что-уже-сделано-в-документах)
5. [Что нужно сделать разработчикам — сводный план](#5-что-нужно-сделать-разработчикам--сводный-план)

---

## 1. Вопрос о возрасте: нам 18+, нужен ли блок «младше 13»?

### Короткий ответ: НЕТ — отдельного блока COPPA «младше 13» не нужно, но нужен правильный экран при регистрации.

### Подробное объяснение

Ваше приложение — **только для 18+**. Это означает:

```
Экран регистрации → пользователь указывает дату рождения
→ если < 18 лет → ОТКАЗ В РЕГИСТРАЦИИ ("Приложение доступно только для лиц от 18 лет")
→ если ≥ 18 лет → регистрация продолжается
```

**Почему одного экрана «18+» достаточно:**

| Закон | Что требует | Как закрывается вашим 18+ блоком |
|---|---|---|
| **COPPA (США)** | Запрет сбора данных детей до 13 лет | ✅ Все, кто < 18 — заблокированы, значит < 13 тоже заблокированы |
| **GDPR Art.8 (ЕС)** | Для 13-16 лет нужно согласие родителей | ✅ Блокируете всех < 18, не нужно обрабатывать детей вообще |
| **DSA Art.28 (ЕС)** | Запрет профилирования детей < 17 | ✅ Если нет пользователей < 18 — DSA не применяется |

**Что именно нужно на экране отказа:**

```
┌─────────────────────────────────────┐
│  Bestme — только для совершеннолетних│
│                                     │
│  Вам должно быть 18 лет или больше  │
│  для использования этого            │
│  приложения.                        │
│                                     │
│  К сожалению, по указанной вами     │
│  дате рождения вы не можете         │
│  зарегистрироваться.                │
│                                     │
│  Если у вас есть вопросы:           │
│  support@bestme.app                 │
│                                     │
│  [Закрыть]                          │
└─────────────────────────────────────┘
```

**Что НЕЛЬЗЯ делать при этом экране:**
- ❌ Не показывать кнопку «Попробовать другую дату» (позволяет обмануть систему)
- ❌ Не хранить введённую дату рождения несовершеннолетнего (нарушение COPPA)
- ✅ Немедленно выйти из флоу, не сохраняя никакие данные

**Нужно ли писать в App Store/Google Play о возрасте?**
- ✅ App Store: в App Store Connect установите возрастной рейтинг **17+** (Apple) или **18+** (Google Play)
- ✅ В Terms of Service явно указать: «Вы должны быть не моложе 18 лет»

### Итог по возрасту

Одного блока **«Вам должно быть 18+»** на экране регистрации с проверкой даты рождения — **достаточно для прохождения ревью** в обоих магазинах и для соответствия COPPA + GDPR Art.8 + DSA Art.28. Отдельный экран «если вам меньше 13» не нужен.

---

## 2. Вопрос о доступности и субтитрах

### Короткий ответ: Вы НЕ обязаны добавлять автосубтитры к каждому видео. Вы обязаны предоставить инструменты доступности на уровне приложения.

### Что требуют законы на практике для социальной сети

EAA (ЕС, с 28 июня 2025), ADA (США), AODA (Канада) и другие законы о доступности применяются к **интерфейсу приложения**, а **не к пользовательскому контенту**.

#### Разграничение ответственности:

| Что это | Чья ответственность | Нужно вам? |
|---|---|---|
| Субтитры к видео которые снял ПОЛЬЗОВАТЕЛЬ | Пользователя | ❌ Нет (вы не создаёте этот контент) |
| Субтитры к ВАШИМ обучающим / системным видео | Ваша | ✅ Да (любые видео внутри приложения от вас) |
| Шрифты, контраст, увеличение текста | Ваша | ✅ Да — это интерфейс |
| Поддержка screen reader (VoiceOver/TalkBack) | Ваша | ✅ Да — это интерфейс |
| Возможность ДОБАВИТЬ субтитры к своему видео | Ваша (фича) | 🟡 Рекомендуется как инструмент |

### Что именно нужно реализовать (и что это НЕ TikTok)

**TikTok добавил автосубтитры** — это их бизнес-решение для улучшения охвата, а не требование закона. Они делают это для глухих/слабослышащих пользователей и для просмотра без звука. Для вас это **рекомендация**, не обязательство.

#### Что обязательно (закон):

**А. Системные настройки доступности в приложении**
Раздел в настройках: Settings → Accessibility

| Настройка | Что это | Закон |
|---|---|---|
| `font_size` | Регулировка размера шрифта (3 размера: Обычный / Крупный / Очень крупный) | EAA · ADA |
| `high_contrast` | Режим высокого контраста | EAA · ADA |
| `reduce_motion` | Отключить анимации (важно при эпилепсии) | EAA |
| `screen_reader_support` | Все кнопки и поля имеют accessibility labels | EAA · ADA · App Store |
| `text_to_speech` | Поддержка VoiceOver (iOS) / TalkBack (Android) | EAA · ADA |

Контраст текста должен быть **≥ 4.5:1** (WCAG 2.1 AA) — это требование верификации при ревью.

**Б. Что НЕ требуется, но рекомендуется:**

| Фича | Сложность | Выгода |
|---|---|---|
| Автосубтитры к пользовательским видео (как TikTok) | Высокая — нужен AI/ML сервис (Google Speech-to-Text, AWS Transcribe) | Охват глухих пользователей |
| Возможность добавить текстовые субтитры вручную | Средняя | Быстрый доступный выход |
| Альтернативный текст (alt-text) для изображений | Низкая — поле при загрузке | Слабовидящие пользователи |

### Практический план по доступности

**Минимум для прохождения ревью (6 шагов):**

1. **Раздел Accessibility в Settings** — уже описан в SettingsTZ.md. Убедитесь что он реализован в коде приложения
2. **VoiceOver/TalkBack** — все интерактивные элементы должны иметь `accessibilityLabel`. Проверяется Apple reviewer с включённым VoiceOver
3. **Контраст 4.5:1** — пройдите через Figma/дизайн и проверьте все цветовые комбинации. Инструмент: [webaim.org/resources/contrastchecker](https://webaim.org/resources/contrastchecker)
4. **Кнопки ≥ 44×44 pt** — минимальный touch target по Apple HIG и WCAG 2.1
5. **Нет мигания >3 раз/сек** — любая анимация не должна создавать риск приступа
6. **Шрифт масштабируется** — если пользователь увеличил шрифт в системе, ваше приложение должно это поддерживать (не фиксированные размеры текста)

**НЕ нужно для публикации:**
- Автосубтитры к пользовательским видео (это рекомендация, не блокер)
- Полная поддержка WCAG 2.1 AAA (достаточно AA)

---

## 3. Статус всех 13 критичных пунктов

### Что уже описано в документах репозитория

| # | Пункт | Статус | В каком документе |
|---|---|---|---|
| 🔴 1 | Веб-форма удаления аккаунта | ✅ Описано | [AccountDeletionSpec.md §11](../03_settings/AccountDeletionSpec.md) |
| 🔴 2 | Блок регистрации < 13 / < 18 лет | ✅ Описано (18+) | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) + этот документ §1 |
| 🔴 3 | «Do Not Sell My Personal Information» | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 4 |
| 🔴 4 | Pre-checked boxes = пустые | ✅ Описано | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |
| 🔴 5 | Accessibility раздел | ✅ Описано | [SettingsTZ.md](../03_settings/SettingsTZ.md) §8 + этот документ §2 |
| 🔴 6 | Art.17(2) де-индексация | ✅ Описано | [AccountDeletionSpec.md §10](../03_settings/AccountDeletionSpec.md) · [GDPRArt25Art17AuditSpec.md](GDPRArt25Art17AuditSpec.md) |
| 🔴 7 | Onboarding disclosure (18+, открытый профиль) | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 1 |
| 🔴 8 | UGC ToS acceptance | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 2 |
| 🔴 9 | Child Safety (Terms, Report, Email) | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) §Child Safety |
| 🔴 10 | ATT диалог (iOS 14.5+) | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 3 |
| 🔴 11 | Prominent Disclosure | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 5 |
| 🔴 12 | SMS consent checkbox (TCPA) | ✅ Описано | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |
| 🔴 13 | Disconnect 3rd-party login | ✅ Описано | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) §Login&Security |

**Все 13 пунктов уже описаны в документах.** Что осталось — это реализация в коде приложения.

---

## 4. Что уже сделано в документах

```
✅ AccountDeletionSpec.md        ← Пункты 1, 6 (4 сценария, 15 экранов, де-индексация)
✅ ProfileSettingsFullSpec.md    ← Пункты 2,3,7,8,9,10,11,13 (6 обязательных потоков)
✅ LegalComplianceSpec.md        ← Пункты 4,12 (21 закон)
✅ SettingsTZ.md                 ← Пункт 5 (Accessibility раздел)
✅ GDPRArt25Art17AuditSpec.md    ← Пункт 6 (де-индексация детально)
```

Документация **готова на 100%**. Следующий этап — разработка.

---

## 5. Что нужно сделать разработчикам — сводный план

### Приоритет 1: Блокеры (без этого App Store и Google Play отклонят)

**Sprint 1 (1-2 недели)**

| Задача | Описание | Ссылка на ТЗ |
|---|---|---|
| **Экран возрастной верификации** | При регистрации: поле «дата рождения», блок если < 18 лет | §1 этого документа |
| **Кнопка «Delete Account» в настройках** | Личный профиль → Settings → Account → Delete Account | [AccountDeletionSpec.md §5](../03_settings/AccountDeletionSpec.md) |
| **Веб-страница** `/account/delete` | HTML-форма на сайте с полем email и подтверждением | [AccountDeletionSpec.md §11](../03_settings/AccountDeletionSpec.md) |
| **ATT диалог (iOS)** | `AppTrackingTransparency.framework`, запросить до инициализации любого аналитического SDK | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 3 |
| **Disconnect 3rd-party** | Кнопка «Отключить» рядом с каждым привязанным провайдером (Google, Facebook, Apple) | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) §Login |

**Sprint 2 (1-2 недели)**

| Задача | Описание | Ссылка на ТЗ |
|---|---|---|
| **UGC ToS modal** | Показать один раз при первом создании поста/комментария | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 2 |
| **Onboarding disclosure** | Экран при первом входе: «Ваш профиль публичен. Вы можете изменить это в настройках» | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 1 |
| **Prominent Disclosure** | Экран ДО запроса Push/Camera/Photos permissions: зачем нужно разрешение | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Flow 5 |
| **Do Not Sell кнопка** | Settings → Your Data → «Do Not Sell My Personal Information» → toggle + подтверждение | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) |
| **SMS consent checkbox** | При добавлении телефона: обязательный чекбокс с текстом про STOP | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |

### Приоритет 2: Юридические требования бэкенда

**Sprint 3 (2-3 недели)**

| Задача | Описание | Ссылка на ТЗ |
|---|---|---|
| **Статусы аккаунта при удалении** | `PENDING_DELETION` → `DELETING` → `DELETED` → `PURGED` | [AccountDeletionSpec.md §9](../03_settings/AccountDeletionSpec.md) |
| **Де-индексация при удалении** | Вызов Google Search Console API + Bing API + Yandex API | [AccountDeletionSpec.md §10](../03_settings/AccountDeletionSpec.md) |
| **Email при удалении** | Отправить подтверждение удаления пользователю (T+0) | [AccountDeletionSpec.md §8](../03_settings/AccountDeletionSpec.md) |
| **Pre-checked = OFF** | Все email/push/SMS opt-in чекбоксы пустые по умолчанию | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |
| **Child Safety** | В Terms of Use запрет CSAE, в «Пожаловаться» категория «Детский контент», email `childsafety@bestme.app` | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) |

### Приоритет 3: Доступность

**Sprint 4 (1 неделя)**

| Задача | Описание | Стандарт |
|---|---|---|
| **AccessibilityLabel на все кнопки** | Каждая кнопка, иконка, поле — описание для VoiceOver/TalkBack | WCAG 2.1 AA |
| **Контраст ≥ 4.5:1** | Проверить все цветовые сочетания текст/фон через инструмент | WCAG 2.1 AA |
| **Кнопки ≥ 44×44 pt** | Touch target минимум 44×44 pt | Apple HIG |
| **Раздел Accessibility в Settings** | font_size, high_contrast, reduce_motion переключатели | EAA / ADA |
| **Dynamic Type (iOS) / Scale (Android)** | Текст должен масштабироваться при системных настройках шрифта | EAA |

---

## Приложение: Инструменты для проверки доступности

| Инструмент | Платформа | Что проверяет |
|---|---|---|
| [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) | Web | Контраст цветов |
| Xcode Accessibility Inspector | iOS | VoiceOver, labels, touch targets |
| Android Accessibility Scanner | Android | TalkBack, touch targets |
| [Color Oracle](https://colororacle.org/) | Desktop | Симуляция дальтонизма |
| [WAVE](https://wave.webaim.org/) | Web | Доступность веб-форм (для /account/delete) |

---

## Краткие ответы на вопросы

**Q: Нам 18+. Нужен ли блок «если тебе меньше 13»?**  
**A:** Нет. Один экран блокировки при регистрации «Вам должно быть 18+» — достаточно для COPPA, GDPR Art.8 и DSA Art.28.

**Q: Нужно ли добавлять субтитры ко всем видео как в TikTok?**  
**A:** Нет, это не требование закона. Закон требует доступность интерфейса приложения (контраст, шрифты, screen reader). Субтитры к пользовательским видео — ваша бизнес-фича по желанию.

**Q: Все 13 критичных пунктов нужно реализовать?**  
**A:** Да, все 13 — блокеры публикации. Но все они уже описаны в документах репозитория. Разработчикам нужен план из §5 этого документа.

---

*ComplianceClarifications.md v1.0 · Bestme · март 2026*  
*Документ не изменяет существующие файлы. Является разъяснением к ProfileSettingsFullSpec.md, AccountDeletionSpec.md, LegalComplianceSpec.md и SettingsTZ.md.*
