# Stage 1 Action OS-Aware Controlled Download Report

Repository: `OrganeticSphere/tobi-validator`  
Branch: `feature/assistant/os-aware-controlled-download`  
Base branch: `main`  
Scope: public GitHub Action wrapper only

## Purpose

Update and validate the public GitHub Action wrapper so Stage 1 validator delivery is OS-aware while preserving controlled access.

The source/build repository remains private. The private distribution repository remains `OrganeticSphere/tobi-validator-dist`.

## Final behavior

When `archive_name` is omitted, the Action infers the controlled release bundle from runner OS and architecture.

| Runner OS | Runner arch | Release asset |
| --- | --- | --- |
| Windows | X64 | `windows-x86_64-release-archive.zip` |
| Linux | X64 | `linux-x86_64-release-archive.zip` |
| macOS | ARM64 | `macos-arm64-release-archive.zip` |
| macOS | X64 | `macos-x86_64-release-archive.zip` |

Explicit `archive_name` overrides remain supported.

When `archive_sha256_name` is omitted, the Action still resolves the sidecar name as:

```text
<archive_name>.sha256
```

Explicit `archive_sha256_name` overrides remain supported. For direct `dist_token` release downloads, the Action also supports GitHub release asset `sha256:` digest metadata when the release asset exists but no separate sidecar asset exists.

## Controlled delivery preserved

The Action still requires either:

- `eval_token`, or
- `dist_token`

The default private distribution repository remains:

```text
OrganeticSphere/tobi-validator-dist
```

No public source/build repository assumption was introduced.

## Checksum and extraction behavior

Checksum verification still runs before extraction.

For direct `dist_token` downloads:

1. The downloaded controlled release bundle is verified with the GitHub release asset `sha256:` digest when no sidecar asset is present.
2. If the controlled bundle contains a nested platform archive and `.sha256` sidecar, the nested archive is verified before nested extraction.
3. Only after checksum verification does the Action extract the archive that contains the executable.

Supported extraction formats:

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

## Smoke workflow

Added:

- `.github/workflows/action-smoke.yml`

Final workflow trigger:

- `workflow_dispatch`

Smoke cases:

- `canon` against `examples/sample.tsubasa`
- `golden` against `examples/golden/fixtures.json`

The workflow uses the local PR-branch action:

```yaml
uses: ./
```

The workflow uses repository secret:

```text
TOBI_DIST_TOKEN
```

No token value is hardcoded.

## GitHub Actions smoke result

Run URL:

- `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503508045`

Run event:

- `push`

Run head SHA:

- `a83166f2c44b435c518da7a1fd18ffc7ecaa6c60`

Pre-merge execution note:

- Direct `workflow_dispatch` through the GitHub API returned `404` while the new workflow existed only on the PR branch and not on the default branch.
- A branch-scoped `push` trigger was used during validation to execute the new workflow before merge.
- The final workflow file is left as `workflow_dispatch`.

Jobs run:

| Job | Status | Job URL |
| --- | --- | --- |
| `ubuntu-latest canon` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503508045/job/81290515331` |
| `ubuntu-latest golden` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503508045/job/81290515321` |
| `windows-latest canon` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503508045/job/81290515330` |
| `windows-latest golden` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503508045/job/81290515355` |

Required passing jobs:

- `ubuntu-latest canon`: passed
- `ubuntu-latest golden`: passed
- `windows-latest canon`: passed
- `windows-latest golden`: passed

## Fixes made after smoke failures

Initial smoke run:

- `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503247987`
- Result: failed
- Cause: inferred asset names did not match the current private distribution release assets.

Second smoke run:

- `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27503398720`
- Result: failed
- Cause: release assets were controlled outer bundles containing nested platform archives; the Action extracted only the outer bundle and then could not find `tobi.exe` / `tobi`.

Fixes:

- Updated default OS/arch mapping to the current controlled release bundle asset names.
- Preserved explicit `archive_name` and `archive_sha256_name` overrides.
- Added direct-release checksum support through GitHub release asset `sha256:` digest metadata when no sidecar asset is present.
- Added nested platform archive detection.
- Added nested `.sha256` verification before extracting nested platform archives.
- Kept `.zip` extraction support.
- Kept `.tar.gz` extraction support.
- Kept Windows `tobi.exe` and Linux/macOS `tobi` executable resolution.

## Not run

- `macos-latest canon`
- `macos-latest golden`
- evaluation broker smoke with `eval_token`
- explicit `archive_name` / `archive_sha256_name` override runtime smoke

## Validation by inspection

Verified in `action.yml`:

- Composite action syntax remains `runs.using: composite`.
- All composite `run` steps use `shell: pwsh`.
- `RUNNER_OS` values handled: `Windows`, `Linux`, `macOS`.
- `RUNNER_ARCH` values handled for supported releases: `X64`, plus macOS `ARM64`.
- Windows `.zip` extraction path is present and passed smoke.
- Linux `.tar.gz` nested extraction path is present and passed smoke.
- `.zip` nested extraction path is present and passed Windows smoke.
- `tobi.exe` resolution passed Windows smoke.
- `tobi` resolution passed Ubuntu smoke.
- Checksum verification runs before outer extraction and before nested payload extraction.
- `eval_token` downloads use the resolved archive and checksum sidecar names.
- `dist_token` downloads use the resolved archive name and either the resolved checksum sidecar or GitHub release asset digest metadata.
- Explicit archive and checksum-name overrides remain wired through the same inputs.

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

Controlled delivery remains intact:

- The Action still requires `eval_token` or `dist_token`.
- The default distribution repository remains private.
- No unrestricted public binary delivery path was introduced.
