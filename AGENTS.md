# Radxa Skills Repository Guide

本仓库是面向 agent 的 Radxa SBC skill 集合。读取时遵循最小上下文原则，不要一次性加载整个仓库。

## 读取流程

1. 先读取 `catalog/skills.yaml`
2. 先判断任务属于通用 skill 还是型号专属 skill
3. 进入对应目录查找目标 skill
4. 只打开目标 `SKILL.md`
5. 只有在 `SKILL.md` 明确引用时，再读取 `references/` 或 `scripts/`

`catalog/skills.yaml` 是发现已有 skill 的权威入口。如果某个 skill 存在于 `skills/` 中但未登记到 catalog，应视为仓库维护不完整并优先补齐。

## 目录规则

- `skills/common/<skill-id>/`
- `skills/models/<board>/<skill-id>/`

## 选择规则

- 多个型号都适用的能力，归入 `skills/common/`
- 明确依赖某个板型硬件差异的能力，归入 `skills/models/<board>/`
- 如果仓库中没有对应 skill，直接说明缺口，不要臆造 skill 内容

## 安全边界

- 默认优先只读、低风险命令
- 未经用户明确同意，不执行刷机、分区、格式化、覆盖 bootloader、改写 EEPROM 等高风险操作
- 未确认具体板型前，不假设接口能力或硬件配置
