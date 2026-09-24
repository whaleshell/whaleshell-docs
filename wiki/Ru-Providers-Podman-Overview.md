<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Провайдер Podman

Podman — полноценный провайдер вычислений. whaleshell находит API-сокет Podman
и идёт по пути Docker Engine client (`driver.OpenEngine("podman")`). Labels,
сети, proxy sidecar и exec совпадают с Docker.

## Страницы

| Страница | Тема |
|----------|------|
| [Требования](Ru-Providers-Podman-Prerequisites) | Сокет, machine, rootless |
| [Создание sandbox](Ru-Providers-Podman-Create-Sandbox) | Переключение драйвера и create |
| [Ограничения](Ru-Providers-Podman-Limitations) | Rootless-сеть, пробелы MVP |
| [Устранение неполадок](Ru-Providers-Podman-Troubleshooting) | Сокет и netavark |

## Активация

```bash
export WHALESHELL_DRIVER=podman
# опционально:
# export WHALESHELL_PODMAN_SOCKET=$XDG_RUNTIME_DIR/podman/podman.sock

whaleshell status    # driver: podman
```

Флаги ресурсов, ротация логов, slim proxy и soft defaults — как у Docker:
[Ресурсы Docker](Ru-Providers-Docker-Resources), [Логи Docker](Ru-Providers-Docker-Logging).
