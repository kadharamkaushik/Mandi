# Graph Report - Mandi  (2026-09-27)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 36 nodes · 36 edges · 6 communities (5 shown, 1 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Community 0
- Community 1
- Community 2
- Community 3
- Community 4
- Community 5

## God Nodes (most connected - your core abstractions)
1. `scripts` - 6 edges
2. `scripts` - 4 edges
3. `visit()` - 3 edges
4. `front_matter()` - 2 edges
5. `load()` - 2 edges
6. `ready()` - 2 edges
7. `render()` - 2 edges
8. `waves()` - 2 edges
9. `engines` - 2 edges
10. `openapi-typescript` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Communities (6 total, 1 thin omitted)

### Community 0 - "Community 0"
Cohesion: 0.22
Nodes (8): devDependencies, openapi-typescript, @stoplight/spectral-cli, name, private, version, openapi-typescript, @stoplight/spectral-cli

### Community 1 - "Community 1"
Cohesion: 0.28
Nodes (8): pathlib, re, sys, front_matter(), load(), Rebuild tasks/INDEX.md from task front matter and check the dependency graph.…, ready(), render()

### Community 2 - "Community 2"
Cohesion: 0.33
Nodes (5): engines, node, name, packageManager, private

### Community 3 - "Community 3"
Cohesion: 0.33
Nodes (6): scripts, build, contracts:gen, contracts:lint, lint, test

### Community 4 - "Community 4"
Cohesion: 0.50
Nodes (4): scripts, breaking, generate, lint

## Knowledge Gaps
- **19 isolated node(s):** `openapi-typescript`, `@stoplight/spectral-cli`, `name`, `private`, `version` (+14 more)
  These have ≤1 connection - possible missing edges. (Counts symbols only; 23 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `scripts` connect `Community 3` to `Community 2`?**
  _High betweenness centrality (0.067) - this node is a cross-community bridge._
- **Why does `scripts` connect `Community 4` to `Community 0`?**
  _High betweenness centrality (0.050) - this node is a cross-community bridge._
- **What connects `openapi-typescript`, `@stoplight/spectral-cli`, `name` to the rest of the system?**
  _19 weakly-connected nodes found - possible documentation gaps or missing edges._