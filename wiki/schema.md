# Wiki Schema 规范文档

> **版本**：v2.1.0（合并版）
> **最后更新**：2026-04-21
> **定位**：本文件是 LLM 操作 Wiki 时的「工作协议」。每次觉得不好用就改它。
> **覆盖范围**：投资研究 + 全领域个人知识库。

---

## 一、目录结构与命名约定

### 1.1 顶层结构

```
my-wiki/
├── raw/                    # 第一层：原始资料库（只读）
│   ├── reports/            # 研报
│   ├── articles/           # 文章
│   ├── filings/            # 公告文件
│   ├── policies/           # 政策文件
│   ├── data/               # 数据文件
│   ├── notes/              # 手记
│   ├── market/             # 行情分析
│   ├── books/              # 书籍（电子书、PDF）
│   ├── courses/            # 课程材料
│   └── assets/             # 图片附件
│
├── wiki/                   # 第二层：知识库（LLM 全权管理）
│   ├── index.md            # 全局索引
│   ├── log.md              # 操作日志（只追加）
│   ├── schema.md           # 本文件
│   ├── entities/           # 实体页面
│   │   ├── stocks/         # 个股
│   │   ├── sectors/        # 板块
│   │   ├── indicators/     # 指标
│   │   ├── people/         # 人物
│   │   ├── books/          # 书籍
│   │   ├── tools/          # 工具/软件
│   │   └── orgs/           # 机构/组织
│   ├── concepts/           # 概念页面
│   │   ├── frameworks/     # 分析框架
│   │   ├── themes/         # 投资主题
│   │   ├── theories/       # 理论模型
│   │   ├── methods/        # 方法论
│   │   ├── definitions/    # 术语定义
│   │   └── technologies/   # 关键技术
│   ├── analyses/           # 分析产出
│   │   ├── comparisons/    # 对比分析
│   │   ├── deep-dives/     # 深度专题
│   │   ├── reviews/        # 复盘笔记
│   │   ├── book-notes/     # 读书笔记
│   │   ├── course-notes/   # 课程笔记
│   │   ├── essays/         # 随笔/个人思考
│   │   └── industries/     # 行业分析
│   └── meta/               # 元信息
│
└── .git/                   # 版本控制
```

### 1.2 命名规则

| 规则 | 说明 | 示例 |
|------|------|------|
| 个股页面 | 公司全名.md | `澜起科技.md`、`阳光电源.md` |
| 板块页面 | 板块名.md | `AI算力.md`、`光伏.md` |
| 人物页面 | 姓名.md | `张三.md` |
| 指标页面 | 指标名.md | `硅料价格.md`、`开工率.md` |
| 书籍页面 | 《书名》.md | `《芯片战争》.md` |
| 工具页面 | 工具名.md | `Obsidian.md`、`Claude Code.md` |
| 机构页面 | 机构全名.md | `台积电.md`、`深交所.md` |
| 框架页面 | 框架名.md | `张新民五维分析法.md` |
| 主题页面 | 主题名.md | `AI-A股.md` |
| 理论页面 | 理论名.md | `库存周期.md`、`康波周期.md` |
| 方法论页面 | 方法论名.md | `费曼学习法.md` |
| 术语定义 | 术语名.md | `CXL.md`、`DDR5.md` |
| 复盘笔记 | YYYY-MM-DD.md | `2026-04-14.md` |
| 对比分析 | A-vs-B.md | `澜起科技 -vs- 聚辰股份.md` |
| 深度报告 | 主题 -YYYYMM.md | `ai 算力 202604.md` |
| 读书笔记 | 《书名》-笔记.md | `《芯片战争》-笔记.md` |
| 课程笔记 | 课程名 - 第 X 周.md | `机器学习 - 第 3 周.md` |
| 随笔 | 标题.md | `为什么我看好算力租赁.md` |
| 行业分析 | 行业名_日期.md | `白酒行业困境与反转_20260416.md` |

### 1.3 文件放置规则

- **一个概念只对应一个页面**。如果页面已存在，执行更新而非新建。
- **个股页面** → `wiki/entities/stocks/`
- **板块页面** → `wiki/entities/sectors/`
- **人物页面** → `wiki/entities/people/`
- **指标页面** → `wiki/entities/indicators/`
- **书籍页面** → `wiki/entities/books/`
- **工具页面** → `wiki/entities/tools/`
- **机构页面** → `wiki/entities/orgs/`
- **分析框架** → `wiki/concepts/frameworks/`
- **投资主题** → `wiki/concepts/themes/`
- **理论模型** → `wiki/concepts/theories/`
- **方法论** → `wiki/concepts/methods/`
- **术语定义** → `wiki/concepts/definitions/`
- **关键技术** → `wiki/concepts/technologies/`
- **对比分析** → `wiki/analyses/comparisons/`
- **深度报告** → `wiki/analyses/deep-dives/`
- **复盘笔记** → `wiki/analyses/reviews/`
- **读书笔记** → `wiki/analyses/book-notes/`
- **课程笔记** → `wiki/analyses/course-notes/`
- **随笔思考** → `wiki/analyses/essays/`
- **行业分析** → `wiki/analyses/industries/`

---

## 二、页面模板

### 2.1 个股页面模板

```markdown
---
title: {公司全名}
type: stock
code: {股票代码。SH/SZ}
sector: {所属板块}
tags: [{标签 1}, {标签 2}, ...]
created: {创建日期}
updated: {最后更新日期}
sources: {基于多少份原始资料}
status: active  # active / archived / watching
---

# {公司全名} ({股票代码})

## 一句话定位
{用一句话概括公司的核心竞争力和投资价值}

## 核心基本面

| 指标 | 最新值 | 数据日期 | 趋势 |
|-----|-------|---------|------|
| PE(TTM) | | | |
| ROE | | | |
| 营收增速 | | | |
| 净利润增速 | | | |

## 业务拆分

### {业务线 1}（收入占比 XX%）
- 关键信息...
- **关键指标追踪**：[指标名](../indicators/指标名.md)

### {业务线 2}（收入占比 XX%）
- ...

## 投资逻辑演进

> 记录认知变化过程，带时间戳

1. **[YYYY-MM-DD]** {初始/更新逻辑}
2. **[YYYY-MM-DD]** {认知变化}

## 关联链接

- 所属板块：[{板块名}](../sectors/板块名.md)
- 竞争对手：[{公司名}](公司名.md)
- 相关概念：[{概念名}](../../concepts/类别/概念名.md)
- 分析框架：应用了 [{框架名}](../../concepts/frameworks/框架名.md)

## 资料来源
1. raw/{子目录}/{文件名}
2. ...
```

### 2.2 板块页面模板

```markdown
---
title: {板块名称}
type: sector
tags: [{标签 1}, {标签 2}]
created: {创建日期}
updated: {最后更新日期}
---

# {板块名称}

## 一句话定位
{板块的核心逻辑和投资主线}

## 产业链图谱

{用文字描述产业链上下游关系}

```
上游 → 中游 → 下游
原料 → 制造 → 应用
```

## 梯队分析

### 第一梯队
- [{公司A}](../stocks/公司A.md) — {一句话说明}
- [{公司 B}](../stocks/公司B.md) — {一句话说明}

### 第二梯队
- ...

### 第三梯队（弹性标的）
- ...

## 核心指标追踪

| 指标 | 最新值 | 趋势 | 追踪链接 |
|-----|-------|------|---------|
| | | | |

## 关联链接

- 相关主题：[{主题名}](../../concepts/themes/主题名.md)
- 相关理论：[{理论名}](../../concepts/theories/理论名.md)
```

### 2.3 概念页面模板

```markdown
---
title: {概念名称}
type: {framework / theme / theory / method / definition / technology}
tags: [{标签 1}]
created: {创建日期}
updated: {最后更新日期}
---

# {概念名称}

## 定义
{清晰的概念定义}

## 核心内容
{详细展开}

## 应用场景
- 在哪些个股/板块分析中用到
- 与其他概念的关系

## 关联链接
- 相关个股：[{公司名}](../../entities/stocks/公司名.md)
- 相关板块：[{板块名}](../../entities/sectors/板块名.md)
```

### 2.4 复盘笔记模板

```markdown
---
title: A 股复盘 {日期}
type: review
date: {YYYY-MM-DD}
created: {创建日期}
---

# A 股复盘 {YYYY-MM-DD}

## 大盘概况

| 指标 | 数值 | 涨跌 |
|-----|------|------|
| 上证指数 | | |
| 深证成指 | | |
| 创业板指 | | |
| 成交额 | | |

## 板块表现

**领涨板块**：
- 

**领跌板块**：
- 

## 持仓关注

| 个股 | 收盘价 | 涨跌幅 | 值得关注的变化 |
|-----|-------|--------|--------------|
| | | | |

## 市场情绪与观点

{今日市场主要矛盾、资金动向、政策信号}

## 明日关注

- 
```

### 2.5 对比分析模板

```markdown
---
title: {A} vs {B}
type: comparison
created: {创建日期}
updated: {最后更新日期}
stocks: [{代码 A}, {代码 B}]
---

# {A} vs {B}

## 对比背景
{为什么要对比这两者}

## 核心指标对比

| 维度 | {A} | {B} |
|-----|-----|-----|
| 市值 | | |
| PE | | |
| ROE | | |
| 营收增速 | | |
| 业务布局 | | |

## 核心差异分析

### {A}的优势/风险
- 

### {B}的优势/风险
- 

## 结论

{对比后的判断}
```

### 2.6 书籍页面模板

```markdown
---
title: 《{书名}》
type: book
author: {作者}
category: {投资/技术/科学/人文/商业/其他}
tags: [{标签 1}, {标签 2}]
rating: ⭐⭐⭐⭐☆
status: reading  # reading / finished / archived
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 1
---

# 《{书名}》

## 一句话总结
{这本书讲了什么}

## 核心观点
1. ...
2. ...

## 关键概念提取
- [[{概念 A}]] → {一句话说明}
- [[{概念 B}]] → {一句话说明}

## 章节笔记
（简述或链接到 analyses/book-notes/ 下的详细笔记）

## 与我已有知识的关联
- 与 [[{已有页面}]] 的关系：...
- 启发：...

## 资料来源
1. raw/books/{文件名}
```

### 2.7 工具页面模板

```markdown
---
title: {工具名}
type: tool
category: {AI 工具/开发工具/投资工具/效率工具/其他}
tags: [{标签}]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# {工具名}

## 一句话定位
{这个工具是干什么的}

## 核心功能
- ...

## 使用场景
- 与 [[{Wiki 页面}]] 结合使用：...
- ...

## 关联链接
```

### 2.8 读书笔记模板

```markdown
---
title: 《{书名}》读书笔记
type: book-note
book: 《{书名}》
date: YYYY-MM-DD
created: YYYY-MM-DD
---

# 《{书名}》读书笔记

## 阅读进度
- 章节：第 X 章 / 共 Y 章

## 核心收获
1. ...

## 精彩摘录
> "{原文引用}"

## 我的思考
{与已有知识的关联、启发}

## 行动项
- [ ] ...
```

### 2.9 课程笔记模板

```markdown
---
title: {课程名} - 第{N}周笔记
type: course-note
course: {课程名}
date: YYYY-MM-DD
created: YYYY-MM-DD
---

# {课程名} — 第{N}周笔记

## 核心概念
- [[{概念}]] → {解释}

## 关键公式/代码
```

## 我的理解
{用自己的话重新表述}

## 与已有知识的关联
- 与 [[{Wiki 页面}]] 的关系：...
```

### 2.10 随笔模板

```markdown
---
title: {标题}
type: essay
tags: [{标签}]
created: YYYY-MM-DD
---

# {标题}

## 想法
{自由书写}

## 关联
- 引用了 [[{概念/页面}]]
- 可能影响 [[{个股/板块}]]
```

### 2.11 行业分析模板

```markdown
---
title: {行业名}
type: industry
date: YYYY-MM-DD
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# {行业名}

## 核心观点
{用一句话概括行业的核心投资逻辑}

## 行业概况
{行业基本情况、市场规模、竞争格局}

## 关键驱动因素
1. 
2. 
3. 

## 重点公司
| 公司 | 代码 | 定位 |
|------|------|------|
| | | |

## 风险因素
- 

## 关联链接
- 相关板块：[[{板块名}]]
- 相关个股：[[{公司名}]]
```

---

## 三、录入工作流 (Ingest)

当用户要求录入新资料时，按以下步骤执行：

### Step 1：确认资料
- 读取用户指定的 `raw/{子目录}/{文件名}`
- 如果文件不存在或无法读取，报告错误

### Step 2：提取关键信息
- 阅读资料全文，提取：
  - 涉及的个股/板块/人物/指标
  - 核心观点和数据
  - 与已有 Wiki 页面的关联

### Step 3：创建/更新页面
- 对每个识别出的实体/概念：
  - 如果页面已存在 → 更新内容（追加新信息，标注来源和日期）
  - 如果页面不存在 → 按对应模板创建新页面
- 更新关联链接

### Step 4：更新索引和日志
- 在 `wiki/index.md` 中添加/更新对应条目
- 更新「最后更新」日期和计数
- 在 `wiki/log.md` 追加操作记录

### Step 5：检查矛盾
- 将新信息与已有页面内容比对
- 如果发现矛盾 → 记录到 `wiki/meta/contradictions.md`

### 一份资料的典型影响范围
- 可能涉及 5-15 个 Wiki 页面的创建或更新
- 始终更新 index.md 和 log.md

---

## 四、查询工作流 (Query)

当用户提出问题时，按以下步骤响应：

### Step 1：定位相关页面
- 先读 `wiki/index.md` 找到相关条目
- 深入阅读相关实体/概念页面

### Step 2：综合回答
- 基于现有 Wiki 内容回答
- **必须引用具体页面链接**作为来源
- 标注信息的时效性

### Step 3：输出形式（按需）
- 直接回答（聊天中）
- Markdown 页面（写回 wiki）
- 对比表格
- 图表/可视化

### Step 4：留存判断
- 有价值的新发现 → 建议用户保存为 Wiki 新页面
- 对比/综合分析 → 写入 `wiki/analyses/` 对应子目录

---

## 五、生成工作流 (Generate)

> 不同于 Ingest（从本地资料提取）和 Query（查询已有内容），
> Generate 从 **Wiki 已有认知 + 外部实时数据** 主动生成新内容并写回 Wiki。

### 五种生成类型

| 类型 | 触发 | 输出路径 |
|------|------|---------|
| 复盘生成 | "做今天复盘" | `analyses/reviews/YYYY-MM-DD.md` |
| 数据刷新 | "更新澜起科技基本面" | 更新已有 `entities/stocks/*.md` |
| 专题生成 | "写一份 AI算力展望" | `analyses/deep-dives/{主题}.md` |
| 对比生成 | "对比澜起和聚辰" | `analyses/comparisons/A-vs-B.md` |
| 指标追踪 | "更新硅料价格数据" | 更新已有 `entities/indicators/*.md` |

### 通用流程

1. **读 Wiki** — 读 index.md + 相关已有页面
2. **拉外部数据** — 调用金融数据 API / 网络搜索获取最新信息
3. **综合生成** — Wiki 认知 + 外部数据 → 按模板格式组织
4. **写入 Wiki** — 新建/更新页面，标注数据来源和日期
5. **更新索引 + 日志** — index.md / log.md 追加
6. **Git 提交** — `generate: {日期} | {类型} | {简述}`

### 外部数据标注规则

所有外部数据在 Wiki 中必须标注：
- 数据来源（API 名称 / 网络来源）
- 数据日期（精确到日）
- 与上次数据的变化

> 详细操作步骤见 `.claude/skills/wiki-generate.md`

---

## 六、检查工作流 (Lint)

定期执行以下排查项目：

| 检查项 | 说明 | 处理方式 |
|-------|------|---------|
| 矛盾检测 | 不同页面的说法是否冲突 | 记录到 contradictions.md |
| 过时内容 | 是否有被新资料推翻的旧观点 | 标注 [待更新] |
| 孤岛页面 | 没有任何入链的孤立页面 | 添加链接或标注 |
| 缺失实体 | 被多次提及但没有独立页面 | 创建占位页面 |
| 引用断裂 | 链接指向不存在的页面 | 修复或移除 |
| 信息空白 | 可以补充的信息缺口 | 记录到 open-questions.md |

**输出**：检查报告保存到 `wiki/meta/lint-report-{日期}.md`
**原则**：能自动修复的直接修复，需人工判断的标记为 [待确认]

---

## 七、重要约定

1. **raw/ 只读**：LLM 不修改 `raw/` 下的任何文件
2. **log.md 只追加**：日志只追加新条目，不修改旧记录
3. **schema.md 协作修改**：Schema 只在用户确认后修改，LLM 不自作主张
4. **链接使用相对路径**：方便整体移动和跨工具兼容
5. **每次操作后 Git 提交**：`git add -A && git commit -m "{操作类型}: {简述}"`
6. **Obsidian 兼容**：使用 `[[双链]]` 和标准 Markdown 格式

---

*本文件会在使用过程中持续迭代完善。*
