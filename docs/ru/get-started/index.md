<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Быстрый старт

От нуля до агента в песочнице. Выполняйте команды по порядку — каждый шаг
заканчивается проверкой.

<div class="ws-steps" markdown>

## Установите CLI

=== "Релизный бинарь"

    ```bash
    curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh
    whaleshell version
    ```

    Бинарь ставится в `~/.local/bin` — этот каталог должен быть в `PATH`.
    Закрепить версию: `WHALESHELL_VERSION=v0.1.0-alpha.1`, другой каталог:
    `WHALESHELL_INSTALL_DIR=/usr/local/bin`.

=== "Из исходников"

    ```bash
    cd /path/to/whaleshell
    export GOWORK=$PWD/go.work

    go build -C whaleshell-cli -o whaleshell ./cmd/whaleshell
    ./whaleshell install
    whaleshell version
    ```

## Запустите контейнерный движок

Нужен работающий провайдер вычислений. По умолчанию — Docker.

=== "Docker"

    Docker Engine 24+ или Docker Desktop. На macOS и Windows лучше backend
    **Docker VMM**.

    ```bash
    docker info
    whaleshell doctor
    whaleshell status
    ```

=== "Podman на macOS"

    ```bash
    podman machine init     # один раз
    podman machine start
    export WHALESHELL_DRIVER=podman
    whaleshell status
    ```

=== "Podman на Linux"

    ```bash
    systemctl --user enable --now podman.socket
    export WHALESHELL_DRIVER=podman
    whaleshell status
    ```

`whaleshell status` должен показать выбранный драйвер (`docker` или `podman`).

## Запустите gateway

Gateway хранит секреты и позволяет подключать провайдеров через `--provider`.

=== "Быстро"

    ```bash
    whaleshell gateway ensure
    whaleshell gateway info
    ```

=== "Docker Compose"

    ```bash
    # опционально постоянный ключ хранилища секретов:
    # export WHALESHELL_SECRETS_KEK="$(openssl rand -base64 32)"

    docker compose -f packaging/compose/docker-compose.yml up -d --build
    whaleshell gateway add http://127.0.0.1:7443 --local --name local
    whaleshell gateway select local
    whaleshell gateway info
    ```

=== "Локальный бинарь"

    ```bash
    go build -C whaleshell-gateway -o whaleshell-gateway ./cmd/whaleshell-gateway
    ./whaleshell-gateway --listen 127.0.0.1:7443 &

    whaleshell gateway add http://127.0.0.1:7443 --local --name local
    whaleshell gateway select local
    whaleshell gateway info
    ```

## Возьмите образ песочницы

```bash
docker pull ghcr.io/whaleshell/whaleshell/sandboxes/base:latest
```

Сборка из hub: `task runtime:image:cli` (base) или `task docker:agent:cursor`
(агент Cursor). Все образы: [Образы](../reference/images.md).

## Создайте первую песочницу

Запускайте из папки проекта, с которым будет работать агент:

```bash
whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --memory 2g
```

| Флаг | Что делает |
|------|------------|
| `--name` | Имя песочницы; контейнер — `whaleshell-<name>` |
| `--workspace` | Папка хоста, монтируется в `/workspace` |
| `--policy` | YAML сетевой политики (всё запрещено + allowlist) |
| `--memory` | Лимит памяти; рекомендуется на Docker Desktop |

## Работайте внутри

```bash
whaleshell sandbox list
whaleshell sandbox exec demo -- uname -a
whaleshell sandbox connect demo
```

`connect` открывает интерактивный shell в песочнице; проект лежит в
`/workspace`.

## Дайте доступы (опционально)

Секреты хранятся в gateway и не попадают в песочницу:

```bash
GITHUB_TOKEN=… whaleshell provider create --name gh --type github --credential GITHUB_TOKEN

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --provider gh
```

Подробнее: [Credential-провайдеры](../guides/credentials.md) · [Cursor Agent](../guides/cursor.md).

## Логи, остановка, удаление

```bash
whaleshell logs demo --tail --source proxy
whaleshell sandbox stop demo
whaleshell sandbox delete demo
```

`delete` удаляет песочницу, её proxy sidecar, сеть и data volumes. Секреты
провайдеров остаются в gateway.

</div>

## Дальше

- [Политика](../guides/policy.md) — что заблокировано и как одобрить узкое правило
- [Провайдеры](../providers/index.md) — Docker и Podman: ресурсы, логи
- [Пересоздание sandbox](../guides/recreate-sandbox.md) — когда изменению нужен новый контейнер
