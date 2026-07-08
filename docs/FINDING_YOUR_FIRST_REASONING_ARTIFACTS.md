# FINDING YOUR FIRST REASONING ARTIFACTS

Status: public-safe explainer draft  
Scope: first discovery guide for teams exploring validator-backed reasoning validation  
Product line: AI Verification Engine / Tobi Validator

## Purpose

This document helps a team answer one practical question:

**What in our workflow could actually count as a reasoning artifact?**

It is written for teams that already use AI tools, agent workflows, CI gates,
scientific pipelines, or review processes, but do not yet have a clean folder
called “reasoning artifacts”.

## First principle

A reasoning artifact is **not** just any smart-looking text.

A reasoning artifact is something that is:

- explicit
- reviewable
- repeatable
- stable enough to compare
- meaningful enough to accept or reject
- useful enough to check in CI or a workflow gate

If pass/fail on that artifact would change what your team does, it is a strong candidate.

## What counts as a good first reasoning artifact

Good first candidates usually look like:

- a small explicit decision rule
- a boundary case your team argues about often
- a “should pass” vs “should fail” example pair
- a canonicalization-sensitive example
- a regression case from a previous mistake
- an artifact that should remain equivalent across surface spelling changes

## What does **not** count

These are weak or bad first candidates:

- broad chat transcripts
- hidden chain-of-thought claims
- giant logs with no clear decision boundary
- vague philosophy about “good reasoning”
- a whole agent session with no stable artifact surface
- invented pseudo-syntax that your validator cannot parse
- imagined runtime behavior that your current product does not expose

## Where to look inside your workflow

Most teams already have reasoning-artifact candidates, just under different names.

### In CI / pull request workflows
Look for:

- pass/fail gate logic
- release blocking conditions
- artifact checks before merge
- policy checks
- validation scripts
- expected-output comparisons

### In agent workflows
Look for:

- explicit agent outputs that are meant to be reused
- decision summaries
- approved action plans
- structured intermediate outputs
- cases where one agent must justify something to another

### In scientific or reproducible workflows
Look for:

- acceptance criteria
- reject criteria
- reproducibility-sensitive artifacts
- explicit “same meaning / different spelling” problems
- boundary cases around malformed or ambiguous inputs

### In manual review
Look for:

- things reviewers repeatedly argue about
- edge cases that force human intervention
- cases where “this should pass” and “this should fail” are not written down clearly
- regressions that happened because meaning drifted across handoff

## What to ask yourself

Use these questions:

1. Does this artifact have a clear pass/fail boundary?
2. Would a wrong acceptance or rejection matter?
3. Could we save this artifact and compare it later?
4. Could two surface forms mean the same thing here?
5. Is there a nearby malformed or bad sibling case?
6. Does this artifact belong in a gate before merge/release/expensive compute?

If the answer is “yes” to several of these, the artifact is probably worth testing.

## Start from the public conformance corpus

You can start from the public Stage 1 conformance corpus:

- [OrganeticSphere/tsubasa-stage1-conformance](https://github.com/OrganeticSphere/tsubasa-stage1-conformance)

The corpus gives you known-good public `.tsubasa` examples to inspect. You can
compare your own artifacts against its style, size, and public Stage 1
boundaries before deciding what belongs in your own case set.

Use the public
[manifest](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json)
and
[verification report](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md)
as examples of how expected outputs should be recorded.

Do not copy unverified expectations into your own final manifest. Any final
canonical output, diagnostic, exit code, or `_h` value must come from a real
Tobi Validator run.

Idempotence remains pending in v0.1 and should not be treated as verified.

## The easiest first family to build

A good first family has only 3–7 cases.

Recommended shape:

- 2–4 accepted cases
- 1–3 reject cases
- 1 equivalence or convergence case if relevant

This is enough to learn something real without drowning in noise.

## Two strong beginner patterns

### Pattern A — boundary family
Use when the question is:
- what should pass?
- what should fail?

Example structure:
- valid artifact
- malformed artifact
- visually confusable or noisy artifact

### Pattern B — convergence family
Use when the question is:
- do these different surface forms really mean the same thing?

Example structure:
- simple accepted form
- accepted variant spelling
- stress spelling with extra normalization pressure
- malformed nearby sibling

## How to know when you found something real

You found a real reasoning artifact when all of this is true:

- the artifact can be written down explicitly
- a reviewer can disagree with it in a concrete way
- a validator or gate could meaningfully check it
- the outcome affects what enters the repository or workflow
- it is smaller than a whole session, but bigger than a random token

## What to do after you find one

Once you have one good candidate:

1. write the accepted and rejected forms explicitly
2. remove vague or imagined behavior
3. narrow it to what your current validator can actually check
4. keep it small
5. save it as a reusable case set
6. run it through your validation path

## Why this matters

The goal is not just to reject bad input.

The deeper value is to move reasoning from:

- opaque
- informal
- hard to compare
- easy to drift

toward something more:

- canonical
- reproducible
- validator-checkable

That is the operational meaning of a reasoning artifact.

## Minimal starter checklist

Before your first pilot, make sure you have:

- one artifact that should pass
- one artifact that should fail
- one reason why the difference matters
- one place in your workflow where a gate is useful

That is enough to begin.

## Bottom line

You do not need a huge corpus to start.

You need one narrow, explicit, consequential artifact family.

Start there.
