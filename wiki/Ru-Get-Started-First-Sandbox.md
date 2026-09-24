<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Первый sandbox

Нужен работающий [провайдер вычислений](Ru-Providers-Overview) и обычно выбранный
gateway ([Установка](Ru-Get-Started-Install)).

## Create

```bash
whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --memory 2g
```

| Флаг | Роль |
|------|------|
| `--name` | Id sandbox (контейнер `whaleshell-<name>`) |
| `--workspace` | Каталог хоста → `/workspace` |
| `--policy` | Базовый YAML политики |
| `--memory` | Рекомендуется на Desktop; опционально |

Без `--from` / `--image` берётся локальный base-образ sandbox.

## Exec и connect

```bash
whaleshell sandbox list
whaleshell sandbox status demo
whaleshell sandbox exec demo -- uname -a
whaleshell sandbox connect demo          # bash -il
```

## Stop, start, delete

```bash
whaleshell sandbox stop demo
whaleshell sandbox start demo
whaleshell sandbox delete demo
```

Delete удаляет sandbox, proxy sidecar, сеть и помеченные data volumes.
Секреты провайдеров в gateway остаются, пока не удалите provider или data
gateway.

## С credentials

```bash
GITHUB_TOKEN=… whaleshell provider create --name gh --type github --credential GITHUB_TOKEN

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --provider gh \
  --memory 2g
```

См. [Credential-провайдеры](Ru-Guides-Credentials) и [Cursor Agent](Ru-Guides-Cursor).

## Наблюдение

```bash
whaleshell logs demo --tail --source proxy
whaleshell term
```

## Далее

- [Docker](Ru-Providers-Docker-Overview) — ресурсы, логи, гигиена Desktop
- [Podman](Ru-Providers-Podman-Overview) — rootless / Machine
- [Пересоздание sandbox](Ru-Guides-Recreate-Sandbox) — после смены policy
- [Политика](Ru-Guides-Policy) — deny и rule approve
