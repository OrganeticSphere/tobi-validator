# Tsubasa Conformance Corpus

The public Tsubasa Conformance Corpus makes observable Tobi Validator behavior
more inspectable without publishing the private validator implementation.

Repository:

- https://github.com/OrganeticSphere/tsubasa-stage1-conformance

The repository slug retains legacy `stage1` spelling for link stability. The
current public display name is **Tsubasa Conformance Corpus**.

The corpus contains public-safe `.tsubasa` source examples, manifest records,
expected canonical outputs, diagnostics, and verification evidence.

Expected outputs are based on real Tobi Validator runs, not invented
documentation values. The current v0.1 corpus is a verified seed corpus, not
full Tsubasa language coverage.

Useful entry points:

- [manifest.v0.1.json](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json)
- [Tobi run verification evidence](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md)
- [Coverage limitations](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/COVERAGE_LIMITATIONS.md)

## Current v0.1 Status

The current public corpus contains:

- 12 public cases
- 11 cases verified with real Tobi Validator v0.7.0
- 1 idempotence case pending

Idempotence is not claimed as verified in v0.1. Any final idempotence statement
must come from a real Tobi Validator run.

The `_h` field is optional. When present, it is a version-bound compatibility
identity only; it is not proof of truth, certification, signature, consensus,
or universal acceptance.

The validator implementation, private source, and private golden corpus remain
private. Everyone can run the public examples with the free GitHub Action or
public release binaries, and inspect the source cases, manifest records,
expected outputs, and coverage limitations.

## Source And Canonical Result

Corpus inputs are authored Tsubasa source. They are not assumed to be canonical.

```text
authored Tsubasa source
→ validation and Tsubasa canonicalization through Tobi
→ canonical output + optional _h
```

Rejected source produces deterministic diagnostics instead.

The Tsubasa language contract owns semantics and canonical rules. Tobi is the
reference validator that implements them.

## Relationship To This Repository

`OrganeticSphere/tobi-validator` provides the public Tobi Validator GitHub
Action wrapper, adoption materials, and usage documentation.

`OrganeticSphere/tsubasa-stage1-conformance` provides the public Tsubasa
Conformance Corpus. Its slug remains unchanged in this migration.

Tobi Validator execution is freely available through the public GitHub Action
and public GitHub Releases. No registration or repository secrets are needed.

## What This Does Not Mean

The public corpus does not:

- make Tobi Validator open source
- publish the private engine or core
- claim full Tsubasa language coverage
- ship a future Organetic consensus product
- make `_h` proof of truth
- establish validator acceptance as universal correctness
