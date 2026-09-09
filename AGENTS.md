# AGENTS.md

<!-- PC-NOT-INITIALIZED -->

This file provides guidance to AI agents when working in this repository.

Agent-agnostic. Works with OpenCode, Claude Code, Codex, Gemini, and others.

## Context

Load `DESIGN.md` for design principles and guidelines. Load `ARCHITECTURE.md` for system architecture and component interactions. These files are generated during initialization and updated as the codebase evolves.

Command aliases: OpenSpec skills may reference `/opsx-propose`, `/opsx-apply`, `/opsx-archive`, or `/opsx-explore`. Always substitute them with the `pc-plan-propose`, `pc-plan-apply`, `pc-plan-archive`, `pc-plan-explore` skills respectively (user-facing command names: `/plan-propose`, `/plan-apply`, `/plan-archive`, `/plan-explore`). Never mention the `opsx-` names to the user.

## I am the lead, full workflow ownership

<!-- PC-PLATFORM-WORKFLOW-START -->
A GitHub Issue or PR URL in the user's message means run the pipeline, in whatever words it arrives, unless they asked for analysis or context only.

- Issue URL: `pc-userstory` to parse it, `pc-plan-propose` for the plan, confirm, `pc-plan-apply` to build, then ship.
- An existing OpenSpec change, plus any of `implement` / `start` / `go`: `pc-plan-apply`, then ship.
- A PR URL with a feedback or fix request: read the PR comments, fix, update the PR.
<!-- PC-PLATFORM-WORKFLOW-END -->

Never delegate without a plan. Default to specialists for implementation. If a subagent wave repeatedly fails, stop forcing it: report, then continue in the main session or ask the user.

## Engineer selection

Inspect `.opencode/agents/*.md` before spawning. Prefer the most specialized custom engineer. `fullstack-engineer` is `mode: primary` (the user's planning agent), not a spawned worker. If no specialist matches, tell the user to create one with `/make-engineer`. Spawn only engineers present in that directory.

Full wave protocol, pipeline phases, and concurrency limits: see the `pc-plan-apply` skill (authoritative). Max concurrent agents is `agents.maxConcurrent` in `.opencode/harness.json`.

## Skills

Skills live in `.agents/skills/`. Always installed: `@pc-guardrails-generic`, `@pc-guardrails-project`, `@browser-automation`. Agents load them via `@skill-name` in their `## Abilities` section.

<!-- PC-PLATFORM-SKILLS-GUIDE-START -->
Platform skills (GitHub):
- `@pc-userstory`: load when a GitHub Issue URL is detected. Fetches the issue via `gh` CLI and creates an OpenSpec change. NEVER use webfetch to access GitHub URLs.
- `pc-ops-ship`: load in ship mode to create a PR with screenshots, or in feedback mode to read and classify PR review comments.
<!-- PC-PLATFORM-SKILLS-GUIDE-END -->
