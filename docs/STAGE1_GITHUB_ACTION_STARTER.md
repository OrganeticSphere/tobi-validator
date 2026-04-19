# Stage 1 GitHub Action Starter

Project: Organetic Sphere  
Component: Tobi  
Product: AI Verification Engine / Tobi Validator  
Scope: GitHub-first workflow-fit starter for the released Stage 1 validator CLI  
Date basis: 2026-04-15

## What This Starter Is

This document is a GitHub-first support-layer adoption path for the released
Stage 1 product line:

- `AI Verification Engine / Tobi Validator`

It is intentionally narrow.

It is:

- a starter for understanding how the released validator CLI fits inside GitHub workflows
- a support-layer example for validator-backed repository gates
- a practical path for canonical reasoning artifact discipline

This starter is not a new product surface.
This starter uses the published GitHub Action wrapper and the current public evaluation access path for the released Stage 1 validator line.
This starter is not a verification API.
This starter is not a platform integration layer.

## What It Uses

This starter uses only the released Stage 1 CLI truth:

- release-accurate commands: `canon` and `golden`
- release-accurate sample/input paths:
  - `examples/sample.tsubasa`
  - `examples/golden/fixtures.json`
- deterministic validator exits for pass/fail handling in CI

Reference command shapes:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

## Important Public-Path Note

The public repository is a GitHub-first documentation and workflow-fit surface.

The example workflow in this repository should be read as:

- a reference integration shape
- a workflow-fit aid
- a support-layer example

It should not be read as proof that unrestricted public full-binary production
usage is already available through the public repository by default.

## What A GitHub Workflow Should Do

A narrow Stage 1 GitHub workflow should:

1. check out the repository that owns the files you want to validate
2. obtain access through the public evaluation access path using TOBI_EVAL_TOKEN
3. verify integrity material before use
4. run the released CLI, not an invented wrapper surface
5. run `canon` and/or `golden` against repository-owned or shipped example files
6. fail the job when the validator reports rejection, mismatch, or invalid input

The minimal example in this repo is meant to show that integration shape.

## Minimal Copy-Paste Path

1. Copy `examples/github-actions/stage1_tobi_validator_example.yml` into
   `.github/workflows/stage1_tobi_validator.yml` in your repository.
2. Keep the default paths for a first pass:
   - `examples/sample.tsubasa`
   - `examples/golden/fixtures.json`
3. Or replace those paths with repository-owned validator inputs after the first
   successful run.
4. Add TOBI_EVAL_TOKEN to your repository secrets and use the published action wrapper path.
5. Treat any non-zero validator exit as a real validation or conformance failure.

## Current public execution path:
- request a 7-day evaluation token from Organetic
- store it as TOBI_EVAL_TOKEN
- use OrganeticSphere/tobi-validator@v1
- run canon and/or golden

## What It Does Not Imply

Using this starter does not imply:

- a shipped verification API
- backend execution
- runtime execution
- broad platform maturity
- Stage 2 product surface
- automatic activation of later workflow channels
