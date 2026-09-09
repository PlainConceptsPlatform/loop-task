---
name: pc-guardrails-generic
description: Generic guardrails, foundational rules that all agents follow. Users add specialized guardrails skills for specific concerns. Covers secrets, code quality, security, tool usage, and engineer workflow.
license: MIT
---

## Transitive loads (optimization skills)

The marker sections below name the optimization skills this project selected. Load each one before doing any work.

## Secrets

- Treat `.env` files as write-only: write to them when configuring, and read credentials at runtime from the environment or the secret store.
- Never put a credential, API key or token in a log line, an output, or a commit in anything but encrypted or template form. Anything printed is in a CI log that outlives the run.

## Code

- Comments are for WHY, not WHAT. Use them only where the code does something non-obvious or the reason cannot be inferred from context. Past a 10% comment ratio in a file, refactor for clarity instead.
- Never add a file that collects unrelated things — `constants.js`, `types.ts`, `config.js`, `utils.ts`. One responsibility per file, split by domain or feature (`user-constants.ts`, `order-types.ts`, `auth-config.ts`). A file importing from many unrelated modules is already the symptom.

## Temporary files

- Never write outside `$REPO_ROOT`, and never to an operating-system temporary directory: the next step and the next agent cannot see it, and nobody cleans it up. Scratch goes under `$REPO_ROOT/.opencode/.tmp/`, in a task-specific child directory when needed (enforced by pc-system-reminders).
- Never report a path under `.tmp/` as a deliverable. Copy or move the artifact to its required repository path first.
- Never leave scratch files behind at the end of a task, unless they are the evidence for a failure you are reporting.

<!-- PC-GUARDRAILS-RTK-START -->
## RTK

- Prefix CLI commands with `rtk` (`rtk git diff`, `rtk pnpm test`); it strips the output down to what matters. Read-only commands like `cat`, `ls` and `Get-Content` are exempt.
<!-- PC-GUARDRAILS-RTK-END -->

<!-- PC-GUARDRAILS-CODEGRAPH-START -->

<!-- PC-GUARDRAILS-CODEGRAPH-END -->

<!-- PC-GUARDRAILS-MEMORY-START -->

<!-- PC-GUARDRAILS-MEMORY-END -->

<!-- PC-GUARDRAILS-SIMPLE-ENGLISH-START -->
## Simple English (optimization skill)

- Apply Simplified Technical English to all prose: `skill("simple-english")`. Editing, shell and spawning stay blocked until it is loaded (pc-system-reminders).
- Keep code blocks, identifiers, CLI commands, file paths, quoted errors, and product names exact.
<!-- PC-GUARDRAILS-SIMPLE-ENGLISH-END -->

<!-- PC-GUARDRAILS-HUMANIZER-START -->
## Humanizer (optimization skill)

- Load `skill("humanizer")` before writing prose (commit messages, PR descriptions, docs, proposals); unhumanized prose reads as machine-written. Editing, shell and spawning stay blocked until it is loaded (pc-system-reminders).
- Never apply it to code, config files, or terminal output: prose only.
<!-- PC-GUARDRAILS-HUMANIZER-END -->

## Engineer workflow (when spawned)

The lead put your task IDs and their text in your prompt. Two things about that are not up to you:

- Load every skill under your `## Abilities` before you start, guardrails first, one `skill` call per `@skill-name`. Editing, shell and spawning are blocked until you have (pc-system-reminders).
- Edit only files in your assigned scope, then return a summary: task IDs done, files changed, tests and lint result, decisions made. Then you exit. Never poll for more work, and never claim a task the lead did not give you: the lead spawns with the work in hand, so a worker that waits is a worker that hangs the wave.
