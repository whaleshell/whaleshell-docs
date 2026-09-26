<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Compute providers

A **compute provider** is the container backend that creates sandbox and proxy
containers. Select it with `WHALESHELL_DRIVER` (default: `docker`).

| Provider | `WHALESHELL_DRIVER` | Maturity |
|----------|---------------------|----------|
| [Docker](./docker/index.md) | `docker` | Default, full support |
| [Podman](./podman/index.md) | `podman` | Supported via Docker-compatible Engine API |
| Kubernetes | `kubernetes` | Experimental |
| MicroVM | `vm` | Experimental |

Credential providers (`--provider github`, `--provider cursor`, …) are separate:
they attach secrets and egress rules. See [Credential providers](../guides/credentials.md).

## Choose Docker when

- You already run Docker Engine or Docker Desktop.
- You need the widest image and networking compatibility.
- You follow the main tutorials and compose packaging.

## Choose Podman when

- You prefer rootless containers on Linux.
- Policy requires a Docker-free host.
- You accept Engine-API parity (same labels, networks, sidecar layout) with
  known rootless networking caveats.

```bash
whaleshell status    # prints active driver
```
