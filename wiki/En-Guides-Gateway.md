<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Gateway

The gateway is the optional control plane: encrypted credential store, sandbox
registry, observation log rings, and policy proposal workflow.

## Run

```bash
whaleshell gateway ensure
whaleshell gateway add http://127.0.0.1:7443 --local --name local
whaleshell gateway select local
whaleshell gateway info
```

Compose: `packaging/compose/docker-compose.yml`.

Listen address defaults to `127.0.0.1:7443`.

## Responsibilities

| Surface | Role |
|---------|------|
| Secrets | AES-GCM store; KEK via `WHALESHELL_SECRETS_KEK` or `secrets.kek` |
| Providers | Named instances + profile composition metadata |
| Sandboxes | Registry upsert/delete; log ring; proposals |
| Sidecar | Resolves secrets over `host.whaleshell.internal` |

## When required

| Operation | Gateway |
|-----------|---------|
| `--provider` attach | Required |
| Egress proxy + rewrite | Required |
| Plain create `--no-proxy` without providers | Optional (dev) |

## Config

Gateways are recorded in `~/.config/whaleshell/config.yaml`:

```yaml
current: local
gateways:
  local:
    url: http://127.0.0.1:7443
```

OIDC fields and tokens may appear for authenticated gateways after
`whaleshell gateway login`.

## Related

- [Credentials](En-Guides-Credentials)
- [Policy](En-Guides-Policy)
- Hub packaging: `packaging/compose/`
