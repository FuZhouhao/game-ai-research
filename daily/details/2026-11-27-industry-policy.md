# 2026-11-27 详尽情报｜业界实践与政策动态（条目 27~37）
> 速览索引：../2026-11-27.md；本文是侦察完整报告的归档展开；源文原文归档见 sources/ 下 2026-11-27-*.md。
> 纪律：每条附原始 URL + 抓取日期（2026-11-27）；只录 transcript 里实际抓到的内容，缺失处明确写「未及抓取」，禁止编造补齐。

## 条目 27｜CUT! 玻璃盒复盘：单人 4 天用 Claude Code 多智能体写完一整款游戏

- **类型**：开发者复盘 devlog（原文已抓取，源文归档 sources/2026-11-27-cut-postmortem.md）
- **来源 URL**：https://itch.io/devlog/1782027/cut-glass-box-dev-log-a-game-made-in-four-days-with-claude-code-agents.amp
- **抓取日期**：2026-11-27

**事件与时间线**：独立开发者 Sébastien（itch.io 用户 sebastienvss-creator）2026-11-16 发布 Epic AI MegaJam 2026（主题 "Director's Cut"）参赛复盘：玩家用左键指挥卡牌挡住怪物扑击、保护摄像机，用时数买卡把灰盒升级成品。首次提交 11-12（周四），4 天完成 UE 5.9 游戏。架构：1 个 Claude Code 主智能体（MCP 驱动虚幻编辑器/打包/资产/日志）+ 最多 9 个并行子智能体（单轮 25~45 分钟，各自独占 editor/git/write 区），共 4 次过夜自主跑；末次提交 01:36 后主智能体不再回答提示词，空转至 08:31。

**数据与证据**：56 个自动化测试 + 机器人试玩 + 截图断言；52 张带 provenance 时间戳卡牌、43 张进入玩法循环；机器人胜率 67~100% vs 人类 1/7；计划每波 3~6 只怪、平均实装 1.6；Windows 包 1.6GB zip；概念图 fal.ai、3D 走 Hyper3D Rodin（以 Blender 渲染图为输入），API 花费设上限。

**各方反应与争议点**：作者自曝翻车清单——主角贴地爬行而 56 测全绿（表现层断言缺失），由此立规 "What I have not seen working on a capture ships switched off"（凡没在截图里见过能工作的功能，一律关闭出货）；瓶颈从写代码移到「合并与审查」；最后一晚跳过检查、soir20 boss 从未 launch；lake-as-grass、打包后灰块、快速改动误删 4 张卡、对 itch.io 文件结构假设错误。感知局限：只看日志+静态截图、音效按名字选、镲片声靠频谱定位、爆炸闪光靠亮度对齐。

**与本团队关联**：单人+多智能体 4 天出货证明小团队可借智能体解带宽约束，但人审成为新瓶颈——与「人是第一责任人」一致；机器人试玩+截图断言可平移到 Godot headless CI；provenance 登记做法可直接抄进资产入库流程。

**对规约/工作流的影响**：已落地——design/dev-standards-draft.md §3「AI 产物登记生成时间与提示词版本」与 §5「单测全绿≠正确、表现层断言、人审带宽预留」（变更日志引条目 27）。新增建议：workflow-recommendations.md §3.3 AI playtest 管线补「机器人试玩 vs 人类玩家对照」指标；§4 增「智能体过夜自主跑须设停止条件与晨检清单」。

## 条目 28｜GDC 第 15 届行业状态调查：40% 开发者用生成式 AI，52% 认为有害

- **类型**：年度行业调查（官网文章 + gamesindustry.biz 报道）
- **来源 URL**：https://gdconf.com/article/gdc-2026-state-of-the-game-industry-reveals-impact-of-layoffs-generative-ai-and-more ；报道 https://www.gamesindustry.biz/gdc-state-of-the-game-industry-report-40-of-developers-are-using-generative-ai-for-work
- **抓取日期**：2026-11-27（两处网页均提取成功；调查原始问卷全文未及抓取）

**事件与时间线**：2026-11-12/13 发布第 15 届 State of the Game Industry：使用生成式 AI 的开发者从 36% 升到 40%（+4pt），其中 57% 每天使用；认为 genAI「有害」的比例两年内从 18% 飙到 52%（部分口径 55%）；过去 24 个月 33% 受访者经历裁员；UE/Unity 市场份额下滑；对下一代平台感兴趣度：PlayStation 10%、Project Helix 8%。

**数据与证据**：40% 使用率 / 57% 日用 / 52%~55% 有害 / 18%（两年前）/ 33% 裁员经历 / 10% 与 8%（主机兴趣）；本届样本量未及抓取。

**各方反应与争议点**：核心张力是「使用率与负面情绪同步上升」，媒体多以「AI 疲劳」框架解读；厂商效能宣传（90%、300% 等，见条目 32/33）与从业者有害感受形成对冲，单边引用任何一方都会失真。

**与本团队关联**：行业情绪基线——引用「AI 提效 X%」必须标注厂商自报口径；52% 有害感受提醒对外披露与对内评审都要留人工环节。

**对规约/工作流的影响**：已落地——design/dev-standards-draft.md §0.1「人是第一责任人」与 §6 披露条目在精神上对齐。新增建议：§7 陷阱表增「厂商口径打折条」（引用厂商效能数字须注来源与口径）；研究周报引用本调查作情绪基线，与条目 32/33 对照使用。

## 条目 29｜《以撒的结合：忏悔+》未披露 AI 音乐被玩家挖出后撤除

- **类型**：新闻报道（Rock Paper Shotgun；HN 讨论）
- **来源 URL**：https://www.rockpapershotgun.com/undisclosed-ai-generated-music-pulled-from-the-binding-of-isaac-repentance-update-as-attempt-to-get-satirical-on-gta-6-launch-day-goes-awry ；HN https://news.ycombinator.com/item?id=50610369
- **抓取日期**：2026-11-27（RPS 全文经 web_reader 抓取并归档：[sources/2026-11-27-isaac-ai-music-rps.md](../../../sources/2026-11-27-isaac-ai-music-rps.md)；IGN 同题报道抓取被拦，未及抓取）

**事件与时间线**：《以撒的结合：忏悔+》（The Binding of Isaac: Repentance+）11-19 推送免费更新，刻意选在 GTA 6 发售日上线（借恶搞 GTA 日常关卡做话题）；11-21 Reddit 用户 ShweetsStuff 从音乐文件元数据挖出 Suno 生成痕迹，而 Steam 商店页无任何 AI 披露，发行商 Nicalis 随即撤除音乐文件；11-23 RPS 报道。该更新属 70 美元本体内容的一部分。

**数据与证据**：Suno 元数据为玩家法证式发现；PC 补丁移除 AI 音乐并顺手修复 Larynx bug，主机版更新待跟进；差评轰炸持续数日；HN 讨论帖 50610369。

**各方反应与争议点**：McMillen 回应 "Woke up to a shit show…"（早上醒来一团糟），自称完全不知情、正在查 AI 音乐如何混进更新；Nicalis 保持沉默；争议点是「连开发者自己都不知道哪来的 AI」——管线失控而非单纯隐瞒。

**与本团队关联**：玩家已会做法证级排查（文件元数据），资产入库 MinIO 必须同步留存来源与工具元数据；外包/协作素材合同要写明是否含生成内容；未披露的代价（差评轰炸）远高于披露成本。

**对规约/工作流的影响**：已落地——design/dev-standards-draft.md §3 资产审计脚本「AI 来源字段」检查（变更日志引条目 29）。新增建议：§3 溯源字段明确覆盖音频（生成工具名与版本入 MinIO 元数据）；§6 发行检查清单加「商店页披露与实际包内容一致性核对」。

## 条目 30｜Steam 新作 AI 披露率首破五成：10 月达 49.9%~54.3%

- **类型**：社区数据分析帖（Reddit r/Steam）+ 高管言论（Reddit r/Games）
- **来源 URL**：https://www.reddit.com/r/Steam/comments/1xlexwi/ ；Sweeney https://www.reddit.com/r/Games/comments/1xg1btm/
- **抓取日期**：2026-11-27（Reddit 原帖多路抓取被拦，数字来自 WebSearch 聚合与转述，未及抓取原帖全文；Sweeney 帖约 10 月底-11 月初，日期未确认）

**事件与时间线**：约 63,600 款 Steam 游戏的统计分析：10 月新作 AI 披露率 49.9%（另一口径 54.3%、对应 1,240 款）；轨迹为 2024-01 的 1.7% → 2024 全年 13.2% → 2026 初 ~26.4% → 10 月近半，帖主称抵达「tipping point」（临界点）。同期 Tim Sweeney 批评 Steam 的 AI 标签。

**数据与证据**：评论 <10 的小游戏披露率 47%，1000+ 评论的大作仅 14%；连续发行 10+ 款的开发商更倾向披露。Sweeney 原话：标签 "abhorrent"（可憎）、"scarlet letter"（像烫字红字）、"really irresponsible"（极不负责任），并称没有任何公开销售数据证明标签影响销量——shattered.io 分析指出双方均属推测，因为 Steam 不公布销售数据。争议自 2025 年底起，2026 年 6/7/10/11 月多次发酵；Valve 披露政策 2024 年初上线。

**各方反应与争议点**：Sweeney 的「烫字论」vs 社区「披露无害论」（小游戏披露率反而更高）；标签是否影响销量双方都拿不出公开数据。

**与本团队关联**：披露已成小团队常态操作而非污点——主动披露不会单独杀死一款游戏；从第一版就按预生成内容如实勾选，与 CI 快照构建一起走人工确认。

**对规约/工作流的影响**：已落地——design/dev-standards-draft.md §6 更新已引用 49.9%~54.3% 与 47%/14% 数据（变更日志引条目 30）。新增建议：季度性跟踪披露率；在 §6 记录「标签影响销量无公开数据」的争议事实，既不过度恐慌也不过度自信。

## 条目 31｜育碧同日宣布裁员 166 人并成立生成式 AI 子公司 Motherbrain

- **类型**：新闻报道（Engadget、IGN）
- **来源 URL**：https://www.engadget.com/2322205/ubisoft-lays-off-166-more-workers-opens-a-generative-ai-studio（全文已归档：[sources/2026-11-27-ubisoft-genai-studio-engadget.md](../../../sources/2026-11-27-ubisoft-genai-studio-engadget.md)）；另见 https://www.ign.com/articles/ubisoft-creates-generative-ai-game-studio-called-motherbrain（IGN 抓取被拦，未及抓取）
- **抓取日期**：2026-11-27

**事件与时间线**：2026-11-19 育碧在蒙特利尔与魁北克城裁员 166 人，同日公布 genAI 子公司 Motherbrain（生成式 AI 用于 gameplay）；子公司名被玩家嘲「Metros 反派」/Metroid villain。年内早前已有约 40 人裁撤；有报道把 Motherbrain 定为 10 月成立（本条以 11-19 报道日为准）；其 AI 驱动团队协作游戏 Teammates 于 2025-11-21 公布；另有腾讯×育碧×NVIDIA NPC 工具合作背景。

**数据与证据**：166 人（Montréal+Québec City 同日）；~40 人（年内早前）；开发者被要求提交提示词与 AI 工作流；公司表态将加大 genAI 投入。

**各方反应与争议点**：「AI 提效」与「裁员」同框成为标志性争议样本；提示词入库要求引发从业者对监控与作品产权的讨论（transcript 仅见报道转述，评论原文未及抓取）。

**与本团队关联**：大厂把提示词与 AI 工作流当正式资产入库管理，验证本团队「提示词进 Git 版本管理、不散落会话」的思路；同时提示提效叙事与岗位收缩的现实关联，团队引入管线时要同步说清人往哪走。

**对规约/工作流的影响**：新增建议——design/dev-standards-draft.md §2 工程阶段增「提示词与 AI 工作流入 Git 版本管理」条目；§7 陷阱表增「提效数据与裁员同框」的解读纪律；研究周报持续跟踪 Motherbrain 实际产出。

## 条目 32｜Gamehaus：AI 管线把可玩原型人力省约 90%，首个 AI 消除游戏合集上线

- **类型**：上市公司新闻稿（Nasdaq 上市游戏公司）
- **来源 URL**：https://ir.gamehaus.com/2026-11-16-Gamehaus-AI-Pipeline-Optimizes-Game-Prototyping-Effort-by-About-90-,-Based-on-Internal-Estimates-Gamehaus-First-AI-Built-Game-Collection,-Ease-Games,-Goes-Live
- **抓取日期**：2026-11-27（新闻稿页提取成功）

**事件与时间线**：2026-11-16 Gamehaus 宣布 AI 管线使可玩原型制作人力约省 90%（内部估算口径；部分媒体转述 87%~90%）；首批 12 款休闲游戏合集「Ease Games」上线；称每款游戏都给管线沉淀了一件可复用能力；目标在此基础上再降 50% 人力；延续其 2026-08 的 AIGC 战略转向（PR Newswire 稿）。

**数据与证据**：~90%（内部估算）、12 款游戏上线、再降 50% 目标；转载渠道含 Nasdaq、moomoo、VIR、Threads、r/Quantisnow 等，均原样转通稿。

**各方反应与争议点**：全部数字为厂商自报、无第三方验证；「每个实验回馈管线一件可复用资产」的度量方式是新闻稿里少有的可迁移干货。

**与本团队关联**：该度量与本团队 exp→main 沉淀模型同构，可作 exp 工单验收标准参考；90% 数字引用时必须标注「内部估算、厂商自报」。

**对规约/工作流的影响**：新增建议——design/dev-standards-draft.md §1 立项/experiment 工单模板加「本实验回馈管线的可复用资产」验收字段；§7 陷阱表「厂商口径打折条」（与条目 28 合并落地）；周报引用其数字一律带口径标注。

## 条目 33｜中国大厂 Q3：网易称 AI 原生管线部分环节效能提升 300%，腾讯利润因 AI 投入下滑

- **类型**：财报报道 + 传闻证伪记录
- **来源 URL**：网易 https://app.xinhuanet.com/news/article.html?articleId=80a52e4243c36b855ac5db22df2f4d3f ；腾讯 https://www.lanjinger.com/d/1795184167467871003 ；证伪 https://www.gamereactor.eu/no-netease-hasnt-put-a-total-ban-on-generative-ai-in-its-games-1670333
- **抓取日期**：2026-11-27（三处均提取成功；检索中另遇 cls.cn 腾讯云混元 3D 页面，实为 2025-09-18 旧文，判为过期不入档）
- **源文口径核对（2026-11-27 全文归档时发现）**：上方新华网链接经全文归档（[sources/2026-11-27-netease-xinhuanet.md](../../../sources/2026-11-27-netease-xinhuanet.md)）核对，实为网易 **2025 年报**（2026-02-11）电话会解读，而非 2026Q3 电话会原文——「最懂游戏的 AI 专家」口号、「300% 效能提升」「2025 年大规模部署」在该文（2 月口径）即已出现；本条归到 Q3 电话会（2026-11-19）的原话表述无归档可对证，引用 300% 时以「厂商 2026-02 年报口径」为准。《燕云十六声》8000 万用户（2 月）vs 1 亿（11 月蓝鲸篇）、《无限大》全平台计划（2 月）vs 定档 2027-01-15（11 月）两套口径对照详见归档头部。

**事件与时间线**：2026-11-19 两家 Q3 财报电话会——网易提出做「最懂游戏的 AI 专家」，AI 原生管线已覆盖美术/策划/编程/动画/QA，部分环节效能提升 300%（厂商口径），称 2025 年已大规模部署；腾讯 Q3 Non-IFRS 经营利润同比 -6%，管理层归因 AI 基础设施投入，次日港股一度跌近 6%。

**数据与证据（含证伪记录）**：300%（厂商自报，无第三方验证）；腾讯 -6%（Non-IFRS）。2026 年 2 月初「网易全面禁 AIGC」传闻再次流传（r/artificial 1qvnt0h、wnhub item-50032，称 "not use it at all"，起因玩家反弹+版权顾虑）；2026-02-05 Gamereactor 求证，网易发言人答复 "This story isn't true – we even have a GDC talk about AI"（即对 FRVR 所言）——明确否认。另：Nagoshi Studio 2026-03 停止出资、2026-10-31 关闭是独立事件；「AI 替代美术师」争议亦为另一脉络。

**各方反应与争议点**：效能声明与利润下滑同框——大厂 AI 投入的短期成本与长期叙事并存；旧闻「禁 AI」回流风险高，需靠日期核对拦截。

**与本团队关联**：引用大厂效能数字时与 GDC 52% 有害感受（条目 28）对照，避免单边采信；证伪链接留档备查，防止旧闻再进周报。

**对规约/工作流的影响**：新增建议——design/dev-standards-draft.md §7 陷阱表增「旧闻回流：引用前核对原始日期」；研究周报引用大厂数字一律带口径与日期；本条证伪记录作周报引用检查的样例。

## 条目 34｜Big Walk 引发 IGF 是否接受生成式 AI 作品的新一轮争论

- **类型**：社论 + 社区讨论（HN）
- **来源 URL**：https://www.rogue.site/editorials/big-walk-ai-disclosure-igf-controversy ；HN https://news.ycombinator.com/item?id=50452407
- **抓取日期**：2026-11-27（社论 2026-11-12；HN 帖 "In defense of giving a shit" 2026-11-11）

**事件与时间线**：独立游戏 Big Walk 的 AI 披露引发 IGF 奖资格之争：评奖旨在 "reward human achievement or recognize the best indie games"（奖励人的成就 / 认可最佳独立游戏）——生成式 AI 作品是否合资格成为焦点；这是玩家态度从「骂 AI 游戏」转向「争 AI 游戏该不该进艺术奖项」的信号。

**数据与证据**：Big Walk 在 Steam 遭负评潮；反例 One More Lawn 因透明披露 AI 歌曲获部分社区称赞；诚实披露者同样会被轰炸（轰炸与披露诚实度并非强相关）；HN 长讨论 + pokeindie.com 关于 Steam Next Fest（2026-10）审核问题的报道佐证平台侧治理压力。

**各方反应与争议点**：两派对立——「AI 作品不该进艺术奖」vs「评最好的游戏就行」；轰炸多来自 vocal minority，多数玩家并不参与（HN 讨论观点，原文细节未及逐条核对）。

**与本团队关联**：披露措辞的两极样本——诚实披露+人工深度把关可获得同情，遮掩者（对照条目 29）遭双重惩罚；团队商店文案可参考两极案例措辞。

**对规约/工作流的影响**：已落地——design/dev-standards-draft.md §6 更新已把条目 34 列入披露措辞参考（变更日志）。新增建议：季度性跟踪玩家态度风向（scout 建议）；exp 试玩记录加「披露后玩家反应」观察项，为发行措辞积累自证数据。

## 条目 35｜Valve 回应开发者对「AI 垃圾与换皮」泛滥的担忧；itch.io 清删升级

- **类型**：平台方表态（Reddit r/Games）+ 媒体报道（GameLuster，源文归档 sources/2026-11-27-itch-io-ai-slop-purge-gameluster.md）
- **来源 URL**：https://www.reddit.com/r/Games/comments/1xhhufp/valve_responds_to_developers_fearing_ai_slop_and（全文已归档：[sources/2026-11-27-reddit-games-valve.md](../../../sources/2026-11-27-reddit-games-valve.md)）；https://gameluster.com/itch-io-deletes-terabytes-of-ai-slop-as-daily-uploads-double（全文已归档：[sources/2026-11-27-itch-io-ai-slop-purge-gameluster.md](../../../sources/2026-11-27-itch-io-ai-slop-purge-gameluster.md)）
- **抓取日期**：2026-11-27（r/Games 原帖经 web_reader 抓取成功并全文归档，原帖发布 2026-10-28T07:48:56Z（页面元数据），快照含标题、OP 与按 Best 排序的热门评论摘录，详见 sources/2026-11-27-reddit-games-valve.md；GameLuster 全文归档见上）

**事件与时间线**：Valve 公开回应开发商对 Steam 上 AI 生成内容与换皮克隆泛滥的担忧——平台方在披露率近五成（条目 30）背景下的最新治理表态。同期 itch.io 在 11-03 过滤器公告后继续扩量清删：GameLuster（2026-11-03，Cody Harwell）披露日上传页从 8-03 约 3000 页涨到 10-30 的 6000+ 页（上传翻倍而下载/购买未翻倍），管理员称 "Just deleted a couple terabytes of ai slop"（刚删掉几个 TB 的 AI 垃圾），被追问依据时回 "Take a guess"（你猜）；披露要求扩展到桌游/书籍/漫画/原声，且即使 AI 内容最终被人工编辑掉，上传时也必须披露；"No AI" 筛选将从标签页扩展进站内搜索。Kotaku 于 11-02~09 间跟进报道。

**数据与证据**：itch.io 政策背景——AI 资产披露要求与质量准则 slop 条款均已存在 2 年以上，本次是执行加码非新规；有高频上传者被警告将失去上传权限。随 Valve 讨论流传的统计：80 款披露游戏中约 60 款零玩家（transcript 见转述，原始出处未及核对；已核对 2026-11-27 归档的原帖快照与热门评论摘录，该统计不在其中，出处仍在原帖更深层回复或外部转述中）。

**各方反应与争议点**：开发者要求平台清理 vs Sweeney 式「标签污名化」论（条目 30）形成平台间路线分歧；「披露即使被编辑掉也要做」的严格化引发合规成本讨论。

**与本团队关联**：平台治理方向是「披露透明化 + 主动过滤」；小团队提前做资产命名与披露合规，避免被批量清理类动作误伤；「诚实披露」在 itch 上已是硬性义务而非可选项。

**对规约/工作流的影响**：新增建议——design/dev-standards-draft.md §6 发行检查清单加「平台政策跟踪（Steam/itch）与披露-内容一致性核对」；§3 资产命名规范与披露字段对齐，便于政策变化时批量自检；研究周报把 itch 政策执行力度列为季度观察项。

## 条目 36｜用 AI 管线 160 小时发完一款 Godot 4.6 手游（r/aigamedev）

- **类型**：社区自述帖（Reddit r/aigamedev）
- **来源 URL**：https://www.reddit.com/r/aigamedev/comments/1w7w0oj/
- **抓取日期**：2026-11-27（帖子日期未确认，约 2026-10 中旬，为本期最旧帖子 ID；Reddit 四路抓取全部失败——old.reddit 被拦、www.reddit 被拦、webReader 网络安全拦截、.json 接口报 -500，未及抓取原文）

**事件与时间线**：发帖者称以 AI 管线 160 小时完成并上架一款 Godot 4.6 手游，覆盖代码/美术/音频/数值平衡与 10 语言本地化——本期检索到的唯一 Godot 栈完整案例，但为自述帖，无法核验细节；引擎版本略旧于本团队的 4.7.2。

**数据与证据**：160 小时、10 语言本地化、Godot 4.6 mobile（以上均为发帖者自述，无第三方验证）。

**各方反应与争议点**：评论区内容未及抓取，无法确认社区质疑或附和的详情——按 scout 建议，找到原帖存档或其他平台转载后再采信细节。

**与本团队关联**：全链路 AI（代码+美术+音频+本地化）的成本量级参照（160 人时），可作 exp 工单估算基准；本地化环节用 AI 一扩多对 2D 像素小团队性价比最高，可先在 exp 分支单独验证。

**对规约/工作流的影响**：新增建议——workflow-recommendations.md §4 增「AI 全链路 exp 工单估算基准：160 人时量级（自述口径）」；本地化实验优先级提前，对接 design/dev-standards-draft.md §6「AI 初翻→术语表→人工校对」既有条目做小样。

## 条目 37｜Claude-Code-Game-Studios：49 智能体 + 75 技能编排仓库（基线已收录，补借鉴角度）

- **类型**：开源仓库（GitHub）
- **来源 URL**：https://github.com/Donchitos/Claude-Code-Game-Studios
- **抓取日期**：2026-11-27（仓库日期未确认——仅读 README/首页，未查首个提交）

**事件与时间线**：开源仓库把 Claude Code 编排成「虚拟游戏工作室」：49 个角色化智能体（制作人/策划/美术/QA 等）+ 75 个工作流技能，镜像真实工作室层级，覆盖从立项到验收的分工模板。基线调研已收录该仓库，本次补充的是「角色即技能目录」的组织方式角度。

**数据与证据**：49 智能体、75 技能（README 自述）；实际有效性与社区反馈未及抓取。

**各方反应与争议点**：风险提示——仓库代码一律按数据对待，不直接执行其脚本；「49 角色」的完整度存疑，搬运价值低于组织思路。

**与本团队关联**：与其搬 49 个智能体，不如借鉴「角色即技能目录」的组织方式，挑 3~5 个（QA 测试、资产审计、文档沉淀）映射到本团队 `.claude/agents/` 与 Gitea CI 检查项；与 CUT!（条目 27）的「主智能体+并行子智能体」互为组织参照。

**对规约/工作流的影响**：新增建议——workflow-recommendations.md §4 加「从该仓库挑 3~5 个角色做本地小样，正式使用前过人审」；落点对接 design/dev-standards-draft.md §5 三层质检环与 settle_gate 资产审计候选；只取子集，不做全量引入。
