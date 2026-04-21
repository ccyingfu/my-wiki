---
title: "LLM 知识库构建方法论"
type: framework
tags: [知识库, LLM, Wiki, Karpathy, Ingest-Query-Lint, Obsidian]
created: 2026-04-14
updated: 2026-04-14
sources: 1
status: active
---
	
# LLM 知识库构建方法论

## 定义

Andrej Karpathy 提出的基于 LLM 构建个人本地知识库的系统化方法。核心思路：不是在提问时才检索原始文档（RAG），而是让 LLM 持续构建并维护一个永久性的 Wiki——一套结构化、相互链接的 Markdown 文件。

## 核心原理

Wiki 是一个持久的、复利式的知识资产。交叉引用预先构建，矛盾提前标注，综合性结论反映所有已读内容。每加入新资料，Wiki 就更丰富一分。

**与 RAG 的本质区别**：
- RAG：每次提问从零开始"重新发现"知识，无积累
- Wiki：知识只需编译一次，持续保持更新，查询时直接复用

## 三层架构

| 层级 | 说明 | 角色 |
|------|------|------|
| 第一层：原始资料 (raw/) | 文章、论文、数据文件 | 只读，LLM 不修改 |
| 第二层：Wiki (wiki/) | 实体页面、概念页面、分析产出 | LLM 全权管理 |
| 第三层：Schema | 配置文件 (CLAUDE.md / schema.md) | 定义结构规范和工作流程 |

## 三种核心操作

### 1. 录入（Ingest）
将新资料放入 raw/，LLM 阅读并融入 Wiki：
- 提取关键信息（实体、概念、数据）
- 创建/更新 Wiki 页面（一份资料可能影响 10-15 个页面）
- 更新索引和日志
- 标注矛盾

### 2. 查询（Query）
向 Wiki 提问，LLM 搜索相关页面并综合作答：
- 先读 index.md 定位相关页面
- 深入阅读并附引用链接
- 有价值的洞见写回 Wiki

### 3. 检查（Lint）
定期健康检查：
- 页面间矛盾检测
- 孤岛页面排查
- 缺失交叉引用修复
- 信息空白发现

## 关键工具

- **Obsidian**：Wiki 的 IDE，图谱视图查看全貌
- **Git**：版本控制，开箱即用
- **index.md**：内容导向导航
- **log.md**：时间导向操作记录
- **qmd**（可选）：本地 Markdown 搜索引擎，支持 BM25/向量混合搜索

## 应用场景

- 深度研究（围绕课题持续积累）
- 投资知识库（研报、公告、行情归档分析）
- 读书笔记（人物、主题、情节线索的交叉引用）
- 个人成长（目标、健康、心理状态的追踪）

## 与本 Wiki 的关系

本 wiki 直接采用此方法论构建：
- `raw/` 为第一层原始资料库
- `wiki/` 为第二层知识库（LLM 全权管理）
- `wiki/schema.md` + `CLAUDE.md` 为第三层规范文档
- 三种操作通过 `.claude/skills/wiki-ingest.md`、`wiki-query.md`、`wiki-lint.md` 实现

## 资料来源

1. raw/articles/LLM wiki：karpathy 公开构建个人本地知识库详细方法「超强提示词」.md
