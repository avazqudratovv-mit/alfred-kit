# The playbook: building any project with AI

Use this every time you start something new: a web app, a mobile app, an AI tool, anything.
It answers "where do I start?" and "what do I do next?", so you never face a blank page.

The idea in one sentence: **you decide and verify, the AI researches and builds, and the repo remembers.**

---

## The 3 roles

| Who | Does what |
|---|---|
| **You** | Decide what to build, approve plans, test with your own eyes, commit. You are the owner. |
| **Claude chat (in a Project)** | Thinking partner: compares options, writes specs and plans, reviews reports, teaches you. |
| **Claude Code (terminal or VS Code)** | Builder: reads and writes code, runs commands, tests, fixes. |

The repo is the memory. Anything that should survive a chat goes into a file in `docs/ai/`, never only into a chat.

---

## Phase 0 — Idea (1 chat, about 1 hour)

Goal: know exactly what you're building, and why.

1. In Claude chat: describe the problem, who it's for, and your deadline.
2. Ask for 5–8 ideas or approaches, each with: pitch, what makes it special, difficulty, time, free services needed.
3. Pick one. Write `docs/ai/SPEC.md` (template in this kit): users, main flows, what's in v1, what's NOT in v1.

Done when: you can explain the project in 2 sentences, and SPEC.md lists the v1 features.

## Phase 1 — Stack (same chat)

Goal: choose the tools, on purpose.

1. Ask: "Given SPEC.md and my skills (…), which stack? Give 2 options with trade-offs."
2. Prefer what you know, plus ONE new thing you want to learn. Never 3 new things at once.
3. Write the choice and the reason into `docs/ai/DECISIONS.md` (#1).

4. Security from the start: run `/security-docs` (or the same questions in Claude chat) to write `docs/security/SECURITY.md`: rules, who can do what, what data you keep, the 3 most likely ways someone could misuse the app, and the launch checklist. Most fields can say "Planned" for now.

Done when: DECISIONS.md says which language, framework, database and hosting, and why, and SECURITY.md has its first version.

## Phase 2 — Skeleton (Claude Code, day 1)

Goal: an empty project that runs, with the AI set up from the start.

1. Create the repo and run the framework's starter (for example `npx create-next-app`).
2. Copy this kit into it: `AGENTS.md`, `CLAUDE.md`, `.claude/`, `docs/ai/`.
3. Fill in AGENTS.md: what it is, commands, folders, rules. Keep it under 200 lines.
4. `git init`, first commit, push to GitHub.

Done when: `dev`, `build` and `lint` commands work, and AGENTS.md describes them.

## UI-first route (if you like to design first)

This works well with the kit. Do phases 0–2 in a Claude chat (idea, stack) plus your design sample, then:
1. Write `docs/ai/DESIGN.md` (tokens, screens, components) from the design sample, and put the sample images in `docs/design/`.
2. Write `docs/ai/DATA.md`: the data shapes every screen shows and the main API operations. Do this BEFORE the UI. It's what keeps "UI first" from turning into "rewrite everything later".
3. Build the screens with mock data that follows DATA.md exactly (one feature at a time, mobile and desktop).
4. Then build the backend to return exactly those shapes, and swap mock data for real data screen by screen.

## Phase 3 — Plan the work (Claude chat or Claude Code plan mode)

Goal: a list of small, ordered steps.

1. Ask: "Break SPEC.md v1 into features. Order them so each one works end to end before the next."
2. Put them in `docs/ai/ROADMAP.md` as a checklist.
3. Start with the thinnest working slice: one page, one API call, one database table, deployed. Then grow.

Done when: ROADMAP.md has 5–15 features, each small enough for one or two sessions.

## Phase 4 — Build loop (repeat for every feature)

This is where 80% of the time goes. Same loop every time:

1. **Start** — new Claude Code chat → `/start-session` (it reads STATE.md and tells you where you are).
2. **Plan** — `/new-feature <name>`: Claude proposes a plan; you read it and say yes or change it.
3. **Build** — Claude writes the code and tests.
4. **Verify** — Claude runs build, lint and tests, and checks in the browser if it's UI. Then YOU try it yourself. If the feature touches login, private data, payments, uploads or AI: also the two-account test (user B must not reach user A's data, even with the exact ID).
5. **Review** — `/review`: Claude checks the diff. Then you skim the diff yourself.
6. **Commit** — you commit, with a clear message.
7. **End** — `/end-session`: Claude updates STATE.md, DECISIONS.md and BACKLOG.md.

Bugs: always `/fix-bug` — reproduce first, fix second, prove third.

Rules for the loop:
- One feature per chat. When the topic changes, start a new chat (or `/clear`).
- Small commits. Never a commit you haven't looked at.
- If Claude guessed twice and it's still broken: stop guessing, make it reproduce and measure.

## Phase 5 — Learn while you build

AI builds faster than you can read, so learning has to be on purpose:

- After each feature: `/explain <file or flow>` and read it line by line.
- Write 3 lines in `docs/ai/LEARNING.md`: what you learned, what confused you, one interview sentence.
- Once a week: rebuild one small part yourself without AI.
- When something new appears (a library, a term), search it for 10 minutes and add a line to LEARNING.md.

You don't need to know everything up front. You learn the parts the project needs, when it needs them.

## Phase 6 — Ship

1. Security: run `/security-review`, fix every Critical and High, and tick the launch checklist in `docs/security/SECURITY.md` (secrets only on the server, minimal database rights, HTTPS, headers, CORS, rate limits, debug off, dependency audit, no secrets in git history).
   Then the rest: env variables documented, error pages, demo data.
2. Deploy (Docker + VPS, or a platform like Vercel/Render/Fly). Write the steps into a `/deploy` skill so the next deploy is one command.
3. README: what it is, screenshots, live link, demo accounts, stack, what's not done.

Repeat `/security-review` after every big feature and before every release, not only the first launch.

## Phase 7 — Look back (30 minutes)

In LEARNING.md: what went well, what was slow, what you'd do differently. Improve this playbook and the kit with it.

---

## When you feel lost

Ask yourself, in this order:
1. What does SPEC.md say v1 needs? (scope)
2. What's the next unchecked item in ROADMAP.md? (next step)
3. What does STATE.md say is in progress? (current step)
4. Still unsure? Ask Claude chat: "Here is STATE.md and ROADMAP.md. What should I do next, and why?"

Feeling overwhelmed by how wide tech is, is normal. Nobody knows it all. Developers who use AI well don't know more tools; they follow a process like this one and learn what the project needs, step by step.
