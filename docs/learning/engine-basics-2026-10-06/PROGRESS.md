# Engine 学习资料任务进度

更新时间：2026-10-06（Asia/Shanghai）。任务：engine-learning。负责人及唯一文档写入者：Codex。Claude：两轮只读教学讨论与审校，均已结束。

## 任务约定

- 工作目录：`/Users/yueminjun/.codex/worktrees/2063/engine-context-state`。
- 基线：`fdd0b1e851a99036cac7e07f489cc2d56b85956f`，detached HEAD，初始 clean，仅 `README.md`。
- 正式要求来源：[用户原话](evidence/user-request.md)，当前会话 AGENTS 全局约定及 `/Users/yueminjun/.codex/AGENTS.md`。
- 目标：渐进路线、可跟学的第一部分、少而精且分层的原始资料、理解检查与速度调整、真实 Codex–Claude 讨论及有意义的分歧。
- 允许修改：根 README 添加入口；`docs/learning/` 教材、进度及必要讨论证据。
- 非目标：业务实现、安装模型/数据库/框架、恢复历史实验、架构定案、全量论文综述。
- 不变量：保留已有文件；不把模拟教学数据当实测；不把局部论文结果当 Engine 方案证明；不把插件预检当 Claude 参与。
- 验证：核对原始来源与日期、教学术语和例题一致性、相对链接、git diff 范围、Claude 实际回执和完整报告。
- 停止/review：插件同类失败无新证据时停止重试并明确状态；超范围改实现/恢复实验需新授权。学习路线细化在本次授权内。
- 回滚：仅撤回本次新建文档和 README 入口；不执行 git reset/stash/clean。
- 资源：Claude 单 run 串行；每轮有时限与费用参数，不启动嵌套代理；本地仅文本、少量远端来源读取。

## 当前状态

本次交付已完成：入口、八阶段路线、第一部分完整教材、贯穿案例/练习、论文阅读卡、分层来源书架、两轮讨论和原始报告。根 README 保留原标题并追加入口；未修改业务实现，未恢复实验，未安装/运行候选组件。

Claude 第一轮提供 6 条发现（含状态项），第二轮提供 3 条文档发现；Codex 逐项裁决见 discussion.md。第二轮发现均已修正，最后改动由 Codex 核验，未追加第三轮。两轮运行时工作区快照差异均为空；编辑发生在运行终止后。

验证：11 份 Markdown 的本地链接、代码围栏、行尾空白检查通过；两份完整结构化报告 JSON 可解析；`git diff --check` 通过。核对了 C1 单一内容、R2/R3 适用范围、当前 v2 任务与是否切换 v3 的区别、五项主线及选学依赖。网页/论文/源码核查范围在 sources.md；没有将原始研究报告数字作为 Engine 验收。

尚未发生：学生实际跟学和反馈；阶段 3–8 的完整逐课讲义尚未展开，但路线、练习、来源和检查已提供。不是要求用户一次性完成教材，也不是声称学生已掌握。

下一步：从第一部分“第一次停下来”两题开始，学生直接在当前对话提交复述、实际用时和困惑，再在同一目录更新后续讲义。无需恢复任何旧实验。

## 决策与后续

项目地图保持候选地位。采纳需求变化先于关系图、Lost in the Middle 作第一篇、来源有效性贯穿、统一退款案例。RAG 和 LangGraph 降为选学；主线五项外部片段。对 Claude 的“每次重发完整历史”作条件化纠正；不预设扁平笔记必败。原始发现和裁决保留在 discussion 与 evidence。

Claude 第一轮：`run-1QGWh9U7vIMk_s__`；第二轮：`run-cfRUzbD2lRug_08g`。两轮均实际 `claude-opus-5-5`、high、reported，Codex 已记录 accepted 与逐项裁决；provider success、bridge exit 0、工具审计完整，无权限拒绝、scope/invariant 错误。strict 为只读工具约束，不宣称 OS sandbox。完整报告保存到 `evidence/claude-round-1.json` 和 `evidence/claude-round-2.json`。没有仍在运行的任务。

恢复记录：最初两次分别遇到 `requirement source must be absolute` 和 `unsafe protected_files path` 参数校验错误，未启动 run；按字段要求分别使用绝对来源路径与相对保护路径后成功。一次辅助 `ps` 读取被宿主沙箱限制，未升级权限；运行终止以插件 bridge_lifecycle、exit 0 和最终回执核对，没有把 ps 失败解释成进程仍活跃。

外部来源：Codex 已在线核对正文/指定段落，源码只读固定提交；ReAct/MemGPT 仅核元数据和摘要。未本地运行任何组件或论文实验。Claude strict 无联网能力，不能宣称它独立检索核验了外部全文。
