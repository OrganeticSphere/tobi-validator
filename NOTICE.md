# NOTICE

This repository is the public GitHub entry and adoption surface for:

**Tobi Validator**
**Reasoning Artifact Validator**

> Deterministic validation for canonical reasoning artifacts.

It exists to provide:

- public documentation
- shipped examples
- GitHub workflow adoption materials
- diagnostics and support guidance
- the public Tobi Validator GitHub Action wrapper

The Action wrapper is public. Validator delivery is controlled and separate:
evaluation users present `TOBI_EVAL_TOKEN`, and Organetic's evaluation broker
provides the requested release assets under the current controlled-access
policy.

This repository is **not**:

- the full private development source repository
- an unrestricted public binary-distribution channel
- the production Tobi implementation
- a public verification API
- a broader platform, runtime, backend, or SDK release surface

The released Tobi Validator surface remains intentionally narrow:

- installable `tobi` CLI
- authored Tsubasa source validation
- Tsubasa canonicalization through Tobi
- canonical ASCII output for accepted source
- current `_h` compatibility identity
- deterministic diagnostics for rejected source
- `golden` conformance execution
- thin packaging and install / usage framing

`_h` is compatibility identity only. Canonical equality does not establish
factual truth, and validator acceptance is not universal correctness.

If you are looking for the public product entry, start with:

- `README.md`
- `docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md`
- `docs/STAGE1_INSTALL_AND_USAGE.md`
- `docs/STAGE1_GITHUB_ACTION_STARTER.md`

The legacy `STAGE1` spelling in those physical filenames is retained for link
stability. Their visible titles and current product language use Tobi Validator.

In short, this repository is the public documentation, Action-wrapper, and
adoption surface for Tobi Validator. Controlled validator delivery remains
separate from unrestricted public repository access.
