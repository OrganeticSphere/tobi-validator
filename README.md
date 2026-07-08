# Tobi Validator

Public GitHub entry surface for the released Stage 1 product line of Organetic:

**AI Verification Engine / Tobi Validator**

This repository provides the public GitHub entry for:

- public documentation
- shipped examples
- GitHub workflow adoption guidance
- diagnostics and support guidance
- workflow-fit and issue intake
- the public GitHub Action wrapper for the released Stage 1 validator line

It is a public documentation and adoption repository.

It is **not** the full development source repository.

It is also **not** an unrestricted public binary distribution channel for the full Stage 1 product surface.

---

## Released Stage 1 Surface

The current released Stage 1 surface is intentionally narrow:

- installable `tobi` CLI
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and install / usage framing

Stage 1 should not be read as:

- a runtime / backend product
- a verification API
- a platform SDK
- a broader Organetic platform release

---

## Start Here

For the shortest public path:

- [Stage 1 Quickstart](./docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md)
- [Finding Your First Reasoning Artifacts](./docs/FINDING_YOUR_FIRST_REASONING_ARTIFACTS.md)
- [Agent workflow governance vs reasoning verification](./docs/AGENT_WORKFLOW_GOVERNANCE_VS_REASONING_VERIFICATION.md)
- [Tsubasa Stage 1 Public Syntax And Authoring Reference](./docs/TSUBASA_STAGE1_PUBLIC_SYNTAX_AND_AUTHORING_REFERENCE.md)
- [Open Stage 1 Conformance Corpus](./docs/OPEN_CONFORMANCE_CORPUS.md)
- [Stage 1 Install And Usage](./docs/STAGE1_INSTALL_AND_USAGE.md)
- [Stage 1 Diagnostics Reference](./docs/STAGE1_DIAGNOSTICS_REFERENCE.md)
- [Stage 1 Support And Issue Reporting](./docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md)
- [Stage 1 GitHub Action Starter](./docs/STAGE1_GITHUB_ACTION_STARTER.md)

Representative command shapes for the released validator line:

```powershell
.\tobi.exe canon .\examples\sample.tsubasa
.\tobi.exe golden .\examples\golden\fixtures.json
```

```sh
./tobi canon ./examples/sample.tsubasa
./tobi golden ./examples/golden/fixtures.json
```

---

### Open Stage 1 conformance corpus

The public Stage 1 conformance corpus for Tsubasa artifacts is available at
[OrganeticSphere/tsubasa-stage1-conformance](https://github.com/OrganeticSphere/tsubasa-stage1-conformance).
It provides public-safe `.tsubasa` examples, manifest records, verified
canonical outputs, diagnostics, and coverage limitations. The corpus makes
Stage 1 validator behavior inspectable without publishing the private Tobi
Validator implementation.

Read the local overview in
[Open Stage 1 Conformance Corpus](./docs/OPEN_CONFORMANCE_CORPUS.md), or inspect
the public corpus
[manifest](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/corpus/manifest.v0.1.json),
[verification report](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/verification/TOBI_RUNS_v0.1.md),
and
[coverage limitations](https://github.com/OrganeticSphere/tsubasa-stage1-conformance/blob/master/docs/COVERAGE_LIMITATIONS.md).

The public corpus can be reviewed independently. Running the validator still
requires authorized Tobi Validator access through the
[evaluation access path](https://organetic.ai/eval-access) or controlled
distribution access. It should not be read as free unrestricted validator
execution.

---

### Proof-by-example repository

See the first public flagship validator-first demo repository:

- [Tobi Flagship Use Case — AI-Agent Reasoning Gate](https://github.com/OrganeticSphere/tobi-flagship-use-case)

This repo shows:
- a valid `.tsubasa` artifact,
- a drift-equivalent convergent variant,
- a malformed reject sibling,
- a GitHub PR gate around the released Stage 1 validator line.

## GitHub Action

This repository exposes the public GitHub Action wrapper for the released Stage 1 validator line.

The wrapper is public.

The binary delivery path is controlled and separate.

That means:

- the public action wrapper lives here
- the private binary artifact is delivered from `OrganeticSphere/tobi-validator-dist`
- public onboarding uses `TOBI_EVAL_TOKEN`
- internal/manual fallback may still use `dist_token`
- the action infers the release archive from the runner OS and architecture when no explicit archive override is provided

Supported runner families for the controlled binary line:

- Windows x86_64
- Linux x86_64
- macOS arm64
- macOS x86_64

Shipped Action modes:

- `canon`
- `golden`

No `validate` mode is shipped.

### Required Secret

For public evaluation access, create a repository secret in the consuming GitHub repository:

- `TOBI_EVAL_TOKEN`

That secret should be the 7-day evaluation token issued by Organetic through the evaluation access path.

https://organetic.ai/eval-access

For controlled private distribution access, internal users may use:

- `TOBI_DIST_TOKEN`

That token must have read access to the private `OrganeticSphere/tobi-validator-dist` repository.

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

      - uses: OrganeticSphere/tobi-validator@v1
        with:
          eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
          mode: canon
          canon_input: examples/sample.tsubasa
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

      - uses: OrganeticSphere/tobi-validator@v1
        with:
          eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
          mode: golden
          golden_fixtures: examples/golden/fixtures.json
```

### Controlled Distribution Example

```yaml
name: Tobi Canon With Private Distribution Token

on:
  workflow_dispatch:

jobs:
  canon:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: OrganeticSphere/tobi-validator@v1
        with:
          dist_token: ${{ secrets.TOBI_DIST_TOKEN }}
          mode: canon
          canon_input: examples/sample.tsubasa
```

### Current v1 Reading

Action v1 is intentionally narrow:

- `canon` mode
- `golden` mode
- evaluation-token access path for public onboarding
- private distribution-token fallback for controlled access
- checksum verification required before extraction
- OS-aware archive selection for Windows, Linux, and macOS
- no runtime/backend/API/platform claims

---

## What This Repository Contains

This repository contains:

- public Stage 1 documentation
- shipped examples
- GitHub workflow starter materials
- support and diagnostics guidance
- public workflow-fit and issue intake paths
- the public action wrapper surface

This repository does **not** contain:

- the full private development source tree
- internal product-boundary notes
- internal launch-control documents
- unrestricted public full-binary distribution for the complete Stage 1 product path

---

## GitHub-First Public Path

The current public launch motion is GitHub-first:

- product understanding
- documentation
- shipped examples
- a narrow GitHub workflow understanding path around the released validator CLI
- a public action wrapper with controlled binary access

The public repository is meant to help users understand the released Stage 1 line and discuss workflow fit.

It should not be read as a promise that the full production usage path is available through unrestricted public binary download.

---

## Support

If you need help interpreting the current Stage 1 surface, start with:

- [Stage 1 Diagnostics Reference](./docs/STAGE1_DIAGNOSTICS_REFERENCE.md)
- [Stage 1 Support And Issue Reporting](./docs/STAGE1_SUPPORT_AND_ISSUE_REPORTING.md)

Please keep reports exact and reproducible.

---

## Contact

- Website: https://organetic.ai
- support@organetic.ai

---

## Current Bottom Line

This repository is the public GitHub entry surface for the released Stage 1 line of Organetic.

In short:

- released product: **AI Verification Engine / Tobi Validator**
- current public path: **GitHub-first**
- current shipped surface: **narrow validator-first CLI**
- this repo: **docs + examples + workflow guidance + action wrapper + issue intake**
- full controlled product delivery: **separate from unrestricted public repo access**

[![Telegram Channel](https://img.shields.io/badge/Telegram-Join_Organetic-blue?logo=telegram&logoColor=white)](https://t.me/+wKVUzIlax44yYjhi)
