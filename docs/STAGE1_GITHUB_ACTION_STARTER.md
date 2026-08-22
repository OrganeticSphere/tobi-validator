# Tobi Validator GitHub Action Starter

Project: Organetic Sphere
Component: Tobi Validator
Descriptor: Reasoning Artifact Validator
Scope: GitHub-first workflow-fit starter for the released Tobi Validator CLI
Date basis: 2026-08-23

> Deterministic validation for canonical reasoning artifacts.

## What This Starter Is

This document is a GitHub-first adoption path for Tobi Validator.

It is intentionally narrow. It provides:

- a starter for understanding how the released validator CLI fits inside GitHub workflows
- a support-layer example for validator-backed repository gates
- a practical path for Tsubasa reasoning-artifact discipline

The authoring and validation model is:

```text
authored Tsubasa source
→ validation and Tsubasa canonicalization through Tobi
→ canonical ASCII + _h compatibility identity
```

or, when input is rejected:

```text
authored Tsubasa source
→ validation through Tobi
→ deterministic diagnostics
```

Authored source is not assumed to be canonical. The Tsubasa language contract
defines the semantic and canonical rules; Tobi implements and operationally
enforces that contract.

This starter is not a new product surface. It uses the published Tobi Validator
GitHub Action wrapper and the current evaluation-access path. It is not a
verification API or a platform integration layer.

## What It Uses

This starter uses only the released Tobi Validator CLI surface:

- commands: `canon` and `golden`
- sample/input paths:
  - `examples/sample.tsubasa`
  - `examples/golden/fixtures.json`
- deterministic validator exits for pass/fail handling in CI
- controlled validator delivery through `eval_token`
- OS-aware archive selection by the Action wrapper

Reference command shapes:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

```sh
./tobi canon ./examples/sample.tsubasa
./tobi golden ./examples/golden/fixtures.json
```

## Important Public-Path Note

The public repository is a GitHub-first documentation and workflow-fit surface.

The example workflow should be read as:

- a reference integration shape
- a workflow-fit aid
- a support-layer example

It should not be read as proof that unrestricted public full-binary production
usage is available through the repository by default.

The Action wrapper is public. Validator delivery is controlled and separate
through Organetic's evaluation broker.

## What A GitHub Workflow Should Do

A narrow Tobi Validator workflow should:

1. check out the repository that owns the files you want to validate
2. request evaluation access from Organetic and store the issued token as `TOBI_EVAL_TOKEN`
3. let the Action infer the platform archive unless an explicit override is required
4. verify integrity material before extraction
5. run the released CLI rather than an invented wrapper surface
6. run `canon` and/or `golden` against repository-owned or shipped example files
7. fail the job when the validator reports rejection, mismatch, or invalid input

## Minimal Copy-Paste Path

1. Copy `examples/github-actions/stage1_tobi_validator_example.yml` into a workflow file in your repository. The legacy example filename is retained for link stability.
2. Keep the default paths for a first pass:
   - `examples/sample.tsubasa`
   - `examples/golden/fixtures.json`
3. Replace those paths with repository-owned validator inputs after the first successful run.
4. Add `TOBI_EVAL_TOKEN` to repository secrets and use the published Action wrapper.
5. Treat any non-zero validator exit as a validation or conformance failure.

## Current Public Execution Path

- request a 7-day evaluation token from Organetic
- store it as `TOBI_EVAL_TOKEN`
- use `OrganeticSphere/tobi-validator@v1`
- pass `eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}`
- run `canon` and/or `golden`

Minimal example:

```yaml
name: Tobi Validator

on:
  workflow_dispatch:
  pull_request:

jobs:
  canon:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: OrganeticSphere/tobi-validator@v1
        with:
          eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
          mode: canon
          canon_input: examples/sample.tsubasa
```

## Language Reference

For the most complete current public-safe authoring guide for repository-owned
artifacts, read:

- `docs/TSUBASA_STAGE1_PUBLIC_SYNTAX_AND_AUTHORING_REFERENCE.md`

The physical filename retains legacy spelling for link stability; the visible
public title is **Tsubasa Language Reference**.

## What It Does Not Imply

Using this starter does not imply:

- factual truth or universal correctness
- a shipped public verification API
- backend or runtime execution
- broad platform maturity
- a future Organetic product surface
- automatic activation of later workflow channels
- unrestricted public source/build access
- a `validate` command

`_h` is compatibility identity only. Canonical equality is not proof of truth.
