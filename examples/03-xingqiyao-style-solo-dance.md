# 星奇摇风 · 单人竖屏热舞（仿风格实验）

| 字段 | 内容 |
|------|------|
| **Genre** | 抖音热舞挑战 / 单人竖屏 |
| **参考** | 用户指定链路：`#星奇摇2`（如「听说大家还想看单人版」类单人版节奏）；**不抄原片动作与人脸**，只学竖屏单人卡点风 |
| **时长** | 约 15 秒样片 |

## 样片资产

路径：`examples/assets/xingqiyao-style/`

| 文件 | 说明 |
|------|------|
| `first-frame.jpg` | 首帧：开场举手肩部预备 |
| `last-frame.jpg` | 尾帧：收势面向镜头 |
| `xingqiyao-style-15s.mp4` | 首尾帧驱动约 15s 成片 |

## 编排

文生图首帧 → 文生图尾帧 → first+last frame 图生视频（竖屏 9:16）。详见 `docs/orchestration-rooftop-neon-dance.md` 同构管线。
