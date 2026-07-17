---
title: "Data-Centric Perspectives on Agentic Retrieval-Augmented Generation: A Survey"
title_zh: 以数据为中心的智能体检索增强生成视角：综述
authors: "Jingwen Deng, Jihao Huang, Zhen Hao Wong, Hao Liang, Quanqing Xu, Bin Cui, Wentao Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.78.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 从数据视角综述智能体检索增强生成
tldr: 智能体RAG通过任务分解与迭代检索突破传统RAG局限，但其发展受数据瓶颈制约。本综述首次从数据中心视角系统梳理智能体RAG，涵盖现有数据集、数据构建方法以及数据与模型的协同设计，旨在揭示数据需求与工具，为构建数据高效的智能体RAG系统提供全面参考。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.78/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 823, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.78/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1535, \"height\": 512, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 417, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 776, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 787, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1616, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1604, \"height\": 1395, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.78/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1601, \"height\": 2549, \"label\": \"Table\"}]"
motivation: 智能体RAG面临数据稀缺，阻碍其快速发展。
method: 综述现有数据集、构建方法和数据-模型协同设计进展。
result: 识别出关键数据瓶颈和未来研究方向。
conclusion: 为数据高效型智能体RAG的开发提供了系统指引。
---

## Abstract
Large Language Models (LLMs) excel at natural language understanding and generation, yet their reliance on static pre-training corpora may lead to outdated knowledge, hallucinations, and limited adaptability. Retrieval-Augmented Generation (RAG) mitigates these issues by grounding model outputs with external retrieval, but conventional RAG remains constrained by a fixed retrieve-then-generate routine and struggles with multi-step reasoning and tool calls. **Agentic RAG** addresses these limitations by enabling LLM agents to actively decompose tasks, issue exploratory queries, and refine evidence through iterative retrieval. Despite growing interest, the development of Agentic RAG is impeded by *data scarcity*: unlike traditional RAG, it requires challenging tasks that require planning, retrieval, and multiple reasoning decisions, and corresponding rich, interactive agent trajectories. This survey presents the first data-centric overview of Agentic RAG, framing its data lifecycle—data collecting, data preprocessing and task formulation, task construction, data for evaluation, and data enhancement for training—and cataloging representative training datasets and benchmarks in different domains (e.g. question answering, web, software engineering). From data perspectives, we aim to guide the creation of scalable, high-quality datasets for the next generation of adaptive, knowledge-seeking LLM agents. The project page is at https://github.com/fatty-belly/Awesome-AgenticRAG-Data/.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将以中文、Markdown 格式，对这篇名为《Data-Centric Perspectives on Agentic Retrieval-Augmented Generation: A Survey》的论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：本文的核心论点是，**数据瓶颈**是当前阻碍**智能体检索增强生成（Agentic RAG）** 系统发展的关键因素。传统的RAG依赖静态的“查询-文档”对，而Agentic RAG则需要包含规划、多步推理、工具调用和迭代检索的复杂任务以及丰富的交互轨迹数据。这类数据获取成本高、难以规模化且自动合成时容易出现质量问题。
*   **研究动机与背景**：
    *   **背景**：LLM存在知识过时和幻觉问题，传统RAG的“检索-生成”固定流程无法应对需要多步推理和主动探索的复杂任务。
    *   **动机**：Agentic RAG通过让智能体自主分解任务、迭代检索和验证信息，能有效弥补传统RAG的不足。然而，该领域的研究如雨后春笋，却缺乏一个从**数据视角**出发的系统性梳理，来指导如何构建高质量、可扩展的数据集以驱动下一代自适应智能体的发展。
*   **整体含义**：本文是首篇以数据为中心的Agentic RAG综述，旨在系统性地审视其数据生命周期，总结数据集的构建方法，并对现有基准进行编目，从而为研究者创建下一代知识寻求型LLM智能体提供数据层面的指引，推动该领域从“模型驱动的架构创新”转向“数据驱动的能力突破”。

### 2. 论文提出的方法论：数据生命周期与构建流程

本文并非提出一个新的Agentic RAG模型，而是**提出了一个分析和构建Agentic RAG数据的系统化框架**，具体包括两大核心部分：

*   **2.1 数据生命周期框架**
    论文将Agentic RAG的数据处理过程划分为五个关键阶段，形成一个完整的生命周期：
    1.  **数据收集**：区分了**静态数据**（如维基百科、GitHub代码库的快照）和**交互数据**（如实时API调用、网页浏览轨迹）。后者对Agentic RAG至关重要。
    2.  **数据预处理与任务定义**：将原始语料清洗、分段，并构建结构化的知识库；同时，根据下游目标（如代码修复、论文撰写）将任务定义为封闭式或开放式，并关联相应的检索工具。
    3.  **任务构建**：这是核心环节，文中提出了一个 **“生成-验证-过滤/精炼”** 的流水线来合成或增强任务。
    4.  **评估数据**：强调评估前必须进行**数据去污**，并提出了超越“正确性”的多维度评估指标。
    5.  **训练数据增强**：根据有监督微调（SFT）或强化学习（RL）的不同范式，对数据进行针对性增强。

*   **2.2 任务构建的核心流程：“生成-验证-过滤/精炼”**
    *   **生成**：利用LLM或人工标注生成任务。为解决模型能力饱和问题，重点总结了**难度增强**的三种策略：
        *   **复杂度增强**：将单轮问答扩展为多轮、多跳、需多工具调用的任务。
        *   **不确定性增强**：引入模糊信息、隐性推理步骤或干扰项，迫使模型进行更深层次推理。
        *   **专业性增强**：创建需要特定领域专家知识的任务（如GPQA, Humanity’s Last Exam），这些任务通常超出了模型预训练语料的覆盖范围。
    *   **验证**：确保生成数据的有效性。包括人工交叉验证和基于LLM的自动化验证（如思想链验证），检查任务是否具有唯一答案、代码是否可复现等。
    *   **过滤/精炼**：从两个维度优化数据集：
        *   **质量**：过滤掉语言不自然、不稳健或包含数据泄露捷径的任务。
        *   **难度**：利用规则（如推理跳数）或LLM代理得分来过滤简单任务，实现课程学习。

### 3. 实验设计：数据与场景

*   **使用的数据集/场景**：本文是综述，因此其分析涵盖了横跨多个领域的众多数据集和基准，而非进行统一的实验。
    *   **问答**：从传统单跳基准（NQ, TriviaQA）到复杂的多跳基准（HotpotQA, MuSiQue）和近期挑战性更强的任务（SimpleQA, GPQA）。
    *   **Web**：从WebArena、GAIA等需要多模态交互的环境，到BrowseComp、WebWalkerQA等侧重信息搜寻与推理的网络任务。
    *   **软件工程**：主要集中在仓库级别的代码修复和生成任务，如SWE-bench、RepoBench。
    *   **科研、医疗、法律**：分别对应MLE-bench、MedQA、LegalBench等，代表了需要深度领域知识、长程规划和工具使用的复杂场景。
*   **对比的方法/基准**：本文的对比发生在概念层面，即对比了**“传统RAG”** 与 **“Agentic RAG”** 在数据生命周期的各个阶段所需数据的不同特征（如表1所示），以及对比了**不同任务构建方法**（如复杂度、不确定性、专业性增强）的动机和效果。

### 4. 资源与算力

*   本文作为一篇综述论文，**并未**使用任何计算资源来训练或评估模型。它不涉及具体的GPU型号、数量或训练时长。其核心贡献在于理论框架的构建和知识体系的梳理，而非实证计算。

### 5. 实验数量与充分性

*   **实验数量**：论文**没有进行传统意义上的实验**。它的主要工作是回顾、分析、归纳和分类了数十篇现有文献中的数据集、基准和构建方法，并在附录中提供了详细的基准特征表。
*   **充分性与客观性**：作为一篇文献综述，其“实验”的充分性体现在文献覆盖的广度和分类的合理性上。论文系统性地引用了大量高质量和近期的工作，覆盖面广。其分类框架（数据生命周期、“生成-验证-过滤/精炼”流程、难度增强三策略）逻辑清晰，为分析现有工作提供了客观的视角。然而，综述的结论部分依赖于作者对现有工作的解读和提炼，不可避免地带有一定的主观性。它没有通过“公平”的实证对比来证明某种数据构建方法优于另一种，而是定性地指出不同方法的适用场景和优缺点。

### 6. 论文的主要结论与发现

*   **数据是Agentic RAG发展的核心瓶颈**：高质量、包含丰富交互轨迹的数据极度稀缺，是当前面临的首要挑战。
*   **从“静态”到“交互”的范式转变至关重要**：Agentic RAG需要的数据模式已从传统RAG的静态“查询-文档”对，转变为动态的、包含规划与工具调用历史的“智能体-环境交互轨迹”。
*   **提出了一个系统化的数据构建框架**：“生成-验证-过滤/精炼”流水线与“复杂度、不确定性、专业性”三位一体的难度增强策略，为构建下一代Agentic RAG数据集提供了可操作的方法论。
*   **评估需超越“正确性”**：仅靠最终答案匹配来评估Agentic RAG系统是不足的，必须引入效率、安全性等多维度指标，并重视过程奖励和评估稳健性。
*   **未来方向**：识别了四个关键的挑战和开放问题，包括数据质量、评估复杂性、评估稳健性以及从无状态检索向持久化AI记忆的演进。

### 7. 优点：方法或实验设计上的亮点

*   **视角新颖**：首次从以数据为中心的全新视角切入，对Agentic RAG这一热门领域进行系统性综述，选题精准，在当下具有极高的指导价值。
*   **框架清晰**：提出的“数据生命周期”和“生成-验证-过滤/精炼”流水线框架，为理解和构建Agentic RAG数据提供了结构化、可复用的思维模型。
*   **分类细致**：将难度增强策略分解为复杂度、不确定性和专业性，清晰揭示了现有基准在达到饱和后面临的深层挑战及应对思路。
*   **领域覆盖广**：全面梳理了问答、Web、软件工程、科研、医疗、法律等多个关键领域的代表性数据集和基准，实用性强。
*   **直指痛点**：“超越正确性”的评估讨论非常深刻，指出了当前评估体系的根本缺陷，为未来研究指明了方向。

### 8. 不足与局限

*   **缺乏量化分析**：作为定性综述，论文未能对不同数据构建策略的效果进行大规模的量化元分析或实证对比，读者无法直观了解哪种策略在提升特定能力上更有效。
*   **可能存在的遗漏与偏差**：尽管覆盖面广，但由于论文发表时间（2026年7月），可能遗漏了该时间点之后或同时期的一些前沿工作。对某些方法的分析可能基于有限的研究实例，存在采样偏差。
*   **不涉及多模态数据**：论文在“Limitations”部分明确指出，其关注点主要是文本数据，未深入探讨多媒体数据（如学术论文中的图表、视频）的构建流程，这限制了其在多模态Agentic RAG领域的直接应用。
*   **应用落地指导有限**：论文侧重于学术研究和基准构建，对于如何将这套数据框架有效迁移到特定工业场景、如何评估数据质量的投资回报率等现实问题，讨论尚不深入。
*   **优化目标的局限性**：虽然提出了超越正确性的评估，但对于如何量化“效率-准确性”的平衡、如何通过数据设计来引导这一平衡，缺乏更具体的案例或准则。

（完）
