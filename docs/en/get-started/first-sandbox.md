<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# First sandbox

Requires a running [compute provider](../providers/index.md) and usually a selected
gateway ([Install](./install.md)).

## Create

```bash
whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --memory 2g
```

| Flag | Role |
|------|------|
| `--name` | Sandbox id (`whaleshell-<name>` container) |
| `--workspace` | Host path bind-mounted at `/workspace` |
| `--policy` | Base policy YAML |
| `--memory` | Soft recommendation on Desktop; optional |

Image defaults to the local base sandbox unless `--from` / `--image` is set.

## Exec and connect

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

Delete removes the sandbox container, proxy sidecar, network, and labeled data
volumes. Gateway provider secrets remain until you delete the provider or wipe
gateway data.

## With credentials

```bash
GITHUB_TOKEN=… whaleshell provider create --name gh --type github --credential GITHUB_TOKEN

whaleshell sandbox create \
  --name demo \
  --workspace "$PWD" \
  --policy whaleshell-cli/policies/default.yaml \
  --provider gh \
  --memory 2g
```

See [Credential providers](../guides/credentials.md) and [Cursor agent](../guides/cursor.md).

## Observe

```bash
whaleshell logs demo --tail --source proxy
whaleshell term
```

## Next

- [Docker provider](../providers/docker/index.md) — resources, logging, Desktop hygiene
- [Podman provider](../providers/podman/index.md) — rootless / Machine
- [Recreate a sandbox](../guides/recreate-sandbox.md) — after policy changes
- [Policy](../guides/policy.md) — denials and rule approve
