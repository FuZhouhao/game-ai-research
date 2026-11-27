# 源文归档｜C2PA：Content Credentials 实施新指南（AI 披露断言）

- **原始 URL**：https://c2pa.org/a-new-implementation-guide-for-content-credentials
- **抓取日期**：2026-11-27（原文发布 2026-07-31；页面标注更新 2026-08-11）
- **类型**：标准组织官方指南
- **发布方**：C2PA（Content provenance and authenticity 标准联盟）
- **关联条目**：daily/2026-11-27.md 条目 12；详尽版 daily/details/2026-11-27-research-content-pipeline.md
- **存档目的**：原文全文存档，防源页失效（link rot）

## 借鉴要点

（以下要点为本团队提炼，细节以文末「原文全文存档」为准。）

**核心机制**：开发者/创作者/平台用 Content Credentials 在防篡改签名清单（signed manifests）里标注 AI 生成、AI 修改、非合成内容。五大板块：

1. **机器可读的 AI 分类**：`digitalSourceType` 字段（源自 IPTC 词表）标明内容是模型全生成 / AI 增强 / 设备拍摄 / 人工编辑。
2. **AI Disclosure 断言**：独立断言类型 `c2pa.ai-disclosure`，记录模型来源（model provenance）、科学领域、人类监督程度（degree of human oversight）——比简单的「AI 生成」布尔标记信息量大得多。
3. **AI 修改的局部化**：Regions of Interest 精确定位受影响区域（图像的某区域、文档的特定段落、音视频的指定片段）。
4. **生成配方留档**：`inputTo` ingredient 断言记录提示词、参考图、种子值与参数。
5. **标准化动作词表**：Actions 断言记录生命周期步骤（如 `c2pa.created`、`c2pa.edited`），每个动作带 AI 使用指示符。

**配套文档**：另有 Content Credentials Deployment Guidance 讲组织落地。

**边界说明（对游戏团队重要）**：本指南覆盖图像、文档、音频、视频——**未提及游戏资产与实时 3D**；游戏资产溯源暂需自行扩展 schema（如 CUT! 复盘的 provenance 时间戳做法，见 sources/2026-11-27-cut-postmortem.md）。

## 原文全文存档

> 以下为 2026-11-27 经 web_reader 提取 的原文正文存档，尽量保留原文结构与措辞；版权仍归原发布方，仅供团队内部研究借鉴，完整原文以上方 URL 为准。

title: A New Implementation Guide for Content Credentials – Coalition for Content Provenance and Authenticity (C2PA)
url: https://c2pa.org/a-new-implementation-guide-for-content-credentials
publishedTime: July 31, 2026

Generative AI systems can now produce photorealistic images, synthetic audio, and convincing video at scale. This capability makes it increasingly important for anyone consuming digital media to be able to understand the extent to which the asset was created or modified by AI. To address the idea of content provenance, the C2PA publishes __Use of Content Credentials to Identify Synthetic and Non-Synthetic Content__, a white paper that clarifies how developers, creators, and platforms can use C2PA's Content Credentials to communicate that information clearly and precisely.

This paper focuses specifically on how Content Credentials can be used to label AI-generated and AI-modified content, as well as non-synthetic content, recorded within tamper-evident, cryptographically signed manifests. Publishing this paper continues the C2PA's deliberate effort to make the open standard both more robust and easier to implement.

The paper addresses five core areas:

- __A machine-readable classification for AI content –__The digitalSourceType field, drawn from the IPTC vocabulary, provides the primary signal for declaring whether an asset was generated entirely by a model, enhanced by AI, captured by a device, or edited by a human.
- __A dedicated AI Disclosure assertion –__The new c2pa.ai-disclosure assertion captures model provenance, scientific domain, and the degree of human oversight, offering transparency well beyond a binary "AI-generated" label.
- __Precise localization of AI modifications –__Using Regions of Interest, Content Credentials can identify exactly which portions of an asset were affected by AI: a region of an image, specific paragraphs in a document, or defined segments of audio and video.
- __Documentation of the generation recipe –__Through inputTo ingredient assertions, the prompts, reference images, seed values, and parameters behind a generation can be recorded as verifiable provenance data.
- __A standardized vocabulary for creation and editing –__Through the Actions assertion, a Content Credential can record each step in an asset's lifecycle using consistent terms such as c2pa.created, c2pa.opened, and c2pa.edited. Because an AI usage indicator can be applied to each individual action, a single file can distinguish a human-created original from a subsequent AI-assisted edit, giving audiences a precise account of when and how AI was involved.

Published alongside the implementation guide is a companion document – Content Credentials Deployment Guidance – that shifts the focus from _how to label AI content_ to _how any organization can adopt Content Credentials in practice._ Written as a practical, non-technical overview for businesses, agencies, publishers, and governments, it walks readers through identifying their role as a producer or validator, choosing tools that attach and preserve credentials by default, and verifying and displaying provenance for their audiences.

As AI-generated and modified content becomes more prevalent, Content Credentials are a dependable foundation for establishing authenticity across every media type. With more than 500 members and over 6,000 affiliates now supporting the standard, the C2PA continues to evolve the Content Credentials specification to keep pace with the dynamic content provenance landscape. The C2PA encourages the technical community to use this publication as a way to provide clarity and standardization of terms for content provenance.

## 存档说明
本文为团队研究存档：上方「原文全文存档」为抓取时点的正文快照（web_reader 工具提取，非逐字节 HTML），「借鉴要点」为本团队提炼；版权归原发布方，仅供团队内部研究借鉴。
