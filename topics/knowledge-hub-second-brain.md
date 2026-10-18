# Knowledge Hub / Second Brain

This file documents the design of the repository you're reading right now — recursive on purpose. If someone asks "how does this thing actually work," this is the answer.

## What it is
A centralized store of **insights**, not just data — the conclusions people have already drawn, not only the raw numbers behind them. Most orgs centralize the data warehouse and leave the insight layer scattered across docs, decks, and memory.

## Scope: finished findings only
This repo holds validated, reviewed conclusions. It does not hold raw signal, half-formed hypotheses, or "noticed something odd, not sure yet." That belongs in a separate, looser working space — a personal or team-level second brain — not here. Mixing the two is how trust in a knowledge base erodes.

## Why GitHub, not Google Drive
- **Diff and history are the review mechanism** — a pull request *is* the governance workflow; Drive has comments and version history, not an approval gate.
- **Markdown is what an AI context window wants** — a flat, well-structured `.md` file is far more reliably parsed than a Drive doc's formatting or a loose folder hierarchy.
- **Grep-ability and structure** — a flat topic layer (see the root README) is natively walkable by both humans and agents.
- **Portability** — "plug and play into other teams' local Claude environments" means pointing a context reference at a URL or a cloned path. A Drive folder needs per-environment connector setup; a GitHub repo doesn't.
- **Honest trade-off**: GitHub has a steeper floor for a non-technical contributor who's never used Git. Solve it with a thin contribution layer (a form, or a Claude-guided prompt that commits the Markdown on their behalf) rather than pretending the friction doesn't exist.

## Governance: how trust is maintained at scale
Every finding passes through an assigned reviewer before it enters the repo — no self-certification. This isn't a new process; it's the review discipline product analytics should already run on individual findings, extended to be the gate for anything that becomes shared organizational memory.

## How we assure everybody has the same knowledge
Not a one-time import. Every team's local Claude environment carries a standing instruction to treat this repo as a live reference — check it before answering a product or customer question, the same way it would check a tracking plan. Freshness matters more than completeness: a small, current, trusted hub beats a large one nobody re-checks.
