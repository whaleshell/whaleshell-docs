<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Провайдер Docker

Docker — провайдер вычислений по умолчанию. whaleshell обращается к локальному
Engine API (`DOCKER_HOST` / сокет Desktop), создаёт внутреннюю сеть на sandbox,
поднимает egress-sidecar, затем sandbox-контейнер.

## Страницы

| Страница | Тема |
|----------|------|
| [Требования](Ru-Providers-Docker-Prerequisites) | Engine, Desktop VMM, образы |
| [Создание sandbox](Ru-Providers-Docker-Create-Sandbox) | `sandbox create` / connect / delete |
| [Ресурсы и лимиты](Ru-Providers-Docker-Resources) | CPU, память, PIDs, soft defaults |
| [Логирование](Ru-Providers-Docker-Logging) | Ротация логов контейнеров, кольца gateway |
| [Устранение неполадок](Ru-Providers-Docker-Troubleshooting) | Типичные сбои |

## Схема (один sandbox)

```text
host Docker Engine
├── whaleshell-<name>              sandbox (образ агента)
├── whaleshell-proxy-<name>        egress sidecar (slim base)
├── whaleshell-net-<name>          внутренняя сеть
├── whaleshell-data-<name>         опциональный data volume
└── whaleshell-ca-<name>           MITM CA (если proxy включён)
```

## Активация

```bash
unset WHALESHELL_DRIVER          # или: export WHALESHELL_DRIVER=docker
whaleshell doctor
whaleshell status
```

В статусе ожидайте `driver: docker`.
