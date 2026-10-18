# Legal & Consent

**Author:** Natalia Wierzbowska
**Reviewer:** —
**Date:** 2026-10-18
**Review status:** Example finding included to demonstrate this repo's format — has not yet passed through this hub's actual review process in a live org deployment.

## Finding

A mismatch between frontend and backend consent state silently double-counted users across reporting at IU — a governance failure, not a technical footnote, and one serious enough to raise directly with the CTO rather than patch quietly.

## Context

IU's consent management ran through Usercentrics and a Domain Proxy, feeding an identity resolution framework spanning Amplitude ID, a backend user_id, and an internal account identifier (ac5id). Frontend and backend reporting pulled from this consent/identity layer independently — and a logic mismatch between the two meant some users were being represented twice across frontend- and backend-sourced reports.

## What this actually was

A systemic cross-team issue, not an individual mistake — the kind of bug that's easy to misattribute to "someone configured something wrong" when the real cause is that two systems built independently made different assumptions about the same consent state. Framing it that way (system design issue, not a person issue) was what made it possible to raise clearly with the CTO under pressure, without it reading as finger-pointing.

## Why it matters

Consent logic has to be correct *before* it's fast. This is the concrete version of that principle: a consent/identity mismatch doesn't just risk a compliance problem, it corrupts the numbers everyone downstream is making decisions on, and it does so silently — nothing errors, the dashboards just quietly lie.

## Caveats

The fix here was specific to IU's stack (Usercentrics + Domain Proxy + three-way identity resolution). The transferable lesson is the *check*: whenever frontend and backend each independently compute or cache consent/identity state, audit for drift between them — don't assume agreement because both "look correct" individually.
