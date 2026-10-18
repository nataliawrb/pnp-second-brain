# Fundamentals & Instrumentation

The layer everything else depends on. If this is wrong, every number built on top of it is wrong too — this is the domain where "finished finding" has to mean *verified against the actual data*, not just plausible.

## Data sources
Where behavioral and transactional data actually originates, and which source is authoritative when two disagree.

## Tracking plan & naming convention
The contract for what gets tracked and how it's named — the single artifact that keeps instrumentation legible as the product and team grow.

## Tracking strategy & ownership
Who decides what gets tracked, who implements it, who's accountable when it breaks. Strategy without named ownership degrades into "everyone's and no one's."

## QA & ownership / unit testing
Events are code. They should be tested like code — payload shape, trigger conditions, edge cases — before they're trusted like data.

## Data accuracy
The gap between "an event fires" and "an event fires correctly, every time, for every user." Most trust failures live in this gap.

## Semantic layer
The translation layer between raw events and business-meaningful metrics — what makes "active user" mean the same thing in every dashboard that uses it.

## Identity resolution & two-sided users
Stitching a user across devices/platforms (Amplitude ID, backend user_id, account ID) — and, where the product is two-sided (e.g. an operator/property-manager account vs. their guests/traffic), deciding which side's identity model the measurement layer is actually built around.

## Legal, consent & cross-platform tracking
Consent logic has to be correct *before* it's fast — a double-counting bug from mismatched consent states across frontend/backend is a governance failure, not a technical footnote.

## Latency, FE/BE, and user access
Operational realities that determine whether "real-time" claims about a metric are true: how fast an event actually reaches the warehouse, where frontend vs. backend tracking diverges, who's allowed to see what.

## Action tracking vs. AI tracking
Traditional action-based event tracking (click, view, submit) doesn't cleanly capture AI-native interactions (a prompt, a multi-turn conversation, an accepted/rejected suggestion) — this needs its own instrumentation pattern, not a forced fit into the old schema. See [`ai-native-measurement.md`](ai-native-measurement.md).
