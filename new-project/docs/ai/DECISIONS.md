# Decisions

<!-- Every non-obvious choice: what, why, and what you didn't choose.
     This is how a future chat (and future you) understands WHY the code looks the way it does.
     Newest at the bottom. Never delete; if a decision changes, add a new one that replaces it. -->

| # | Date | Decision | Why | Rejected alternatives |
|---|---|---|---|---|
| 1 | <YYYY-MM-DD> | <Stack: Next.js + NestJS + MongoDB> | <I know NestJS; MongoDB fits nested event data> | <Django (new language, deadline)> |
| 2 | <YYYY-MM-DD> | <JWT in localStorage, not cookies> | <Simple for a demo; no cross-site cookie setup> | <httpOnly cookie (safer, more setup)> |
