# Wiki — LLM 驱动的投资研究知识库

> 基于 Andrej Karpathy 的 Wiki 模式构建的持久化知识库，用于 A 股投资研究与产业链高频监控。

---

## 📖 项目简介

### 核心理念

**不是 RAG 检索，而是 LLM 持续维护的结构化知识体系。**

传统 RAG 方案在每次查询时临时检索片段，知识无法沉淀。本 Wiki 采用 Karpathy 提出的模式：让 LLM 持续编译、维护一套结构化的 Markdown 文件。知识**编译一次、持续复用**，每次查询都是在已有的知识网络上叠加新的认知。

### 主要用途

- 📊 **A 股投资研究** — 持仓标的深度跟踪、基本面分析
- 🏭 **产业链监控** — 四维三层高频数据追踪（周度/月度更新）
- 📈 **个股深度分析** — 业务拆分、投资逻辑演进、竞争对手对比
- 📋 **政策研报解读** — 结构化沉淀到实体页面和分析报告

---

## 🌟 核心特性

| 特性 | 说明 |
|------|------|
| **三层架构** | `raw/`原始资料（只读）→ `wiki/`知识库（LLM 维护）→ `schema.md`规范 |
| **实体驱动** | 个股、板块、指标、概念、人物 —— 所有投资要素都有独立页面 |
| **交叉引用** | 页面间通过双向链接形成知识网络，支持深度遍历 |
| **操作可追溯** | `log.md`记录每一次录入/查询/检查，支持审计与回滚 |
| **LLM 全权维护** | 三个核心技能（Ingest/Query/Lint）覆盖完整工作流 |

---

## 📁 目录结构

```
wiki/
├── raw/                    # 原始资料库（只读层，LLM 不修改）
│   ├── reports/            # 券商研报、行研报告
│   ├── articles/           # 公众号、媒体文章
│   ├── filings/            # 年报/季报、公司公告
│   ├── policies/           # 政策文件
│   ├── data/               # 原始数据（CSV/Excel）
│   ├── notes/              # 手记、复盘笔记
│   └── assets/             # 图片、附件
│
├── wiki/                   # 知识库（LLM 全权维护）
│   ├── schema.md           # ⬅️ 规范文档（"宪法"，操作前必读）
│   ├── index.md            # 全局索引（精简导航入口）
│   ├── log.md              # 操作日志（只追加不修改）
│   │
│   ├── entities/           # 实体页面（具体的"东西"）
│   │   ├── _index-stocks.md      # 个股子索引（39 家公司）
│   │   ├── _index-sectors.md     # 板块子索引（5 个行业）
│   │   ├── _index-indicators.md  # 指标子索引（4 个高频数据）
│   │   ├── stocks/               # 个股页面：贵州茅台、宁德时代、阳光电源...
│   │   ├── sectors/              # 板块页面：AI 算力、光伏、新能源汽车...
│   │   ├── indicators/           # 指标页面：DRAM 合约价、碳酸锂价格...
│   │   └── people/               # 人物页面（待扩展）
│   │
│   ├── concepts/           # 概念页面（抽象的"想法"）
│   │   ├── _index-concepts.md      # 概念子索引
│   │   ├── frameworks/             # 分析框架：四维三层监控体系、杠铃策略...
│   │   ├── themes/                 # 投资主题：核心 - 卫星配置...
│   │   └── technologies/           # 关键技术：HBM 高带宽内存...
│   │
│   ├── analyses/           # 分析产出
│   │   ├── _index-analyses.md      # 分析子索引
│   │   ├── comparisons/            # 对比分析（待扩展）
│   │   ├── deep-dives/             # 深度专题（待扩展）
│   │   └── reviews/                # 复盘笔记：产业链周报、组合分析...
│   │
│   └── meta/               # 元信息
│       ├── reading-list.md       # 待读清单
│       ├── open-questions.md     # 未解问题（17 条）
│       └── contradictions.md     # 矛盾记录
│
├── .claude/
│   └── skills/             # 核心工作流技能定义
│       ├── wiki-ingest.md      # 资料录入操作
│       ├── wiki-query.md       # 知识查询操作
│       └── wiki-lint.md        # 健康检查操作
│
├── CLAUDE.md               # 项目配置与工作规范
└── README.md               # 本文件
```

---

## 🛠️ 三种核心操作

用户通过自然语言触发以下操作，系统自动读取 `.claude/skills/` 下对应的技能文件执行：

| 用户说 | 技能 | 做什么 | 输出 |
|--------|------|--------|------|
| **"录入 xxx"** | `wiki-ingest.md` | 阅读 `raw/` 资料 → 创建/更新 Wiki 页面 → 更新索引 + 日志 | 5-15 个页面更新 + 分析摘要页 |
| **"查询 / 问一下 / 对比"** | `wiki-query.md` | 查索引定位 → 深入阅读 → 综合作答 → 引用来源 | 直接回答 或 Markdown 报告 |
| **"检查 / lint / 体检"** | `wiki-lint.md` | 7 项健康检查 → 出报告 → 自动修复能修的 | `lint-report-YYYY-MM-DD.md` |

### 操作示例

```bash
# 录入操作
"录入 raw/reports/最新研报.md"
→ LLM 阅读理解 → 创建/更新相关实体页 → 生成分析摘要 → 提交 git

# 查询操作
"对比一下阳光电源和宁德时代的业务结构"
→ 查索引定位 → 阅读两个公司页面 → 综合对比 → 输出表格

# 检查操作
"给 Wiki 做个体检"
→ 7 项检查（矛盾/过时/孤岛/缺失/断链/空白/合规）→ 输出报告
```

---

## 📊 当前规模

| 类型 | 数量 | 说明 |
|------|------|------|
| 原始资料 | 6+ | 研报、文章、公告、数据文件 |
| Wiki 页面 | 71+ | 持续更新中 |
| 个股覆盖 | 39 | 持仓标的 + 产业链核心公司 |
| 板块覆盖 | 5 | AI 算力、光伏、新能源汽车、存储芯片、有色金属 |
| 高频指标 | 4 | DRAM 合约价、碳酸锂价格、硅料价格、LME 铜价 |
| 概念框架 | 13 | 分析框架、投资主题、关键技术 |
| 分析产出 | 10+ | 产业链周报、组合分析、策略报告 |

---

## 🔗 页面类型与模板

### 1. 个股实体页 (`entities/stocks/{股票名}.md`)

```yaml
---
title: 股票名称
type: stock
code: XXXXXX.SH/SZ
sector: 所属板块
tags: [标签 1, 标签 2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
status: active | watching | archived
---
```

**核心章节**：一句话定位、核心基本面（PE/ROE/毛利率）、业务拆分、投资逻辑演进、关联链接

### 2. 板块实体页 (`entities/sectors/{板块名}.md`)

```yaml
---
title: 板块名称
type: sector
tags: [标签]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
status: active
---
```

**核心章节**：一句话定位、产业链结构（上游→中游→下游）、龙头梯队、高频指标追踪、催化/风险

### 3. 指标实体页 (`entities/indicators/{指标名}.md`)

```yaml
---
title: 指标名称
type: indicator
category: 价格 | 开工率 | 出货量 | 库存 | 宏观
unit: 单位
frequency: 日度 | 周度 | 月度 | 季度
source: 数据来源说明
---
```

**核心章节**：定义说明、数据趋势表（日期/数值/环比/同比）、投资含义、关联关系

### 4. 概念页 (`concepts/{frameworks,themes,technologies}/{名称}.md`)

```yaml
---
title: 名称
type: framework | theme | theory
tags: [标签]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
---
```

**核心章节**：核心思想、要点拆解、应用案例、局限性

### 5. 分析产出页 (`analyses/{reviews,comparisons,deep-dives}/{标题}.md`)

```yaml
---
title: 分析标题
type: comparison | deep-dive | review
date: YYYY-MM-DD
related_entities: [entity1, entity2]
related_concepts: [concept1]
tags: []
---
```

**核心章节**：背景、核心发现、结论与行动建议、引用来源

---

## 📜 工作规范

### 基本原则

1. **先读 schema.md** — 所有操作前必须先读取规范文档
2. **绝不修改 raw/** — 原始资料是只读层
3. **每次 Ingest/Lint 后 git commit** — 保持版本可追溯
4. **log.md 只追加不修改** — 固定前缀格式：`## [YYYY-MM-DD] {操作类型} | {标题}`
5. **不确定就问用户** — 尤其是对矛盾信息的判断
6. **有价值的 Query 结果要写回 Wiki** — 不让好想法消失在聊天中

### Git 提交规范

```bash
# Commit message 格式
ingest: {日期} | {资料简短标题}
query: {日期} | {问题摘要} → 产出：{文件}
lint: {日期} | {模式} — 发现 N 个问题，修复 M 个
refactor: {描述}
```

---

## 🔍 索引架构设计

### 分类拆分设计

总入口 `index.md` 保持精简（< 50 行），详细条目在各子索引中：

```
index.md (精简总入口，仅分类导航 + 元信息概览)
├── entities/_index-stocks.md      (个股索引)
├── entities/_index-sectors.md     (板块索引)
├── entities/_index-indicators.md  (指标索引)
├── concepts/_index-concepts.md    (概念索引)
└── analyses/_index-analyses.md    (分析索引)
```

### 规模扩展预案

| 页面总数 | 索引策略 |
|---------|---------|
| 0-200 | 子索引单文件即可 |
| 200-500 | 按首字母或时间拆分子索引 |
| 500+ | 引入搜索引擎，索引退化辅助浏览 |

---

## 📈 健康检查（7 项）

定期执行 Lint 检查，确保知识库质量：

| # | 检查项 | 操作 |
|---|-------|------|
| 1 | **矛盾检测** | 扫描所有页面，找出相互冲突的陈述 |
| 2 | **过时内容** | 标注被新资料推翻或已过期的旧说法 |
| 3 | **孤岛页面** | 找出没有任何入链的孤立页面 |
| 4 | **缺失实体** | 找出被多次提及但无独立页面的概念 |
| 5 | **引用断裂** | 检查所有链接是否指向存在的页面 |
| 6 | **信息空白** | 识别可以通过网络搜索填补的信息缺口 |
| 7 | **扩展建议** | 推荐值得深入研究的新方向和新资料 |

---

## 🚀 快速开始

### 前置条件

- Claude Code / Anthropic SDK 环境
- Git 配置完成
- 读取 `CLAUDE.md` 和 `wiki/schema.md`

### 第一次录入资料

1. 将原始资料放入 `raw/` 对应子目录
2. 告知 LLM：`"录入 raw/reports/xxx.md"`
3. LLM 自动执行：
   - 阅读理解资料
   - 创建/更新相关页面
   - 更新索引和日志
   - 提交 git

### 查询已有知识

直接提问即可：
- `"阳光电源的业务拆分是什么？"`
- `"对比一下光伏和 AI 算力板块的景气度"`
- `"HBM 相关的 A 股公司有哪些？"`

---

## 📚 相关资源

- [CLAUDE.md](CLAUDE.md) — 项目配置与工作规范
- [wiki/schema.md](wiki/schema.md) — 页面模板与命名约定
- [wiki/index.md](wiki/index.md) — 全局索引导航
- [.claude/skills/](.claude/skills/) — 核心工作流技能定义

---

*基于 Andrej Karpathy 的 Wiki 模式构建 | 最后更新：2026-04-16*
