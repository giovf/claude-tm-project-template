# Project guidelines for Claude Code

This file is loaded automatically by Claude Code at the start of every session
(both `claude` in the terminal and the IDE extension). Keep it small and
high-signal — it's part of every prompt, so verbosity costs tokens.

<!-- SETUP: If this comment is still here, the project hasn't been bootstrapped
     yet — run /setup (it follows docs/SETUP.md). During setup, fill in every
     SETUP marker below and then delete the markers. -->

## Architecture
- Product/system architecture lives in `docs/ARCHITECTURE.md` (imported
  below). That file tracks the PRD (`.taskmaster/docs/prd.md`); this file is
  conventions and practices only — keep PRD-specific detail out of here.

## Stack
<!-- SETUP: replace with the real stack, e.g. framework + language + targets.
     One bullet per load-bearing choice. -->
- **Package manager**: npm (don't switch to pnpm/yarn without asking)
- **Language**: TypeScript everywhere — strict mode
<!-- SETUP: add the commands that matter: dev server, build, test, lint. -->

## Conventions
- All new code in TypeScript with explicit return types on exported functions
- No `any`, no `// @ts-ignore` without a comment explaining why
- Prefer named exports over default exports
<!-- SETUP: add stack-specific conventions (routing, state management, styling/
     design tokens, folder layout). For UI projects: enable the frontend-design
     plugin and reference the design-token location here. -->

## Working loop (mandatory — applies even if the user doesn't mention Taskmaster)
A **functional change** is anything that changes behaviour: features, bug
fixes, behaviour-changing refactors, new deps, schema/API changes. Docs-only,
formatting, typo fixes and answering questions are exempt. For every
functional change, before writing code:

1. **File it** — reuse the task that already covers it, otherwise
   `task-master add-task --prompt="<what and why>"`.
2. **Score it** — `task-master analyze-complexity --id=<id> --threshold=7`,
   then read the score with `task-master complexity-report`.
3. **Split if > 6/10** — `task-master expand --id=<id>` (uses the report's
   recommended subtask count). Then work subtask by subtask.
4. **Check the blueprint** — does the change alter scope, features, data
   model, stack, external services or the out-of-scope list? If so, update
   `.taskmaster/docs/prd.md` and add a dated entry to its `## Changelog`;
   if a stable decision changed, update `docs/ARCHITECTURE.md` too. Changes
   to approved scope need the user's OK first.
5. **Implement** — `set-status --status=in-progress`, log notes with
   `task-master update-subtask`, verify (typecheck/lint/tests — not "should
   work"), then `set-status --status=done`.

- Never hand-edit `.taskmaster/tasks/tasks.json` — use the CLI/MCP tools.
- Don't commit `node_modules/`, `.taskmaster/reports/`, or anything in
  `.gitignore`.

## Dependencies
- Add deps with `npm install <pkg>@latest` (or the scaffolder's `@latest`);
  never hand-type version numbers. The lockfile provides reproducibility.

## Things to ask before doing
- Adding a new top-level dependency
- Changing the package manager
- Modifying anything inside `.devcontainer/`
- Deploying, publishing, or submitting to any store/registry
<!-- SETUP: add project-specific irreversible actions (e.g. running cloud
     migrations, store submissions, sending real notifications). -->

## Product architecture
**Import the architecture overview; treat as if inlined here.**
@./docs/ARCHITECTURE.md

## Task Master AI Instructions
**Import Task Master's development workflow commands and guidelines, treat as if import is in the main CLAUDE.md file.**
@./.taskmaster/CLAUDE.md
