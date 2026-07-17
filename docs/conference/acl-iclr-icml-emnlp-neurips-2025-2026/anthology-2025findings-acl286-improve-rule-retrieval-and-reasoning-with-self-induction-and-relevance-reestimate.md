---
title: Improve Rule Retrieval and Reasoning with Self-Induction and Relevance ReEstimate
title_zh: 通过自引导与相关性重估计改进规则检索与推理
authors: "Ziyang Huang, Wangtao Sun, Jun Zhao, Kang Liu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.286.pdf"
tags: ["query:agentic-rag"]
score: 7.0
evidence: SIAR利用LLM自引导规则并重估计相关性以改进检索辅助推理
tldr: 规则检索中因实例化事实与抽象规则间的语义鸿沟导致检索不准，影响推理。提出SIAR，利用大语言模型自引导可能的推理性规则，并重新估计相关性，弥合语义差距，从而提升规则检索质量。实验表明该方法有效提高了检索准确率并增强了下游推理能力，为知识检索与推理的融合提供了新思路。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.286/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.286/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 682, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 1414, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1644, \"height\": 686, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 835, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1651, \"height\": 1049, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1641, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.286/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 486, \"label\": \"Table\"}]"
motivation: 规则检索面临实例事实与抽象规则间的语义鸿沟，导致检索不准、推理受损。
method: SIAR利用LLM自引导潜在推理规则，并重新估计检索相关性，提升检索质量。
result: 实验表明SIAR显著提高了规则检索准确率和下游推理性能。
conclusion: 自引导与相关性重估计能有效弥合语义鸿沟，增强检索增强推理。
---

## Abstract
This paper systematically addresses the challenge of rule retrieval, a crucial yet underexplored area. Vanilla retrieval methods using sparse or dense retrievers to directly search for relevant rules to support downstream reasoning, often suffer from low accuracy. This is primarily due to a significant semantic gap between the instantiated facts in the queries and the abstract representations of the rules. Such misalignment results in suboptimal retrieval quality, which in turn negatively impacts reasoning performance. To overcome these challenges, we propose Self-Induction Augmented Retrieval (SIAR), a novel approach that utilizes Large Language Models (LLMs) to induce potential inferential rules that might offer benefits for reasoning by abstracting the underlying knowledge and logical structure in queries. These induced rules are then used for query augmentation to improve retrieval effectiveness. Additionally, we introduce Rule Relevance ReEstimate (R 3 ), a method that re-estimates the relevance of retrieved rules by assessing whether the abstract knowledge they contain can be instantiated to align with the facts in the queries and the helpfulness for reasoning. Extensive experiments across various settings demonstrate the effectiveness and versatility of our proposed methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **规则检索的困境**：在基于规则推理的场景（如法律、医疗、逻辑问答）中，给定一个包含实例化事实的查询（如“Alice 搬到了加州，加州的新环境法要求回收”），需要从规则库中检索出能为推理提供支撑的抽象规则（如“若某人搬到某地且该地适用某法律，则需遵守该法律”）。传统搜索方法（稀疏 BM25、稠密检索）直接对查询和规则进行匹配，但由于查询是具体的、实例化的，而规则是抽象的、用变量和谓词表达的，两者之间存在显著语义鸿沟，导致检索准确率低。
- **研究动机**：实验表明，若直接给模型提供“黄金规则”，下游推理性能可大幅提升（7B 模型提升 31.54%，72B 提升 23.67%），但现有检索方法非但无法提供这种帮助，其返回的不相关或噪声规则反而会使推理性能下降到低于“不使用规则”的水平，形成性能瓶颈。因此，需要专门针对规则检索的语义对齐和相关性评估问题提出解决方案。

### 2. 论文提出的方法论

核心思想是通过大语言模型（LLM）缩小查询与规则之间的语义差异，并重新评估检索结果的相关性。

- **SIAR：自引导增强检索**
  - **步骤**：在检索前，利用 LLM 从查询中自我归纳（self-induction）出一条潜在的推理规则。该规则对查询中的事实进行抽象，总结其内在知识和逻辑结构，猜测可能的推导关系。
  - **原理**：查询所在的事实子空间与规则所在的抽象子空间几乎不重叠。自我归纳相当于将查询尽可能投影到规则子空间，生成的新查询（自引导规则）与原规则在语义上更匹配。
  - **查询形式**：生成的自引导规则可单独作为新查询（`w/ SI`），或与原查询拼接后作为新查询（`w/ SI + input`）。实验显示，稠密检索更适仅用自引导规则，稀疏检索更适合拼接后的查询。

- **R³：规则相关性重估计**
  - **插入点**：在 SIAR 获得初始检索结果（top-n）之后，调用 LLM 对结果列表进行重排序。
  - **评估原则**：1) 规则中的抽象知识能否被实例化为查询中的事实；2) 规则是否可以被应用到查询上，为推理提供帮助。
  - **实现方式**：采用类似 RankGPT 的思路，用提示词指导 LLM 一次性输出全部规则的相关性排序（`[2] > [1] ...`），从中选取 top-k 作为最终结果。该过程无需训练，仅依赖提示。

### 3. 实验设计

- **数据集**：
  - 两个合成数据集：**CLUTRR**（1,048 条规则）、**ULogic**（830 条规则）；
  - 一个真实场景数据集：**CAIL2018**（法律判决预测，166 条规则）。
  - 每个数据集构建自然语言规则库和形式语言规则库，以测试不同规则格式的影响。

- **检索器与模型**：
  - 稀疏检索：BM25（Pyserini 实现）。
  - 稠密检索：`bge-base-en` 编码器。
  - 推理与自引导/重排序 LLM：**GPT-4o**、**Qwen2.5-7B-Instruct**、**Qwen2.5-72B-Instruct**；消融实验还扩展了 **Llama-3.1-8B**、**Yi-1.5-6B**。
  - 生成式检索模型对比：`bge-gemma2`（9B 参数 LLM retriever）。

- **评估指标**：检索指标用 `Recall@1,5,10`；推理指标用 `Match`（生成答案中包含标准答案即视为正确）。

- **对比基线**：
  - 推理基线：Direct（直接回答）、Golden rule（提供黄金规则）、CoT（思维链）、Self-Induction（仅用自引导规则推理，不检索）。
  - 检索基线：vanilla retrieval（原始查询检索）、vanilla retrieval + R³（原始查询检索后直接重排序）。

- **实验组合**：全面对比了不同检索器（稀疏/稠密）、规则格式（自然语言/形式语言）、查询形式（w/ SI / w/ SI + input）以及不同参数规模模型下的性能。

### 4. 资源与算力

论文未明确提及训练所用的 GPU 型号、数量或训练时长。该方法**无训练环节**，所有操作均基于 LLM 的提示（零样本或少样本），仅需推理资源。文中提到使用 **VLLM** 框架加速 LLM 推理，但未给出具体硬件配置。稠密检索使用轻量级 `bge-base` 模型，没有进行微调。因此，算力消耗主要体现在 LLM 的 API 调用或本地推理上，但未被量化。

### 5. 实验数量与充分性

- **实验组次丰富**：从表格看，论文覆盖了 3 个数据集 × 2 种规则格式 × 2 种检索器 × 3 个主测模型 × 多种方法变体（vanilla, SIAR, SIAR-R³ 等），合计超过百组对比。
- **消融/附加实验**：
  - **不同模型架构**：除 Qwen 系列外，补充了 Llama 和 Yi 模型。
  - **不同检索器类型**：验证了稀疏、稠密、LLM 检索器。
  - **规则数量压力测试**：在 ULogic 基础上增加反事实规则（规则量翻倍），检验方法鲁棒性。
  - **查询形式对比**：对比了仅用自引导规则与拼接原始查询的效果。
- **公平性**：所有对比均在相同推理模型和数据集上进行，检索指标与推理指标均采用标准方法计算；不使用任何外部监督信号，只依赖 LLM 自身能力。实验设计客观、全面。

### 6. 论文的主要结论与发现

- **语义鸿沟确实存在**：直接检索规则用于推理，可能使性能低于不使用任何规则，嘈杂的规则会干扰 LLM。
- **SIAR 有效弥合语义差距**：通过自我归纳生成抽象规则进行查询增强，在所有数据集和检索器组合下均能显著提升检索召回率（例如在 CLUTRR 上 Recall@1 最大提升 60.12 个百分点）。
- **R³ 可进一步提升质量**：在 SIAR 基础上对检索结果重排序，能再次提升检索和推理性能，尤其对于 ULogic 和 CAIL2018 提升显著，说明 LLM 有能力评估“规则对查询的适用性”。
- **不同查询形式适配不同检索器**：稠密检索更适合使用自引导规则（`w/ SI`），稀疏检索更适合拼接原查询（`w/ SI + input`）。
- **大模型能力更强**：72B 模型的自引导和重排序能力显著优于 7B，但在某些配置下开源模型（Qwen2.5-72B）与闭源 GPT-4o 表现相当，甚至更优。
- **方法通用性强**：在不同模型架构、不同检索器类型、不同规则语言格式下均能保持性能提升，且当规则库规模增大时仍然稳健。

### 7. 优点

- **创新性好**：首次系统分析并明确规则检索的语义错位问题，提出了“投影到规则空间”的解决思路。
- **方法简洁高效**：无需任何训练，完全基于 LLM 的提示工程实现自引导与重排序，插入成本低，易于集成。
- **理论与实践结合**：不仅提升了检索指标，还切实提高了下游推理准确率，弥合了检索与推理间的鸿沟。
- **实验扎实**：覆盖多种数据场景、多种模型、多种消融维度，结论说服力强。

### 8. 不足与局限

- **规则库规模有限**：实验中最大规则库仅 1,048 条，远小于真实世界的知识库规模。随着规则量激增，性能能否保持未知。
- **依赖 LLM 能力**：自引导规则和重排序的质量高度依赖 LLM 的归纳与判别能力，在较小或较弱的模型上收益有限（如 CLUTRR 复杂场景下 7B 模型 R³ 增益很小）。
- **计算开销**：每一条查询都需额外调用 LLM 一次（自引导）到两次（加重排序），相比直接检索增加了推理延迟和成本，但论文未做效率分析。
- **重排序的鲁棒性**：R³ 对复杂数据集（如 CLUTRR）和形式语言规则库的提升不够稳定，甚至有轻微波动。
- **评估指标单一**：推理只用了 Match，未考虑生成的合理性、忠实度等，检索也仅用了 Recall，未评估排序精度（如 MRR、NDCG）。
- **实际领域应用未深入**：虽然在 CAIL2018 上测试，但法律规则库极简（166 条），与真实法律检索差距较大，医疗等场景未有涉及。

（完）
