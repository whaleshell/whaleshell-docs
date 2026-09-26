<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Get started

From zero to an agent running in a sandbox. Run the commands in order; each
step ends with a check.

<div class="ws-steps" markdown>

## Install the CLI

=== "Release binary"

    ```bash
    curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh
    whaleshell version
    ```

    The binary goes to `~/.local/bin` — make sure it is on your `PATH`.
    Pin a version with `WHALESHELL_VERSION=v0.1.0-alpha.1`, or pick another
    directory with `WHALESHELL_INSTALL_DIR=/usr/local/bin`.

=== "From source"

    ```bash
    cd /path/to/whaleshell
    export GOWORK=$PWD/go.work

    go build -C whaleshell-cli -o whaleshell ./cmd/whaleshell
    ./whaleshell install
    whaleshell version
    ```

## Start a container engine

whaleshell needs a running compute provider. Docker is the default.

=== "Docker"

    Docker Engine 24+ or Docker Desktop. On macOS and Windows prefer the
    **Docker VMM** backend.

    ```bash
    docker info
    whaleshell doctor
    whaleshell status
    ```

=== "Podman on macOS"

    ```bash
    podman machine init     # once
    podman machine start
    export WHALESHELL_DRIVER=podman
    whaleshell status
    ```

=== "Podman on Linux"

    ```bash
    systemctl --user enable --now podman.socket
    export WHALESHELL_DRIVER=podman
    whaleshell status
    ```

`whaleshell status` should print the driver you picked (`docker` or `podman`).

## Start the gateway

The gateway stores secrets and lets you attach providers with `--provider`.

=== "Quick"

    ```bash
    whaleshell gateway ensure
    whaleshell gateway info
    ```

=== "Docker Compose"

    ```bash
    # optional durable key for the secrets store:
    # export WHALESHELL_SECRETS_KEK="$(openssl rand -base64 32)"

    docker compose -f packaging/compose/docker-compose.yml up -d --build
    whaleshell gateway add http://127.0.0.1:7443 --local --name local
    whaleshell gateway select local
    whaleshell gateway info
    ```

=== "Local binary"

    ```bash
    go build -C whaleshell-gateway -o whaleshell-gateway ./cmd/whaleshell-gateway
    ./whaleshell-gateway --listen 127.0.0.1:7443 &

    whaleshell gateway add http://127.0.0.1:7443 --local --name local
    whaleshell gateway select local
    whaleshell gateway info
    ```

## Get a sandbox image

```bash
docker pull ghcr.io/whaleshell/whaleshell/sandboxes/base:latest
```

Building from the hub instead: `task runtime:image:cli` (base) or
`task docker:agent:cursor` (Cursor agent). All images: [Images](../reference/images.md).

## Create your first sandbox

Run this from the project folder you want the agent to work on:

```bash
whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --memory 2g
```

| Flag | What it does |
|------|--------------|
| `--name` | Sandbox name; the container is `whaleshell-<name>` |
| `--workspace` | Host folder mounted at `/workspace` |
| `--policy` | Network policy YAML (default-deny + allowlist) |
| `--memory` | Memory cap; recommended on Docker Desktop |

## Work inside

```bash
whaleshell sandbox list
whaleshell sandbox exec demo -- uname -a
whaleshell sandbox connect demo
```

`connect` opens an interactive shell inside the sandbox; your project is in
`/workspace`.

## Give it credentials (optional)

Secrets live in the gateway and never enter the sandbox:

```bash
GITHUB_TOKEN=… whaleshell provider create --name gh --type github --credential GITHUB_TOKEN

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --provider gh
```

More: [Credential providers](../guides/credentials.md) · [Cursor agent](../guides/cursor.md).

## Watch, stop, clean up

```bash
whaleshell logs demo --tail --source proxy
whaleshell sandbox stop demo
whaleshell sandbox delete demo
```

`delete` removes the sandbox, its proxy sidecar, network and data volumes.
Provider secrets stay in the gateway.

</div>

## Next

- [Policy](../guides/policy.md) — see what is blocked and approve narrow rules
- [Providers](../providers/index.md) — Docker and Podman details, resources, logging
- [Recreate a sandbox](../guides/recreate-sandbox.md) — when a change needs a fresh container
