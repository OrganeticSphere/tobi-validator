# Tobi Validator GitHub Action Version Policy

## Supported Line

Current supported Action major: `v2`.

Current integration reference: `OrganeticSphere/tobi-validator@v2`.

The free public-download path starts with `v2.1.0`. It requires no registration,
access token, or repository secret. The floating `v2` tag tracks the maintained
line. Pin an exact release commit when reproducibility requires it.

## Historical Releases

Exact older releases and the frozen `v1` line retain their original code.
They do not provide the current free-download contract. Migrate consumers to
`v2` or the `v2.1.0` commit. Historical tags are not rewritten.

## Compatibility Boundary

The delivery change does not change Tsubasa semantics or Tobi canonicalization.
`_h` remains compatibility identity only. The default validator release remains
`stage1-tobi-validator-v0.7.0`.

The Action exposes only `canon` and `golden`, with checksum verification before
extraction. It does not add a `validate` mode, create a public verification API,
or expose the production validator implementation.

See the [migration guide](./TOBI_ACTION_V2_MIGRATION.md).
