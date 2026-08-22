# Tobi Validator Diagnostics Reference

Project: Organetic Sphere
Component: Tobi Validator
Descriptor: Reasoning Artifact Validator
Scope: operator reference for current released validator diagnostics
Date basis: 2026-08-23

## What This Document Is For

This document is a practical operator reference for Tobi diagnostics.

Use it to answer:

- what an error code usually means
- whether failure occurred during source ingestion, parsing, or semantic checks
- what to check before reporting an issue
- how to distinguish source rejection from `golden` mismatch

This document is not:

- semantic authority
- a promise of broader platform behavior
- a runtime, backend, or public API guide

The Tsubasa language contract owns semantics. Tobi implements and
operationally enforces that contract.

For issue classification and the exact reproduction checklist, use:

- `docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md`

## Reading Model

There are three main outcomes in the released validator workflow.

### Accepted Authored Source

If authored Tsubasa source is accepted, `canon` produces:

- `CANON:`
- canonical ASCII
- `HASH:`
- current `_h` rendered as hex

Authored source is not assumed to be canonical. The accepted result is produced
through Tsubasa canonicalization in Tobi.

### Rejected Authored Source With Diagnostics

If source is rejected, Tobi returns a diagnostic code, message, and usually a
span.

Practical rule:

- ingress, lexer, or parser rejection means the source was not accepted
- `E100`–`E107` means the source parsed far enough to reach current static-semantics checks

### Conformance / Golden Mismatch

`golden` mismatch is different from source rejection.

It means:

- the fixture expected one result
- the current validator produced another result

Typical mismatch classes include:

- canonical mismatch
- hash mismatch
- error code mismatch
- error message-class mismatch
- error span mismatch

This is a conformance expectation failure, not automatically a parser or
semantic acceptance failure.

## Error-Code Reference

This reference covers the released semantic diagnostic range:

- `E100`
- `E101`
- `E102`
- `E103`
- `E104`
- `E105`
- `E106`
- `E107`

### `E100` — semantic call arity mismatch

- Short meaning:
  - a builtin was called with the wrong number of arguments
- Typical cause:
  - calling `to_dec`, `to_flt`, `__not`, `__and`, `__or`, or comparison/equality forms with too few or too many arguments
- What to check first:
  - the callee name
  - the expected argument count for that builtin
  - whether an optional context argument is the only extra argument in `to_dec` / `to_flt`
- Usual class:
  - callable/use-shape issue

### `E101` — semantic exact-decimal type mismatch

- Short meaning:
  - a strict exact-decimal comparison received the wrong type
- Typical cause:
  - `__lt`, `__le`, `__gt`, or `__ge` received a non-`Dec` value where exact decimal comparison is required
- What to check first:
  - whether both comparison inputs are exact decimals
  - whether you accidentally passed `Bool`, `String`, or another incompatible value
  - whether you expected float-like comparison instead of exact decimal comparison
- Usual class:
  - typing issue

### `E102` — semantic builtin argument type mismatch

- Short meaning:
  - the call shape is valid, but one or more builtin arguments have the wrong type
- Typical cause:
  - boolean builtin received non-boolean input
  - equality operands have incompatible types
  - `to_dec` / `to_flt` optional context argument is not a string
- What to check first:
  - the builtin being called
  - the type of each argument at the reported span
  - whether mixed-type equality or wrong context-argument type was used
- Usual class:
  - typing issue

### `E103` — semantic match arm result type mismatch

- Short meaning:
  - match arms do not return the same result type
- Typical cause:
  - one arm returns a decimal-like result while another returns string, boolean, or another type
- What to check first:
  - each arm result expression
  - whether one arm accidentally returns a different type than the others
- Usual class:
  - typing issue

### `E104` — semantic atomic/effect boundary violation

- Short meaning:
  - an atomic-only or effectful expression was used in the wrong context
- Typical cause:
  - `to_flt(...)` used outside `atomic{...}`
  - effectful expression such as `atomic{...}` or `note ...` used where a pure value is required
- What to check first:
  - whether the operation must be inside `atomic{...}`
  - whether an effectful expression appears in a pure value position
  - the exact span, because it usually points at the boundary violation
- Usual class:
  - atomic/barrier issue

### `E105` — semantic explicit barrier required

- Short meaning:
  - exact decimal comparison requires an explicit barrier conversion
- Typical cause:
  - floatish value from `to_flt(...)` was compared without explicit `to_dec(...)`
- What to check first:
  - whether comparison input came from `to_flt(...)`
  - whether an explicit `to_dec(...)` conversion is missing before exact decimal comparison
- Usual class:
  - atomic/barrier issue

### `E106` — semantic pattern type mismatch

- Short meaning:
  - the pattern does not match the scrutinee type expected by the current validator
- Typical cause:
  - boolean pattern used against a non-boolean scrutinee
- What to check first:
  - the scrutinee type
  - the pattern kind at the reported span
- Usual class:
  - typing issue

### `E107` — semantic call target is not callable

- Short meaning:
  - the current MVP rejected the call target itself
- Typical cause:
  - calling a local value as if it were callable
  - calling a boolean literal as if it were callable
  - using a non-identifier call target in the MVP
- What to check first:
  - the callee expression itself
  - whether the callee is a builtin identifier, unresolved external identifier, or local non-callable value
- Usual class:
  - callable/use-shape issue

## Parser / Validation / Golden Distinction

Keep these failure modes separate.

### Parser / Earlier Validation Rejection

Typical signs:

- codes outside `E100`–`E107`
- malformed source
- invalid token or character
- delimiter or structure problems

Representative examples:

- `E010` unexpected character
- `E021` unclosed delimiter / delimiter-shape failure
- `E023` invalid `let` structure

Meaning:

- source was not accepted by the frontend
- static semantics may not have run

### Semantic Rejection

Typical signs:

- codes `E100`–`E107`
- source parsed, but current semantic checks rejected it

Meaning:

- syntax was accepted far enough to perform current static-semantics checks
- rejection concerns current validator constraints rather than malformed syntax alone

### Golden Mismatch

Typical signs:

- `golden canonical mismatch`
- `golden hash mismatch`
- `golden error code mismatch`
- `golden error message class mismatch`
- `golden exact span mismatch`

Meaning:

- fixture expectation did not match actual validator behavior
- source may still be valid or invalid exactly as designed; the issue is the conformance expectation

## Common Operator Mistakes

### Wrong file path

- `canon` fails because the input path is wrong
- check the path before assuming validator failure

### Wrong fixture path

- `golden` fails because the fixture file does not exist or the wrong fixture corpus was used
- check the exact fixture path first

### Malformed source

- parser/earlier rejection appears before semantic checks
- look for non-`E100`–`E107` codes such as lexer/parser failures

### Semantic rejection

- source parses, then current semantic checks reject it
- use the `E100`–`E107` table before guessing

### Using the wrong fixture corpus

- shipped demo fixtures and project-owned fixtures are not interchangeable unless intended
- confirm which corpus the command was supposed to use

### Reading a `golden` mismatch as “the platform is broken”

- a `golden` mismatch is usually a conformance expectation mismatch
- keep interpretation narrow and validator-first

## What To Capture When Reporting An Issue

Capture exactly:

- exact command
- exact source file or fixture file
- exact output
- exact diagnostic code and span if present
- validator version / release tag

The current technical release tag remains:

- `stage1-tobi-validator-v0.7.0`

That compatibility-sensitive identifier is not the public product name.

Support-quality rule:

- prefer minimal reproducible inputs
- prefer exact fixture files over paraphrases
- identify whether the issue occurred in `canon` or `golden`
- identify whether it concerns docs, diagnostics clarity, fixture mismatch, or workflow friction

## Boundaries

This document does not:

- define Tsubasa semantics
- replace release documentation
- promise runtime behavior
- promise backend/materialization behavior
- promise public verification API behavior
- widen Tobi Validator into a broader platform

`_h` is compatibility identity only. Canonical equality does not establish
factual truth, and validator acceptance is not universal correctness.

Later enhancement, not part of the current diagnostics/reference UX:

- richer diagnostic cookbook by syntax family
- platform-specific onboarding
- API-oriented error-handling guidance
