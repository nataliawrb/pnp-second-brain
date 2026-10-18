# AI-Native Measurement

The newest domain, and the one where the old playbook breaks fastest — activity metrics that meant "more value" in a traditional product can mean the opposite in an AI-native one.

## Measuring AI activity & translating conversation into event data
A prompt, a multi-turn exchange, an accepted or corrected suggestion isn't a click — it needs its own event schema rather than being squeezed into action-tracking patterns built for buttons and forms.

## Comparing AI vs. non-AI features
Can't compare on activity (AI is often *designed* to reduce human effort, so less activity can mean a better outcome, not a worse one). Compare on a mechanism-agnostic outcome instead — "task completed correctly and fast," true whether a human or the AI did it — and normalize effort by outcome, not by time.

## Agents, AI automations & morning briefings
The practical surface area: scheduled/triggered automations, agent-run workflows, and digest-style outputs (e.g. a morning briefing) — each needs its own definition of "worked" that isn't just "ran without erroring."

## Omni models & the Omni API to Claude
How a BI layer (Omni) and an LLM layer (Claude) connect — what gets modeled once in Omni and queried conversationally through Claude, versus logic that has to live natively in one or the other.

## Conversational analytics
Letting someone ask a question in plain language and get a correct, sourced answer — the UX promise this whole measurement layer is ultimately in service of.

## Balance of new UX with prompt-based agents
An open design question, not a solved one: how much of the interface becomes conversational/agentic before it stops feeling like the product people are used to. See [`open-tensions.md`](open-tensions.md).

## Trust & calibration metrics (methodology note)
When outcome metrics alone aren't enough: acceptance rate of AI recommendations, override/correction rate, and escalation-to-human rate — these catch the case where an AI feature looks efficient but is quietly being overridden or ignored. Watch for two specific traps: **survivorship bias** (the AI cherry-picks easy cases and escalates hard ones — measure across the whole population, not just what the AI chose to handle) and **quality substitution** (faster only counts as a win if outcome quality holds — otherwise the cost just moved somewhere less visible).
