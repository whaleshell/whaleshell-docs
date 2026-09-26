<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Провайдеры

**Провайдер вычислений** — движок, на котором работают песочница и её
egress-прокси. Выбирается через `WHALESHELL_DRIVER` (по умолчанию `docker`),
проверяется командой `whaleshell status`.

<div class="grid cards" markdown>

-   :material-docker:{ .lg .middle } __Docker__ &nbsp; <span class="ws-badge ws-badge--ok">по умолчанию</span>

    ---

    Docker Engine или Docker Desktop. Лучшая совместимость образов и сети;
    на нём все инструкции.

    [:octicons-arrow-right-24: Docker](docker/index.md)

-   :simple-podman:{ .lg .middle } __Podman__ &nbsp; <span class="ws-badge ws-badge--ok">поддерживается</span>

    ---

    Rootless на Linux или Podman Machine на macOS через совместимый с
    Docker Engine API.

    [:octicons-arrow-right-24: Podman](podman/index.md)

-   :material-kubernetes:{ .lg .middle } __Kubernetes__ &nbsp; <span class="ws-badge ws-badge--soon">скоро</span>

    ---

    Песочницы как pod'ы, gateway через Helm.

    [:octicons-arrow-right-24: Kubernetes](kubernetes.md)

-   :material-chip:{ .lg .middle } __MicroVM__ &nbsp; <span class="ws-badge ws-badge--soon">скоро</span>

    ---

    Лёгкая VM на каждую песочницу: граница прочнее, проброс GPU.

    [:octicons-arrow-right-24: MicroVM](microvm.md)

</div>

| Провайдер | `WHALESHELL_DRIVER` | Статус |
|-----------|---------------------|--------|
| Docker | `docker` | По умолчанию, полная поддержка |
| Podman | `podman` | Поддерживается через Engine API |
| Kubernetes | `kubernetes` | Скоро |
| MicroVM | `vm` | Скоро |

!!! tip "Не путать с credential-провайдерами"
    `--provider github`, `--provider cursor` и другие подключают к песочнице
    секреты и egress-правила. Они работают с любым провайдером вычислений —
    см. [Credential-провайдеры](../guides/credentials.md).
