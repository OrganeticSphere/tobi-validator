---
name: Workflow fit discussion
about: Ask a concrete GitHub-first workflow-fit question for Tobi Validator
title: "[workflow-fit] "
labels: workflow-fit
assignees: ''
---

# Workflow Fit Discussion

Use this template for a concrete workflow-fit question related to Tobi
Validator.

**Tobi Validator**
**Reasoning Artifact Validator**

The current public adoption path is GitHub-first.

Use this template when you want to discuss:

- where Tobi Validator fits in a GitHub workflow
- how to use `canon` and `golden` in CI
- how a workflow policy should consume a Tobi validation result

Tobi supplies validator success or failure. The consuming workflow owns any
allow, block, merge, release, or escalation policy.

Do not use this template to assume that the following are already active public
channels:

- GitLab
- Nextflow
- Snakemake
- broader platform/runtime/backend/API surfaces
- future Organetic products

## 1. Workflow Summary

Describe your workflow in one or two direct sentences.

## 2. What You Are Trying To Accomplish

Examples:

- use a Tobi result in a pre-merge policy check
- compare recorded canonical outputs across runs
- use `golden` as a reproducibility-oriented check
- understand whether the released CLI fits a narrow CI validation step

## 3. Current Environment

- GitHub repository type:
- local or CI usage:
- expected trigger:
  - [ ] pull request
  - [ ] push
  - [ ] release
  - [ ] other
- operating environment:
- current workflow tooling:

## 4. Current Question

State the concrete question clearly.

Examples:

- where should `canon` run in this workflow?
- where should `golden` run in this workflow?
- should the validator result be consumed by a pull-request or release policy?
- does this fit the current Tobi Validator surface?

## 5. Relevant Command / Draft Workflow

```yaml
paste workflow or command here
```

## 6. What Kind Of Answer You Need

- [ ] placement guidance
- [ ] docs clarification
- [ ] starter workflow interpretation
- [ ] understanding product scope
- [ ] determining whether this fits the current Tobi Validator surface
- [ ] other narrow workflow-fit guidance

## 7. Scope Confirmation

- [ ] I understand the current public adoption path is GitHub-first
- [ ] I am not treating later workflow channels as already active public paths
- [ ] I understand that Tobi supplies a validator result and my workflow owns downstream policy
- [ ] I am asking about narrow workflow fit around the released validator CLI
