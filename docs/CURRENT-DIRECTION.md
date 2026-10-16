# 当前方向与已确认决定

整理日期：2026-10-16（Asia/Shanghai）。初步头脑风暴已结束，当前进入资料归档节点。这是相关讨论的接续入口；具体要求仍以用户原话及实际授权为准。

## 两条工作线

| 工作线 | 当前方向 | 当前完成程度 |
| --- | --- | --- |
| Plan A：现有开发工作流自动化 | 在现有 Codex／Claude 工作流外增加事件发现、实施资格检查、任务接续与交付；工程任务最终以 Jira 上经确认的实施资格为依据 | [计划已形成](planning/2026-10-16/PLAN-A.md)，待具体项目与实施范围确认；没有部署服务、写票、执行真实任务或创建 PR |
| Plan B：个人多用途 Harness | 边学习边构建自己的运行机制，coding 是一项能力，未来可扩展资料、文档、消息等个人事务 | [U 系列学习路线](planning/2026-10-16/PLAN-B.md)整体获用户认可；没有实现课程代码或发起模型实验 |

两条线可以并行。B 的学习与职业能力建设本身有价值，不以先证明优于所有成熟工具为前提；A 不必等待 B 成为完整平台。

## 学习方式与技术方向

用户主要使用 **Kotlin，目前不会 Go**；语言学习不阻塞规划。Go 是有理由的倾向，具体模块、工具链和 UI 技术仍可选择。

每个单元保留：必要概念与少量资料 → 用户先提出设计 → Codex 质询 → 用户修订并动手关键机制 → Claude 辅助实现和首轮讲解 → 先预测再运行对照 → Codex 独立 review 与有增量的补充教学。用户不需要手写所有代码，也不能只提出一句需求、让 AI 完全代做设计后听讲。

长期客户端方向是 **共享运行内核，加 CLI、TUI 及以后需要的 UI／客户端**。CLI 与 TUI 可以共存；起步不必拆成多个进程或服务。语言、通信协议、工具数量及完整架构尚未冻结。来源：[Plan B 后续讨论](discussions/2026-10-16-plan-b-and-reference-repositories.md)。

用户已有 DeepSeek／Gemini API，Codex／Claude 订阅用于辅助开发和学习；采购 OpenAI／Anthropic API 不是前置条件。真实调用前仍需明确所用服务、模型及预算。本次资料整理没有调用付费模型 API。

早期教材的固定时间估算、强制核心手写建议，以及“先证明自建价值才继续”的说法，不能覆盖后续澄清。模型训练、微调和从零训练语言模型不在当前学习主线。

## 工作流与协议材料的地位

复杂任务中的协调、实施、独立测试与审查职责分离，是需要保留的讨论方向；lane 按任务依赖与协作需要采用，简单工作不强制进入完整编排。

已找到 [v2.10 候选正文](workflow/2026-10-15-protocol-proposal/orchestration-protocol-v2.10-candidate.md)及[采用与审查说明](workflow/2026-10-15-protocol-proposal/adoption-review-and-checks.md)。**候选稿存在，不等于已经替换全局 v2.9 或生效。** 部分背景材料里的“尚未起草”没有反映这份已存在的候选产物；归档保留原文，在这里指出差异。

`workflow/source-materials/` 是阅读参考；`reviews/workflow-spec-review/inputs/` 是当次审查的输入。它们没有成为 Waygoing 的新 AGENTS 规则，也不改变仍采用旧版本的任务。既有暂停 Goal 未恢复。

## Waygoing 的实际状态

用户最初要求沿用指定 commit，随后明确改为“直接拉取到最新的”。已通过 GitHub CLI 克隆并同步远端默认分支，登记为 submodule：

| 目录 | 跟踪分支 | 本次同步后版本 |
| --- | --- | --- |
| [codex](../reference-harness/codex/) | main | `6ae8b8aa` |
| [deepseek-harness](../reference-harness/deepseek-harness/) | master | `86a40220` |
| [deer-flow](../reference-harness/deer-flow/) | main | `ec07de96` |
| [llm-space](../reference-harness/llm-space/) | main | `bec6fcd1` |

这些版本记录本次同步结果，不是要求长期停留在这些 commit。Git submodule 仍会记录当前检出的版本；后续更新需要显式获取远端变化。原仓库保留，Tianshu 排除；本轮按用户要求将资料与引用信息作为头脑风暴结束的本地提交，不推送。中断克隆的残留已保留在 Waygoing 的 `.git/interrupted-clones/` 中。

文档现在分类复制到 `docs/`。原计划、附件、学习资料和审查记录没有移动或改写；新增的是索引、当前方向、来源表及可见讨论整理。

[云环境讨论](discussions/2026-10-16-waygoing-cloud-environment.md)当时只确认空仓库和通用环境草稿。没有证据表明环境已发布；其中列出的工具版本也不能当作这台 Mac 的版本。本地资料尚未推送，因此不能假定云端已有这些新文件。

## 仍需按下一步补充的信息

首个真实样板任务、未来实现目录、首家模型服务与实验预算，尚未最终确定。每次学习投入时间可以实际开始后调整；最终部署也待真实运行需求出现后决定。这些不阻塞当前资料整理。

用户报告过正常模式慢。后续核查确认交接整理约耗时 23 分 20 秒，但没有取得足以计算真实 tokens/s 的数据，不能据此认定云端一定更快或模型输出速度下降。详见[两次核查记录](discussions/2026-10-16-harness-performance-check.md)。

下一次继续学习时，先读本页和 Plan B，选一个小单元，由用户先形成设计；不要把归档完成理解为已授权启动全部工程、部署或外部写入。


参考仓库不会将源码导入 Waygoing；云端复用与更新的建议见 [参考资源配置](REFERENCE-HARNESS.md)。该配置尚未在云端执行，未创建定时更新任务。
