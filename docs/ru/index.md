---
hide:
  - navigation
  - toc
---

<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

<div class="ws-hero" markdown>

# whaleshell

<p class="ws-hero__tagline">Песочницы с политикой для coding-агентов.<br>
Cursor, Claude, Codex — или любой свой агент — на Docker или Podman.</p>

[Начать](get-started/index.md){ .md-button .md-button--primary }
[Провайдер Docker](providers/docker/index.md){ .md-button }

</div>

## Быстрый старт

```bash
curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml

whaleshell sandbox connect demo
```

!!! note "Важно"
    Перед созданием sandbox нужен работающий контейнерный движок (Docker или Podman).

## Разделы

<div class="grid cards" markdown>

-   :material-rocket-launch:{ .lg .middle } __Быстрый старт__

    ---

    Установка CLI, первый sandbox, exec и connect.

    [:octicons-arrow-right-24: Установка](get-started/install.md)

-   :material-docker:{ .lg .middle } __Провайдеры вычислений__

    ---

    Docker — по умолчанию; Podman работает через Engine API.

    [:octicons-arrow-right-24: Провайдеры](providers/index.md)

-   :material-shield-lock:{ .lg .middle } __Политика__

    ---

    Egress по умолчанию запрещён, L7-allowlist, предложения через `policy.local`.

    [:octicons-arrow-right-24: Политика](guides/policy.md)

-   :material-key-chain:{ .lg .middle } __Секреты__

    ---

    Секреты хранятся в gateway один раз и подключаются через `--provider`.

    [:octicons-arrow-right-24: Credential-провайдеры](guides/credentials.md)

-   :material-sitemap:{ .lg .middle } __Концепции__

    ---

    Плоскости control, data и enforcement; путь запроса на создание.

    [:octicons-arrow-right-24: Архитектура](concepts/architecture.md)

-   :material-console:{ .lg .middle } __Справка__

    ---

    CLI, образы sandbox на GHCR, переменные окружения.

    [:octicons-arrow-right-24: Справка](reference/index.md)

</div>
