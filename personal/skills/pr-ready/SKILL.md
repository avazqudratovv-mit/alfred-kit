---
name: pr-ready
description: Check my branch before I open a pull request: diff review, tests, leftovers, and a PR description draft.
argument-hint: [optional: the base branch, default main]
disable-model-invocation: true
---

Base branch: $ARGUMENTS (default: the repo's default branch)

1. Read the project's PR rules (CONTRIBUTING.md, PR template in .github/, CLAUDE.md/AGENTS.md).
2. Show `git diff <base>...HEAD --stat` and review the full diff for:
   - bugs, missing edge cases, missing error handling
   - security: secrets, missing auth/ownership checks, trusting client input, unsafe queries
   - leftovers: console.log/print, debug code, commented-out code, TODOs I added, unrelated file changes, formatting-only noise
   - style that doesn't match the codebase
3. Run the project's lint, type check, tests and build. Report pass/fail.
4. Check the branch is up to date with the base; warn about conflicts (don't rebase without asking).
5. Draft the PR description in the project's template (or: What / Why / How to test / Screenshots / Risks).
6. Give a verdict: Ready, or a numbered list of what to fix first. Don't commit, push or open the PR.
