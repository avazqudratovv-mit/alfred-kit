# Security

<!-- One file, five parts. Small project: keep everything here. Big project: split each part into its own file
     in docs/security/ (rules.md, auth.md, data.md, threats.md, checklist.md).
     Written with /security-docs in phase 1; checked with /security-review before every deploy.
     The golden rule of this file: a control is only "Done" when it has a test that passed.
     Status values: Planned → Built → Tested (date). -->

Updated: <YYYY-MM-DD>

## 1. Rules every feature follows

| # | Rule | Enforced where | Test | Status |
|---|---|---|---|---|
| R1 | Never trust the client: prices, totals, roles, user IDs, limits are decided on the server | <service layer> | Send a modified request (role=admin, price=1) → server ignores it | Planned |
| R2 | Every input is validated on the server (type, length, range, format) | <DTOs / zod schemas> | Send wrong types and huge strings → 400 with a code | Planned |
| R3 | Database queries never build strings from user input | <ORM / query builder> | Send `{"$gt":""}` / `' OR 1=1` in fields → no data leak | Planned |
| R4 | Secrets live only in server env; nothing secret in `NEXT_PUBLIC_*` / `VITE_*` / the mobile bundle | <env config> | Search the built frontend bundle for key patterns → none | Planned |
| R5 | Uploads: allowed types, size limit, stored outside the code folder, served with safe headers | <upload middleware> | Upload a .html / 50 MB file → rejected | Planned |
| R6 | Expensive actions (login, signup, AI, uploads, emails) are rate-limited per user and per IP | <rate limiter> | 30 login attempts in a minute → 429 | Planned |
| R7 | Errors return a code, never stack traces or internal messages | <error filter> | Trigger a server error → only `{code}` reaches the browser | Planned |

## 2. Who can do what (auth)

Login: <email + password with bcrypt / OAuth provider / ...>. Session: <JWT in ..., expires after ...>.

| Role | View | Create | Change | Delete |
|---|---|---|---|---|
| Visitor | <public pages> | <account> | — | — |
| User | <own records> | <...> | <own records> | <own account> |
| Admin | <everything> | <...> | <...> | <...> |

Per-record rule: the server checks **ownership** (record.ownerId === current user) on every read and write, not only the role.

Account lifecycle: sign-up → <verification?> → active → suspended/deleted. What happens to existing sessions when access is removed: <...>. Password reset: <...>.

Tests (two-account test, always):
- [ ] User A can read and change A's record.
- [ ] User B gets "not found/forbidden" for A's record, even with the exact ID or URL.
- [ ] A suspended or deleted user's old token is refused.
- [ ] A normal user calling an admin action is refused by the server (hiding the button is not enough).

## 3. Data we keep

| Data | Why we need it | Where (incl. copies: logs, backups, previews, 3rd parties) | Who can access | Deleted when |
|---|---|---|---|---|
| <email> | <login> | <DB members collection> | <user, admin> | <account deletion + backup expiry> |
| <password> | <login> | <bcrypt hash only> | <nobody can read it> | <account deletion> |
| <uploaded file> | <...> | <disk / bucket, thumbnails> | <owner, admin> | <...> |

Rules: passwords hashed (never encrypted or logged); tokens, passwords and private content never written to logs; database user has the minimum rights on one database; backups noted with how long they live.

## 4. What could go wrong (threat model)

Start with the 3 most realistic ways to misuse THIS app. Add more as it grows.

| Risk | Why it matters | Protection | Test | Owner | Status |
|---|---|---|---|---|---|
| <User changes an ID in a request to read someone else's order> | <private data leak> | <ownership check in OrderService> | <two-account test> | <me> | Planned |
| <Bot hammers the AI endpoint> | <bill / quota used up> | <per-user + global daily cap, rate limit> | <script 100 calls → capped> | <me> | Planned |
| <Stolen token used after password change> | <account takeover> | <token version / short expiry> | <old token → 401> | <me> | Planned |

Keep "possible risks" and "weaknesses actually found in the code" separate. Found weaknesses also go to BACKLOG.md as bugs.

## 5. Before every launch

- [ ] `/security-review` run, no Critical/High left open
- [ ] Dependency audit (`npm audit --omit=dev` / `yarn npm audit`), no critical issues in runtime packages
- [ ] No secrets in git history (`gitleaks detect` or GitHub secret scanning on)
- [ ] `.env` files only on the server, `chmod 600`; `.env.example` has names only
- [ ] HTTPS only; security headers (helmet: HSTS, no sniff, frame options, CSP where possible)
- [ ] CORS allows only the real site origin(s)
- [ ] Database: own user, minimum rights, IP allowlist; dev and prod databases separate
- [ ] Ports: only 80/443 (and SSH) open; app ports bound to 127.0.0.1
- [ ] Rate limits on login, signup, password, AI, uploads
- [ ] Debug off in production: no source maps served, no GraphQL playground/introspection if not needed, no stack traces
- [ ] Demo/test accounts have strong passwords; admin password unique
- [ ] Backups: what's backed up, how often, a restore tested once

## Open questions
- <...>
