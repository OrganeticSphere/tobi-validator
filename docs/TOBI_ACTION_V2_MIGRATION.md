# Migrate to Tobi Validator GitHub Action v2

## Current Floating `@v1` User

A current floating-line integration may look like this:

```yaml
- uses: OrganeticSphere/tobi-validator@v1
  with:
    eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
    mode: canon
```

Change only the Action reference:

```yaml
- uses: OrganeticSphere/tobi-validator@v2
  with:
    eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
    mode: canon
```

For this consumer class, the token input, secret name, mode, and default
validator release identifier do not change. The Action reference changes to the
maintained `v2` line.

## Exact `@v1.0.0` User

The exact historical release used an earlier contract that may include the
`dist_token` input. To migrate:

1. Obtain approved Organetic evaluation access.
2. Store the issued token in the repository secret `TOBI_EVAL_TOKEN`.
3. Change the Action reference to `OrganeticSphere/tobi-validator@v2`.
4. Pass the secret through the required `eval_token` input.
5. Remove direct-distribution credential configuration.
6. Preserve `canon` and/or `golden` usage as applicable.

Do not expose private repository credentials. `dist_token` is not a hidden
compatibility input in `v2`.

## Minimal Examples

For `canon`:

```yaml
- uses: OrganeticSphere/tobi-validator@v2
  with:
    eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
    mode: canon
    canon_input: path/to/artifact.tsubasa
```

For `golden`:

```yaml
- uses: OrganeticSphere/tobi-validator@v2
  with:
    eval_token: ${{ secrets.TOBI_EVAL_TOKEN }}
    mode: golden
    golden_fixtures: path/to/fixtures.json
```

## Common Boundaries

`_h` is compatibility identity only.

Canonical equality does not establish factual truth.

Validator acceptance is not universal correctness.

The consuming workflow owns merge, release, allow, block, and escalation
policy.

See the [Action version policy](./TOBI_ACTION_VERSION_POLICY.md) for the
supported and legacy release lines.
