# Tobi Validator Quickstart — First 10 Minutes

Project: Organetic Sphere
Component: Tobi Validator
Descriptor: Reasoning Artifact Validator
Scope: first-time public GitHub entry quickstart
Date basis: 2026-08-23

> Deterministic validation for canonical reasoning artifacts.

## What This Product Is

Tobi Validator is a narrow validator-first CLI.

It is for:

- validating authored Tsubasa source
- applying Tsubasa canonicalization through Tobi
- producing canonical ASCII for accepted source
- producing the current `_h` compatibility identity
- surfacing deterministic diagnostics for rejected source
- running shipped `golden` conformance checks

It is not:

- a runtime
- a backend
- a public verification API
- a platform SDK
- a theorem prover or universal truth engine

The source-to-result model is:

```text
authored Tsubasa source
→ validation and canonicalization through Tobi
→ canonical ASCII + _h compatibility identity
```

or:

```text
authored Tsubasa source
→ validation through Tobi
→ deterministic diagnostics
```

Authored input is not assumed to be canonical. The Tsubasa language contract
owns semantics; Tobi is the reference validator that implements that contract.

## What This Public Repository Is For

This public repository is for:

- understanding the released Tobi Validator surface
- reading public documentation
- inspecting shipped examples
- understanding GitHub workflow fit
- reporting reproducible issues and workflow-fit questions

It is not the full private development source repository or an unrestricted
public full-binary distribution path.

## First 10 Minutes In This Repository

Use these first 10 minutes to:

1. understand the released Tobi Validator product contour
2. inspect the shipped examples
3. understand the command shapes of the released CLI
4. understand the GitHub-first Action path

## Released Command Shapes

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

These commands show how the validator is used. They do not imply unrestricted
public binary delivery through this repository.

## Shipped Examples

This repository includes:

- `examples/sample.tsubasa`
- `examples/golden/fixtures.json`

Use them to understand:

- the shape of authored Tsubasa source
- the canonical output produced for accepted source
- the fixture structure used by `golden`

## What Successful Output Looks Like

For `canon`, the expected output shape is:

- `CANON:`
- canonical ASCII body
- `HASH:`
- current `_h` rendered as hex

For `golden`, the expected output shape is:

- `OK (<n> fixtures)`

For the current shipped fixture corpus, a representative success reading is:

- `OK (45 fixtures)`

## How To Read The Output

### Canonical ASCII

Canonical ASCII is the stable representation produced through Tsubasa
canonicalization in Tobi for accepted source. Supported surface variants may
converge to the same recorded canonical output.

### `HASH:` Label And `_h`

`HASH:` is the CLI label under which Tobi prints the current `_h` compatibility
identity for the accepted canonical artifact.

`_h` is compatibility identity only. It is not proof, certification, signature,
or consensus.

### Diagnostics

If input is rejected, Tobi returns deterministic diagnostics:

- stable error codes
- stable spans under the current validator contract
- explicit failure instead of silent acceptance

## What This Release Does Not Do

The current product does not provide:

- runtime execution
- backend output
- code generation
- materialization
- public verification API
- broader platform or integration surface

Do not read the repository or its examples as proof of runtime, backend, or
platform maturity beyond the validator-first contour.

## What To Do Next

Continue with:

- `docs/STAGE1_INSTALL_AND_USAGE.md`
- `docs/STAGE1_DIAGNOSTICS_REFERENCE.md`
- `docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md`
- `docs/STAGE1_GITHUB_ACTION_STARTER.md`

The physical filenames retain legacy `STAGE1` spelling for link stability.
Their visible titles and current product language use Tobi Validator.
