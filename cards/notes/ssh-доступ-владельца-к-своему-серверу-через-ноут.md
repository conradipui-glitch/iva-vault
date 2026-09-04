---
type: "note"
description: "Сервер conradipui.fvds.ru (85.137.95.104), порт 48176, вход только по SSH-ключу (пароль отключён). 04.09.2026 добавлен ключ tahara-key (ed25519) без ограничения по IP."
tags: ["ssh","vps","server-admin","access"]
status: "active"
confidence: "EXTRACTED"
domain: "knowledge"
created: "2026-09-05"
source: "daily/2026-09-05.md"
last_accessed: "2026-09-05"
tier: "active"
relevance: 1.0
access_count: 1
---

# SSH-доступ владельца к своему серверу через ноут

Владелец (12:32, 04.09.2026) попросил команду для подключения к серверу через ноут. Сервер: conradipui.fvds.ru, IP 85.137.95.104, порт 48176 (нестандартный), пользователь root, вход по паролю отключён (PasswordAuthentication no) — только SSH-ключ. Команда: ssh root@conradipui.fvds.ru -p 48176.

В ~/.ssh/authorized_keys на сервере разрешены два ключа: supportAccessKey (ограничен IP 85.198.118.171 и 85.198.75.83) и vps-n8n-2026-07-28. 04.09.2026 владелец прислал публичную часть своего ключа (ed25519, комментарий tahara-key); она добавлена в authorized_keys без ограничений по IP — заходить можно откуда угодно.

## Related

- [[cards/notes/_index]]
- [[cards/projects/гермес-агент-сосед-на-vps]]
- [[cards/projects/hd-продукт-бот-астрология-денежный-код-на-рф]]
