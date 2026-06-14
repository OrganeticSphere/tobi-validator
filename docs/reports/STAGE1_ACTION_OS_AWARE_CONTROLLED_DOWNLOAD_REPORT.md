# Stage 1 Action OS-Aware Controlled Download Report

Repository: `OrganeticSphere/tobi-validator`  
Branch: `feature/assistant/os-aware-controlled-download`  
Base branch: `main`  
Scope: public GitHub Action wrapper only

## Purpose

Update the public GitHub Action wrapper so it no longer defaults to the Windows-only Stage 1 validator archive on Linux and macOS runners.

The source/build repository remains private. The private distribution repository remains `OrganeticSphere/tobi-validator-dist`.

## Previous behavior

The Action accepted `eval_token`, `dist_token`, `version`, `dist_repo`, `archive_name`, and `archive_sha256_name`.

However, the default archive names were Windows-only:

- `stage1-tobi-validator-v0.7.0-windows-x86_64.zip`
- `stage1-tobi-validator-v0.7.0-windows-x86_64.zip.sha256`

Extraction used `Expand-Archive`, and executable discovery searched only for `tobi.exe`.

## New behavior

When `archive_name` is omitted, the Action infers the release archive from runner OS and architecture.

Mapping:

| Runner OS | Runner arch | Archive |
| --- | --- | --- |
| Windows | X64 | `stage1-tobi-validator-v0.7.0-windows-x86_64.zip` |
| Linux | X64 | `stage1-tobi-validator-v0.7.0-linux-x86_64.tar.gz` |
| macOS | ARM64 | `stage1-tobi-validator-v0.7.0-macos-arm64.tar.gz` |
| macOS | X64 | `stage1-tobi-validator-v0.7.0-macos-x86_64.tar.gz` |

When `archive_sha256_name` is omitted, the Action resolves it as:

```text
<archive_name>.sha256
```

Explicit `archive_name` and `archive_sha256_name` overrides remain supported.

## Controlled delivery preserved

The Action still requires either:

- `eval_token`, or
- `dist_token`

The default private distribution repository remains:

```text
OrganeticSphere/tobi-validator-dist
```

No public source/build repository assumption was introduced.

## Extraction and executable resolution

Supported archive formats:

- `.zip`
- `.tar.gz`

Executable resolution:

- Windows: `tobi.exe`
- Linux/macOS: `tobi`

Linux/macOS executables are marked executable with `chmod +x` after extraction.

## CLI surface

Allowed Action modes remain:

- `canon`
- `golden`

No `validate` command or mode was added.

## Files changed

- `action.yml`
- `README.md`
- `docs/STAGE1_GITHUB_ACTION_STARTER.md`
- `examples/github-actions/stage1_tobi_validator_example.yml`
- `docs/reports/STAGE1_ACTION_OS_AWARE_CONTROLLED_DOWNLOAD_REPORT.md`

## Validation performed by inspection

Verified in patch content:

- Action keeps `eval_token`
- Action keeps `dist_token`
- Action keeps `dist_repo`
- Action keeps `version`
- Action verifies SHA256 before extraction
- Action supports `.zip` and `.tar.gz`
- Action resolves `tobi.exe` on Windows and `tobi` on Linux/macOS
- Action still only dispatches `canon` and `golden`
- README does not claim public source/build publication
- README preserves controlled binary delivery framing

## Not run

The following require repository-side workflow execution and/or secrets and were not run through this connector-only edit:

- GitHub Actions smoke workflow with `TOBI_DIST_TOKEN`
- `ubuntu-latest` action smoke
- `windows-latest` action smoke
- `macos-latest` action smoke
- evaluation broker path smoke with `eval_token`

An attempt to add a repository smoke workflow using a repository secret was blocked by the available tooling safety layer. That workflow should be added or executed by a local agent with repository workflow-writing capability.

## Product and security boundary confirmation

This change does not add or expose:

- source code
- compiler internals
- build logic
- backend/runtime/WASM claims
- public verification API claims
- Stage 2 claims
- receipt/bundle/suite/outcome-trace schema
- `.tobi-sync` protocol
- `validate` command
