# 🔔 Notifications / Уведомления

## Overview / Обзор

This document describes the complete structure of the Notifications settings section in Bestme.

Этот документ описывает полную структуру раздела настроек Уведомлений в Bestme.

---

## Structure / Структура

```
🔔 Notifications / Уведомления
│
├── Push Notifications / Push-уведомления
│   ├── Enable push notifications / Включить push-уведомления
│   │   [Master toggle ON/OFF] / [Главный переключатель Вкл/Выкл]
│   │
│   ├── Likes and Reactions / Лайки и реакции
│   │   └── When someone likes or reacts to your post
│   │       Когда кто-то лайкает или реагирует на пост
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Comments / Комментарии
│   │   └── When someone comments on your post
│   │       Когда кто-то комментирует ваш пост
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── New Followers / Новые подписчики
│   │   └── When someone follows you
│   │       Когда кто-то подписывается на вас
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Messages / Сообщения
│   │   └── When you receive a new message
│   │       Когда получаете новое сообщение
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Mentions and Tags / Упоминания и отметки
│   │   └── When someone @mentions or tags you
│   │       Когда кто-то @упоминает или отмечает вас
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Friend Requests / Запросы в друзья
│   │   └── When someone sends you a friend request
│   │       Когда кто-то отправляет запрос в друзья
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Live Videos / Прямые эфиры
│       └── When people you follow go live
│           Когда люди, на которых вы подписаны, в эфире
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
├── Email Notifications / Email-уведомления
│   ├── Activity Summary / Сводка активности
│   │   └── Daily or weekly summary of activity
│   │       Ежедневная или еженедельная сводка активности
│   │       [Never / Daily / Weekly] / [Никогда / Ежедневно / Еженедельно]
│   │
│   ├── Reminder Emails / Письма-напоминания
│   │   └── Reminders about posts, friends, or events
│   │       Напоминания о постах, друзьях или событиях
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   ├── Product Updates / Обновления продукта
│   │   └── News about new features and updates
│   │       Новости о новых функциях и обновлениях
│   │       [Toggle ON/OFF] / [Вкл/Выкл]
│   │
│   └── Newsletter / Новостная рассылка
│       └── Tips, stories, and inspiration
│           Советы, истории и вдохновение
│           [Toggle ON/OFF] / [Вкл/Выкл]
│
└── In-App Settings / Настройки в приложении
    ├── Sound / Звук
    │   └── Play sound for notifications
    │       Воспроизводить звук для уведомлений
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    ├── Vibration / Вибрация
    │   └── Vibrate for notifications
    │       Вибрация для уведомлений
    │       [Toggle ON/OFF] / [Вкл/Выкл]
    │
    └── Badge Count / Счетчик значков
        └── Show number of unread notifications on app icon
            Показывать количество непрочитанных на иконке
            [Toggle ON/OFF] / [Вкл/Выкл]
```

---

## Detailed Breakdown / Детальное описание

### 1. Push Notifications / Push-уведомления

**Location:** Main section in Notifications  
**Расположение:** Основная секция в Уведомлениях

**Master Control:**
- **Enable push notifications** - Main ON/OFF toggle that controls all push notifications
- **Включить push-уведомления** - Главный переключатель, контролирующий все push-уведомления

**7 Notification Types / 7 типов уведомлений:**

1. **Likes and Reactions / Лайки и реакции**
   - When: Someone likes or reacts to your post
   - Когда: Кто-то лайкает или реагирует на ваш пост
   - Control: Toggle ON/OFF

2. **Comments / Комментарии**
   - When: Someone comments on your post
   - Когда: Кто-то комментирует ваш пост
   - Control: Toggle ON/OFF

3. **New Followers / Новые подписчики**
   - When: Someone follows you
   - Когда: Кто-то подписывается на вас
   - Control: Toggle ON/OFF

4. **Messages / Сообщения**
   - When: You receive a new message
   - Когда: Получаете новое сообщение
   - Control: Toggle ON/OFF

5. **Mentions and Tags / Упоминания и отметки**
   - When: Someone @mentions or tags you
   - Когда: Кто-то @упоминает или отмечает вас
   - Control: Toggle ON/OFF

6. **Friend Requests / Запросы в друзья**
   - When: Someone sends you a friend request
   - Когда: Кто-то отправляет запрос в друзья
   - Control: Toggle ON/OFF

7. **Live Videos / Прямые эфиры**
   - When: People you follow go live
   - Когда: Люди, на которых вы подписаны, в эфире
   - Control: Toggle ON/OFF

---

### 2. Email Notifications / Email-уведомления

**Location:** Second section in Notifications  
**Расположение:** Вторая секция в Уведомлениях

**4 Email Types / 4 типа email:**

1. **Activity Summary / Сводка активности**
   - Description: Daily or weekly summary of activity
   - Описание: Ежедневная или еженедельная сводка активности
   - Options: Never / Daily / Weekly
   - Опции: Никогда / Ежедневно / Еженедельно

2. **Reminder Emails / Письма-напоминания**
   - Description: Reminders about posts, friends, or events
   - Описание: Напоминания о постах, друзьях или событиях
   - Control: Toggle ON/OFF

3. **Product Updates / Обновления продукта**
   - Description: News about new features and updates
   - Описание: Новости о новых функциях и обновлениях
   - Control: Toggle ON/OFF

4. **Newsletter / Новостная рассылка**
   - Description: Tips, stories, and inspiration
   - Описание: Советы, истории и вдохновение
   - Control: Toggle ON/OFF

---

### 3. In-App Settings / Настройки в приложении

**Location:** Third section in Notifications  
**Расположение:** Третья секция в Уведомлениях

**3 Settings / 3 настройки:**

1. **Sound / Звук**
   - Description: Play sound for notifications
   - Описание: Воспроизводить звук для уведомлений
   - Control: Toggle ON/OFF

2. **Vibration / Вибрация**
   - Description: Vibrate for notifications
   - Описание: Вибрация для уведомлений
   - Control: Toggle ON/OFF

3. **Badge Count / Счетчик значков**
   - Description: Show number of unread notifications on app icon
   - Описание: Показывать количество непрочитанных на иконке
   - Control: Toggle ON/OFF

---

## User Flow / Пользовательский процесс

**From Settings First Screen:**

```
Settings / Настройки
  ↓ [Tap / Нажать]
🔔 Notifications / Уведомления
  ↓ [Opens / Открывается]
Notifications Screen with 3 sections:
  1. Push Notifications
  2. Email Notifications
  3. In-App Settings
```

**Example Navigation:**

```
Settings → Notifications → Push Notifications → Likes and Reactions → [Toggle ON/OFF]
Настройки → Уведомления → Push-уведомления → Лайки и реакции → [Вкл/Выкл]
```

---

## Summary / Итого

**Total Settings:**
- **3 main sections** / **3 основные секции**
- **7 push notification types** / **7 типов push-уведомлений**
- **4 email notification types** / **4 типа email-уведомлений**
- **3 in-app settings** / **3 настройки в приложении**

**Total: 14 notification controls + 3 in-app settings = 17 settings**  
**Всего: 14 контролов уведомлений + 3 настройки в приложении = 17 настроек**
