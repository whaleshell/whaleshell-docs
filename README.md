<!--
SPDX-FileCopyrightText: Copyright (c) 2026 whaleshell
SPDX-License-Identifier: MIT
-->

# whaleshell documentation

Shared documentation for all whaleshell modules, built with
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) (EN / RU).

**Site:** https://whaleshell.github.io/

## Layout

```text
mkdocs.yml            theme, navigation, RU nav titles
docs/
├── en/               English (default, served at /)
├── ru/               Russian (same tree, served at /ru/)
└── assets/           shared CSS
```

Keep `docs/en/` and `docs/ru/` in lockstep: same file names, same paths.
New pages also need an entry in `nav` in `mkdocs.yml` (and a RU title in
`nav_translations` if the label is new).

## Local preview

```bash
python3 -m venv .venv && . .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Pushes to `main` build with `mkdocs build --strict` and deploy to GitHub Pages.
