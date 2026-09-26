<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Providers

A **compute provider** is the engine that runs the sandbox and its egress
proxy. Pick one with `WHALESHELL_DRIVER` (default: `docker`) and check it with
`whaleshell status`.

<div class="grid cards" markdown>

-   :material-docker:{ .lg .middle } __Docker__ &nbsp; <span class="ws-badge ws-badge--ok">default</span>

    ---

    Docker Engine or Docker Desktop. Widest image and networking
    compatibility; every tutorial uses it.

    [:octicons-arrow-right-24: Docker](docker/index.md)

-   :simple-podman:{ .lg .middle } __Podman__ &nbsp; <span class="ws-badge ws-badge--ok">supported</span>

    ---

    Rootless on Linux or Podman Machine on macOS, through the
    Docker-compatible Engine API.

    [:octicons-arrow-right-24: Podman](podman/index.md)

-   :material-kubernetes:{ .lg .middle } __Kubernetes__ &nbsp; <span class="ws-badge ws-badge--soon">coming soon</span>

    ---

    Sandboxes as pods, gateway via Helm.

    [:octicons-arrow-right-24: Kubernetes](kubernetes.md)

-   :material-chip:{ .lg .middle } __MicroVM__ &nbsp; <span class="ws-badge ws-badge--soon">coming soon</span>

    ---

    A lightweight VM per sandbox for a stronger boundary, GPU passthrough.

    [:octicons-arrow-right-24: MicroVM](microvm.md)

</div>

| Provider | `WHALESHELL_DRIVER` | Status |
|----------|---------------------|--------|
| Docker | `docker` | Default, full support |
| Podman | `podman` | Supported via Engine API |
| Kubernetes | `kubernetes` | Coming soon |
| MicroVM | `vm` | Coming soon |

!!! tip "Not the same as credential providers"
    `--provider github`, `--provider cursor` and friends attach secrets and
    egress rules to a sandbox. They work with any compute provider — see
    [Credential providers](../guides/credentials.md).
