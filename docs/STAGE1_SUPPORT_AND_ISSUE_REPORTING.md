# Tobi Validator Support And Issue Reporting

Project: Organetic Sphere
Component: Tobi Validator
Descriptor: Reasoning Artifact Validator
Scope: public support and issue-reporting guidance
Date basis: 2026-08-23

## What This Document Is

This document explains how to report problems and workflow-fit friction for
Tobi Validator.

The current public adoption path is GitHub-first.

This document is for:

- reproducible bug reports
- diagnostics-oriented failure reporting
- workflow-fit questions grounded in the released validator CLI
- documentation clarification requests

This document is not a promise of:

- runtime/backend support
- public verification API support
- broader platform support
- automatic support for later Organetic product surfaces

## Current Released Tobi Validator Surface

Keep reports narrowly grounded in:

- installable `tobi` CLI
- authored Tsubasa source validation
- Tsubasa canonicalization through Tobi
- canonical ASCII output
- current `_h` compatibility identity
- deterministic diagnostics
- `golden` conformance execution
- thin packaging and workflow usage

Tobi supplies validator results. A consuming workflow owns any allow, block,
merge, release, or escalation policy around those results.

## Start Here Before Reporting

Check:

- `docs/STAGE1_QUICKSTART_FIRST_10_MINUTES.md`
- `docs/STAGE1_INSTALL_AND_USAGE.md`
- `docs/STAGE1_DIAGNOSTICS_REFERENCE.md`
- `docs/STAGE1_GITHUB_ACTION_STARTER.md`

The physical filenames retain legacy spelling for link stability. Their visible
titles and current product language use Tobi Validator.

If your question concerns GitHub workflow placement, use the workflow-fit issue
template rather than a generic bug report.

## What To Report

Appropriate public reports include:

- a command that failed unexpectedly
- a diagnostic message that is unclear
- a fixture mismatch in `golden`
- documentation that does not match observed released behavior
- a narrow GitHub workflow-fit question around the released validator CLI

## What Not To Report As If Already Released

Do not file support requests as if the following are already available:

- runtime execution
- backend execution
- public verification API
- platform SDK
- broad GitLab / Nextflow / Snakemake rollout
- broader Organetic platform availability
- unrestricted public access to the production validator implementation

## How To Write A Good Bug Report

Include:

- exact release version / tag
- exact command run
- exact source file or fixture used
- exact observed output
- expected behavior
- actual behavior
- diagnostic code and span if present
- whether the issue is reproducible

Good reports are concrete. Vague reports create noise and slow support.

## How To Write A Good Workflow-Fit Question

Include:

- what workflow you are trying to support
- whether this is local or GitHub CI usage
- where you think `canon` or `golden` belongs
- what policy will consume the validator result
- what is unclear in current docs or starter materials
- whether you are asking about current Tobi Validator fit rather than future products

## Recommended Issue Paths

Use:

- `Bug report` for reproducible Tobi Validator issues
- `Workflow fit discussion` for GitHub-first workflow-fit questions

For security-sensitive matters, do not open a detailed public issue. Use the
private contact path in `SECURITY.md`.

## Scope Reminder

This repository is the public GitHub documentation, Action-wrapper, and
adoption surface for Tobi Validator. It is not the full development source
repository.

Reports should stay grounded in:

- docs
- examples
- controlled validator delivery
- released CLI behavior
- workflow adoption materials

## Current Bottom Line

Use public issues for:

- reproducible Tobi Validator problems
- diagnostics questions
- documentation mismatches
- GitHub-first workflow-fit questions

Do not use public issues to treat unreleased runtime, backend, API, platform, or
future-product surfaces as if they were already available.

Keep reports narrow, exact, and reproducible.
