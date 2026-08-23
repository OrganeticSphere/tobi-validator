---
name: Bug report
about: Report a reproducible issue in Tobi Validator
title: "[bug] "
labels: bug
assignees: ''
---

# Bug Report

Use this template only for issues grounded in the currently released Tobi
Validator surface.

**Tobi Validator**
**Reasoning Artifact Validator**

> Deterministic validation for canonical reasoning artifacts.

The released surface is intentionally narrow:

- installable `tobi` CLI
- authored Tsubasa source validation
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and workflow usage

Tobi supplies validator success or failure. A consuming workflow owns any allow,
block, merge, release, or escalation policy around that result.

Do not use this template for requests about:

- runtime/backend features
- public verification API features
- broader platform features
- future Organetic products as already-available functionality

## 1. Issue Summary

Describe the problem in one or two direct sentences.

## 2. Exact Command Run

```text
paste command here
```

## 3. Exact Source / Fixture Used

State the exact source file or fixture used.

Examples:

- `examples/sample.tsubasa`
- `examples/golden/fixtures.json`
- your own source file
- your own fixture file

## 4. Environment

- release version / tag:
- operating system:
- shell / terminal:
- local run or workflow run:
- if workflow run, which environment:

## 5. Expected Behavior

Describe what you expected to happen.

## 6. Actual Behavior

Describe what happened.

```text
paste exact output here
```

## 7. Diagnostics

If a diagnostic was produced, include:

- diagnostic code:
- span / location if visible:
- whether this was from `canon` or `golden`:

## 8. Reproduction

Can you reproduce it consistently?

- [ ] yes
- [ ] no
- [ ] uncertain

If yes, list the shortest reproduction steps.

## 9. Issue Classification

- [ ] docs mismatch
- [ ] diagnostics clarity issue
- [ ] expected reject but wording unclear
- [ ] unexpected reject
- [ ] fixture mismatch
- [ ] workflow friction
- [ ] setup / operator issue
- [ ] other narrow Tobi Validator issue

## 10. Scope Confirmation

- [ ] this report is grounded in the currently released Tobi Validator surface
- [ ] this report is not asking for runtime/backend/API/platform functionality as if already released
- [ ] the information above is exact to the best of my ability
