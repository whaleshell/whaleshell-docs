<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Провайдеры вычислений

**Провайдер вычислений** — контейнерный backend, который создаёт sandbox и
proxy-контейнеры. Выбор: `WHALESHELL_DRIVER` (по умолчанию `docker`).

| Провайдер | `WHALESHELL_DRIVER` | Зрелость |
|-----------|---------------------|----------|
| [Docker](Ru-Providers-Docker-Overview) | `docker` | По умолчанию, полная поддержка |
| [Podman](Ru-Providers-Podman-Overview) | `podman` | Через Docker-совместимый Engine API |
| Kubernetes | `kubernetes` | Эксперимент — [exp/KUBERNETES](../../../exp/KUBERNETES.md) |
| MicroVM | `vm` | Эксперимент — [exp/MICROVM](../../../exp/MICROVM.md) |

Credential-провайдеры (`--provider github`, `--provider cursor`, …) — отдельная
сущность: секреты и правила egress. См. [Credential-провайдеры](Ru-Guides-Credentials).

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
