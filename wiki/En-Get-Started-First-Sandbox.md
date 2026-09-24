<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# First sandbox

Requires a running [compute provider](En-Providers-Overview) and usually a selected
gateway ([Install](En-Get-Started-Install)).

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

See [Credential providers](En-Guides-Credentials) and [Cursor agent](En-Guides-Cursor).

## Observe

```bash
whaleshell logs demo --tail --source proxy
whaleshell term
```

## Next

- [Docker provider](En-Providers-Docker-Overview) — resources, logging, Desktop hygiene
- [Podman provider](En-Providers-Podman-Overview) — rootless / Machine
- [Recreate a sandbox](En-Guides-Recreate-Sandbox) — after policy changes
- [Policy](En-Guides-Policy) — denials and rule approve
