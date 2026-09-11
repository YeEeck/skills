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
| [`subagent-impl`](skills/subagent-impl/SKILL.md) | `to-spec`/`to-tickets` 的下游：每张票派发一个子代理（实施纪律内联进 prompt，不点名其他技能），严格按票据顺序串行推进，逐票验收，全部完成后用 `code-review` 做全量终审。**user-invoked，只能手动点名调用**（`/subagent-impl`），不会自发触发。 |
| [`design-talk`](skills/design-talk/SKILL.md) | 需求导入后的设计讨论：陪伴式共同探索，把需求的运作逻辑与数据流画成链路图、一次铺开全部断点、只深挖最上游那条；冲突用枚举加代价对比处置，收尾做一次闭环核查。产出落 `docs/design-talk/`，只理清思绪、不落决定、不动代码。**user-invoked，只能手动点名调用**（`/design-talk`），不会自发触发。 |
