---
title: "SeekerGym: Benchmarking Agentic Information Seeking under Uncertainty"
title_zh: SeekerGym：不确定性下智能体信息搜寻的基准测试
authors: "Remy Kim, Minseung Lee, Shuo Li, Osbert Bastani"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=QzXdRJqZq8"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 包含元反思的智能体信息搜寻基准
tldr: 现有AI智能体缺乏自主信息搜寻评估体系，提出SeekerGym基准环境，通过重建维基百科和生成立项论文等任务评测智能体的信息搜寻能力，并设计带元反思的SeekerAgent进行跨案例学习。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 智能体信息搜寻能力缺乏专门评估基准。
method: 构建SeekerGym环境，设计SeekerAgent采用信念结构化管道和元反思进行跨案例学习。
result: 全面实验揭示了当前LLM智能体在信息搜寻中的优势与不足。
conclusion: 为智能体RAG的信息检索环节提供了标准化评测平台。
---

## Abstract
Effective information seeking is a prerequisite for AI agents, yet current systems often fail to autonomously identify, retrieve, and integrate relevant context. We propose SeekerGym, a modular environment for evaluating LLM agents on information-seeking tasks. Unlike prior benchmarks that focus on end-to-end task performance, SeekerGym evaluates agentic information seeking capabilities in two complex tasks: reconstructing Wikipedia pages and finding related literature for computer science survey papers. Furthermore, we design an information seeking agent called SeekerAgent, which employs various belief structuring pipelines including meta-reflection for cross-example learning. Through comprehensive experiments using SeekerGym, we evaluate several design choices for information seeking agents. We find that SeekerAgent improve recall by as much as 68% compared to frontier models.

---

## 论文详细总结（自动生成）

# SeekerGym: Benchmarking Agentic Information Seeking under Uncertainty 论文总结

## 1. 论文的核心问题与整体含义
- **核心问题**：当前AI智能体在自主识别、检索并整合相关上下文方面存在严重不足，缺乏专门评估智能体信息搜寻能力的标准化基准。
- **研究动机**：现有基准多关注端到端任务性能，而忽略了智能体在不确定性下进行动态信息搜寻这一关键环节。信息搜寻是智能体完成任务的前提，亟需系统性的评测环境。
- **整体含义**：通过构建SeekerGym环境和SeekerAgent，为智能体RAG（检索增强生成）中的信息检索阶段提供可复现、可扩展的评测平台，推动智能体具备更强的自主信息获取与整合能力。

## 2. 论文提出的方法论
- **SeekerGym环境**：一个模块化、可定制的评估环境，专门用于测试LLM智能体在复杂信息搜寻任务上的表现。强调“agentic”（智能体式）搜索，即智能体需要自主规划、执行多步检索并处理不确定性。
- **SeekerAgent设计**：
  - **信念结构化流水线**：将智能体的内部状态构建为结构化的信念（belief），以更好地跟踪已获取信息、缺失信息与置信度。
  - **元反思（meta-reflection）机制**：智能体能够从多个案例中跨样本学习，通过反思自身搜索策略的成败，动态调整后续行为，从而提升在新任务上的表现。
  - 方法未显式给出公式，但核心思想是将信息搜寻过程分解为信念更新、动作选择与元认知回顾三个阶段。

## 3. 实验设计
- **任务与数据集**：
  1. **维基百科页面重建**：要求智能体通过搜索重建指定维基百科页面的内容。
  2. **计算机科学综述论文的相关文献查找**：为给定主题寻找相关的文献，模拟文献综述的信息收集过程。
- **基准对比**：将SeekerAgent与前沿LLM模型（极可能包括GPT-4等）在相同的SeekerGym任务上进行对比，比较召回率等指标。
- **评测指标**：召回率（recall）作为主要衡量，此外可能涉及精确率、搜索步数等。

## 4. 资源与算力
- 所提供的元数据及文本片段中**未提及**所使用的GPU型号、数量、训练时长或推理算力消耗。论文可能未详细说明，或未能在当前提取文本中体现。

## 5. 实验数量与充分性
- 基于元数据，实验覆盖：
  - 两个主要任务环境（维基百科重建、文献查找）。
  - 多个设计选择的消融实验（如信念结构化的不同方式、是否采用元反思等）。
  - 与前沿模型的直接比较。
- **充分性评估**：实验设计考虑了多任务、多维度评估，并对智能体内部机制进行了消融，较为全面。但由于缺乏详细指标和统计显著性信息，无法完全判断客观性与公平性；所用数据集可能偏向英文维基百科和CS领域，覆盖范围有限。

## 6. 论文的主要结论与发现
- SeekerAgent通过元反思机制显著提升了信息检索的**召回率**，最高可达68%的提升（相较于未使用该机制的前沿模型）。
- 信念结构化流水线有助于智能体更准确地追踪搜索进度，减少遗漏关键信息。
- 当前LLM智能体在信息搜寻任务中存在明显弱点，尤其在需要多步推理和不确定性处理时，而SeekerAgent的设计有效弥补了部分缺陷。
- SeekerGym作为一个基准，能够细致揭示不同智能体在搜寻策略上的优劣势。

## 7. 优点
- **任务回归本质**：聚焦于智能体的核心能力——搜寻信息，而非仅有端到端应用指标。
- **环境设计模块化**：可灵活扩展，便于后续研究复用。
- **创新性机制**：引入元反思实现跨案例学习，增强了智能体的适应性和持续改进能力。
- **评测全面**：涵盖两类具有代表性的复杂信息搜寻任务，兼顾事实重建与文献探索。

## 8. 不足与局限
- **任务领域较窄**：当前仅涉及维基百科和CS综述，向其他领域（如金融、医疗）的泛化性未验证。
- **元反思的可解释性**：未提及如何处理反思的质量与潜在的错误累积。
- **算力成本未知**：缺乏对资源需求的报告，不利于复现和实际部署的评估。
- **可能的评估偏差**：维基百科重建任务容易受训练数据泄露影响（LLM可能已记忆部分页面），文献查找任务对主题依赖性强，可能高估或低估性能。
- **动态环境缺失**：未考虑信息实时变化或对手信息的场景，与现实世界信息搜寻的不确定性仍有差距。

（完）
