# Tobi Validator

**Reasoning Artifact Validator**

> Deterministic validation for canonical reasoning artifacts.

Tobi Validator deterministically validates and canonicalizes Tsubasa reasoning
artifacts for use at workflow boundaries.

The public authoring and validation model is:

```text
authored Tsubasa source
→ validation and Tsubasa canonicalization through Tobi
→ canonical ASCII + _h compatibility identity
```

or, for rejected input:

```text
authored Tsubasa source
→ validation through Tobi
→ deterministic diagnostics
```

Authored source is not assumed to be canonical. The Tsubasa language contract
defines the semantic and canonical rules; Tobi is the reference validator that
implements and operationally enforces that contract.

This repository is the public GitHub entry surface for Tobi Validator. It
provides:

- public documentation
- shipped examples
- GitHub workflow adoption guidance
- diagnostics and support guidance
- workflow-fit and issue intake
- the public Tobi Validator GitHub Action wrapper

It is a public documentation and adoption repository.

It is **not** the full development source repository.

The Action runs freely without registration or repository secrets. Released
validator binaries and SHA-256 sidecars are available in this repository's
[GitHub Releases](https://github.com/OrganeticSphere/tobi-validator/releases/tag/stage1-tobi-validator-v0.7.0).

---

## Released Tobi Validator Surface

The released surface is intentionally narrow:

- installable `tobi` CLI
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and install / usage framing

Tobi Validator should not be read as:

- a runtime / backend product
- a public verification API
- a platform SDK
- a theorem prover or universal truth engine
- a broader Organetic platform release

`_h` is compatibility identity only. Canonical equality does not establish
factual truth, and validator acceptance is not universal correctness.

---

## Start Here

For the shortest public path:

- [Tobi Validator Quickstart](./docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md)
- [Finding Your First Reasoning Artifacts](./docs/FINDING_YOUR_FIRST_REASONING_ARTIFACTS.md)
- [Agent Workflow Governance vs Reasoning Verification](./docs/AGENT_WORKFLOW_GOVERNANCE_VS_REASONING_VERIFICATION.md)
- [Tsubasa Public Syntax and Authoring Reference](./docs/TSUBASA_STAGE1_PUBLIC_SYNTAX_AND_AUTHORING_REFERENCE.md)
- [Tsubasa Conformance Corpus](./docs/OPEN_CONFORMANCE_CORPUS.md)
- [Tobi Validator Install and Usage](./docs/STAGE1_INSTALL_AND_USAGE.md)
- [Tobi Validator Diagnostics Reference](./docs/STAGE1_DIAGNOSTICS_REFERENCE.md)
- [Tobi Validator Support and Issue Reporting](./docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md)
- [Tobi Validator GitHub Action Starter](./docs/STAGE1_GITHUB_ACTION_STARTER.md)

The public syntax-and-authoring document above is an interim reference for the
current released validator corridor. It does not replace the forthcoming
complete **Tsubasa Language Reference** book.

The physical filenames above retain legacy `STAGE1` spelling for link stability.
Their visible titles and current product language follow the active Tobi public
naming contract.

Representative command shapes:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

```sh
./tobi canon ./examples/sample.tsubasa
./tobi golden ./examples/golden/fixtures.json
```

---

### Tsubasa Conformance Corpus

The public Tsubasa Conformance Corpus is available at
[OrganeticSphere/tsubasa-stage1-conformance](https://github.com/OrganeticSphere/tsubasa-stage1-conformance).
The repository slug is retained for link stability. The corpus provides
public-safe `.tsubasa` examples, manifest records, verified canonical outputs,
diagnostics, and coverage limitations. It makes observable Tobi Validator
behavior more inspectable without publishing the private validator
implementation.

Read the local overview in
[Tsubasa Conformance Corpus](./docs/OPEN_CONFORMANCE_CORPUS.md), or inspect the
public corpus
[manifest](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json),
[verification report](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md),
and
[coverage limitations](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/COVERAGE_LIMITATIONS.md).

The public corpus can be reviewed independently and checked with the freely
available Tobi Validator GitHub Action or public release binaries.

---

### Validator-Backed Example Repository

See the first public flagship validator-first demo repository:

- [Tobi Flagship Use Case — AI-Agent Reasoning Gate](https://github.com/OrganeticSphere/tobi-flagship-use-case)

This repository shows:

- a valid `.tsubasa` artifact
- a surface-different accepted variant with the same recorded canonical result
- a malformed reject sibling
- a GitHub workflow that uses Tobi Validator results as a pull-request check

## Tobi Validator GitHub Action

This repository exposes the public Tobi Validator GitHub Action wrapper.

The Action is free to run in public and private repositories, including fork
pull requests. No registration, access token, or repository secret is required.

- the public Action wrapper lives here
- binaries are downloaded directly from this repository's public GitHub Releases
- SHA-256 checksums are verified before extraction
- the Action selects the archive for the runner OS and architecture

The Action exposes validator success or failure to GitHub. The consuming
workflow owns any merge, release, allow, block, or escalation policy.

Supported runner families:

- Windows x86_64
- Linux x86_64
- macOS arm64
- macOS x86_64

Current Action modes:

- `canon`
- `golden`

No `validate` mode is shipped.

### Setup

Check out your repository and run `OrganeticSphere/tobi-validator@v2` with
`mode` and the input path. No secret setup is needed.

### Minimal Linux `canon` Example

```yaml
name: Tobi Canon

on:
  workflow_dispatch:
  pull_request:

jobs:
  canon:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: OrganeticSphere/tobi-validator@v2
        with:
          mode: canon
          canon_input: path/to/artifact.tsubasa
```

### Minimal Windows `golden` Example

```yaml
name: Tobi Golden

on:
  workflow_dispatch:
  pull_request:

jobs:
  golden:
    runs-on: windows-latest

    steps:
      - uses: actions/checkout@v4

      - uses: OrganeticSphere/tobi-validator@v2
        with:
          mode: golden
          golden_fixtures: path/to/fixtures.json
```

### Current `v2` Reading

Action `v2` is intentionally narrow:

- `canon` mode
- `golden` mode
- free execution without repository secrets
- public GitHub Release downloads
- checksum verification before extraction
- OS-aware archive selection for Windows, Linux, and macOS
- no runtime, backend, public API, or platform claims

See the [Action version policy](./docs/TOBI_ACTION_VERSION_POLICY.md) and
[v2 migration guide](./docs/TOBI_ACTION_V2_MIGRATION.md) for the supported line
and legacy migration boundaries.

---

## What This Repository Contains

This repository contains:

- public Tobi Validator documentation
- shipped examples
- GitHub workflow starter materials
- support and diagnostics guidance
- public workflow-fit and issue-intake paths
- the public Action wrapper surface

This repository does **not** contain:

- the full private development source tree
- internal product-boundary notes
- internal launch-control documents
- the production Tobi implementation

---

## GitHub-First Public Path

The current public adoption path is GitHub-first:

- product understanding
- documentation
- shipped examples
- a narrow workflow path around the released validator CLI
- a public Action wrapper with free execution and public binary downloads

Use the examples to check workflow fit, then point the Action at your own
Tsubasa artifacts. Public release downloads support local CLI use as well.

---

## Support

For failure interpretation and issue reporting, start with:

- [Tobi Validator Diagnostics Reference](./docs/STAGE1_DIAGNOSTICS_REFERENCE.md)
- [Tobi Validator Support and Issue Reporting](./docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md)

Please keep reports exact and reproducible.

---

## Contact

- Website: https://organetic.ai
- support@organetic.ai

---

## Current Bottom Line

This repository is the public GitHub entry surface for Tobi Validator.

In short:

- product: **Tobi Validator**
- descriptor: **Reasoning Artifact Validator**
- category line: **Deterministic validation for canonical reasoning artifacts.**
- public path: **GitHub-first**
- current surface: **narrow validator-first CLI + GitHub Action wrapper**
- this repository: **docs + examples + workflow guidance + Action wrapper + issue intake**
- execution: **free GitHub Action + public release binaries**

[![Telegram Channel](https://img.shields.io/badge/Telegram-Join_Organetic-blue?logo=telegram&logoColor=white)](https://t.me/+wKVUzIlax44yYjhi)
[![X Profile](https://img.shields.io/badge/X-Follow_Organetic-black?logo=x&logoColor=white)](https://x.com/OrganeticSphere)
