# 面向真正工程师的技能库 (Skills For Real Engineers)

这些是我日常用于**真正工程开发**的智能体技能 (Agent skills)——拒绝“意识流编程 (Vibe coding)”。

开发真正的应用程序绝非易事。诸如 GSD、BMAD 和 Spec-Kit 等方案试图通过接管开发流程来解决这个问题。但在接管的同时，它们也剥夺了你的控制权，导致流程中产生的 Bug 极难排查。

这套技能库的设计理念是：小巧、易适配、可组合。它们适用于任何模型，并且全部基于数十年的工程经验沉淀。随意魔改 (Hack around) 它们，打造属于你自己的工作流。尽情享受吧。

如果你想第一时间获取这些技能的更新，或者我创建的全新技能，欢迎与近 60,000 名开发者一起订阅我的 Newsletter：

[订阅 Newsletter](https://www.google.com/search?q=https://www.aihero.dev/s/skills-newsletter)

## 快速开始 (30秒极速配置)

1. 运行 skills.sh 安装程序：

```bash
npx skills@latest add mattpocock/skills

```

2. 挑选你想要的技能，以及你打算将它们安装到哪些代码智能体上。**请务必勾选 `/setup-matt-pocock-skills**`。
3. 在你的智能体中运行 `/setup-matt-pocock-skills`。它会执行以下初始化：

- 询问你希望使用哪个 Issue 追踪系统（GitHub、Linear 或是本地文件）
- 询问你在进行工单分流 (Triage) 时使用的标签规范（`/triage` 命令会用到这些标签）
- 询问你希望将生成的技术文档存放在哪个目录

4. 搞定——开箱即用。

## 为什么要做这套技能库？

我构建这套技能库，是为了解决我在使用 Claude Code、Codex 等代码智能体时观察到的常见失败模式 (Failure modes)。

### #1：智能体根本没理解我的需求

> “没有人确切知道他们想要什么。”
> David Thomas & Andrew Hunt, [《程序员修炼之道》(The Pragmatic Programmer)](https://www.google.com/search?q=https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**痛点**。软件开发中最常见的失败模式就是“目标未对齐 (Misalignment)”。你以为开发者懂你要什么，结果看到做出来的东西才发现——他们根本没 get 到你的点。

在 AI 时代，同样的问题依然存在。你和智能体之间存在沟通鸿沟。解决这个问题的办法是引入**深度拷问 (Grilling session)**——强制让智能体针对你要构建的需求，向你发起极其详细的反问。

**解决方案**是使用以下技能：

- [`/grill-me`](https://www.google.com/search?q=./skills/productivity/grill-me/SKILL.md) - 用于非代码场景
- [`/grill-with-docs`](https://www.google.com/search?q=./skills/engineering/grill-with-docs/SKILL.md) - 与 [`/grill-me`](https://www.google.com/search?q=./skills/productivity/grill-me/SKILL.md) 类似，但附加了更多高阶功能（见下文）

这是我最受欢迎的两个技能。它们能在真正动手之前，帮助你和智能体达成认知对齐，并迫使你对即将进行的变更进行深度思考。建议在*每一次*修改代码前都使用它们。

### #2：智能体废话太多 (太啰嗦)

> “通过使用统一语言，开发人员之间的交流以及代码的表达，都将源自同一个领域模型。”
> Eric Evans, [《领域驱动设计》(Domain-Driven-Design)](https://www.google.com/search?q=https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**痛点**：在项目初期，开发者和需求方（领域专家）往往说着两套不同的语言。

我在使用智能体时也有同样的割裂感。智能体通常被直接扔进项目里，并被要求在干活的过程中自行悟出项目里的业务黑话。这就导致本来 1 个词就能说清的事，它们偏要啰嗦 20 个词。

**解决方案**是建立“统一语言 (Shared language)”。即通过一份文档，帮助智能体解码当前项目特有的业务黑话。

以下是一个截取自我的 `course-video-manager` 仓库中 [`CONTEXT.md`](https://www.google.com/search?q=https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 的真实例子。对比一下哪个更容易阅读？

- **修改前**：“当一门课程某个章节里的具体一节课被‘具象化’（即在文件系统中为其分配了一个真实路径）时，存在一个问题。”
- **修改后**：“物化级联 (Materialization cascade) 存在一个问题。”

这种极致的精简，会在后续无数次的会话中带来巨大的回报。

这个机制被内置在了 [`/grill-with-docs`](https://www.google.com/search?q=./skills/engineering/grill-with-docs/SKILL.md) 中。它不仅是一个深度拷问会话，更能辅助你与 AI 共同沉淀统一语言，并将那些难以言传的架构决策以内联的形式记录在 ADR（架构决策记录）中。

很难用语言形容这个技巧到底有多强大。它可能是这个仓库里最硬核的一招。亲自试一下，你就懂了。

> [!TIP]
> 统一语言不仅能减少啰嗦的废话，还有诸多优势：
>
> - **变量、函数和文件命名高度一致**，全面对齐统一语言。
> - 因此，**代码库对智能体来说更容易进行上下文导航**。
> - 由于智能体掌握了更精炼的表达方式，它在**思考（思维链）上消耗的 Token 也会显著减少**。

### #3：代码跑不起来

> “始终保持小步快跑，稳扎稳打。反馈的频率就是你的限速器。永远不要一口气接下过于庞大的任务。”
> David Thomas & Andrew Hunt, [《程序员修炼之道》(The Pragmatic Programmer)](https://www.google.com/search?q=https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**痛点**：假设你和智能体在需求上已经完全对齐了。如果智能体*依然*产出垃圾代码怎么办？

这时候必须审视你的反馈循环 (Feedback loops) 了。如果智能体无法获得“它写的代码跑起来到底咋样”的真实反馈，它就相当于在盲飞。

**解决方案**：你需要常规的闭环反馈基建：静态类型检查、浏览器环境访问以及自动化测试。

对于自动化测试而言，红-绿-重构 (Red-Green-Refactor) 循环至关重要。即让智能体先写一个会报错的测试用例，再去修复代码让测试通过。这能为智能体提供持续且稳定的反馈，从而产出质量极高的代码。

我编写了一个 **[`/tdd`](https://www.google.com/search?q=./skills/engineering/tdd/SKILL.md) 技能**，你可以无缝插拔到任何项目中。它强制执行红-绿-重构循环，并为智能体提供了大量关于“什么是好测试、什么是烂测试”的指导原则。

针对 Debug 场景，我也编写了一个 **[`/diagnose`](https://www.google.com/search?q=./skills/engineering/diagnose/SKILL.md)** 技能，它将业界最佳的排障实践封装成了一个极简闭环。

### #4：我们造了一坨“大泥球 (Ball of mud)”

> “*每天*都要对系统的设计进行投资。”
> Kent Beck, [《解析极限编程》(Extreme Programming Explained)](https://www.google.com/search?q=https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> “最好的模块是‘深模块 (Deep modules)’。它们通过极简的接口暴露出极度强大的底层能力。”
> John Ousterhout, [《软件设计哲学》(A Philosophy Of Software Design)](https://www.google.com/search?q=https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**痛点**：大多数使用 AI 智能体堆出来的应用，架构都异常复杂且极难重构。因为智能体极大提升了写代码的速度，它同时也以前所未有的速度加剧了软件熵增 (Software entropy)。

**解决方案**是采用一种针对 AI 辅助开发的激进新视角：必须极其在乎代码架构设计。

这种理念贯穿了本技能库的每一层：

- [`/to-prd`](https://www.google.com/search?q=./skills/engineering/to-prd/SKILL.md) 会在生成 PRD 之前，盘问你当前到底在修改哪些底层模块。
- [`/zoom-out`](https://www.google.com/search?q=./skills/engineering/zoom-out/SKILL.md) 强制智能体跳出局部细节，从全局系统架构的视角来解释代码。
- 最核心的是，[`/improve-codebase-architecture`](https://www.google.com/search?q=./skills/engineering/improve-codebase-architecture/SKILL.md) 能帮你拯救那些已经腐化成“大泥球”的代码库。我强烈建议你每隔几天就在自己的代码库里跑一次这个技能。

### 总结

软件工程的基本功在 AI 时代比以往任何时候都更加重要。这套技能库是我将这些基本功浓缩为可复用实践的最佳心血，旨在帮助你交付职业生涯中最棒的应用。尽情享受吧。

## 指南参考 (Reference)

### 工程类技能 (Engineering)

我每天在代码开发中使用的核心技能。

- **[diagnose](https://www.google.com/search?q=./skills/engineering/diagnose/SKILL.md)** — 针对疑难 Bug 和性能退化 (Regression) 的严密排障循环：复现 → 最小化 → 提出假设 → 埋点插桩 → 修复 → 回归测试。
- **[grill-with-docs](https://www.google.com/search?q=./skills/engineering/grill-with-docs/SKILL.md)** — 深度拷问会话，利用现有的领域模型挑战你的方案，精准统一术语，并内联更新 `CONTEXT.md` 和 ADR 文档。
- **[triage](https://www.google.com/search?q=./skills/engineering/triage/SKILL.md)** — 利用基于 Triage 角色的状态机来分流/定级 Issue。
- **[improve-codebase-architecture](https://www.google.com/search?q=./skills/engineering/improve-codebase-architecture/SKILL.md)** — 挖掘代码库中可以被“深化 (Deepening)”的重构机会，依据是 `CONTEXT.md` 中的业务统一语言以及 `docs/adr/` 中的历史架构决策。
- **[setup-matt-pocock-skills](https://www.google.com/search?q=./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 脚手架工具，用于初始化供其他工程技能消费的单仓级配置（如 Issue 追踪器类型、分流标签字典、领域文档目录结构）。在使用 `to-issues`, `to-prd`, `triage`, `diagnose`, `tdd`, `improve-codebase-architecture` 或 `zoom-out` 之前，每个仓库需运行一次。
- **[tdd](https://www.google.com/search?q=./skills/engineering/tdd/SKILL.md)** — 严格遵循 红-绿-重构 循环的测试驱动开发。以“垂直切片 (Vertical slice)”的方式逐个构建需求或修复 Bug。
- **[to-issues](https://www.google.com/search?q=./skills/engineering/to-issues/SKILL.md)** — 将任何方案、技术规范或 PRD，按照垂直切片原则拆解为 GitHub 上可独立认领的 (Independently-grabbable) Issue。
- **[to-prd](https://www.google.com/search?q=./skills/engineering/to-prd/SKILL.md)** — 将当前的对话上下文提炼总结为 PRD，并直接以 GitHub Issue 的形式提交。没有反问环节——纯粹是对你们已讨论内容的精华合成。
- **[zoom-out](https://www.google.com/search?q=./skills/engineering/zoom-out/SKILL.md)** — 指令智能体拉高视角，针对极其陌生的代码区块，提供宏观上下文或高层架构剖析。
- **[prototype](https://www.google.com/search?q=./skills/engineering/prototype/SKILL.md)** — 快速糊一个用完即弃的原型 (Throwaway prototype) 来验证设计——它可以是用于验证状态管理/业务逻辑的可运行纯终端 App，也可以是同一路由下可通过开关切换的多个差异巨大的 UI 变体方案。

### 生产力技能 (Productivity)

通用工作流提效工具（非特定于写代码）。

- **[caveman](https://www.google.com/search?q=./skills/productivity/caveman/SKILL.md)** — 极度压缩的通信模式（山顶洞人模式）。剔除所有废话并保持 100% 技术准确率，可将 Token 消耗暴降约 75%。
- **[grill-me](https://www.google.com/search?q=./skills/productivity/grill-me/SKILL.md)** — 让 AI 对你的方案或设计进行毫无留情的交叉盘问，直到决策树的所有边缘分支都被彻底解决。
- **[handoff](https://www.google.com/search?q=./skills/productivity/handoff/SKILL.md)** — 将当前上下文极其庞大的对话压缩为一份“交接文档 (Handoff document)”，以便你可以开个新会话让另一个智能体接力开发。
- **[write-a-skill](https://www.google.com/search?q=./skills/productivity/write-a-skill/SKILL.md)** — 使用合理的工程结构、渐进式披露 (Progressive disclosure) 原则以及捆绑资源来创建全新的自定义技能。

### 杂项 (Misc)

备用库，我留着但使用频率不高。

- **[git-guardrails-claude-code](https://www.google.com/search?q=./skills/misc/git-guardrails-claude-code/SKILL.md)** — 配置 Claude Code 拦截钩子，在它执行高危 git 命令（如 `push`, `reset --hard`, `clean` 等）前将其拦下。
- **[migrate-to-shoehorn](https://www.google.com/search?q=./skills/misc/migrate-to-shoehorn/SKILL.md)** — 将测试文件中的 `as` 类型断言平滑迁移至 `@total-typescript/shoehorn`。
- **[scaffold-exercises](https://www.google.com/search?q=./skills/misc/scaffold-exercises/SKILL.md)** — 脚手架工具，用于一键生成包含章节、题目、解答与解析的标准练习题目录结构。
- **[setup-pre-commit](https://www.google.com/search?q=./skills/misc/setup-pre-commit/SKILL.md)** — 初始化 Husky 的 pre-commit 钩子，自动集成 lint-staged、Prettier、TSC 类型检查和单元测试。
