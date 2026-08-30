---
type: note
description: Эксплуатация IVA и Telegram-моста как нативных user-level systemd служб.
tags: [curator, infrastructure, iva, telegram, systemd, user-service, diagnostics]
status: active
confidence: EXTRACTED
domain: knowledge
created: 2026-08-01
source: current-vps-architecture
last_accessed: 2026-08-04
tier: "cold"
relevance: 0.595
---

# IVA и Telegram-мост

IVA и `iva-telegram-poll.service` — не Docker-контейнеры. Их статус и журналы проверяются в user-level systemd.

- Статус: `systemctl --user status iva.service iva-telegram-poll.service`.
- Логи: `journalctl --user -u iva.service` и `journalctl --user -u iva-telegram-poll.service`.
- После перезагрузки VPS обе службы должны быть enabled и active.
- Проверка IVA: локальный HTTP-ответ плюс реальное сообщение боту.
- Проверка Telegram-моста: обработка тестового сообщения без ошибок Telegram API.

Не выдавай ответ прокси за подтверждение работы IVA. LLM, поиск и голос могут занимать заметное время; оценивай завершение пользовательского сценария, а не мгновенность ответа.
