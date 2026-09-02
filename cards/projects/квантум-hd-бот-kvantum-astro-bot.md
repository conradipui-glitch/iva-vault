---
type: "project"
description: "MVP-проверка спроса: отдельный TG-бот Human Design. Онбординг дата/время/город → бодиграф PNG (cosmic) + выжимка → кнопка waitlist «ежедневный прогноз». Запущен 26.08 как systemd --user kvantum-astro. Критерий GO общий с лендингом: ≥20 заявок, 3+ предоплаты."
tags: ["human-design","telegram-bot","mvp","astrology","waitlist"]
status: "active"
confidence: "EXTRACTED"
created: "2026-08-26"
source: "daily/2026-08-26.md"
domain: "work"
last_accessed: "2026-08-27"
tier: "active"
relevance: 0.895
---

# Квантум HD-бот kvantum_astro_bot

Продукт: бесплатная бодиграф-карта по дате рождения → подписка на ежедневный прогноз (299/499/799 ₽/мес — цены из плана MVP). Бот — часть проверки спроса к задаче «MVP HD-бот» (критерий GO ≥20 заявок и 3+ предоплаты).

Технически:
- код: data/custom/kvantum-astro/scripts/bot.py (python3 + requests, long polling)
- токен: data/custom/kvantum-astro/.env (chmod 600, вне git)
- сервис: systemctl --user {status,restart} kvantum-astro; логи journalctl --user -u kvantum-astro
- расчёт: обёртка scripts/iva-hd.py (движок repos/hd-sharp), карта юзера хранится в data/hd/u<chat_id>.json
- побочный эффект обёртки — карточка в vault/cards/hd/: бот её сразу удаляет (чужие карты в память Ивы не попадают)
- users.json рядом со скриптом: стадии онбординга + поле waitlist (время нажатия кнопки) = лист ожидания
- витрина: имя «Квантум · Human Design», описания и аватар (cosmic bodygraph) выставлены через Bot API 26.08

Название «AstraBulda» владелец не подтвердил; юзернейм бота kvantum_astro_bot создан им через BotFather 26.08.

Дальше: лендинг с waitlist (дублирует воронку вне Telegram), трафик, потом мультиюзерный прогноз 07:00.

## Related

- [[cards/projects/hd-продукт-бот-астрология-денежный-код-на-рф]]
