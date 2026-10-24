# Joining an existing project (a job, a startup, someone else's repo)

The idea in one sentence: **their project, their rules — your AI setup stays personal, local and out of their git.**

---

## Day 0 — before you touch AI at work

Ask your lead or check the handbook. Get answers to these 5 questions:

| Question | Why it matters |
|---|---|
| Are AI coding tools allowed? Which ones? | Some companies ban them, some allow only one (Copilot, Cursor, Claude via company account). |
| Company account or personal account? | Company code in a personal account can break your contract and leak code. |
| Can AI read the whole repo, or only some parts? | Some repos (payments, client projects, game IP under NDA) are off-limits. |
| Is there an existing AI setup (CLAUDE.md, AGENTS.md, .cursor/rules)? | You follow it instead of bringing your own. |
| Can AI-written code be committed? Any labeling rules? | Some teams require "AI-assisted" in the PR or forbid certain uses. |

**If the answer is "no AI":** follow it. You can still use Alfred for general learning (concepts, docs, your own practice code) — never paste company code there.

**Never, in any company:** paste company code, internal docs, customer data, keys or credentials into a personal AI chat. Describe the problem in general terms instead ("a NestJS guard that returns 403 for valid tokens").

---

## Week 1 — understand before you change

1. Get it running locally: follow README / onboarding doc. Write down every step that was missing or wrong — that's your first useful contribution (a docs PR).
2. In Claude Code (company-approved): `/onboard` → a map of the codebase.
3. Pick the area of your first ticket: `/trace <the flow>`.
4. Read the last 20 merged PRs: how big they are, how they're described, what reviewers comment on.
5. Write your private notes in `CLAUDE.local.md` (template in this folder) — commands, people, gotchas.
6. Ask questions early. "I spent 30 min on X, here's what I tried" is always welcome.

## Every ticket after that

1. Read the ticket. Unclear? Ask before coding.
2. `/trace` the area if new to you.
3. Bug → `/debug`. Change in risky code → `/safe-change`. Feature → plan mode first, then build.
4. Small PRs. One ticket = one branch = one PR.
5. `/pr-ready` → fix → open PR yourself.
6. You must be able to explain every line in your PR. If you can't, `/explain-code` until you can. Reviewers will ask.

---

## The 4 situations

### A. The project already has an AI setup
- Use theirs. Don't add your own CLAUDE.md, rules or skills to the repo.
- Your personal layer: `~/.claude/CLAUDE.md` + `~/.claude/skills/` (loaded on your machine only) and a gitignored `CLAUDE.local.md`.
- If their setup misses something useful, suggest it in a small PR or to the lead — don't change it on your own.

### B. AI is allowed but there's no setup
- Work with your personal layer only for the first weeks.
- Once you know the codebase, offer the team a short AGENTS.md (use `new-project/AGENTS.md` as a starting point). Ask first; it becomes a team file.
- Keep it short and factual: commands, folders, rules. No personal style.

### C. Startup / greenfield inside a team
- Use `new-project/` as a base, but agree on it with the team before committing.
- Security docs (`docs/security/SECURITY.md`) are an easy win at startups — usually nobody has written one.

### D. Game company / unusual stack (Unity, Unreal, Godot, C++, C#)
- Big binary assets: AI can't read scenes, prefabs or blueprints well. Focus it on scripts (C#, C++, GDScript) and tooling.
- Generated files and engine folders (Library/, Intermediate/, Binaries/, .import/) — tell Claude to never edit them; add them to your personal rules or `CLAUDE.local.md`.
- Performance matters more: ask for the cost of a change (allocations per frame, draw calls), not just "does it work".
- Game IP is very sensitive (unreleased game, story, art). Assume the strictest AI policy until told otherwise.
- Backend/live-ops/tools teams in game companies use normal web stacks — your NestJS/Next.js skills transfer directly.

---

## What goes where

| Where | What | In company git? |
|---|---|---|
| Repo `CLAUDE.md` / `AGENTS.md` / `.claude/` | The team's setup | Yes (team's files) |
| Repo `CLAUDE.local.md` | Your notes for this repo | **No** — must be in `.gitignore` (or `.git/info/exclude`) |
| `~/.claude/CLAUDE.md` | Your rules for every project | No (your machine) |
| `~/.claude/skills/` | Your personal skills | No (your machine) |
| Alfred chat | Learning, career, your own projects | Never company code |

If the repo's `.gitignore` doesn't list `CLAUDE.local.md`, add it to `.git/info/exclude` instead (local only, doesn't change their files):
```
echo "CLAUDE.local.md" >> .git/info/exclude
```

---

## Red flags — stop and ask
- You're about to run something against a shared/staging/production database.
- A migration, a force-push, or deleting a branch that isn't yours.
- The AI wants to change CI, auth, payments or infra config for a "small" ticket.
- You can't explain why the fix works.
