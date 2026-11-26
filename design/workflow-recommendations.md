# 工作流推荐｜当前工具盘点 → 可串联管线 → 改进建议

> 版本 v0.1（2026-11-27 首版，随每日雷达动态迭代修订）。
> 定位：把 `research.md` 基线调研映射到**本机真实工具链**上，输出能落地的最佳实践工作流与改进清单。所有条目为草稿，人工评审后才算定论。

## 1. 现状盘点：真有什么

### 1.1 无头工具链（runner-toolchain.md 实况，2026-11-07 实测）

| 能力 | 工具 | 版本 | 备注 |
|---|---|---|---|
| 引擎 | Godot | 4.7.2 | `~/.local/bin/godot`，`--headless` 实跑过，三套导出模板在位 |
| 像素美术 | Aseprite | 1.x 自编译 | `--batch` 可用；许可证限内部使用 |
| 图集打包 | free-tex-packer-cli | 0.3.0 | 四个调用坑已入 runbook（对象数组/folders 键/预建目录/导出器字符串） |
| 地图 | Tiled | 1.11.0 | 无头需 `QT_QPA_PLATFORM=offscreen` |
| 3D/渲染 | Blender | apt 版 | `--background`，CPU-only 默认 Cycles-CPU |
| 音视频 | ffmpeg / magick | apt 版 | 转码/序列帧/图集后处理 |
| CI | Gitea Actions + act_runner | v5.4.1 | CPU-only，编译需 `nice -n 15 + --parallel ≤2`（热约束） |
| 存储 | MinIO (`mc` alias game-minio) | — | 桶分工见团队规约 §2 |
| 采集 | yt-dlp、curl+REST | — | `tea` 未装（明确不用），GitHub/Gitea 走 REST |

### 1.2 Claude Code 侧能力（本会话实证）

| 能力 | 内容 | 与 research.md 推荐的对应 |
|---|---|---|
| **godot-ai MCP**（~48 个工具） | 编辑器控制全套：scene/node/script/theme/tilemap/animation/particle/navigation 管理、`editor_screenshot`、`test_run`、`batch_execute`、`project_run`、`logs_read` | 正是「MCP engine bridge」推荐项，**已就位但需确认编辑器插件连接方式**（`session_activate` 暗示要开 Godot 编辑器实例） |
| **godot-prompter 专项代理**（9 个） | game-architect / game-dev / csharp-engineer / animator / ui-designer / shader-author / tools-engineer / performance-profiler / code-reviewer | 多角色工作室的**轻量落地版**——不必上 49-agent 框架，按需召唤专项代理即可 |
| **godot-prompter 技能库**（~60 个） | 2d-essentials、state-machine、save-load、dialogue-system、export-pipeline、godot-testing、localization、procedural-generation… | 相当于「godot-skills 1.1.0」同类物，已内建 |
| fetch MCP / WebSearch / WebFetch | REST 调用 + 网页抓取 | Gitea/MinIO/GitHub REST 通道 |
| 上下文纪律 | 分块读、子代理隔离、带焦点压缩 | 团队规约已有 |

### 1.3 已跑通的管线（本次建立）

- **每日雷达管线**：cron 触发 → 3 路并行侦察代理 → `daily/YYYY-MM-DD.md` 增量捕获 → commit + push 到 github.com/FuZhouhao/game-ai-research。
- 与团队 Gitea `research_collect.yml`（每周一/周四 RSS/GitHub Trending）互补：本管线是**日更 + 更广域**，团队管线是**周更 + 结构化 PR**。

## 2. 差距分析：research.md 推荐栈 vs 本机实况

| research.md 推荐 | 本机现状 | 判定 | 行动 |
|---|---|---|---|
| MCP 引擎桥（godot-mcp 等） | godot-ai MCP + 9 专项代理 + 60 技能 | ✅ 超出 | 验证编辑器连接，写进规约 §代码阶段 |
| 契约式任务下发 | Gitea 工单模板已有（experiment/settled_feature/research-brief） | ✅ 对齐 | 补「契约字段」：验收命令、触点文件白名单、禁止清单 |
| 多 agent 工作室（49-agent 框架） | 9 个专项代理按需召唤 | 🟡 轻量版够用 | 不引入重型框架；先用专项代理跑一个真实 exp 验证 |
| AI 2D 资产生成（SDXL/Flux 本地） | **无 GPU，无法本地跑扩散模型** | ❌ 硬缺口 | 见 §3.2 资产管线的 CPU-only 现实路径 |
| AI playtest（headless 自动试玩） | godot `--headless` + gdUnit4 式测试可串 | 🟡 可组装 | 用 godot-ai `test_run` + `editor_screenshot` + LLM 截图判读组一个 exp |
| 音频生成管线 | 只有 ffmpeg（处理），无生成 | ❌ 缺口 | 短期走云 API 小样；关注 sfx 生成工具动态（雷达持续追踪） |
| 政策合规（Steam/Itch AI 披露） | 无流程 | ❌ 缺口 | 规约 §发行阶段落一条「AI 披露检查」 |
| 模型选型 | research.md 有总表 | ✅ | 规约引用，不复制 |

## 3. 推荐工作流（按优先级）

### 3.1 情报→实验闭环（最高优先，已具备全部件）

```
每日雷达（本仓库 daily/）
  → 值得验证的情报 → 建 Gitea research-brief 工单（引用 daily 条目 URL）
  → 从 main 切 exp/* 分支（引用 research-brief 编号）
  → 实验沉淀时回填 research-brief 评论「哪些资料真正帮上忙」
```
改动成本≈0，只差执行纪律。**建议把「每日筛 1~3 条建 research-brief」写进每日雷达流程。**

### 3.2 美术资产管线（CPU-only 约束下的现实路径）

本地扩散模型不可行（无 GPU），推荐**「锁定风格 → 云端小批生成 → 本地标准化 → CI 批处理 → 入库」**五段：

1. **风格锁定**：Aseprite 调色板文件（`.gpl`）+ 参考帧模板，作为生成的「契约」输入。
2. **生成**：云 API/在线工具小批出图（每次 ≤20 张，控制成本）；调色板约束优先选支持 palette-conditioning 的工具。
3. **本地标准化**：magick 量化到锁定调色板 + 尺寸归一 → Aseprite `--batch` 精修/切分。
4. **CI 批处理**：Gitea Actions 跑图集打包（free-tex-packer-cli）+ 资产审计，产物进 MinIO。
5. **溯源入库**：每批记录 prompt/工具/模型/日期，存 MinIO `exp-source`（实验期）→ 沉淀时迁 `source-blend`/`source-aseprite`；**生成素材版权状态必须记录**（训练数据来源不明的不进正式资产）。

### 3.3 AI playtest 管线（建议下一个 exp）

```
godot --headless 跑自动试玩脚本（随机输入/脚本输入）
  → 定期 editor_screenshot / 截帧
  → 截图喂 LLM 判读（UI 破损？黑屏？明显卡死？）
  → 输出 qa-report 桶 + Markdown 报告
```
全部件已就位（headless Godot、godot-ai 截图、ffmpeg 截帧），只差一个 exp 分支组装。

### 3.4 代码阶段工作流（专项代理 + 契约下发）

- 任务下发用**契约模板**：目标文件白名单、验收命令（`gdlint` + `godot --headless --script tests/xxx.gd`）、禁止触碰清单。
- 实现按角色召唤专项代理（architect 出方案 → game-dev 实现 → code-reviewer 过一遍 → performance-profiler 只在有性能症状时介入）。
- 编辑器内操作（场景搭建、tilemap、动画）走 godot-ai MCP；**注意需先确认其与 Godot 编辑器的连接机制**，headless CI 内不可用（MCP 是本地调试通道，正式产出走 CI——团队规约 §0.4）。

## 4. 改进建议清单（可执行，按优先级）

| # | 建议 | 成本 | 优先级 |
|---|---|---|---|
| 1 | 每日雷达产出后筛 1~3 条建 Gitea research-brief，闭合情报→实验环 | 低 | ★★★ |
| 2 | 验证 godot-ai MCP 的编辑器连接方式，跑通一次「建场景→截图→读日志」小样 | 低 | ★★★ |
| 3 | 开 exp：AI playtest 管线（§3.3） | 中 | ★★★ |
| 4 | 开 exp：调色板锁定 + 云生成的像素资产五段管线（§3.2）小样 | 中 | ★★ |
| 5 | 把契约式任务下发模板做成 Gitea Issue 模板（experiment.md 加契约字段） | 低 | ★★ |
| 6 | 音频生成工具雷达专题（sfx/music 生成，CPU-only 可用性评估） | 低 | ★★ |
| 7 | AI 披露合规检查清单进规约发行阶段（Steam/Itch 政策持续追踪） | 低 | ★★ |
| 8 | 侦察代理产出中若发现值得安装的新 CLI 工具，先评估内存/热约束再装（预授权已给） | 视工具 | ★ |

## 5. 本文档的迭代机制

- 每日雷达若发现**改变现状判断**的动态（新工具、政策变化、关键仓库大版本），在对应小节追加一行「> 2026-MM-DD 更新：…」，不重写全文。
- 每周 `review/` 沉淀时把已验证的建议从「建议」移入规约正文。
- 规约正文见 [dev-standards-draft.md](dev-standards-draft.md)。
