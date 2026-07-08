# Open Stage 1 Conformance Corpus

The public Stage 1 conformance corpus makes Stage 1 Tobi Validator behavior
more inspectable without publishing the private validator engine or core.

Repository:

- https://github.com/OrganeticSphere/tsubasa-stage1-conformance

The repository is a public Stage 1 `.tsubasa` conformance corpus. It contains
public-safe source examples, manifest records, expected canonical outputs,
diagnostics, and verification evidence.

Expected outputs in the corpus are based on real Tobi Validator runs, not
invented documentation values. The current v0.1 corpus is a verified seed
corpus, not full Tsubasa language coverage.

Useful public entry points:

- [manifest.v0.1.json](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json)
- [Tobi run verification evidence](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md)
- [Coverage limitations](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/COVERAGE_LIMITATIONS.md)

## Current v0.1 Status

The current v0.1 public corpus contains:

- 12 public cases
- 11 cases verified with real Tobi Validator v0.7.0
- 1 idempotence case pending

Idempotence is not claimed as verified in v0.1. Any final idempotence statement
must come from a real Tobi Validator run.

The `_h` field is optional. When present, it is a version-bound compatibility
identity only; it is not a proof of truth, certification, or universal
acceptance.

The validator implementation, private source, private binary distribution, and
private golden corpus remain private.

Users who have authorized Tobi Validator access can run the public examples
themselves. Users without authorized execution can still inspect the source
cases, manifest records, expected-output records, coverage limitations, and
public/private boundary docs.

## How This Relates To This Repository

`OrganeticSphere/tobi-validator` provides the public GitHub Action, adoption
wrapper, and usage docs for the released Stage 1 validator line.

`OrganeticSphere/tsubasa-stage1-conformance` provides the open Stage 1 public
conformance corpus.

Authorized Tobi Validator execution remains controlled through eval access or
authorized distribution.

## What This Does Not Mean

The public conformance corpus does not make Tobi Validator open source.

It does not publish the private engine or core.

It does not provide unrestricted binary distribution.

It does not claim full Tsubasa language coverage.

It does not ship Stage 2.

It does not make `_h` a proof of truth.
