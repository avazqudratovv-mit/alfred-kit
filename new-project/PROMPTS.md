# Prompt templates

Copy, fill in the <...>, paste. Every good prompt has the same 4 parts:
**goal**, **context**, **rules**, **done when**.

---

## 1. New feature (Claude Code)
```
Goal: <what the user can do after this, in one sentence>.
Context: <where in the app; related files or features; screenshots if UI>.
Rules: follow AGENTS.md; don't commit; <anything special, e.g. "no new dependencies">.
Plan first and wait for my OK.
Done when: <concrete checks, e.g. "a buyer can pay with any 16 digits; 17th digit is ignored; works at 360 px; all 4 languages">.
```
(or just: `/new-feature <one sentence>`)

## 2. Bug (Claude Code)
```
Bug: <what happens> on <page/URL>, as <role>, on <phone/desktop>.
Expected: <what should happen>.
Steps: 1) ... 2) ... 3) ...
Evidence: <screenshot / recording / error text / log lines>.
Reproduce it first, explain the cause, then fix and prove it. Don't commit.
```
(or: `/fix-bug <the same text>`)

## 3. Choose between options (Claude chat)
```
I need to decide <what>. Context: <project, my skills, deadline, budget>.
Give me 2–4 options, each with pros, cons, effort and risk. Recommend one and say why.
Ask me questions first if something important is missing.
```

## 4. Review a report from Claude Code (Claude chat)
```
Here is Claude Code's report for <task>. Check it against what I asked (<paste the prompt>).
Tell me: is anything missing, risky or unverified? What should I test myself? What's the commit message?
```

## 5. Learn something (Claude chat or /explain)
```
Teach me <topic> using my real code in <file/flow>. I'm a beginner.
Line by line, plain English, and end with 3 questions to check me.
```

## 6. Start a new project (Claude chat)
```
I want to build <idea or problem>. I know <skills>. Deadline <date>. Free tiers only.
Phase 0 of my playbook: give me 5–8 approaches (pitch, what's special, difficulty, time, services).
Then help me write SPEC.md for the one I pick.
```

## 7. Hand off to a new chat
```
Read docs/ai/STATE.md, ROADMAP.md and the last 5 DECISIONS.md entries. Summarize where we are in 10 lines, then wait.
```
(or: `/start-session`)
