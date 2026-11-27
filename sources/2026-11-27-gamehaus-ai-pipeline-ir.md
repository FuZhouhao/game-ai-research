# 源文归档｜Gamehaus：AI 管线将游戏原型工作量降约 90%，首批 AI 构建游戏合集 Ease Games 上线（Gamehaus IR）

- **原始 URL**：https://ir.gamehaus.com/2026-11-16-Gamehaus-AI-Pipeline-Optimizes-Game-Prototyping-Effort-by-About-90-,-Based-on-Internal-Estimates-Gamehaus-First-AI-Built-Game-Collection,-Ease-Games,-Goes-Live
- **抓取日期**：2026-11-27（原文发布时间 2026-11-16，据 URL 路径与页面元信息；正文电头日期在城市名被剥离后未完整显示）
- **类型**：上市公司投资者关系新闻稿（PRNewswire 通稿）
- **作者/发布方**：Gamehaus Holdings Inc.（Nasdaq: GMHS），SOURCE: Gamehaus Holdings Inc.
- **关联条目**：daily/2026-11-27.md 条目 32；详尽版 daily/details/2026-11-27-industry-policy.md
- **存档目的**：原文全文存档，防源页失效（link rot）

## 借鉴要点

- 效率数字（公司自述、标注为内部估算 "Based on Gamehaus' internal estimates"）：可玩原型的制作从"约 3 名开发 × 1~1.5 周"降到"平均 1 名开发 × 1.5~2 天"，按人日计即从 15–22.5 人日降到 1.5–2 人日，降幅 "approximately 87%–93% (about 90% at the midpoint)"。
- 产品已落地：首个基于该管线的产物 __Ease Games: Fun Anytime__ 已上线 Google Play，首发 12 款休闲游戏（数独 Sudoku、Arrows Out、Water Sort 等）；后续更新到 20 款，目标"约两个季度内做到约 50 款"（"targets approximately 50 games in the collection within the next two quarters"）。
- 交付时间线：2026 年 8 月下旬与 Witmani 启动项目 → 9 月中工具与工作流就绪 → 10 月中完成 app 框架 + 前 12 款游戏 → 10 月底上线并完成首轮验证，即"kickoff 到 12 款成品约七周"。
- 管线覆盖面：涵盖 "game implementation, art and visual assets, level generation, SDK integration and launch"，底座是双方联合适配的 canvas 式 AI 开发工具 Game Assets Generation Agent，开发者在画布上统一编排 AI 工作流与美术资产。
- 复用与自动化机制：前 12 款游戏每款都向管线沉淀可复用 AI 能力（"every new game starts from a stronger base than the last"）；管线产出的原型完整度高于传统早期原型；AI 模块已自动完成 SDK 集成与埋点，下一步是"automated bug detection and self-correction"。
- AI 原生玩法两个在测原型：Inner Island（玩家与 AI 伙伴通过对话共建个人岛屿，AI 从对话中提取要点塑形岛屿）与 AI 互动故事游戏（角色带预设人格/记忆/已知事实，AI 随剧情现场组装场景）；公司将其与通过 Anamana 投资的 AI 原生微短剧战略相连——"the line between a game and a serialized drama begins to blur"。
- 合作方 Witmani：Gamehaus 2026 年 6 月对其做少数股权投资；创始人兼 CEO Dr. Daley Dai 为港科大（广州）博士、曾在 UC Berkeley 做部分博士研究，在 NeurIPS/ICLR/ICCV 有发表；其创作者平台让用户"用对话描述想法"即可生成可玩游戏，无需先学编程或画画。
- 引用注意：新闻稿风险段自列多项不确定因素——AI 产游戏的 "market acceptance and monetization"、对 Witmani 的第三方工具依赖、AI 模型与基础设施的性能/可用性、AIGC 训练数据与知识产权的法律监管框架等；引用 90% 效率数据时必须保留 "internal estimates" 限定语。

## 原文全文存档

> 以下为 2026-11-27 经 mcp__web_reader__webReader 提取的原文正文存档，尽量保留原文结构与措辞；版权仍归原发布方，仅供团队内部研究借鉴，完整原文以上方 URL 为准。

Gamehaus AI Pipeline Optimizes Game Prototyping Effort by About 90%, Based on Internal Estimates; Gamehaus' First AI-Built Game Collection, Ease Games, Goes Live

_Jointly developed by Gamehaus and AI game creation team Witmani, the pipeline took the Ease Games collection from kickoff to 12 finished games in about seven weeks; the collection targets approximately 50 games within two quarters_

, /PRNewswire/ -- Gamehaus Holdings Inc. ("Gamehaus" or the "Company") (Nasdaq: GMHS) today announced that its AI-driven game production pipeline has optimized the efficiency for building a playable game prototype: from roughly three developers working one to one-and-a-half weeks under the Company's traditional process, to an average of one developer working one-and-a-half to two days. Based on Gamehaus' internal estimates, measured in developer working days (assuming a five-day work week), this represents a reduction from 15–22.5 developer-days to 1.5–2 developer-days, or approximately 87%–93% (about 90% at the midpoint), in the labor required to produce a playable prototype. Gamehaus' first product built on the pipeline, __Ease Games: Fun Anytime__, is now live on Google Play with 12 casual games. An upcoming update will bring the collection to include 20 games, and the Company targets approximately 50 games in the collection within the next two quarters, subject to development progress and market conditions.

In August 2026, Gamehaus announced that it was shifting resources toward AI-generated content, starting with casual mobile games. Over the past quarter, that direction has moved from strategy into product validation. The Company is pursuing AI games on two levels: first, production efficiency, building a repeatable process that makes a new game far faster and cheaper to produce; and second, AI as gameplay, creating AI-enabled interactive experiences that were not possible in traditional game formats.

__From Kickoff to a Live Product in About Two Months__

Gamehaus and its strategic partner Witmani began the Ease Games project in late August 2026. Tools and workflows were ready by mid-September. By mid-October, the app framework and the first 12 games were complete, and after quality assurance the app went live and completed its first round of validation at the end of October.

Ease Games brings puzzle, relaxation and arcade-style casual games, including Sudoku, Arrows Out and Water Sort, into a single app. It plays fully offline and saves progress automatically. Beyond its preset levels, each game includes a built-in level generator with three difficulty tiers that creates new levels on demand, so players do not run out of content.

__How AI Is Used in Production__

The pipeline covers game implementation, art and visual assets, level generation, SDK integration and launch. It is built on Game Assets Generation Agent, a canvas-based AI development tool that the two teams jointly adapted for Ease Games. Developers build and manage AI workflows and handle art assets in one place on the canvas.

- __Reusable capabilities.__ Each of the first 12 games added reusable AI capabilities to the pipeline, so every new game starts from a stronger base than the last.
- __Higher completeness.__ Prototypes built through the pipeline reach a higher level of completeness than early prototypes under the traditional process.
- __Automated integration.__ An AI module now handles SDK integration and analytics event tracking automatically. The next step is automated bug detection and self-correction.

For Gamehaus, Ease Games is the testing ground for the pipeline as much as a product. Every new game added is a live measurement of production speed and quality, and the results feed back into the pipeline.

__About the Partnership with Witmani__

Witmani is an AI game creation team in which Gamehaus made a minority equity investment in June 2026. The two companies are jointly developing the AI production pipeline and have formed an in-depth strategic partnership in global publishing.

Witmani was founded by Dr. Daley Dai, its Founder and Chief Executive Officer, who holds a Ph.D. from The Hong Kong University of Science and Technology (Guangzhou), conducted part of his doctoral research at UC Berkeley, and has published at leading AI conferences including NeurIPS, ICLR and ICCV. Witmani's creator platform lets users build a playable game by describing their idea in a conversation, without first learning to code or draw.

__Exploring AI-Native Gameplay__

Rather than adding an AI chat feature to existing game types, Gamehaus is focused on where AI changes the experience itself, and on new kinds of games that AI makes possible. Two early prototypes are in testing:

- __Inner Island.__ Players build a personal island together with an AI companion through conversation instead of fixed building tasks. The AI picks up what matters in each conversation and shapes the island accordingly, so each player's island grows into their own.
- __AI interactive story game.__ Using the Company's in-house scripts and art, players act freely within the rules of a story. Characters draw on preset personalities, memory and known facts to respond meaningfully, and the story changes based on what players say and do, with AI assembling the scenes as the story unfolds.

This work connects directly to the Company's investment in AI-native micro-serials through Anamana. When players can shape a story, the line between a game and a serialized drama begins to blur.

"In August, we began repositioning Gamehaus as an AI-enabled content generation and distribution platform," said Yimin Cai, Chief Executive Officer of Gamehaus. "One quarter later, that strategy is taking shape on two fronts at once. In AI micro-serials, we have built our presence through Anamana. In AI games, Ease Games is live, built on an AI production pipeline we developed with Witmani, and our first AI-native gameplay prototypes are in testing. Looking ahead, we expect to apply these capabilities to new forms of AI-enabled interactive entertainment beyond what traditional game formats offer."

__About Gamehaus__

Gamehaus Holdings Inc. (Nasdaq: GMHS) is a technology-driven global mobile entertainment and game publisher dedicated to bridging creative studios and audiences worldwide. With a vision to be the go-to partner for creative teams, the company specializes in combining global reach with AI- and data-powered solutions to help partners build lasting success. For more information, please visit https://ir.gamehaus.com.

__Forward-Looking Statements__

This press release contains forward-looking statements within the meaning of Section 27A of the Securities Act of 1933, as amended, and Section 21E of the Securities Exchange Act of 1934, as amended. These statements include, but are not limited to, statements regarding the expansion of Ease Games, including the number and timing of new games; the development of the Company's AI production pipeline; the development of AI-native gameplay prototypes; the Company's collaboration with Witmani; and the business strategies of Gamehaus. Investors can identify these statements by words such as "approximates," "believes," "expects," "anticipates," "estimates," "projects," "intends," "plans," "targets," "will," "would," "should," "could," "may," or similar expressions.

These forward-looking statements are based on current expectations, forecasts, and assumptions that involve known and unknown risks and uncertainties that could cause actual results to differ materially from those projected. Key factors that could cause or contribute to such differences include, among others: market acceptance and monetization of AI-produced games; the Company's ability to sustain the efficiency gains described in this release as the number and complexity of games grow; the Company's reliance on third parties, including Witmani, for AI tools and technology; the performance and availability of AI models and infrastructure used in the Company's AI production pipeline; the Company's ability to maintain or further improve the development efficiencies as described in this press release; technological changes and reliance on underlying AI architectures; competition in the casual mobile game market; app store policies; and the legal and regulatory framework governing AI-generated content, training data, and intellectual property.

These statements speak only as of the date they are made, and Gamehaus undertakes no obligation to update or revise any forward-looking statements to reflect subsequent events or circumstances, except as required by law. For a more detailed discussion of these and other risk factors, please refer to Gamehaus's filings with the U.S. Securities and Exchange Commission, including its annual report on Form 20-F and current reports on Form 6-K.

__Investor Relations Contact__

The Blueshirt Group
Jack Wang
Gamehaus@TheBlueshirtGroup.co

Gamehaus Holdings Inc.
Investor Relations Team
ir@gamehaus.com

SOURCE Gamehaus Holdings Inc.

## 存档说明

本文为团队研究存档：上方「原文全文存档」为抓取时点的正文快照（mcp__web_reader__webReader 提取，非逐字节 HTML），「借鉴要点」为本团队提炼；版权归原发布方，仅供团队内部研究借鉴。
