# game-ai-research｜AI × 游戏开发每日全球动态雷达

> 由 Claude Code 每日任务（cron `23 8 * * *`）驱动：极大范围扫描全世界「AI 在游戏上的应用实践」，把新动态结构化入库，并持续产出工作流推荐与改进建议。

## 仓库结构

| 路径 | 内容 |
|---|---|
| `research.md` | 基线文档：截至 2026-11-25 的全球 AI 游戏开发深度调研（工作流哲学、工具选型总表、全源社区清单、GitHub 宝库、论文与政策） |
| `daily/` | 每日动态捕获：`YYYY-MM-DD.md`，只记基线之后的**增量**，每条附原始 URL + 抓取日期 |
| `design/` | 工作流设计：结合本机工具链（Godot 4.7.2 headless / Blender CLI / Aseprite / Gitea Actions CI）的管线方案草稿 |
| `internal/` | 内部工作笔记：任务状态、检索策略迭代、自动化管线说明 |
| `review/` | 周期回顾：每周从 daily 中人工筛选沉淀的精华与趋势判断 |

## 纪律（与团队规约一致）

- 情报只收**公开可访问**来源；每条笔记必须附原始 URL + 抓取日期。
- 摘要为中文，标注「可借鉴点」面向 2D 像素游戏小团队（Godot 4.7.2 + CPU-only CI）。
- 本仓库只放 Markdown；视频/代码 zip/大文件不入库。
- Claude 产出为草稿，人工评审后才视为定论（人是第一责任人）。

## 相关仓库

- 团队研发规约与行业雷达流程：`game-team-research-pipeline`（Gitea）
- 游戏资产工作流实践：`FuZhouhao/game-asset-workflows`
