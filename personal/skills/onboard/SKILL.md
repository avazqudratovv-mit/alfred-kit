---
name: onboard
description: Map an unfamiliar codebase for me: what it is, how it runs, where things live, and its existing AI setup. Read-only.
argument-hint: [optional: the area I'll work on first]
disable-model-invocation: true
---

I'm new to this codebase. Focus area (optional): $ARGUMENTS

Read-only: don't change, install, run migrations or start anything that writes data. Never open `.env` or secret files.

1. Existing rules first: read CLAUDE.md, AGENTS.md, .cursor/rules, .github/copilot-instructions.md, CONTRIBUTING.md, README, docs/. Summarize what they require. These beat my personal rules.
2. What it is: one paragraph — product, users, main features.
3. Stack: languages, frameworks, database, hosting, key libraries (from package.json / requirements / go.mod / .csproj / engine project files).
4. How to run: install, dev, test, lint, build commands. Which env variable NAMES are needed (from .env.example or config code).
5. Map: the top folders and what each holds, in a table. Where requests enter, where data is stored, where the UI lives.
6. Conventions: naming, file structure, state management, error handling, test style, commit/branch style (from git log).
7. Risky areas: auth, payments, migrations, generated code, anything marked "do not edit".
8. For the focus area: the 5–10 files I should read first, in order, and why.
9. Questions I should ask my team (things the code can't answer).

Report in plain English. Don't commit.
