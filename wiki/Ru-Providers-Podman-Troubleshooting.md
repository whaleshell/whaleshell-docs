<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Устранение неполадок (Podman)

| Симптом | Действие |
|---------|----------|
| `no API socket found` | `systemctl --user enable --now podman.socket`; задайте `WHALESHELL_PODMAN_SOCKET` |
| macOS не коннектится | `podman machine start`; проверьте sock под `~/.local/share/containers/podman/` |
| Драйвер всё ещё docker | `export WHALESHELL_DRIVER=podman` в том же shell, что CLI |
| Сеть sidecar сломана | Тест без proxy; netavark/CNI; см. [ограничения](Ru-Providers-Podman-Limitations) |
| Образа нет | Образ должен быть в store Podman (`podman images`), не только в Docker |

```bash
export WHALESHELL_DRIVER=podman
podman info
whaleshell status
whaleshell doctor
```
