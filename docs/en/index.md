---
hide:
  - navigation
  - toc
---

<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

<div class="ws-hero" markdown>

# whaleshell

<p class="ws-hero__tagline">Policy-bound sandboxes for coding agents.<br>
Cursor, Claude, Codex — or anything you bring — on Docker or Podman.</p>

[Get started](get-started/index.md){ .md-button .md-button--primary }
[Docker provider](providers/docker/index.md){ .md-button }

</div>

## Quick start

```bash
curl -LsSf https://raw.githubusercontent.com/whaleshell/whaleshell-cli/main/install.sh | sh

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml

whaleshell sandbox connect demo
```

!!! note
    You need a working container engine (Docker or Podman) before creating a sandbox.

## Explore

<div class="grid cards" markdown>

-   :material-rocket-launch:{ .lg .middle } __Get started__

    ---

    Install the CLI, create your first sandbox, exec and connect.

    [:octicons-arrow-right-24: Install](get-started/install.md)

-   :material-docker:{ .lg .middle } __Compute providers__

    ---

    Docker is the default backend; Podman works through the Engine API.

    [:octicons-arrow-right-24: Providers](providers/index.md)

-   :material-shield-lock:{ .lg .middle } __Policy__

    ---

    Default-deny egress, L7 allowlists, `policy.local` proposals and approve.

    [:octicons-arrow-right-24: Policy guide](guides/policy.md)

-   :material-key-chain:{ .lg .middle } __Credentials__

    ---

    Store secrets once in the gateway and attach them with `--provider`.

    [:octicons-arrow-right-24: Credential providers](guides/credentials.md)

-   :material-sitemap:{ .lg .middle } __Concepts__

    ---

    Control, data and enforcement planes; how a create request flows.

    [:octicons-arrow-right-24: Architecture](concepts/architecture.md)

-   :material-console:{ .lg .middle } __Reference__

    ---

    CLI surface, sandbox images on GHCR, environment variables.

    [:octicons-arrow-right-24: Reference](reference/index.md)

</div>
