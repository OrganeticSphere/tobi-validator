# Tsubasa For Agents

Status: public-safe explainer draft
Scope: narrow guidance for agent-authored artifacts under the released Tobi Validator contract
Product: Tobi Validator — Reasoning Artifact Validator

## Purpose

This document explains how an AI agent should approach Tsubasa when producing
artifacts for Tobi Validator.

It is intentionally narrow. It does not try to teach the complete long-term
language vision. It teaches enough to produce validator-meaningful authored
source without inventing unsupported semantics.

## First Rule

Do not treat Tsubasa as a general scripting language.

Use this mental model:

```text
agent authors Tsubasa source
→ Tobi validates and applies the Tsubasa canonicalization contract
→ canonical artifact + _h, or deterministic diagnostics
```

Authored source is not assumed to be canonical. Tsubasa owns the language and
canonicalization contract; Tobi is the reference validator that implements and
operationally enforces that contract.

The safe agent behavior is:

- produce small explicit artifacts
- avoid imagined runtime features
- avoid invented authoring syntax
- stay close to what Tobi can actually check
- learn from canonical output and deterministic diagnostics

## What An Agent Should Try To Produce

A good agent-authored artifact is:

- small
- explicit
- reviewable
- narrow in scope
- suitable for pass/reject reasoning
- easy to place beside nearby sibling cases

A bad agent output is:

- a long essay presented as executable structure
- policy prose with no artifact form
- pseudo-code Tobi cannot parse
- smart-sounding structure with no operational meaning
- already-canonical claims unsupported by a real validator run

## What Agents Must Not Invent

Do **not** invent:

- regex engines
- runtime APIs
- generic byte scanners
- general string sanitation layers
- backend execution behavior
- platform features
- YAML-like wrappers and call them Tsubasa
- broad language rules not exposed by the current public contract

If uncertain, narrow the artifact instead of broadening it.

## A Better Mental Model

Think in terms of:

- accepted case
- rejected sibling
- canonical convergence family
- validator-facing boundary
- smallest useful case set

This is better than thinking in terms of:

- feature-rich language program
- mini runtime
- generic parser DSL
- policy file pretending to be code

## Good First Authoring Pattern

A useful first agent-authored family looks like this.

### Accepted case

A small valid source artifact.

### Accepted variant

A different supported surface form expected to produce the same recorded
canonical output under the same validator contract.

### Reject sibling

A nearby malformed or unsupported case expected to produce deterministic
diagnostics.

That is enough for a useful first validator-facing experiment.

## Two Concrete Patterns

### Pattern 1 — Boundary

Use when the question is whether a kind of source should pass or reject.

Shape:

- one accepted case
- one malformed reject
- one confusable/noisy reject if relevant

### Pattern 2 — Convergence

Use when the question is whether different supported surface forms produce one
recorded canonical result.

Shape:

- baseline accepted form
- alternate accepted form
- stress form
- malformed sibling

## From Raw Model Output To Tsubasa Source

### Step 1 — Start with the claim

Examples:

- “this source should pass”
- “this malformed sibling should reject”
- “these two supported forms should produce the same canonical result”

### Step 2 — Strip unsupported mechanism

Remove:

- invented regex rules
- runtime assumptions
- non-existent APIs
- pseudo metadata wrappers

### Step 3 — Reduce to explicit source cases

Write actual Tsubasa source, not commentary pretending to be executable
structure.

### Step 4 — Keep only validator-meaningful expectations

For example:

- should pass
- should reject
- should produce the same recorded canonical output as another accepted case
- should retain stable compatibility identity when exposed

### Step 5 — Save the smallest useful set

Do not begin with 50 cases. Begin with 3–7.

## Canon-Oriented Thinking

Focus on:

- exact authored source
- exact rejected source
- canonical output for accepted source
- recorded comparison among accepted cases under the same validator contract
- no canonical output for rejected source

Do not fill canonical output or `_h` from model memory. Record them only from a
real Tobi run.

## Golden-Oriented Thinking

Readable golden sets may include:

- baseline accepted case
- accepted variant
- stress form
- malformed nearby sibling

Golden fixtures remain conformance evidence. They do not make validator
acceptance universal correctness.

## What Agents Should Optimize For

Optimize for:

- explicitness
- narrowness
- comparability
- repeatability
- operational usefulness

Do not optimize for:

- expressive overreach
- pseudo-language design
- broad future-looking semantics
- sounding impressive

## Compact Self-Check

Before finalizing authored source, ask:

1. Can Tobi actually check this source under the public contract?
2. Did I invent any runtime, API, or syntax?
3. Did I write actual source cases, or only policy prose?
4. Is there a nearby reject sibling?
5. Is the artifact small enough for a workflow to use as a validation check?
6. Am I treating canonical output as a result of validation rather than an input assumption?

If the answer to question 2 is yes, rewrite and narrow.

The consuming workflow owns any allow, block, merge, release, or escalation
policy. Tobi supplies the validator result; it does not authorize downstream
action.

## Boundaries

`_h` is compatibility identity only. It is not proof, signature,
certification, or consensus. Canonical equality does not establish factual
truth. Tobi implements the Tsubasa language contract but does not own semantic
authority.

## Bottom Line

The productive move is not to generate more language. It is to generate less
noise.

A good agent-authored Tsubasa artifact begins as small, explicit source and
becomes canonical only after acceptance through Tobi.
