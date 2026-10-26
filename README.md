# Claude Project Template

A dev-container starter for new projects, built around **Claude Code +
Taskmaster**. The container ships only the global toolchain (Node LTS, git,
GitHub CLI, Claude Code, Taskmaster, TypeScript); everything project-specific
is added by Claude during a guided `/setup` conversation based on the project
scope you give it.

> This README is for the **human**. The machine-facing setup guide Claude
> follows is `docs/SETUP.md`. At the end of setup, Claude replaces this README
> with a real project README.

> **Contributions:** this template is shared as-is and doesn't accept pull
> requests (they're closed automatically). Issues and the wiki are open for
> questions and bug reports. Fork it freely — it's MIT-licensed.

## Getting started

1. **Copy the template into a new folder.** Either click **"Use this
   template"** on GitHub and clone your new repo, or copy a local clone (note
   the `/.` — it copies dotfiles too):

   ```bash
   cp -a claude-tm-project-template/. /path/to/my-new-project/
   ```

2. **Make it a git repo** (skip if you used "Use this template"; you own git
   setup by design):

   ```bash
   cd /path/to/my-new-project
   git init
   git add -A && git commit -m "chore: bootstrap from claude-project-template"
   ```

3. **Open the folder in VS Code** → when prompted, **"Reopen in Container"**
   (Command Palette → *Dev Containers: Reopen in Container*). The first build
   takes a few minutes.

4. **Start Claude and sign in** (once per project — auth persists in a
   per-project Docker volume across rebuilds):

   ```bash
   claude
   ```

   Run `/login` if prompted.

5. **Type `/setup`.** Claude reads `docs/SETUP.md` and takes it from there:
   it asks for your project scope (a file or a description), interviews you on
   the gaps, picks/confirms the stack, extends the dev container, scaffolds
   the project, drafts a PRD with you, and initialises the Taskmaster backlog.

   Setup usually includes **one container rebuild** (to bake in stack-specific
   dependencies). Claude will tell you exactly when and how; afterwards, start
   `claude` again and type `/setup` — it resumes from
   `docs/SETUP-PROGRESS.md` automatically.

## What's in the box

| Path | What it is |
| --- | --- |
| `.devcontainer/` | Ubuntu LTS + Node LTS image (latest at build time), global CLIs, per-project volumes for Claude auth / `node_modules` / shell history. Project deps get added between the `<<PROJECT-DEPS-*>>` markers in the Dockerfile. |
| `CLAUDE.md` | Always-loaded project instructions (conventions, workflow). Contains `SETUP:` markers Claude fills in during setup. |
| `docs/SETUP.md` | The guided-setup playbook Claude follows after `/setup`. |
| `docs/ARCHITECTURE.md` | Architecture summary skeleton, imported into every Claude session via `CLAUDE.md`. |
| `.claude/commands/setup.md` | The `/setup` slash command. |
| `.claude/commands/tm/` | Slash commands for common Taskmaster operations (`/tm/next-task`, `/tm/parse-prd`, …). |
| `.mcp.json` | Registers the `task-master-ai` MCP server (approve it once when Claude Code asks). |
| `.taskmaster/` | Taskmaster config (uses the `claude-code` provider — **no API keys needed**), PRD template, docs folder. |
| `LICENSE` | MIT license for the template. `/setup` asks which license your project wants and replaces it. |
| `.env.example` | Baseline env file; extended with project variables during setup. |

## Notes

- **Volumes are per-project** (named after the folder), so multiple projects
  created from this template never share `node_modules`, Claude auth, or
  shell history. Rebuilding the container keeps all three.
- **Rebuilds**: any time `.devcontainer/Dockerfile` changes, run Command
  Palette → *Dev Containers: Rebuild Container*. Claude cannot do this from
  inside the container — it will ask you.
- **Taskmaster API keys** are only needed if you want non-Claude models or
  `--research` mode; add them to `.env` / `.mcp.json` (see `.env.example`).
- To test on a physical phone from inside a container (mobile projects), use
  tunnel mode (e.g. `npx expo start --tunnel`) — LAN forwarding through Docker
  often doesn't reach the device.
