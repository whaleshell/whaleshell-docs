<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# whaleshell documentation

Canonical, shared documentation for the [whaleshell](https://github.com/whaleshell)
multi-repo product. Not duplicated inside CLI, driver, or proxy repositories.

| Language | Home |
|----------|------|
| English | [en/Home.md](./en/Home.md) |
| Русский | [ru/Home.md](./ru/Home.md) |

## Tree

```text
.
├── en/                     English
│   ├── Home.md
│   ├── SUMMARY.md
│   ├── get-started/
│   ├── concepts/
│   ├── providers/          compute backends (priority)
│   │   ├── docker/         ★ default
│   │   └── podman/         ★ Engine API parity
│   ├── guides/
│   └── reference/
└── ru/                     Russian (mirror structure)
```

## Compute providers (priority)

| Provider | Status | Docs |
|----------|--------|------|
| **Docker** | Default | [en](./en/providers/docker/) · [ru](./ru/providers/docker/) |
| **Podman** | Supported (Engine API) | [en](./en/providers/podman/) · [ru](./ru/providers/podman/) |

## Local workspace

In the org hub checkout this repository as `whaleshell-docs/` next to the other
`whaleshell-*` modules. Product code repos do not vendor these pages.

## Style

- NVIDIA OpenShell–aligned: short sections, imperative voice, tables for facts.
- Dual language: keep `en/` and `ru/` paths in lockstep.
- Credential providers (`--provider github`, …) are documented under Guides —
  separate from compute providers (Docker / Podman).
