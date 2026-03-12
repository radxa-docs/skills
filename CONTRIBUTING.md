# Contributing

欢迎为 Radxa SBC 场景贡献 skill。

## 新增 skill 的最低要求

1. 先判断该 skill 属于通用 skill 还是型号专属 skill
2. 在对应目录创建 skill：
   - `skills/common/<skill-id>/`
   - `skills/models/<board>/<skill-id>/`
3. 添加 `SKILL.md`
4. 在 frontmatter 中至少提供：
   - `name`
   - `description`
5. 在 `catalog/skills.yaml` 中登记该 skill

## 推荐做法

- 先参考 `templates/skill/`
- 把核心流程写在 `SKILL.md`
- 把长篇参考内容放到 `references/`
- 把可复用命令流程写到 `scripts/`
- 新增或移动 skill 后，同步更新 `catalog/skills.yaml`

## 安全要求

- 默认不要包含 destructive 操作
- 涉及刷写镜像、修改分区表、更新 bootloader 的内容时，必须明确前置确认条件
