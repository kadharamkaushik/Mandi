---
id: MND-009
title: "Keep the Graphify knowledge graph current"
epic: PLAT
prd: F10
status: todo
owner: agent
size: S
depends_on: []
---

# MND-009 — Keep the Graphify knowledge graph current

**Why:** Graphify builds a knowledge graph of this repo so agents navigate by structure instead of grepping. It is installed at the repo root; the graph must stay fresh as code lands.

Epic `PLAT` · PRD F10 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- Nothing; can start now.

## Read first

- [AGENTS.md#5-graphify](../../AGENTS.md#5-graphify)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] A code-only starter graph (36 nodes) is already in graphify-out/. Build the full graph (code + docs, needs an LLM) with `/graphify .` from a Claude Code or Cowork session and commit graphify-out/ (except cache).
- [ ] Enable `graphify hook install` for post-commit rebuilds in developer clones; document it in AGENTS.md.
- [ ] CI job (weekly and on docs/ changes) that rebuilds the graph and opens a PR if it changed.

- [ ] packages/design-tokens/tokens.json is skipped as 'potentially sensitive' because of its name; add it via .graphifyignore rules or rename it, and update the iOS/Android generators accordingly.

## Acceptance criteria

- [ ] graphify-out/GRAPH_REPORT.md exists and lists docs, services and apps as communities.
- [ ] Agents' Grep/Glob calls show the Graphify PreToolUse reminder (from CLAUDE.md integration).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-009: Keep the Graphify knowledge graph current` with acceptance criteria ticked.
