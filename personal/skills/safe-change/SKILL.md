---
name: safe-change
description: Make a change in code I don't fully know without breaking things: find who depends on it, plan, change small, verify.
argument-hint: [the change I need to make]
disable-model-invocation: true
---

Change: $ARGUMENTS

1. Impact first: find every place that uses the code I'll touch (search callers, imports, GraphQL/REST consumers, config, tests, other services). List them.
2. Check how it's tested today. If there's no test for the current behavior, propose one to write FIRST so we know we didn't break it.
3. Plan: the smallest set of edits, in order, and the risk of each. Mention anything that needs a migration, a feature flag, or a coordinated deploy. Wait for my OK.
4. Change in small steps, matching the existing style. No drive-by refactors or reformatting.
5. Verify: run tests, lint, type check and build for the affected parts; test the main flow manually or with Playwright if it's UI.
6. Report: files changed, callers checked, tests run and results, risks left, what to tell the reviewer. Don't commit.
