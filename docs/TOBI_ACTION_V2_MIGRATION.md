# Migrate to the Free Tobi Validator GitHub Action

Use `OrganeticSphere/tobi-validator@v2` for the maintained Action line.
The free download path starts with `v2.1.0`.

1. Update older Action references to `OrganeticSphere/tobi-validator@v2`.
2. Remove credential inputs from the Action's `with` block.
3. Remove obsolete validator-access secrets from repository settings.
4. Keep `mode`, input paths, and any archive overrides you need.

No registration, access token, or repository secret is required. The Action
downloads public release binaries and verifies SHA-256 checksums before use.
Exact older releases retain their original implementation; use the maintained
line or pin the `v2.1.0` commit to get the free execution path.

## Minimal Examples

For `canon`:

```yaml
- uses: OrganeticSphere/tobi-validator@v2
  with:
    mode: canon
    canon_input: path/to/artifact.tsubasa
```

For `golden`:

```yaml
- uses: OrganeticSphere/tobi-validator@v2
  with:
    mode: golden
    golden_fixtures: path/to/fixtures.json
```

## Common Boundaries

`_h` is compatibility identity only.

Canonical equality does not establish factual truth.

Validator acceptance is not universal correctness.

The consuming workflow owns merge, release, allow, block, and escalation
policy.

See the [Action version policy](./TOBI_ACTION_VERSION_POLICY.md).
