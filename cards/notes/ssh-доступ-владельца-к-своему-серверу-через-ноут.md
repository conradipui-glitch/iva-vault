---
type: "note"
description: "Сервер 85.137.95.104:48176, вход только по SSH-ключу. 15.09.2026 владелец подключился из MobaXterm — добавлены три новых RSA-ключа, всего шесть в authorized_keys."
tags: ["ssh","vps","server-admin","access","mobaxterm"]
status: "active"
confidence: "EXTRACTED"
domain: "knowledge"
created: "2026-09-05"
source: "daily/2026-09-05.md"
last_accessed: "2026-09-16"
tier: "active"
relevance: 0.925
access_count: 1
updated: "2026-09-16"
---

# SSH-доступ владельца к своему серверу через ноут

Владелец (12:32, 04.09.2026) попросил команду для подключения к серверу через ноут. Сервер: conradipui.fvds.ru, IP 85.137.95.104, порт 48176 (нестандартный), пользователь root, вход по паролю отключён (PasswordAuthentication no) — только SSH-ключ. Команда: ssh root@conradipui.fvds.ru -p 48176.

В ~/.ssh/authorized_keys на сервере разрешены два ключа: supportAccessKey (ограничен IP 85.198.118.171 и 85.198.75.83) и vps-n8n-2026-07-28. 04.09.2026 владелец прислал публичную часть своего ключа (ed25519, комментарий tahara-key); она добавлена в authorized_keys без ограничений по IP — заходить можно откуда угодно.

## Related

- [[cards/notes/_index]]
- [[cards/projects/гермес-агент-сосед-на-vps]]
- [[cards/projects/hd-продукт-бот-астрология-денежный-код-на-рф]]

## Log

- 2026-09-16:
  Владелец (12:32, 04.09.2026) попросил команду для подключения к серверу через ноут. Сервер: conradipui.fvds.ru, IP 85.137.95.104, порт 48176 (нестандартный), пользователь root, вход по паролю отключён (PasswordAuthentication no) — только SSH-ключ. Команда: ssh root@conradipui.fvds.ru -p 48176.
  
  В ~/.ssh/authorized_keys на сервере разрешены два ключа: supportAccessKey (ограничен IP 85.198.118.171 и 85.198.75.83) и vps-n8n-2026-07-28. 04.09.2026 владелец прислал публичную часть своего ключа (ed25519, комментарий tahara-key); она добавлена в authorized_keys без ограничений по IP — заходить можно откуда угодно.
  
  15.09.2026 владелец настроил терминальное подключение из MobaXterm (Windows): сначала упёрся в «No supported authentication methods (server sent: publickey)» — пароль на сервере отключён, нужен ключ. В течение дня добавлены ещё три RSA-публичных ключа: rsa-key-20260915, mobaxterm-root-85.137.95.104-20260915 (4096 бит, сгенерирован самим MobaXterm) и его v3-версия. Промежуточная ошибка «Unable to use certificate file … .ppk» была клиентской — MobaXterm не прочитал файл с пробелами в пути; решилось использованием нативно поддерживаемого ключа. В 14:52 подключение заработало. Итого в authorized_keys шесть ключей, ничего не удалялось.
