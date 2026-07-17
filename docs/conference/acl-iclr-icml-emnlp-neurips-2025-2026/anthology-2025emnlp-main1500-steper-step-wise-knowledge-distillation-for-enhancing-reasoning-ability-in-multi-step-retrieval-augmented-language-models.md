---
title: "StepER: Step-wise Knowledge Distillation for Enhancing Reasoning Ability in Multi-Step Retrieval-Augmented Language Models"
title_zh: StepER：面向多步检索增强语言模型推理能力增强的分步知识蒸馏
authors: "Kyumin Lee, Minjin Jeon, Sanghwan Jang, Hwanjo Yu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1500.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 分步知识蒸馏增强多步检索增强语言模型的推理能力
tldr: 针对现有多步RAG知识蒸馏忽视不同步骤间推理能力差异的问题，提出分步知识蒸馏框架StepER。通过为每步设计专门的监督信号匹配阶段信息需求，并结合难度感知训练逐步优化，显著提升了多步检索增强模型在复杂问答上的推理准确率与泛化性。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1567, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1312, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 764, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 798, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1500/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 342, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 1043, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 595, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 126, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 800, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1551, \"height\": 1396, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1500/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1589, \"height\": 1691, \"label\": \"Table\"}]"
motivation: 传统知识蒸馏未考虑多步RAG各阶段需不同推理能力，导致迁移效果受限。
method: 提出分步知识蒸馏，用分步监督对齐各步的推理需求，并引入难度感知训练策略。
result: 在多个复杂问答数据集上推理性能显著提升，且所需检索步数更少。
conclusion: StepER为多步RAG的知识迁移提供了阶段自适应方案，增强了模型的综合推理能力。
---

## Abstract
Answering complex real-world questions requires step-by-step retrieval and integration of relevant information to generate well-grounded responses. However, existing knowledge distillation methods overlook the need for different reasoning abilities at different steps, hindering transfer in multi-step retrieval-augmented frameworks. To address this, we propose Step-wise Knowledge Distillation for Enhancing Reasoning Ability in Multi-Step Retrieval-Augmented Language Models (StepER). StepER employs step-wise supervision to align with evolving information and reasoning demands across stages. Additionally, it incorporates difficulty-aware training to progressively optimize learning by prioritizing suitable steps. Our method is highly adaptable across various frameworks of multi-step retrieval-augmented language models, including those based on reasoning paths or question decomposition. Extensive experiments show that StepER outperforms prior methods on multi-hop QA benchmarks, with an 8B model achieving performance comparable to a 70B teacher model.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将以 Markdown 形式，对给定论文进行结构化、深入、客观的总结。

### **1. 核心问题与研究动机**

-   **核心问题**：复杂问题的回答往往需要**多步检索与推理**。现有知识蒸馏（KD）方法在将大模型（教师）的这种多步推理能力迁移给小模型（学生）时存在不足。
-   **动机与背景**：
    -   **现有方法局限**：传统 KD 方法（如 Vanilla-KD）仅让学生模型基于累积的全部检索结果来模仿完整的推理过程，**忽视了不同推理步骤所需的特定推理能力**，例如，初始化、扩展和聚合信息的能力。
    -   **问题场景需求**：以医生诊断为例，推理过程可分为“初始化（根据初步症状推断）”、“扩展（进行更多检查获取信息）”、“聚合（综合信息得出结论）”三个阶段，每个阶段所需的信息量和推理能力不同。
    -   **现有方法失效**：Vanilla-KD 训练出的模型倾向于在第一步获取极少信息时就试图生成全部推理，导致推理初始阶段失败，最终性能受限。

### **2. 方法论：StepER 框架**

-   **核心思想**：**分步知识蒸馏**。将多步检索增强语言模型的推理过程分解为初始化、扩展和聚合三个阶段，并针对每个阶段设计专门的监督信号，训练学生模型逐步掌握相应的推理能力。
-   **关键技术细节（数据构建与训练）**：
    -   **分步数据集构建**：利用教师模型（70B LLM）执行多步检索与推理，并按步骤记录生成过程和上下文信息，构建一个分步数据集 ( \( D_{steps} \) )。
        1.  **推理初始化（First-step）**：仅基于初始问题和首次检索到的段落，由教师模型生成第一步推理。
        2.  **推理扩展（Mid-step）**：基于前一步推理生成检索查询，结合新检索和累积的段落、推理链，由教师模型生成后续推理步骤。
        3.  **推理聚合（Final-step）**：在最后一步，教师模型聚合所有信息，得出最终答案。数据仅保留教师回答正确的样本，以过滤错误推理。
    -   **多任务学习目标**：训练学生模型时，最小化一个联合损失函数，该函数同时要求模型在给定对应步骤信息条件下，预测初始化、扩展和聚合三个阶段的推理文本。
    -   **推理难度感知训练**：
        -   **问题**：在训练的不同阶段，各个推理步骤的学习难度是动态变化的。
        -   **方法**：引入可训练的参数 \( \sigma_j \) （j ∈ {init, exp, agg}）来表征每个步骤任务的难度。最终的损失函数 \( L_{final} \) 变为自适应加权形式：\( L_{final} = \sum_{j} \left( \frac{1}{2\sigma_j^2} L_j + \log \sigma_j \right) \)。
        -   **效果**：该策略允许模型在训练初期优先学习简单的步骤，随着能力提升，再逐步将重心转移到更难的任务上，实现课程学习式的动态优化。

### **3. 实验设计**

-   **数据集**：实验在三个主流的、具有挑战性的多跳问答基准数据集上进行：
    -   **2WikiMultiHopQA**
    -   **HotpotQA**
    -   **MuSiQue**
-   **评估指标**：使用精确匹配（EM）、F1 分数和准确率（Acc）进行评估。
-   **对比方法（Baselines）**：
    -   **上下文学习**：包括无检索、单步检索（如 Vanilla-RAG）、多步检索（如 ITER-RETGEN, IRCoT, Self-Ask, ReAct）的直接LLM推理。
    -   **知识蒸馏**：包括针对单步检索（SAIL, KARD, CoN）和多步检索（Self-RAG, Vanilla-KD）的 KD 方法。其中，**Vanilla-KD** 是核心对比基线，它用最终步骤的完整推理路径监督学生模型。

### **4. 资源与算力**

-   **核心模型**：教师模型为 Llama3.1-Instruct 70B，学生模型为 Llama3.1-Instruct 8B。
-   **硬件配置**：使用 **4 × A100 GPU** 进行训练。
-   **优化技术**：采用 DeepSpeed ZeRO Stage 3 和梯度检查点技术以减少显存消耗。
-   **训练细节**：学习率为 \( 5 \times 10^{-6} \)，训练 2 个 epoch，并使用了余弦退火调度器和线性预热。**文中未明确给出具体总训练时长**。

### **5. 实验数量与充分性评估**

-   **实验数量**：实验设计全面且丰富，包括：
    1.  **主实验**：在3个数据集上对比了大量基线方法。
    2.  **消融研究**：分析了使用不同步骤数据对三种推理能力的影响；对比了固定加权与自适应难度加权的效果。
    3.  **泛化性实验**：验证了StepER在另一种多步检索框架（Self-Ask）上的适用性。
    4.  **模型扩展性实验**：在Qwen2.5的不同规模模型（0.5B-7B）上验证效果。
    5.  **分析性实验**：评估了推理质量（G-Eval）、推理链有效性（SubQA）、跨领域迁移能力，以及效率与精度的权衡。
-   **充分性与公平性**：
    -   **充分性**：实验覆盖从核心性能、内部机制、可扩展性到外部泛化性的多个维度，论证非常充分。
    -   **客观公平性**：对比的基线方法覆盖全面，且统一使用 Llama3.1-Instruct 作为基础模型，保证了比较的公平性。

### **6. 主要结论与发现**

-   **性能显著提升**：StepER 在所有数据集上均优于现有 KD 方法，平均准确率比 Vanilla-KD 提升了约 **9.5%**。
-   **以小博大**：StepER 蒸馏的 8B 模型性能可媲美 70B 的教师模型，有效缩小了模型规模带来的性能差距。
-   **分步数据有效性**：实验证明，同时利用初始、中间和最终步骤的数据进行训练，能系统性提升模型的推理初始化、扩展和聚合能力。
-   **难度感知训练有效**：动态自适应加权策略优于任何固定权重的训练方式，证实了课程式学习在多步推理蒸馏中的价值。
-   **强泛化能力**：StepER 不仅适用于不同的多步检索框架，还在跨领域迁移和不同规模模型上表现出色，展示了其通用性和鲁棒性。

### **7. 优点与亮点**

-   **方法论创新与洞察**：
    -   明确界定并解决了多步推理 KD 中被忽视的“步骤特异性需求”问题，思想深刻。
    -   将推理过程分解为初始化、扩展、聚合三个阶段，与人类认知过程相呼应，设计合理。
-   **技术设计精巧**：
    -   **分步监督**自然地将复杂的整段推理转化为一系列由简到繁的子任务。
    -   **难度感知训练**通过可学习参数实现了任务权重的动态平衡，方法优雅且无需手动调参。
-   **实验严谨全面**：消融实验、泛化性验证、可扩展性分析等设计，强有力地支撑了论文的核心论断。
-   **模型无关性**：该方法可灵活应用于基于推理路径（如 IRCoT）或问题分解（如 Self-Ask）等不同范式的多步RAG模型。

### **8. 不足与局限**

-   **教师模型依赖与错误传播**：学生模型能力受限于教师模型生成的推理数据质量。过滤策略仅基于最终答案是否正确，无法排除推理过程错误但答案凑巧正确的“歪打正着”样本，可能导致错误推理模式的传播。
-   **训练效率与成本**：虽然本文提升了小模型的推理性能，但构造分步数据集和进行多任务训练的过程本身计算开销较大。
-   **框架复杂度**：相比于简单的 Vanilla-KD，StepER 的实现和训练流程更为复杂。
-   **局限性未充分探讨**：论文在局限性部分提到，未来可考虑更细粒度的步骤级别过滤，以及结合参数高效微调（PEFT）方法，暗示了当前版本在这些方面尚有提升空间。

（完）
