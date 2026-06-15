# Agent workflow governance vs reasoning verification

Status: public-safe positioning note  
Scope: Stage 1 / Tobi Validator public repository documentation  
Product line: AI Verification Engine / Tobi Validator

## Purpose

This note clarifies a boundary that is becoming more important as adjacent AI-agent governance tools appear in the market.

Some tools control how AI agents produce software or other deliverables. They may provide approval gates, review steps, event logs, evidence packs, hash-chained audit trails, or human sign-off rules.

Those systems are useful, but they solve a different problem from Tobi Validator.

## The distinction

```text
Agent workflow governance controls process and delivery.
Tobi Validator validates the reasoning artifact.
```

A workflow-governance system can answer questions such as:

- Was a plan approved?
- Did a review step run?
- Was a branch selected?
- Did a human approve promotion?
- Was an event log or evidence pack produced?

Tobi Validator answers a narrower artifact-boundary question:

```text
Can this reasoning artifact become canonical, reproducible, and validator-checkable?
```

## Operational evidence vs validator-grounded artifact evidence

Operational evidence may include:

- workflow logs,
- approval records,
- review summaries,
- hash-chained event logs,
- evidence packs,
- selected branch reports,
- human approval records.

Validator-grounded artifact evidence may include:

- accepted or rejected validator outcome,
- canonical ASCII output,
- `_h` compatibility identity,
- deterministic diagnostics,
- golden/conformance execution result.

Both can be useful. They should not be confused.

## Boundary note

`_h` is compatibility identity only. It is not proof of truth.

Validator acceptance is not consensus by itself.

A hash-chained event log can show that events were recorded in sequence, but it does not prove that the reasoning artifact is canonical or validator-checkable.

Human approval can authorize a workflow, but it is not deterministic validation.

## How Tobi fits with agent governance systems

Tobi can be used inside agent-governance or agent-factory systems as a gate:

```text
agent produces artifact
→ Tobi validates artifact
→ canonical ASCII / _h / diagnostics emitted
→ governance system records validator result
→ workflow continues, blocks, or escalates
```

This makes Tobi complementary to agent workflow governance.

## Bottom line

```text
They govern agent delivery.
We validate reasoning artifacts.

They produce operational evidence.
We produce validator-grounded artifact evidence.

They gate workflow completion.
We gate artifact trust before action.
```

This distinction keeps the Stage 1 product surface clear: Tobi Validator is a narrow validator-first CLI for canonical, reproducible, validator-checkable reasoning artifacts.
