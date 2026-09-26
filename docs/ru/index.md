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

<p class="ws-hero__tagline">Песочницы с политикой для coding-агентов.<br>
Cursor, Claude, Codex — или любой свой агент — на Docker или Podman.</p>

[Начать](get-started/index.md){ .md-button .md-button--primary }
[Провайдеры](providers/index.md){ .md-button }

</div>

## Зачем

Coding-агенты запускают команды, ставят пакеты и ходят в API за вас. Если
запускать их прямо на машине, им доступны весь домашний каталог, SSH-ключи,
облачные доступы и открытый интернет. Одного неудачного промпта или
заражённого пакета хватит, чтобы что-то утекло или сломалось.

whaleshell запускает агента в контейнере, который видит **только ваш проект**
и может ходить **только на разрешённые хосты**. Секреты остаются снаружи.

<div class="grid cards" markdown>

-   :material-folder-lock:{ .lg .middle } __Только проект__

    ---

    Папка монтируется в `/workspace`. Внутри нет `docker.sock`, `~/.ssh`
    и `~/.aws`.

-   :material-wall-fire:{ .lg .middle } __Сеть закрыта по умолчанию__

    ---

    Наружу уходит только то, что разрешает политика: хост, а для HTTPS —
    ещё метод и путь.

-   :material-key-chain:{ .lg .middle } __Секреты снаружи__

    ---

    Агент видит заглушки. Настоящие токены подставляет прокси — и только в
    разрешённые запросы.

-   :material-sync:{ .lg .middle } __Политика на лету__

    ---

    Агент предлагает узкое правило, вы одобряете, прокси перечитывает его
    примерно за секунду — без пересборки.

-   :material-robot-outline:{ .lg .middle } __Любой агент__

    ---

    Готовые образы для Cursor, Claude и Codex или свой контейнер.

-   :material-docker:{ .lg .middle } __Docker или Podman__

    ---

    Одинаковая схема на обоих движках; Kubernetes и MicroVM — в работе.

</div>

## Как это работает

```mermaid
sequenceDiagram
    autonumber
    actor You as Вы
    participant S as Песочница (агент)
    participant P as Egress-прокси
    participant U as Интернет
    You->>S: whaleshell sandbox create
    S->>P: HTTPS-запрос с заглушкой секрета
    P->>P: Проверка хоста, метода и пути по политике
    alt разрешено
        P->>U: Запрос с настоящим секретом
        U-->>S: Ответ
    else заблокировано
        P-->>S: 403 + причина
        S->>You: Предложение узкого правила
        You->>P: whaleshell rule approve
    end
```

1. **Создание.** `whaleshell sandbox create` поднимает два контейнера в
   приватной сети: песочницу с агентом и вашим проектом и рядом egress-прокси.
2. **Все запросы идут через прокси.** Другого выхода у песочницы нет, поэтому
   весь трафик проверяется по вашей политике.
3. **Секреты подставляются на выходе.** У агента только заглушки вида
   `whaleshell:resolve:env:GITHUB_TOKEN`; настоящий токен прокси вставляет в
   запросы, которые разрешает политика.
4. **Блокировка с объяснением.** Запрещённый запрос получает 403 с причиной,
   и агент может попросить ровно тот доступ, который нужен.
5. **Решаете вы.** Одобрите или отклоните предложение; новая политика
   начинает действовать примерно через секунду, песочницу пересоздавать не надо.

Подробнее: [Архитектура](concepts/architecture.md) · [Безопасность](concepts/security.md).

## Разделы

<div class="grid cards" markdown>

-   :material-rocket-launch:{ .lg .middle } __Быстрый старт__

    ---

    Установка, движок, gateway и первая песочница — по шагам.

    [:octicons-arrow-right-24: Начать](get-started/index.md)

-   :material-server-network:{ .lg .middle } __Провайдеры__

    ---

    Сейчас Docker и Podman; Kubernetes и MicroVM — скоро.

    [:octicons-arrow-right-24: Провайдеры](providers/index.md)

-   :material-shield-lock:{ .lg .middle } __Политика__

    ---

    Allowlist, L7-правила, предложения и одобрение.

    [:octicons-arrow-right-24: Политика](guides/policy.md)

</div>
