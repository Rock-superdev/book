---
title: "当 AI 替你做完所有事：腾讯 WorkBuddy 深度体验与产品哲学"
date: 2026-07-09
tags: ["AI Agent", "WorkBuddy", "腾讯云", "产品分析", "办公自动化"]
author: workbuddy-research-team
---

2026 年 6 月的一个周二早上，跨境电商运营 Lisa 收到老板一条消息："下午 3 点前给我一份 Q2 北美市场各 SKU 销售对比，带图表和原因分析。" 她没有打开 Excel、没有找数据组、没有约会议，而是在 WorkBuddy 里敲了一句："读 ~/Desktop/Q2 销售数据 文件夹下所有 Excel，合并去重后按 SKU 出季度对比图，生成一份含原因假设的分析报告，存到桌面。"

40 分钟后，一份带 5 张图表的 .docx 报告静静躺在她桌面，旁边是一份格式干净的 .xlsx 数据透视表。她点了一下"通过微信发给老板"，起身去倒了杯咖啡。

这不是科幻。这是 2026 年 5 月 28 日腾讯云 Cloud Day Hong Kong 上正式发布的 WorkBuddy AI 桌面工作台的典型一天。[¹](https://www.workbuddy.ai/)

## 一、产品定位：它不是 Asana，也不是 ChatGPT

WorkBuddy 是腾讯云 CodeBuddy 团队推出的**多智能体 AI 桌面工作台**（Multi-agent AI Agent Desktop Workstation），2026-05-28 在 Cloud Day Hong Kong 发布，2026-07-05 在 Product Hunt 上拿到 **Launch of the Day #1**。[²](https://www.producthunt.com/products/workbuddy-2/awards)

在做任何对比之前必须先澄清一件事：WorkBuddy **不是** Asana / Trello / Notion / Jira / Linear 那一类"项目管理/协作"工具。它没有看板、没有任务卡流转、没有评论线程、没有 @ 派活流——这些维度在它身上几乎不存在。它的"任务/协作/AI/集成"模块是 **AI Agent 工作流** 的对应物，不是传统 SaaS 的对应物。

如果硬要用一句话给它的定位画边界：**Asana 类工具解决"如何让一群人协作完成一件事"；WorkBuddy 解决"如何让一支 AI 团队替一个人把事做完"。**

官方在 PH 上对自身定位的描述非常精准："AI 让'想'变快了，但人仍然要花数小时把'回答'变成'可交付的文件'。WorkBuddy 就是要关闭从 AI 输出到可交付物之间的 Execution Gap（执行鸿沟）。"[³](https://www.producthunt.com/products/workbuddy-2)

### 目标用户

WorkBuddy 的目标用户画像由官方和第三方评测共同勾勒出三类：

- **"一人即公司"型**：自由职业者、小团队负责人、跨境电商运营——不愿在多个工具间手工搬运。腾讯云 Cloud Day 上专门强调这是典型场景。[⁴](https://www.tencentcloud.com/act/pro/workbuddy)
- **企业内部知识工作者**：运营、数据、行政、HR、产品经理，每天在 Excel、PPT、邮件、IM 之间切来切去。
- **市场调研/竞品分析人员**：需要快速产出结构化报告。

Shanghai Jiaoruan 的产品经理 Jiahe Sun 在官方证言里说得很直接："相比传统办公软件，更像 AI 同事——能理解、拆解、执行任务；连表格处理、内容生成、信息整理、报告输出，对 HR/运营/行政/PM 都有帮助。"[⁵](https://www.workbuddy.ai/)

## 二、核心功能矩阵：按"用它干什么"组织

传统 SaaS 的功能介绍按"任务/协作/AI/集成"分章，但 WorkBuddy 的功能不是这样组织的——它是按"用户用 WorkBuddy 解决什么问题"组织的。下面这张表按六个用户视角维度拆解它的能力：

| 维度 | WorkBuddy 提供的能力 | 典型使用场景 |
|---|---|---|
| **任务/项目管理** | 一次性 brief → 多 Agent 拆解 → 并行执行 → 真实文件交付；支持周期调度任务（每天 9 点自动导订单并发群） | "合并我桌面 Q1 销售文件夹的所有 Excel，生成柱状图+分析报告"（官方示例）[⁶](https://www.tencentcloud.com/techpedia/144100?lang=en) |
| **协作沟通** | **9 个** IM 通道远程派活：Slack / Telegram / Discord / WeChat Assistant Bot / 企业微信 / QQ / 元宝派 / 钉钉 / 飞书 | 通勤路上用微信让 WorkBuddy 准备会议材料，桌面端执行完直接回传微信[⁷](https://www.tencentcloud.com/act/pro/workbuddy) |
| **AI 能力** | 100+ 行业 Expert 开箱即用；Skill 市场和自定义 Slash 命令；TokenHub 路由 14 个大模型（DeepSeek-V4-Pro/Flash、MiniMax M2.5/M3、Kimi K2.6、GLM 5.1/5.2、腾讯混元等） | "让运营专家+数据专家+财务专家同时分析一份方案，要求保留各自动观点"[⁸](https://www.workbuddy.ai/pricing) |
| **数据/报表** | 直接读写本地 Excel/PPT/Word，输出 .xlsx/.docx/.pptx/.pdf 真实文件；支持按 quarter-over-quarter 等维度计算 | 输入一句"按渠道出季度对比图"，输出一份带图的 PPT 落到桌面 |
| **集成生态** | 腾讯生态（企微/飞书/钉钉/QQ/元宝派/腾讯文档/腾讯会议）+ 海外（GitHub/Jira/Linear/Notion/Google Drive/Slack/Office/Gmail） | 在飞书群里 @WorkBuddy bot 触发一份周报生成[⁹](https://www.workbuddy.ai/) |
| **权限/合规** | 沙盒执行 + 文件夹显式授权 + Team 版 Admin Console + Enterprise 高级安全 | Team 管理员可统一席位、统一计费、统一审计[¹⁰](https://www.workbuddy.ai/pricing) |

几个值得展开的点：

**第一，交付物是真实文件，不是聊天回复**。这是它和 ChatGPT / Claude / Gemini 最大的体感差异——你不是在和一个 bot 对话，你是在和一个能跑 Python、操作 Excel、写 PPT 的"团队"对话，最后拿到的不是 Markdown 文本，而是落到桌面的 .xlsx 和 .pptx。PH 上官方对此的描述是 "Real deliverables: finished files in your folders, not trapped in a chat"。[¹¹](https://www.producthunt.com/products/workbuddy-2)

**第二，本地文件直读直写**。首次启动时用户显式授权 Desktop / Documents / Downloads 等本地文件夹，Agent 直接读写，无需先上传云端。这点和 Manus、Devin 的"沙箱里跑"路线不同——WorkBuddy 更贴近"你电脑上的智能助理"。[¹²](https://www.tencentcloud.com/techpedia/144100?lang=en)

**第三，调度任务是一等公民**。WorkBuddy 把"每天 9 点自动导订单并发群"这种周期任务做成了 first-class feature，而不是塞进 cron 配置文件里。这对一个每天要发日报、周报、月报的运营/数据岗位意义很大。

**第四，Skill 市场 + 自定义 Slash 命令**。官方文档列出 Skill 示例：PDF 处理、Excel 数据分析、PPT 构建、浏览器自动化等；用户也可以基于 Markdown 写自己的 Skill 放进 `skills/` 目录，把命令放进 `commands/` 目录。这意味着它有"用户共建生态"的潜力，而不仅仅是一个封闭产品。[¹³](https://www.tencentcloud.com/techpedia/144100?lang=en)

## 三、差异化亮点：与同类 AI Agent 桌面工作台的真实差异

用户对标的 Asana/Trello/Notion/Jira/Linear 与 WorkBuddy 不在同一赛道（见第一章定位说明）。下面分两组对比：**（a）与真正可比的 AI Agent 桌面工具对比**；**（b）与 Manus/Devin/ChatGPT 等热门 Agent 对比**。

### 与同类 AI Agent 桌面工作台对比

来自 CoworkHow 2026 年 AI Agent 工具横评（覆盖 8 款桌面 Agent）的对比表：[¹⁴](https://coworkhow.com/comparison)

| 工具 | 主要定位 | 多 Agent 并行 | 远程通道 | 桌面 GUI | Free tier | 目标用户 |
|---|---|---|---|---|---|---|
| **Tencent WorkBuddy** | AI 工作台（办公+跨工具） | ✅ 多 Agent 并行 | **9 个**：Slack/Telegram/Discord/微信助手/企微/QQ/元宝派/钉钉/飞书 | ✅ Mac/Win | ✅（2 周 Pro 试用 250 credits；PH 首发前 300 名额外送 500 credits，截至 2026-07-20） | 知识工作者（HR/运营/PM/销售） |
| Claude Cowork | 文档自动化 | ✅ 多个 | ✅ | ✅ | — | 全员（非技术） |
| Kimi Work | 本地 Agent+浏览器自动化 | ✅ 最多 300 个 swarm | — | ✅ Mac/Win | — | 知识工作者 |
| OpenAI Codex | 编码 Agent | ✅ 多个并行线程 | ✅ | ✅ + CLI | — | 开发者 |
| Gemini CLI | 开源终端 Agent | 受限 | — | ❌ CLI only | ✅（60 req/min） | 开发者 |
| Google Antigravity 2.0 | 多 Agent 编排 SDK | ✅ | — | ✅ + CLI + SDK | — | 开发者团队 |
| Devin Desktop | Agent IDE（Kanban 视角） | ✅ | — | ✅ + Cloud | — | 工程团队 |
| ZCode (z.ai) | GLM-5.2 长任务 ADE | ✅ | WeChat/Feishu/Telegram | ✅ 全平台 | — | GLM 用户 |

从这张表可以看出 WorkBuddy 的卡位：**它不是给开发者的工具，而是给知识工作者的桌面 Agent；它不是单 Agent，而是开箱即用的"100+ 专家团队"**。和它最像的是 Claude Cowork 和 Kimi Work，但 WorkBuddy 在两个维度有显著差异：

1. **远程通道覆盖最广**：**9 个** IM 通道（Tencent WorkBuddy）对比 Claude Cowork/Kimi Work 的 0-1 个。如果你日常在微信/飞书/钉钉/Slack 上办公，这直接决定了你会不会用它。
2. **腾讯生态集成最深**：WorkBuddy 与 CodeBuddy（开发者 AI 编程助手）共享订阅；WorkBuddy 与企业微信/飞书/钉钉/QQ/元宝派/腾讯文档/腾讯会议全线打通。[¹⁵](https://www.workbuddy.ai/pricing)

### 与 Manus / Devin / ChatGPT 等热门 Agent 对比

- **vs ChatGPT / Claude / Gemini（通用 Chatbot）**：WorkBuddy 的多 Agent 架构自动做工作流编排（拆解、调工具、综合输出），单轮 Chatbot 把编排留给用户。多步骤任务下 WorkBuddy 设计上更适合。Eigent 评测对此给出的判断是：WorkBuddy 是 "credible, production-ready AI agent workspace from one of the world's largest tech companies"。[¹⁶](https://www.eigent.ai/blog/workbuddy-ai-review)

- **vs Manus（2025-12 被 Meta 收购的研究型 Agent）**：Manus 强在 GAIA 评测（基础 86.5%、中等 70.1%、复杂 57.7%），定位"研究+报告生成"；WorkBuddy 强在"办公全场景+腾讯生态 IM 联动+多模型路由+跨工具本地执行"。Manus 单次复杂任务耗 500-900 credits；WorkBuddy 用 credit 月度池子（月费里送 1000-2000 credits）。[¹⁷](https://viktor.com/blog/viktor-vs-devin-vs-manus)

- **vs Devin（编码 Agent）**：Devin 只做软件工程，独立任务 ~15% 成功率（无辅助下），$20-$500/月+ACU 计费；WorkBuddy 主战场不是编码，是办公全场景。

### 一个产品哲学层面的洞察

WorkBuddy 在 PH 上被用户问得最多的一个问题是：**"当多个 Expert 并行跑同一个任务，它们之间真的会互相校验吗？还是合并步骤只是混合各自动看法、不一致被悄悄消失？"**[¹⁸](https://www.producthunt.com/products/workbuddy-2)

官方的回答（Sherina Chen, maker 回复）是：**默认"综合输出"，但用户可以在 brief 里明确要求"保留各 Agent 原始观点"，让分歧可见**。Caddy Liu（另一位 maker）补充说合并更接近"editor/moderator"而非简单投票：若有专家标记反对意见，该信号会影响最终输出——可能是修正、补 caveat、reframe，或显式标注存在未解决的分歧。

这个设计选择背后其实有一个产品哲学：**WorkBuddy 把"专家之间的真实分歧"视为有价值的信号，而不是要被融合掉的噪声**。这一点和很多多 Agent 框架（默认最后只有一个统一答案）在底层假设上不同。在 PM/HR/战略咨询这类"需要多视角碰撞"的工作场景里，这个差异会被放大成体感优势：你不需要每个决策都让 AI 综合一次，你可以让它把三个不同立场的观点并列呈现，然后你自己判断。

——这是 WorkBuddy 在"产品设计哲学"层面值得专门点出来的一个洞察，而不仅仅是一个功能列表项。

## 四、商业化与定价：海外/国内两套体系，Credit 制而非时长制

### 海外版（workbuddy.ai，国际站）

| 套餐 | 价格 | Credits | 包含 |
|---|---|---|---|
| **Free** | $0 | 新用户免费试用 Pro 2 周，含 250 credits（PH 首发前 300 名额外送 500 credits，截至 2026-07-20） | 高级模型全部可用；Next-Step Edit 无限；BuddyTab 无限；Preview 功能 |
| **Pro** | **$9.95/月**（年付优惠 50%，原价 $19.90/月） | 1,000 credits/月 | 全部免费功能 + 大量 Skills 与 Connectors + 个性化记忆 |
| **Team** | **$40/seat/月**（$480/seat/年） | 1,000 credits/seat/月（共享池） | 全部 Pro 功能 + Admin Console + 统一计费 + IDE/CLI/Plugin 多形态 |
| **Enterprise** | 联系销售 | — | 高级安全 + 强管理控制 |

来源：[WorkBuddy Pricing](https://www.workbuddy.ai/pricing)、[Tencent Cloud WorkBuddy](https://www.tencentcloud.com/act/pro/workbuddy)

### 中国版（腾讯云子站）

| 版本 | 价格 | Credits |
|---|---|---|
| 个人专业版 | 58 元/人/月 | 2,000 credits/月 |
| SaaS 企业版（旗舰） | 198 元/人/月 | 2,000 credits/席位（共享） |
| 专属云企业版 | 316 元/人/月 | 2,000 credits/用户（共享） |

来源：[Eigent 转载腾讯云定价](https://www.eigent.ai/blog/workbuddy-ai-review)

### 计费模式要点

**Credit 制而非时长制**：复杂任务消耗更多 credits，新手起步 credit 用完可购买额外包。对企业采购方的好处是"花多少算多少，不会出现月末莫名其妙的高账单"；对个人用户的风险是"复杂任务可能迅速耗光月度池子"。[¹⁹](https://www.tencentcloud.com/techpedia/144100?lang=en)

**TokenHub 模型市场**：14 个模型，每个新用户 100 万免费 credits 起步——这是一个比较激进的新用户补贴策略，目的是让用户尝试不同模型，最后沉淀到 WorkBuddy 的生态里。

**跨产品订阅**：WorkBuddy 订阅同时适用于 CodeBuddy——这是腾讯把"开发者 AI 编程助手"和"办公 AI 工作台"打包销售的策略，对同时是开发者又要做运营工作的人有吸引力。

从 ROI 视角看，Pro $9.95/月对应 1000 credits，对一个每天花 1-2 小时在数据搬运/报表生成的运营/PM 来说，理论上首月就能收回时间成本（按每次中等复杂任务消耗约 150 credits 估算，实际随任务复杂度差异较大）。这是它对企业买家最有说服力的 ROI 论证角度。

## 五、用户口碑与市场反馈：刚 launch 一个月，信号不足但有方向

> ⚠️ 在 G2/Capterra/FeaturedCustomers 上搜索 "WorkBuddy" 会撞到澳大利亚 WorkBuddy Software（现场服务管理产品），与本文主角无关；本文所有口碑数据均来自 PH、X、官方首页与第三方评测。

### Product Hunt 核心阵地

- **2026-07-05 Launch**：获得 **Launch of the Day #1**，累计 20+ upvote。
- **评分**：4.0/5，仅 1 条正式 review（早期阶段）。
- **官方推广**：前 300 名 PH 来客额外送 500 credits，截止 2026-07-20。

来源：[WorkBuddy Awards](https://www.producthunt.com/products/workbuddy-2/awards)

真实用户评论样本（原始出处全部为 PH 评论页 [²⁰](https://www.producthunt.com/products/workbuddy-2)）：

> **MAVOUNGOU Malahim Kiamet Zenou**（2026-07）："execution gap 描述很到位……通常 AI 工具解决了思考瓶颈，但留你独自面对'把它变成可交付物'的部分。"

> **Omri Ben-Shoham**（2026-07）："我最好奇的是 expert 互相校验——当一个 expert 标记某事时，它真的会改变最终综合输出，还是合并步骤只是混合各自动看法、不一致被悄悄消失？"

> **Vijay Garg**（2026-07）："如果一个专家团队对一个任务（研究、起草、QA）并行跑，能否给每个专家分配不同的模型？"

> **Dogan Akbulut**（2026-07）："一直在协调不同 AI 工具，有统一的专家团队听起来很理想。'专家们'到底怎么彼此沟通？"

这些评论的共同信号是：**用户最关心的不是"AI 能不能干活"，而是"AI 之间怎么协作、怎么保留分歧"**——这恰恰印证了第三章提到的产品哲学洞察。

### X / Twitter

- **Tencent Cloud 官方**（2026-07-06）："WorkBuddy - No. 1 Product of the Day on Product Hunt. People don't just want more AI answers. They want work that actually ships."（likes 15、retweets 2）[²¹](https://x.com/tencentcloud/status/2074086751531049272)
- **AinaAiTech**（2026-07-06）："#1 on Product Hunt Huge congrats! … Free credits too Had to try it"
- **@dftyuon**（2026-07-07）："Looking crazy wanna explore it"

注意：这些评论距 launch 仅几天，属于"高情绪+低使用深度"型，作为口碑信号的可信度有限。

### 第三方深度评测

- **Eigent Blog**（2026-06）：把 WorkBuddy 定位为 "credible, production-ready AI agent workspace from one of the world's largest tech companies"；同时指出"国际体验可能滞后，地区碎片化"。[²²](https://www.eigent.ai/blog/workbuddy-ai-review)
- **MyClaw Blog**（2026-07-02）：建议把 WorkBuddy 与 OpenClaw / Hermes Agent 类比，关注"实际完成的任务而不是 demo"。[²³](https://myclaw.ai/blog/workbuddy)
- **CoworkHow 横评**（2026）：把 WorkBuddy 归入"知识工作者 Agent"组，与 Claude Cowork / Kimi Work 同组，与 Codex/Gemini CLI/Devin 等开发者工具区别开。[²⁴](https://coworkhow.com/comparison)

### 官方证言（workbuddy.ai 首页，2026-07-09 抓取）

| 姓名 | 身份 | 表述要点 |
|---|---|---|
| Wanqing Zhao | Product Manager, Jieshun Technology | "WorkBuddy is heavily used in our daily office work, including PPT creation, document data analysis, and image design. It improves efficiency by more than 90% in individual workflows, though occasional retry errors and lag can still happen." |
| Wenbo Zhou | Product Operations, Maiya Media | "I cannot write a single line of code, but I had wanted to build web apps for clients and my alma mater for more than a year. With WorkBuddy, I made it happen in a week. The built-in Experts are very friendly for beginners." |
| Jiahe Sun | Product Manager, Shanghai Jiaoruan | "Compared with traditional office software, WorkBuddy feels more like an AI colleague that understands, breaks down, and executes tasks. It connects spreadsheet processing, content generation, information organization, and report output, which is helpful for HR, operations, admin, and product managers." |
| Ruixiang Liu | Technical Engineer, Tencent | "What impresses me most about WorkBuddy is that it does not just give suggestions like a typical AI chat tool. It actually completes office tasks. From organizing files and analyzing spreadsheets to generating reports, everything can start with a single sentence." |
| Mingyuan Zhang | Senior Engineer, Tencent | "After using WorkBuddy, office workflows feel much simpler. Data summaries, chart analysis, and weekly reports used to require switching across tools. Now I can hand them directly to an AI Agent, and the efficiency gain is obvious." |
| Sihan Li | Delivery Manager, Tencent | "WorkBuddy has a very clear positioning. It is not a complex tool only for technical users, but an AI workbench for everyday professionals. Natural-language tasks, parallel multi-agent execution, and final document or chart delivery are genuinely useful." |
| Kevin Zheng | Frontend Developer, Tencent | "CodeBuddy and WorkBuddy both feel great. Remote mobile connectivity is convenient, and sending instructions through WeChat or WeCom is very smooth. Many colleagues have moved from Cursor to CodeBuddy." |
| Haoran Chen | Project Manager, Mercedes-Benz | "We use WorkBuddy ourselves and have promoted it across 15 departments. The new mini-program experience makes it quick to try without downloading, and colleagues say it feels like having an AI work partner." |

来源：[workbuddy.ai 首页](https://www.workbuddy.ai/)

需要单独点出的负面信号：**Jieshun Technology 的 PM Wanqing Zhao 在官方证言里坦承"efficiency improvement of 90%+ in individual workflows, though occasional retry errors and lag can still happen"**——这条信号很重要，因为它来自官方渠道而非第三方，说明 WorkBuddy 团队自己承认早期产品稳定性不是完美状态。

## 六、局限性与给读者的启示

### 已知局限（基于官方与第三方明示事实）

**1. 产品成熟度早期阶段**
- 2026-05-28 才正式发布，2026-07-05 才上 PH，国际版早期，文档与体验仍在迭代。
- PH 上只有 1 条正式 review，4.0/5，样本不足。
- 真实用户报告"偶发重试错误和卡顿"（Wanqing Zhao，官方证言）。

**2. 地区与生态碎片化**
- 官方说明：定价、文档、部分功能为中国市场优化，国际体验可能滞后。
- 第三方评测：在腾讯生态（微信、飞书、钉钉）内最强；Google Workspace / Slack / GitHub / Notion / Telegram 等海外 SaaS 栈表现待验证。

**3. 合规清单未公开**
- 截至 2026-07-09，公开页面未公示 SOC2 / ISO27001 / GDPR 等合规认证名（Enterprise 页面仅写"advanced security"）。采购方应在签约前向厂商索取最新合规清单。
- 数据出境：跑在国际版的用户需自行评估跨境数据合规（涉及腾讯云基础设施）。

**4. 与传统协作 SaaS 比的功能缺口（事实层面）**
- 无传统任务卡 / 看板 / 状态字段 / 评论线程。
- 无 @ 派活流：任务派活路径是"对话或 IM 派 brief"，不是"@ 同事"。
- 没有公开 REST API / Webhook 端点：仅 MCP 风格工具层。
- 没有内嵌多人实时协作光标：交付物是文件，协作靠 Office / Notion / Google Docs 自身。

**5. 同名陷阱**
- G2 / Capterra / FeaturedCustomers 上的 "WorkBuddy" 实为澳大利亚 WorkBuddy Software（现场服务管理/调度），与腾讯无关。**不要**引用这两条评论当作腾讯 WorkBuddy 的口碑——这是一个在搜索调研时容易踩的坑。

### 给不同读者的可借鉴点

**对决策层（领导/老板）**：
- ROI 视角：Pro $9.95/月对应 1000 credits，对一个每天花 1-2 小时在数据搬运/报表生成的运营/PM，理论上首月就能收回时间成本（按 150 credits/中等任务估算，实际差异较大）。
- 选型边界：如果你的核心痛点是"跨团队任务流转、状态同步、合规审计"，传统 Asana/Notion/Jira 仍不可替代；如果你的核心痛点是"一个人（或小团队）要把多个工具的产出拼成最终交付物"，WorkBuddy 是当前市场上最接近"AI 工作搭子"的产品形态。
- 合规风险：海外版数据合规清单未公开，跨国企业部署前需自行评估。

**对产品经理（同行视角）**：
- 多 Agent 哲学可借鉴：WorkBuddy 把"专家之间的真实分歧"视为有价值的信号，而不是要被融合掉的噪声——这在多 Agent 框架里是一个底层设计选择，可以借鉴到自己的产品中。
- IM 作为"控制台"是值得抄的：它把 9 个 IM 通道变成"派活入口"，触达用户的方式变了，而不是只在桌面 GUI 里等用户来。
- Skill 市场 + 自定义 Slash 命令是用户共建生态的正确打开方式，但门槛（写 Markdown）决定了它更适合 P5 以上用户，大众化还需要简化。

**对创业者**：
- WorkBuddy + CodeBuddy 共享订阅 + TokenHub 模型市场 = 腾讯在 AI Agent 时代的"操作系统+应用商店"打法，这是中国云厂在 2026 年给出的一个清晰战略卡位。
- 切入角度：WorkBuddy 没有做好的领域（传统协作、跨团队流转、企业合规审计）仍是大公司的护城河；WorkBuddy 表现强的领域（知识工作者单人/小团队的全场景办公）还有"垂直行业版"的创业机会。

## 结语

WorkBuddy 不是另一个 ChatGPT，也不是另一个 Asana。它是腾讯云在 AI Agent 时代给出的一个回答——**当 AI 替你做完所有事，人需要做什么？** 答案是：把 brief 写清楚，把分歧看清楚，把判断做出来。其余的，交给那支 100+ Expert 的 AI 团队。

---

## 字数统计

中文字符数（不含 frontmatter、标题、参考资料链接、空格、标点）：**约 4,280 字**

## 参考资料链接清单

1. [WorkBuddy 官网（海外）](https://www.workbuddy.ai/)
2. [WorkBuddy Awards - Product Hunt](https://www.producthunt.com/products/workbuddy-2/awards)
3. [WorkBuddy - Product Hunt 主页](https://www.producthunt.com/products/workbuddy-2)
4. [腾讯云 WorkBuddy 子站（中国）](https://www.tencentcloud.com/act/pro/workbuddy)
5. [WorkBuddy 首页用户证言](https://www.workbuddy.ai/)
6. [Tencent WorkBuddy Download, Install and Use Guide (Overseas)](https://www.tencentcloud.com/techpedia/144100?lang=en)
7. [腾讯云 WorkBuddy 产品页（含 IM 通道与场景）](https://www.tencentcloud.com/act/pro/workbuddy)
8. [WorkBuddy 定价页](https://www.workbuddy.ai/pricing)
9. [WorkBuddy 集成生态](https://www.workbuddy.ai/)
10. [WorkBuddy Enterprise 高级安全](https://www.workbuddy.ai/pricing)
11. [WorkBuddy - Product Hunt 描述（"finished files in your folders, not trapped in a chat"）](https://www.producthunt.com/products/workbuddy-2)
12. [Tencent WorkBuddy Techpedia - 本地文件操作](https://www.tencentcloud.com/techpedia/144100?lang=en)
13. [Tencent WorkBuddy Techpedia - Skill 市场与 Slash 命令](https://www.tencentcloud.com/techpedia/144100?lang=en)
14. [CoworkHow - 8 款 AI Agent 桌面工具横评](https://coworkhow.com/comparison)
15. [WorkBuddy 与 CodeBuddy 订阅共享](https://www.workbuddy.ai/pricing)
16. [Eigent Blog - WorkBuddy AI 深度评测](https://www.eigent.ai/blog/workbuddy-ai-review)
17. [Viktor Blog - Manus vs Devin vs Viktor](https://viktor.com/blog/viktor-vs-devin-vs-manus)
18. [WorkBuddy PH 评论（Omri Ben-Shoham 等）](https://www.producthunt.com/products/workbuddy-2)
19. [Tencent WorkBuddy Techpedia - Credit 计费](https://www.tencentcloud.com/techpedia/144100?lang=en)
20. [WorkBuddy - Product Hunt 评论页（用户原话引用）](https://www.producthunt.com/products/workbuddy-2)
21. [Tencent Cloud X 账号 - #1 Product of the Day 公告](https://x.com/tencentcloud/status/2074086751531049272)
22. [Eigent Blog - WorkBuddy 区域碎片化](https://www.eigent.ai/blog/workbuddy-ai-review)
23. [MyClaw Blog - WorkBuddy 实用视角](https://myclaw.ai/blog/workbuddy)
24. [CoworkHow - 知识工作者 Agent 分组](https://coworkhow.com/comparison)