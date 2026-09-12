# skills

My personal [Agent Skills](https://agentskills.io) collection, in the layout the [`skills` CLI](https://github.com/vercel-labs/skills) discovers: each skill is a directory under `skills/` containing a `SKILL.md` with YAML frontmatter (`name`, `description`).

Repo: <https://github.com/YeEeck/skills> — public, so `npx skills add` works with no authentication.

## Install a skill from this repo

```bash
# from GitHub: one skill, into your user directory
npx skills add YeEeck/skills --skill subagent-impl -g

# both skills at once
npx skills add YeEeck/skills --skill subagent-impl --skill design-talk -g

# see what's available without installing anything
npx skills add YeEeck/skills --list

# from a local clone (run from the repo root)
npx skills add . --skill subagent-impl -g
```

Drop `-g` to install into the current project (`./.claude/skills/`, `./.agents/skills/`, …) instead of your user directory. `-a <agent>` picks a specific target agent, and `-y` skips the prompts (handy in scripts). Add `--skill '*'` to pull every skill in the repo.

## Update / remove

```bash
npx skills update subagent-impl   # re-pull the latest commit of an installed skill
npx skills remove subagent-impl   # uninstall
```

## Skills

| Skill | What it does |
| --- | --- |
| [`subagent-impl`](skills/subagent-impl/SKILL.md) | `to-spec`/`to-tickets` 的下游：每张票派发一个子代理（实施纪律内联进 prompt，不点名其他技能），严格按票据顺序串行推进，逐票验收，全部完成后用 `code-review` 做全量终审。**user-invoked，只能手动点名调用**（`/subagent-impl`），不会自发触发。 |
| [`design-talk`](skills/design-talk/SKILL.md) | 需求导入后的设计讨论：陪伴式共同探索，把需求的运作逻辑与数据流画成链路图、一次铺开全部断点、只深挖最上游那条；冲突用枚举加代价对比处置，收尾做一次闭环核查。**方向确认之前不派发子代理查询**——链路图铺开后拿一句廉价的问题换用户点头，确认到手才给清单与押注、等他回应后才派发（用户点名要查的除外）；派发之后冻结到整批返回。产出落 `docs/design-talk/`，只理清思绪、不落决定、不动代码。**user-invoked，只能手动点名调用**（`/design-talk`），不会自发触发。 |
