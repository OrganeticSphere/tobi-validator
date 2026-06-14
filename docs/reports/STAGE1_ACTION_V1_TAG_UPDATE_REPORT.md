# Stage 1 Action v1 Tag Update Report

Repository: `OrganeticSphere/tobi-validator`
Branch used for report: `feature/codex/v1-tag-update-report`
Base branch: `main`
Date: 2026-06-15

## Purpose

Move the public major GitHub Action tag `v1` so users of:

```yaml
uses: OrganeticSphere/tobi-validator@v1
```

receive the merged OS-aware controlled-download Action implementation from PR #1.

Merged PR:

- `https://github.com/OrganeticSphere/tobi-validator/pull/1`

## Main commit used

Verified `main` SHA:

```text
59b5ddb02fe6ba5939b1685b69712ebc1c9f982a
```

This matched `origin/main` after:

```text
git fetch origin main --tags
git checkout main
git pull --ff-only origin main
git rev-parse HEAD
```

## Previous v1 ref

Before the update, fetched local tag metadata showed `v1` was annotated:

```text
85c5078f1aba6bb4134977be52543ac53635256a refs/tags/v1
6134b5e480fa09f47603cd90967ee755d19583b9 refs/tags/v1^{}
```

Remote `refs/tags/v1` before the update:

```text
85c5078f1aba6bb4134977be52543ac53635256a refs/tags/v1
```

No repository policy requiring annotated major tags was found during this update, so `v1` was replaced with a lightweight tag pointing directly at the verified main commit.

## New v1 ref

Commands run:

```text
git tag -f v1 59b5ddb02fe6ba5939b1685b69712ebc1c9f982a
git push origin refs/tags/v1 --force
git ls-remote origin refs/tags/v1
```

Verified remote result:

```text
59b5ddb02fe6ba5939b1685b69712ebc1c9f982a refs/tags/v1
```

Final `v1` SHA:

```text
59b5ddb02fe6ba5939b1685b69712ebc1c9f982a
```

## Main post-tag smoke

Requested `gh` CLI commands were not available because `gh` is not installed in this environment. The equivalent GitHub Actions API workflow dispatch and run polling were used.

Workflow:

```text
action-smoke.yml
```

Ref:

```text
main
```

Run URL:

- `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512782108`

Run result:

```text
success
```

Jobs:

| Job | Result | Job URL |
| --- | --- | --- |
| `ubuntu-latest canon` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512782108/job/81315878599` |
| `ubuntu-latest golden` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512782108/job/81315878630` |
| `windows-latest canon` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512782108/job/81315878606` |
| `windows-latest golden` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512782108/job/81315878611` |

Required job status:

- `ubuntu-latest canon`: passed
- `ubuntu-latest golden`: passed
- `windows-latest canon`: passed
- `windows-latest golden`: passed

## Consumer-style @v1 smoke

Consumer-style smoke was run from a temporary branch using a temporary workflow that referenced:

```yaml
uses: OrganeticSphere/tobi-validator@v1
```

The temporary branch was deleted after the run completed.

Run URL:

- `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512834557`

Run result:

```text
success
```

Jobs:

| Job | Result | Job URL |
| --- | --- | --- |
| `ubuntu-latest canon via v1` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512834557/job/81316029411` |
| `windows-latest golden via v1` | Passed | `https://github.com/OrganeticSphere/tobi-validator/actions/runs/27512834557/job/81316029422` |

The workflow used repository secret:

```text
TOBI_DIST_TOKEN
```

No token values were hardcoded.

## Not run

- `gh workflow run action-smoke.yml --ref main`
- `gh run list --workflow action-smoke.yml --branch main --limit 5`
- `gh run watch <RUN_ID>`
- macOS smoke
- `eval_token` broker smoke
- explicit `archive_name` / `archive_sha256_name` override smoke

The `gh` commands were not run because `gh` was not installed. The GitHub Actions API was used instead for dispatching and polling.

## Boundary confirmation

No Action logic was changed as part of this v1 tag update report.

This update did not add or change:

- `validate`
- `canon` behavior
- `golden` behavior
- `eval_token`
- `dist_token`
- source/build repository visibility
- private distribution architecture
- source/build internals
- GitLab work

Controlled delivery remains token-gated:

- the Action still requires `eval_token` or `dist_token`
- `dist_repo` remains `OrganeticSphere/tobi-validator-dist`
- no unrestricted public binary delivery path was introduced
