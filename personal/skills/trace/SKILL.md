---
name: trace
description: Follow one feature or request through the code end to end, from the user action to the database and back. Read-only.
argument-hint: [the flow, e.g. "user buys a ticket" or "POST /orders"]
disable-model-invocation: true
---

Trace this flow: $ARGUMENTS

Read-only. Don't change code.

1. Start where the user acts (button, route, API call, game input, cron job).
2. Follow every hop in order: UI → API call → route/resolver/controller → service → database/queue/external service → response → UI update.
3. For each hop: file:line, function name, and one plain sentence of what it does. Note checks done (auth, validation, ownership).
4. Draw the flow as a short numbered list or a small text diagram.
5. Point out: where errors are handled (or not), where the data shape changes, side effects (emails, events, caches), and anything that looks wrong or risky.
6. End with 3 questions to check my understanding.
