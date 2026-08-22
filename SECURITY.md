# SECURITY

## Security reporting

If you believe you have found a security-sensitive issue related to Tobi
Validator, do not open a public issue when disclosure would create unnecessary
risk.

Instead, report it privately through the project contact path.

Current private reporting path:

- security / product contact: support@organetic.ai

## What to include

Please include:

- exact product version or release tag
- operating system / environment
- exact command run
- exact input or fixture involved
- exact observed behavior
- whether the issue affects:
  - controlled binary delivery
  - validator execution
  - workflow usage
  - diagnostics/reporting
- steps to reproduce if available

## Scope note

This repository is the public GitHub documentation, Action-wrapper, and adoption
surface for Tobi Validator.

Security reports should stay narrowly grounded in the released surface:

- installable `tobi` CLI
- authored Tsubasa source validation
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and workflow usage

This repository should not be read as a claim of:

- runtime/backend product surface
- public verification API surface
- platform SDK surface
- broader Organetic platform release surface
- unrestricted public access to the production validator implementation
