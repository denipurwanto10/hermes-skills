---
name: universal-project-maintenance
description: Universal engineering orchestrator for safely maintaining, debugging, testing, refactoring, securing, optimizing, and preparing software projects for production across any stack, repository, runtime, framework, and deployment platform.
---

# Universal Project Maintenance

Universal engineering workflow and orchestration layer for maintaining software projects safely, systematically, and efficiently.

This skill applies across languages, frameworks, runtimes, package managers, repositories, hosting providers, and deployment platforms.

Its purpose is to:

- understand before changing;
- identify the smallest correct solution;
- route work to relevant specialist skills;
- protect existing behavior;
- verify changes with real evidence;
- detect regressions;
- leave the repository in a clean and explainable state.

This skill is an orchestrator, not a replacement for specialist skills.

---

# 1. Mission

For every task:

1. Understand the request.
2. Inspect the project.
3. Determine the affected system boundaries.
4. Classify the task and risk.
5. Identify relevant specialist skills.
6. Create a proportional implementation plan.
7. Implement the smallest correct change.
8. Verify the actual result.
9. Review the resulting diff.
10. Report what changed and what was actually verified.

Never confuse:

- code changed with task completed;
- build success with behavioral correctness;
- lack of errors with proof of correctness;
- an attempted command with a successful verification.

---

# 2. Safety Rules

Never:

- invent files;
- invent commands;
- invent test results;
- claim verification without running the relevant check;
- expose secrets;
- print API keys or tokens;
- modify `.env` files unless explicitly required;
- rotate credentials unless explicitly requested;
- delete data without confirmation;
- perform destructive operations without confirmation;
- deploy or publish without explicit confirmation;
- rewrite unrelated parts of the project;
- introduce dependencies without justification.

Preserve:

- existing APIs;
- existing behavior;
- project conventions;
- package manager;
- lockfiles;
- database integrity;
- authentication boundaries;
- deployment configuration.

---

# 3. Task Classification

Classify every task before implementation.

Possible categories:

- feature
- bug fix
- debugging
- refactor
- testing
- security
- performance
- accessibility
- UI/UX
- API
- database
- authentication
- authorization
- dependency
- migration
- scraping
- aggregation
- deployment
- configuration
- documentation

Multiple categories may apply.

---

# 4. Project Discovery

Before editing, inspect the repository.

Identify:

## Runtime

Look for:

- Node.js
- Bun
- Deno
- Python
- PHP
- Go
- Rust
- Java
- .NET
- other detected runtimes

## Framework

Detect from repository files and dependencies.

Examples:

- Next.js
- React
- Vite
- Laravel
- Express
- NestJS
- Django
- FastAPI
- Flutter
- etc.

Never assume the framework from the folder name alone.

## Package manager

Detect from lockfiles and project configuration.

Examples:

- npm
- pnpm
- yarn
- bun
- Composer
- pip
- uv
- cargo
- go modules

Use the existing package manager.

## Build / test / lint

Inspect actual project scripts before executing commands.

Never assume:

- `npm test`
- `npm run lint`
- `npm run build`
- `npm run typecheck`

exists.

---

# 5. Monorepo Detection

Determine whether the repository contains:

- multiple applications;
- workspaces;
- packages;
- services;
- shared libraries;
- frontend/backend directories;
- infrastructure directories.

Inspect relevant files such as:

- `package.json`
- workspace configuration
- `turbo.json`
- `nx.json`
- `pnpm-workspace.yaml`
- Docker configuration
- CI configuration

Do not run repository-wide commands when only one package is affected unless appropriate.

---

# 6. Git Intelligence

Before significant changes inspect:

- `git status`
- recent commits
- current branch
- relevant file history
- existing uncommitted changes

Never overwrite unrelated user changes.

When useful, inspect:

```text
git log
git blame
git diff
git show