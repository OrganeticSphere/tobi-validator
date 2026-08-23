# Tobi Validator Install And Usage

Project: Organetic Sphere
Component: Tobi Validator
Descriptor: Reasoning Artifact Validator
Scope: install / usage / output interpretation
Date basis: 2026-08-23

For the shortest first-time path from download to successful `canon` and
`golden` runs, start with:

- `docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md`

The physical filename retains legacy spelling for link stability; the visible
title of that document is **Tobi Validator Quickstart — First 10 Minutes**.

## Install

The current release-family filenames retain their compatibility-sensitive
`stage1-*` identifiers. Do not rename them when following this guide.

First-cut install flow:

1. Obtain the authorized Tobi Validator release bundle for your platform.
2. Verify the bundle against its published `.sha256` sidecar.
3. Unpack the bundle.
4. Keep the extracted directory intact so the shipped examples remain available.
5. Keep the bundle-internal `SHA256SUMS.txt` for local integrity verification.
6. Run `tobi --help` or `tobi.exe --help` from the extracted directory.
7. Optionally add the extracted directory to `PATH`.

For the current Windows x86_64 release family, the technical asset identifiers
remain:

- `stage1-tobi-validator-v0.7.0-windows-x86_64.zip`
- `stage1-tobi-validator-v0.7.0-windows-x86_64.zip.sha256`

Those identifiers are retained for release compatibility and do not represent
the current public product name.

The current `stage1-tobi-validator-v0.7.0` binary help banner retains the
historical lockup `AI Verification Engine / Tobi Validator`. This documentation
migration does not modify the released binary. The active public name for new
product copy is **Tobi Validator**.

## Canon Usage

Example:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
```

This sample is shipped inside the release bundle.

The processing model is:

```text
authored Tsubasa source
→ validation and Tsubasa canonicalization through Tobi
→ canonical ASCII + _h compatibility identity
```

Expected output shape:

- `CANON:` section with canonical ASCII
- `HASH:` section containing the current `_h` value rendered as hex

Authored input is not assumed to be canonical. Tobi implements the Tsubasa
language contract and produces the canonical representation for accepted
source.

## Golden Usage

Example:

```powershell
.\tobi.exe golden .\examples\golden\fixtures.json
```

This fixture file is shipped inside the release bundle.

Expected output shape:

- `OK (<n> fixtures)` on success
- deterministic diagnostic/conformance failure on mismatch

## Output Interpretation

### Canonical ASCII

Canonical ASCII is the stable user-visible representation produced for accepted
Tsubasa source. Equivalent accepted surface forms should converge here.

### `HASH:` Label And `_h`

`HASH:` is the CLI label under which Tobi prints the current `_h` compatibility
identity for the accepted canonical artifact.

`_h` is not a signature, certification, consensus result, or proof of truth.

### Diagnostics

Rejected input produces deterministic diagnostics with stable error codes and
spans under the current validator contract.

## Compatibility And Conformance Note

Tobi Validator is intentionally validator-first. It is intended for
canonicalization, validation, diagnostics, and conformance work.

It is not intended for:

- runtime execution
- backend emission
- public verification API integration
- broader SDK/platform embedding

Validator acceptance is not universal correctness. Canonical equality does not
establish factual truth.

## Non-Goals

Do not infer from this install guide that the product ships:

- backend-entry surface
- runtime
- codegen
- materialization
- public verification API
- the production validator source code

## Where To Go Next

After install and first-run validation:

- use `docs/STAGE1_DIAGNOSTICS_REFERENCE.md` when `canon` or `golden` fails
- use `docs/STAGE1_GITHUB_ACTION_STARTER.md` when GitHub workflow fit matters
