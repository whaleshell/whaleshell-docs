<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Docker provider

Docker is the default compute provider. whaleshell talks to the local Engine
API (`DOCKER_HOST` / Desktop socket), creates an internal network per sandbox,
starts an egress proxy sidecar, then starts the sandbox container.

## Pages

| Page | Topic |
|------|-------|
| [Prerequisites](En-Providers-Docker-Prerequisites) | Engine, Desktop VMM, images |
| [Create a sandbox](En-Providers-Docker-Create-Sandbox) | `sandbox create` / connect / delete |
| [Resources and limits](En-Providers-Docker-Resources) | CPU, memory, PIDs, soft defaults |
| [Logging](En-Providers-Docker-Logging) | Container log rotation, gateway rings |
| [Troubleshooting](En-Providers-Docker-Troubleshooting) | Common failures |

## Layout (one sandbox)

```text
host Docker Engine
├── whaleshell-<name>              sandbox (agent image)
├── whaleshell-proxy-<name>        egress sidecar (slim base)
├── whaleshell-net-<name>          internal network
├── whaleshell-data-<name>         optional data volume
└── whaleshell-ca-<name>           MITM CA volume (when proxy enabled)
```

## Activate

```bash
unset WHALESHELL_DRIVER          # or: export WHALESHELL_DRIVER=docker
whaleshell doctor
whaleshell status
```

Expect `driver: docker` in status output.
