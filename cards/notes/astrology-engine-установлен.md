---
type: note
description: >-
  Установка и работа astrology-engine (hrabanazviking/astrology-engine): 12 рун по знакам Луны, «Руна дня». Расширение до 24 рун отложено.
tags: [astrology, swiss-ephemeris, cli, installed, runes, python, hrabanazviking]
status: active
confidence: EXTRACTED
created: 2026-08-05
source: daily/2026-08-05.md
domain: personal
updated: 2026-08-06
access_count: 2
last_accessed: 2026-07-23
relevance: 0.867
tier: warm
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

## Log
- 2026-08-06:
  Руны · 05.08.2026:
  - В классическом Старшем Футарке 24 руны (Феху…Отала), но в astrology-engine зашито только 12 — по одной на знак зодиака (Луна в Тельце → Феху, Луна во Льве → Совелу и т.д.). Урезанный набор для простоты.
  - 18:41 владелец: «давай пока просто руну с картинкой» — показана карточка «Руна дня» (тёмный викингский фон, золотая рамка, дата, символ руны, название ФЕХУ, значение, фаза луны).
  - Механика: astrology-engine в режиме lunar → руна по знаку Луны → карточка через Pillow → отправка в чат. Вариант команды /rune; владелец упоминал web3-меню в Telegram с анимацией.
  - 18:48 владелец: «Давай это отложим… надо понять что постить сейчас в тредс» — расширение до 24 рун и «рунный календарь» ОТЛОЖЕНЫ. Полный набор 24 рун (Феху, Уруз, Турисаз, Ансуз, Райдо, Кано, Гебо, Вуньо, Хагалаз, Наутиз, Иса, Йера, Эйваз, Пертро, Альгиз, Совелу, Тейваз, Беркано, Эваз, Манназ, Лагуз, Ингуз, Дагаз, Отала) — предложен, не утверждён.

## Related
- [[cards/contacts/volmarr-wyrd-hrabanazviking]]
## History

- 2026-08-06: в теле был дубль H1 (два разных заголовка: «Astrology Engine — установлен» и «Astrology Engine (hrabanazviking/astrology-engine)») — свёрнут в один канонический.
