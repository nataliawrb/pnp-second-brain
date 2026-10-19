# Scaling the hub: multiple repos, one contract

Forward-looking — not needed for a single repo. The moment a second hub appears
(a different team / access model / lifecycle owns it), use this so the *contracts*
don't drift even as the *content* spreads.

## Principle

**One consumption contract, many content repos.** The behavioral rules (cite,
don't invent, finished-findings-only) are defined **once** in a shared location;
every content repo's `AGENTS.md` is a **thin pointer** to it plus only what's local
to that repo (what it owns, its folder map). Same SSOT move as `CLAUDE.md →
AGENTS.md`, lifted one level up.

```
org-standards/                      ← canonical consumption contract (ONE place)
  AGENTS.md  ───────────────┐
                            │  every content repo points here
   ┌───────────────┬────────┴───────┬──────────────────┐
 pnp-second-brain/   metrics-hub/     tracking-plan/     …
   AGENTS.md*         AGENTS.md*        AGENTS.md*
   topics/…           definitions/…     plans/…
   * thin: "follow org-standards/AGENTS.md" + what THIS repo owns + its folder map
```

## 1. The canonical contract (`org-standards/AGENTS.md`)

```
# Insight Hub — consumption contract (canonical)
Applies to every repo that points here.

1. Route by question type: our metrics / definitions / decisions / findings →
   consult the hubs; general method/best-practice → answer normally.
2. Cite — MANDATORY. End any hub-sourced answer with a line:
   Source: <repo>/<path>   e.g. Source: pnp-second-brain/topics/why-github-not-drive.md
3. Don't invent coverage — if the hubs don't cover it, say "not covered".
4. Findings are point-in-time reviewed truth — flag staleness for re-review,
   don't silently correct.
5. Finished findings only — ignore stubs.
6. Precedence: a repo's local AGENTS.md may ADD domain specifics; it may NOT
   weaken rules 2–5. More-specific extends, never overrides, the baseline.
7. Before answering, use the routing map to pick the right repo.
```

## 2. The thin per-repo header (each repo's `AGENTS.md`)

```
# <repo-name> — local hub header
This repo follows the canonical contract: org-standards/AGENTS.md. Read it first.

Owns: <one line — e.g. "validated product-analytics findings">
Folder map:
  topics/…  finished findings by cluster
  assets/…  frozen chart snapshots
  src/…     the SQL/py that regenerates them
Cite files here as:  Source: <repo-name>/<path>
```

## 3. The routing map (which repo owns what)

Lives in the canonical contract and is echoed in each consumer's activator
(Project instructions / skill). Without it, the model doesn't know which hub to open.

```
| Question is about…                         | Repo             |
|--------------------------------------------|------------------|
| Product-analytics findings & conclusions    | pnp-second-brain |
| Metric & dimension definitions (semantic)   | metrics-hub      |
| Event tracking plan / naming conventions    | tracking-plan    |
```

## 4. Citation format, now repo-qualified

A path alone is ambiguous across repos, so citations carry the repo:

```
Source: <repo>/<path>
e.g. Source: pnp-second-brain/topics/why-github-not-drive.md
```

## 5. Consumer activation (unchanged shape, just points at the shared contract)

The synced files are *data*; the binding still comes from the consumer's own layer:
- **Claude Code** → `CLAUDE.md` points to the repo's `AGENTS.md`, which points to the canonical contract.
- **Project** → one scoped bullet: "For our metrics/definitions/findings, consult
  the synced hubs per their `AGENTS.md`, use the routing map, and cite
  `Source: <repo>/<path>`."
- **Skill** → one installable "insight-hub" skill carries the same, for portability.

## The discipline that stops sprawl

Split repos by **owner / access / lifecycle — not by topic.** Topics are *folders
inside a repo*; a new repo is a new governance + access + maintenance boundary. Add
one when a different team owns it or it needs different access — not just because
it's a new subject. One well-structured hub beats five thin ones.

---

**Interview line:** "One contract, many scoped content repos. Each repo's
`AGENTS.md` points to a single canonical rulebook and adds only its own domain and
folder map; a routing map says which repo owns what; citations are repo-qualified;
and the baseline rules can be extended locally but never weakened. Repos split on
ownership and access, not topic — so it scales across teams without the governance
fragmenting."