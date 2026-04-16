# Harness（智能体评估/协同框架）

> 来源：my-wiki/raw/articles | Ingest: 2026-04-16
> 原始文件：`raw/articles/什么是 Harness.md`、`raw/articles/李开复陆奇重仓同一家Harness智能体公司.md`

## 定义

**Harness**（意为"马具"）在 AI 领域有两层含义：

1. **评估框架（Evaluation Harness）**：标准化工具集，用于系统性测试和比较 AI 模型性能（公平、可复现、全面）
2. **智能体协同框架（Agent Harness）**：连接模型与人类需求的核心框架，通过约束、规范与协同机制引导多智能体高效协作

---

## 1. 评估框架（EleutherAI LM Evaluation Harness）

大语言模型评估领域最广泛使用的开源框架。

| 特性 | 说明 |
|------|------|
| 任务丰富 | 200+ 评估任务（推理/知识/代码/数学/多语言/安全） |
| 标准化实现 | 统一提示词模板、生成参数、后处理逻辑 |
| 模型兼容 | HuggingFace / OpenAI API / vLLM / 本地模型 |
| 可复现 | 固定随机种子 |

```bash
pip install lm-eval
lm_eval --model hf --model_args pretrained=meta-llama/Llama-2-7b \
        --tasks arc_easy,hellaswag,gsm8k --batch_size 8
```

### 解决的核心问题

- 结果不可比（不同论文用不同提示词/参数）
- 数据泄露（测试集混入训练）
- 评估不完整（只测简单任务）
- 复现困难

---

## 2. 智能体协同框架（Agent Harness）

### 核心价值：「约束换自主」

不直接参与任务执行，通过明确的约束与协同机制，引导多智能体高效协作、避免失控。

### 行业共识形成过程

| 时间 | 事件 |
|------|------|
| 2025年12月 | 李笛团队提出群体智能理论，预判Harness趋势 |
| 2026年2月 | OpenAI 发布《Harness Engineering: Leveraging Codex in an Agent-First World》 |
| 2026年2月 | Anthropic 发布 Managed Agents 架构，强调 Agent Harness |
| 2026年初 | 明日新程（Nextie）发布「团子」tuanzi.ai 内测版 |

### 明日新程（Nextie）— 李笛团队

- **创始人**：李笛（「小冰之父」、微软亚洲互联网工程院原副院长）
- **融资**：成立4个月完成两轮，创新工场+Atypical Ventures领投，奇绩创坛跟投，资金储备够3-5年
- **产品**：
  - **团子（tuanzi.ai）**：原生群体智能平台，数十个Agent辩论/投票/同行评审
  - **卫士虾（TuanziGuardianClaw）**：群体智能自主设计的安全审计Agent
  - **新版「小冰岛」**：预计2026年4月底推出

### Harness 三大核心组件

1. **上下文管理** — 确保信息准确全面适度，避免过载或偏差
2. **多智能体池（Agent Pool）** — 根据任务动态搭配不同功能Agent
3. **协同方法（认知碰撞）** — 辩论/挑战/反思/同行评审/投票，打破单一Agent认知盲区

### 效果数据

- 综合表现优于 ChatGPT-5.2 Thinking 等单一大模型
- 同等思考深度下，Token消耗降低约50%
- 五维评测指标：视角完备性/辩证深度/落地实操性/隐含诉求满足度/决策质量

### OpenAI 的通用 Harness 方向

Jakub Pachocki（OpenAI首席科学家）观点：

> 「harness的实现很长一段时间内都不应该成为限制。我们会有更通用的harness。Codex用在编程以外的地方效果也不错。」
>
> **长期来看，AI应该默认出现在你所在的地方。如果没有，那只应该是因为它有了新的能力，而不是因为它有局限。**

---

## 相关条目

- [[李笛]] — 明日新程创始人
- [[Jakub Pachocki]] — OpenAI首席科学家
- [[LLM Wiki知识库模式]] — Karpathy的知识构建方法论
- [[美伊战争情景分析框架]] — 另一种结构化分析框架
