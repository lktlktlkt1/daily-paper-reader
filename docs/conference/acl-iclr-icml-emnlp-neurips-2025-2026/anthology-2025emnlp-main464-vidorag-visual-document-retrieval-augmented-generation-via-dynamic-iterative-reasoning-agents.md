---
title: "ViDoRAG: Visual Document Retrieval-Augmented Generation via Dynamic Iterative Reasoning Agents"
title_zh: ViDoRAG：通过动态迭代推理智能体进行视觉文档检索增强生成
authors: "Qiuchen Wang, Ruixue Ding, Zehui Chen, Weiqi Wu, Shihang Wang, Pengjun Xie, Feng Zhao"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.464.pdf"
tags: ["query:agentic-rag"]
score: 10.0
evidence: ViDoRAG使用动态迭代推理智能体进行视觉文档RAG
tldr: 针对视觉丰富文档RAG中检索、理解和推理的挑战，提出ViDoSeek数据集和ViDoRAG框架，采用动态迭代推理智能体。该框架通过多步骤检索和推理，有效整合文本与视觉特征，弥补现有方法推理不足的问题。实验表明，ViDoRAG在复杂视觉文档问答上显著优于传统RAG方法，为多模态RAG的智能体推理开辟了新方向。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 1100, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 756, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 251, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 722, \"height\": 290, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 603, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 786, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 513, \"height\": 230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 515, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.464/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 353, \"height\": 229, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1275, \"height\": 788, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 731, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 584, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 647, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 645, \"height\": 170, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 795, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 799, \"height\": 508, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 449, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 447, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1643, \"height\": 434, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 799, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.464/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 796, \"height\": 144, \"label\": \"Table\"}]"
motivation: 视觉文档RAG存在检索融合不佳和推理深度不足的局限。
method: 提出ViDoRAG，基于动态迭代推理智能体，多步骤融合文本与视觉特征进行检索与推理。
result: 在ViDoSeek数据集上，ViDoRAG大幅提升复杂视觉文档问答性能。
conclusion: 动态迭代智能体推理为视觉文档RAG提供了有效解决方案。
---

## Abstract
Understanding information from visually rich documents remains a significant challenge for traditional Retrieval-Augmented Generation (RAG) methods. Existing benchmarks predominantly focus on image-based question answering (QA), overlooking the fundamental challenges of efficient retrieval, comprehension, and reasoning within dense visual documents. To bridge this gap, we introduce ViDoSeek , a novel dataset designed to evaluate RAG performance on visually rich documents requiring complex reasoning. Based on it, we identify key limitations in current RAG approaches: (i) purely visual retrieval methods struggle to effectively integrate both textual and visual features, and (ii) previous approaches often allocate insufficient reasoning tokens, limiting their effectiveness. To address these challenges, we propose ViDoRAG , a novel multi-agent RAG framework tailored for complex reasoning across visual documents. ViDoRAG employs a Gaussian Mixture Model (GMM)-based hybrid strategy to effectively handle multi-modal retrieval. To further elicit the model’s reasoning capabilities, we introduce an iterative agent workflow incorporating exploration, summarization, and reflection, providing a framework for investigating test-time scaling in RAG domains. Extensive experiments on ViDoSeek validate the effectiveness and generalization of our approach. Notably, ViDoRAG outperforms existing methods by over 10% on the competitive ViDoSeek benchmark. The code will be available.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：视觉丰富文档（含图表、表格、流程图等）在金融、教育等领域广泛存在，但传统检索增强生成（RAG）方法在检索、理解与推理上表现不佳，主要面临两大瓶颈：（1）纯视觉检索难以有效融合文本与视觉特征；（2）生成阶段分配不足的推理 token，限制了模型的深层推理能力。
- **现有基准的局限**：目前主流视觉问答（VQA）数据集大多仅关联单张图像或单个文档，无法评估大规模文档集合下的 RAG 系统。为此，论文构建了 **ViDoSeek**——首个面向视觉文档集合的检索‑推理‑问答数据集，每个查询在全局语料中有唯一答案，以此推动 RAG 在真实多文档场景下的研究。
- **整体含义**：提出 **ViDoRAG** 多智能体框架，结合动态多模态检索与迭代推理，旨在系统性解决视觉文档 RAG 中的检索精度低、噪声干扰大、推理深度不足等问题。

### 2. 论文提出的方法论

- **核心思想**：将 RAG 流程解耦为**多模态混合检索**与**多尺度多智能体生成**两个阶段，通过从粗到细的迭代过程提高结果的准确性和鲁棒性。
- **关键技术细节**
  - **多模态混合检索**（Multi‑Modal Hybrid Retrieval）
    - 分别建立文本（OCR 文本块）与视觉（图像）两条检索管线，利用稠密向量模型计算查询与文档的余弦相似度 \(S(q, C)\)。
    - 引入**高斯混合模型（GMM）**假设相似度分布由高相关（\(T\)）和低相关（\(F\)）两个高斯分量组成：
      \[
      P(s) = w_F \cdot \mathcal{N}(s|\mu_F, \sigma_F^2) + w_T \cdot \mathcal{N}(s|\mu_T, \sigma_T^2)
      \]
      通过 EM 算法估计每个文档属于高相关分量的后验概率，从而**动态决定每条管线的召回数量 \(K\)**（\(K = |\{p_i \sim \mathcal{N}(\mu_T, \sigma_T^2)\}|\)）。
    - 最后对文本与视觉的召回结果取并集 \(R_{\text{hybrid}}\)，并按原始页码排序，以利用相邻页面的语义相关性。
  - **多智能体生成与迭代推理**（Multi‑Agent Generation）
    - 三个角色：**Seeker Agent**（寻图者）、**Inspector Agent**（审查者）、**Answer Agent**（回答者）。
    - **Seeker** 在候选图像（初始为检索结果）中快速选择可能相关的图像，并记录思考记忆 \(M_t\)；若收到 Inspector 的反馈 \(F_{t-1}\)，则据此调整下一轮选择。
    - **Inspector** 对 Seeker 所选图像进行细粒度审查：若信息充足，给出草拟答案 \(\hat{A}\) 和参考图像 \(I_{\text{ref}}\)；否则反馈具体需求 \(F_t\)，并保留部分相关图像 \(I_r^t\) 供下轮使用。
    - **Answer Agent** 在最后一步验证草拟答案与参考图像的一致性，结合查询 \(Q\) 给出最终答案 \(A\)。
    - 通过若干轮次的 Seek‑Inspect 交互，实现从粗到细的迭代推理，显著减少无关图像噪声，增强答案可信度。

### 3. 实验设计

- **数据集 / 场景**
  - **ViDoSeek**：包含约 1.2k 个查询，覆盖 12 个领域、4 种内容类型（文本、图表、表格、布局）以及单跳 / 多跳推理。查询要求在全量文档集合中给出唯一答案。
  - **SlideVQA‑Refined**：对公开 SlideVQA 的查询进行改写，使其适用于大规模文档 RAG 场景，用于验证方法的泛化性。
- **Benchmark 与对比方法**
  - 基线：
    - **TextRAG**：OCR 文本 + NV‑Embed‑V2 检索，取 Top‑5 页面输入 LLM 生成。
    - **VisualRAG**：ColQwen2 视觉检索，同样取 Top‑5 页面输入 VLM 生成。
  - 自家方法：**ViDoRAG**（GMM 动态召回 + 多智能体生成）。
  - 上限参考：**Upper Bound**（直接输入金标准页面）。
- **评价指标**
  - 端到端准确率：采用 GPT‑4o 进行 1‑5 分模型评估，≥4 分为正确。
  - 检索指标：Recall@K、MRR@K。
  - 另外补充了 EM、F1、ANLS 等指标验证一致性。
- **模型选择**：分别使用闭源模型 GPT‑4o 和开源模型 Qwen2.5‑VL‑7B、Llama3.2‑Vision‑90B 等测试框架的通用性。

### 4. 资源与算力

- 文中提及使用 **8 块 A100 GPU** 和 **96 个 CPU 核** 的服务器进行实验，主要服务于开源模型的推理（未报告训练环节）。对于闭源 API 调用，未给出具体算力消耗。总体而言，算力资源集中在推理阶段，框架本身不需要大规模训练，因此计算负担主要源自多智能体迭代带来的额外推理延迟。

### 5. 实验数量与充分性

- **实验规模**：
  - 主表（表 2）涵盖 **3 种模型家族 × 多种方法**（Upper Bound、TextRAG、VisualRAG、ViDoRAG），共 12 组端到端对比。
  - 检索对比（表 3）评估了 **6 种检索器**（BM25、BGE‑M3、NV‑Embed‑V2、VisRAG、ColPali、ColQwen2）。
  - 消融实验（表 4）逐步测试动态召回与多智能体生成的效果，含 6 种配置。
  - 进一步分析包括：动态召回的延迟与准确率权衡（表 5、图 5）、不同模态与推理类型上的性能（图 6）、测试时缩放行为（图 7）、不同评估模型与人类评估的一致性（表 6‑10）等。
- **充分性与公平性**：
  - 实验在多个大模型上复现，并选用统一的公平基线（固定 Top‑5 检索），避免了因上下文长度差异造成的偏差。
  - 消融设计清晰，能够独立验证 GMM 动态召回和多智能体迭代的增益。
  - 额外分析了检索阶段 GMM 对平均页面数的影响，以及多智能体交互轮次与模型能力的关联，论证较为充分。
  - 数据集构建流程包含语义过滤、多模态审查和人工 refine，增强了评估的客观性。

### 6. 论文的主要结论与发现

- **ViDoRAG 显著提升性能**：在 ViDoSeek 上，ViDoRAG 相较于最强基线（VisualRAG）在 GPT‑4o 下的整体准确率从 72.1% 提升至 79.4%，相对提升超过 10%，在所有内容类型和推理类型上均表现一致。
- **动态混合检索比固定 Top‑K 更优**：GMM 自适应召回在平均召回页面更少（从 10 页降至 6.76 页）的同时，端到端准确率反而提升，有效平衡了上下文长度与信息充分性。
- **多智能体迭代推理是有效的测试时缩放方法**：模型性能越强，需要的交互轮次越少；通过将复杂任务分解为多个简单步骤，可以在不改变模型参数的情况下稳定提升生成质量。
- **视觉信息对视觉文档 RAG 至关重要**：即使针对纯文本问题，仅靠文本检索的 TextRAG 仍大幅落后于包含视觉信息的管线，说明视觉特征对于理解布局与关系不可或缺。

### 7. 优点

- **问题定义清晰，数据集针对性强**：ViDoSeek 填补了大规模视觉文档 RAG 评估的空白，要求唯一答案和特定参考页，能更真实地反映系统能力。
- **方法设计精巧且可扩展**：GMM 动态召回不需要繁琐的超参数调优，可自动适配不同查询；混合检索与多智能体迭代可灵活嵌入不同的检索引擎和生成模型。
- **实验验证全面**：覆盖多种模型规模、多种模态管线、消融分析、时间效率分析和人工评估，结论稳健。
- **多智能体角色分工明确**：Seeker 负责粗筛、Inspector 负责精读和反馈、Answer Agent 负责最终校验，这种从粗到细的推理范式能有效抑制噪声、增强答案一致性。

### 8. 不足与局限

- **查询构建可能引入人为偏差**：ViDoSeek 由专家标注，问题措辞和类型可能无法完全覆盖真实用户的多样性，影响模型在开放场景下的泛化性。
- **计算延迟增加**：多智能体迭代式交互带来了额外的推理开销，在低延迟要求的应用中可能成为瓶颈。
- **模型幻觉问题未彻底解决**：文中承认生成模型仍可能产生未基于检索信息的幻觉答案，这是整体可靠性的潜在风险。
- **实验集中于英文幻灯片文档**：数据集以英文幻灯片为主，对其他视觉文档类型（如发票、设计图等）和多语言环境的覆盖不足。
- **未探索训练 / 微调**：主要工作在零样本或少样本推理层面，未涉及针对 ViDoSeek 的微调或强化学习优化，上限可能仍有提升空间。

（完）
