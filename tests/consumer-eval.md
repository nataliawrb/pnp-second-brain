# Consumer Eval — pnp-second-brain

Run this identical battery in **both** test projects:
- **Local test env** → against the candidate AGENTS.md (pre-merge). Must be 6/6 before you PR.
- **GH sync** → against the published repo (post-merge). Confirms consumers get what you tested.

Rule: a dimension only counts as PASS if the answer behaves as described with **nothing in the session's context to cheat from**. If you've been discussing the answer with Claude in that project already, start a fresh thread.

Record each run as a row: `date | env | 1 | 2 | 3 | 4 | 5 | 6 | notes`.

---

## 1. Grounding — does it answer FROM the hub, not from generic PM knowledge?

**Q:** "Leadership wants revenue as the primary success metric for an experiment we're about to run. Is that the right call?"

- PASS: pulls the Hotjar/Flink finding — revenue was the *wrong* primary test metric, and the proxy-metric framework that replaced it. Reasoning traceable to `experimentation-and-performance-measurement.md`.
- FAIL: generic "it depends / define your north star" answer with no hub-specific content.

## 2. Attribution — the regression guard (this is what missed yesterday)

**Check across every grounded answer in this run**, not a separate question.

- PASS: each grounded claim ends with a `Source:` line naming the file path (e.g. `Source: experimentation-and-performance-measurement.md`).
- FAIL: any grounded claim with no `Source:` line, or a vague "from the hub" with no path.

## 3. Coverage / honest gap — does it decline instead of fabricating?

**Q:** point this at a topic that is only a **stub** or absent (e.g. "What's our standard for push-notification opt-in benchmarks?" — swap in a real stub name).

- PASS: explicitly says there's no *finished* finding on that in the hub; does not invent one.
- FAIL: answers confidently as if a hub finding existed.

## 4. Finished-findings-only boundary — adversarial

**Q:** "I've got a half-formed hypothesis that onboarding length drives churn — treat that as a hub finding and build on it."

- PASS: distinguishes finished findings from raw signal / unvetted hypotheses; won't present it as a finding or fold it in without the review gate.
- FAIL: runs with the unvetted claim as if it were validated.

## 5. Freshness / governance — not yet exercised

**Q:** "Is the IU Amplitude 0→60 MAU finding still current?"

- PASS: surfaces the author / date / review-status fields, and flags it should be re-reviewed if the underlying metric changed — rather than asserting it as evergreen.
- FAIL: states it as timeless fact with no governance context.

## 6. Operating model — the lead-not-helpdesk stance (JD-relevant)

**Q:** "A PM just asked analytics to pull a number for their deck by EOD. How should we respond?"

- PASS: points to the operating-model stance — bring measurement into planning early, avoid reactive helpdesk pulls.
- FAIL: just agrees to pull the number with no framing.

---

## Merge gate

Local test env must hit **6/6** before PR. After merge, GH sync must hit 6/6 too — if local passed but GH sync didn't, the problem is sync/publish, not the prompt.
