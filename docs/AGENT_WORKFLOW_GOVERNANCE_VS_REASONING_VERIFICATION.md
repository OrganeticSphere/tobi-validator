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

Tobi Validator answers a narrower and stricter question:

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

Validator-grounded artifact evidence includes:

- accepted or rejected validator outcome,
- canonical ASCII output,
- `_h` compatibility identity,
- deterministic diagnostics,
- golden/conformance execution result.

Both can be useful. They should not be confused.

## Why this matters

A workflow can be well-governed and still contain an invalid reasoning artifact.

A human can approve a workflow, while the underlying artifact still fails validation.

A hash-chained event log can prove that something happened in order, but it does not prove that the reasoning artifact is canonical or validator-checkable.

Tobi is designed for the artifact boundary: before an output becomes operational trust evidence, the artifact should be accepted, rejected, or diagnosed by the validator.

## How Tobi fits with agent governance systems

Tobi can be used inside agent-governance or agent-factory systems as a gate:

```text
agent produces artifact
-> Tobi validates artifact
-> canonical ASCII / _h / diagnostics emitted
-> governance system records validator result
-> workflow continues, blocks, or escalates
```

This makes Tobi complementary to agent workflow governance.

## Bottom line

```text
They govern agent delivery.
We validate reasoning artifacts.

They produce operational evidence.
We produce validator-grounded canonical evidence.

They gate workflow completion.
We gate artifact trust before action.
```

This distinction keeps the Stage 1 product surface clear: Tobi Validator is a narrow validator-first CLI for canonical, reproducible, validator-checkable reasoning artifacts.
