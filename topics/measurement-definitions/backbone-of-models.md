# Backbone of Models to Feed Into

**Author:** Natalia Wierzbowska
**Reviewer:** —
**Date:** 2026-10-18
**Review status:** Example finding included to demonstrate this repo's format — has not yet passed through this hub's actual review process in a live org deployment.

## Finding

A validated behavioral threshold can replace a lagging revenue/retention signal as the input to downstream models, when the threshold is chosen by minimizing misclassification rather than by gut feel.

## Context

At HelloFresh, the team needed an early signal of whether a new subscriber was on track to become a sticking, profitable customer — long before revenue or 12-month retention data would confirm it either way. Waiting for the lagging signal meant every experiment and every model built on top of it ran slow and noisy.

## Method

Built a cohort matrix of order-composition thresholds — from "1 box in the first 10 weeks" up to "10 boxes in the first 10 weeks." For each threshold, plotted precision against recall at the 1-year retention mark: how reliably hitting that threshold predicted actual long-term retention, versus how many eventual retainers would be missed by setting the bar there.

**"5 boxes in 10 weeks" was the threshold where the two curves crossed** — the point that minimized total misclassification, rather than over-indexing on catching everyone (a low bar, lots of false positives) or being overly conservative (a high bar, lots of missed retainers).

## Why it matters

This became the standard predictive signal the team fed into downstream models and reporting, used instead of waiting for lagging revenue/retention data to confirm the same thing months later. The same logic (find the threshold where precision and recall cross, rather than picking a round number) is reusable for any "is this behavior an early signal of a later outcome" question — see also the resolved-conversation calibration approach in [AI-Native Measurement](../ai-event-data/).

## Caveats

The specific threshold (5-in-10) is HelloFresh/meal-kit specific — a function of that product's cadence and the cost of a false positive. What transfers is the *method* (cohort matrix + precision/recall crossing), not the number itself. Re-derive the threshold for any new product rather than importing "5-in-10" as a constant.
