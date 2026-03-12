# SKILL.md - 瑞莎硬件检测

## 简介

检测当前运行的硬件产品型号，用于匹配瑞莎文档系列。

## 设备检测脚本

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

## 硬件型号到瑞莎系列映射

| 硬件型号关键词 | 对应瑞莎系列 | 示例产品 |
|---------------|-------------|----------|
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

## 使用场景

1. **查文档前** - 确定当前硬件型号，直接去对应系列查文档
2. **编程任务前** - 确认硬件型号，查GPIO引脚定义等
3. **问题排查** - 确认具体型号再搜索解决方案

## 注意事项

- 如果是 x86 PC/服务器（非瑞莎硬件），无需匹配系列
- 文档存放在 `~/.openclaw/MDMaker/dist/`
