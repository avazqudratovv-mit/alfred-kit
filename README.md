# alfred-kit

My setup for working with AI as a developer: a mentor persona, personal Claude Code rules and skills, a playbook for joining existing projects, and a starter kit for new ones.

**New here? Read [HOW-TO-USE.md](HOW-TO-USE.md).**

## What's inside

| Folder | What it's for | Where it goes |
|---|---|---|
| `alfred/ALFRED.md` | The Alfred persona: my technical partner in Claude chat | Claude Project custom instructions (or paste into a new chat) |
| `personal/CLAUDE.md` | My rules for every project | `~/.claude/CLAUDE.md` |
| `personal/skills/` | `/onboard`, `/trace`, `/debug`, `/safe-change`, `/pr-ready`, `/explain-code` | `~/.claude/skills/` |
| `existing-project/` | Playbook for joining a team/project + private notes template | Read it; copy `CLAUDE.local.md.example` into a repo |
| `new-project/` | Starter kit for my own projects (playbook, AGENTS.md, skills, docs, security) | Copy into a new repo |

## Setup on a new computer (2 minutes)

```bash
git clone https://github.com/<you>/alfred-kit.git ~/alfred-kit
mkdir -p ~/.claude/skills
cp ~/alfred-kit/personal/CLAUDE.md ~/.claude/CLAUDE.md      # careful: replaces an existing one
cp -r ~/alfred-kit/personal/skills/* ~/.claude/skills/
```
Then restart Claude Code. Type `/` to see the skills.

## Alfred (Claude chat)
1. claude.ai → Projects → New project → name it **Alfred**.
2. Paste everything below the `---` in `alfred/ALFRED.md` into the project instructions.
3. Start every technical chat inside that project.

## Which one do I use?

| Situation | Use |
|---|---|
| My own new project | `new-project/` → follow its PLAYBOOK |
| New job / joining a repo | `existing-project/PLAYBOOK.md` → company AI policy first |
| Learning, career, planning | Alfred chat |
| Any repo, any day | personal skills (`/debug`, `/pr-ready`, ...) |

## Rules this kit follows
- No secrets, no personal data, no company code in this repo.
- In a company repo, the team's rules and AI policy win over anything here.
