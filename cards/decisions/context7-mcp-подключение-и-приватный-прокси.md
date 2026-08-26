---
type: "decision"
description: "Context7 MCP подключён к workflow разработки (по просьбе владельца 23.08): только 2 read-only инструмента, локальный privacy-прокси на 127.0.0.1, вывод ограничен 8000 символами, изолирован от .env/vault/SSH/GPG/user D-Bus."
tags: ["context7","mcp","workflow","security","proxy","codesearch"]
status: "active"
confidence: "EXTRACTED"
domain: "work"
created: "2026-08-24"
source: "daily/2026-08-24.md"
access_count: 1
last_accessed: "2026-07-15"
relevance: 0.355
tier: "cold"
updated: "2026-08-24"
---

# context7-mcp-подключение-и-приватный-прокси

23.08.2026 владелец попросил поставить Context7 MCP и использовать его для доработки нашего workflow. Подключение официального Context7.

Что сделано:
- Доступны только два read-only инструмента: поиск ID библиотеки (resolve-library-id) и получение документации (query-docs). Allowlist минимален для заявленного сценария.
- Добавлен локальный privacy-прокси на 127.0.0.1 (data/custom/scripts/context7-proxy.mjs): наружу не уходят многострочный текст, секреты, приватные пути, email, логи и фрагменты кода. Валидация NFKC, fail-closed на неоднозначном тексте.
- Ответ ограничен 8000 символами и помечается как недоверенная внешняя документация (UNTRUSTED), с marker и [TRUNCATED] в пределах лимита.
- Прокси работает отдельным systemd-сервисом (iva-context7-proxy.service), активен и в автозапуске, слушает только 127.0.0.1:8787, capabilities обнулены, сеть ограничена AF_INET/AF_INET6, закрыты .env, vault, tasks, usage, SSH/GPG и user D-Bus.
- Обновлён gstack-workflow: Context7 используется точечно только для актуальных API внешних библиотек. Локальный код и тесты остаются первичным источником. Если ID библиотеки известен — пропускаем лишний поиск и сразу берём нужный фрагмент.
- API-ключ не обязателен (сейчас публичный режим); при необходимости отдельный ключ добавляется без открытия общего .env. Ключ читается только из process.env.CONTEXT7_API_KEY и применяется после перезапуска.

Аудит безопасности (adversarial review, несколько раундов): критичных ломающих находок нет; закрыты реальные обходы DLP, ограничение ответа, lifecycle cleanup, isError, изоляция root user-service. Итог — ready / низкий риск. Защита от prompt injection внутри внешней документации остаётся модельной (недетерминированной). Модель не является security boundary; остаточный риск — недетерминированный фильтр инъекций.

Остался перезапуск корневой Ивы штатной командой /restart, чтобы она увидела новое подключение.

## Related

- [[cards/decisions/gstack-workflow-адаптация-методологии-под-иву]]
- [[cards/decisions/пилот-явного-prompt-caching-для-iva]]
- [[cards/notes/curator-hamel-husain]]
- [[cards/decisions/_index|Решения]]

## Log

- 2026-08-24: 23.08.2026 владелец попросил поставить Context7 MCP и использовать его для доработки нашего workflow. Подключение официального Context7.
