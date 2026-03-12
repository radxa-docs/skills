# Radxa Skills

这是一个面向 Radxa SBC 用户与 agent 的 skills 仓库，用于沉淀可被 agent 直接读取和复用的业务 skill。

仓库的基本组织方式分两类：

- 通用 skill
- 型号专属 skill

## 仓库结构

```text
.
├── AGENTS.md
├── CONTRIBUTING.md
├── catalog/
│   └── skills.yaml
├── templates/
│   └── skill/
│       ├── SKILL.md.example
│       └── agents/
│           └── openai.yaml.example
└── skills/
    ├── common/
    └── models/
```

## 目录约定

- `skills/common/<skill-id>/`
  适合放多款 Radxa SBC 可复用的 skill
- `skills/models/<board>/<skill-id>/`
  适合放某个具体型号专属的 skill

## Agent 读取方式

1. 先读取 `catalog/skills.yaml`
2. 根据任务判断应使用通用 skill 还是型号专属 skill
3. 找到目标 skill 后，只打开对应 `SKILL.md`
4. 只有在 `SKILL.md` 明确引用时，再读取 `references/` 或 `scripts/`

## 索引说明

`catalog/skills.yaml` 是仓库的机器可读索引。agent 或工具应优先通过它发现 skill，而不是盲扫整个仓库。

README 不维护具体 skill 清单。随着 skill 增长，实际可用项应以 `catalog/skills.yaml` 为准。
