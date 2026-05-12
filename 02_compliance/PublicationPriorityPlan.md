# PublicationPriorityPlan.md — Что нужно для публикации, а что предотвращает штрафы

**Версия:** 1.0 · **Дата:** март 2026  
**Кому:** Продакт-менеджер, дизайнер, разработчик

> **Цель этого документа:** Чётко разделить (A) то, что Apple/Google **отклонят приложение** без этого, и (B) то, что **не блокирует публикацию**, но может привести к штрафам. Сначала — блокеры, потом — всё остальное.

---

## Быстрый ответ на главные вопросы

| Вопрос | Ответ |
|---|---|
| Экран «Welcome to BestMe» с описанием публичности профиля — это достаточно? | ✅ **Да** — это именно GDPR Art.25(2) Onboarding Disclosure (Поток 1). Уже реализовано. |
| 18+ экран при регистрации закрывает COPPA/GDPR Art.8/DSA? | ✅ **Да** — один экран блокировки достаточен. Отдельный блок «<13 лет» не нужен. |
| Нужно ли добавлять субтитры ко всем видео (как TikTok)? | ❌ **Нет** — нужен только переключатель в Accessibility Settings + системные видео приложения. |
| Какие 6 потоков уже были написаны? | ✅ Потоки 1–6 описаны в ProfileSettingsFullSpec.md. Детали ниже. |

---

## Часть A — 🔴 БЛОКЕРЫ ПУБЛИКАЦИИ

> Без этих пунктов **App Store и/или Google Play отклонят приложение** на ревью. Это первый приоритет.

### A1. Google Play — обязательно к моменту сабмита

| # | Что требуется | Где реализовать | ТЗ |
|---|---|---|---|
| **1** | **Веб-форма удаления аккаунта** — страница `/account/delete` на сайте с полем email | Сайт bestme.app | [AccountDeletionSpec.md §11](../03_settings/AccountDeletionSpec.md) |
| **9** | **Child Safety**: (a) запрет CSAE в Terms of Use; (b) категория «Child Safety» в «Пожаловаться»; (c) email `childsafety@bestme.app` в Help & Support | Приложение + сайт + Terms of Use | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) |
| **11** | **Prominent Disclosure** — экран с объяснением ЗАЧЕМ нужны разрешения, показывается ДО запроса Push / Camera / Photos | Приложение (onboarding или перед первым запросом) | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Поток 3 |
| **8** | **UGC ToS acceptance** — модаль «Принять правила сообщества» при первом создании контента (пост, комментарий, фото) | Приложение | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Поток 2 |

### A2. Apple App Store — обязательно к моменту сабмита

| # | Что требуется | Где реализовать | ТЗ |
|---|---|---|---|
| **10** | **ATT диалог** (`AppTrackingTransparency.framework`) — показать ДО инициализации любого аналитического или рекламного SDK (Firebase, Amplitude, Facebook SDK и т.д.) | iOS только | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) Поток 4 |
| **13** | **Кнопка «Отключить»** рядом с каждым привязанным 3rd-party провайдером (Google, Facebook, Apple) в Login & Security | Приложение (Settings → Login & Security) | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) §Login |
| **1** | **Веб-страница удаления** — также требуется App Store Connect (поле Support URL должно вести к форме удаления) | Сайт | [AccountDeletionSpec.md §11](../03_settings/AccountDeletionSpec.md) |

### A3. Оба магазина

| # | Что требуется | Почему блокирует |
|---|---|---|
| **2** | **Возрастная верификация при регистрации** — экран «Вам должно быть 18+» + блокировка если < 18, без сохранения данных несовершеннолетнего | Google Play требует заявить возрастную политику в Play Console; App Store требует возрастной рейтинг |
| **5** | **Accessibility Settings раздел** — минимум: font_size, high_contrast, reduce_motion, screen reader поддержка | App Store 2.5.4 может отклонить если VoiceOver не работает; Google Play аналогично |

---

## Часть B — 🟡 ШТРАФНЫЕ РИСКИ (не блокируют публикацию, но могут привести к штрафам)

> Эти пункты **не заблокируют ревью**, но нарушение может привести к штрафам от регуляторов. Внедрять после блокеров.

| # | Что требуется | Закон | Штраф | ТЗ |
|---|---|---|---|---|
| **3** | Кнопка «Do Not Sell My Personal Information» в Settings → Your Data | CCPA/CPRA §1798.120 (Калифорния) | До $7 500 за нарушение | [ProfileSettingsFullSpec.md](../03_settings/ProfileSettingsFullSpec.md) |
| **4** | Все email/push/SMS opt-in чекбоксы пустые по умолчанию (не pre-checked) | CASL (Канада) · ePrivacy Directive Art.13 | До $10 млн CAD | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |
| **6** | При Delete Account: API-запрос удаления URL в Google Search Console + Bing + Yandex (если seo_indexable = ON) | GDPR Art.17(2) | До €20 млн | [AccountDeletionSpec.md §10](../03_settings/AccountDeletionSpec.md) |
| **7** | Onboarding Disclosure — экран о публичности профиля **до** первого использования | GDPR Art.25(2) | До €20 млн | **✅ УЖЕ РЕАЛИЗОВАН** — см. скриншот «Welcome to BestMe» ниже |
| **12** | SMS consent checkbox с текстом «Для отписки ответьте STOP» при добавлении телефона | TCPA 47 U.S.C. §227 | $1 500 за каждое SMS | [LegalComplianceSpec.md](LegalComplianceSpec.md) §2.10 |

---

## Часть C — Статус 6 потоков из ProfileSettingsFullSpec.md

Все 6 потоков **описаны в ProfileSettingsFullSpec.md**. Статус реализации:

| Поток | Название | Статус документа | Статус в приложении |
|---|---|---|---|
| **Поток 1** | Onboarding Disclosure — экран о публичности профиля (GDPR Art.25) | ✅ Описан | ✅ **Уже реализован** (скриншот подтверждает) |
| **Поток 2** | UGC Terms Acceptance — модаль при первом создании контента | ✅ Описан | ⬜ Нужно реализовать (блокер Google Play) |
| **Поток 3** | Prominent Disclosure — объяснение ДО запроса Push/Camera/Photos | ✅ Описан | ⬜ Нужно реализовать (блокер Google Play) |
| **Поток 4** | ATT Диалог — iOS 14.5+ | ✅ Описан | ⬜ Нужно реализовать (блокер App Store) |
| **Поток 5** | TCPA SMS Consent — при добавлении телефона | ✅ Описан | ⬜ Нужно реализовать (штрафной риск) |
| **Поток 6** | Delete Account Modal — с объяснением де-индексации | ✅ Описан | ⬜ Нужно реализовать (блокер + штрафной риск) |

---

## Уточнение по субтитрам (Пункт 5 — Accessibility)

В таблице 13 критичных пунктов написано «субтитры» в составе Accessibility раздела. Вот точное значение:

### Что «субтитры» означает в контексте EAA / App Store 2.5.4:

**НЕ нужно:**
- ❌ Автоматические субтитры ко всем видео пользователей (UGC) — это бизнес-фича TikTok, не закон
- ❌ AI-генерация субтитров для всего контента на платформе

**Нужно:**
- ✅ **Переключатель `closed_captions_enabled`** в разделе Accessibility Settings (ON/OFF)
- ✅ **Субтитры к системным видео** — если в приложении есть обучающие видео / туториалы от вас (не UGC), они должны иметь субтитры
- ✅ **VoiceOver/TalkBack** — все кнопки, иконки, поля имеют `accessibilityLabel`
- ✅ **Контраст текста ≥ 4.5:1** (WCAG 2.1 AA)

**Почему TikTok добавил авто-субтитры к UGC-видео:**
Это маркетинговое решение для глухих и слабослышащих аудиторий — не требование закона. Ни App Store, ни Google Play не проверяют наличие субтитров на пользовательских видео.

---

## Порядок реализации (Sprint-план)

### Sprint 1 — Публикация (всё что блокирует ревью)

```
Неделя 1-2:
□ Веб-страница /account/delete (сайт)                    ← Google Play + App Store
□ Кнопка «Отключить» для 3rd-party логина (iOS/Android)  ← App Store §5.1.1(v)
□ ATT диалог перед инициализацией SDK (iOS only)         ← App Store §5.1.2(i)
□ Возрастной рейтинг в App Store Connect = 17+            ← формальное требование
□ Возрастной рейтинг в Google Play Console = 18+          ← формальное требование

Неделя 3-4:
□ UGC ToS модаль при первом контенте                      ← Google Play + App Store
□ Prominent Disclosure перед Push/Camera/Photos           ← Google Play
□ Child Safety: Terms of Use запрет CSAE                  ← Google Play Child Safety
□ Child Safety: категория в «Пожаловаться»                ← Google Play Child Safety  
□ Child Safety: childsafety@bestme.app в Help & Support   ← Google Play Child Safety
□ Accessibility Settings раздел (5 переключателей)        ← App Store 2.5.4
```

### Sprint 2 — Защита от штрафов

```
Неделя 5-6:
□ SMS consent checkbox с текстом STOP                     ← TCPA (штраф $1500/SMS)
□ Pre-checked = OFF для всех email/push/SMS opt-in        ← CASL / ePrivacy
□ «Do Not Sell My Personal Information» кнопка            ← CCPA штраф $7500
□ Delete Account Modal с объяснением де-индексации        ← GDPR Art.17(2) штраф €20M

Неделя 7-8:
□ Backend де-индексация: Google/Bing/Yandex API при удалении ← GDPR Art.17(2)
□ Purge timeline: T+0 (session) → T+30d (PII) → T+90d (logs) ← GDPR Art.5
```

---

## Что уже готово ✅

| Что | Подтверждение |
|---|---|
| Поток 1 — Onboarding Disclosure «Welcome to BestMe» | Скриншот в задаче — экран показывает публичность профиля, ссылки на Settings → Privacy & Visibility, Privacy Policy и Terms of Service |
| Все 6 потоков — ТЗ написано | ProfileSettingsFullSpec.md |
| Удаление аккаунта — ТЗ написано | AccountDeletionSpec.md |
| GDPR Art.17(2) де-индексация — ТЗ написано | GDPRArt25Art17AuditSpec.md |
| Accessibility — ТЗ написано | SettingsTZ.md §8 |

---

## Ответы на вопросы из обсуждения

**Q: Мы уже показываем экран «Welcome to BestMe» — этого достаточно для GDPR Art.25?**  
**A:** ✅ Да! Этот экран именно то, что требует GDPR Art.25(2). Он содержит всё обязательное: уведомление о публичности профиля, где это изменить, и ссылку на Privacy Policy. Поток 1 реализован.

**Q: Экран возрастной верификации 18+ — достаточно для всех законов?**  
**A:** ✅ Да. Один экран 18+ закрывает COPPA (США), GDPR Art.8 (ЕС), DSA Art.28 (ЕС). Отдельный блок «< 13 лет» не нужен.

**Q: Субтитры — это блокер для публикации?**  
**A:** ⚠️ Только частично. Вам нужен переключатель «Closed Captions» в Accessibility Settings (App Store 2.5.4). Авто-субтитры к пользовательским видео — НЕ нужны и НЕ блокируют публикацию.

**Q: Что делать сначала — блокеры или штрафные риски?**  
**A:** Сначала Sprint 1 (блокеры публикации), потом Sprint 2 (штрафные риски). Без Sprint 1 приложение не выйдет. Sprint 2 можно делать параллельно, но он не блокирует релиз.

---

*PublicationPriorityPlan.md v1.0 · Bestme · март 2026*  
*Приоритизирован для команды разработки: сначала всё, что блокирует ревью в App Store / Google Play.*
