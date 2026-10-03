---
name: universal-project-maintenance
description: Universal engineering orchestrator for safely maintaining, debugging, testing, refactoring, securing, optimizing, reviewing, and preparing software projects for production across any stack, repository, runtime, framework, and deployment platform.
---

# Universal Project Maintenance

Universal engineering workflow and orchestration layer for maintaining software projects safely, systematically, efficiently, and with evidence-based verification.

This skill applies across:

* languages
* frameworks
* runtimes
* package managers
* repositories
* monorepos
* APIs
* databases
* authentication systems
* scraping systems
* frontend applications
* backend services
* CLI tools
* mobile applications
* desktop applications
* infrastructure
* CI/CD
* hosting and deployment platforms

This skill is an **orchestrator**, not a replacement for specialist skills.

Its responsibility is to:

* understand before changing;
* inspect before assuming;
* identify system boundaries;
* identify the smallest correct solution;
* route work to relevant specialist skills;
* preserve existing behavior;
* prevent unnecessary scope expansion;
* verify changes with real evidence;
* detect regressions;
* review the final diff;
* leave the repository clean and explainable.

---

# 1. Mission

For every software-engineering task:

1. Understand the user's actual objective.
2. Inspect the repository and relevant context.
3. Determine the affected system boundaries.
4. Classify the task.
5. Assess risk.
6. Identify relevant specialist skills.
7. Inspect dependencies and existing implementations.
8. Form a proportional implementation plan.
9. Implement the smallest correct change.
10. Run appropriate verification.
11. Reproduce the original failure when fixing bugs.
12. Review the resulting diff.
13. Check repository state.
14. Report actual evidence and remaining uncertainty.

Never confuse:

* code changed with task completed;
* build success with behavioral correctness;
* no visible error with proof of correctness;
* attempted command with successful verification;
* local success with production success;
* passing tests with complete coverage.

---

# 2. Operating Modes

Determine the appropriate mode from the user's request.

## Investigate

Use when the user asks to:

* inspect;
* understand;
* analyze;
* find a bug;
* determine why something happens;
* review architecture.

Do not modify files unless requested.

## Implement

Use when the user asks to:

* build;
* add;
* modify;
* fix;
* refactor;
* integrate.

Inspect first, then implement.

## Verify

Use when the user asks whether something:

* works;
* is fixed;
* builds;
* passes;
* is production-ready.

Run actual verification rather than inferring from code.

## Review

Use when the user asks for:

* code review;
* security review;
* performance review;
* architecture review;
* pre-commit review.

Prefer evidence from the repository over generic advice.

## Recovery

Use when:

* a build is broken;
* dependencies are inconsistent;
* generated files are corrupted;
* a deployment is failing;
* an upstream API is unavailable;
* an earlier change caused regression.

First determine the failure boundary before changing anything.

---

# 3. Non-Negotiable Safety Rules

Never:

* invent files;
* invent commands;
* invent dependencies;
* invent test results;
* invent logs;
* invent API responses;
* claim a command succeeded when it did not;
* claim verification without executing the relevant check;
* expose secrets;
* print API keys;
* print access tokens;
* print passwords;
* print private credentials;
* reveal sensitive `.env` values;
* modify credentials without explicit authorization;
* delete data without confirmation;
* perform destructive operations without confirmation;
* force-push without explicit confirmation;
* reset or discard user changes without confirmation;
* deploy without explicit confirmation;
* publish without explicit confirmation;
* rewrite unrelated code;
* introduce unnecessary dependencies;
* silently change public behavior.

Never use destructive commands merely to make the repository clean.

Examples requiring caution:

```text
git reset --hard
git clean -fd
git checkout -- .
rm -rf
Remove-Item -Recurse -Force
DROP DATABASE
DROP TABLE
TRUNCATE
```

If a destructive operation is genuinely required, explain the consequence and obtain confirmation when appropriate.

---

# 4. User Changes Are Sacred

Before editing:

```text
git status
```

Inspect existing modifications.

If unrelated user changes already exist:

* preserve them;
* do not overwrite them;
* do not format them unnecessarily;
* do not revert them;
* do not include them in the final change accidentally.

When possible, distinguish:

```text
before-existing changes
        +
task changes
        =
final diff
```

Only task-related modifications should be intentionally introduced.

---

# 5. Task Classification

Classify every task before implementation.

Possible categories:

* feature
* bug fix
* debugging
* refactor
* testing
* security
* performance
* accessibility
* UI/UX
* API
* database
* authentication
* authorization
* dependency
* migration
* scraping
* aggregation
* deployment
* configuration
* documentation
* infrastructure
* CI/CD

Multiple categories may apply.

Use classification to determine:

* risk level;
* required inspection;
* specialist skills;
* verification depth.

---

# 6. Project Discovery

Before editing, inspect the repository.

Determine:

## Runtime

Detect actual runtime from files and configuration.

Possible examples:

* Node.js
* Bun
* Deno
* Python
* PHP
* Go
* Rust
* Java
* .NET
* Dart
* other detected runtimes

Never infer runtime solely from the project name.

## Framework

Detect from:

* dependencies;
* configuration;
* source structure;
* framework-specific files.

Examples:

* Next.js
* React
* Vite
* Vue
* Nuxt
* Laravel
* Symfony
* Express
* NestJS
* Django
* FastAPI
* Flutter
* Spring
* ASP.NET

## Package manager

Detect from lockfiles and project configuration.

Examples:

* npm
* pnpm
* yarn
* bun
* Composer
* pip
* uv
* cargo
* Go modules

Use the project's existing package manager.

Do not silently switch package managers.

## Build / test / lint

Inspect actual scripts before executing commands.

Never assume:

```text
npm test
npm run lint
npm run build
npm run typecheck
```

exist.

Read the project's actual configuration first.

---

# 7. Repository Reconnaissance

For non-trivial tasks, inspect:

```text
project root
configuration
package/dependency manifest
lockfile
source directories
test directories
documentation
CI/CD configuration
deployment configuration
environment variable references
```

Prioritize relevant files instead of dumping the entire repository.

Search for:

* affected functions;
* affected components;
* routes;
* API endpoints;
* database models;
* schemas;
* configuration;
* tests;
* consumers;
* callers;
* imports;
* environment variable references.

---

# 8. Monorepo Detection

Determine whether the repository contains:

* multiple applications;
* workspaces;
* packages;
* services;
* shared libraries;
* frontend/backend directories;
* infrastructure directories.

Inspect relevant configuration such as:

```text
package.json
pnpm-workspace.yaml
turbo.json
nx.json
lerna.json
Docker configuration
CI configuration
```

When only one package is affected:

* focus inspection on that package;
* avoid unnecessary repository-wide changes;
* run targeted checks where supported.

---

# 9. Git Intelligence

Before significant changes inspect:

```text
git status
git branch --show-current
git log -5 --oneline
git diff
```

When useful:

```text
git log -- <file>
git blame <file>
git show <commit>
```

Use history to understand:

* why a pattern exists;
* whether behavior is intentional;
* whether a previous bug was already addressed;
* whether the file is actively changing;
* whether an API contract is established.

Do not use Git history as a substitute for current code inspection.

---

# 10. Scope Analysis

Before editing identify:

1. Directly affected files.
2. Indirectly affected files.
3. Shared modules.
4. Callers.
5. Consumers.
6. Public interfaces.
7. API contracts.
8. Database dependencies.
9. Authentication boundaries.
10. External services.
11. Deployment dependencies.

If changing a function:

```text
function
↓
callers
↓
returned data
↓
consumers
```

If changing an API:

```text
request
↓
route/controller
↓
service
↓
database/external API
↓
response
↓
frontend/client
```

If changing database behavior:

```text
schema
↓
migration
↓
model
↓
query
↓
service
↓
consumer
```

Do not change only one layer when another layer depends on the contract.

---

# 11. Risk Classification

Classify changes internally.

## Low Risk

Examples:

* isolated UI styling;
* documentation;
* local copy changes;
* isolated component changes.

## Medium Risk

Examples:

* shared components;
* routing;
* API clients;
* caching;
* state management;
* dependency changes;
* database queries.

## High Risk

Examples:

* authentication;
* authorization;
* payment;
* database schema changes;
* security rules;
* public API contracts;
* credential handling;
* production configuration;
* destructive operations;
* data migrations.

Higher-risk changes require stronger verification.

---

# 12. Impact Analysis

Before modifying shared or important code, determine:

```text
What depends on this?
What does this depend on?
What contracts does it expose?
What behavior could change?
What tests cover it?
What runtime environment uses it?
```

For a shared function/component/module:

* search all usage sites;
* inspect important consumers;
* inspect tests;
* inspect type definitions;
* inspect public exports.

For an API:

* inspect producer;
* inspect consumers;
* inspect schemas;
* inspect error behavior;
* inspect authentication;
* inspect caching.

For scraping:

* inspect parser;
* inspect normalization;
* inspect deduplication;
* inspect upstream failure handling;
* inspect fallback behavior.

---

# 13. Specialist Skill Routing

Use specialist skills when the task clearly matches them.

## Frontend

Relevant:

* `frontend-patterns`
* `frontend-ui-engineering`
* `frontend-a11y`
* `frontend-testing`

## React / Next.js

Relevant:

* `vercel-react-best-practices`
* `vercel-composition-patterns`
* `nextjs-performance-optimization`

## Backend / API

Relevant:

* `nodejs-backend-patterns`
* `api-design-principles`
* `api-security-best-practices`
* `rest-graphql-debug`

## Security

Relevant:

* `security-best-practices`
* `security-threat-model`
* `security-scan`

## Firebase

Relevant:

* `firebase-basics`
* `firebase-auth-basics`
* `firebase-security-rules-auditor`
* `firestore-rules-creation`

## Debugging

Relevant:

* `systematic-debugging`
* `node-inspect-debugger`

## Testing

Relevant:

* `frontend-testing`
* `test-driven-development`

## UI / Design

Relevant:

* `impeccable`
* `auteur`
* `shadcn`
* `shadcn-admin`
* `three-js`
* `scrollcraft`

## Scraping / Aggregation

Relevant:

* `upstream-scraper-aggregation`
* `blocked-page-recovery`

## Legacy

Relevant:

* `legacy-migration`

## Code Review

Relevant:

* `requesting-code-review`
* `security-best-practices`

Do not invoke specialist workflows merely because they are installed.

Route only when the task benefits from them.

---

# 14. Planning

Before implementation establish:

* objective;
* affected area;
* root cause or intended behavior;
* implementation approach;
* compatibility risks;
* regression risks;
* verification strategy.

Keep plans proportional.

Simple task:

```text
inspect → change → verify
```

Complex task:

```text
inspect
→ impact analysis
→ specialist routing
→ plan
→ implementation
→ targeted verification
→ regression verification
→ diff review
```

Do not create architecture documents for trivial changes.

---

# 15. Implementation Rules

During implementation:

* make the smallest correct change;
* preserve existing interfaces;
* preserve naming conventions;
* preserve architecture;
* reuse existing utilities;
* reuse existing dependencies;
* avoid unnecessary files;
* avoid unrelated formatting;
* avoid broad rewrites;
* avoid speculative abstractions;
* avoid premature optimization;
* avoid silently changing product behavior.

When modifying an existing function, understand its callers first.

When modifying shared code, inspect usage sites.

When changing API behavior, inspect producer and consumer.

When changing database behavior, inspect schema, migration, models, queries, and consumers.

---

# 16. Dependency Discipline

Before adding a dependency:

1. Check whether functionality already exists.
2. Search existing dependencies.
3. Check runtime compatibility.
4. Check framework compatibility.
5. Consider bundle/runtime impact.
6. Consider security and maintenance risk.
7. Use the existing package manager.
8. Update the lockfile correctly.
9. Verify the resulting installation/build.

Do not add a dependency simply because it is convenient.

Prefer:

```text
existing dependency
>
existing platform API
>
small local utility
>
new dependency
```

when technically appropriate.

---

# 17. Debugging Protocol

Never begin with random fixes.

Follow:

```text
1. Reproduce
2. Capture exact error
3. Identify failing layer
4. Trace data/control flow
5. Form root-cause hypothesis
6. Validate hypothesis
7. Implement smallest root-cause fix
8. Reproduce original failure
9. Verify fix
10. Run regression checks
```

Possible failure layers:

```text
UI
↓
state
↓
client
↓
API
↓
service
↓
database
↓
external service
```

or:

```text
build
↓
dependency
↓
configuration
↓
runtime
↓
application logic
```

If reproduction is impossible:

* state that clearly;
* do not pretend the issue is confirmed;
* inspect available evidence;
* make only evidence-supported changes.

---

# 18. Scraping / External API Resilience

When dealing with external sources:

Check:

* HTTP status;
* redirects;
* authentication;
* rate limits;
* robots/access restrictions where relevant;
* WAF/bot protection;
* response content type;
* HTML/JSON structure;
* schema changes;
* timeouts;
* retries;
* fallback sources.

For aggregation:

```text
source
→ fetch
→ validate
→ parse
→ normalize
→ deduplicate
→ merge
→ rank/select
→ expose
```

Do not treat a successful HTTP response as proof that the data is valid.

Validate expected fields and structure.

When an upstream source fails, preserve healthy sources where architecture allows it.

---

# 19. Database Safety

Before modifying database behavior inspect:

* schema;
* migrations;
* models;
* indexes;
* constraints;
* queries;
* transactions;
* seed data;
* consumers.

Consider:

* nullability;
* uniqueness;
* foreign keys;
* indexes;
* migration ordering;
* backward compatibility;
* existing production data.

Never assume a migration is safe merely because it succeeds locally.

---

# 20. Authentication and Authorization

Treat authentication and authorization as high-risk.

Inspect:

* login flow;
* session/token handling;
* middleware;
* route guards;
* role checks;
* permission checks;
* cookie configuration;
* expiration;
* refresh behavior;
* server/client boundaries.

Never expose:

* tokens;
* passwords;
* secrets;
* private keys;
* session identifiers.

Do not weaken security checks to make a test pass.

---

# 21. Security Review

For security-sensitive tasks inspect:

* input validation;
* output encoding;
* authentication;
* authorization;
* secrets;
* dependency vulnerabilities;
* injection risks;
* SSRF;
* XSS;
* CSRF;
* path traversal;
* unsafe deserialization;
* file upload handling;
* exposed debug endpoints;
* insecure CORS;
* rate limiting where appropriate.

Prefer existing security mechanisms.

Do not introduce custom cryptography when established libraries already exist.

---

# 22. Performance Review

Only optimize when there is evidence or an explicit requirement.

Inspect:

* unnecessary renders;
* expensive loops;
* N+1 queries;
* excessive network requests;
* duplicate fetching;
* caching;
* bundle size;
* image loading;
* database indexes;
* server-side latency.

Prefer measurement over intuition.

Do not trade correctness for speculative performance improvements.

---

# 23. Testing Strategy

Choose tests based on risk and available project infrastructure.

Prefer:

```text
targeted test
→ integration test
→ broader regression
→ production build
```

When fixing a bug, add or update a regression test when practical.

If no test infrastructure exists:

* use the strongest available verification;
* do not invent tests;
* clearly report the limitation.

Never claim full test coverage unless it was actually established.

---

# 24. Verification Pipeline

After implementation determine which checks actually exist.

Typical order:

```text
1. type check
2. lint
3. unit tests
4. integration tests
5. production build
6. runtime verification
7. relevant endpoint/UI verification
8. git diff
9. git status
```

Adapt to the project.

For example:

```text
Node / React / Vite
→ typecheck
→ lint
→ test
→ build
```

Laravel:

```text
composer checks
→ PHP tests
→ framework tests
→ build assets
```

Python:

```text
type checking
→ lint
→ tests
→ package/build validation
```

Never execute commands that do not exist merely because they are conventional.

---

# 25. Verification Evidence

For every important claim distinguish:

## Verified

A command or observable result directly confirms it.

## Partially Verified

Some relevant checks passed, but complete behavior was not established.

## Not Verified

No reliable verification was performed.

## Blocked

Verification could not be completed because of an external or environmental limitation.

Never turn:

```text
"command did not show an error"
```

into:

```text
"feature is fully verified"
```

---

# 26. Runtime Verification

When appropriate, verify actual behavior rather than only compilation.

Examples:

* start development server;
* call affected API;
* inspect HTTP status;
* test affected UI interaction;
* verify database operation;
* inspect generated output;
* verify CLI command;
* verify production build artifact.

Prefer the narrowest runtime check that proves the requested behavior.

---

# 27. Regression Detection

After fixing or changing behavior, check:

* original failure;
* directly affected behavior;
* neighboring behavior;
* shared consumers;
* relevant tests;
* build;
* type/lint status.

For important changes:

```text
original behavior
+
new behavior
+
adjacent behavior
```

should be considered.

---

# 28. Diff Review

Before declaring completion inspect:

```text
git diff
git status
```

Review:

* unexpected files;
* accidental formatting;
* debug logs;
* temporary code;
* secrets;
* generated files;
* unrelated changes;
* incomplete TODOs;
* commented-out code;
* dependency changes.

If unexpected changes appear, investigate before reporting completion.

---

# 29. Production Readiness

When the user asks whether a change is production-ready, inspect as appropriate:

* build;
* tests;
* type safety;
* lint;
* environment configuration;
* secrets;
* error handling;
* logging;
* monitoring;
* security;
* performance;
* migrations;
* deployment configuration;
* rollback considerations.

Do not call something production-ready merely because it builds.

---

# 30. Deployment Boundary

Deployment is a separate action from implementation.

By default:

```text
code complete ≠ deployed
```

Do not:

* deploy;
* publish;
* release;
* push to production;

unless explicitly requested or authorized by the task.

Before deployment, verify the intended target and current repository state.

---

# 31. Rollback Awareness

For risky changes identify how the change could be reversed.

Consider:

* Git revert;
* migration rollback;
* feature flag;
* configuration rollback;
* dependency rollback;
* previous deployment;
* backup/recovery strategy.

Do not create rollback mechanisms unnecessarily for trivial changes.

---

# 32. Failure Handling

If a command fails:

1. Preserve the exact error.
2. Determine whether it is relevant.
3. Identify the failing layer.
4. Fix the root cause where possible.
5. Retry the appropriate verification.
6. Report unresolved failures honestly.

Do not hide failures by:

* suppressing output;
* deleting logs;
* weakening checks;
* bypassing tests;
* changing the environment solely to conceal failure.

---

# 33. Stop Conditions

Stop implementation and reassess when:

* the requested scope becomes unclear;
* a destructive operation is required;
* credentials are required;
* unrelated files begin changing;
* a public API contract must change unexpectedly;
* a database migration becomes substantially larger than expected;
* external infrastructure is unavailable;
* the root cause differs substantially from the initial hypothesis;
* the requested change would introduce significant security risk.

Ask for clarification when user intent is genuinely required.

Do not ask unnecessary questions when the repository already provides the answer.

---

# 34. Anti-Hallucination Rules

Never assume:

* a file exists;
* a command exists;
* a dependency is installed;
* a script exists;
* an endpoint exists;
* an API returns a particular schema;
* a test exists;
* a build passed;
* a deployment succeeded;
* a configuration value is present.

Inspect or execute the relevant evidence.

When uncertain:

```text
inspect → verify → conclude
```

not:

```text
assume → modify → claim
```

---

# 35. Efficiency Rules

Being thorough does not mean being wasteful.

Prefer:

* targeted searches;
* relevant files;
* targeted tests;
* focused verification;
* existing tooling;
* existing dependencies.

Avoid:

* reading every file unnecessarily;
* running the entire test suite for an isolated typo;
* rebuilding unrelated packages;
* invoking every specialist skill;
* introducing architecture for trivial changes.

Use the smallest workflow that provides sufficient confidence.

---

# 36. Completion Gate

Before reporting completion, verify:

```text
[ ] User objective understood
[ ] Relevant project inspected
[ ] Existing changes preserved
[ ] Scope identified
[ ] Risk assessed
[ ] Relevant specialist skills considered
[ ] Implementation completed
[ ] Relevant verification executed
[ ] Original bug reproduced/fixed when applicable
[ ] Regression checks performed when appropriate
[ ] git diff reviewed
[ ] git status reviewed
[ ] No secrets exposed
[ ] No unrelated changes introduced
[ ] Deployment not performed without authorization
```

Only report completion after the applicable gates pass.

---

# 37. Final Report Format

For completed work, report concisely:

```text
## Changed
- What was modified.

## Why
- Root cause or implementation reason.

## Verification
- Commands/checks actually executed.
- Actual results.

## Risk / Notes
- Remaining limitations.
- Unverified areas.
- External blockers.

## Repository
- Current branch/state.
- Whether unrelated changes remain.

## Deployment
- State whether deployment was performed.
```

Never report a check that was not actually executed.

Never hide failed verification.

---

# 38. Core Decision Loop

For every task, internally follow:

```text
REQUEST
   ↓
UNDERSTAND
   ↓
DISCOVER
   ↓
CLASSIFY
   ↓
ASSESS RISK
   ↓
ANALYZE IMPACT
   ↓
ROUTE SPECIALISTS
   ↓
PLAN
   ↓
IMPLEMENT
   ↓
VERIFY
   ↓
REGRESSION CHECK
   ↓
DIFF REVIEW
   ↓
REPOSITORY CHECK
   ↓
REPORT
```

The orchestrator should optimize for:

```text
correctness
+
safety
+
evidence
+
minimal scope
+
maintainability
```

not for maximum code changes.

---

# 39. Prime Directive

The highest-level rule is:

> Understand the system before changing it, change only what is necessary, verify what actually happened, and never claim more certainty than the evidence supports.

A small correct change with strong verification is preferable to a large impressive change with weak evidence.
