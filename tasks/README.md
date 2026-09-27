# Tasks

One markdown file per task under an epic folder (`plat`, `api`, `store`, `core`, `ios`, `and`, `qa`). Each file is self-contained so a Cowork session can pick it up cold: why it matters, what to read first, scope, acceptance criteria and definition of done.

## Front matter

```yaml
id: MND-031
title: "Basket optimiser package"
epic: CORE            # PLAT | API | STORE | CORE | IOS | AND | QA
prd: F4               # feature ids from docs/prd.md
status: todo          # todo | in-progress | in-review | done | blocked
owner: agent          # agent | human | human+agent
size: M               # S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks
depends_on: []        # task ids that must be done first
```

## Index

`python3 tasks/index.py` rebuilds [INDEX.md](INDEX.md) (waves, ready list, status counts); `--check` validates ids, statuses and the dependency graph and is meant for CI.

## Handing a task to Cowork

Start a Cowork session with the Mandi folder connected and say, for example:

> Read AGENTS.md, then do tasks/core/MND-031-basket-optimiser-package.md. Follow its acceptance criteria and definition of done.

Human-owned tasks (`owner: human`) are external actions such as account creation, store partnerships, contracts and legal review; agents should not attempt them.
