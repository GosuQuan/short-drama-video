# 编排说明：霓虹天台舞蹈样片

对应资产：`examples/01-rooftop-neon-dance.md` + `examples/assets/rooftop-neon-dance/`

## 这条流水线在干什么

把「爆款短剧节奏」落成可复现的 **AI 编排（orchestration）**：先叙事分镜，再提示词，再锁定首尾帧，最后用图生视频把 15 秒高光段拉出来。技术价值不在「一键成片」，而在 **镜头可控、角色/场景可对齐、后续可替换模型而不改剧本结构**。

## 编排步骤（实际执行顺序）

1. **题材调研（轻量）**  
   扫爆款短剧/舞蹈向竖屏常见钩子：前 2–3 秒冲突 → 中段张力 → 舞蹈卡点 → 态度/身份反转。只借节奏骨架，文案与分镜原创。

2. **Storyboard → Prompt 管线**  
   每个镜号固定字段：景别、人物、动作、对白/VO、**英文 AI Prompt**（竖屏 9:16、光影、单动作、时长暗示）。  
   价值：把「感觉」拆成模型可执行约束，方便换 Kling / 即梦 / Runway 时只换执行器、不换剧本。

3. **首帧 / 尾帧一致性**  
   - 首帧：举手开场舞姿（天台霓虹夜景）  
   - 尾帧：旋转结束、面向镜头的收势  
   同一场景母题（霓虹天台 + 东亚女舞者），用双帧钉住开场与收束，减少纯文生视频的漂移。  
   已知缺口：样片礼服造型与分镜角色卡（夹克舞裤）尚未完全统一——后续应用同一参考图或统一服装 prompt 再生成。

4. **15 秒成片生成**  
   模式：**first + last frame → video**（`duration=15`，竖屏约 9:16，720p）。  
   Prompt 只描述运动与运镜（连贯旋转/步伐、发丝与裙摆、轻环绕镜头），不让模型重写剧情。  
   上限 15s 正好覆盖「高光舞段」；完整 45–60s 短剧应拆多段再剪辑拼接。

5. **模型链式（model chaining）**  
   `文生图（首帧） → 文生图（尾帧） → 图生视频（双帧驱动）`  
   剧本/分镜 markdown 是编排的「控制面」；生成模型是「执行面」。换供应商时优先保持控制面不变。

6. **提示词工程要点**  
   - 景别 + 单一动作 + 光色（cyan/magenta）+ 情绪词  
   - 竖屏与「no text / no watermark」显式写出  
   - 视频侧少叙事、多运动，避免和分镜台词抢戏

7. **后处理（当前未做 / 可演进）**  
   - 未做：调色统一、BGM 卡点、字幕烧录、多镜拼接  
   - 建议下一跳：按分镜表批量出镜 → 剪辑时间线 → 对口型/VO → 封面定帧

## 产出清单

| 路径 | 内容 |
|------|------|
| `examples/01-rooftop-neon-dance.md` | 完整分镜 + prompt |
| `examples/02-cafe-rain-dance-reveal.md` | 第二套舞蹈叙事示例 |
| `examples/assets/rooftop-neon-dance/first-frame.jpg` | 首帧 |
| `examples/assets/rooftop-neon-dance/last-frame.jpg` | 尾帧 |
| `examples/assets/rooftop-neon-dance/rooftop-neon-dance-15s.mp4` | ~15s 样片 |
| `docs/orchestration-rooftop-neon-dance.md` | 本文 |

## 技术价值一句话

**分镜结构化 + 双帧锚定 + 短窗图生视频**，把短剧高光从「碰运气生成」变成可迭代的编排实验；完整成片靠多段同一管线拼接，而不是单次超长生成。
