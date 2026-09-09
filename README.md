# skills

Personal [Agent Skills](https://agentskills.io) collection, in the layout the [`skills` CLI](https://github.com/vercel-labs/skills) discovers: each skill is a directory under `skills/` containing a `SKILL.md` with YAML frontmatter (`name`, `description`).

## Install a skill from this repo

```bash
# from GitHub (after pushing)
npx skills add <you>/skills --skill subagent-impl -g

# or from a local clone
npx skills add ./skills --skill subagent-impl -g
```

## Skills

| Skill | What it does |
| --- | --- |
| [`subagent-impl`](skills/subagent-impl/SKILL.md) | Downstream of `to-spec`/`to-tickets`: dispatch one subagent per ticket, strictly serially in ticket order, verifying each before the next. |
