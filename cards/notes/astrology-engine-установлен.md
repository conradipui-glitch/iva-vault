---
type: note
description: >-
  Установка и работа astrology-engine: SwissEph-движок, 12 рун по знакам Луны, «Руна дня». 07.08.2026 добавлено: Human Design движок SharpAstrology 1.2.0 (3 слоя трактовки линий) и расписание астропрогноза (07:00 iva-astro, 08:00 iva-money).
tags: [astrology, swiss-ephemeris, cli, installed, runes, python, hrabanazviking, human-design]
status: active
confidence: EXTRACTED
created: 2026-08-05
source: daily/2026-08-05.md
domain: personal
updated: 2026-08-08
access_count: 2
last_accessed: 2026-07-23
relevance: 0.584
tier: cold
---

# Astrology Engine — установлен

## Что это
Полноспектровый астрологический движок на Swiss Ephemeris (pyswisseph), без облака и API-ключей. Клонирован в `/root/iva/repos/astrology-engine`. Установлен: `pip install pyswisseph kerykeion geopy timezonefinder pytz`.

## Запуск
```bash
cd /root/iva/repos/astrology-engine && python3 astrology_engine.py <режим> [флаги]
```
Проверено: `lunar` (текущая Луна: фаза, позиция, руна, аспекты), `transit --date ... --city ... --nation ... [--transit-date ...]` (транзиты к натальной карте), `synastry`, `composite`, `synergy`, `predict`, `geoastrology`, `aspect-grid`.

## Режимы (16)
natal, transits, solar-return, lunar-return, progressions, synastry, composite, synergy, predict (4 слоя: точные транзиты, станции, ингрессии, затмения; окно по умолчанию год), geoastrology (астрокартография, MC/IC/ASC/DSC линии), aspect-grid, lunar, planetary-hours, eclipses, arabic-lots (жребии), hellenistic.

## Геокодинг
Каскад: --lat/--lon → Nominatim (OSM, бесплатно) → kerykeion geonames (SQLite) → hardcoded ~70 городов → предупреждение (0,0). Часовой пояс: timezonefinder + pytz.

## Нюансы
- Названия режимов в CLI чуть отличаются от README (например `transit`, `lunar`).
- DeprecationWarning про utcnow — безвреден, фильтровать в выводе.
- Требует сеть для Nominatim (если город не из базы); для надёжности можно передавать `--lat/--lon`.
- Движок ориентирован на Hermes Agent skill, но работает standalone.
- Есть docs/, ARCHITECTURE.md, COMMANDS.md, ROADMAP.md.

## Связанные
- Автор: [[cards/contacts/volmarr-wyrd-hrabanazviking]] — мануал для агентов в `/root/iva/repos/hrabanazviking`
- RuneTarotEngine, Kybalion — тоже его эзотерические репозитории

## Related
- [[cards/contacts/volmarr-wyrd-hrabanazviking]]
## History

- 2026-08-06: в теле был дубль H1 (два разных заголовка: «Astrology Engine — установлен» и «Astrology Engine (hrabanazviking/astrology-engine)») — свёрнут в один канонический.

## Log
- 2026-08-06:
  Руны · 05.08.2026:
  - В классическом Старшем Футарке 24 руны (Феху…Отала), но в astrology-engine зашито только 12 — по одной на знак зодиака (Луна в Тельце → Феху, Луна во Льве → Совелу и т.д.). Урезанный набор для простоты.
  - 18:41 владелец: «давай пока просто руну с картинкой» — показана карточка «Руна дня» (тёмный викингский фон, золотая рамка, дата, символ руны, название ФЕХУ, значение, фаза луны).
  - Механика: astrology-engine в режиме lunar → руна по знаку Луны → карточка через Pillow → отправка в чат. Вариант команды /rune; владелец упоминал web3-меню в Telegram с анимацией.
  - 18:48 владелец: «Давай это отложим… надо понять что постить сейчас в тредс» — расширение до 24 рун и «рунный календарь» ОТЛОЖЕНЫ. Полный набор 24 рун (Феху, Уруз, Турисаз, Ансуз, Райдо, Кано, Гебо, Вуньо, Хагалаз, Наутиз, Иса, Йера, Эйваз, Пертро, Альгиз, Совелу, Тейваз, Беркано, Эваз, Манназ, Лагуз, Ингуз, Дагаз, Отала) — предложен, не утверждён.
- 2026-08-08:
  **Human Design — система и движок (07.08.2026):** классический Human Design (система Рейв, Ра Уру Ху): 64 ворота, 6 линий на ворота (384), центры, авторитеты, профили, Variables. Движок — SharpAstrology.HumanDesign 1.2.0 поверх SwissEph; эфемериды Swiss (.se1) файловые, строгий режим (нет тихого падения на Moshier). Тип, ворота/линии, цвет/тон/база, крест, Variables — из расчёта; стратегия и «не-я» — фиксированная таблица по типу. Справочник трактовки линий — 3 слоя: `source` (12 линий, цитаты), `composed` (склейка), `generated` (тексты модели, не канон); «Рейв И-Цзин» под копирайтом — канона 384 линий в открытом доступе нет. Планеты экзальтации/ущерба — таблица FixingState из кода библиотеки. Расчёт и трактовка разделены: числа в `data/hd/*.json`, разборы — карточками в vault (напр. `cards/hd/anton.md`). Карта Антона: Манифестирующий Генератор, профиль 6/2, Сакральный авторитет, LeftAngleCrossOfTheAlpha, рождение 1984-07-30 17:50 Омск.
  
  **Расписание (07.08.2026, systemd-таймеры, Омск):** 07:00 — `iva-astro.timer`/`iva-astro.service`: ежедневный астропрогноз (фаза Луны, руна дня, ключевые аспекты, фон по деньгам/отношениям) по наталке 30.07.1984. 08:00 — `iva-money.timer`/`iva-money.service`: проверка финансовых окон, скрипт `/root/iva/scripts/money-windows.mjs`, state `.state/money-windows-sent.json` (без дублей); предупреждение за 2 дня до окна («ПОДЪЁМ — ДЕЙСТВУЙ»), за 5 дней — «ПОДГОТОВКА».
