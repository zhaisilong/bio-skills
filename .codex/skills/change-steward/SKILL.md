---
name: change-steward
description: Curate repository changes before commit or push. Use when Codex needs to inspect a dirty worktree, group changed files by intent, identify documentation/changelog/version needs, prepare a commit scope/message, or judge commit/push readiness.
---

# Change Steward

Use this skill as a repository-local change curator after implementation work.
Collect, organize, and explain the finished changes, then decide whether the
repository is ready for commit or push. Do not use this skill as a git hook, and
do not stage, commit, push, or revert work without explicit user confirmation.

## Workflow

1. Inspect repository state before editing:
   - `git status --short --branch`
   - `git diff --stat`
   - `git diff --cached --stat`
   - `git log --oneline -8`
   - if an upstream exists, inspect commits ahead of it with
     `git log --oneline @{upstream}..HEAD`
2. Identify the intended change set:
   - Treat the user's latest request and already-reviewed edits as the primary
     scope.
   - Use dirty files as evidence, not as automatic scope expansion.
   - Keep unrelated dirty files separate and call them out instead of mixing
     them into the proposed commit.
3. Group changes by intent:
   - user-facing behavior, public API, or public contract
   - CLI, configuration, schema, generated output, or directory layout
   - runtime, infrastructure, dependency, environment, or reproducibility
   - tests, validation, fixtures, benchmark, or smoke evidence
   - documentation, release notes, examples, or internal refactor
4. Decide documentation work:
   - Follow the repository's existing conventions first.
   - Update a changelog or release notes when user-visible behavior, public
     contracts, workflows, compatibility, or important validation changes are
     present.
   - Update debugging or operations notes only when a reproducibility,
     environment, dependency, runtime, or validation incident has a concrete
     symptom, cause, fix, and validation trail worth preserving.
   - Update task-specific docs when commands, schemas, layouts, setup,
     examples, or test policy changed.
5. Decide version impact when the repository has versioned releases:
   - Patch for fixes, documentation/test stabilization, reproducibility fixes,
     dependency/runtime fixes, or small compatibility adjustments.
   - Minor for new public workflows, commands, options, schemas, layouts,
     integrations, backends, or validation capabilities.
   - Major only after asking the user.
   - Detect version sources from existing project conventions, such as
     `pyproject.toml`, `package.json`, `Cargo.toml`, `go.mod`, or obvious
     project version files. Do not invent a versioning scheme for an
     unversioned repository.
6. Verify consistency:
   - Check that docs, changelog/release notes, version files, tests, and final
     changed files describe the same scope.
   - If checks are too heavy or unavailable, report that explicitly instead of
     implying they passed.
7. Report readiness:
   - `not ready`: scope unclear, docs/version state inconsistent, checks
     failed or are missing, unrelated dirty files would be mixed in, or
     generated artifacts are unreviewed.
   - `commit ready`: intended files are reviewed, documented as needed,
     versioned as needed, and checks are run or explicitly skipped.
   - `push ready`: intended commits exist locally, branch/upstream are
     understood, the dirty state is clean or intentionally explained, and no
     required local validation remains.

## Commit And Push Rules

- Never revert unrelated user changes.
- Never stage, commit, or push without explicit user confirmation.
- Stage only reviewed files that belong to the explained change set.
- Before committing, show the readiness state, files to stage, proposed commit
  message, checks run, and checks skipped.
- Before pushing, confirm the branch, upstream, commits to push, and any
  remaining dirty files.

## Writing Rules

- Write changelog or release bullets about behavior, contracts, workflows, and
  operational impact, not implementation noise.
- Prefer focused documentation updates over broad rewrites.
- Keep debugging notes practical: symptom, cause, fix, and validation.
- If repository evidence conflicts with helper output or prior assumptions,
  explain the conflict and make the final judgment from repository evidence.
