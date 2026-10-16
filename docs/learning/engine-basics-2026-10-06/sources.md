# 阅读材料与来源核对

核查日期：2026-10-06（Asia/Shanghai）。这是按课程需要筛选的书架，不是开课前的阅读清单。必学只指下述指定片段；第一次打开课程不必点任何外链。论文优先用固定版本，网站未显示发布日期时明确写“未标明”，不以抓取日期代替出版日期。

## 主线材料

只读五项的指定片段；编号用于引用，S5、S6 移入选学后保留编号。

### S1 工具调用往返

- 来源：[Anthropic Tool use with Claude](https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview)，官方动态文档，发布日期未标明；本次核对 overview 及 How tool use works。
- 阶段 2 必读 15–25 分钟：只跟一遍 client tool 的请求、`tool_use`、应用执行、`tool_result`，不复制安装步骤。
- 要学会：分别指出谁建议行动、谁执行、谁把观察加入下一次调用。服务端工具由服务方执行，客户端工具由你的应用执行。
- 边界：这是一种 API 的接口约定；示例成功不证明工具结果真实、操作幂等或 Agent 任务完成。课程的退款例子是独立编写的教学材料。

### S2 从调用到执行循环

- 来源：[Anthropic Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)，发布 2024-12-19；网页已含后续工具更新说明。
- 阶段 2 必读 15–20 分钟：What are agents、When (and when not) to use agents、Agents 三节；其余模式选读。
- 要学会：固定步骤与模型动态选择下一步的区别，以及为什么需要环境反馈和停止条件。
- 边界：这是厂商工程经验，不是统一学术定义或最优性证明。旧文章的具体产品列表不作为选型依据。

### S3 选择上下文

- 来源：[Anthropic Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)，发布 2025-09-29。
- 阶段 3 必读 20–30 分钟：Context retrieval and agentic search、Context engineering for long-horizon tasks。核查了原文相关段落。
- 要学会：按需取信息、摘要、持久笔记分别改变了哪一环。
- 边界：文中的 attention budget 是工程解释，不作为可直接测量的固定常数；课程也不从注意力计算复杂度直接推导“内容越多必然越差”。摘要的遗漏风险要另验。

### S4 第一篇论文

- 来源：Nelson F. Liu 等，[Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172v3)。首发 2023-07-06，所读 v3 为 2023-11-20；[全文](https://arxiv.org/html/2307.03172v3)。
- 阶段 3 必读 45–75 分钟：摘要、Figure 1、§2.1–2.3；按 [论文阅读卡](paper-reading.md) 读。§3、§5 是可选的第二次阅读，另约 20–30 分钟，不计入首次必读时间。
- 核对所得：实验在多文档问答和键值检索中改变相关信息位置与输入长度，报告了受测模型的表现变化。
- 边界：实验用的是当时模型及指定任务。不能断言 2026 年所有模型都会同样失败，不能由此断定“中间永远不能放重要信息”。我们复用的是对照思路。

### S7 代码地图的具体实现

- 来源：[Aider Repository map](https://aider.chat/docs/repomap.html)，官方动态文档，发布日期未标明；[固定提交的 repomap.py](https://github.com/Aider-AI/aider/blob/5dc9490bb35f9729ef2c95d00a19ccd30c26339c/aider/repomap.py)。
- 阶段 4 必读文档 20–30 分钟。阶段 7 后源码选读 30–60 分钟：`get_repo_map` → `get_tags_raw` → `get_ranked_tags` → `get_ranked_tags_map`。先问各函数输入输出，不逐行啃 867 行。
- 本次核查：远端 main 为 `5dc9490bb35f9729ef2c95d00a19ccd30c26339c`；读取了原始文件及上述相关路径，确认符号提取、图排序和预算裁剪入口；未运行 Aider。
- 边界：静态符号引用不等于精确运行时调用图，也不覆盖完整业务意图与决策。读取文件修改时间的缓存策略不证明业务理解正确更新。

## 选学材料

每阶段最多选一项；不影响进入下一阶段。更深入的阅读留到某个问题确实卡住你时。

### S5 检索后生成的原始研究

- 来源：Patrick Lewis 等，[Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401v4)。首发 2020-05-22，所读 v4 为 2021-04-12；[全文](https://arxiv.org/html/2005.11401v4)。
- 阶段 4 后选读 45–75 分钟：Figure 1、§2 开头、§3.1、Table 1 和 §4.5 的 retrieval ablations。公式先只认输入、文档、输出，不推导。
- 核对所得：该工作结合 DPR 检索器和 BART 生成器，并进行训练；区分 RAG-Sequence 与 RAG-Token。
- 边界：今天常说的“检索文本拼入提示”是更宽泛的工程用法，不等于原论文全部算法。其问答结果不证明可持续维护项目决策、代码状态或交接理解。

### S6 记忆的存储与作用域

- 来源：[LangGraph Memory overview](https://docs.langchain.com/oss/python/concepts/memory) 及 [Persistence](https://docs.langchain.com/oss/python/langgraph/persistence)，官方动态文档，发布日期未标明。
- 阶段 5 后选读 20–30 分钟：前者 Short-term memory、Long-term memory；后者只看 checkpoints 与 threads 概念，不跑示例。
- 要学会：线程内状态恢复与跨会话数据读取是不同需求。持久化解决“还在”，选择与校验解决“适合现在用”。
- 边界：这里的 graph 首先指执行流程图，不自动成为业务知识图谱。保存状态不证明它仍符合最新需求。

### 其他按需选学

| 材料与日期 | 何时打开与只读哪里 | 用处与不能推出的结论 |
|---|---|---|
| Hugging Face [How do Transformers work](https://huggingface.co/learn/llm-course/chapter1/4?fw=pt)、[Tokenizers](https://huggingface.co/learn/llm-course/chapter2/4?fw=pt)；官方课程，日期未标明 | 阶段 1 后，20–30 分钟；causal language modeling、Attention layers、tokenization 概念 | 补足文本如何变成输入表示、生成如何继续；跳过训练环境和全课程，不把所有 Transformer 都说成只会预测下一个 token |
| Yao 等 [ReAct](https://arxiv.org/abs/2210.03629v3)；首发 2022-10-06，v3 2023-03-10 | 阶段 2 后仍想理解行动循环时，30–45 分钟；摘要和一条任务轨迹 | 研究推理文本、行动与观察的交替；不要求产品公开模型私有思考，也不把文本轨迹当真实因果解释。本次仅核对元数据和摘要，实验全文未审阅 |
| Packer 等 [MemGPT](https://arxiv.org/abs/2310.08560v2)；首发 2023-10-12，v2 2024-02-12 | 阶段 5 后，45–60 分钟；系统图、记忆层次、一次数据换入换出 | 用有限上下文配合外部存储；操作系统类比不表示真正拥有无限上下文。本次核对元数据/摘要，不转述提升百分比 |
| [MCP Architecture overview](https://modelcontextprotocol.io/docs/2026-07-28/learn/architecture)；固定文档版本 2026-07-28 | 阶段 8 后考虑跨 Agent 复用时，20–30 分钟；host、client、server 及 tools/resources | 接口复用候选；协议连通不保证记忆正确、当前有效或模型会选对证据。暂不部署 MCP 服务 |

## 深入阅读

### D1 GraphRAG 与整体性问题

Darren Edge 等，[From Local to Global: A Graph RAG Approach to Query-Focused Summarization](https://arxiv.org/abs/2404.16130v2)，首发 2024-04-24，v2 2025-02-19；[全文](https://arxiv.org/html/2404.16130v2)、[官方实现文档](https://microsoft.github.io/graphrag/)。阶段 6 之后，约 1–2 小时，读方法图、§3 评价方法、§6.1 局限。

核对所得：从文本抽取实体关系，形成社区摘要以支持全局性问题。论文评价涉及两个约百万 token 的语料，含模型生成问题与模型裁判。它为“跨很多材料提炼主题”提供依据，没有直接测试连续编码中需求变化后的正确行动。不可直接搬用问答偏好分数作为 Engine 验收。

### D2 时间知识图与变化更新

Rasmussen 等，[Zep: A Temporal Knowledge Graph Architecture for Agent Memory](https://arxiv.org/abs/2501.13956v1)，2025-01-20；[全文](https://arxiv.org/html/2501.13956v1)。阶段 7 之后，约 1–2 小时，读 §2 图构建、时间字段及实验设置。

本次核对了正文的图分层、时间提取和 DMR/LongMemEval 评价背景。论文为作者系统的研究报告；对话记忆指标不能直接等同代码变更质量。原始 episode 被保留，也不意味着抽取的事实和冲突判断绝不丢失或出错。

实现入口：[Graphiti 固定提交](https://github.com/getzep/graphiti/tree/4083f51812d381d7ca28b887cfa3c3db188f576d)。2026-10-06 核对 main 为 `4083f51812d381d7ca28b887cfa3c3db188f576d`，阅读 README、[graphiti.py](https://github.com/getzep/graphiti/blob/4083f51812d381d7ca28b887cfa3c3db188f576d/graphiti_core/graphiti.py) 的 `add_episode`、`search` 与 [edges.py](https://github.com/getzep/graphiti/blob/4083f51812d381d7ca28b887cfa3c3db188f576d/graphiti_core/edges.py) 的时间字段；未安装、未运行、未复现其性能。

源码阅读问题：新增资料如何提取实体并对齐已有实体？关系怎样被判为被替代？新事实录入与摘要更新是否同一路径？当前接口的 `update_communities=False` 默认值提醒我们不能从“支持增量”推定所有派生摘要自动同步。先画调用流程，再决定是否需要运行。将来复用前另查许可证、依赖成本、数据边界和当前版本行为；本次不是组件选型或集成验收。

## 来源使用边界

以上已核查页面能支持局部机制说明；没有任何一篇单独证明 Engine 愿景成立。学习中的退款数据、练习判断和评估草案是本课程自编，明确区别于论文实验。后续源码变动时先对照固定提交，读新版本是另一次核查。链接可访问和片段已阅读不表示实验已经复现。

教师额外校核，不加入学生阅读负担：2026-10-06 核对 Anthropic [Messages API](https://platform.claude.com/docs/en/api/messages/create) 的无状态多轮说明及 `messages` 字段，与 [Managed Agents sessions](https://platform.claude.com/docs/en/managed-agents/sessions) 的会话历史说明。两者支持第一课区分“接口是否代管会话”和“信息是否进入本次推理”；两份动态文档均未标明发布日期。本课没有要求使用这些产品。
