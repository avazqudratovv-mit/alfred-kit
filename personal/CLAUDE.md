# My personal Claude Code rules (all projects)

<!-- Copy to ~/.claude/CLAUDE.md on every computer you use. It loads in every project,
     alongside the project's own CLAUDE.md / AGENTS.md. The project's rules win when they conflict.
     Keep it short: only things true everywhere. -->

## Always
- Never read, print or edit `.env` files, secrets, keys or credentials. Refer to env variables by name only.
- Never type passwords or log in for me; ask me to sign in.
- Don't commit, push, open PRs or deploy unless I explicitly ask in this session.
- Never run destructive commands (rm -rf outside the project's build folders, drop/delete data, force-push, reset --hard on shared branches) without asking first.
- If the project has its own CLAUDE.md, AGENTS.md, .cursor/rules, CONTRIBUTING.md or style guide, follow it; its conventions beat my preferences.
- Match the existing code style of the file you're editing. Don't reformat files you didn't need to touch.
- Keep changes focused on the task; list unrelated problems instead of fixing them silently.
- Plan first for anything bigger than a small fix and wait for my OK.
- Bugs: reproduce before fixing; if a fix failed twice, stop and measure.

## Reports
Plain English, short: what changed (files), what passed, what you could NOT verify, open questions.

## My personal skills (in ~/.claude/skills)
`/onboard` (map an unfamiliar codebase), `/trace` (follow one flow end to end), `/debug` (reproduce-first bug fixing), `/safe-change` (change risky code safely), `/pr-ready` (check my branch before a PR), `/explain-code` (teach me code line by line).
