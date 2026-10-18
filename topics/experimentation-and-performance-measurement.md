# Experimentation & Performance Measurement

**Author:** Natalia Wierzbowska
**Reviewer:** —
**Date:** 2026-10-18
**Review status:** Example finding included to demonstrate this repo's format — has not yet passed through this hub's actual review process in a live org deployment.

## Finding

Revenue is usually the wrong primary metric for an experiment in a fast-delivery or subscription business — not because it doesn't matter, but because it's too lagging and too noisy to give a clean read on a single feature change.

## Context

At both Hotjar and Flink, the default instinct was to test features against revenue, since revenue is what the business ultimately cares about. In practice, revenue in these businesses depends on basket composition and takes weeks to materialize, so testing against it directly requires large samples and long runtimes to detect anything.

## What was proposed instead

Order conversion rate and average basket value — both metrics closer to what the feature actually touches, both fast enough to give a clean read within a normal experiment runtime. Revenue stayed tracked as the outcome the org ultimately cared about, just not the thing being tested against directly.

## Why it matters

This became the standard framework for how the team ran experiments going forward — not a one-off override, but an adopted default. The underlying principle generalizes: **pick the fastest, least noisy metric that sits causally closest to what the feature changes, and keep the lagging business metric as a tracked outcome rather than the test target.**

This is especially relevant for B2B SaaS with annual contracts, where revenue recognition can lag a renewal decision by months — proxy metrics matter even more there than in a fast-delivery business.

## Caveats

A proxy metric is only valid if it's been checked to actually correlate with the lagging outcome it's standing in for — see the calibration approach in [backbone of models](measurement-definitions/backbone-of-models.md) for how that validation was done in a related case. Don't adopt a proxy metric on the argument "it's faster" alone.
