# Reporting & Measurement

The layer that turns instrumented events into numbers people actually act on.

## KPI tree & key reports
The hierarchy connecting top-line business outcomes down to the leaf metrics product teams can actually move — and the small set of reports that stay authoritative rather than proliferating into forty slightly-different dashboards.

## Defining granularity of the reporting layer
Deciding the right level of aggregation (event → session → user → account → org) for a given question — too granular and nobody can read it, too aggregated and it hides the thing you needed to see.

## How measures are calculated
The actual formula behind a metric name, documented well enough that two people computing "retention" independently get the same number.

## Backbone of models to feed into
Which downstream models (churn, LTV, scoring) this reporting layer needs to support — reporting isn't just dashboards, it's the input layer for everything built on top.

## Activation, conversion & retention
Defining the activation window and first-usage signal, conversion per plan/product, and the activation-to-retention pipeline as one connected funnel rather than three separate analyses that don't reconcile.

## Monetization strategy
How usage and value translate into revenue model decisions — pricing tiers, plan design, expansion triggers.

## Features & models
The catalog of what's shipped and what's been built to score/predict on top of it — kept current enough that "do we already have a model for this" has a fast answer.

## Experimentation & performance measurement
How clean A/B tests get run where possible, and what replaces them where they're not (see [`ai-native-measurement.md`](ai-native-measurement.md) for the AI-specific version of this problem).
