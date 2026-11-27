# 源文归档｜EndWeaver：用 LLM 对多结局游戏任务做自动化冒烟测试（arXiv 2611.32089）

- **原始 URL**：https://arxiv.org/abs/2611.32089
- **抓取日期**：2026-11-27（论文 v1 提交 2026-11-24；已录用 IEEE Transactions on Games）
- **类型**：学术论文摘要页（cs.SE）
- **作者**：Jinyu Cai, Mingyue Zhang, Nianyu Li, Jinglue Xu, Tianshui Li, Jialong Li, Hitoshi Iba, Kenji Tei（摘要页未列机构）
- **关联条目**：daily/2026-11-27.md 条目 2；详尽版 daily/details/2026-11-27-research-content-pipeline.md
- **存档目的**：原文全文存档，防源页失效（link rot）

## 摘录

（以下为 WebFetch 对摘要页的结构化提取要点，非原文全文；完整论文见上方 URL。）

**问题定义**
- 现代任务（quest）带分支叙事与多结局，现有自动化冒烟测试普遍存在三类缺陷：结局覆盖不足、动作序列冗余、交互成本高到不可用。

**方法**
- LLM 解读任务描述与游戏环境，生成两层规划：「高层方法」引导全局探索 + 「原语任务序列」做细粒度规划；
- 与动态构建的状态转移图结合——保证覆盖全部可能结局，并让测试高效收敛。

**评测**
- 四个游戏环境：Mini RPG、Overcooked Plus、Minecraft、PySC2；对比多条基线。
- 结果：所有环境里稳定完成任务、高可靠性，显著优于基线；
- 成本：数千步（"a few thousand steps"）即全覆盖全部结局，基线方法需数百万步；
- 消融实验确认各组件均有实质贡献。

## 原文全文存档

> 以下为 2026-11-27 经 web_reader 提取的原文正文存档，尽量保留原文结构与措辞；版权仍归原发布方，仅供团队内部研究借鉴，完整原文以上方 URL 为准。

View PDF
HTML (experimental)

> Abstract:Modern game quests are increasingly trending toward high freedom and multiple endings, making their design and testing more complex. Smoke testing in games aims to rapidly validate quest functionality, but existing automated testing approaches face critical limitations when handling quests with branching narratives, and multiple possible endings. These challenges result in insufficient exploration of endings, redundant action sequences, and prohibitively high interaction costs. To address these challenges, we propose EndWeaver, an automated smoke testing framework specifically designed for multi-ending game tasks. EndWeaver leverages LLMs to interpret quest descriptions and game environments, generating high-level methods to guide global exploration, complemented by the generated primitive task sequences for fine-grained planning. By combining this multi-level planning structure with the dynamic construction of state-transition graphs, EndWeaver ensures comprehensive coverage of all possible endings and enables efficient testing. We evaluated EndWeaver on four game environments---Mini RPG, Overcooked Plus, Minecraft, and PySC2 against baseline methods. In all environments, EndWeaver achieved stable quest completion with high reliability, significantly outperforming the baselines. In terms of testing cost, EndWeaver required only a few thousand steps, while baseline methods required millions of steps, all while ensuring comprehensive coverage of all possible quest endings. Ablation studies further demonstrated the critical contributions of each framework component, validating the effectiveness and robustness of our approach.

## Submission history

From: Jinyu Cai [view email]   
 __[v1]__
Tue, 24 Nov 2026 07:12:39 UTC (2,018 KB)

## 存档说明
本文为团队研究存档：上方「原文全文存档」为抓取时点的正文快照（工具提取，非逐字节 HTML），「借鉴要点」为本团队提炼；版权归原发布方，仅供团队内部研究借鉴。
