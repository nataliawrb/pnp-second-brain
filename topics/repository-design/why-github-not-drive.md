# Single source of truth: why Git, not Google Drive

**Author:** Natalia Wierzbowska · **Date:** 2026-10-19
**Status:** Living rationale · **Reviewer:** — *(unreviewed, per the hub's own rule)*

---

## The outlook

Across every org I've built product analytics in — HelloFresh, Flink, Hotjar, IU —
the same failure repeats: insight lives in one analyst's head, one Slack thread,
one dashboard nobody else can parse. When that person is out, the org re-derives
it or acts on a stale version.

My job is to make insights **correct, reliable, timely, and accessible.** The hub
is the mechanism. It has to hold three things most tools make you pick two of:

- **Reliable** — trustworthy without re-checking.
- **Gated** — nothing becomes shared truth without review.
- **Distributed** — reaches people where they already work.

## Why Git, not Drive

Two non-reasons to drop from the pitch: Drive also stores Markdown, and Drive also
has version history. What actually separates them:

| Dimension | Google Drive | Git / GitHub |
|---|---|---|
| Review / approval | Comments — a *convention* anyone can bypass | **Enforced gate**: branch protection, nothing reaches `main` without reviewer approval |
| History | Per-file, opaque | Atomic commits, line-level diffs, a message saying **why** |
| Attribution | "Last edited by" | Author + reviewer + timestamp are structural; `git blame` answers "who vetted this, when" |
| Access / automation | Needs a connector per environment; weak triggers | Clone/raw-URL anywhere; a git event per merge triggers any downstream |

The three benefits that survive scrutiny:

1. **Governance lives in the tool, not in people's discipline.** The gate is
   mechanical (branch protection), not a folder convention you hope nobody
   bypasses — and one direct edit to a canonical file kills trust org-wide.
2. **Portable access** — a URL plugs into any workflow or assistant. (Drive *is*
   AI-readable; the edge is frictionless, uniform access.)
3. **Lives next to the metric definitions** (tracking plans, dbt/SQLMesh), so
   "re-review when the metric changes" can be automated, not hoped for.

**The crux:** the real question is *where governance lives — in the tool or in
people's heads.* For trust at scale, it has to be structural, because
discipline-based gates collapse when the org gets busy. The tell that this was
reasoned, not cargo-culted: for a **single-author** base (a personal second
brain), Drive is the right call — no gate to enforce, less friction. Git wins
*here* only because of the multi-contributor + governance requirement.

## The architecture

```
Author → PR → review gate → merge to main   ← the ONLY write path, the source of truth
                                  │
             CI / webhook fans out on every merge
   ┌──────────────┬──────────────┬──────────────┬─────────────┐
 Internal wiki  Confluence     Notion         Slack          Any LLM / RAG
 (GitHub Pages)  mirror         mirror        notify+ask      index (not just Claude)
   └────────────── all READ-ONLY projections of vetted content ───────────┘
```

One write path, many read paths. The gate sits in one place; every surface
downstream inherits its trust by being a read-only mirror.

## Storing analytics results: finding vs. evidence vs. method

A chart is **evidence**, not the finding. Three things get separated:

- **Finding** → Markdown: the conclusion in words + numbers ("X → +12% 30-day
  retention, n=…, caveat Y"). If it can't be stated as text, it isn't finished.
- **Evidence (chart)** → a committed image *file* referenced from the `.md`
  (prefer **SVG** — text-based, scales, diffs a little; PNG only when
  raster-heavy). Not pasted as Markdown.
- **Method** → the SQL / `.py` that regenerates it, versioned next to the finding
  and linked from the `.md`. (Avoid raw `.ipynb` as canonical — it diffs badly;
  keep a `.py` or an exported `.md`/`.html`.)

```
topics/experimentation-and-performance-measurement/
  revenue-wrong-primary-metric.md   # finding: conclusion + caveat + embeds
  assets/revenue-vs-proxy.svg        # frozen, reviewed snapshot
  src/revenue-vs-proxy.sql           # the query
  src/revenue-vs-proxy.py            # regenerates the SVG
```

**Frozen vs. live** — the key line: a finding is a *point-in-time reviewed
conclusion*, so its chart is a **frozen snapshot** committed alongside it; it must
not silently change after review. If the underlying metric moves, that triggers a
**re-review** (a new version), not a live update. Interactive, always-current
charts stay in the BI tool (Amplitude / Omni / Looker); the finding **links** to
them, never embeds them as the finding.

**Rendering in Confluence / Notion — project, don't recreate:**
1. **Frozen snapshot** — the one-way sync carries the `.md` + its SVG/PNG and
   renders them read-only, so the page always matches what was reviewed. (Default.)
2. **Live view** — embed the BI tool via an iframe/macro at its URL, clearly
   labeled "live," beside the frozen finding — never masquerading as it.

*(Optional: CI can regenerate the SVG from the `.py` on demand, but that needs
warehouse credentials in CI — overkill for most hubs. The bar is: a human can
rerun the method.)*

## Distribution — reaching people who don't live in Git (or Claude)

Nobody has to open GitHub. Authors/reviewers work there; everyone else reads it
where they already are:

- **Internal wiki** (GitHub Pages / MkDocs) — auto-published on merge, searchable;
  readers never see Git. Removes the non-technical barrier.
- **Confluence / Notion mirror** — CI upserts pages on merge, **one-way and
  read-only** ("edit in the repo"). An editable mirror = two truths again.
- **Slack** — merge posts a new-finding alert; optional bot answers from the repo.
  Announce + ask, never store.
- **Any LLM / RAG** — plain Markdown at stable URLs ingests into Claude, Glean,
  Notion AI, Copilot, whatever runs next year. The hub is vendor-agnostic; it
  doesn't depend on being a Claude shop.

## Costs and barriers

- **Contributor floor** (a PM who's never used Git) — the real cost. Mitigated by
  in-browser edit+PR, a Claude-guided flow that writes the file and opens the PR,
  and Markdown preview. The floor hits *contributors*, not readers.
- **Access control** — private repo + SSO if findings touch sensitive metrics.
- **Maintenance** — each sync is real engineering; don't ship all at once, and
  keep every spoke strictly one-way/read-only (bidirectional sync drifts).

## MVP sequencing

1. Repo + branch protection + the worked findings (the governed core).
2. Slack merge-notification (cheapest reach).
3. GitHub Pages / MkDocs wiki (removes the non-technical barrier).
4. Confluence / Notion mirror — only if the org lives there.
5. Broader RAG indexing once the content base is worth retrieving.
