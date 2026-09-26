<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Провайдеры вычислений

**Провайдер вычислений** — контейнерный backend, который создаёт sandbox и
proxy-контейнеры. Выбор: `WHALESHELL_DRIVER` (по умолчанию `docker`).

| Провайдер | `WHALESHELL_DRIVER` | Зрелость |
|-----------|---------------------|----------|
| [Docker](./docker/index.md) | `docker` | По умолчанию, полная поддержка |
| [Podman](./podman/index.md) | `podman` | Через Docker-совместимый Engine API |
| Kubernetes | `kubernetes` | Эксперимент |
| MicroVM | `vm` | Эксперимент |

Credential-провайдеры (`--provider github`, `--provider cursor`, …) — отдельная
сущность: секреты и правила egress. См. [Credential-провайдеры](../guides/credentials.md).

## Когда выбирать Docker

- Уже есть Docker Engine или Docker Desktop.
- Нужна максимальная совместимость образов и сети.
- Идёте по основным туториалам и compose-пакетам.

## Когда выбирать Podman

- Предпочитаете rootless на Linux.
- На хосте нельзя Docker.
- Устраивает паритет Engine API (те же labels, сети, sidecar) с известными
  оговорками по rootless-сети.

```bash
whaleshell status    # активный драйвер
```
