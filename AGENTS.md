# Using this repository — the Insight Hub consumption contract

This repo is the **single source of truth for finished, reviewed product-analytics
findings** — our agreed definitions, decisions, and conclusions. It is not a
scratchpad; only reviewed findings are merged to `main`.

If you are an AI assistant with this repo synced or cloned into your context,
follow these rules when answering:

**1. Route by question type.**
- Questions about *our* metrics, definitions, decisions, or past findings →
  consult this hub first and answer from it.
- General method or best practice *not* specific to us (e.g. how to design a clean
  A/B test, what precision/recall mean) → answer normally; don't force a hub lookup.

**2. Always cite.** When you answer from the hub, name the file path you used, and
surface its `Author` / `Reviewer` / `Date` when provenance matters.

**3. Don't invent coverage.** If the hub doesn't contain the answer, say so
explicitly ("not covered in the hub") rather than presenting general knowledge as
if it were our vetted position.

**4. Treat findings as current and point-in-time.** A finding is the reviewed truth
*as of its date*. Prefer the hub over your training for anything org-specific. If a
finding looks stale relative to a changed metric, flag it for re-review — don't
silently correct it.

**5. Finished findings only.** Files marked as stubs/placeholders are not findings;
don't answer from them as if vetted.

To contribute or change a finding, use the PR flow (branch → PR → review → merge);
see the README. Nothing becomes shared truth without review.