---
type: note
description: "Минимальная сетевая гигиена VPS: SSH, внутренние порты, reverse proxy и TLS."
tags: [curator, infrastructure, network, ssh, ufw, tls, reverse-proxy, security]
status: active
confidence: INFERRED
domain: knowledge
created: 2026-08-01
source: christian-lempa-corpus-curated
last_accessed: 2026-08-04
tier: warm
relevance: 0.835
---

# Сеть и доступ

Минимизируй поверхность атаки, но не усложняй доступ без причины.

- Базы данных и внутренние API не публикуй напрямую в интернет.
- Публичные веб-сервисы выводи через TLS reverse proxy; 80/443 — нормальные публичные порты для этой цели.
- SSH защищай ключами, отключённой парольной аутентификацией, firewall и контролем попыток входа.
- Перед правкой UFW держи вторую рабочую SSH-сессию или доступ к аварийной консоли провайдера.
- Выбирай Caddy, Traefik или Nginx/Angie по реальной сложности: Caddy проще для малого числа сервисов; Traefik удобен при динамических Docker labels; Nginx/Angie полезен для привычной статической конфигурации.

Любая сетевая правка должна иметь проверку снаружи и быстрый способ возврата прежнего правила.
