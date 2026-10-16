## 0 需求对照

文件简称（下文证据均指这些文件）：
- `AGENTS.md`：`/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/inputs/01-AGENTS.md`
- `protocol.md`：`/Users/yueminjun/.codex/claude-orchestrator/v1/runs/run-4_t8G7HzghM6Oy9c/inputs/02-orchestration-protocol.md`
- `setup.md`：`/Users/yueminjun/.claude/protocols/oracle-protection-setup.md`（仅作旁证）
- `skill.md`：`/Users/yueminjun/.claude/skills/dispatch/SKILL.md`（仅作旁证）

| 要求（来源） | 状态 | 证据 |
|---|---|---|
| 重新 review 协议 v2.9 与 Codex 全局规格（用户原话 2） | 已做 | 两份全文已读 [`AGENTS.md:1-136`][`protocol.md:1-103`] |
| 对照旧审计 16 条（用户原话 2） | 已做 | 第 3 节对照表 |
| 关注流程偏重、裁决者与执行者是同一实例（用户原话 1） | 已做 | F3、A1、F9 |
| 区分原文直接成立、组合后已缓解、夸大或错误、缺证据（协调者） | 已做 | 第 3 节“判定”列 |
| 正式发现带行号、反例、影响、最小建议（协调者） | 已做 | 第 2 节共 18 条 |
| 查优先级、启用边界、授权与暂停、证据有效期、恢复与纠正、finding 闭合、责任归属（协调者） | 已做 | 第 4 节有索引 |
| 优先迭代项，以及不建议采纳的重方案（协调者） | 已做 | 第 5 节 |
| 只读，不写 v2.10（约束） | 已做 | 只用了 Read、Glob、Grep |

## 1 核心结论

1. 协议的判据保护只盯清单文件的内容 [`protocol.md:86-90`]。lane 写面、测试实际执行范围、合入后的整合树这三处没有机械检查。日常偏离最容易从这三处漏过（F1、F2、F5）。
2. “裁决者=执行者”在两份规格里都成立。协议不禁止协调者亲自实施 lane，也不要求 review 席独立于实施者 [`protocol.md:57`]。AGENTS.md 明确允许主代理实作并裁决 [`AGENTS.md:15`][`AGENTS.md:40`]。
3. 这个问题的最小修法不是加席位，要做三件事。第一，review 席用新上下文。第二，记录谁做的分类、谁改的判定。第三，在 final 里单列协调者改过的判定（F3）。
4. 流程偏重，根源是协议没写入口条件 [`protocol.md:3`]。AGENTS.md 已有轻量路径 [`AGENTS.md:15-17`]。但两份规格互不引用（X1、F9）。
5. 旧 16 条多数在原文成立。#9 夸大了。#11 误读了“较轻模式”。#2 的 gitignore 说法对判据文件不成立。几条旧修法偏重，见第 5 节。
6. 旧审计漏了两点。第一，并行 lane 的 worktree 不在保护登记内（F4）。第二，恢复时需要的 lane 起点没有落盘（F8）。

## 2 正式发现（按实际影响排序）

### F1【高】lane 写面没有强制检查，回退后越界写入会留下
- 位置：owned files 只是 dispatch 表里的一列 [`protocol.md:13`]。EDIT/FEATURE 的闸都不查写面 [`protocol.md:33-35`]。只有 FEATURE 做测试 diff 定性 [`protocol.md:57`]。回退只动 owned files [`protocol.md:65`]。
- 反例：一条串行 EDIT lane 为了让测试变绿，改弱了 lane A 新写的测试。新测试不在判据清单内 [`setup.md:26`]，所以 Gate-M 输出为空 [`protocol.md:89`]。该 lane 若红灯回退，越界改动仍留在工作区。
- 影响：清单外的测试会被静默改弱。回退后留下的改动可能被下一 lane 一起提交 [推断]。
- 已有缓解：W09 要求写入归属 [`AGENTS.md:99`]。W03 要求主代理核对 diff [`AGENTS.md:56`]。两条都只约束 Codex，而且靠人工核对。
- 最小建议：波次闸加一项机械检查。`git diff --name-only <lane 起点>..HEAD` 的结果加上未跟踪文件，必须全部落在 owned files 内。owned files 从 lane 起点提交里的 dispatch.md 读取。只要 diff 碰到测试或闸配置，不管 lane 是什么类型，都做 §3 的完整性定性。

### F2【高】测试执行范围被缩小时，闸仍可能全绿
- 位置：dispatch 可以改命令，“不得减少覆盖”却没有配套检查 [`protocol.md:13`]。Gate-M 只比文件内容 [`protocol.md:89`]。定性只看“测试目录” [`protocol.md:57`]。hook 只管 Write/Edit [`protocol.md:88`]。当时沙箱未启用 [`setup.md:9`]。
- 反例：(a) 把闸命令改成带 `--tests 'Foo*'`。(b) 在 lane 自己 owned 的构建脚本里加 test exclude。(c) 在清单外的测试里加 `assumeTrue(false)`。(d) 重新生成 lint baseline。四种都不碰清单文件，Gate-M 输出为空。(b) 连 F1 的写面检查也能通过。
- 影响：报告写“闸通过”，实际跑的测试却变少了。“未执行不算通过”这条规则没有落地手段 [`protocol.md:13`]。
- 已有缓解：W06 在规范层禁止缩分母、放宽阈值、跳过场景 [`AGENTS.md:74-76`]。本会话加载的 Claude 全局指令里没有对应条文 [本会话 `/Users/yueminjun/.claude/CLAUDE.md`]。
- 补充 [推断，未实测]：清单文件可能先被设 `git update-index --skip-worktree`，再被修改。这样 `git diff` 和 `git status` 都可能看不到改动。这与“检查真实工作区”的说法不符 [`protocol.md:89`]。触发前提是 ①② 两层都没拦住这次写入。
- 最小建议：闸记录执行数、跳过数、失败数，并与基线闸对比。执行数不能降，跳过数不能升。delta 的必需覆盖尽量写成具体测试 ID。闸要核对这些 ID 都已执行且通过。Gate-M 可加一步：比对文件内容哈希与基线 blob。仓库里有闸配置时（过滤条件、baseline、阈值），把它们列入清单。

### F3【中高】协议里自己裁决的地方看不见，review 席也不要求独立
- 位置：类型和席位由协调者调整，不需重新确认 [`protocol.md:13`]。CODE Major 能否带债合入由协调者定 [`protocol.md:50`]。谁给 finding 分类没写 [`protocol.md:52`]。MOVE 只有协调者抽查，席位也不要求独立 [`protocol.md:57`]。红灯由协调者裁决 [`protocol.md:59`]。final 由谁写没写 [`protocol.md:76`]。
- 反例：协调者亲自实施了一条 EDIT lane，review 席报出 CODE Major。协调者把它改判为 REG，或决定带债合入 [推断：协调者是事实上的分类人]。final 只列一句“债务摘要”。Boss 看 PR 时，看不到实施者改判了自己 lane 的 finding。另一个反例：review 席直接复用实施这条 lane 的 subagent 上下文。
- 影响：实施、审查、裁决落到同一实例时，偏差没有出口。这正是用户点名的问题。
- 已有缓解：PR 只能人工合并 [`protocol.md:67`]。CODE Major“不等于验收通过，final 必列” [`protocol.md:50`]。Codex 作协调者时，W03 要求核对产物 [`AGENTS.md:56`]。
- 最小建议（不加席位）：(1) review 席必须是没参与该 lane 实施的新上下文。(2) findings.jsonl 记录分类人和改判人。(3) 下面几类改动在 final.md 单列：协调者下调 review 分类、带债合入、调整类型或席位。这一节从 jsonl 和 PROGRESS 机械导出。(4) 协调者亲自实施的 lane，其 finding 争议进 DECISIONS。协调者能否亲自实施 lane，由用户决定。

### F4【中高】并行 lane 的 worktree 不在保护登记范围内
- 位置：同轮并行的写 lane 要开 worktree [`protocol.md:64`]。①② 两层依赖登记 [`protocol.md:87-88`]。登记的 root 是执行 worktree 的根目录 [`setup.md:21`][`setup.md:24`]。denyWrite 用的是绝对路径 [`setup.md:40`]。只有确认在登记范围外的写入才放行 [`setup.md:63`]。改登记要重启会话 [`skill.md:56`]。
- 反例：某轮有两条并行写 lane。协调者新建 worktree `/x/repo-lane2`，登记里却只有 plan worktree 的 root。lane2 用 Edit 改 `/x/repo-lane2/<判据路径>`，hook 判为范围外并放行 [推断：未读 hook 实现]。沙箱 denyWrite 的绝对路径也不包含这个 worktree。
- 影响：两道事前防线恰好在并行写入处缺失。只剩 ③ 层能事后发现，而且前提是合入前在该 worktree 里跑了 Gate-M。
- 最小建议：二选一，由用户定。(a) 开工时就建好所有并行 lane 的 worktree，一次登记（登记支持多项 [`setup.md:24`]）。(b) 并行 lane 明确只有 ③ 层，作为已批准的较轻模式写进 delta [`protocol.md:90`]。波次闸先在该 worktree 跑 Gate-M。

### F5【中】闸证据没有绑定到提交，rebase 后也不要求重跑
- 位置：EDIT 用结果文件的时间戳校验 [`protocol.md:34`]。只有 cherry-pick 要求重跑 [`protocol.md:66`]。“强制重跑全量单测”列在“按适用选择”的候选里 [`protocol.md:39-40`]。
- 反例：lane A 和 B 并行，A 先以 fast-forward 合入。B rebase 到 task 分支最新提交后再 fast-forward。协议只对 cherry-pick 要求重跑，没提 rebase。A+B 的整合树要到阶段收官才可能跑测试。第 40 行写着“按适用选择”，收官时是否必跑全量单测并不明确。
- 时间戳的问题：协议没写拿时间戳跟什么比。结果文件不记录命令和过滤范围，只跑一个子集也会生成新时间戳。`touch` 还能伪造时间戳。
- 已有缓解：W11 要求记录验证结果及对应版本 [`AGENTS.md:121`]。W07 要求分开说明各类证据 [`AGENTS.md:89`]。两条都只约束 Codex。
- 最小建议：每次闸结果记录 HEAD sha、工作区是否干净、闸命令原文。合入条件是闸结果的 sha 等于被合入的提交。rebase 后 sha 会变，自然要重跑。同时写明阶段收官必跑全量单测。

### F6【中】常见搬迁过不了 MOVE 的 R100 规则，例外清单会变成整文件豁免
- 位置：[`protocol.md:33`]；MOVE 不派 review [`protocol.md:57`]。
- 反例：把 `a/b/Foo.kt` 搬到 `a/c/Foo.kt`。Foo.kt 的 package 行变了，不再是 R100。引用它的 N 个文件改了 import，显示为 `M` 行。MOVE 的定义还包括“删除”，删除显示为 `D` 行。凡是靠 import 引用的语言都会这样，不限于 JVM [推断：Git 行为未实测]。
- `<base>` 没有定义。如果按 plan 基线算，前面 lane 的改动会让本 lane 直接 FAIL [推断]。
- 影响：结果只有两种。要么 MOVE 经常 FAIL，要么预登记例外列满文件。例外按整文件算，例外文件里改什么都能过闸。MOVE 又不派 review，只剩协调者抽查。
- 最小建议：写明 `<base>` = lane 起点提交。例外条目写明允许的改动类别，比如只改 package/import 行，或删除。用 `git diff -U0` 过滤，校验例外文件只改了这些行。超出范围就按 EDIT 处理。不必新增 MOVE+ 类型。

### F7【中】finding 的分类人、关闭人和关闭核验都没指定，记录字段也不够
- 位置：[`protocol.md:48-54`]，[`protocol.md:77`]。预算来源：协议把 lane 的时长和 token 记在 PROGRESS [`protocol.md:72`]，skill 却从 findings 的 `cost` 取 [`skill.md:43`]。
- 反例：review 席报出一条 CODE Major，带复现命令 [`protocol.md:54`]。执行席自修一轮后说已修好。协调者填上 same_kind_scan，标为 fixed。没人在合入提交上重跑那条复现命令。jsonl 也没有 id、file:line、复现命令、sha 这些字段 [`protocol.md:77`]，事后无法核验。
- 影响：fixed 只是一句陈述。“不采信台账”只约束下一次 review 的输入 [`protocol.md:46`]，管不到关闭动作本身。
- 附带两点：第一，hook 拒绝写判据的尝试不留记录 [`protocol.md:88`]。v2.3 的 oracle-tamper 记账，在 v2.9 正文里已没有对应条文 [`protocol.md:102`]。第二，预算来源两处不一致，见上面“位置”。
- 最小建议：jsonl 加字段 `id`、`location`、`repro`、`classified_by`、`closed_by`、`closed_at_sha`。标为 fixed 前，在合入提交上重跑 repro 并记录结果。hook 拒绝写已确认受保护路径时，追加一行日志，计为一类 finding。

### F8【中】恢复所需的 lane 级状态没有落盘
- 位置：恢复规则只讲怎么取回协议正文 [`protocol.md:5`]。PROGRESS 每个 lane 只记状态、类型、时长和 token [`protocol.md:72`]。回退却要用“lane 起点” [`protocol.md:65`]。
- 反例：Claude 协调者在上下文压缩后恢复，PROGRESS 显示 lane3 为 in-progress。它不知道 lane3 的起点提交和 worktree 路径，也不知道执行 subagent 是否还在写。协调者重派 lane3，同一范围于是出现两个写入者。要回退时，也找不到“lane 起点”。
- 已有缓解：W09 要求接手前确认原写入者已停止 [`AGENTS.md:99`]。W11 要求记录仍在运行的任务 ID，并在恢复时核实真实状态 [`AGENTS.md:121`][`AGENTS.md:125`]。这些只约束 Codex。
- 最小建议：PROGRESS 每个 lane 行加三列：起点提交、worktree 路径、执行实例 ID。F1、F5、F6 的检查都要用到起点提交。

### F9【中】协议没有入口条件，也不分档；保护登记的固定成本高
- 位置：协议没写适用范围 [`protocol.md:3`]。state 文件固定 5 个 [`protocol.md:15`]。每个 lane 都要记时长和 token [`protocol.md:72`]。每个阶段都要对账和单源性审计 [`protocol.md:75`]。“较轻模式”只指保护层 [`protocol.md:90`]。协议只能显式触发 [`skill.md:6-7`]。登记要改环境变量并重启会话 [`skill.md:56`]。
- 反例：一次重构有 2 条 lane、1 个阶段。要写 delta、dispatch、清单和 5 个 state 文件。要过 Boss 审阅，登记后重启会话。每个 lane 都要 review，还要做单源性审计和 final。中途若获准改一次判据，要出新基线、改登记、再重启 [`skill.md:74`]。
- 影响：中等任务不会走协议，也就用不上协议里最有用的几项机械检查 [推断：没有任务分布数据]。
- 已有缓解：AGENTS.md 已有轻量路径。简单任务直接做，复杂任务写一份简要任务约定 [`AGENTS.md:15-17`]。Claude 侧的入口由全局指令和 skill 的触发词决定 [`skill.md:6-7`]。
- 最小建议：协议头部写入口条件，比如有多条写入 lane 或分多个阶段，具体阈值由用户定。不要在协议里再定 2 到 3 档模式。把写面检查、测试计数比对、判据 diff 做成可单独调用的脚本。AGENTS.md 任务约定里的“对照验证”可以直接引用这些脚本。

### X1【中】两份规格的关系、启用边界和优先级都没写
- 位置：AGENTS.md 全文没有引用协议。优先级只分上级指令、用户要求、项目约定 [`AGENTS.md:7`]。方法可按需调整 [`AGENTS.md:9`]。“不另建固定状态文件” [`AGENTS.md:17`]。只在有收益时派发 [`AGENTS.md:36`]。不为普通微调做多路审查 [`AGENTS.md:84`]。同一任务只用一份 PROGRESS [`AGENTS.md:113`]。对比协议的固定 state 文件 [`protocol.md:15`] 和固定席位 [`protocol.md:57`]。
- 反例 1：Codex 按协议跑 3 条 lane，依据 [`AGENTS.md:9`] 把 EDIT 的 review 席当作“方法”省掉了。协议写“EDIT 一席”，AGENTS.md 允许按需调整方法，两边都说得通。
- 反例 2：Codex 在插件运行目录记一份进度，Claude 在仓库 state 目录再记一份 PROGRESS。这违反了 [`AGENTS.md:113`] [推断：未读插件实现]。
- 反例 3：Codex 委派 Claude 跑 /dispatch，于是出现两个“协调者”。Codex 负责规划和验收，Claude 按协议裁决红灯。最终裁决权归谁，两份规格都没写 [推断]。
- 影响：同一任务两边执行力度不一致，跨模型交接时口径也会冲突。
- 最小建议：AGENTS.md 加一段：用户或项目指定按执行协议运行时，协议规定的闸、席位、state 文件属于必要验收，不按 W01/W07 省略；协议没覆盖的地方按 AGENTS.md。协议头部写明两点：Boss = 用户；嵌套委派时由谁担任协调者。

### X2【中】“负责人 / owner / Boss”没有定义，两份规格里含义冲突，而且牵涉授权
- 位置：“负责人沿已有批准更新基线登记” [`protocol.md:90`]。“任务负责人沿已有授权” [`setup.md:18`]。owner 有四种用法 [`protocol.md:12`][`protocol.md:51`][`protocol.md:74`][`protocol.md:83`]。AGENTS.md 里也有三种：约定负责人合并 [`AGENTS.md:101`]、记录负责人 [`AGENTS.md:115`]、任务负责人 [`AGENTS.md:121`]。
- 反例：Codex 当协调者，按 W11 把自己当作“任务负责人”。Boss 批准修改一处判据后，Codex 按 §6④ 自己更新登记。它顺带收下了其他测试改动，并自行判定这些也属于“获准差异”。
- 影响：§6④ 本来是授权关口。在 Codex 读来，它可能变成自己给自己授权。
- 已有缓解：skill 写明登记由 Boss 来写，执行代理不能代做 [`skill.md:56`]。这条只约束 Claude 侧。
- 最小建议：§6④ 和 [`setup.md:18`] 里的“负责人”改成“Boss”。协调者可以准备差异，但不能写登记。协议 §0 前加一张 5 行的角色表：Boss、协调者、执行席、review 席、owner（只指事实的 owner 文件）。

### A1【中】AGENTS.md 默认允许主代理自己实作、自己验收、自己裁决
- 位置：主代理可以实作和整合 [`AGENTS.md:15`]。审查力度由错误后果决定，由主代理自己判断 [`AGENTS.md:21`]。主代理已是 Astra 时，只在“有明确收益”时另开一个 [`AGENTS.md:40`]。W03 只约束派出去的工作 [`AGENTS.md:56`]。
- 反例：Codex 主代理实作了一个复杂的状态机改动，一个邻近测试失败。它自己判定“是既有问题，与本次无关”，然后交付。另一种情况：Claude 的 review 结论与 Codex 自己的方案冲突，Codex 按 W01 自己裁决。
- 影响：用户点名的“裁决者=执行者”，在 AGENTS.md 这一层同样存在，而且没有触发条件。
- 最小建议：只在“主代理是争议一方”时生效，一般任务不加审查，处理方式二选一。一是把争议材料按 [`AGENTS.md:40`] 的格式交给没参与的新上下文裁决。二是在交付里单列“自裁项”，写出判断和证据。

### F10【低中】红灯后“另派一次”没有次数上限
- 位置：[`protocol.md:59`]。
- 反例：自修一轮后仍红，协调者选“另派”。新执行者也红，又自修一轮。协调者再选“另派”，条文没有禁止这种循环。
- 已有缓解：W07 要求在没有信息增量时停止同类循环 [`AGENTS.md:87`]。这条只约束 Codex。
- 最小建议：同一 lane 最多另派一次，再红只能回退或 park。旧修法可直接采纳。

### F11【低中】DECISIONS 的“默认动作”没有定义含义
- 位置：[`protocol.md:73`]。
- 反例：协调者写下“默认动作：采用方案 B”。Boss 没回复，协调者就按 B 执行了，条文没有禁止。
- 已有缓解：[`protocol.md:60`]、[`protocol.md:90`]、[`AGENTS.md:109`] 都要求只暂停依赖该决定的工作。
- 最小建议：补一句话。默认动作只能是两种之一：暂停依赖项、继续无关工作；或者停止。不能执行待决的选项。

### F12【低中】全文只标了 [M]，需要判断的条文被写成了机械条文
- 位置：第 6 行定义了 [M] 和 [R] 两类 [`protocol.md:6`]。但 6 个章节标题全标 [M] [`protocol.md:20`][`protocol.md:27`][`protocol.md:44`][`protocol.md:62`][`protocol.md:70`][`protocol.md:80`]。下面这些都要靠判断：“语句不变” [`protocol.md:33`]、“行为不变” [`protocol.md:34`]、nature 分类 [`protocol.md:49`]、“高风险” [`protocol.md:57`]、“按适用” [`protocol.md:40`]、“模块职责声明 vs 内容” [`protocol.md:75`]。
- 影响：协调者的判断写进报告后，看起来像机械检查的结果。这会放大 F3 的问题 [推断]。
- 最小建议：逐条标出 [R]，写明由谁判断、记在哪里。可以和 F3 的改判单列一起做。

### F13【低】已知红名单缺少“只减不增”的约束
- 位置：[`protocol.md:12`]，[`protocol.md:24`]，[`protocol.md:74`]。
- 反例：已知红测试 T 在 lane2 被修绿，lane4 又把它弄红了。T 仍在冻结名单里，闸照样放行。
- 旧 #9 说的“互相卡住”不成立。DEBT 到期只是升级到 DECISIONS [`protocol.md:74`]，不需要改冻结的 delta。
- 最小建议：名单里的测试一旦转绿，就从放行范围移除，并记入 PROGRESS。往名单里加测试需要授权。

### F14【低】若干自洽问题
- “唯一权威副本” [`protocol.md:3`] 与“执行中按基线 commit 里的副本” [`protocol.md:4-5`] 字面上冲突。
- FEATURE“每项独立 commit” [`protocol.md:35`] 与“一 lane 一 commit” [`protocol.md:64`] 冲突。
- 版本号 v2.9 写死在 skill 和 setup 里 [`skill.md:14`][`setup.md:1`]。这违背了“同一事实只有一个 owner” [`protocol.md:84`]。
- 最小建议：每处改一句即可。

### A2【低】W01–W02 篇幅大，W02 全是机械规则
- 位置：第 19–50 行，约占全文 136 行的 24% [`AGENTS.md:19-50`]。W02 示例里出现了 Terra [`AGENTS.md:46`]，W01 的系列表里却只有 Luna/Sol/Astra [`AGENTS.md:23-28`][`AGENTS.md:32`]。
- 影响：每次加载全局规格都要读进大段命名细则 [推断]。Terra 的定位不明，可能导致路由时靠猜。第 34 行已声明示例不是白名单，所以影响小 [`AGENTS.md:34`]。
- 最小建议：W02 的格式规则交给派发工具，做成校验或模板，正文只留一句。补一句 Terra 的定位，或者换掉这个示例。

## 3 旧 16 条逐项判定

| # | 判定 | 依据 | 对旧修法的评价 | 对应发现 |
|---|---|---|---|---|
| 1 | 部分成立 | 协调者调整 dispatch、裁决红灯有原文 [`protocol.md:13`][`protocol.md:59`]。谁分类、谁写记录原文没写，“协调者都做”是推断。“负责人”未定义成立 [`protocol.md:90`]，skill 已规定由 Boss 登记 [`skill.md:56`]。 | “负责人=Boss”可以采纳。覆盖映射改成“核对必需测试 ID 已执行”更实在。独立收官席不宜默认加。“改动在 final 单列”可以采纳，应该机械导出。 | F2、F3、X2 |
| 2 | 部分成立 | 命令可调且没有检查 [`protocol.md:13`]。定性只看测试目录，且只给 FEATURE [`protocol.md:57`]。golden 已由 skill 列入清单 [`skill.md:39`]。阈值和 golden 有 W06 规范保护 [`AGENTS.md:74-76`]。gitignore 那条对判据文件不成立：清单只展开基线里已跟踪的文件 [`setup.md:26`]，已跟踪文件的改动不受 .gitignore 影响 [推断，未实测]。真正的漏洞在仓库外的闸输入和 index 标志位。 | 计数比对可以采纳，性价比最高。配置和 baseline 入清单可以采纳。“生产代码新增 suppress 一律记 finding”噪声大，建议只限闸检查的那些规则。 | F2 |
| 3 | 成立 | 新测试不会自动成为判据 [`protocol.md:18`][`setup.md:26`]，后续 lane 还能“依据正式要求”修改它 [`protocol.md:60`]。review 的输入要求里没有“对照 delta 原句核对新测试” [`protocol.md:46`]。 | “审查席确认后登记转正”要出新基线、改登记、重启会话 [`skill.md:56`][`skill.md:74`]，每条 FEATURE 都这样走太重。建议默认做法：review 对照 delta 原句核对新测试；合入后靠 F1 和 F2 保护这些测试。独立席写测试只给高风险 lane。 | F1、F2 |
| 4 | 成立 | 回退只动 owned files [`protocol.md:65`]，闸也不查写面 [`protocol.md:33-35`]。越界改动留下来，主要发生在串行 lane。并行 lane 不合入时，改动进不了 task 分支 [推断]。 | 越界检查可以采纳。不建议“登记文件进 denyWrite”：同一会话里，沙箱分不清协调者和执行者。改成从 lane 起点提交读取 owned files 即可。 | F1 |
| 5 | 成立，而且范围更广 | R100 的要求在 [`protocol.md:33`]，`<base>` 没定义。任何靠 import 引用的语言都会触发。删除也不是 R100。 | `<base>`=lane 起点可以采纳。行级白名单可以采纳。不需要新增 MOVE+ 类型。 | F6 |
| 6 | 成立 | 同轮第二个合入的 lane 无法 fast-forward [`protocol.md:66`]。旧审计没点出的更关键问题是：rebase 后没有重跑要求。 | “rebase 后重跑波次闸，作为常规路径”可以采纳。用 sha 绑定可以一并解决。 | F5 |
| 7 | 成立 | 时间戳拿什么比没有定义 [`protocol.md:34`]。Codex 侧 W11 要求记录版本 [`AGENTS.md:121`]，算部分缓解。 | 记录 HEAD sha 可以采纳，tree hash 可选。Gradle 缓存键属于项目层，不进通用协议。 | F5 |
| 8 | 成立 | [`protocol.md:59`]。Codex 侧有 W07 缓解 [`AGENTS.md:87`]。 | 可以直接采纳。 | F10 |
| 9 | 夸大 | DEBT 到期升级到 DECISIONS，不需要改 delta [`protocol.md:74`]，不存在互相卡住。实际缺的是“只减不增”的约束。 | “只冻结上限”效果相同，可以采纳，优先级低。 | F13 |
| 10 | 部分成立 | 字段含义没定义 [`protocol.md:73`]。但 [`protocol.md:60`]、[`protocol.md:90`]、[`AGENTS.md:109`] 已限定为只暂停依赖工作。 | 可以采纳，补一句话即可。 | F11 |
| 11 | 部分成立，有误读 | 冷启动：skill 规定没有历史数据时标 [估] [`skill.md:43`]，协议正文没写。“较轻模式”在原文里指保护层模式 [`protocol.md:90`][`setup.md:48`]，不是流程档位。流程偏重本身成立（见用户原话 1）。 | “冷启动用保守值，标未校准”可以采纳。不建议“定义 2 到 3 档”。改为写清入口条件，轻量任务回到 AGENTS.md 默认流程，并复用脚本。 | F9 |
| 12 | 成立 | 第 6 行定义了两类，章节标题却全是 [M]，见 F12。 | 可以采纳，和 F3 一起做。 | F12 |
| 13 | 成立，影响低 | [`protocol.md:3-5`]。 | 可以采纳。 | F14 |
| 14 | 成立 | 见 X2。“波次闸”与 lane 的关系，只能从“每 lane 合入后”推出来 [`protocol.md:29`]。 | 术语表可以采纳，控制在几行内。 | X2 |
| 15 | 事实成立，结论部分成立 | v2.4–v2.9 都在同一天发布 [`protocol.md:94-101`]。v2.5 明写“按外部评审” [`protocol.md:100`]。元规则讲的是按违反数据增删规则 [`protocol.md:85`]，不完全约束设计缺陷的修补。setup 显示保护层当时都没启用 [`setup.md:9-10`]，所以 v2.9 很可能缺少实跑数据 [推断]。 | 攒成一批发 v2.10、每处标出触发事件，可以采纳。 | 不单列 |
| 16 | 成立，影响低 | v2.3 的记账 [`protocol.md:102`] 在正文里已没有对应条文。 | 可以采纳。由 hook 机械追加，不靠协调者手记。 | F7 |

结构建议（拆成三层）：脚本层可以采纳。不建议另拆四份分阶段检查清单，因为 dispatch skill 已经起到清单作用 [`skill.md:62-76`]。文件越多，同步负担越重。

旧审计“只改三处”（#1/#2/#4）：方向对。建议把 #1 收窄为“负责人=Boss，加上改判可见”，并补上 F4 和 F8。

## 4 W01–W12 本身及交叉使用

- AGENTS.md 本身问题少，正式发现只有 A1 和 A2。
- 两份规格一致的地方：暂停语义 [`AGENTS.md:109`][`protocol.md:60`]。判据保护 [`AGENTS.md:74-78`][`protocol.md:60`]。恢复时核对真实状态 [`AGENTS.md:125`][`protocol.md:46`]。
- 组合使用时，Codex 侧的 W03/W07/W09/W11 补上了协议的一些缺口，见 F5、F8、F10。Claude 侧加载的全局指令里没有这些条文 [本会话上下文]。所以同一份协议，在两侧的执行强度不同。
- 协调者要求查的各项，对应发现如下：
  - 优先级：X1。
  - 启用边界：X1、F9。
  - 授权与暂停：X2、F11。
  - 证据有效期：F5。
  - 跨轮恢复：F8。
  - finding 闭合：F7。
  - 责任归属：F3、X2、A1。
- 纠正：获准的判据变更，已由 [`protocol.md:18`] 和 [`protocol.md:90`] 覆盖，没有另列发现。

## 5 优先迭代项与不建议的重方案

优先迭代（按投入产出排）：
1. lane 起点写进 PROGRESS。加写面检查。改动碰到测试或闸配置时触发定性。（F8、F1）
2. 闸结果记录执行计数和 sha。核对必需测试 ID 已执行。rebase 后重跑。（F2、F5）
3. 让自己裁决的地方可见。review 用新上下文，jsonl 记录分类人和改判人，final 单列改判，“负责人”改为 Boss。（F3、X2、A1）
4. 两份规格互相引用，写清入口条件、协议在 Codex 侧属于必要验收、嵌套委派时谁是协调者。（X1、F9）
5. 决定并行 worktree 的保护方式。（F4）

不建议默认采纳：
- 每个阶段加独立只读审查席。只在协调者亲自实施过 lane、或 lane 为高风险时考虑。
- 新测试默认走“重新登记转正”。每次都要重启会话。
- 用 denyWrite 保护登记文件。
- 生产代码新增的 suppress 一律记 finding。
- 新增 MOVE+ 类型。
- 在协议里定 2 到 3 档模式，或另拆四份阶段清单。

## 6 实际运行的验证

- 没有执行 shell 命令，也没有运行任何测试。
- 用 Read 读了 4 个文件全文：两份冻结副本，以及作为旁证的 `setup.md` 和 `skill.md`。
- 用 Grep 查看了工作目录里 `orchestration-protocol.md` 的标题行和修订记录行。它们与冻结副本一致，但没做逐字节比对。

## 7 未核实

- `~/.claude/hooks/oracle-guard.sh` 的实现没读。F4 里“范围外放行”的判断，来自 [`setup.md:63`]。
- Codex–Claude 插件的实现没读。X1 的反例 2、反例 3 都是推断。
- 以下 Git 行为都没有实测：`skip-worktree` 能否躲过 `git diff`/`git status`，`-M100%` 对 package/import 改动的输出，已跟踪文件不受 .gitignore 影响。
- setup 里写的保护层状态是 2026-09-09 的，现在的实际状态未知 [`setup.md:9-10`]。
- 有没有 plan 实际跑过 v2.9，未知。也没有 findings.jsonl 数据可以印证 F9 的成本判断。
- 9 月 30 日的那次审计对话本身没看到，只看了用户转述的内容。
- [`AGENTS.md:133`] 引用的 `skills/technical-report-writing/SKILL.md` 是否存在，没有检查。

## 8 偏离与异议

- 宿主全局指令要求把“未核实”放在报告末尾。本任务书规定的顺序是先列未验证项，再写异议和问题。我按任务书的顺序写。
- 宿主全局指令规定，纯分析任务不读协议文档。本任务的审查对象就是协议，所以按任务书读了。setup 和 skill 只作旁证。
- 对旧审计的部分内容有异议：#2 的 gitignore 说法、#9 的“互相卡住”、#11 对“较轻模式”的理解。这些是内容判断上的分歧，不是指令冲突。
- 对协调者说明没有异议。

## 9 需要用户决定的问题

1. 协议下，协调者能否亲自实施 lane？如果允许，这些 lane 的改判和带债合入，是否一律进 DECISIONS？
2. 多少条写入 lane、分几个阶段的任务才走协议？这要看实际的任务分布。
3. 新测试的保护走哪条路？默认靠写面检查和测试计数（较轻），还是重新登记转正（需重启会话）？
4. 并行写 lane 怎么保护？开工时预先登记各 worktree，还是接受并行 lane 只有 ③ 层？
5. Codex 委派 Claude 跑协议时，谁是协议里的“协调者”？红灯和改判由谁裁决？