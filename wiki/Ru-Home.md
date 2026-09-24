<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# Документация whaleshell

whaleshell запускает coding-агентов в контейнерах с политикой. **Провайдер
вычислений** (Docker или Podman) поднимает sandbox и egress-sidecar; опциональный
gateway хранит секреты и собирает профили credential-провайдеров.

> Перед созданием sandbox нужен работающий контейнерный движок.

## Languages

- [English](En-Home)
- Русский (эта страница)

## С чего начать

1. [Установка](Ru-Get-Started-Install)
2. [Первый sandbox](Ru-Get-Started-First-Sandbox)
3. Выберите провайдер вычислений:
   - [Docker](Ru-Providers-Docker-Overview) (по умолчанию)
   - [Podman](Ru-Providers-Podman-Overview)

## Разделы

| Раздел | Содержание |
|--------|------------|
| [Быстрый старт](Ru-Get-Started-Overview) | CLI, gateway, первый create |
| [Концепции](Ru-Concepts-Overview) | Архитектура, модель безопасности |
| [Провайдеры](Ru-Providers-Overview) | Docker, Podman (compute) |
| [Руководства](Ru-Guides-Overview) | Credentials, gateway, policy, Cursor |
| [Справка](Ru-Reference-Overview) | CLI, образы, переменные окружения |

Полное оглавление: [SUMMARY.md](Ru-SUMMARY).

## Связанное

Обзор hub: [../../README.md](../../README.md) · Модули: [../MODULES.md](../MODULES.md)
