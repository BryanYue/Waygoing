# 来源与覆盖范围

整理及更新日期：2026-10-16（Asia/Shanghai）。首次归档复制 42 份原文件，整理 6 个活动的 37 个轮次、166 条可见消息。另有 9 月既有聊天导出包含在原文件中；这些计数只描述首次归档。

## 后续维护来源

用户在当前 Waygoing 聊天认可 LifeOS 作为应用方向、先用 DeepSeek 验证并保留自研学习；随后明确要求更新现有文档、三路线及第一阶段计划，先规划不实施。原话保存在 [Plan C](planning/2026-10-16/PLAN-C.md)。据此新增 Plan C，更新当前方向、索引、A／B 的路线联系、共同交接稿与云配置说明。原位置文件不变；这些规划入口不再承诺与原件逐字相同。

后续用户原话：“嗯，先把这次文档提交并推送，云环境 配置好了”。据此授权本次文档 Git 交付，并将云环境当前状态改为“配置完成（用户确认）”；早期草稿记录保留为历史，不代表本聊天独立验证了最终配置。三路线仍仅规划，不启动工程。

本轮事实来源：LifeOS `d2607cef` 的 `src/server.ts`、`src/store.ts` 与领域文档；DeepSeek Harness `86a40220` 的插件／MCP 实现与开发者预览说明；Waygoing 远端 main 的 HTTPS `git ls-remote` 结果 `ea85baf7`；重新读取原活动“设置 Waygoing”（`01a142fa-9d85-7727-a52e-a0e73977e096`）的可见消息和操作记录；OpenAI 官方云环境文档。源码结论与精确版本在 Plan C，云状态和官方链接在 [REFERENCE-HARNESS](REFERENCE-HARNESS.md)。没有运行两项目、读取私人业务数据或改变云配置。

## 文件复制来源

下表记录首次复制时的来源，当时以直接内容比较确认一致。此后当前规划按上节维护；其余历史材料保留原文的路径、日期、旧结论和校验记录。原件均保留。

| 分类 | 本目录副本 | 原位置 |
| --- | --- | --- |
| 当前规划与交接 | [planning/2026-10-16/AI-HANDOFF.md](planning/2026-10-16/AI-HANDOFF.md) | `/Users/yueminjun/WorkPlace/codex/outputs/personal-agent-planning-20261016/AI-HANDOFF.md` |
| 当前规划与交接 | [planning/2026-10-16/PLAN-A.md](planning/2026-10-16/PLAN-A.md) | `/Users/yueminjun/WorkPlace/codex/outputs/personal-agent-planning-20261016/PLAN-A.md` |
| 当前规划与交接 | [planning/2026-10-16/PLAN-B.md](planning/2026-10-16/PLAN-B.md) | `/Users/yueminjun/WorkPlace/codex/outputs/personal-agent-planning-20261016/PLAN-B.md` |
| 头脑风暴原始背景 | [brainstorming/2026-10-15-personal-harness-background.txt](brainstorming/2026-10-15-personal-harness-background.txt) | `/Users/yueminjun/.codex/attachments/2af11805-2597-4adc-9b6c-829a8564e60a/已粘贴的文本.txt` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/01-model-and-agent.md](learning/engine-basics-2026-10-06/01-model-and-agent.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/01-model-and-agent.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/PROGRESS.md](learning/engine-basics-2026-10-06/PROGRESS.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/PROGRESS.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/README.md](learning/engine-basics-2026-10-06/README.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/README.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/discussion.md](learning/engine-basics-2026-10-06/discussion.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/discussion.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/evidence/claude-round-1.json](learning/engine-basics-2026-10-06/evidence/claude-round-1.json) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/evidence/claude-round-1.json` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/evidence/claude-round-2.json](learning/engine-basics-2026-10-06/evidence/claude-round-2.json) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/evidence/claude-round-2.json` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/evidence/codex-proposal.md](learning/engine-basics-2026-10-06/evidence/codex-proposal.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/evidence/codex-proposal.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/evidence/user-request.md](learning/engine-basics-2026-10-06/evidence/user-request.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/evidence/user-request.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/paper-reading.md](learning/engine-basics-2026-10-06/paper-reading.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/paper-reading.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/roadmap.md](learning/engine-basics-2026-10-06/roadmap.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/roadmap.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/sources.md](learning/engine-basics-2026-10-06/sources.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/sources.md` |
| 早期学习资料 | [learning/engine-basics-2026-10-06/workbook.md](learning/engine-basics-2026-10-06/workbook.md) | `/Users/yueminjun/.codex/worktrees/2063/engine-context-state/docs/learning/workbook.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/adoption-review-and-checks.md](workflow/2026-10-15-protocol-proposal/adoption-review-and-checks.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/adoption-review-and-checks.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/delivery-manifest.json](workflow/2026-10-15-protocol-proposal/delivery-manifest.json) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/delivery-manifest.json` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/candidate-check.md](workflow/2026-10-15-protocol-proposal/evidence/candidate-check.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/candidate-check.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/claude-plan-result.json](workflow/2026-10-15-protocol-proposal/evidence/claude-plan-result.json) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/claude-plan-result.json` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/claude-plan-review.md](workflow/2026-10-15-protocol-proposal/evidence/claude-plan-review.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/claude-plan-review.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/independent-plan-review.md](workflow/2026-10-15-protocol-proposal/evidence/independent-plan-review.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/independent-plan-review.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/plan-for-review.md](workflow/2026-10-15-protocol-proposal/evidence/plan-for-review.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/plan-for-review.md` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/plugin-verdict.json](workflow/2026-10-15-protocol-proposal/evidence/plugin-verdict.json) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/plugin-verdict.json` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/review-adjudication.json](workflow/2026-10-15-protocol-proposal/evidence/review-adjudication.json) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/review-adjudication.json` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/evidence/source-manifest.json](workflow/2026-10-15-protocol-proposal/evidence/source-manifest.json) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/evidence/source-manifest.json` |
| 协议候选与审查 | [workflow/2026-10-15-protocol-proposal/orchestration-protocol-v2.10-candidate.md](workflow/2026-10-15-protocol-proposal/orchestration-protocol-v2.10-candidate.md) | `/Users/yueminjun/Documents/Codex/2026-10-15/agent-workflow-spec/orchestration-protocol-v2.10-candidate.md` |
| 协议修订单原文 | [workflow/source-materials/2026-10-15-v2.10-amendment.txt](workflow/source-materials/2026-10-15-v2.10-amendment.txt) | `/Users/yueminjun/.codex/attachments/a0d1b6a4-fdea-4f8b-9d5b-8e0ba0052fdf/已粘贴的文本.txt` |
| 规则参考副本，不是安装或启用 | [workflow/source-materials/codex-global-rules-reference.md](workflow/source-materials/codex-global-rules-reference.md) | `/Users/yueminjun/.codex/AGENTS.md` |
| 规则参考副本，不是安装或启用 | [workflow/source-materials/orchestration-protocol-v2.9-reference.md](workflow/source-materials/orchestration-protocol-v2.9-reference.md) | `/Users/yueminjun/.claude/protocols/orchestration-protocol.md` |
| 规则参考副本，不是安装或启用 | [workflow/source-materials/oracle-protection-setup-reference.md](workflow/source-materials/oracle-protection-setup-reference.md) | `/Users/yueminjun/.claude/protocols/oracle-protection-setup.md` |
| 历史咨询与核验 | [reviews/learning-collaboration/brief.md](reviews/learning-collaboration/brief.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-s5Br4RTVlGDO2rFt/brief.md` |
| 历史咨询与核验 | [reviews/learning-collaboration/report.md](reviews/learning-collaboration/report.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-s5Br4RTVlGDO2rFt/report.md` |
| 历史咨询与核验 | [reviews/learning-collaboration/final-message.md](reviews/learning-collaboration/final-message.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-s5Br4RTVlGDO2rFt/final-message.md` |
| 历史咨询与核验 | [reviews/learning-collaboration/decision.json](reviews/learning-collaboration/decision.json) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-s5Br4RTVlGDO2rFt/decision.json` |
| 历史咨询与核验 | [reviews/workflow-spec-review/brief.md](reviews/workflow-spec-review/brief.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/brief.md` |
| 历史咨询与核验 | [reviews/workflow-spec-review/report.md](reviews/workflow-spec-review/report.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/report.md` |
| 历史咨询与核验 | [reviews/workflow-spec-review/final-message.md](reviews/workflow-spec-review/final-message.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/final-message.md` |
| 历史咨询与核验 | [reviews/workflow-spec-review/decision.json](reviews/workflow-spec-review/decision.json) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/decision.json` |
| 当次审查输入 | [reviews/workflow-spec-review/inputs/codex-global-rules.md](reviews/workflow-spec-review/inputs/codex-global-rules.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/inputs/01-AGENTS.md` |
| 当次审查输入 | [reviews/workflow-spec-review/inputs/orchestration-protocol.md](reviews/workflow-spec-review/inputs/orchestration-protocol.md) | `/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/inputs/02-orchestration-protocol.md` |
| 既有聊天导出 | [discussions/2026-09-14-orchestration-transcript.md](discussions/2026-09-14-orchestration-transcript.md) | `/Users/yueminjun/Documents/Codex/2026-09-14/referenced-chatgpt-conversation-this-is-an-2/outputs/orchestration-chat-transcript-2026-09-14.md` |

## 活动讨论来源

活动接口按分页读取到无下一页，再仅整理用户与助手的可见消息。隐藏推理、工具内部记录与环境注入未纳入。语音保留工具返回的请求和补充转写，不补写未取得的音频内容。

| 活动原名 | 记录 | 活动 ID | 轮次 / 可见消息 |
| --- | --- | --- | --- |
| 讨论个人 harness 学习路线 | [查看记录](discussions/2026-10-15-16-personal-harness-brainstorm.md) | `01a13f35-9df0-7a72-ae1b-68bca4c7dc9e` | 17 / 62 |
| Review DeepSeek harness 与天枢 | [查看记录](discussions/2026-10-15-harness-architecture-and-workflow.md) | `01a13e52-2f9c-74b2-b127-3b933885b6eb` | 7 / 48 |
| 规划工作流事件自动化 | [查看记录](discussions/2026-10-16-plan-a.md) | `01a14249-e452-77e6-bedb-8c93af25f0db` | 3 / 12 |
| 规划 Harness 学习开发 | [查看记录](discussions/2026-10-16-plan-b-and-reference-repositories.md) | `01a1424a-1f63-7127-a663-e67b696650dc` | 6 / 26 |
| 设置 Waygoing | [查看记录](discussions/2026-10-16-waygoing-cloud-environment.md) | `01a142fa-9d85-7727-a52e-a0e73977e096` | 2 / 7 |
| 核查 Harness 活动变慢 | [查看记录](discussions/2026-10-16-harness-performance-check.md) | `01a1406d-9ff6-716c-be67-c3f7400a3027` | 2 / 11 |

## 范围与尚未取得的材料

- 覆盖已明确定位的个人 Harness／工作流讨论、当前两份计划、10 月 6 日学习目录、v2.10 候选目录、两次直接相关的 Claude 咨询，以及 9 月已有编排聊天导出。未扫描无关项目或账户的其他会话。
- 交接来源活动 `01a13e58-a8f6-76cd-bd53-8c929ca500c6` 的查询返回零轮次、无标题，未取得可导出的正文。相关派发要求在 Plan A／B 活动及本会话中已保留；不能声称该来源活动另有一份完整导出。此项是返回内容为空，不是权限拒绝。
- Personal Context 检索在本会话不可用；已使用明确路径和活动读取接口完成上述归档，没有据此补造旧讨论。
- 背景中引用的 9 月 30 日 Claude 网页对话没有在本轮取得原始全文。已保留用户转述的 16 项问题、修订单和后续本地审查。外部网页、论文与官方资料仍作为原文链接，本次没有镜像下载或重新核验其当前内容。
- 部分历史审查还引用旧临时目录或插件运行目录；本次复制文档与结构化报告，未复制会话数据库、运行环境、认证配置或工具流日志。早期学习资料内已保存的两轮完整结构化报告原样保留。
- 本次讨论整理以读取时可访问的文本为准；当前归档工作自身后续的进展消息不再递归加入记录。不是全部账户历史或完整语音录像的备份。

## 版本与链接

新索引使用相对链接。已有原文按字节保留，因此里面的 Mac 绝对路径在其他机器可能不可访问；请按上表寻找对应副本。源码旧版本与最新子模块不同，未把旧行号静默替换为最新版本的行号。

两份当前规则的参考副本与当次审查输入分开保存，便于区分整理时文件和历史审查对象；归档不安装或启用这些规则。此处没有新建哈希快照，复制校验使用直接内容比较。

