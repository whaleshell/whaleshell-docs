<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Установка

## Релизный бинарь

```bash
curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh
whaleshell version
```

| Цель | Команда |
|------|---------|
| Последний релиз | `curl … \| sh` |
| Закрепить версию | `WHALESHELL_VERSION=v0.1.0-alpha.1 sh` |
| Nightly | `WHALESHELL_VERSION=nightly sh` |
| Свой каталог | `WHALESHELL_INSTALL_DIR=/usr/local/bin sh` |

По умолчанию бинарь ставится в `~/.local/bin`. Каталог должен быть в `PATH`.

`whaleshell install` (когда бинарь уже есть) только копирует или делает symlink
в `~/.local/bin` и **не** качает релизы.

## Из исходников (hub workspace)

```bash
cd /path/to/whaleshell
export GOWORK=$PWD/go.work

go build -C whaleshell-cli -o whaleshell ./cmd/whaleshell
./whaleshell install
whaleshell version
```

## Контейнерный движок

Перед create установите и запустите один провайдер вычислений:

| Провайдер | Документация |
|-----------|--------------|
| Docker (default) | [Требования](Ru-Providers-Docker-Prerequisites) |
| Podman | [Требования](Ru-Providers-Podman-Prerequisites) |

```bash
whaleshell doctor
whaleshell status
```

## Gateway

Для proxy, encrypted secrets и `--provider` нужен доступный gateway.

### Локальный бинарь

```bash
go build -C whaleshell-gateway -o whaleshell-gateway ./cmd/whaleshell-gateway
./whaleshell-gateway --listen 127.0.0.1:7443 &

whaleshell gateway add http://127.0.0.1:7443 --local --name local
whaleshell gateway select local
whaleshell gateway info
```

`whaleshell gateway ensure` поднимает локальный gateway, если ни один не выбран.

### Docker Compose

```bash
# опционально постоянный KEK:
# export WHALESHELL_SECRETS_KEK="$(openssl rand -base64 32)"

docker compose -f packaging/compose/docker-compose.yml up -d --build
whaleshell gateway add http://127.0.0.1:7443 --local --name local
whaleshell gateway select local
```

OIDC (Dex): `packaging/compose/docker-compose.oidc.yml`, затем
`whaleshell gateway login`.

KEK и store: [Credential-провайдеры](Ru-Guides-Credentials).

## Образы

```bash
task runtime:image:cli             # whaleshell-sandbox:local
task docker:agent:cursor           # опциональный flavor агента
# или: docker pull ghcr.io/whaleshell/whaleshell/sandboxes/base:latest
```

Каталог: [Образы](Ru-Reference-Images).

## Чеклист

| Проверка | Команда |
|----------|---------|
| CLI | `whaleshell version` |
| Engine | `whaleshell doctor` |
| Драйвер | `whaleshell status` |
| Gateway | `whaleshell gateway info` |

Далее: [Первый sandbox](Ru-Get-Started-First-Sandbox).
