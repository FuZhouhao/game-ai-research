# 源文归档｜PixelBench：像素画创建的 LLM 基准与工具型智能体环境（arXiv 2611.20628）

- **原始 URL**：https://arxiv.org/abs/2611.20628
- **抓取日期**：2026-11-27（论文 v1 提交 2026-11-16）
- **类型**：学术论文摘要页（cs.CV）
- **作者**：Mutian Hong, Jianxuan Yao, Mingkun Yue, Changkai Li, Hower Yang, Haibin Ling
- **许可**：CC BY 4.0
- **关联条目**：daily/2026-11-27.md 条目 1；详尽版 daily/details/2026-11-27-research-content-pipeline.md
- **存档目的**：原文全文存档，防源页失效（link rot）

## 摘录

（以下为 WebFetch 对摘要页的结构化提取要点，非原文全文；完整论文见上方 URL。）

**基准定位**
- PixelBench 把像素画的形式化要求（紧凑分辨率与调色板限制下的可读形体、空间连贯、配色和谐）落成两条任务的评测：text-to-pixel-art 生成 + 指令引导的编辑。
- 同时提供智能体环境：语言模型智能体写代码调用绘图工具来创建/修改像素画，质量由人类与多模态 LLM 裁判双重评判（裁判与人类偏好的一致性经过验证）。

**评测设置**
- 任务：文生像素画 + 指令编辑；智能体在创作环境中以代码调用绘图工具。
- 模型：多语言模型、多配置，跨不同主题与画布尺寸对比（摘要点名 GPT-6 Astra）。

**关键发现**
- GPT-6 Astra 同时拿下最高平均裁判分与最佳平均人类排名——通用语言模型在像素画创作上确有真实潜力。

**开源情况**
- 作者声明开放任务集、全部生成画作、人类排名与裁判协议；摘要页未给出具体代码仓库链接。

## 原文全文存档

> 以下为 2026-11-27 经 web_reader 提取的原文正文存档，尽量保留原文结构与措辞；版权仍归原发布方，仅供团队内部研究借鉴，完整原文以上方 URL 为准。

[2611.20628] PixelBench: Evaluating Language Models for Pixel-Art Creation

Skip to main content
![Image 1: archive](https://static.arxiv.org/static/design-system/latest/logos/arxiv-logo.svg)
Search

Submit
Donate
Log in 

Search arXiv

Press Enter to search · Advanced search

# Computer Science > Computer Vision and Pattern Recognition

__arXiv:2611.20628__ (cs)

[Submitted on 16 Nov 2026]

# Title:PixelBench: Evaluating Language Models for Pixel-Art Creation

Authors:Mutian Hong, Jianxuan Yao, Mingkun Yue, Changkai Li, Hower Yang, Haibin Ling

View a PDF of the paper titled PixelBench: Evaluating Language Models for Pixel-Art Creation, by Mutian Hong and 5 other authors

View PDF
HTML (experimental)
> Abstract:Pixel art is widely used in games and digital content creation, requiring readable forms, coherent spatial relationships, and harmonious colors under limited resolution and palette constraints. Language models show growing promise in visual creation, yet their pixel art creation capabilities lack systematic evaluation. We introduce PixelBench, formalizing text-to-image generation and instruction-guided editing for pixel art and providing a benchmark for these tasks. We further present a creation environment in which language model agents invoke drawing tools through code to generate and edit pixel art. We assess the quality of generated artwork through human evaluation and employ a multimodal large language model as a judge, validating the agreement between its automated assessments and human preferences. We compare language models and configurations across diverse subjects and canvas sizes. In our experiments, GPT-6 Astra achieves both the highest average judge score and the best average human rank, highlighting the potential of general-purpose language models for pixel art creation. We release the tasks, all artworks, the human rankings, and the judge protocol.

|  |  |
| --- | --- |
| Comments: | 38 pages, 12 figures, 11 tables |
| Subjects: | Computer Vision and Pattern Recognition (cs.CV) |
| Cite as: | arXiv:2611.20628 [cs.CV] |
|  | (or  arXiv:2611.20628v1 [cs.CV] for this version) |
|  | https://doi.org/10.48550/arXiv.2611.20628 Focus to learn more  arXiv-issued DOI via DataCite (pending registration) |

## Submission history

From: Mutian Hong [view email]   
 __[v1]__
Mon, 16 Nov 2026 06:51:56 UTC (9,423 KB)

Full-text links:

## Access Paper:

View a PDF of the paper titled PixelBench: Evaluating Language Models for Pixel-Art Creation, by Mutian Hong and 5 other authors

- View PDF
- HTML (experimental)
- TeX Source

![Image 2: license icon](https://arxiv.org/icons/licenses/by-4.0.png)
view license

### Additional Features

- Audio Summary

### Current browse context:

cs.CV

< prev
  |   
next >

new
 | 
recent
 | 2026-11

Change to browse by:

cs

### References & Citations

- SciX
- Google Scholar
- Semantic Scholar

export BibTeX citation

Loading...

## BibTeX formatted citation

×

loading...

Data provided by:

### Bookmark

![Image 3: BibSonomy](https://arxiv.org/static/browse/0.3.4/images/icons/social/bibsonomy.png)
![Image 4: Reddit](https://arxiv.org/static/browse/0.3.4/images/icons/social/reddit.png)

Bibliographic Tools

# Bibliographic and Citation Tools

Bibliographic Explorer Toggle

Bibliographic Explorer _(What is the Explorer?)_

Connected Papers Toggle

Connected Papers _(What is Connected Papers?)_

Litmaps Toggle

Litmaps _(What is Litmaps?)_

scite.ai Toggle

scite Smart Citations _(What are Smart Citations?)_

Code, Data, Media

# Code, Data and Media Associated with this Article

alphaXiv Toggle

alphaXiv _(What is alphaXiv?)_

Links to Code Toggle

CatalyzeX Code Finder for Papers _(What is CatalyzeX?)_

DagsHub Toggle

DagsHub _(What is DagsHub?)_

GotitPub Toggle

Gotit.pub _(What is GotitPub?)_

Huggingface Toggle

Hugging Face _(What is Huggingface?)_

ScienceCast Toggle

ScienceCast _(What is ScienceCast?)_

Demos

# Demos

Replicate Toggle

Replicate _(What is Replicate?)_

Spaces Toggle

Hugging Face Spaces _(What is Spaces?)_

Spaces Toggle

TXYZ.AI _(What is TXYZ.AI?)_

Related Papers

# Recommenders and Search Tools

Link to Influence Flower

Influence Flower _(What are Influence Flowers?)_

Core recommender toggle

CORE Recommender _(What is CORE?)_

- Author
- Venue
- Institution
- Topic

About arXivLabs

# arXivLabs: experimental projects with community collaborators

arXivLabs is a framework that allows collaborators to develop and share new arXiv features directly on our website.

Both individuals and organizations that work with arXiv have embraced and accepted our values of openness, community, excellence, and user data privacy. arXiv is committed to these values and only works with partners that adhere to them.

Have an idea for a project that will add value for arXiv's community? __Learn more about arXivLabs__.

Which authors of this paper are endorsers? |
Disable MathJax (What is MathJax?)

We gratefully acknowledge support from our __major funders__,
__member institutions__, ,
and all contributors.

About ·
Help ·
Contact ·
Subscribe ·
Copyright ·
Privacy ·
Accessibility ·
Operational Status (opens in new tab)

## 存档说明
本文为团队研究存档：上方「原文全文存档」为抓取时点的正文快照（工具提取，非逐字节 HTML），「借鉴要点」为本团队提炼；版权归原发布方，仅供团队内部研究借鉴。
