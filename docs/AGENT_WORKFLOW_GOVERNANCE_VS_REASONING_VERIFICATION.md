# Agent Workflow Governance vs Reasoning Verification

Status: public-safe positioning note
Scope: Tobi Validator public repository documentation
Product: Tobi Validator — Reasoning Artifact Validator

## Purpose

This note clarifies a boundary that matters as AI-agent governance tools become
more common.

Some systems control how agents produce software or other deliverables. They may
provide approval gates, review steps, event logs, evidence packs, hash-chained
audit trails, or human sign-off rules.

Those systems are useful, but they solve a different problem from Tobi
Validator.

## The Distinction

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
Can this authored Tsubasa source be accepted and converted into a canonical,
reproducible, validator-checkable artifact under the Tsubasa language contract?
```

Authored source is not assumed to be canonical. Tsubasa owns semantics and the
canonicalization contract; Tobi implements and operationally enforces that
contract.

## Operational Evidence vs Validator-Grounded Artifact Evidence

Operational evidence may include:

- workflow logs
- approval records
- review summaries
- hash-chained event logs
- evidence packs
- selected branch reports
- human approval records

Validator-grounded artifact evidence may include:

- accepted or rejected validator outcome
- canonical ASCII output
- `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance result

Both can be useful. They should not be confused.

## Boundary Note

`_h` is compatibility identity only. It is not proof, signature,
certification, or consensus.

Validator acceptance is not universal correctness.

A hash-chained event log can show that events were recorded in sequence, but it
does not establish that the reasoning artifact is canonical under the Tsubasa
contract.

Human approval can authorize a workflow, but it is not deterministic artifact
validation.

## How Tobi Fits With Agent Governance Systems

Tobi can be used inside agent-governance or agent-factory systems as a gate:

```text
agent authors Tsubasa source
→ Tobi validates and canonicalizes it
→ canonical ASCII / _h / diagnostics emitted
→ governance system records the validator result
→ workflow continues, blocks, or escalates
```

This makes Tobi complementary to agent workflow governance.

## Bottom Line

```text
They govern agent delivery.
Tobi validates reasoning artifacts.

They produce operational evidence.
Tobi produces validator-grounded artifact evidence.

They gate workflow completion.
Tobi gates artifact trust before action.
```

Tobi Validator remains a narrow validator-first product for Tsubasa reasoning
artifacts. It is not a generic agent-governance platform.
