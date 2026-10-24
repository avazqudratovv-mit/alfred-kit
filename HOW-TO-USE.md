# How to use alfred-kit

A practical guide: what to do, when, and in what order.

---

## 1. One-time setup (on every computer)

### Download the kit
```bash
git clone https://github.com/avazqudratovv-mit/alfred-kit.git ~/alfred-kit
```
The private Alfred file isn't on GitHub. Copy `ALFRED.private.md` from your backup (iCloud or a private repo) into `~/alfred-kit/alfred/`.

### Install personal rules and skills
```bash
ls ~/.claude/CLAUDE.md
```
- **"No such file":**
  ```bash
  mkdir -p ~/.claude/skills
  cp ~/alfred-kit/personal/CLAUDE.md ~/.claude/CLAUDE.md
  cp -r ~/alfred-kit/personal/skills/* ~/.claude/skills/
  ```
- **The file already exists:** don't overwrite it. Open both files and merge them by hand. Then copy only the skills:
  ```bash
  mkdir -p ~/.claude/skills
  cp -r ~/alfred-kit/personal/skills/* ~/.claude/skills/
  ```

### Check that it worked
Restart Claude Code in any folder and type `/`. You should see `onboard`, `trace`, `debug`, `safe-change`, `pr-ready` and `explain-code`.

### Set up Alfred (Claude chat)
1. On claude.ai, go to **Projects → New project** and name it **Alfred**.
2. Open `alfred/ALFRED.private.md` and copy everything below the `---` line.
3. Paste it into the project's **instructions**.
4. Test it: start a chat in the project and ask "who are you?".

---

## 2. Which tool for which job

| I want to… | Use | Where |
|---|---|---|
| Plan, compare options, learn, prepare for an interview, review a Claude Code report | **Alfred** | Claude chat, Alfred project |
| Write or change code, run commands, test | **Claude Code** | VS Code or terminal, inside the repo |
| Start my own new project | **new-project/** | Copy it into the new repo |
| Join a project at a job or a startup | **existing-project/PLAYBOOK.md** | Read it before day 1 |

The simple rule: **Alfred thinks, Claude Code builds, you decide and commit.**

---

## 3. Working with Alfred (the chat loop)

1. Tell Alfred what you want ("add a payment page to Indesk").
2. Alfred asks questions or gives you options. Pick one.
3. Alfred writes a **Claude Code prompt** for you.
4. Paste the prompt into a **fresh** Claude Code chat in the right repo.
5. Copy Claude Code's **report** back to Alfred.
6. Alfred checks the report, tells you what to test, and gives you the commit commands.
7. Test it yourself, then commit.

Tips:
- One topic per chat. When a chat gets long, ask Alfred for a "handoff summary" and start a new chat with it.
- Add useful files to the Alfred project: your CV, job ads, project notes.
- Never paste passwords, API keys, `.env` values or company code into chat. If you do by accident, rotate the key right away.

---

## 4. The personal skills (any repo)

Type these in Claude Code. The text after the command is what you want.

| Command | When | Example |
|---|---|---|
| `/onboard` | First day in a codebase you don't know | `/onboard the payments module` |
| `/trace` | "How does this work?" One flow, from start to finish | `/trace user buys a ticket` |
| `/debug` | Something is broken | `/debug checkout returns 500 after clicking Pay, should show success` |
| `/safe-change` | A change in code you don't fully know | `/safe-change rename the price field to amount` |
| `/pr-ready` | Before opening a pull request | `/pr-ready main` |
| `/explain-code` | Learn a file line by line | `/explain-code src/auth/jwt.guard.ts` |

`/onboard`, `/trace` and `/explain-code` only read code. `/debug` and `/safe-change` change it, but never commit.

---

## 5. Starting your own new project

1. Create the project, for example `npx create-next-app@latest my-app`.
2. Copy the kit into it:
   ```bash
   cp -r ~/alfred-kit/new-project/. ~/my-app/
   ```
3. Add these lines to `.gitignore`: `.env`, `.env.*`, `!.env.example`, `CLAUDE.local.md`.
4. In Claude Code, have it fill in `AGENTS.md` (the exact prompt is in `new-project/README.md`).
5. Follow `new-project/PLAYBOOK.md`: Idea → Stack → Skeleton → Plan → Build loop → Learn → Ship.

The daily commands for that project are `/start-session`, `/new-feature`, `/fix-bug`, `/review` and `/end-session`. Run `/security-review` before every deploy.

---

## 6. Joining a project at a job

**Before using AI on company code**, ask:
1. Are AI tools allowed? Which ones?
2. Company account or personal account?
3. Is there already an AI setup in the repo (CLAUDE.md, AGENTS.md, .cursor/rules)?

Then:
1. **Week 1:** get the project running, then use `/onboard` and `/trace` to learn it. Read recent pull requests.
2. **Private notes:** copy `existing-project/CLAUDE.local.md.example` into the repo as `CLAUDE.local.md`, then keep it out of git:
   ```bash
   echo "CLAUDE.local.md" >> .git/info/exclude
   ```
3. **Every ticket:** use `/debug` or `/safe-change`, then `/pr-ready`, then open the PR yourself.
4. **Never** commit your personal files into the company repo, and never paste company code into Alfred.

The full guide, including game companies and startups, is in `existing-project/PLAYBOOK.md`.

---

## 7. Keeping the kit up to date

When you improve a skill or a rule:
```bash
cd ~/alfred-kit
# edit the files
git add . && git commit -m "Improve debug skill" && git push
```
Copy the changed files into `~/.claude/` again, using the commands from section 1.

On another computer, run `git pull` in `~/alfred-kit` and copy the files again.

Update "About me" in `ALFRED.private.md`, and in the Alfred project instructions, whenever your situation changes: a new job, new skills, new projects.

---

## 8. Something isn't working?

| Problem | Fix |
|---|---|
| Skills don't show when I type `/` | Check that `~/.claude/skills/<name>/SKILL.md` exists, then restart Claude Code. |
| Alfred doesn't act like Alfred | The chat isn't inside the Alfred project, or the instructions are empty. |
| `ALFRED.private.md` shows up in `git status` | Don't commit. Check that `.gitignore` has `*.private.md`. |
| Claude Code reads `.env` | Check that `.claude/settings.json` in the repo has the deny rules (they're in new-project). |
