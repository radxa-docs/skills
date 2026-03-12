# SKILL.md - 瑞莎产品文档查询

## 简介

本技能用于查询瑞莎（Radxa）硬件产品的技术文档。文档存放在本地文件系统中，包含单板计算机、计算模块、网络设备等产品的详细技术资料。

> ⚠️ **前置要求**：使用本 SKILL 前，请确保已按 mdmaker-deploy SKILL 完成文档部署。

## 典型使用场景

当需要编写涉及硬件操作的代码时（如 GPIO 控制、LED 点亮、传感器读取等），必须先查阅文档确认硬件参数：

1. 确定产品型号 → 找到对应目录
2. 查阅引脚定义 → hardware-design 或 getting-started/interface-usage
3. 确认参数后再编程

**示例**：在 ROCK5B+ 上点亮 LED
→ 先查 `rock5/rock5b/hardware-design/` 中的 GPIO 引脚定义
→ 确认引脚编号和配置方式
→ 再编写代码

## 文档内链接处理

文档中如有 `.md` 结尾的跳转链接，可以直接在 dist 目录中找到对应文件。

### 链接解析方法

瑞莎文档的 URL 路径规律：
```
https://docs.radxa.com/n/{产品系列}/{产品型号}/.../{子目录}/{文档名}.md
```

**示例**：
```
yolov8n/../../../../../orion/o6/app-development/artificial-intelligence/env-setup.md
```

解析步骤：
1. 向上回溯 `../` 找到产品系列和型号 → `orion/o6`
2. 拼接子目录 → `app-development/artificial-intelligence`
3. 拼接文档名 → `env-setup.md`
4. 组合路径：`orion/o6/app-development/artificial-intelligence/env-setup.md`
5. 加上前缀：`orion_o6_app-development_artificial-intelligence_env-setup.md`

### 快速查找命令

```bash
# 根据当前文档路径 + 链接文档名搜索
cd ~/.openclaw/MDMaker/dist/orion/o6n/app-development/artificial-intelligence/
find . -name "*env-setup*"
```

### 链接对应表

| 原始链接 | 对应离线文件 |
|----------|-------------|
| `env-setup.md` | `orion_o6n_app-development_artificial-intelligence_env-setup.md` |
| `ai-hub.md` | `orion_o6n_app-development_artificial-intelligence_ai-hub.md` |
| `API-manual.md` | `orion_o6n_app-development_artificial-intelligence_API-manual.md` |

## 文档根目录

```
~/.openclaw/MDMaker/dist
```

## 目录结构

### 产品系列（一级目录）

| 目录 | 说明 |
|------|------|
| rock2 | ROCK 2 系列 |
| rock3 | ROCK 3 系列 (RK3568) |
| rock4 | ROCK 4 系列 (RK3399) |
| rock5 | ROCK 5 系列 (RK3588) |
| zero | Zero 系列 (低功耗) |
| x | X 系列 (Intel处理器) |
| e | E 系列 (网络计算设备) |
| nio | NIO 系列 |
| rockpi | ROCK Pi 系列 |
| som | 计算模块 (CM3, CM4, CM5等) |
| accessories | 配件产品 |
| aicore | AI核心模块 |
| cubie | Cubie 系列 |
| dragon | Dragon 系列 |
| orion | Orion 系列 |
| roobi | Roobi 系列 |
| sirider | SiRider 系列 |
| fogwise | FogWise 系列 |
| compliance | 合规文档 |

### 子栏目（二级目录）

每个产品型号目录下包含以下子栏目：

| 子栏目 | 说明 |
|--------|------|
| getting-started | 入门指南 |
| hardware-design | 硬件设计 |
| low-level-dev | 底层开发 |
| os-config | 系统配置 |
| radxa-os | Radxa OS 使用指南 |
| other-os | 其他操作系统 |
| app-development | 应用开发 |
| apps-deployment | 应用部署 |
| accessories | 配件使用 |

## 文档命名规则

```
产品系列_产品型号_子栏目_专栏.md
```

示例：
- `zero_zero_os-config_README.md` = Zero系列 → Zero型号 → os-config子栏目 → README专栏
- `rock5_rock5a_getting-started_install-os.md` = Rock5系列 → Rock5A型号 → getting-started子栏目 → install-os专栏
- `rock5_rock5b_hardware-design_hardware-interface.md`

## 使用方法

### 1. 查找特定产品的文档

```bash
# 查看某产品系列下有哪些型号
ls ~/.openclaw/MDMaker/dist/<产品系列>/

# 示例：查看 rock5 系列有哪些型号
ls ~/.openclaw/MDMaker/dist/rock5/
```

### 2. 查找特定产品的特定栏目文档

```bash
# 查看某型号下有哪些子栏目
ls ~/.openclaw/MDMaker/dist/<产品系列>/<产品型号>/

# 示例：查看 rock5a 的子栏目
ls ~/.openclaw/MDMaker/dist/rock5/rock5a/
```

### 3. 搜索特定文档

```bash
# 查找包含关键词的 md 文件
find ~/.openclaw/MDMaker/dist -name "*关键词*.md"

# 示例：查找所有关于 install-os 的文档
find ~/.openclaw/MDMaker/dist -name "*install-os*.md"

# 示例：查找 rock5a 相关的所有文档
find ~/.openclaw/MDMaker/dist -name "*rock5a*.md"
```

### 4. 读取文档内容

使用 read 工具读取 md 文件：

```
read(path="~/.openclaw/MDMaker/dist/rock5/rock5a/getting-started/rock5_rock5a_getting-started_install-os.md")
```

## 常用产品查询速查

### ROCK 5 系列
- ROCK 5A: `rock5/rock5a/`
- ROCK 5B: `rock5/rock5b/`
- ROCK 5C: `rock5/rock5c/`
- ROCK 5 ITX: `rock5/rock5itx/`
- ROCK 5T: `rock5/rock5t/`

### ROCK 4 系列
- ROCK 4A/4B: `rock4/rock4ab/`
- ROCK 4C: `rock4/rock4c/`
- ROCK 4C+: `rock4/rock4c+/`
- ROCK 4SE: `rock4/rock4se/`
- ROCK 4D: `rock4/rock4d/`

### ROCK 3 系列
- ROCK 3A: `rock3/rock3a/`
- ROCK 3B: `rock3/rock3b/`
- ROCK 3C: `rock3/rock3c/`

### Zero 系列
- Zero: `zero/zero/`
- Zero 2: `zero/zero2/`
- Zero 3: `zero/zero3/`

### 计算模块 (SOM)
- CM3: `som/cm3/`
- CM3I: `som/cm3i/`
- CM3J: `som/cm3j/`
- CM4: `som/cm4/`
- CM5: `som/cm5/`
- NX5: `som/nx5/`

### E 系列（网络设备）
- E20C: `e/e20c/`
- E24C: `e/e24c/`
- E52C: `e/e52c/`
- E54C: `e/e54c/`

## 回答问题的流程

当用户询问瑞莎产品相关问题时：

1. **检测当前硬件型号** - 先执行设备检测脚本，确认当前运行在什么硬件上
2. **确定产品系列和型号** - 根据用户描述确定对应的产品系列（如 rock5, zero 等）
3. **优先查询当前硬件对应文档** - 如果当前硬件就是瑞莎产品，优先从对应系列查找
4. **定位产品型号目录** - 找到对应的型号目录
5. **查找相关子栏目** - 根据问题类型选择合适的子栏目（getting-started, hardware-design, low-level-dev 等）
6. **搜索相关文档** - 使用 find 命令或直接查看子栏目中的 md 文件
7. **读取文档内容** - 使用 read 工具读取相关文档
8. **根据文档内容回答** - 从文档中提取相关信息回答用户问题

## 硬件型号到产品系列映射

检测到当前硬件后，根据型号匹配对应的瑞莎产品系列：

| 硬件型号关键词 | 对应瑞莎系列 | 示例 |
|---------------|-------------|------|
| ROCK 5, Rock 5, rock5, RK3588 | rock5 | ROCK 5A, ROCK 5B, ROCK 5C |
| ROCK 4, Rock 4, rock4, RK3399 | rock4 | ROCK 4A, ROCK 4B, ROCK 4C+ |
| ROCK 3, Rock 3, rock3, RK3568 | rock3 | ROCK 3A, ROCK 3B, ROCK 3C |
| ROCK 2, Rock 2, rock2, RK3328 | rock2 | ROCK 2A, ROCK 2F |
| Zero, zero, RK3528 | zero | Zero, Zero 2, Zero 3 |
| X15, X2L, x15, x2l, Intel | x | X15, X2L |
| E20C, E24C, E52C, E54C | e | E20C, E54C |
| CM3, CM4, CM5, CM3I, CM3J | som | CM3, CM4, CM5, NX5 |
| Orion, orion, O6, O6N | orion | Orion O6, Orion O6N |
| Cubie, cubie, A5E, A7A | cubie | Cubie A5E, Cubie A7A |
| Dragon, dragon, Q6A | dragon | Dragon Q6A |
| SiRider, sirider, S1 | sirider | SiRider S1 |
| Fogwise, fogwise, AIRbox | fogwise | AIRbox, AIRbox Q900 |
| AICore, aicore, AX-M1, DX-M1 | aicore | AX-M1, DX-M1 |
| NIO, nio, NIO12L | nio | NIO12L |

## 设备检测脚本

查询瑞莎文档前，先检测当前硬件：

```bash
#!/bin/bash
if [ -f /proc/device-tree/model ]; then
  tr -d '\0' < /proc/device-tree/model
elif [ -f /sys/firmware/devicetree/base/model ]; then
  tr -d '\0' < /sys/firmware/devicetree/base/model
elif [ -f /sys/class/dmi/id/product_name ]; then
  cat /sys/class/dmi/id/product_name
else
  grep "Model" /proc/cpuinfo
fi
```

**注意**：如果是 x86 PC/服务器（非瑞莎硬件），则无需优先匹配系列，可以直接按用户描述查找。

## 注意事项

- 文档采用中文编写
- 文档内容非常详细，包含从入门到高级开发的各类指南
- 如果找不到具体文档，可以尝试用 find 全局搜索关键词
- productlist.md 包含完整的产品列表和简介
