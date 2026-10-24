# AI project starter kit

A ready-made setup for building any project with Claude Code. Copy it into every new repo.

## What's inside

| File / folder | What it's for |
|---|---|
| `PLAYBOOK.md` | The step-by-step pattern from idea to deploy. Read this first. |
| `PROMPTS.md` | Copy-paste prompt templates (feature, bug, decision, learning, handoff). |
| `AGENTS.md` | The main instructions every AI tool reads. Fill in the `<...>` parts. |
| `CLAUDE.md` | One line imports AGENTS.md, plus Claude Code-only notes. |
| `CLAUDE.local.md.example` | Your personal notes. Rename to `CLAUDE.local.md` and keep it out of git. |
| `.claude/settings.json` | Blocks Claude from reading or editing `.env` files (enforced, not just a request). |
| `.claude/rules/` | Rules for backend, frontend and database that load only when Claude works on matching files, plus `security.md`, which is always on. |
| `.claude/skills/` | Your commands: `/start-session`, `/end-session`, `/new-feature`, `/fix-bug`, `/review`, `/explain`, `/deploy`, `/security-docs`, `/security-review`. |
| `docs/ai/STATE.md` | The handoff: where the project is right now. Every new chat reads it first. |
| `docs/ai/DECISIONS.md` | Why things are the way they are. |
| `docs/ai/ROADMAP.md` | The ordered plan. |
| `docs/ai/BACKLOG.md` | Bugs and ideas, so nothing gets lost. |
| `docs/ai/SPEC.md` | What you're building (written once, at the start). |
| `docs/ai/DESIGN.md` | Design tokens, screens and components, from your design sample (images in `docs/design/`). |
| `docs/ai/DATA.md` | Data shapes and API operations; mock data follows them, the backend fills them later. |
| `docs/ai/LEARNING.md` | What you learned, for you and for interviews. |
| `docs/security/SECURITY.md` | Your app's security in one file: rules, who can do what, data kept, threats, launch checklist. Every control has a test and an honest status. |
| `.claude/rules/security.md` | Always-on security rules for every session ("never trust the client", ownership checks, no secrets in client code). |
| `.claude/skills/security-docs` | `/security-docs`: Claude interviews you one question at a time and writes SECURITY.md. |
| `.claude/skills/security-review` | `/security-review`: an audit that proves each finding with a request or test. Before every deploy. |

## Setup in a new project (5 minutes)
1. Create the project (for example `npx create-next-app@latest my-app`).
2. Copy everything from this kit into the project root, except `README.md` (keep your own README) and `PLAYBOOK.md` / `PROMPTS.md` (keep those in a personal folder, or copy them too).
3. Add to `.gitignore`:
   ```
   .env
   .env.*
   !.env.example
   CLAUDE.local.md
   ```
4. Open Claude Code in the project and run:
   ```
   Fill in AGENTS.md for this project: read package.json and the folder structure, replace the <...> parts, delete sections that don't apply, keep it under 200 lines. Adapt the paths in .claude/rules/ to this project's folders. Don't touch .env files.
   ```
5. Commit the kit: `git add . && git commit -m "Add AI setup"`.

## Daily use
- New chat → `/start-session`
- Build → `/new-feature <what>`
- Bug → `/fix-bug <what, where, expected>`
- Before committing → `/review`
- Learn → `/explain <file or flow>`
- End of the day → `/end-session`
- Before every deploy → `/security-review`

## Extra safety nets (set up once per repo, free)
- GitHub → Settings → Code security: turn on **Dependabot alerts** and **Secret scanning** (warns you about vulnerable packages and leaked keys).
- Before the first push of a new repo, scan for leaked secrets: `gitleaks detect` (install with `brew install gitleaks`).
- Add two-account tests to your end-to-end tests (user B can't open user A's private page), so access control is checked on every run, not just once.

## Use it everywhere
To have the skills in every project without copying them, put them in your home folder instead: `~/.claude/skills/<name>/SKILL.md`. Keep project-specific ones (like `/deploy`) in the repo.
