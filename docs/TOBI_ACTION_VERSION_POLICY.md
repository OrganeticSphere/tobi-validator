# Tobi Validator GitHub Action Version Policy

## Supported Line

Current supported Action major:

`v2`

Current integration reference:

`OrganeticSphere/tobi-validator@v2`

First v2 release:

`v2.0.0`

The floating `v2` reference is the maintained integration line after the first
v2 release is published.

## Legacy Line

`v1.0.0` is the legacy exact Marketplace release. The floating `v1` reference
is a frozen transitional line. Movement or deletion of `v1` is not planned.

Existing workflows are not automatically rewritten. Consumers must select the
version appropriate to their integration and migrate explicitly.

## Compatibility Boundary

The exact `v1.0.0` release used an earlier credential and distribution
contract. Action `v2` uses controlled evaluation access through the required
`eval_token` input and the public `TOBI_EVAL_TOKEN` secret convention. This is
a new major because the public Action contract and security boundary changed.

The version-line change does not alter the validator contract:

- `v2` does not change Tsubasa semantics.
- `v2` does not change Tobi canonicalization.
- `v2` does not change `_h`; `_h` remains compatibility identity only.
- `v2` does not change the default validator release identifier,
  `stage1-tobi-validator-v0.7.0`.
- `v2` continues to expose only `canon` and `golden`; it does not add a
  `validate` mode.
- `v2` does not create a public verification API.
- `v2` does not expose the production validator implementation.

For consumer changes, see the [v2 migration guide](./TOBI_ACTION_V2_MIGRATION.md).
