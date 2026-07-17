---
title: "s3: You Don’t Need That Much Data to Train a Search Agent via RL"
title_zh: s3：无需大量数据即可通过RL训练搜索智能体
authors: "Pengcheng Jiang, Xueqiang Xu, Jiacheng Lin, Jinfeng Xiao, Zifeng Wang, Jimeng Sun, Jiawei Han"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1095.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 通过RL训练轻量级、模型无关的搜索智能体，执行多轮检索并与生成解耦
tldr: 训练RAG搜索智能体通常需要大量数据并将检索与生成耦合，限制了实用性。s3提出一种模型无关的轻量框架，将搜索器与生成器完全解耦，仅利用少量数据与环境奖励训练一个独立的搜索策略。该策略可直接与任意冻结大模型协同工作，执行多轮交互式检索。实验显示，s3用极少数据训练的搜索器在多个知识密集型任务中达到甚至超越全模型微调的性能，极具实用价值。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 755, \"height\": 1038, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1650, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1630, \"height\": 877, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 784, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1649, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 1372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 779, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1095/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 790, \"height\": 591, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 1535, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1657, \"height\": 916, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1460, \"height\": 701, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1095/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1535, \"height\": 1800, \"label\": \"Table\"}]"
motivation: 现有搜索智能体训练需大量数据或全模型微调，检索与生成耦合限制实用性。
method: 提出s3框架，解耦搜索与生成，仅训练轻量搜索器，通过环境奖励进行RL训练。
result: 使用极少数据训练的搜索器在多轮检索中取得优异性能，兼容不同生成模型。
conclusion: 解耦搜索与生成并利用环境奖励能高效训练RAG搜索智能体。
---

## Abstract
Retrieval-augmented generation (RAG) systems empower large language models (LLMs) to access external knowledge during inference. Recent advances have enabled LLMs to act as search agents via reinforcement learning (RL), improving information acquisition through multi-turn interactions with retrieval engines. However, existing approaches either optimize retrieval using search-only metrics (e.g., NDCG) that ignore downstream utility or fine-tune the entire LLM to jointly reason and retrieve—entangling retrieval with generation and limiting the real search utility and compatibility with frozen or proprietary models. In this work, we propose **s3**, a lightweight, model-agnostic framework that decouples the searcher from the generator and trains the searcher using a Gain Beyond RAG reward: the improvement in generation accuracy over naïve RAG. **s3** requires only 2.4k training samples to outperform baselines trained on over 70 × more data, consistently delivering stronger downstream performance across six general QA and five medical QA benchmarks.

---

## 论文详细总结（自动生成）

好的，我将严格遵循您的要求，对这篇论文进行结构化、深入、客观的总结。

### 1. 核心问题与研究背景

论文关注的是如何高效地训练**面向检索增强生成（RAG）的搜索智能体**。现有方法存在两大局限：
*   **目标不一致**：基于检索指标（如NDCG）优化的智能体，忽略了检索结果对下游生成任务的实际效用。
*   **模块耦合度高**：通过强化学习进行端到端（检索+生成）微调的方法，不仅将搜索能力与生成能力粗暴绑定，难以兼容冻结或闭源的生成模型，而且需要海量训练数据。
*   **核心矛盾**：如何设计一种轻量、解耦的框架，用极少的数据和算力，训练出一个能显著提升任意生成模型输出质量的搜索智能体。

### 2. 方法论：s3 框架

该工作的核心思想是完全解耦搜索器与生成器，并设计了一个直接反映生成质量提升的奖励信号。

*   **框架架构**：提出 **s3**（Optimized Search-Select-Serve Flow）框架，由一个可训练的搜索策略和一个冻结的生成模型组成。
*   **多轮搜索-选择循环**：
    *   搜索器基于问题进行初始化，并在每轮迭代中依次执行**查询生成**、**检索文档**、**选择关键文档**、**判断是否终止**四个步骤。
    *   通过`<query>`, `<information>`, `<important_info>`, `<search_complete>`等结构化标签，引导模型进行可控的交互式搜索。
    *   最终，所有被选中的文档`Ds3`被拼接为上下文，传递给冻结的生成器产生最终答案。
*   **训练信号：超越RAG增益奖励**：
    *   提出一种新颖的奖励信号：`GBR(Q) = Acc(G(Q, Ds3), A) - Acc(G(Q, DRAG), A)`。
    *   其中，`Acc`是任务特定的生成准确率，`A`是标准答案，`DRAG`是原始问题直接检索得到的朴素RAG上下文。
    *   该信号直接量化了**搜索器带来的上下文质量提升**，而非中间检索指标或答案的表面形式匹配。
*   **策略优化**：采用**近端策略优化**算法对搜索策略`πs3`进行训练。通过预计算并过滤掉朴素RAG已能正确回答的样本，使训练专注于搜索能带来增益的困难问题。

### 3. 实验设计

*   **数据集与基准**：
    *   **训练集**：从Natural Questions和HotpotQA中筛选出朴素RAG无法回答的困难样本，仅构成**2.4k**的训练集。
    *   **评估基准**：在**六个通用领域QA**（如NQ, TriviaQA, HotpotQA, 2WikiMultihopQA等）和**五个医学领域QA**（如MedQA-US, PubMedQA等）上进行测试。医学领域评估采用两种知识库设定（仅维基百科和维基百科+PubMed+教科书）。
*   **评估指标**：提出**生成准确率**，这是一种结合了快速词元匹配和LLM语义评判的复合指标，用以解决传统精确匹配指标过于僵化的问题。
*   **对比方法**：与三大类方法进行了全面对比：
    *   **端到端微调**：完全微调模型的Search-R1等。
    *   **静态检索 + 冻结生成器**：RAG-BM25/E5，以及优化检索指标的DeepRetrieval。
    *   **主动检索 + 冻结生成器**：通过提示或训练进行多轮检索的IRCoT、Search-o1、Search-R1 (仅提取其检索结果)。
    *   在各种方法中使用了不同型号的生成器（如Qwen2.5-7B/14B, Claude-3-Haiku）进行测试。

### 4. 资源与算力

*   **硬件**：训练和评估均在**五块NVIDIA A100 80GB PCIe GPU**上进行。
*   **训练效率**：
    *   s3 **单个训练步长耗时较长（5.7分钟）**，因为在训练中需要调用冻结的LLM来动态计算奖励。
    *   然而，得益于极高的数据效率，s3仅需**20个PPO步**（总计约2.4k样本）即可收敛，总训练时间约为**114分钟**。
    *   与之形成鲜明对比的是，Search-R1训练需要约2100步，总时间约3780分钟。s3的**总计算/时间成本降低了一个数量级（约33倍）**。

### 5. 实验充分性分析

论文进行了相当充分和细致的实验，以验证其主张。

*   **多维度对比**：在11个不同领域和复杂度的QA数据集上，与10余种方法进行了比较，涵盖了端到端、静态检索、主动检索等多种范式。
*   **鲁棒性验证**：使用了三个不同的冻结生成器评测性能，充分证明了s3的模型无关性。
*   **消融研究**：详细分析了**检索文档数、搜索轮数、文档选择模块**以及**“从问题开始搜索”**这一初始化策略的影响，验证了每个组件的贡献。
*   **奖励函数分析**：对比了使用不同指标（LLMJudge, GenAcc, Span, EM）作为奖励函数的性能差异，说明了选择生成质量感知奖励的重要性。
*   **过程分析**：展示了训练奖励曲线和具体案例的搜索轨迹，直观地呈现了策略的学习过程和效果。
*   **公平性**：为所有多轮对比方法设定了相同的最大搜索轮数和上下文长度限制，确保了对比的公正性。

### 6. 主要结论与发现

*   **解耦优化优于端到端**：仅优化搜索器的s3，其性能显著优于联合优化搜索和生成的Search-R1，表明RAG的性能增益主要源于更好的搜索，而非生成能力的对齐。
*   **极致的样本效率**：s3仅用2.4k训练样本就能超越用70k乃至170k样本训练的基线模型，证明了聚焦于生成增益的奖励信号的有效性。
*   **强大的领域泛化能力**：在通用领域QA上训练的策略，可零样本迁移到医学领域并取得最佳性能，显示出强化学习所培养出的搜索技能具有更强的泛化性。
*   **模块化设计优势**：s3的轻量、解耦特性使其能作为即插即用的组件，服务于任意冻结的、甚至是黑盒的生成式语言模型。

### 7. 优点与亮点

*   **新颖的奖励设计**：“超越RAG增益”信号，将优化目标从“如何找得全/准”直接转变为“如何让最终生成变得更好”，直击RAG系统的核心痛点。
*   **优雅的框架设计**：将搜索与生成干净地解耦，不仅使训练变得高效轻量，还极大增强了框架的通用性和灵活性。
*   **极强的实证性能**：以极低的训练成本和数据需求，在广泛的基准上超越了众多参数量更大、训练成本更高的模型，这一成果令人印象深刻。提出的生成准确率指标对RAG领域的评估也有参考价值。

### 8. 不足与局限

*   **对基础生成器的依赖**：框架的有效性建立在存在一个能力较强的冻结生成器之上，若生成器本身难以有效利用外部知识，搜索器的增益将无法充分体现。
*   **奖励计算开销**：训练时的奖励计算依赖于LLM的生成和评判，这导致单步训练时间显著长于检索优化等方法。其效率优势主要源于极少的训练步数。
*   **应用场景局限**：论文主要在短文本问答场景下验证，其架构和奖励机制在长文本生成、开放对话等任务上的适用性有待考察。
*   **潜在的社会偏见**：论文也指出，作为检索增强系统，s3的性能和安全性会继承其搜索库和生成器中固有的偏差，在敏感领域部署时需谨慎。

（完）
