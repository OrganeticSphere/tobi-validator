# Finding Your First Reasoning Artifacts

Status: public-safe explainer draft
Scope: first discovery guide for teams exploring validator-backed reasoning artifacts
Product: Tobi Validator — Reasoning Artifact Validator

## Purpose

This document helps a team answer one practical question:

**What in our workflow could actually count as a reasoning artifact?**

It is written for teams that already use AI tools, agent workflows, CI gates,
scientific pipelines, or review processes, but do not yet have a clean folder
called “reasoning artifacts”.

## First Principle

A reasoning artifact is **not** just any smart-looking text.

A useful first candidate is:

- explicit
- reviewable
- repeatable
- stable enough to compare
- meaningful enough to accept or reject
- useful enough to check in CI or a workflow gate

If pass/fail on that artifact would change what your team does, it is a strong
candidate.

For Tobi Validator, the artifact begins as authored Tsubasa source:

```text
authored Tsubasa source
→ validation and Tsubasa canonicalization through Tobi
→ canonical artifact + _h, or deterministic diagnostics
```

Authored source is not assumed to be canonical. Tsubasa owns the language and
canonicalization contract; Tobi implements that contract.

## Good First Candidates

Good first candidates usually look like:

- a small explicit decision rule
- a boundary case your team argues about often
- a “should pass” vs “should reject” example pair
- a canonicalization-sensitive example
- a regression case from a previous mistake
- source forms that should converge to the same canonical representation

## Weak Or Bad First Candidates

Avoid:

- broad chat transcripts
- hidden chain-of-thought claims
- giant logs with no clear decision boundary
- vague philosophy about good reasoning
- a whole agent session with no stable artifact surface
- invented pseudo-syntax Tobi cannot parse
- imagined runtime behavior the current product does not expose

## Where To Look Inside Your Workflow

Most teams already have candidates under different names.

### In CI / Pull-Request Workflows

Look for:

- pass/fail gate logic
- release-blocking conditions
- artifact checks before merge
- policy checks
- validation scripts
- expected-output comparisons

### In Agent Workflows

Look for:

- explicit agent outputs intended for reuse
- decision summaries that need a stable handoff
- approved action plans
- structured intermediate outputs
- cases where one agent must provide evidence to another

### In Scientific Or Reproducible Workflows

Look for:

- acceptance criteria
- reject criteria
- reproducibility-sensitive artifacts
- same-meaning / different-surface problems
- boundary cases around malformed or ambiguous source

### In Manual Review

Look for:

- things reviewers repeatedly argue about
- edge cases that force human intervention
- cases where pass and reject expectations are not written down
- regressions caused by meaning drift across a handoff

## Questions To Ask

1. Does this candidate have a clear pass/reject boundary?
2. Would a wrong acceptance or rejection matter?
3. Could we save it and compare it later?
4. Could two supported source forms express the same canonical structure?
5. Is there a nearby malformed sibling?
6. Does it belong in a gate before merge, release, or expensive compute?

If several answers are yes, the candidate is probably worth testing.

## Start From The Tsubasa Conformance Corpus

Start from the public Tsubasa Conformance Corpus:

- [OrganeticSphere/tsubasa-stage1-conformance](https://github.com/OrganeticSphere/tsubasa-stage1-conformance)

The repository slug retains legacy spelling for link stability. The corpus gives
you known public `.tsubasa` source examples, expected results, and explicit
coverage limitations.

Use the public
[manifest](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json)
and
[verification report](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md)
as examples of how observed results should be recorded.

Do not copy unverified expectations into a final manifest. Canonical output,
diagnostics, exit codes, and `_h` values must come from real Tobi Validator
runs.

Idempotence remains pending in v0.1 and must not be treated as verified.

## The Easiest First Family

A good first family has only 3–7 cases:

- 2–4 accepted cases
- 1–3 reject cases
- 1 equivalence or convergence case when relevant

This is enough to learn something real without drowning in noise.

## Two Strong Beginner Patterns

### Pattern A — Boundary Family

Use when the question is what should pass and what should reject.

Example structure:

- valid authored source
- malformed source
- visually confusable or noisy source

### Pattern B — Convergence Family

Use when the question is whether different supported surface forms converge to
one canonical representation.

Example structure:

- simple accepted form
- accepted variant
- stress form with additional normalization pressure
- malformed nearby sibling

## How To Know When You Found Something Real

You found a useful reasoning-artifact candidate when:

- it can be written down explicitly
- a reviewer can disagree with it concretely
- Tobi can meaningfully accept or reject it
- the result affects what enters a repository or workflow
- it is smaller than a whole session but larger than a random token

## What To Do Next

1. write accepted and rejected source forms explicitly
2. remove vague or imagined behavior
3. narrow the case to what Tobi can currently check
4. keep it small
5. save it as a reusable case set
6. run it through the validation path
7. record only observed canonical output or diagnostics

## Why This Matters

The goal is not only to reject malformed source. It is to move an important
handoff from:

- trace-like
- informal
- hard to compare
- easy to drift

toward an artifact that is:

- canonical after acceptance
- reproducible
- validator-checkable
- suitable for a workflow boundary

## Minimal Starter Checklist

Before your first pilot, have:

- one source artifact expected to pass
- one source artifact expected to reject
- one reason why the difference matters
- one place in your workflow where a gate is useful

That is enough to begin.

## Boundaries

`_h` is compatibility identity only. Canonical equality does not establish
factual truth. Validator acceptance is not universal correctness.

## Bottom Line

You do not need a huge corpus to start. You need one narrow, explicit,
consequential artifact family.
