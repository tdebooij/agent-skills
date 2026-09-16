# agent-skills

Personal library of AI agent skills — reusable instructions that extend Claude, Codex, and other skill-aware agents with my own workflows and conventions.

---

## What is a Skill?

A skill is a small package that loads context and instructions into an AI agent on demand. When a task matches a skill's description, the agent pulls in the relevant knowledge — conventions, step-by-step workflows, reference material — without it needing to be re-explained every time.

Skills live in `.agents/skills/<name>/` inside a project, or globally in `~/.agents/skills/` (or the agent's own global skills directory, e.g. `~/.claude/skills/` for Claude Code).

---

## Available Skills

| Skill | Description | Install |
|-------|-------------|---------|
| `tim-pr-review` | Personal PR review workflow — checks a PR against the `9to5-web-dev` skill's conventions plus general correctness, security, and overengineering concerns, then walks through issues one at a time in severity order with fix options. | `npx skills add tdebooij/agent-skills@tim-pr-review` |

> New skills added to this repo will appear here.

---

## Installing a Skill

Skills are installed using the [`skills` CLI](https://skills.sh):

```bash
npx skills add tdebooij/agent-skills@<skill-name>
```

### Project-level install

Installs into the current project so the skill is versioned alongside the repo:

```bash
cd your-project
npx skills add tdebooij/agent-skills@tim-pr-review --agent universal --yes
```

### Global install

Installs the skill for every project on this machine:

```bash
npx skills add tdebooij/agent-skills@tim-pr-review -g
```

### Keeping skills up to date

```bash
# See which installed skills have updates available
npx skills check

# Update everything
npx skills update
```

Re-running `add` on an installed skill replaces the local copy with the latest version from this repo.

---

## Repository Structure

```
agent-skills/
└── .agents/
    └── skills/
        └── <skill-name>/
            ├── SKILL.md          ← required: frontmatter + instructions
            ├── scripts/          ← optional: helper scripts
            ├── references/       ← optional: reference docs loaded on demand
            └── assets/           ← optional: templates, images, boilerplate files
```

Every skill has a `SKILL.md` with a YAML frontmatter block:

```yaml
---
name: skill-name
description: "What this skill does and when the agent should use it."
---
```

The directory name and frontmatter `name` must match. The `description` is the primary trigger — it should match the kinds of questions or tasks that make the skill relevant.

---

## Adding a New Skill

1. Scaffold it with the `skill-creator` skill (`npx skills add skill-creator -g`, then ask your agent to create a skill), or write `SKILL.md` by hand.
2. Place it at `.agents/skills/<skill-name>/`.
3. Add a row to the [Available Skills](#available-skills) table above.
4. Commit and open a PR.

---

## Getting Help

- **Browse the open skills ecosystem:** [skills.sh](https://skills.sh)
- **Search for existing skills:** `npx skills find [query]`
- **Skills CLI docs:** `npx skills --help`
