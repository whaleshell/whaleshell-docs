<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Install

## Release binary

```bash
curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh
whaleshell version
```

| Goal | Command |
|------|---------|
| Latest release | `curl … \| sh` |
| Pin version | `WHALESHELL_VERSION=v0.1.0-alpha.1 sh` |
| Nightly | `WHALESHELL_VERSION=nightly sh` |
| Custom dir | `WHALESHELL_INSTALL_DIR=/usr/local/bin sh` |

The installer places the binary under `~/.local/bin` by default. Ensure that
directory is on `PATH`.

`whaleshell install` (when you already have a binary) only copies or symlinks
into `~/.local/bin`. It does not download releases.

## From source (hub workspace)

```bash
cd /path/to/whaleshell
export GOWORK=$PWD/go.work

go build -C whaleshell-cli -o whaleshell ./cmd/whaleshell
./whaleshell install
whaleshell version
```

## Container engine

Install and start one compute provider before create:

| Provider | Docs |
|----------|------|
| Docker (default) | [Prerequisites](En-Providers-Docker-Prerequisites) |
| Podman | [Prerequisites](En-Providers-Podman-Prerequisites) |

```bash
whaleshell doctor
whaleshell status
```

## Gateway

Proxy, encrypted secrets, and `--provider` attach need a reachable gateway.

### Local binary

```bash
go build -C whaleshell-gateway -o whaleshell-gateway ./cmd/whaleshell-gateway
./whaleshell-gateway --listen 127.0.0.1:7443 &

whaleshell gateway add http://127.0.0.1:7443 --local --name local
whaleshell gateway select local
whaleshell gateway info
```

`whaleshell gateway ensure` starts a local gateway when none is selected.

### Docker Compose

```bash
# optional durable KEK:
# export WHALESHELL_SECRETS_KEK="$(openssl rand -base64 32)"

docker compose -f packaging/compose/docker-compose.yml up -d --build
whaleshell gateway add http://127.0.0.1:7443 --local --name local
whaleshell gateway select local
```

OIDC (Dex): `packaging/compose/docker-compose.oidc.yml`, then
`whaleshell gateway login`.

KEK and store layout: [Credentials guide](En-Guides-Credentials).

## Images

```bash
task runtime:image:cli             # whaleshell-sandbox:local
task docker:agent:cursor           # optional agent flavor
# or: docker pull ghcr.io/whaleshell/whaleshell/sandboxes/base:latest
```

Catalog: [Images reference](En-Reference-Images).

## Checklist

| Check | Command |
|-------|---------|
| CLI | `whaleshell version` |
| Engine | `whaleshell doctor` |
| Driver | `whaleshell status` |
| Gateway | `whaleshell gateway info` |

Next: [First sandbox](En-Get-Started-First-Sandbox).
