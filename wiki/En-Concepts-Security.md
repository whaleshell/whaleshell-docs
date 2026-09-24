<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Security

| Boundary | Trust |
|----------|-------|
| Host Engine / Desktop | Trusted operator machine |
| Sandbox container | Untrusted agent |
| Egress proxy | Trusted sidecar |
| Gateway secrets store | Trusted control plane |
| noVNC / display | Operator loopback only |

## Defaults

- No `docker.sock` inside the sandbox
- Workspace bind with deny-list for `$HOME`, `~/.ssh`, `~/.aws`, `~/.cursor`
- Default-deny network; allowlist from policy + composed providers
- Secrets as `whaleshell:resolve:env:…` rewritten on egress only
- Docker default seccomp kept; `no-new-privileges`; `CapDrop=NET_RAW`
- Landlock via `whaleshell-init` when kernel ABI ≥ 1 (often ABI 0 on Desktop)

## Credentials

Prefer `provider create` over `--env`. Cursor uses `agent login` instead of
injecting `CURSOR_API_KEY`. See [Credentials](En-Guides-Credentials).

## Resource hygiene

Uncapped guests and unbounded container logs inflate Docker Desktop VMs. Use
`--memory`, soft defaults, and default json-file rotation:

- [Docker resources](En-Providers-Docker-Resources)
- [Docker logging](En-Providers-Docker-Logging)

Full model: [SECURITY.md](../../../docs/SECURITY.md).
