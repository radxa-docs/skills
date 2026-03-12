---
name: mdmaker-deploy
description: Use when you need to deploy, build, or update the local MDMaker-based Radxa documentation mirror under ~/.openclaw/MDMaker.
---

# SKILL.md - MDMaker 瑞莎文档本地部署

## 简介

本技能用于本地部署和管理瑞莎（Radxa）参考文档。MDMaker 是一个从 radxa-docs 仓库生成离线文档的工具。

**重要**：部署目录选择在 `~/.openclaw/MDMaker/`，避免被用户误删。

## 文档位置

- **项目目录**：`~/.openclaw/MDMaker/`
- **构建输出**：`~/.openclaw/MDMaker/dist/`
- **原始仓库**：`~/.openclaw/MDMaker/radxa-docs/`

### 语言目录

构建输出 `dist/` 下包含两种语言的文档：

| 目录 | 说明 |
|------|------|
| `dist/zh/` | 中文文档 |
| `dist/en/` | 英文文档 |

## 工具说明

本项目包含两个主要工具：

### build_md_docs.py
- **用途**：第一次部署后生成可用于参考的瑞莎文档
- **功能**：从 radxa-docs 仓库生成完整的离线文档
- **运行方式**：
```bash
cd ~/.openclaw/MDMaker
source venv/bin/activate
python build_md_docs.py
```

### update_md_docs.py
- **用途**：更新和同步最新的瑞莎文档
- **功能**：
  - 自动 git pull 最新的 radxa-docs 仓库
  - 比较差异
  - 只更新有变动的文档
  - 同步到 dist 目录
- **运行方式**：
```bash
cd ~/.openclaw/MDMaker
source venv/bin/activate
python update_md_docs.py
```

## 部署步骤

### 1. 克隆仓库

```bash
cd ~/.openclaw && git clone -b agent https://github.com/ZIFENG278/MDMaker.git
```

### 2. 创建虚拟环境并安装依赖

```bash
cd ~/.openclaw/MDMaker
python3 -m venv venv
source venv/bin/activate
pip install requests tqdm
```

### 3. 构建文档（首次部署）

```bash
cd ~/.openclaw/MDMaker
source venv/bin/activate
python build_md_docs.py
```

构建完成后，文档会输出到 `~/.openclaw/MDMaker/dist/` 目录。

### 4. 更新文档

当需要更新文档时，运行：

```bash
cd ~/.openclaw/MDMaker
source venv/bin/activate
python update_md_docs.py
```

这个脚本会：
- 自动 git pull 最新的 radxa-docs 仓库
- 比较差异
- 只更新有变动的文档
- 同步到 dist 目录

## 使用方法

当用户要求部署瑞莎文档时，按照以下步骤执行：

1. 检查 `~/.openclaw/MDMaker/` 目录是否存在
2. 如果不存在，克隆仓库
3. 检查虚拟环境是否存在，如果不存在，创建并安装依赖
4. 首次部署运行 `python build_md_docs.py` 构建文档
5. 更新文档运行 `python update_md_docs.py`
6. 确认构建成功，检查 `~/.openclaw/MDMaker/dist/` 目录

## 验证构建

构建完成后，可以验证：

```bash
ls ~/.openclaw/MDMaker/dist/
# 应该看到：zh en ...

ls ~/.openclaw/MDMaker/dist/zh/
# 应该看到：rock2 rock3 rock4 rock5 zero orion ...

ls ~/.openclaw/MDMaker/dist/zh/orion/o6n/hardware-use/
# 应该看到硬件信息文档

# 英文文档结构相同
ls ~/.openclaw/MDMaker/dist/en/rock5/
```

## 注意事项

- 首次构建需要克隆完整的 radxa-docs 仓库，可能需要一些时间
- 更新文档需要确保网络能访问 GitHub
- 构建后的文档路径用于 radxa-doc 技能查询
- 部署在 `~/.openclaw/` 下可避免被用户误删
