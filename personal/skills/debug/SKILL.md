---
name: debug
description: Fix a bug in any codebase by reproducing it first, finding the real cause, then fixing and proving it.
argument-hint: [what goes wrong, where, and what should happen]
disable-model-invocation: true
---

Bug: $ARGUMENTS

1. Follow the project's own rules (CLAUDE.md / AGENTS.md / CONTRIBUTING.md) for tests and style.
2. Reproduce before changing anything: a failing test, a script, curl, Playwright, logs. Write the exact steps and what you saw. If you can't reproduce it, stop and ask me for details; don't guess.
3. Cause: explain in plain words why it happens, with file:line. Check git log/blame for when and why that code changed.
4. Fix the cause, not the symptom. Smallest change that matches the existing style.
5. Prove it: repeat step 2 and show it's gone. Add a regression test if the project has tests.
6. Run the project's test and lint commands for the touched area.
7. Same mistake elsewhere? List it, don't fix it without asking.
8. Report: cause, fix (files), evidence before/after, what you couldn't verify. Don't commit.
If two fixes failed: stop, add logging or measurements, and show me the data before trying a third.
