# Schema — Wiki 规范文档

> 这是本知识库的"宪法"。LLM 在执行任何操作（录入/查询/检查）时都必须遵循此规范。
> 此文档会随着使用不断迭代更新。

---

## 1. 系统概述

本 Wiki 是一个**投资研究知识库**，采用 Andrej Karpathy 提出的"LLM 驱动的持久化 Wiki"模式构建。
核心场景：A股投资研究、产业链高频监控、个股深度追踪、政策研读。

### 三层架构

| 层级 | 路径 | 说明 | 权限 |
|-----|------|------|------|
| 原始资料库 | `raw/` | 研报、文章、公告、政策等原始文档 | 只读（LLM不修改） |
| 知识库 | `wiki/` | LLM 生成的结构化 Markdown 文件 | LLM全权负责 |
| Schema | `wiki/schema.md` | 本文档 — 约定与工作流规范 | 人机共同维护 |

---

## 2. 目录结构

```
my-wiki/
├── raw/                           # 原始资料（只读）
│   ├── reports/                   # 券商/行研报告
│   ├── articles/                  # 公众号/媒体文章
│   ├── filings/                   # 年报/季报/公告
│   ├── policies/                  # 政策文件
│   ├── data/                      # 原始数据(CSV/Excel)
│   ├── notes/                     # 手记/思考碎片
│   └── assets/                    # 图片附件
│
├── wiki/                          # 知识库（LLM维护）
│   ├── schema.md                  # ⬅ 你正在阅读的这个文件
│   ├── index.md                   # 全局索引
│   ├── log.md                     # 操作日志
│   │
│   ├── entities/                  # 实体页面（具体的"东西"）
│   │   ├── stocks/                # 个股页面
│   │   ├── sectors/               # 板块页面
│   │   ├── people/                # 人物页面
│   │   └── indicators/            # 指标页面
│   │
│   ├── concepts/                  # 概念页面（抽象的"想法"）
│   │   ├── frameworks/            # 分析框架/方法论
│   │   ├── themes/                # 投资主题
│   │   └── theories/              # 理论模型
│   │
│   ├── analyses/                  # 分析产出
│   │   ├── comparisons/           # 对比分析
│   │   ├── deep-dives/            # 深度专题
│   │   └── reviews/               # 复盘笔记(按日期归档)
│   │
│   └── meta/                      # 元信息
│       ├── reading-list.md        # 待读清单
│       ├── open-questions.md      # 未解问题
│       └── contradictions.md      # 矛盾记录
│
└── .git/
```

---

## 3. 页面模板

### 3.1 个股实体页 (`wiki/entities/stocks/{股票名}.md`)

```markdown
---
title: 股票名称
type: stock
code: XXXXXX.SH/SZ
sector: 所属板块
tags: [标签1, 标签2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
status: active | archived | watching
---

# {股票名称} ({code})

## 一句话定位
用一句话概括这家公司的投资价值。

## 核心基本面

| 指标 | 最新值 | 数据日期 | 趋势 |
|-----|-------|---------|------|
| PE(TTM) | | | |
| ROE | | | |
| 毛利率 | | | |

## 业务拆分
### 业务线1（收入占比XX%）
- 描述
- **关键指标链接**: [指标名](../indicators/xxx.md)

### 业务线2（收入占比XX%）
- ...

## 投资逻辑演进
> 按时间倒序记录认知变化过程

1. **[YYYY-MM-DD]** 变化说明
2. **[YYYY-MM-DD]** 变化说明

## 关联链接
- 所属板块：[板块名](../sectors/xxx.md)
- 竞争对手：[公司名](xxx.md)
- 相关概念：[概念名](../../concepts/xxx.md)
- 分析框架：[框架名](../../concepts/frameworks/xxx.md)

## 资料来源
1. raw/...
2. raw/...
```

### 3.2 板块实体页 (`wiki/entities/sectors/{板块名}.md`)

```markdown
---
title: 板块名称
type: sector
tags: [标签1, 标签2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
status: active
---

# {板块名称}

## 一句话定位
一句话概括该板块的核心投资逻辑。

## 产业链结构
上游 → 中游 → 下游，标注关键环节和相关个股。

## 龙头梯队
| 梯队 | 公司 | 代码 | 定位 |
|------|------|------|------|
| 一梯队 | | | |
| 二梯队 | | | |

## 高频指标追踪
| 指标 | 最新值 | 更新日期 | 趋势意义 |
|-----|-------|---------|---------|
| [指标名](indicators/xxx.md) | | | |

## 近期催化 / 风险
- 催化：
- 风险：

## 关联链接
- 包含个股：[...](stocks/...)
- 相关主题：[...](../../concepts/themes/...)

## 资料来源
```

### 3.3 指标实体页 (`wiki/entities/indicators/{指标名}.md`)

```markdown
---
title: 指标名称
type: indicator
category: 价格 | 开工率 | 出货量 | 库存 | 宏观
unit: 单位
frequency: 日度 | 周度 | 月度 | 季度
source: 数据来源说明
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# {指标名称}

## 定义
这个指标是什么，为什么重要。

## 数据趋势
> 由 LLM 定期更新最新数据点

| 日期 | 数值 | 环比 | 同比 | 备注 |
|-----|------|-----|------|------|
| | | | | |

## 投资含义
- 指标上升意味着什么
- 指标下降意味着什么
- 关键阈值/拐点信号

## 关联关系
- 上游影响因素：...
- 下游影响标的：...
- 相关指标：[...](xxx.md)
```

### 3.4 概念页 (`wiki/concepts/{子类}/{名称}.md`)

```markdown
---
title: 名称
type: framework | theme | theory
tags: [标签]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: N
---

# {名称}

## 核心思想
简要描述这个框架/主题/理论的关键内容。

## 要点拆解
1. 要点1
2. 要点2
3. ...

## 应用案例
- 在哪些分析中使用过此框架
- 链接到具体的应用页面

## 局限性
此方法的不足或适用边界。

## 关联链接
- 相关个股：[...](../../entities/stocks/...)
- 相关板块：[...](../../entities/sectors/...)
```

### 3.5 分析产出页 (`wiki/analyses/{子类}/{标题}.md`)

```markdown
---
title: 分析标题
type: comparison | deep-dive | review
date: YYYY-MM-DD
related_entities: [entity1, entity2]
related_concepts: [concept1]
tags: []
---

# {标题}

## 背景
为什么要做这次分析。

## 核心发现
1. 发现1
2. 发现2

## 结论与行动建议
- 具体的可执行结论

## 引用来源
- [相关实体](../entities/xxx.md) 的相关段落
- raw/原始资料
```

---

## 4. 工作流规范

### 4.1 录入 (Ingest)

**触发条件**：用户将新资料放入 `raw/` 并告知 LLM "录入这份资料"

**步骤**：

1. **读取并理解资料**
   - 全文阅读，提取核心论点、数据、观点
   - 如果是图片/扫描件，先读取文本再查看关键图片

2. **与用户确认要点**（除非用户要求跳过）
   - 列出你认为最重要的3-5个要点
   - 询问用户是否需要补充关注重点

3. **创建/更新Wiki页面**
   - 创建摘要页：`wiki/analyses/reviews/{资料简称}-摘要.md`
   - 创建或更新所有涉及的**实体页面**（个股、板块、指标等）
   - 创建或更新所有涉及的**概念页面**
   - 一份资料预计影响 **5-15个页面**

4. **更新索引和日志**
   - 更新 `wiki/index.md`：新增条目或修改摘要
   - 追加记录到 `wiki/log.md`：格式为 `## [YYYY-MM-DD] ingest | 资料标题`

5. **处理矛盾和新问题**
   - 如发现与已有内容矛盾 → 追加到 `wiki/meta/contradictions.md`
   - 如产生新的待解答问题 → 追加到 `wiki/meta/open-questions.md`

### 4.2 查询 (Query)

**触发条件**：用户向 Wiki 提问

**步骤**：

1. **先查索引**
   - 阅读 `wiki/index.md`，定位可能相关的页面列表

2. **深入阅读**
   - 打开相关页面，仔细阅读内容和交叉引用

3. **综合回答**
   - 基于已有知识作答，附上引用来源（具体到页面路径）

4. **输出形式**（根据问题类型选择）
   - 直接回答 — 简单事实性问题
   - Markdown 页面 — 有价值的深度回答，写回 `wiki/analyses/`
   - 对比表格 — 多对象比较时使用
   - 幻灯片 (Marp) — 需要演示时使用

5. **重要规则**：如果回答本身有长期价值（新发现的关联、对比分析、综合结论），必须作为新页面写回 Wiki。不要让好想法消失在聊天中。

### 4.3 检查 (Lint)

**触发条件**：用户要求检查 / 定期执行（建议每周一次）

**检查项目**：

| # | 检查项 | 操作 |
|---|-------|------|
| 1 | **矛盾检测** | 扫描所有页面，找出相互冲突的陈述 |
| 2 | **过时内容** | 标注被新资料推翻或已过期的旧说法 |
| 3 | **孤岛页面** | 找出没有任何入链的孤立页面 |
| 4 | **缺失实体** | 找出被多次提及但无独立页面的概念 |
| 5 | **引用断裂** | 检查所有链接是否指向存在的页面 |
| 6 | **信息空白** | 识别可以通过网络搜索填补的信息缺口 |
| 7 | **扩展建议** | 推荐值得深入研究的新方向和新资料 |

**输出**：生成一份 lint 报告，列出所有问题和建议操作。

---

## 5. 命名约定

### 文件命名
- 使用中文命名（这是中文知识库）
- 个股：`{股票名}.md`，如 `澜起科技.md`
- 板块：`{板块名}.md`，如 `AI算力.md`
- 指标：`{指标名}.md`，如 `硅料价格.md`
- 分析：`{简短标题}.md`，如 `澜起科技-vs-聚辰股份.md`
- 复盘：`{YYYY-MM-DD}.md`，如 `2026-04-13.md`
- 摘要：`{资料简称}-摘要.md`

### 链接格式
- 相对路径链接，使用 Obsidian 兼容的 `[[wikilink]]` 或标准 `[text](path)` 格式
- 统一使用相对路径，从当前文件位置出发

### YAML 前置元数据
- 所有 Wiki 页面必须有 YAML frontmatter
- 必填字段：`title`, `type`, `created`, `updated`
- 可选字段：按各模板定义

---

## 6. 日志格式

`wiki/log.md` 采用固定前缀格式，便于 Unix 工具查询：

```markdown
## [YYYY-MM-DD] {operation} | {简短描述}
- 来源：raw/...
- 涉及页面：...
- 关键发现：...
- 矛盾标注：（如有）
```

operation 类型：`ingest` | `query` | `lint` | `update` | `review`

常用命令速查：
```bash
# 最近10条操作
grep "^## \[" wiki/log.md | tail -10

# 所有录入记录
grep "ingest" wiki/log.md

# 某天的操作
grep "2026-04-13" wiki/log.md
```

---

## 7. 与现有系统的关系

| 系统 | 用途 | 与Wiki的关系 |
|------|------|------------|
| WorkBuddy MEMORY.md | 跨会话的工作偏好记忆 | 互补。MEMORY存偏好，Wiki存研究内容 |
| A股复盘笔记 | 日度市场复盘 | 迁移至 `wiki/analyses/reviews/`，增强版带交叉引用 |
| 产业链监控 | 四维三层数据追踪 | 结构化进入 `wiki/entities/indicators/` |
| Obsidian | 浏览和可视化 | Wiki 的前端界面（IDE） |

---

*最后更新：2026-04-13 | 版本：v0.1*
