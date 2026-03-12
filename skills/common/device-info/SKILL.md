---
name: device-info
description: Use when you need to detect the current hardware model and map a Radxa device to the correct product series before reading documentation or performing board-specific work.
---

# SKILL.md - 瑞莎硬件检测

## 简介

检测当前运行的硬件产品型号，用于匹配瑞莎文档系列。

## 设备检测脚本

```bash
#!/bin/bash

# 1. Device Tree（ARM 开发板最可靠）
if [ -f /proc/device-tree/model ]; then
  tr -d '\0' < /proc/device-tree/model
elif [ -f /sys/firmware/devicetree/base/model ]; then
  tr -d '\0' < /sys/firmware/devicetree/base/model
# 2. DMI 信息
elif [ -f /sys/class/dmi/id/product_name ]; then
  cat /sys/class/dmi/id/product_name
# 3. Hostname（瑞莎官方镜像常用，hostname 就是设备名）
elif command -v hostname &> /dev/null; then
  hostname
else
  grep "Model" /proc/cpuinfo
fi
```

## 硬件型号到瑞莎系列映射

### Device Tree / DMI / Hostname 关键词

| 硬件型号关键词 | 对应瑞莎系列 | 示例产品 |
|---------------|-------------|----------|
| ROCK 5, rock5, rock5b, rock5a, RK3588 | rock5 | ROCK 5A, ROCK 5B, ROCK 5C |
| ROCK 4, rock4, rock4a, RK3399 | rock4 | ROCK 4A, ROCK 4B, ROCK 4C+ |
| ROCK 3, rock3, rock3a, RK3568 | rock3 | ROCK 3A, ROCK 3B, ROCK 3C |
| ROCK 2, rock2, rock2f, RK3328 | rock2 | ROCK 2A, ROCK 2F |
| Zero, zero, zero3, zero2 | zero | Zero, Zero 2, Zero 3 |
| X15, X2L, Intel | x | X15, X2L |
| E20C, E24C, E52C, E54C | e | E20C, E54C |
| CM3, CM4, CM5, CM3I, CM3J, cm5 | som | CM3, CM4, CM5, NX5 |
| Orion, orion, O6, O6N, o6n | orion | Orion O6, Orion O6N |
| Cubie, cubie, A5E, A7A | cubie | Cubie A5E, Cubie A7A |
| Dragon, dragon, Q6A | dragon | Dragon Q6A |
| SiRider, sirider, S1 | sirider | SiRider S1 |
| AIRbox, aicore | aicore/fogwise | AIRbox, AICore |
| NIO, nio, NIO12L | nio | NIO12L |

## 使用场景

1. **查文档前** - 确定当前硬件型号，直接去对应系列查文档
2. **编程任务前** - 确认硬件型号，查GPIO引脚定义等
3. **问题排查** - 确认具体型号再搜索解决方案

## 注意事项

- 瑞莎官方镜像的 hostname 通常就是设备名（如 `rock5b`, `zero3`）
- 如果是 x86 PC/服务器（非瑞莎硬件），无需匹配系列
- 文档存放在 `~/.openclaw/MDMaker/dist/zh/`（中文）或 `~/.openclaw/MDMaker/dist/en/`（英文）
