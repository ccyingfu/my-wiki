# CLAUDE.md — Wiki 知识库项目配置

## 项目说明

这是一个 **LLM 驱动的持久化知识库**（基于 Andrej Karpathy 的 Wiki 模式），用于投资研究与产业链监控。

**核心思路**：不是 RAG 检索，而是让 LLM 持续维护一套结构化的 Markdown 文件。知识编译一次、持续复用。

## 目录速览

```
my-wiki/
├── raw/              # 原始资料库（只读层）
│   ├── reports/      # 研报
│   ├── articles/     # 文章
│   ├── filings/      # 公告
│   ├── policies/     # 政策
│   ├── data/         # 数据文件
│   ├── notes/        # 笔记
│   └── assets/       # 图片附件
│
├── wiki/             # 知识库（LLM 全权维护）
│   ├── schema.md     # ⬅️ 规范文档（先读这个）
│   ├── index.md      # 总索引（精简入口）
│   ├── log.md        # 操作日志（只追加）
│   ├── entities/     # 个股 / 板块 / 指标 / 人物
│   ├── concepts/     # 框架 / 主题 / 理论
│   ├── analyses/     # 复盘 / 对比 / 深度报告
│   └── meta/         # 待读清单 / 未解问题 / 矛盾记录
│
├── .claude/skills/   # ⬅️ 核心工作流技能定义
│   ├── wiki-ingest.md    # 录入操作
│   ├── wiki-query.md     # 查询操作
│   └── wiki-lint.md      # 检查操作
│
└── CLAUDE.md         # ⬅️ 本文件
```

## 三种核心操作

用户会以自然语言触发以下操作，请读取 `.claude/skills/` 下对应的技能文件来执行：

| 用户说 | 读取技能 | 做什么 |
|-------|---------|-------|
| "录入 xxx" | `wiki-ingest.md` | 阅读 raw/ 资料 → 创建/更新 wiki 页面 → 更新索引+日志 |
| "查询 / 问一下 / 对比" | `wiki-query.md` | 查索引定位页面 → 深入阅读 → 综合作答 → 引用来源 |
| "检查 / lint / 体检" | `wiki-lint.md` | 7项健康检查 → 出报告 → 自动修复能修的 |

## 工作规范

1. **每次操作前先读 `wiki/schema.md`** — 了解页面模板和命名约定
2. **绝不修改 `raw/` 目录** — 原始资料是只读层
3. **每次 Ingest/Lint 完成后执行 `git commit`**
4. **log.md 只追加不修改** — 固定前缀格式：`## [YYYY-MM-DD] {操作类型} | {标题}`
5. **不确定就问用户** — 尤其是对矛盾信息的判断
6. **有价值的 Query 结果要建议写回 Wiki**

## Git 规范

```bash
# Commit message 格式
ingest: {日期} | {资料简短标题}
query: {日期} | {问题摘要} → 产出: {文件}
lint: {日期} | {模式} — 发现N个问题, 修复M个
refactor: {描述}
```

## 关键文件优先级

1. `wiki/schema.md` — 所有操作的规范依据（最高优先级）
2. `wiki/index.md` — 导航入口
3. `wiki/log.md` — 操作历史
4. `.claude/skills/*.md` — 工作流详细步骤

---

*此文件与 .claude/skills/ 下的三个技能文件配合使用。*
