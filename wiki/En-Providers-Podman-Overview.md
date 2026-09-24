<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Podman provider

Podman is a first-class compute provider. whaleshell discovers a Podman API
socket and reuses the Docker Engine client path (`driver.OpenEngine("podman")`).
Sandbox labels, networks, proxy sidecar, and exec flows match Docker.

## Pages

| Page | Topic |
|------|-------|
| [Prerequisites](En-Providers-Podman-Prerequisites) | Socket, machine, rootless |
| [Create a sandbox](En-Providers-Podman-Create-Sandbox) | Switch driver and run create |
| [Limitations](En-Providers-Podman-Limitations) | Rootless networking, MVP gaps |
| [Troubleshooting](En-Providers-Podman-Troubleshooting) | Socket and netavark issues |

## Activate

```bash
export WHALESHELL_DRIVER=podman
# optional:
# export WHALESHELL_PODMAN_SOCKET=$XDG_RUNTIME_DIR/podman/podman.sock

whaleshell status    # driver: podman
```

Resource flags, log rotation, slim proxy image, and soft defaults behave the
same as on Docker — see [Docker resources](En-Providers-Docker-Resources) and
[Docker logging](En-Providers-Docker-Logging).
