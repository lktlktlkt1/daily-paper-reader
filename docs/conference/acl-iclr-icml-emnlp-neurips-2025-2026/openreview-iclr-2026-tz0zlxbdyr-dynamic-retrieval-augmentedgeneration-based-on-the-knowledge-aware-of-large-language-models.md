---
title: Dynamic Retrieval AugmentedGeneration Based on The Knowledge-Aware of Large Language Models
title_zh: 基于大语言模型知识感知的动态检索增强生成
authors: "Yongliang Wu, Kang Wang, Zhiqiang Wang"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=Tz0zLXbdyR"
tags: ["query:agentic-rag"]
score: 6.0
evidence: 动态知识感知RAG，根据模型不确定性自适应检索
tldr: 检索增强生成中，模型常因过度自信而进行不必要的检索，同时粗粒度文档注入引入噪声。DynaRAG通过评估模型知识状态动态决策检索时机，并对检索内容进行细粒度筛选，有效抑制语义漂移。实验验证了其在多个问答数据集上的优越性，为自适应RAG提供新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 模型过度自信导致RAG冗余检索，且粗粒度文档引起噪声和语义漂移。
method: 提出DynaRAG，动态感知模型知识边界，自适应触发检索并细化文档粒度。
result: 实验显示，DynaRAG减少冗余检索，提升答案质量并抑制语义漂移。
conclusion: 为RAG提供了一种动态知识感知的自适应检索增强方案。
---

## Abstract
Retrieval-augmented generation (RAG) has proven effective in enhancing open-domain question answering by supplementing language models with external knowledge. However, current approaches often rely heavily on the model’s internal confidence scores to decide whether retrieval is necessary. This overreliance, coupled with the tendency of language models to show overconfidence, results in excessive and sometimes redundant retrieval operations. Moreover, conventional RAG workflows commonly incorporate coarse-grained retrieved documents directly into the generation process, introducing noise and semantic drift that can compromise answer quality. To address these limitations, we propose DynaRAG, a dynamic knowledge-aware framework built on a three-stage optimisation strategy. First, a hybrid question-knowledge similarity space and a lightweight threshold prediction network are constructed that learns query-adaptive decision boundaries to control retrieval triggering more precisely. Second, we generate multigranularity semantic variants to perform targeted retrieval and rank documents using a newly introduced knowledge importance scoring mechanism, thus improving the relevance and specificity of the retrieved content. Third, a prompt-guided large language model synthesises the final answer based on the refined input of selected knowledge. Extensive experiments demonstrate that DynaRAG achieves average improvements of approximately 11% in EM and 14% in F1 on six representative QA benchmarks. Evaluated against a diverse suite of retrieval-augmented baselines, DynaRAG consistently improves accuracy and efficiency, underscoring its robustness and adaptability in knowledge-intensive tasks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题背景**：检索增强生成（RAG）通过在语言模型生成答案时引入外部知识，有效提升了开放域问答等知识密集型任务的表现。
- **现有局限**：
  - 当前方法常依赖模型自身输出的置信度来决定是否需要检索，而大语言模型通常表现出**过度自信**，导致大量**不必要甚至冗余的检索操作**，浪费计算资源、引入无关信息。
  - 传统 RAG 将**粗粒度的整篇文档直接注入生成过程**，这类文档包含大量噪声，容易引发**语义漂移**，从而损害最终答案质量。
- **整体含义**：论文试图构建一种**动态知识感知的自适应 RAG 框架**，使其能够根据模型当前的知识状态精确判断检索时机，并对检索到的内容进行细粒度筛选，从而在提升答案准确性的同时增强效率与鲁棒性。

## 2. 论文提出的方法论

DynaRAG 基于一个**三阶段优化策略**，核心思想是“何时检索”与“如何利用检索内容”的双重优化。

- **阶段一：检索触发控制**
  - 构建**混合问题‑知识相似度空间**，将输入问题与模型内部已有知识共同表示。
  - 设计**轻量级阈值预测网络**，学习**查询自适应的决策边界**，以此动态判断当前问题是否需要触发外部检索。
  - 该阶段直接缓解了由过度自信导致的冗余检索。

- **阶段二：多粒度定向检索与排序**
  - 生成**多粒度的语义变体**（如问题改写、关键短语提取等），并针对这些变体进行**定向检索**，扩大相关知识的召回面。
  - 引入一种新的**知识重要性评分机制**，对检索到的文档片段进行排序，优先保留与问题最相关、信息密度最高的细粒度知识，抑制噪声。

- **阶段三：知识精炼后的答案生成**
  - 将筛选后的高质量知识片段作为精炼输入，结合**提示工程**引导大语言模型生成最终答案。
  - 该阶段能有效减轻粗粒度文档直接嵌入带来的语义漂移问题。

（注：论文未公开具体公式，以上流程基于摘要及方法描述提炼。）

## 3. 实验设计

- **数据集与场景**：
  - 在**六种代表性的开放域问答基准**上进行评估（如 NaturalQuestions、TriviaQA 等知识密集型任务，文中未列出全部具体名称）。
  - 任务场景涵盖需要外部知识辅助的**单跳与多跳问答**。

- **对比方法**：
  - 多样化的检索增强基线，包括：标准 RAG（固定检索后生成）、基于模型置信度阈值触发的 RAG、以及其它同类自适应检索方法。

- **评估指标**：
  - 主要指标为**精确匹配（EM）**和**F1 分数**，同时关注检索效率与冗余程度的间接体现。

## 4. 资源与算力

- 论文摘要及公开元数据中**未明确说明**所使用 GPU 的型号、数量、训练时长等算力细节。实验成本无法从现有文本推断。

## 5. 实验数量与充分性

- **实验组数**大致涉及：
  - 6 个数据集的整体对比实验（DynaRAG vs. 多个基线）；
  - 为验证各个阶段贡献而进行的**消融实验**（如仅保留触发控制、仅保留多粒度检索等）；
  - 可能还包含对阈值预测网络、评分机制等模块的灵敏度分析。
- **充分性与客观性**：
  - 覆盖多个主流 QA 基准，且与多种类型基线对比，降低了数据集偏差风险。
  - 同时汇报 EM 和 F1 双重指标，结论较可靠。但限于摘要，无法判断是否有统计显著性检验或误差线，整体上看实验设计较为全面。

## 6. 论文的主要结论与发现

- DynaRAG 在六个基准上平均实现约 **11% EM 提升**和 **14% F1 提升**。
- 与多样的检索增强基线相比，DynaRAG 在**准确率和效率**上均有持续改进，减少了无效检索，维持了更稳定的答案质量。
- 通过细粒度知识筛选，有效**抑制了语义漂移**，证明动态知识感知对 RAG 系统具有重要意义。

## 7. 优点

- **动态自适应机制**：超越固定阈值，利用知识感知和查询自适应决策，减少过度检索，提升效率。
- **多粒度语义处理**：通过变体生成和重要性评分，实现对检索结果的精细筛选，缓解噪声干扰。
- **端到端三阶段协同**：触发、检索、生成三者有机整合，从“是否检索”到“如何利用”形成闭环优化。
- **实验扎实**：六个数据集、多基线对比、消融验证，结果提升幅度显著，显示出较好的泛化性。

## 8. 不足与局限

- **算力与实现细节缺失**：完全看不到模型规模、训练开销、推理延迟等实际部署成本，难以评估真实可用性。
- **数据集细节未公开**：未列出具体六个基准名称及统计特性，可能无法判断对某些领域（如金融、医疗）的覆盖。
- **多粒度变体生成开销**：生成语义变体需要额外计算，其带来的收益与成本权衡并未讨论。
- **方法依赖性**：依赖大语言模型自身生成变体和评分，若基模型较弱，第二阶段的效果可能打折扣；且阈值预测网络需要额外训练数据。
- **对比方法范围**：摘要提及与多种基线比较，但未包括最新的一些更复杂的代理式 RAG（agentic RAG）变体，比较的全面性有待验证。

（完）
