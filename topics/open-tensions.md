# Open Tensions

Unresolved by design — naming these out loud is more useful than pretending they're solved.

## How this differs from Product Ops
Product Ops governs *how decisions get made* — process, rituals, tooling, backlog hygiene, often the PRD template itself. This repo governs *what's actually true to decide with* — validated evidence. One is operational rigor, the other epistemic rigor; that's why the entry gate here is analyst review, not a generalist process check.

Where the two will look like they overlap:
- **Prioritization frameworks** — Ops may run the ritual of a prioritization meeting; this repo supplies the validated inputs that make it data-informed rather than opinion-informed.
- **Documentation standards** — Ops may mandate that a one-pager exists; this repo owns whether the measurement claims inside it are correct and sourced.
- **PRD process** — the sharpest overlap, since "PRDs with sizing, expected metric impact, a measurement plan" sits right at the seam of who owns the template vs. who owns the measurement content filling it in.

## Balance of data governance vs. insight-sharing speed
Too much review latency and people route around the hub entirely. Too little and it's back to unverified noise. The lever is reviewer capacity and rotation, not a fixed policy — this needs to flex as the org and the team grow.

## Org design implication
If this works, "contributor to the shared insight hub" becomes part of how PM/analyst/research/design roles are defined, not just a tool they use. That's a bigger ask than a repo — worth being explicit about if it comes up.

## How is this different from Product Ops, part 2: does it even exist yet?
Nothing confirms whether a given org (e.g. one just being joined) has a Product Ops function at all. If it doesn't, this tension is moot for now — worth flagging as "revisit once both functions exist" rather than over-preparing a boundary dispute that may not be real yet.

## New way of organizing product and analytics teams
An open structural question: centralized vs. embedded vs. some hybrid, and whether that choice changes once a shared insight repo removes some of the reason embedding existed in the first place (proximity to context that used to live only in one person's head).

## Balance of new UX with prompt-based agents
As more of the interface becomes conversational, how much of the traditional UI stays, and for which tasks. Not solved — see [`ai-native-measurement.md`](ai-native-measurement.md).

## Conversational analytics vs. Product Ops, redux
Where "ask a question in plain language and get an answer" starts to blur with what a Product Ops-style enablement function might also claim to own.
