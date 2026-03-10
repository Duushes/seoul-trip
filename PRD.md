# Промпт для Claude Code — Сеульский трип-трекер (GitHub + Railway)

## Задача

Создай и задеплой мобильный сайт-трекер для поездки в Сеул (13–15 марта 2026).
Стек: статический HTML/CSS/JS сайт, сервер на Node.js/Express,
деплой через GitHub → Railway (автодеплой при пуше).

---

## Что нужно сделать по шагам

1. Создать структуру проекта
2. Написать сайт (`public/index.html`)
3. Написать сервер (`server.js`)
4. Создать `package.json`, `.gitignore`, `railway.toml`
5. Инициализировать git, создать репозиторий на GitHub, запушить
6. Подключить репозиторий к Railway и задеплоить
7. Открыть живой URL и убедиться, что сайт работает

---

## Структура проекта

```
seoul-trip/
├── public/
│   └── index.html        # весь фронтенд (HTML + CSS + JS)
├── server.js             # Express сервер
├── package.json
├── .gitignore
└── railway.toml
```

---

## server.js

```js
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.static(path.join(__dirname, 'public')));

app.get('*', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

app.listen(PORT, () => {
  console.log(`Seoul trip running on port ${PORT}`);
});
```

---

## package.json

```json
{
  "name": "seoul-trip",
  "version": "1.0.0",
  "description": "Seoul trip tracker — Mar 2026",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "engines": {
    "node": ">=18.0.0"
  }
}
```

---

## railway.toml

```toml
[build]
builder = "nixpacks"

[deploy]
startCommand = "npm start"
restartPolicyType = "on-failure"
```

---

## .gitignore

```
node_modules/
.env
.DS_Store
```

---

## Данные маршрута для public/index.html

### Общее
- Отель: Stay 42 Dongmyo · координаты: `37.5716, 127.0114`
- Курс: 1 USD ≈ 90 ₽ · 1 000 KRW ≈ $0.73 / 66 ₽

### День 1 — Пятница 13 Мар · «Прилёт + Восточный Чонно»
Транспорт: AREX Инчхон → Seoul Station (43 мин, ₩9 500) → Линия 1 до Dongmyo

| # | Время | Место | lat | lng | Тип | Заметка |
|---|-------|-------|-----|-----|-----|---------|
| 1 | 07:10–09:00 | ✈ Прилёт → Stay 42 Dongmyo | 37.5716 | 127.0114 | transit | Купи T-money в аэропорту: ₩2 500 |
| 2 | 09:00–11:00 | Рынок Кванджан | 37.5700 | 126.9996 | food | Маяк-кимбап ₩3 000, бинтэток ₩5 000 |
| 3 | 11:00–13:30 | Деревня Иксон-дон | 37.5737 | 126.9901 | culture | Ханок-кафе, сикхе ₩4 000 |
| 4 | 13:30–15:30 | Ручей Чхонгечхон | 37.5691 | 126.9787 | scenic | Хоттеок у Чхонгечхон Плаза ₩2 000 |
| 5 | 16:00–18:00 | 🛏 Отдых в отеле | 37.5716 | 127.0114 | rest | — |
| 6 | 18:30–20:00 | Блошиный рынок Донмё | 37.5718 | 127.0105 | market | Только наличные |
| 7 | 20:00–21:30 | Тток-покки, Синдан-дон | 37.5635 | 127.0089 | food | Тток-покки ₩7 000–10 000 |

Бюджет дня: $25–35 / 2 250–3 150₽

### День 2 — Суббота 14 Мар · «Королевский Северный Сеул»
Транспорт: Метро Линия 3 от Донмё → ст. Ангук / Кёнбоккун (~15 мин)

| # | Время | Место | lat | lng | Тип | Заметка |
|---|-------|-------|-----|-----|-----|---------|
| 1 | 08:45–12:00 | Дворец Кёнбоккун | 37.5796 | 126.9770 | culture | Билет ₩3 000, в ханбоке бесплатно. Смена стражи 10:00 |
| 2 | 12:00–13:30 | Тосокчон Самгетан | 37.5815 | 126.9699 | food | Самгетан ₩17 000 |
| 3 | 13:30–15:30 | Деревня Букчон Ханок | 37.5815 | 126.9850 | culture | Смотровая Букчон-ро 5-гиль |
| 4 | 15:30–17:00 | Самчхон-дон | 37.5835 | 126.9820 | scenic | Кофе Bora ₩8 000 |
| 5 | 17:00–19:00 | Инса-дон | 37.5742 | 126.9856 | market | Хоттеок ₩2 000 |
| 6 | 19:00–21:00 | Переулок Пимаголь | 37.5700 | 126.9823 | food | Хэмуль паджон ₩15 000 + макколли ₩8 000 |

Бюджет дня: $35–45 / 3 150–4 050₽

### День 3 — Воскресенье 15 Мар · «Сочон + Чхандоккун → Вылет»
Транспорт: Метро Линия 3 → ст. Кёнбоккун (выход 2). AREX Seoul Station → Инчхон в 15:30 → прибытие 16:13. Вылет 17:50.

| # | Время | Место | lat | lng | Тип | Заметка |
|---|-------|-------|-----|-----|-----|---------|
| 1 | 09:00–10:30 | Деревня Сочон | 37.5787 | 126.9731 | culture | Café Dalant ₩6 000 |
| 2 | 10:30–13:30 | Дворец Чхандоккун + Тайный сад | 37.5794 | 126.9910 | culture | Дворец ₩3 000 + Тайный сад ₩8 000. Бронь онлайн! |
| 3 | 13:30–14:30 | Прощальный обед, Чонно 3-га | 37.5737 | 126.9901 | food | Сет-меню ₩12 000–15 000 |
| 4 | 15:00–15:20 | 🧳 Чекаут из отеля | 37.5716 | 127.0114 | transit | Такси до Seoul Station ~₩9 000 |
| 5 | 15:30→16:13 | AREX: Seoul Station → Инчхон | 37.5547 | 126.9706 | transit | ₩9 500 · посадка 17:50 |

Бюджет дня: $30–40 / 2 700–3 600₽

---

## Дизайн public/index.html

### Цвета
```css
--bg:       #F7F3EE;
--text:     #1A1410;
--accent:   #C4705A;
--day1:     #8B3A3A;
--day2:     #2C4A6E;
--day3:     #3D6B4F;
--done:     #6B7B6B;
--card-bg:  #FFFFFF;
--muted:    #888880;
```

### Шрифты (Google Fonts)
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```
- Заголовки: `Playfair Display`
- Интерфейс: `Inter`

### Иконки типов
```js
const ICONS = {
  culture: '🏛', food: '🍜', scenic: '🌿',
  market: '🛍', transit: '🚇', rest: '🛏'
};
```

---

## Функциональность

### Навигация
- Три sticky-таба вверху: **Пт 13**, **Сб 14**, **Вс 15**
- Активный таб — цвет соответствующего дня
- Текущий день определяется автоматически по `new Date()`

### Карточки активностей
Каждая карточка:
```
[иконка] [время]            [чекбокс ✓]
[название места — крупно]
[заметка — мелко, серо]
[📍 Открыть в Maps]  [🗺 Маршрут сюда]
```
- **📍 Открыть в Maps** → `https://www.google.com/maps/search/?api=1&query=LAT,LNG`
- **🗺 Маршрут сюда** → `https://www.google.com/maps/dir/?api=1&destination=LAT,LNG`
- Левая цветная полоса = цвет текущего дня
- Выполненная карточка: `opacity: 0.45`, текст названия зачёркнут, фон чуть серее

### Прогресс дня
- Под табами: `«Выполнено: 3 / 7»` + горизонтальный прогресс-бар цветом дня

### Чекбоксы
- Большой круглый чекбокс (44×44px), кастомный стиль
- `localStorage` ключ: `seoul_2026_progress`
- Структура: `{ "day1_item2": true, "day2_item4": true, ... }`

### Фиксированная кнопка «В отель»
- FAB (floating action button) снизу-справа экрана
- Иконка 🏠, тап → `https://www.google.com/maps/dir/?api=1&destination=37.5716,127.0114`
- Всегда поверх контента (z-index высокий)

### Транспортная подсказка дня
- Под прогресс-баром — аккордеон с деталями транспорта дня
- Свёрнут по умолчанию, тап разворачивает

### Бюджет дня
- Карточка в конце списка каждого дня
- Показывает суммы в ₩ / $ / ₽

### Раздел «Полезное»
Аккордеон в конце страницы (всегда виден, не зависит от дня):

**🚇 Транспорт**
- T-money: ₩2 500 / ~$1.8 / ~165₽
- Тариф метро: ₩1 400–1 600 / $1–1.15 / 90–105₽
- AREX Экспресс Инчхон → Seoul Station: 43 мин, ₩9 500 (~$6.9 / ~620₽)
- Такси: приложение Kakao T

**💱 Курс**
- 1 USD ≈ 90 ₽
- 1 000 KRW ≈ $0.73 / 66 ₽
- 10 000 KRW ≈ $7.3 / 660 ₽

**📍 Быстрые ссылки Maps**
- Аэропорт Инчхон: `https://www.google.com/maps/search/?api=1&query=37.4602,126.4407`
- Seoul Station (AREX): `https://www.google.com/maps/search/?api=1&query=37.5547,126.9706`
- Stay 42 Dongmyo: `https://www.google.com/maps/search/?api=1&query=37.5716,127.0114`

### Сброс прогресса
- Кнопка «Сбросить прогресс» в подвале
- Требует confirm() перед сбросом

---

## Мобильная оптимизация

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="theme-color" content="#F7F3EE">
```

```css
/* Убрать задержку 300ms на тапах */
* { touch-action: manipulation; }

/* Safe area для iPhone */
body {
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
}

/* Все кнопки — минимум 44px */
button, .card-action { min-height: 44px; min-width: 44px; }

/* Шрифт не меньше 16px (iOS не зумит) */
input, textarea { font-size: 16px; }
```

---

## Деплой: пошаговые команды

После создания всех файлов выполни:

```bash
# 1. Установить зависимости
npm install

# 2. Проверить локально
npm start
# открыть http://localhost:3000

# 3. Инициализировать git
git init
git add .
git commit -m "init: Seoul trip tracker"

# 4. Создать репозиторий на GitHub (через gh CLI)
gh repo create seoul-trip --public --push --source=.

# Если gh CLI не установлен:
# Создать вручную на github.com, затем:
# git remote add origin https://github.com/USERNAME/seoul-trip.git
# git push -u origin main

# 5. Задеплоить на Railway (через Railway CLI)
railway login
railway init
railway up

# Railway автоматически:
# - обнаружит package.json
# - запустит npm start
# - выдаст публичный URL вида: https://seoul-trip-XXXX.up.railway.app
```

---

## Итоговые требования к результату

- [ ] Сайт открывается на телефоне и выглядит как нативное приложение
- [ ] Три дня маршрута, все 16 активностей на правильных вкладках
- [ ] Каждая карточка имеет кнопку 📍 Maps (открыть место) и 🗺 (маршрут сюда)
- [ ] FAB кнопка 🏠 «В отель» всегда видна
- [ ] Чекбоксы работают и сохраняются в localStorage
- [ ] Прогресс-бар показывает `выполнено / всего` для каждого дня
- [ ] Сайт доступен по публичному Railway URL
- [ ] При пуше в GitHub → Railway автоматически пересобирает сайт