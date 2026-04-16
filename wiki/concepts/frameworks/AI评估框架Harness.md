---
title: AI评估框架（Evaluation Harness）
type: framework
tags: [AI, 评估, 基准测试, 模型评测, EleutherAI]
created: 2026-04-16
updated: 2026-04-16
sources: 1
status: active
---

# AI 评估框架（Evaluation Harness）

## 一句话定位

一套标准化的工具和流程，用于系统性测试和比较AI模型的性能，解决"公平、可复现、全面"的模型评估核心问题。

## 核心思想

Harness 的本质是连接"模型（马匹）"与"人类需求（骑手）"的核心框架。它不直接参与任务执行，而是通过**明确的约束、规范与协同机制**，引导多智能体高效协作、避免失控。

> **类比**：就像骑手的马具——不替马跑，但让马的力气精准用在需要的地方。

## 要点拆解

### 解决的核心问题

| 问题 | 说明 |
|------|------|
| **结果不可比** | 不同论文使用不同提示词/参数，分数差异巨大 |
| **数据泄露** | 测试集混入训练数据导致分数虚高 |
| **评估不完整** | 只测简单任务，忽略复杂推理或安全性 |
| **复现困难** | 别人无法重现论文报告的分数 |

### 最著名实现：EleutherAI LM Harness

- 支持 **200+ 个评估任务**，涵盖推理、知识、代码、数学等
- 统一的提示词模板、生成参数、后处理逻辑
- 支持 HuggingFace、OpenAI API、vLLM、本地模型等
- 固定随机种子确保每次运行结果一致

### 支持的任务类型

- **问答**：ARC, HellaSwag, OpenBookQA
- **常识推理**：PIQA, WinoGrande, SIQA
- **阅读理解**：RACE, DROP, SQuAD
- **数学**：GSM8k, MATH
- **代码**：HumanEval, MBPP
- **安全性**：TruthfulQA, BOLD

## 行业共识与发展

1. **OpenAI（2026.2）**：发布官方 Blog 《Harness Engineering》，证明3人小组5个月可用Agent构建百万行代码产品
2. **Anthropic**：新 Agent 架构 Managed Agents 文档反复强调 "Agent Harness"
3. **明日新程（Nextie）**：将 Harness 工程化理念与群体智能深度融合，核心组件 = 上下文管理 + 多智能体 + 协同方法（"认知碰撞"）
4. **通用 Harness 趋势**：OpenAI 首席科学家 Jakub Pachocki 明确表示未来会有更通用的 harness 可被用于各种领域

## 与多智能体的关系

Harness 是智能体落地的**核心支撑**。单一超级智能体在长程任务中错误会指数级放大，而 Harness 通过：
- **上下文管理**：确保信息准确全面，避免偏差
- **认知碰撞**：辩论、挑战、反思、投票打破单一 Agent 认知盲区
- **Agent 池优化**：按需求动态搭配不同功能定位的 Agent

## 关联链接

- 相关概念：[[多智能体协同]]
- 相关公司：[[明日新程]]
- 相关人物：[[李笛]]、[[Jakub Pachocki]]
- 技术应用：[[LLM Wiki模式]]

## 资料来源

1. raw/articles/什么是 Harness.md
2. raw/articles/李开复陆奇重仓同一家Harness智能体公司...md
3. raw/articles/OpenAI首席科学家最新采访...md
