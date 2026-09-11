---
type: "project"
description: "Второй агент на том же VPS («сосед», glmbot): dashboard на порту 9119, gateway как systemd-сервис, модель gpt-5.6-luna (Codex) как у Ивы; Telegram-бот подключается отдельно. Панель соседа открывается по /glmbot/ в nginx (не как n8n)."
tags: ["agent","vps","systemd","telegram","infra"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-31"
source: "daily/2026-08-31.md"
last_accessed: "2026-08-31"
tier: "warm"
relevance: 0.82
updated: "2026-09-07"
---

# Гермес — агент-сосед на VPS

30.08.2026 владелец попросил «оживить» агента-соседа Гермеса («сосед недавно появился, что-то подзавис»). Dashboard отвечал на порту 9119, но gateway висел/не был запущен — поднят системным сервисом: active (running), автозапуск включён, heartbeat снова виден cron. Messaging-платформы у Гермеса поначалу не были включены.

По просьбе владельца Гермесу поставлена та же модель, что у Ивы: gpt-5.6-luna, провайдер OpenAI Codex / ChatGPT, reasoning max, авторизация активна; gateway работает и перезапускается автоматически. Модель ответила на тест-проверку, но Гермес молчал, потому что не был подключён мессенджер — для Telegram нужен отдельный бот от @BotFather; токен передан владельцем 30.08 (значение в память не записывается).

30.08 по команде владельца установлен sudoers-файл /etc/sudoers.d/hermes-disk из /home/hermes-pilot/hermes-sudoers (права 0440, root:root; visudo на сервере нет, синтаксис отдельно не проверялся).

## Related

- [[cards/projects/_index]]
- [[cards/projects/черновики-openbot-mcp-roadmap-и-локальной-llm-вечер-23-08]]
- [[cards/projects/iva-write-пул-исполнителей-подписки]]

## Log

- 2026-09-07: 06.09.2026 сосед (glmbot) через инбокс /home/hermes-pilot/iva-inbox/ поставил задачу: добавить location /glmbot/ в nginx, чтобы панель соседа открывалась как отдельный ресурс, а не как n8n. Выполнено: бэкенд на 127.0.0.1:8731 живой (200), сделан бэкап /etc/nginx/conf.d/n8n.conf.bak-20260906-glmbot, вставлен блок location /glmbot/ → proxy_pass 127.0.0.1:8731 (выше location /, по образцу /app/), nginx -t валиден, перезагружен. Проверка: /glmbot/ → 200 (HTML панели glmbot), / (n8n) → 200, /app/ → 200 — не сломано. Ранее в тот же день выполнена ещё одна задача glmbot: перезапуск hermes-gateway.service (перечитал свежий конфиг) и добавлено sudoers-правило /etc/sudoers.d/iva-glmbot-restart (hermes-pilot может перезапускать шлюз без пароля).
