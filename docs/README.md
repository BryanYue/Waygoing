# Waygoing 文档索引

整理日期：2026-10-16（Asia/Shanghai）。

这里集中保存个人 Harness、现有工作流自动化、学习路线和编排机制的讨论与文档。已复制 42 份已有资料，另整理 6 个相关活动的可见讨论；原文件保留在原处。

先读 [当前方向与决定](CURRENT-DIRECTION.md)，再按目的选择：

| 目的 | 入口 |
| --- | --- |
| 继续边学边做个人 Harness | [Plan B](planning/2026-10-16/PLAN-B.md) |
| Review 现有工作流自动化方案 | [Plan A](planning/2026-10-16/PLAN-A.md) |
| 给新会话交接两条工作线 | [AI 交接稿](planning/2026-10-16/AI-HANDOFF.md)，同时附上当前方向 |
| 先学模型请求、工具和 Agent 循环 | [第一课](learning/engine-basics-2026-10-06/01-model-and-agent.md) |
| 回看最早的问题与头脑风暴 | [原始背景](brainstorming/2026-10-15-personal-harness-background.txt)、[个人 Harness 语音讨论](discussions/2026-10-15-16-personal-harness-brainstorm.md) |
| 查看协议改善候选 | [v2.10 候选](workflow/2026-10-15-protocol-proposal/orchestration-protocol-v2.10-candidate.md)、[采用计划与审查结论](workflow/2026-10-15-protocol-proposal/adoption-review-and-checks.md) |
| 查某份材料从哪里复制过来 | [来源与覆盖范围](SOURCES.md) |

参考仓库的 Git 保存边界和云端配置建议见 [REFERENCE-HARNESS](REFERENCE-HARNESS.md)。

## 分类

| 目录 | 内容与使用方式 |
| --- | --- |
| `planning/2026-10-16/` | 两份计划及共同交接稿；保留原文，后续澄清见当前方向 |
| `brainstorming/` | 语音前的原始背景，包含历史问题、偏好和早期开放项 |
| `learning/engine-basics-2026-10-06/` | 早期路线、完整第一课、练习、论文阅读卡、来源书架、教学讨论和原报告 |
| `workflow/2026-10-15-protocol-proposal/` | v2.10 候选正文、采用说明及审查证据；没有启用到全局规则 |
| `workflow/source-materials/` | 原始修订单、W01–W12、v2.9 与判据保护说明的参考副本 |
| `reviews/learning-collaboration/` | 关于学习分工的 Claude 咨询、委派材料和 Codex 核验 |
| `reviews/workflow-spec-review/` | 两份工作规格的历史审查、当次输入与核验 |
| `discussions/` | 9 月已有聊天导出，以及本次整理的 6 个相关活动 |

## 讨论入口

- [2026-09-14：早期编排完整聊天导出](discussions/2026-09-14-orchestration-transcript.md)
- [2026-10-15：Harness 架构、工作流和协议](discussions/2026-10-15-harness-architecture-and-workflow.md)
- [2026-10-15–16：个人 Harness 头脑风暴与语音澄清](discussions/2026-10-15-16-personal-harness-brainstorm.md)
- [2026-10-16：Plan A](discussions/2026-10-16-plan-a.md)
- [2026-10-16：Plan B、客户端方向与参考仓库](discussions/2026-10-16-plan-b-and-reference-repositories.md)
- [2026-10-16：Waygoing 云环境](discussions/2026-10-16-waygoing-cloud-environment.md)
- [2026-10-16：活动耗时核查](discussions/2026-10-16-harness-performance-check.md)

## 怎样看待历史材料

已有文件按原内容复制，正文里的旧建议、状态、绝对路径和既有校验记录都保留。它们说明当时讨论到哪里；最新用户澄清见 [当前方向](CURRENT-DIRECTION.md)。归档没有修改或启用全局协议，也没有恢复历史任务。早期学习目录中的 `PROGRESS.md` 是那次教材编写的历史进度。

本索引使用相对链接，可以随 Waygoing 搬到其他环境。原文中的 Mac 绝对路径可能在其他机器不可用；[来源表](SOURCES.md) 给出已迁入文档的对应位置。原文对源码的引用仍对应当时版本，不能把旧行号直接当成最新子模块的定位。

参考源码放在 [reference-harness](../reference-harness/)，文档归本目录管理。Tianshu 的既有研究讨论保留，但没有克隆其仓库。

本次未新增 SHA-256 快照；复制一致性通过直接比较文件内容确认。历史材料自身带有的校验记录原样保留。
