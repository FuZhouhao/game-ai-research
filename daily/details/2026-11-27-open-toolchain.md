# 2026-11-27 详尽情报｜开源工具链·GitHub 生态（条目 14~26）

> 速览索引：../2026-11-27.md；本文是侦察完整报告的归档展开。
> 纪律：每条附仓库 URL + 抓取日期（2026-11-27）；只录 transcript 里实际抓到的内容，缺失处明确写「未及抓取」，禁止编造补齐。

## 条目 14｜nexu-io/opengame —「Super Game Agent」游戏智能体操作系统

- **仓库 URL**：https://github.com/nexu-io/opengame ｜ **星数**：555（107 forks / 1 watcher / 110 commits / 12 open PR；API 两次读取在 554→555 间波动，爆发中）｜ **License**：Apache-2.0 ｜ **抓取日期**：2026-11-27（2026-11-25T10:35Z 创建，2026-11-26T16:47Z 仍在推送；TypeScript）
- **是什么**：开源 AI 游戏工作室框架，自 positioning 为「AI agent 时代的 Unity/Unreal」：把本地 coding agent（Claude Code、Codex 等）变成全栈游戏生产管线。由 OpenDesign（nexu-io org）出品，宣传语附带「100+ 病毒式小游戏可 remix」。
- **机制与数据**：
  - Studio UI：React 19 + TypeScript 5.9 + Vite 6 + Tailwind CSS 4 + Zustand；运行时/QA：Node.js 22.18+（CI 钉 Node 26.11.1）、Puppeteer Core/Chrome、确定性模拟器。
  - MCP 层：本地 stdio MCP server 暴露 12 个 `openmotion_game_*` 工具（create、validate、simulate、playtest、capture、trailer、publish 等）+ 媒体/资产工具。
  - 技能层：入口 skill + 18 份工程手册（game design、3C/操控、动画、音频、playable ads、QA 门禁）。
  - BYOK 多模态网关：图像（GPT Image、Seedream、Nano Banana、FLUX）、音乐（ElevenLabs、Suno）、语音（ElevenLabs、BytePlus TTS）、视频（Wan、Seedance）；无 key 时降级为零 key 程序化兜底。
  - 预告片管线：无头捕获 + HTML 合成 + FFmpeg 导出 MP4。仓库布局：`studio/`、`gateway/`、`skills/`、`templates/`、`mcp.ts`、`server.ts`，`templates/games/` 下 25 个模板游戏（3D/voxel/anime/pixel/9:16，如 Tidebreaker、Neon Drift、Skyline Courier、Gate Legion、Merge Bakery，均可一键 remix/re-style）。
  - 引擎实质：**并非** Unity/Unreal——产物是独立 HTML5/Canvas，3D 用 vendored Three.js。兼容 22 种本地 agent（Claude Code、Codex CLI、DeepSeek TUI/Harness、Gemini CLI、Cursor Agent、WorkBuddy、OpenCode、Kimi CLI、Aider、Devin 等）。发布目标：微信小游戏、抖音、TikTok、itch.io（平台发布部分在路线图）、9:16 playable-ad 导出。
  - README 关键原文摘录："The Super Game Agent — the Unity & Unreal for AI agents, with 100+ viral games to remix."（中译：超级游戏智能体——AI agent 时代的 Unity 与 Unreal，附 100+ 可 remix 的爆款游戏。）
- **成熟度评估**：创建仅 2 天即 555★，爆发期；commit 活跃（110 次）；页面无 release/包，仅有 CHANGELOG.md（内容未展示）。架构文档齐全但未经时间检验，API 数据有延迟（星数两次读取不一致）。
- **与本团队关联**：非 Godot 技术栈（HTML5/Canvas），不能直接产出我们的引擎产物；但其「动词命名 + validate/simulate/playtest 内置」的 MCP 工具面可直接对照本机 godot-ai MCP（端口 8000 系）白名单设计；「playtest/截图/预告片全链路无头跑通」与 Gitea Actions CI 化思路同构；18 份工程手册是 godot-prompter 技能包的内容对标物。Node+Puppeteer 栈在 CPU-only 机器上可跑但占内存，试装前按 §7 评估。
- **借鉴点与建议动作**：① 对照 `openmotion_game_*` 工具面重审我们 MCP 白名单条款；② 参考其无头产物链设计阶段 4 Demo 验证；③ 手册分层（skills/handbooks）借鉴进技能包结构。**建议：值得深挖**（观察 2 周热度后再决定是否试装小样）。

## 条目 15｜gamedev-skills/awesome-gamedev-agent-skills —79 技能 + 引擎路由器

- **仓库 URL**：https://github.com/gamedev-skills/awesome-gamedev-agent-skills ｜ **星数**：11.5k（1.2k forks / 53 watchers / 300 commits）｜ **License**：Apache-2.0（维护者 Abhishek Barali）｜ **抓取日期**：2026-11-27（2026-11-11 完成 12 引擎版本校准）
- **是什么**：目前规模最大的游戏开发 agent 技能合集：79 个技能按 9 类组织，配一个「引擎探测→按需加载」路由器；SKILL.md 格式，兼容 Claude Code/Cursor/Codex/Gemini CLI。
- **机制与数据**：
  - 技能构成：引擎类 50（Godot 16、Unity 9、Unreal 6、Ebitengine 1、Web 引擎 6、其他引擎 12）；学科类 15（create-game-assets、game-ai、procedural-gen、save-systems、game-feel、performance-optimization 等）；品类 9（platformer、roguelike、rpg、fps-shooter、tower-defense、card-game、visual-novel、survival-crafting、puzzle）；工作流 5（game-jam、prototype-fast、steam-publish、itch-publish、game-docs）。50+15+9+5=79。
  - 覆盖 12 引擎：Godot、Unity、Unreal、Ebitengine、Phaser、PixiJS、three.js、Bevy、pygame、LÖVE、Defold、Roblox；钉版本：**Godot 4.7.2**、Unity 6.3 LTS、Unreal 5.8、Phaser 4.2.1、three.js r187。
  - 路由器三步：① 从项目文件探测引擎（`project.godot` 即 Godot）→ ② 读请求判断任务/品类/发布环节 → ③ 只加载匹配技能（先引擎基础、再概念、后品类粘合）。引擎选择互斥，学科/品类/工作流叠加。
  - README 关键原文摘录："In 366 blind test prompts the right skill loaded for 98.7% of the requests."（中译：366 条盲测提示词中，正确技能加载命中率 98.7%。）引擎版本说明标注 "checked 2026-11-11"（2026-11-11 校验）。
  - 安装：`npx skills add` 或 Claude Code plugin。其中 godot-resources 技能为纯指令无脚本（最后改动 2026-10-23）。
  - 姊妹篇：zhuyansen/awesome-3d-skills（https://github.com/zhuyansen/awesome-3d-skills ，2026-11-07 创建，9★，2026-11-25 仍在推送）——"MCP servers and skills that let AI agents work in 3D"（让 AI agent 干 3D 活的 MCP 与技能），覆盖 Blender/Unity/Godot/Unreal/CAD/Three.js，按安全风险分级。
- **成熟度评估**：11.5k★ 高热度、300 commits 持续维护、版本校准日期明确（11-11）、盲测数字公开可复核；风险在于技能量大质参差，需逐条过。
- **与本团队关联**：它 pin 的 Godot 4.7.2 与本机 `~/.local/bin/godot` 运行版本一致，Godot 16 技能可逐条对照补强现有 godot-prompter ~60 技能；「引擎探测→按需加载」入口模式可直接套用；awesome-3d-skills 的安全分级维度（读/写/执行）可回填 `.claude/rules/mcp-and-headless.md` 白名单条款。
- **借鉴点与建议动作**：① 先装 Godot 子集（16 条）做 diff 对照；② 抄路由器设计；③ 把安全分级维度写进 MCP 规约 PR。**建议：可直接试装**。

## 条目 16｜msveshnikov/claude-game-pipeline —概念图→Blender 无头→Godot 4 全链路插件

- **仓库 URL**：https://github.com/msveshnikov/claude-game-pipeline ｜ **星数**：44（6 forks / 1 watcher / 8 commits on main）｜ **License**：MIT ｜ **抓取日期**：2026-11-27（2026-11-13T19:19Z 创建，2026-11-23T10:02Z 仍在推送；Python）
- **是什么**：Claude Code 插件，一句话管线："ChatGPT concept art → Blender (Python, headless) → Godot 4 → Windows / Web / Android builds"（中译：ChatGPT 概念图 → Blender 无头 Python → Godot 4 → Windows/Web/Android 构建），宣称适配任意品类（RPG/射击/恐怖/平台/竞速/生存）。
- **机制与数据**：
  - 自动化内容：全部 3D 资产由 Python 程序化生成；UI 即代码；运行时关卡加载；自动截图巡游；自玩测试 `--autotest`；OpenCV ECC 把手绘概念图对齐到布局渲染图；按任务粒度 commit/构建/部署/验证；共享风格块 + 调色板 + 命名约定保持一致性。
  - 插件结构：`.claude-plugin/`（插件元数据）；`skills/game-pipeline/` 含 SKILL.md + 6 份参考文档（概念/提示词、task1–task5 模板、Blender、Godot、ChatGPT 浏览器下单流程、发布）；`scripts/` 含 `align_to_layout.py` 与 `chatgpt_upload/` 助手。
  - 依赖要求：Claude Code 桌面版（需登录 ChatGPT）、Blender 4.2+（作者在 5.2 开发）、Godot 4.x（**作者明示在 4.7.2 开发**）+ 导出模板、Python 3（numpy/pillow/opencv-python）。
- **成熟度评估**：44★ 起步期，8 个 commit，无 release 页；但依赖链简单（全是本机已有工具），文档结构完整，是 13 条里与本队技术栈重合度最高的一条。
- **与本团队关联**：本队正是「Blender CLI + Godot 4.7.2 + CI」同构栈；其 Blender Python 程序化资产生成的参考文档可直接读；`--autotest` 自玩 + 截图巡游可改造成 Gitea Actions 阶段 4 Demo 验证步骤；「共享风格块/调色板/命名约定」的一致性约束写法适配 exp 模板。Android 构建需 SDK/NDK/CMake，本机未配，先不管。
- **借鉴点与建议动作**：① 读源码提取 Blender→Godot 资产约定，写进 exp-template；② 把 `--autotest`+截图巡游方案抄进 exp_pipeline.yml 设计稿；③ 不必整包装。**建议：值得深挖**。

## 条目 17｜enoch3712/spine-hero-skill —一张原画→骨骼动画的 agent 技能（含确定性门禁）

- **仓库 URL**：https://github.com/enoch3712/spine-hero-skill ｜ **星数**：50（15 forks / 1 watcher / 3 commits）｜ **License**：**无**（页面未示 license，文件列表无 LICENSE；README 自述插件校验通过时带 "warnings about metadata the plugin directory asks for (licence, icon, author)"——插件目录要求而项目未提供的元数据警告）｜ **抓取日期**：2026-11-27（2026-11-11T18:43Z 创建，同日 19:03Z 最后推送；JavaScript）
- **是什么**：agent 技能（Claude Code/Codex/Cursor 三格式）：把一张角色原画切件绑到 Spine 式骨骼上，动画以代码化 key/IK 写出，取代旧 flipbook 路线（原文自述替换 "10 clips, 403 frames cut from generated videos"——10 段 clip、从生成视频抽的 403 帧）。武器/装备挂独立骨骼，换装不断招式。
- **机制与数据**（7 步管线）：
  1. Plan & brief——编排者每个动作写一份 brief，经子 agent 并行执行；
  2. Reference video——图生视频模型只为节奏/拍点参考，绝不描帧；
  3. Paint missing pieces——图像模型补被遮挡部件、新装备、快速挥击的关键姿势；
  4. Write each move——强编码模型把动作写成 key/IK，构建、捕获、自审；
  5. **Gate**——确定性脚本；
  6. Close-up check——独立模型按清单看特写；
  7. Final say——人工裁决，新缺陷回填系统。
  - Gate 设计：`gate.mjs` 纯 Node 无依赖（Node 18+），检查捕获的 `metrics.json`：滑步、地面速度、裂纹/残影、未回待机位、画出角色包围盒；原文强调 "No model judges the numbers"（中译：数字裁决不经过任何模型）。`gate-limits.json` 提供按「一款游戏、一个捕获尺寸」标定的示例阈值；`gate.test.mjs` 自带测试；`with_lock.sh` 支持多作者共享锁。
  - 缺陷检查：独立模型对脚部/头部 2 倍特写对照 `defects.md`——13 条「人工抓到而自动化漏掉」的缺陷；此后人工每抓到新缺陷即新增清单行或新 gate 检查项，形成反馈环。
  - 附带物：SKILL.md + 参考文档（pipeline/rig/locomotion/moves/reference-video/defects/gate/orchestration）+ gate 脚本 + 示例 metrics + 三工具插件清单。**不附带**：rig 构建器与帧捕获脚本（原项目专用）；需自备原画、Spine 式运行时（原例 Spine 4.2 + PixiJS）、捕获工具、模型（原例用 Claude Opus/Sonnet 5.5、Google Flow 视频、Nano Banana 2.1——注明为示例非要求）。
- **成熟度评估**：单游戏验证（侧视原画英雄、web 运行时），作者明示未在第二处试过；Codex/Cursor 安装路径明确标注未测；3 个 commit、无 LICENSE——只可读借鉴，不可入库其内容。
- **与本团队关联**：三层质检环（确定性 gate + 缺陷清单 + 人工回填）可直接迁移到 Aseprite 导出与 settle_gate 资产审计；并行子 agent 按动作拆 brief 的编排可借鉴；换装独立骨骼思路适用 2D 像素角色；Spine 4.2 商业运行时本队没有，需换 Godot Skeleton2D 或开源运行时才能落地。
- **借鉴点与建议动作**：① 把 gate.mjs 模式改写成 Godot 截图 metrics 校验脚本；② 缺陷清单反馈环写进 settle_gate 设计；③ 无 LICENSE，只读设计不入内容。**建议：值得深挖（只读）**。

## 条目 18｜owoevan-dev/music-skill —离线 CPU 的 agent 作曲/混音技能（游戏 loop 原生支持）

- **仓库 URL**：https://github.com/owoevan-dev/music-skill ｜ **星数**：293（34 forks / 50 commits on main）｜ **License**：分层——代码/文档 MIT；示例乐曲与录音 CC0 1.0；音色库 CC0/无限制（University of Iowa）/Unlicense（steel pan）；MS Basic 回退音色 MIT；Surge XT 及 `surge_host.py` GPL-3.0-or-later（只约束程序不约束产出的音乐）｜ **抓取日期**：2026-11-27（2026-11-02T10:25Z 创建，2026-11-26T15:01Z 仍在推送；Python；版本 v0.7.0——取自示例文件名，最新示例 release tag 为 `examples-5`）
- **是什么**：Agent Skill（Claude Code/Codex CLI 及其他技能加载型 agent）：agent 不用音频生成模型，逐音符写可编辑乐谱，管线 Write → Check score → Perform → Render → Mix → Measure（写→校验→演奏→渲染→混音→测量）；原文强调 "Runs offline on CPU; no GPU, account, or telemetry"（中译：纯离线 CPU 运行，无 GPU、无账号、无遥测）。
- **机制与数据**：
  - 记谱：音高/时值在乐谱内，演奏细节（力度、时值、release）分开存；改一个音符只重合成该声部，未改声部播放缓存 stem（类比冻结的 DAW 轨）；长曲由 agent 生成短 Python 脚本书写。
  - 游戏向功能：loop 点按 **Godot 和 RPG Maker 认的格式**写进 WAV/Ogg；混响尾折回 loop 头；每段落打 cue point；loop 可拆成求和等于整混音的分层 stem——原文 "music that builds as play heats up"（中译：随玩法升温而层层加入的音乐）；按精确长度/打击点/loop 长度写出，编辑时只重写变动小节；8-bit/chiptune 支持（示例：平台跳跃第一关 loop）。
  - 混音与测量：drum/bass/rhythm/ensemble/lead 五总线 + 4 个生成混响；母线 −16 LUFS 默认（流媒体 −14）、true peak ≤ −1 dBTP；管弦距离、可选耳机混音、分声部立体声运动；电子乐扩展（sidechain ducking、节拍同步延迟、滤波扫频）；`analyze` 报告分段电平/频谱/声像/旋律-伴奏距离/对商业参考的音色平衡。
  - 产物：MP3+WAV、MIDI、每声部一根 stem、总线与混响返回、工程文件；带 loop 元数据的游戏用 Ogg；piano-roll 视频（<10 MB）与静帧。24 线程笔记本上六个示例渲染耗时 25–156 秒。
  - 音源：31 个采样 SoundFont 库（约 3.6 GB 下载 / 8 GB 安装；CC0 或无限制）经 FluidSynth；Surge XT 合成器 3,008 音色（GPL，经独立 GPL host 运行）；内置合成器/鼓机；电吉他/贝斯逐弦经箱体模型渲染；支持自定义 SF2/SFZ。
- **成熟度评估**：293★/50 commits 活跃维护；版本号取自示例文件名（非正式 release），文档完整；纯 CPU 渲染在秒级，工程风险低。
- **与本团队关联**：CPU-only runner 完全可跑；Godot loop 元数据写入直接解决 BGM 循环需求；分层 stem 适合动作类 demo；但 **SoundFont 全量 8 GB 磁盘占用触发本队 §7 内存/磁盘守则**——先装 MS Basic（MIT）回退音色小样验证，按需再装子集；产物（WAV/Ogg/stem）按规约进 MinIO 不进 Git。
- **借鉴点与建议动作**：① loop 元数据格式直接用于 exp demo BGM；② stem 分层结构借鉴进动作 demo 音乐设计；③ 按小节增量重写的缓存策略符合分批守则。**建议：可直接试装（注意磁盘约束）**。

## 条目 19｜jasonmello/pixelstrata —2D/3D 像素游戏 agent 技能包（PixelLab 生成管线）

- **仓库 URL**：https://github.com/jasonmello/pixelstrata ｜ **星数**：2（0 forks / 0 watchers / 12 commits on main）｜ **License**：Apache-2.0（含 NOTICE 文件；示例截图 © Scraphead Games 不在授权内；声明与 PixelLab/ElevenLabs/Gameplay Atlas 无隶属关系）｜ **抓取日期**：2026-11-27（2026-11-02T18:18Z 创建，API 显示 2026-11-22T08:15Z 有推送，仓库页未显日期；Python；Godot 4.x 徽章）
- **是什么**：面向 "2D and 3D pixel-art games"（2D/3D 像素游戏）的开源 Agent Skills 包（兼 Claude Code plugin），在 awesome-gamedev-agent-skills（即条目 15，77 个引擎/品类/学科技能 + 代码路由器）之上叠加规划与资产生成层。
- **机制与数据**：
  - 工作流：plan mode 起步→询问视觉风格（pixel-16bit、hi-bit、low-poly、toon）→从 Gameplay Atlas 取机制→分阶段门禁推进：Setup → Concept → Prototype → Vertical slice → Production → Polish → Ship。
  - 技能清单：`pixelstrata`（入口 + 资产管线 + `assets.json` 清单）、`pixelorama`（Pixelorama 清理与 CLI spritesheet 导出）、`material-maker`（JSON 程序化材质）、`terrain3d`、`jolt-physics`、`three-quarks`（three.js 粒子 VFX）、`godot-mcp`（跑 Godot、读报错）。
  - PixelLab 角色：生成像素 sprite/tileset，**付费 API**、用用户自己的 key（`PIXELLAB_API_KEY`）；ElevenLabs 做 SFX/音乐/语音（`ELEVENLABS_API_KEY`）；两者在无 key 时优雅降级。
  - 引擎目标：跟随条目 15 路由器的 12 引擎全集；Godot 专属增强为 godot-mcp 验证与 Terrain3D；three.quarks 面向 three.js。
  - 发布复用依赖包的 `itch-publish`/`steam-publish`。
- **成熟度评估**：极早期——2★、12 commits、release 空、日期信息不全；质量未经第三方验证；其价值几乎全部来自底层条目 15。
- **与本团队关联**：`assets.json` 清单驱动「生成+校验」的模式可对照 MinIO 资产审计脚本设计；Pixelorama CLI 是 Aseprite（本机为自编译、不得分发）之外的**开源替代参考**，对团队许可证合规有直接意义；分阶段门禁命名（Vertical slice 等）可借鉴进实验工单模板。付费 API 需自带 key，按规约 key 只进运行机环境变量。
- **借鉴点与建议动作**：① 存档 `assets.json` 模式；② 记下 Pixelorama CLI 备选路线；③ 不装包，等成熟或直接吸收条目 15 底座。**建议：仅存档**。

## 条目 20｜RainBowLuoCS/Gamer —米哈游崩坏 AI 团队的实时游戏 VLA 基础模型

- **仓库 URL**：https://github.com/RainBowLuoCS/Gamer ｜ **星数**：1.6k（27 forks / 23 watchers / 6 open issues / 5 commits on main）｜ **License**：Apache-2.0 ｜ **抓取日期**：2026-11-27（2026-10-30T07:10Z 创建，2026-11-16T05:39Z 推送；arXiv:2611.18397；伴生论文 GameScaling arXiv:2610.28698）
- **是什么**：通用视觉-语言-动作（VLA）基础模型：看屏幕截图、直接输出**原生键鼠动作**，处理 2D GUI 与 3D 世界中的长时程实时任务。出品方：米哈游「崩坏 AI 研发团队」，合作机构含新加坡国立大学、清华、国科大、中科大。
- **机制与数据**：
  - 三阶段训练：continued pre-training（CPT）→ sparse-reasoning SFT → Temporal-Aware GRPO（TA-GRPO）强化学习。
  - 动作表示：200ms 动作块（6×约 33ms 步）、74 个大小写敏感按键 token；记忆系统跨上下文窗口携带任务进度。
  - 基准：《崩坏：星穹铁道》两支线——"Opportunity Makes the Thief (Part I)" 80.0%（RL 后，CPT 仅 34.4%）、"Bestial Ferocity" 83.6%；七类小游戏宏平均 49.7%（RL 后）；在传统 2D 游戏基准上亦有竞争力。
  - 推理：NVIDIA H200 + Qwen3.5-35B-A3B MoE 底座，时延 1306.00ms → 65.12ms（20.1 倍提速）。
  - 开源状态：论文、system-prompt 文档、demo 已完成；**streaming-vLLM 推理引擎标注 "Coming soon"（中译：即将推出）**；模型在 THUSI-Lab Hugging Face 集合；用法细节在伴生仓库 GameScaling。
- **成熟度评估**：论文级开源（5 个 commit，代码形态偏研究发布）；核心推理组件未放出；无 GPU 环境不可复现推理。
- **与本团队关联**：本队 CPU-only runner 无法自跑（H200 量级），不试装；但其「真实键鼠动作 vs API 注入」路线是 xt4d/PlayCraft 类 AI playtest 方向的重量级参考实现；「确定性动作块 + 记忆跨窗口」设计可借鉴进长流程测试 agent 的编排；后续 streaming-vLLM 开源与 20 倍推理优化值得持续跟踪。
- **借鉴点与建议动作**：① 留作 playtest 情报源，跟踪其推理引擎开源；② 借鉴动作块/记忆设计写进测试 agent 方案稿；③ 不装。**建议：仅存档（季度跟踪）**。

## 条目 21｜cranebeaker/coop-anything —用 agent 给任意单机游戏加联机

- **仓库 URL**：https://github.com/cranebeaker/coop-anything ｜ **星数**：2213（301 forks / 11 watchers / 1299 commits on main / 164 open issues / 9 PR）｜ **License**：MIT ｜ **抓取日期**：2026-11-27（2026-10-16T11:12Z 创建，2026-11-25T21:14Z 仍在推送；Python；伴生网站 coopanything.app）
- **是什么**：给 AI coding agent 用的 playbook + MCP 服务器：把 agent 指向任意单机游戏，建造或复活联机 mod（在线与分屏）。README 标语："Any single-player game. Your friends. Your agent does the work."（中译：任何单机游戏。你的朋友。活让 agent 干。）
- **机制与数据**：
  - "Co-op Anything MCP"：让任意 agent 搜索联机目录、从游戏安装目录探测引擎、读 playbook/技能、校验社区贡献；Claude Code 经仓库 `.mcp.json` 自动发现，其他 agent 手动接入（`playbook/mcp.md`）；设计上与 **REA 逆向工程 MCP** 配对。
  - 支持 agent：Claude Code、Codex、Gemini CLI、Cursor、OpenCode 等。
  - 已落地作品：**Deus Ex（已发布）**、Fallout: New Vegas、Zelda: Ocarina of Time（全同步）、Dungeon Keeper、S.T.A.L.K.E.R. Shadow of Chernobyl；社区在建含 Mega Man X/X4、Pilotwings 64、Enter the Gungeon、Stacklands、Divinity II、Command & Conquer 3 等；目录收录 230+ 联机 mod 与缺口。
- **成熟度评估**：2.2k★/1299 commits/164 issues，社区真实活跃，有已发布成品；模式经过实战验证。
- **与本团队关联**：与主业（自研游戏）无直接交集，但三个模式可借鉴：① 「引擎探测→按引擎发 playbook→贡献校验」的编排与 CI 按分支跳 Godot 步骤的守卫思路同源；② 「validate contribution」校验模式可用于 research 采集结果入库前校验；③ 逆向+agent 改造老游戏对研究前辈像素游戏资产/玩法有工具价值。（归档者注：本机工具链已装有 REA MCP，与 coop-anything 声明的配对对象一致，未来做逆向类实验时可直接组合。）
- **借鉴点与建议动作**：① 记录引擎探测/贡献校验两个模式；② 逆向前辈游戏素材研究时可启用。**建议：仅存档**。
- **勘误**：速览版写「已落地《杀手》等联机 mod」，按本次抓到的 README 原文应为 **Deus Ex（杀出重围）**，速览版系笔误，以此为准。

## 条目 22｜MikeSchulze/gdUnit4 v6.2.3 —已知项目新版本（Godot 4.7 兼容修复）

- **仓库 URL**：https://github.com/MikeSchulze/gdUnit4/releases ｜ **抓取日期**：2026-11-27（releases API 抓最近 5 个版本）
- **是什么**：本队基线已收录的 Godot 4 单测框架发布补丁版 v6.2.3，重点是与 Godot 4.7 的兼容修复。
- **机制与数据**（releases API 原始列表）：
  - **v6.2.3**（2026-11-01T19:59Z）：修复 Godot 4.7 字号问题、logger 泄漏、参数化/跳过测试、scene runner 输入；降低 auto-save 开销。
  - v6.2.2（2026-10-07T18:52Z）：修复 bash shebang、run-until-failed、孤儿节点检测、字符串 diff 内存、inspector 缩放；**CI 升级到 Godot v4.8.dev7**。
  - v6.2.1（2026-08-20T11:42Z）：修复 CI runner 关闭、大小写不敏感 mock 匹配、TCP 帧重组、spy 崩溃、测试参数解析。
  - v6.2.0（2026-07-28T19:38Z）：大版本——Inspector UI 重做、报告含完整错误堆栈、孤儿节点检测重构。
  - v6.1.3（2026-04-27T14:52Z）：CLI 发现阶段 parse-error 检测、项目设置变更韧性、inspector 无响应与 HTML 报告修复。
- **成熟度评估**：发版节奏稳定（4-27 / 7-28 / 8-20 / 10-07 / 11-01 五连发），上游 CI 已在跟 Godot 4.8.dev7——既证明维护活跃，也提供了观察 Godot 4.8 变化的窗口。
- **与本团队关联**：v6.2.3 的「Godot 4.7 字号修复」正命中本机 4.7.2 运行时；scene runner 输入修复直接关系 `godot --headless` 单测稳定性——这两点都是 settle_gate 测试链路的直接依赖。
- **借鉴点与建议动作**：① CI/本机把 gdUnit4 升到 v6.2.3；② 升级后跑一遍现有单测回归确认无破坏；③ 顺带盯 v6.2.2 起的 4.8.dev7 适配笔记。**建议：可直接试装**。

## 条目 23｜npgamedev Godot MCP Toolkit 1.1.2 —资产库上架的 Godot MCP 插件

- **仓库 URL**：https://store.godotengine.org/asset/npgamedev/godot-mcp-toolkit ｜ **抓取日期**：2026-11-27
- **是什么**：上架 Godot 官方资产库的 MCP server + addon 双件套，代表「插件化 MCP 进官方资产库」的发行形态；与基线里的 Coding-Solo/godot-mcp（0.42）是**不同项目**。
- **机制与数据**：1.1.2 于 2026-10-29 发布，重点修复 **Linux/macOS 端口问题**（非 Windows 平台可用性）。其余：addon 与 server 的具体工具面、依赖、配置方式——**未及抓取**（本次只经搜索结果确认版本与修复要点，未抓取资产库页面或仓库 README；GitHub API 检索亦未命中该仓库）。
- **成熟度评估**：能进官方资产库本身即通过 Godot 资产库的提审；1.1.2 的平台修复说明早期版本在 Linux 上有实际障碍。
- **与本团队关联**：其 Linux 端口问题记录可与本机 godot-ai MCP（端口 8000 系）的部署经验对照排坑；「addon+server 双件套」形态可作未来团队内部工具经 Gitea 分发的参考形态。本队已有可用 godot-ai 工具链，不重复引入。
- **借鉴点与建议动作**：① 存档发行形态与版本节点；② 遇 godot-ai 端口/平台问题时回头查其修复记录。**建议：仅存档**。

## 条目 24｜平台信号：Epic 与 Unity 的官方引擎内置 MCP

- **来源 URL**：Epic 文档 https://dev.epicgames.com/documentation/unreal-engine/unreal-mcp-in-unreal-editor ｜ Unity 文档 https://docs.unity3d.com/Packages/com.unity.ai.assistant@2.0/manual/unity-mcp-overview.html ｜ UEFN 公告 https://www.fortnite.com/news/unreal-mcp-is-now-available-in-uefn ｜ **抓取日期**：2026-11-27（三个官方页面本体**未及抓取**，以下日期与功能描述来自本次搜索结果摘要与多条独立来源交叉）
- **是什么**：两大商业引擎先后把 MCP 做成编辑器原生能力的平台级信号；Godot 仍无官方方案，全靠社区（bradypp/godot-mcp、npgamedev、Godot 论坛 addon 等）。
- **机制与数据**：
  - **Epic / Unreal**：UE 5.8（约 2026-06-23 发布）内置**实验性 MCP server**，支持 Claude、Codex 等 MCP 客户端（官方演示含 AI 辅助程序化城市生成）；Unreal MCP 是编辑器内原生 server：暴露经 **Toolset Registry**（工具集注册表）注册的工具、支持 Resources、接受任意 MCP 客户端连接；2026-08-20 Epic 宣布 Unreal MCP 进 UEFN——免装插件，agent（Claude Code、Cursor）可写 Verse、摆设备、搭 UI、跑试玩会话；2026-11-11 Epic AI MegaJam 2026 开赛，主推口号 "connect your agents to the editor with Unreal MCP"（中译：把你的 agent 接到编辑器上）。Reddit 迹象显示 Epic 在持续向编辑器内建 AI agent 框架（commit 观察）。
  - **Unity**：Unity AI 公测 2026-05-01 起对 Unity 6+ 全体开发者开放，官方 MCP Server 是头部功能；文档挂在 `com.unity.ai.assistant` 包（2.0.0-pre.1）；后续更新把**官方 MCP server 改为付费功能**，引发 Reddit r/Unity3D 争议（用户自带 AI 订阅/key 还要再付费）；第三方 CoplayDev/unity-mcp（MIT）保持免费。
- **成熟度评估**：Epic 路线 = 免费内置 + 大赛推流，节奏快；Unity 路线 = 官方收费 + 社区免费并行，分化明确。两者共同宣告「引擎原生 MCP 成标配」。
- **与本团队关联**：Epic Toolset Registry 的「工具集注册+白名单暴露」设计可参考本队「MCP 只传参数」治理条款；Unity「官方收费、社区免费」的分化验证了本队「REST 优先、薄 MCP 自持」路线的独立性价值；Godot 官方是否跟进内置 AI/MCP 直接影响本机 godot-ai 工具链的中期路线——列入季度跟踪。
- **借鉴点与建议动作**：① 季度复查看 Godot 官方动向；② 白名单治理条款可参考 Toolset Registry 语义。**建议：仅存档（趋势条目，季度跟踪）**。

## 条目 25｜superwyh/Game-Localization-Engineering —面向 coding agent 的游戏本地化工程技能

- **仓库 URL**：https://github.com/superwyh/Game-Localization-Engineering ｜ **星数**：79 ｜ **抓取日期**：2026-11-27（2026-11-14T08:31Z 创建，同日 14:03Z 最后推送；Python）
- **是什么**：给 coding agent 的游戏本地化工程流程技能。GitHub API 描述原文："Engineering-focused game localization for coding agents: contextual translation, review, engine integration, QA, reports"（中译：面向 coding agent 的工程化游戏本地化：上下文翻译、审校、引擎集成、QA、报告）。
- **机制与数据**：定位偏「工程流程」而非纯翻译——上下文感知翻译、审校环节、引擎集成、QA 与报告产出。具体技能拆分、术语表机制、引擎对接方式、LICENSE——**未及抓取**（仅命中 GitHub API 检索列表与一段描述，未抓 README/仓库页；创建与推送同在 11-14 当天，推测一次性上传）。
- **成熟度评估**：79★ 起步热度可观，但当天建当天推、无后续推送记录，持续维护情况未知。
- **与本团队关联**：中文是本队工作语言，「上下文术语表 + 审校」环节可直接用于游戏中文文案质量流程；「本地化 QA 报告」形态可挂进 settle_gate 检查项；出海/多语言需求出现时它是现成起点。
- **借鉴点与建议动作**：① 存档；② 有出海需求时再抓 README 深挖。**建议：仅存档**。

## 条目 26｜op7418/guizang-game-skill —单 HTML 3D 动作游戏 agent 技能

- **仓库 URL**：https://github.com/op7418/guizang-game-skill ｜ **星数**：511 ｜ **抓取日期**：2026-11-27（2026-11-11T16:28Z 创建，同日 18:22Z 最后推送；JavaScript）
- **是什么**：歸藏（op7418）发布的 Claude Code/Codex 技能。GitHub API 描述原文："Agent skill for Claude Code / Codex that builds a playable browser 3D action game with AI-generated assets"（中译：为 Claude Code/Codex 构建可玩浏览器 3D 动作游戏的 agent 技能，资产由 AI 生成），three.js 实现、**单 HTML 文件**产出，附可玩武侠 demo。
- **机制与数据**：技能内部结构、提示词组织、资产生成调用链——**未及抓取**（仅 API 检索列表级信息，未抓 README）。同形态旁证（同批 API 检索抓到）：elcronos/whiteout-onefile——"WHITEOUT: a single-file (1.15 MB) procedural 3D survival horror browser game"（1.15 MB 单文件程序化 3D 生存恐怖浏览器游戏）+ 创建它的 Claude Code（Opus 5.5）技能，8★，2026-11-19 创建；Megasu/jimao-3a-game——Saltline 中文版存档（来源 Felix Rieseberg 的 Claude 案例，约 1.4 MB 单文件离线 3D 射击），138★。说明「技能即可直接产出可玩成品」形态 11 月连续出现。
- **成熟度评估**：511★ 传播力强；单 commit 日完成、demo 即成品；工程深度未知，价值在形态不在实现。
- **与本团队关联**：非 Godot 技术栈（three.js 单文件），不试装；但「技能 + 可跑 demo 成品」作为技能包的交付/宣传形态值得 godot-prompter 技能包补一个可跑 demo；单文件产物小，便于进 `qa-report`/`build-exp` 做小样评审。
- **借鉴点与建议动作**：① 给现有技能包补 demo 成品；② 单文件产物作为小样评审载体。**建议：仅存档（借鉴形态）**。

## 基线复核（展开）

对基线已收录项目的 release/版本动态复核结论（第 1 路侦察收尾步骤，全部有 API/搜索原始证据）：

1. **Coding-Solo/godot-mcp**：releases API（`/repos/Coding-Solo/godot-mcp/releases?per_page=5`）返回空数组 `[]`——无新 release，**0.42 仍为最新**。基线不用动。
2. **godot-skills 1.1.0**：专项搜索（"godot-skills release new version November 2026"）确认**无 11 月新版本发布公告**；但生态活跃：skills-hub.ai 收录页 2026-11-23 同步；Godot 官方论坛 2026-10-15 出现 24 技能 MIT 包（Codex/Claude Code/Cursor/Gemini CLI）；2026-11-21 出现 76 技能 12 引擎新包；alexmeckes/godot-claude-skills（5 技能，MIT，2026-03）与 fenixnix/Godot-Skills（12 技能，MIT，2026-03）为更早的同类包。结论：基线 1.1.0 维持，生态增量记入本条目 15。
3. **Donchitos/Claude-Code-Game-Studios**：仅星数上涨至约 40.8k（49 agents、72-74 skills 结构不变），无结构变化，基线不用动。
4. **GameAnything（AetherLabsAI）**：2026-11-23 创建、33★（本次 API 检索再次抓到），**已在基线内，不重报**。
5. **同名消歧**：本次条目 14 的 **nexu-io/opengame（2026-11-25 创建，爆发中）** 与早前 **leigest519/OpenGame（2026-04，prompt→网页游戏）** 是两个同名不同仓库；后者是 4 月旧项目，前者才是本次爆发的新项目，引用时勿混。

## 附：过程性发现

侦察过程中抓到但未列入正式条目的信号（按主题归组，均来自本次 transcript 实抓内容）：

- **MCP 安全**：npm 包 "Godot MCP" server 披露 **CVE-2026-25546**（0.1.1 修复，NIST 收录日期 2026-02-04）——印证 `.claude/rules/mcp-and-headless.md`「来源不明 MCP 不装」黑名单条款的必要性。
- **Godot MCP 生态增量**：Godot Editor MCP 2026.11.04 版本；Reddit r/godot 讨论确认 Godot AI HTTP server **默认端口 8000**（与本机 godot-ai 端口系一致）；bradypp/godot-mcp；Godot 论坛免费 MCP server+addon（2026-02）；summerengine.com 的 Godot MCP 指南（2026-03）。
- **技能生态增量**：zhuyansen/awesome-claude-code-skills-collections；某 1000+ 技能的 claude-code-skills 仓库（2026-10）——技能合集赛道整体过热，采信前需逐个验源。
- **Playtest 方向旁证**：OpenAI Agent Skills 库含 **game-playtest** 技能（检查项：开机序列、输入处理、场景切换、HUD 可读性、视觉状态校验）——其详情页 mcpservers.org 抓取返回 **HTTP 403**，源仓库归属未确认，**未及抓取**；Unity Play Mode C# 试玩讨论（r/LLMDevs）；arXiv 2509.22170（LLM 游戏测试）。
- **AI NPC 方向旁证**（与日报学术条目 4 ChatNPC 同主题）：code-forge-temple/local-llm-npc（Gemma 3n，Godot 4.2.x drop-in）；AkshitIreddy/Interactive-LLM-Powered-NPCs；GigaxGames/gigax；neocortex.link 的 Godot AI NPC 工具（2026-10，Godot 4 SDK，含情绪/口型/群聊）——CPU-only 约束下 Gemma 3n 级本地模型路线相对可行。
- **社区引擎 MCP 旁证**：IvanMurzak/Unity-MCP（2026-11-08 上架 Google MCP registry）；CoderGamester/mcp-unity；ChiR24/Unreal_mcp（issue #54 活跃）——与条目 24 的官方化趋势互为印证。
- **GitHub API 检索长尾**（本次三条查询：`godot mcp created:>2026-11-01` 命中 99 条取前 15；`claude game created:>2026-11-10` 前 15；`game agent playtest OR playtesting created:>2026-10-15` total_count 10474 宽匹配取前 15）里有参考价值的旁证仓库：realskyrin/ns-game-apple-arm-port（539★，Switch 游戏→Apple Silicon 移植技能，Rust+Metal）；daniel-madrid-07/weeping-of-the-empire（346★，TotK 1.0.0 重编译到 Windows/Vulkan，主要由 AI agent 写就，不含游戏文件）；abouchedidxcode/open-source-hands（225★，MediaPipe 摄像头手势游戏）；LumioGames/LGUI（169★，「给 AI agent 的游戏 UI 框架」，浏览器搭建导出 Unity）；Cynthia-wlan9509/offline-game-revival（123★，停运手游离线纪念版复活技能，截图/录屏数据抢救管线）；uilianks/kiln（87★，低模/体素 3D 资产即代码 DSL，导出 GLB，agent 可读预览）；luccacerfz/character-factory-skills（42★，7 技能：一页人设→绑定测量的 Unity prefab，经 Tripo+Blender Rigify+critic agent）；chongdashu/unreal-5.9-skill（16★，UE 5.9 Preview 实战经验技能，跑在引擎内置 MCP 上——与条目 24 互证）；devall96/Unchained（9★，Whiplash 2003 静态重编译原生移植）；bbayram-l/retrocrunch（5★，PS1 风格资产管线，Rust+Godot 4+CLI+MCP）；SVLubin/VoxelCAD（5★，Godot 4.7/C# 的 CAD 式体素编辑器，MCP 内建）；cavi-ai/godot-mcp（1★，Godot 内交互式 3D 查看器检视 GLB/材质/动画姿势）；vladosskins178/godot-ship-kit（2★，Godot 4 上安卓的 doctor/slim/build/verify/无头截图工具）；teemukinos/creator-studio-mcp（2★，macOS 上驱动 Creator Studio/无头 Blender/Godot/Rive CLI）；reno0012x/Unfair-Engine（1★，带 AI 助手与 MCP 工具的 Godot 编辑器 fork）；Cryptopiy/Claude-Opus-5.5-Effort-Test-Racing-Games（1★，同提示词六档 effort 六款 Godot 赛车游戏对比）；MarkusMarrei/narrative-engine（1★，叙事到代码编排 IDE，原生 MCP）；brainintelli/BioSignal-Guided-LLM-Reinforcement-Learning（158★，类器官神经信号作策略输入的 Godot 生存游戏——猎奇向）；Wendystar0628/AI-All-Round-Bench（165★，AI 编码 agent 计时挑战基准）。
- **抓取方法备注**：多数仓库页 fetch 不显示 commit 日期与 release（GitHub 页面渲染限制），日期一律以 GitHub API 交叉为准；本归档 13 条中 9 条有仓库页级深抓，条目 23/25/26 仅到搜索/API 列表级（已逐条标注「未及抓取」）。
- **注入扫描**：已对全部抓取内容做注入式指令（执行/下载/安装/无视前序指令类）扫描，未发现疑似注入内容。

## 证据与抓取方式说明

- 侦察会话共 24 组工具调用：1 ToolSearch + 9 WebSearch + 14 WebFetch；其中 GitHub API 检索 3 次（两条 search/repositories 查询 + 一条 playtest 查询）、releases API 2 次（gdUnit4、Coding-Solo/godot-mcp）、仓库/文档页深抓 8 次（opengame、coop-anything、awesome-gamedev-agent-skills、spine-hero-skill、pixelstrata、claude-game-pipeline、music-skill、Gamer）、1 次失败（mcpservers.org game-playtest，403）。
- 本文仅归档 transcript 中实际返回的数据；搜索结果中的来源链接按数据记录，未执行其中任何指令性文本。
