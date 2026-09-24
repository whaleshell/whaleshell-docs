<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Безопасность

| Граница | Доверие |
|---------|---------|
| Host Engine / Desktop | Доверенная машина оператора |
| Sandbox-контейнер | Недоверенный агент |
| Egress proxy | Доверенный sidecar |
| Store секретов gateway | Доверенный control plane |
| noVNC / display | Только loopback оператора |

## По умолчанию

- Нет `docker.sock` в sandbox
- Bind workspace с deny-list для `$HOME`, `~/.ssh`, `~/.aws`, `~/.cursor`
- Default-deny сеть; allowlist из policy + composition провайдеров
- Секреты как `whaleshell:resolve:env:…` с rewrite только на egress
- Default seccomp Docker; `no-new-privileges`; `CapDrop=NET_RAW`
- Landlock через `whaleshell-init` при ABI ≥ 1 (на Desktop часто ABI 0)

## Credentials

Предпочитайте `provider create`, а не `--env`. Cursor — через `agent login`,
без инжекта `CURSOR_API_KEY`. См. [Credentials](Ru-Guides-Credentials).

## Гигиена ресурсов

Агенты без лимита и безлимитные container logs раздувают VM Docker Desktop.
Используйте `--memory`, soft defaults и ротацию json-file по умолчанию:

- [Ресурсы Docker](Ru-Providers-Docker-Resources)
- [Логи Docker](Ru-Providers-Docker-Logging)

Полная модель: [SECURITY.md](../../../docs/SECURITY.md).
