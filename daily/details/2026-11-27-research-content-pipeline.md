# 2026-11-27 详尽情报｜学术研究 × 内容管线（条目 1~13）
> 速览索引：../2026-11-27.md；本文是侦察完整报告的归档展开。
> 纪律：每条附原始 URL + 抓取日期（2026-11-27）；只录 transcript 里实际抓到的内容，缺失处明确写「未及抓取」，禁止编造补齐。

## 条目 1｜PixelBench：像素画创建的 LLM 基准与工具型智能体环境
- **类型/来源/抓取**：学术论文（arXiv cs.CV）｜ https://arxiv.org/abs/2611.20628 ｜ 2026-11-27（v1 发布 2026-11-16）
- **是什么**：把「文本生成像素画 + 指令引导编辑」形式化为基准，并提供让语言模型智能体写代码调用绘图工具来创作/修改像素画的环境。作者：Mutian Hong, Jianxuan Yao, Mingkun Yue, Changkai Li, Hower Yang, Haibin Ling。
- **机制与数据**：非扩散路线——智能体在创作环境里写代码、调绘图工具逐笔作画；领域难点定义为「紧凑分辨率与调色板约束下的可读形体、空间连贯、配色和谐」。评测双轨：人类评审 + 多模态 LLM 评委，且评委与人类偏好的一致性经过验证；对比多款模型/多配置、多主体与多画布尺寸。关键结论：**"GPT-6 Astra earned both the top average judge score and the best average human ranking"**（GPT-6 Astra 评委均分与人类排名双双第一），作者据此认为 "general-purpose language models hold real promise for pixel-art creation"（通用语言模型在像素画创作上确有真实潜力）。任务集、全部生成作品、人类排序、评委协议全公开；CC BY 4.0；摘要页未见代码仓库链接（未及抓取到发布仓库）。
- **与本团队关联**：Godot 4.7.2 / CPU-only 视角——「写代码调绘图原语」无扩散推理，CPU 可行；评委协议可移植进 CI 做出图质量门禁；与本队 Aseprite CLI 脚本化能力契合。
- **借鉴点与建议动作**：等任务集/代码放出后做小样复现；先抄「多模态评委 + 人类一致性校验」协议进资产审计回归基准。

## 条目 2｜EndWeaver：基于 LLM 的多结局任务冒烟测试
- **类型/来源/抓取**：学术论文（arXiv cs.SE，已录用 IEEE Transactions on Games）｜ https://arxiv.org/abs/2611.32089 ｜ 2026-11-27（v1 发布 2026-11-24）
- **是什么**：针对分支叙事多结局任务的自动化冒烟测试框架。作者：Jinyu Cai, Mingyue Zhang, Nianyu Li, Jinglue Xu, Tianshui Li, Jialong Li, Hitoshi Iba, Kenji Tei（抓取页未列机构）。
- **机制与数据**：痛点=现有方法「结局覆盖不足、动作序列冗余、交互成本高」。方法：LLM 解读任务描述与游戏环境，生成 **"high-level methods to guide global exploration"**（高层方法引导全局探索）+ **"primitive task sequences for fine-grained planning"**（原子任务序列做细粒度规划）的两级规划，再动态构建状态转移图——原文：**"ensures comprehensive coverage of all possible endings and enables efficient testing"**（保证全部可能结局覆盖并支持高效测试）。评测：Mini RPG、Overcooked Plus、Minecraft、PySC2 四环境全部稳定通关、高可靠，显著超基线；成本只需 **"a few thousand steps"**（数千步）对基线百万级；消融证明每个组件均有贡献。
- **与本团队关联**：exp Demo 包缺「分支/结局覆盖」验收手段；该框架是现成方法论模板；步数成本可直接当 CI 验收阈值；CPU-only 无关（LLM 在云端）。
- **借鉴点与建议动作**：状态转移图增量构建可先在本队 Dialogue/任务树小样上试；「步数成本」写进 exp_pipeline.yml 验收清单。

## 条目 3｜3D GameDev Arena：编码智能体从零建 3D 游戏的对战基准
- **类型/来源/抓取**：学术论文（arXiv 基准）｜ https://arxiv.org/abs/2611.24073 ｜ 2026-11-27（v1 发布 2026-11-18）
- **是什么**：目前最大规模「AI 造游戏」横评基准，对象是编码智能体从零构建的 3D 浏览器游戏。
- **机制与数据**：transcript 仅抓到 feed 一句话摘要：**"Benchmark of 108 from-scratch 3D browser-game builds by coding agents with automated playtesting and blind human preference rankings"**（108 个编码智能体从零构建的 3D 浏览器游戏，配自动化实机测试与人类盲评偏好排名）。评审机制=「自动化 playtesting 打分 + 人类盲评偏好」双轨并合成排名。论文摘要全文、作者、上榜模型名单、游戏样例**未及抓取**（本轮只命中 feed 条目，未单独 fetch 摘要页）。
- **与本团队关联**：与本队无关 3D 开发本身，而在其**评审协议**——「自动化实机测试评分 + 人类盲评」正是评估 AI 产出 Demo 可抄的流程；排行榜形态适合移植为内部 exp 横评。
- **借鉴点与建议动作**：存档；如需榜单数据（哪些模型造游戏最强）需补抓 arXiv 摘要页。

## 条目 4｜ChatNPC：情绪感知与上下文锚定的 NPC 对话
- **类型/来源/抓取**：学术论文｜ https://arxiv.org/abs/2611.29372 ｜ 2026-11-27（v1 发布 2026-11-22）
- **是什么**：情绪感知的陪伴型 NPC 框架（论文题 *Emotion-Aware and Context-Grounded Dialogue Agents for Personalized Video Game Interactions*，《面向个性化游戏交互的情绪感知与上下文锚定对话智能体》）。
- **机制与数据**：transcript 仅抓到 feed 一句话：**"ChatNPC: emotion-aware companion NPC adapting dialogue to player emotional shifts in real time via LLM tool-calling"**（ChatNPC 经 LLM 工具调用实时感知玩家情绪变化，动态调整对话个性化与情感基调）。技术路线确认为 **LLM tool-calling**；情绪状态的输入模态、对话生成模型、评测协议与数据集**未及抓取**（未单独 fetch 摘要页）。
- **与本团队关联**：像素 AVG 的 NPC 情绪系统可直接借鉴「情绪状态 → 对话参数」接口设计；tool-calling 是 NPC 记忆/情绪落地的主流做法，与本队薄 MCP「只传参数」纪律同构。
- **借鉴点与建议动作**：存档；若立项 NPC 情绪实验，先补抓摘要确认其情绪感知输入与评测基准。

## 条目 5｜PixelLab MCP Server（官方）：编码智能体内直接产像素画
- **类型/来源/抓取**：商业服务（官方托管 MCP + REST API）｜ https://www.pixellab.ai/vibe-coding （社区收录 https://mcp.so/servers/pixellab-mcp，条目 2026-10-08）｜ 2026-11-27
- **是什么**：PixelLab 官方 MCP 服务器，让 Claude Code/Codex 等 AI 编码助手在编码环境内直接生成游戏就绪像素画。
- **机制与数据**：能力覆盖：4/8 方向角色（**"characters with 4 or 8 directions"**）、骨骼与文本两种动画、tileset、新增的文本提示编辑像素画（免费）；mcp.so 条目 2026-10-08 更新，含定价（提及 Brazil-only 区域计划）。PixelLab 本体是**纯 REST API**；社区封装：PixelLabRat（DasDarki，带项目管理/资产评审/内嵌 Claude 助手）、pixellab-forge-mcp（rabbitcannon，纯 API 包装）、另有 pxl 开源工具与 YAML 配置批量动画生成器；r/aigamedev 有「Feedbacks on PixelLab MCP + Claude code」实测帖；存在「AI Builds a Godot Game From Scratch | PixelLab MCP」实机教程。官方定价页细节**未及抓取**。
- **与本团队关联**：覆盖「角色→动画→tileset」完整 2D 链路，正对本队美术管线缺口；REST 形态按「REST 优先、薄 MCP 兜底」可绕过 MCP 直接 curl 进 CI；第三方 MCP 封装属规约黑名单「未评审」范畴。
- **借鉴点与建议动作**：先 REST API 小样验证出图质量、tileset/autotile 格式能否直进 Godot 4.7；MCP 版留待人工评审后再用。

## 条目 6｜Texel Studio：开源「像画家一样作画」的像素画智能体
- **类型/来源/抓取**：开源项目（source-available，非 OSI；SPDX NOASSERTION）｜ https://github.com/EYamanS/texel-studio ｜ 2026-11-27（建于 2026-04-01，最近 push 2026-10-12，259 stars / 46 forks，main 36 commits）
- **是什么**：**"AI pixel art agent that paints like a real artist"**（像真画家一样作画的像素画智能体），明确非扩散模型；驱动商业站 texel.studio。
- **机制与数据**：绘图原语=pixels、rects、Bresenham lines、circles/ellipses、triangles、noise 与 Voronoi 填充，画后自检画布迭代；流程=用户描述 → Gemini 生成概念参考 → 智能体逐步作画 → 聊天微调 → 导出 PNG / 512px 放大 / **16 变体 autotile tileset**。技术栈 Python+FastAPI+LangGraph+LangChain，Next.js 静态前端；模型可插拔：Gemini（概念+智能体）、OpenAI（仅智能体）、本地 Ollama（推荐 qwen3:8b、llama3.1:8b）、任意 OpenAI 兼容端点（Llama.cpp/VLLM/LM Studio/OpenRouter）；可选 Redis 队列、S3 存储、LangSmith/PostHog 追踪。**无 CLI**：Web UI（localhost:8500）+ HTTP API `POST /api/jobs`，job 种类 `sprite.generate`/`sprite.chat`/`sprite.reference`/`sprite.tileset`/`sprite.from_photo`，README 有流式 curl 示例。许可原文：**"Use it freely — self-host, modify, use commercially, sell anything you generate"**，唯一限制是不得托管为竞品 SaaS；托管版 texel.studio 每日 5 免费 credits、Pro $9/月。
- **与本团队关联**：自托管 + 本地 8B 模型 = 无云端依赖、无按张付费，CPU-only runner 可过夜跑小样；`sprite.tileset` 的 autotile 变体可接 Godot 4.7 terrain；HTTP API「参数进、产物出」符合薄封装纪律。
- **借鉴点与建议动作**：试装；用 qwen3:8b 起步验证 sprite.generate/tileset 两类 job 的质量与耗时。

## 条目 7｜Retro Diffusion（Aseprite 原生扩展）：本地运行的像素画专用模型
- **类型/来源/抓取**：商业工具（专训模型 + Aseprite 扩展，本地运行）｜ https://astropulse.itch.io/retrodiffusion （另有 Gumroad 与 GitBook 文档站）｜ 2026-11-27（条款更新 2026-09-28）
- **是什么**：Astropulse 出品的像素画专训 AI 模型，以 Aseprite 扩展/插件形态在本地 GPU 或 CPU 上运行，在 Aseprite 内直接生成。
- **机制与数据**：特性=智能颜色/调色板与色板控制；生成大图无典型 AI 感（**"without typical AI artifacts like glow or blur"**——无光晕/糊化伪影）。定价：完整 Aseprite 扩展约 **$65 一次性买断**，另有 **$20 档**的提及。oryn.dev 对比文（2026-10-30 更新）指出其条款 **2026-09-28 更新、涉及生成产物归属**。2026 横评（Ludo「8 Best AI Pixel Art Generators in 2026」、GameDevAIHub「Retro Diffusion vs PixelLab (2026)」）将其列第一梯队，主要竞品为 PixelLab（亦有 Aseprite 扩展）。当前版本号/changelog**未及抓取**。
- **与本团队关联**：长在本队已在用的 Aseprite 上，摩擦最低的 AI 像素画入口；CPU 模式对无 GPU 机可用；调色板锁定对齐「风格锁定」需求；GUI 插件能否进无头 CI 未验证。
- **借鉴点与建议动作**：买前人工核对商用授权与产物归属条款；先在本地 Aseprite 做小样对比 PixelLab REST 出图质量。

## 条目 8｜Layer.ai：Reference Sets 风格训练 + Godot 插件
- **类型/来源/抓取**：商业云服务（风格训练）+ 编辑器插件｜ https://layer.ai/features/reference-sets （插件页 https://layer.ai/integrations/godot）｜ 2026-11-27（页面日期未及抓取）
- **是什么**：面向游戏工作室的 **"Reference Sets"**——角色与风格库，核心卖点 **"Train a Custom Art Style on Your Own Game Art"**（用自家美术训练自定义风格），功能覆盖 LoRA 微调、风格训练（旁及 voice cloning）。
- **机制与数据**：Godot 插件支持 **Godot 4.5+**，在编辑器内生成 sprite / sprite sheet / 9-slice UI，生成的 tile 通过 **TileMapLayer 集成**直接铺图。计费为按张付费的云服务（侦察报告口径）；具体价格、数据驻留条款、插件版本号**未及抓取**。旁证：r/aigamedev 有 3 人无美术独立队自训像素 LoRA 解决同款风格一致性问题的案例帖；PixAI 2026-05 教程给风格 LoRA 通用建议（数据集单一风格、触发词简单）。
- **与本团队关联**：「拿本队已定稿像素风格训专属风格库」是风格锁定方向最对口的商业方案；插件 tile 直连 TileMapLayer 可打通「生成→入库→铺图」全链路，与 Godot 4.7.2 兼容（4.5+）。
- **借鉴点与建议动作**：深挖；先补抓定价页与数据出境条款，再做 5~10 张同风格小样对比内部 LoRA 方案。

## 条目 9｜Gamedev AI（Fredarts）v1.1.0：Godot 4.7+ 专用 MIT 开源 AI 助手插件
- **类型/来源/抓取**：开源编辑器插件（MIT，Godot Asset Library #5086，分类 Tools/Community）｜ https://godotengine.org/asset-library/asset/5086 ｜ 2026-11-27（v1.1.0，2026-10-05）
- **是什么**：Fredarts 出品，自称 **"AI-powered coding assistant built from the ground up for Godot 4.7+"**（为 Godot 4.7+ 从零构建）/ "The Autonomous Software Engineer for Godot 4.7+"；横评称其为 **"closest free equivalent to commercial options"**（最接近商业方案的免费等价物）。
- **机制与数据**：**65 个智能体工具**，覆盖 scripts、nodes、TileMaps、程序化地牢（procedural dungeons）、animations；GDScript 生成带**可视 diff 预览**后应用；场景树节点编辑；**程序化合成 SFX**（procedural audio）；可视化 shader 生成（不含 sprite/图像生成）；**Watch Mode** 自动修引擎控制台报错；多智能体流水线 **Architect → Scene Builder → Coder → QA Tester** 带 auto-healing；本地向量库做代码库 RAG 检索；Git 页签可生成 AI commit message。API key 非必需：**Ollama / LM Studio 全本地可离线**，亦可接 Gemini/OpenAI/OpenRouter/NVIDIA NIM 云端。
- **与本团队关联**：版本精确匹配本队 Godot 4.7.2 且 MIT 免费；程序化音效合成是音频缺口的首个插件内补充；本地模型路径对 CPU-only 友好（8B 级推理慢但可用）。
- **借鉴点与建议动作**：试装；先在 exp 分支验证 65 工具集里 TileMap/地牢工具的实际覆盖与本地模型响应速度。

## 条目 10｜3D 生成秋季矩阵：Meshy 7.1 / Rodin Gen-2.5 / Hunyuan3D 3.1 Pro / Tripo 3.1 与 P2
- **类型/来源/抓取**：厂商对比文档（Scenario 帮助中心）｜ https://help.scenario.com/articles/1263568892-comparing-generative-3d-models ｜ 2026-11-27（页面 "Last updated 16 days ago" ≈ 2026-11-10/11）
- **是什么**：生成式 3D 模型横向对比页，收录当代 8 款 + 遗留 16 款模型。
- **机制与数据**：当代八款——Hunyuan 3D 3.1 Pro/Multiview（**10B 参数、1536 体素**、可选 PBR、multiview 最多 8 图）；**Tripo P2（preview）**原生 3D 扩散、**"optional quad mesh output"**、引擎就绪拓扑；Tripo 3.1（game-ready PBR、密度可调、四边网格）；Meshy 7.1（standard/2K/4K 分辨率档 + **"2K to 8K PBR texturing"**）；Rodin Gen-2.5（**"Five quality tiers, quad or triangle topology, and PBR textures"**）；Hitem3D 3.0（2048³、最高 5M 面）；Sparc3D 2.1（watertight、最高 2M 面、Portrait 变体）。遗留系：Hunyuan 3.0（Pro/Multiview/Sketch）/Part/2.1、Rodin Gen-2/Gen-1+HighPack、Sparc3D 2.0/初代、Meshy Image/Text-to-3D+Retexture/Remesh/Rigging、Trellis/Trellis 2、Direct3D-S2、PartCrafter、SAM3D 套件、Voxel Crafter 1.0。**关键硬信息：Tripo 2.5 的 "API integrations" 只工作到 2026-12-01**；各模型 API 可用性与定价页内未细分（未及抓取）。
- **与本团队关联**：本队无 GPU，3D 生成若做（2.5D/过场）只能走云端 API；Tripo 3.1/P2 四边网格对 Blender 后处理最友好。
- **借鉴点与建议动作**：存档；**如有历史 Tripo 2.5 集成脚本，2026-12-01 前必须迁移**（写进待办）。

## 条目 11｜Tripo H3.1 高细节模型 + Runway 官方集成 3D
- **类型/来源/抓取**：产品发布 + 平台集成｜ https://www.tripo3d.ai/blog/introducing-hd-model-v3-1 （博客日期未及抓取/未确认）；集成公告 2026-11-12（https://ashutoshai.com/ai-compass/2026/11/12/runway-3d-generation-tripo-h3-1 ；Runway 官方 X）｜ 2026-11-27
- **是什么**：Runway 官宣 **"3D is now supported in Runway"**（Runway 现已支持 3D）：文本或图像生成 3D 模型由 Tripo H3.1 驱动，亦可上传自有网格；入口 app.runway.com。Tripo 官方确认 **"proud to power Runway's new 3D capabilities"**。
- **机制与数据**：生成**带贴图 3D 模型**（textured models from text or images）；Runway 侧计费 **10-50 credits/次**；Tripo 列为 affiliate partner；模型可用作视频/创意工作流的 **shot references**。H3.1 定位：Tripo 旗舰高细节生产模型，致密几何，面向 **hero 资产与营销视觉**。另预告 3D 打印级输出（2026-11-17 PR：*Tripo AI Gives A First Look at Its Upcoming Print-Ready*——H 系列数分钟内把想法变成 3D 可打印物体）。
- **与本团队关联**：趋势信号——「专业 3D 模型被通用创意平台白牌集成」是 3D 资产分发新形态；H3.1 更适合营销渲染图而非游戏内资产（面数/拓扑未给游戏引擎适配口径）；本队无 GPU，此类生成全依赖云端。
- **借鉴点与建议动作**：存档；若日后需要 3D 营销渲染图，按 10-50 credits/次评估成本。

## 条目 12｜C2PA 新增 AI 披露断言 + 「签名覆盖零字节」漏洞
- **类型/来源/抓取**：标准实施指南 + 安全事件｜ 指南 https://c2pa.org/a-new-implementation-guide-for-content-credentials （页面更新 2026-08-11）；漏洞 https://www.lumethic.com/en/articles/c2pa-exclusion-flaw-signature-covers-nothing （演示 2026-10-02）；相机伪造 https://www.da.vidbuchanan.co.uk/blog/android-c2pa.html ｜ 2026-11-27
- **是什么**：C2PA 新实施指南教开发者为 AI 生成/AI 修改/非合成内容打防篡改签名清单；同期曝出动摇其核心保证的重大漏洞。
- **机制与数据**：指南五大板块：1) **`digitalSourceType`**（IPTC 词表：全模型生成/AI 增强/设备拍摄/人工编辑）；2) **`c2pa.ai-disclosure`** 断言——原文 **"captures model provenance, scientific domain, and the degree of human oversight"**（模型来源、科学领域、人工监督程度；页面未列更细子字段）；3) ROI 定位改动区域（**"a region of an image, specific paragraphs in a document, or defined segments of audio and video"**）；4) **`inputTo`** ingredient 配方记录 prompt、参考图、seed、参数；5) Actions 词表记录 `c2pa.created`/`c2pa.edited` 等生命周期步骤及每步 AI 使用标记。配套《Deployment Guidance》讲组织落地。游戏资产/实时 3D 未被提及（仅图像/文档/音频/视频）。漏洞侧：David Buchanan（retr0id）2026-10-02 利用 exclusion 机制造出 **"valid C2PA signatures cover literally zero bytes of the actual image content"**（有效签名实际覆盖 0 字节图像内容）的图片，彩票时间戳伪造演示证明可通过验证却系伪造；其 2026-08 已破 Google Pixel Android 最高评级 C2PA 相机实现（AI 图伪装成验证过的 Pixel 相片，硬件级缺陷无法现实修补）；另有 2026-03 「Authenticated Contradictions from Desynchronized」研究；Laburity/WorkOS 均有分析，维基百科 Content Credentials 词条已收录该漏洞。
- **与本团队关联**：asset_audit.py 可低成本顺手读取/记录 C2PA 元数据（哪张图出自哪个模型+seed）；**不可把 C2PA 当防篡改保证**——内部溯源仍以 MinIO 对象版本+清单为准。
- **借鉴点与建议动作**：把 `ai-disclosure`/`digitalSourceType`/`inputTo` 字段抄作资产审计元数据 schema；披露策略照旧「从第一版如实标注」。

## 条目 13｜ElevenLabs 11 月更新：Scribe v3 / v3 Live 语音转写进 API
- **类型/来源/抓取**：厂商更新（语音 AI）｜ https://releasebot.io/updates/eleven-labs （模型清单 https://elevenlabs.io/docs/overview/models）｜ 2026-11-27（Scribe v3 2026-11；Eleven v4 2026-09-28）
- **是什么**：ElevenLabs 11 月动态汇总：STT 新模型上线 + 语音智能体平台集成；TTS 旗舰仍是 9 月底的 Eleven v4。
- **机制与数据**：11 月 release notes——**Scribe v3 与 Scribe v3 Live**（实时版）进入 Speech to Text API；2026-11-04 **ElevenAgents** 与 NICE CXone、Genesys Cloud 等坐席平台原生集成（Voice AI Weekly #16）；voice agent 定价 **$0.08/通话分钟**（另加 LLM 与电话费）。**Eleven v4**（2026-09-28 发布）仍是最具情感表现的 TTS：从文本读出 **tone/pacing/emotion**（语气/节奏/情绪）、更准跟随导演指令、长篇制作中声音保持一致（the-decoder 口径；2026-11-16 research update 重申「最 emotive」）。对照面：Cartesia 11 月无新模型（仅对比文与 5 语言流式 STT 提及）；Hume 无结果；三厂商均**无游戏 NPC 专用语音模型**发布。
- **与本团队关联**：Scribe v3 Live 可低成本搭「配音对白自动转字幕/本地化校对」管线（CPU-only 转写走 API，本机零负载）；v4 文本内嵌语气/停顿标记利于 NPC 配音导演化；$0.08/min 对小样预算可控。
- **借鉴点与建议动作**：存档；出现 NPC 配音需求时先试 v4 + 语气标记的导演化写法。

## 附：过程性发现（侦察过程中的分支收获，未单列条目）
- **arXiv feed 富矿**：抓取当日 feed（2190 条命中、可见 39 条）另含大量游戏相关论文未单列：Lost in the Grid（2611.34152，GridProbe 定位 MLLM 在 Sokoban/迷宫是感知/规则/规划哪层失败）、中文狼人杀战略对话（2611.33747，12 模型对比）、S1Arena-MM（2611.29773，含 102 个截图闭环游戏环境）、RuleCraft（2611.28745，1240 道 Minecraft 规则题，「点名游戏」即可修正真实物理默认）、Schedule Rank Profile（2611.28368，自适应调度+Bradley-Terry 排行榜）、AstronautBench（2611.26910，Outer Wilds 自我改进）、MANGO Arena（2611.23613，供应链公司博弈）、GTAGym（2611.13028，GTA V 103 任务环境+LoRA-RL）、PlayCraft（2611.26624，视觉智能体玩游戏反哺改游戏）、社交博弈可验证训练（2611.31821，SFT+RLVR 使 Qwen3-4B 胜率 33%→81%）等，可作后续选题池。
- **Godot AI 插件生态横断面**：Godot AI（Asset Library #5050）v3.2.5 是支持 4.5/4.6 的最终版、4.7 以下不再支持、 reportedly 在 immutable Linux 上失效；hi-godot/godot-ai 提供 production-grade MCP server（Snap 安装）；r/godot 反馈单月涌入 12+ 个 AI 插件、社区情绪分化；**Godot 4.7 兼容已成为新版插件分水岭**；ziva.sh 维护 38 个 AI 工具分类清单。
- **像素画/音频补充工具**：SpriteCook.ai 纯 REST 像素画 API（sprites/animations/characters/tilesets，自带批量去背景）；SpriteFusion 精确尺寸 16×16~128×128、8 方向；音频侧 MMAudio（视频转音频，TAAFT 收录 3 个相关 API）、Eachlabs 多模型音频聚合 API（music/SFX/stems）。
- **数据处理说明**：网页摘要中的搜索引擎样板句（"REMINDER: You MUST include the sources..."）与 WebFetch 续读提示均为对抓取方的格式性元信息，已按数据处理、未执行；全程未发现要求执行/下载/安装的注入内容，未下载任何文件。
