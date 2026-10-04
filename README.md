# Hi, I'm Linsheng Yin (caysonyin)

做两件事：**把计算机视觉跑成能演示的实时系统**，以及**把 LLM 的实验做成一条命令就能复现的流程**。
下面的仓库分成五条线——视觉安全监控、LLM 数学推理与提示词工程、低比特量化数值参考、多视角视频理解、Agent Skill。

---

## 1. 视觉安全监控（CV Safety）

面向展区/文物场景的一体化视觉安全方案：目标检测 + 多目标跟踪 + 人体姿态 + 越界与危险物关联告警 + 桌面可视化。

| 仓库 | 说明 |
| --- | --- |
| [**cv_safety_sys**](https://github.com/caysonyin/cv_safety_sys) | 主项目（Python）。YOLOv7-tiny 检测 + 轻量多目标跟踪，MediaPipe Pose 33 关键点，展品安全围栏侵入检测与危险物-人员关联告警，PySide6 桌面端实时叠层与告警列表，首次运行自动下载模型权重。GPL-3.0 |
| [**safety_sys**](https://github.com/caysonyin/safety_sys) | 本机开发版（中文文档）。在同一视频流水线里加入**三级报警状态机**（安全 / 模拟红外触发 / 视觉风险自动触发 / 模拟 MPU6050 展品移动），并按华为云 IoTDA 属性上报格式发布 MQTT Topic。GPL-3.0 |
| [**cv_safety_orangepi**](https://github.com/caysonyin/cv_safety_orangepi) | 边缘端适配版。推理迁移到**昇腾 CANN + MindSpore Graph 模式**（YOLOv7-tiny MindIR），自研 `SimpleTracker`（质心 + IoU 混合策略）与 `CupFence` / `HazardBinder` 安全逻辑，含 Unicode 中文字体渲染，轻量依赖、单机 CPU 可实时运行 |

## 2. LLM 数学推理与提示词工程

| 仓库 | 说明 |
| --- | --- |
| [**math-prompt-eval**](https://github.com/caysonyin/math-prompt-eval) | 裸 LLM 单轮数学求解器 + 完整提示词实验框架：模板注册表、批量 sweep runner、对比报告、sweep 级校验。单次 API 调用解题，无工具、无重试、无候选筛选，输出与上游 `MathSolverAgent` 同 schema 的 `MathSolution` JSON。目标是**让 A/B 提示词实验便宜到一条 CLI 命令** |
| [**mathsolve-agent**](https://github.com/caysonyin/mathsolve-agent) | fork 自 [Cat-blizzard/mathsolve-agent](https://github.com/Cat-blizzard/mathsolve-agent)（上游 [InternLM/lagent](https://github.com/InternLM/lagent)）。在 `math_prove/` 下维护稳定的单 Agent 数学解题流水线：批量求解、Intern-S1 API 配置、benchmark 转换、schema 校验、答案等价判定、准确率报告与消融实验，另有保守准确率护栏与 sidecar 并行批量运行器 |

## 3. 量化与数值参考

| 仓库 | 说明 |
| --- | --- |
| [**rubin-w3a8**](https://github.com/caysonyin/rubin-w3a8) | LUT 式 **W3A8 / W3A16** 的 CPU 数值参考实现，用于 Rubin 相关研究。只刻画逻辑行为与量化配方，**不是硬件模拟器**，不做吞吐、时延、功耗、CUDA/PTX 或 Tensor Core 方面的结论。含实现、测试、复现脚本与已记录的评测产物（Qwen3-0.6B-Base + WikiText-2，seed 42，CPU-only），`uv` 锁定依赖 |

## 4. 多视角视频理解

| 仓库 | 说明 |
| --- | --- |
| [**sn-mvfoul**](https://github.com/caysonyin/sn-mvfoul) | fork 自 [SoccerNet/sn-mvfoul](https://github.com/SoccerNet/sn-mvfoul)。SoccerNet-MVFoul 多视角犯规视频数据集与 VARS 多相机视频识别系统（犯规类型与严重程度分类），对应论文 [arXiv:2304.04617](https://arxiv.org/abs/2304.04617) |

## 5. Agent Skill

| 仓库 | 说明 |
| --- | --- |
| [**gym-coach-skill**](https://github.com/caysonyin/gym-coach-skill) | 力量训练私教 Codex Skill。单会话闭环：今日训练计划 → 记录组数/次数/重量 → 汇总容量与最佳表现 → 更新动作历史以改进下次推荐，包含器械库、动作库、渐进超负荷规则与训练模板等结构化引用数据 |

---

## 技术栈

`Python` · `OpenCV` · `PyTorch` · `MediaPipe` · `MindSpore / Ascend CANN` · `PySide6` · `YOLOv7` · `uv` · `MQTT / IoTDA` · `Prompt Engineering & LLM Evaluation`

> 说明：本仓库是我 GitHub 主页的 Profile README，内容按各仓库现状整理，会随项目推进更新。
