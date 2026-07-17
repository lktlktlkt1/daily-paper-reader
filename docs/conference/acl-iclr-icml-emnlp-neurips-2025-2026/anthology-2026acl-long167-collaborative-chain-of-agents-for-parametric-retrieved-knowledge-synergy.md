---
title: Collaborative Chain-of-Agents for Parametric-Retrieved Knowledge Synergy
title_zh: 协同智能体链：参数化与检索知识的协同
authors: "Yi Jiang, Sendong Zhao, Jianbo Li, Haochun Wang, Lizhe Zhang, Yan Liu, Bing Qin (秦兵)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.167.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 多智能体RAG框架融合参数化与检索知识
tldr: 现有RAG方法难以充分利用参数化知识与检索知识的协同，提出协同智能体链框架，通过多智能体协作先进行条件知识归纳再生成，在知识密集型任务中显著提升生成准确性。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1602, \"height\": 678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 714, \"height\": 228, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 728, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 722, \"height\": 270, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 295, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 780, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1585, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1537, \"height\": 1784, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1553, \"height\": 1857, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.167/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1531, \"height\": 1791, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1614, \"height\": 909, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 792, \"height\": 349, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 791, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 773, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 755, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1462, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1544, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1509, \"height\": 716, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1502, \"height\": 361, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.167/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1661, \"height\": 2053, \"label\": \"Table\"}]"
motivation: RAG中参数化知识与检索知识协同不足，检索内容可能误导生成。
method: 设计协同智能体链，包含CoCoA-zero等多智能体模块，通过条件知识归纳显式融合两类知识。
result: 在多种知识密集型任务上，CoCoA框架优于单智能体RAG和现有融合方法。
conclusion: 多智能体协同机制有效释放了参数与检索知识的互补潜力。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models (LLMs), especially for knowledge-intensive tasks. Despite its advantages, current RAG methods often struggle to fully exploit knowledge during generation. In particular, the synergy between the model’s internal parametric knowledge and external retrieved knowledge remains limited. Retrieved contents may sometimes mislead generation, while certain generated content can guide the model toward more accurate outputs. In this work, we propose Collaborative Chain-of-Agents, a framework designed to enhance explicitly synergy over both parametric and retrieved knowledge. Specifically, we first introduce CoCoA-zero, a multi-agent RAG framework that first performs conditional knowledge induction and then reasons answers. Building on this, we develop CoCoA, a long-chain training strategy that synthesizes extended multi-agent reasoning trajectories from CoCoA-zero to fine-tune the LLM. This strategy enhances the model’s capability to explicitly integrate and jointly leverage parametric and retrieved knowledge. Experimental results demonstrate the superiority of CoCoA in open-domain QA and multi-hop QA.

---

## 论文详细总结（自动生成）

好的，以下是根据论文内容生成的结构化中文总结。

## 论文核心问题与整体含义
- **核心问题**：当前检索增强生成（RAG）方法未能充分发挥模型内部参数化知识与外部检索知识之间的协同效应（Synergy）。模型要么过度依赖检索内容，容易受噪声误导，要么完全依赖内部知识，忽略了外部信息。
- **整体含义**：本研究旨在提出一种框架，显式地融合并协同两类知识（参数化与检索），从而在知识密集型的问答任务中，提升大语言模型（LLM）生成答案的准确性和鲁棒性。

## 方法论
- **核心思想**：通过“多智能体链”架构，将知识归纳和推理决策过程解耦并协调起来，形成一种“先归纳、后决策”的协同机制。
- **技术细节**：
    1. **CoCoA-zero框架**：
        - 这是一个两阶段的零样本多智能体推理框架。
        - **第一阶段：知识归纳**。它包含两个专门的智能体：
            - **内部知识归纳智能体**：先基于问题让LLM生成候选答案，再以该答案为条件，引导LLM总结出相关的参数化知识。
            - **外部知识归纳智能体**：先基于问题和检索到的文档生成候选答案，再以此为条件，从文档中归纳出外部知识。
        - **第二阶段：高层决策**。引入一个决策智能体，基于前两个智能体生成的候选答案和归纳知识，进行思维链推理，并生成最终答案。
    2. **CoCoA训练策略**：
        - **长链监督微调**：将CoCoA-zero框架运行过程中产生的多智能体协作轨迹（内部归纳、外部归纳、思维链、最终答案）拼接成一个单一的长文本回复，作为监督信号来微调LLM。
        - **偏好优化**：采用直接偏好优化（DPO）方法，将CoCoA-zero生成的协作式回答作为“正样本”，将单智能体生成的零样本回答作为“负样本”，进一步对齐模型的偏好。

## 实验设计
- **数据集**：
    - **开放域问答（Open-domain QA）**：WebQuestions, TriviaQA。
    - **多跳问答（Multi-hop QA）**：HotpotQA, 2WikiMultiHopQA。
    - **训练集**：从HotpotQA、2WikiMultiHopQA和WebQuestions的训练集中抽样，利用CoCoA-zero合成并过滤出约6.8k样本用于监督微调。
- **基准方法**：涵盖了多类代表性方法。
    - **无检索/无训练**：LLaMA-3.1直接生成、思维链（CoT）提示、GenRead。
    - **有检索/无训练**：标准RAG、带CoT的RAG、Chain-of-Note、SURE。
    - **检索增强语言模型**：Self-RAG、DeepSeek-R1-Distill-8B、InstructRAG。
- **评估指标**：采用精确匹配（EM）和 F1 分数，报告二者平均值。

## 资源与算力
- **GPU**：所有实验均在**单张NVIDIA A100（80GB或40GB显存） GPU**上完成。
- **模型与框架**：
    - 基础模型为LLaMA3.1-8B，使用vLLM框架进行推理加速。
    - 微调采用参数高效方法，具体为使用LoRA技术。
    - 检索器为Contriever，召回文档数 `k` 默认为5。

## 实验数量与充分性
- **实验组数**：实验设计非常详尽，包括但不限于：
    - **主实验**：在4个数据集上对比了所提方法与9种基线方法的性能（表1）。
    - **消融实验**：分别移除了推理环节、内部知识归纳和外部知识归纳等组件，验证各部分的有效性（表2）。
    - **训练策略消融**：对比了长链SFT、长链DPO、短链SFT以及独立多模型短链SFT的效果（表3）。
    - **鲁棒性分析**：测试了不同检索器、不同检索文档数 `K` 对性能的影响（图8, 图6）。
    - **泛化性分析**：在非问答任务上测试了迁移性；在TriviaQA上检验了分布外泛化性；在不同规模的模型（70B）上测试了零样本框架的性能。
    - **效率与案例分析**：分析了推理成本和回答长度（表4），并进行了定性案例研究（图4, 9-11）。
- **充分性评估**：实验设计充分且客观。对比方法全面，消融研究细致，不仅验证了性能提升，还深入探讨了模型在不同条件下的鲁棒性和泛化能力，论证过程公平。

## 主要结论与发现
- **协同有效性**：通过显式地融合参数化与检索知识，CoCoA框架在多个知识密集型问答任务上均取得了最优或次优性能，验证了知识协同的必要性和巨大潜力。
- **训练范式优势**：提出的长链训练策略（尤其是结合DPO）能够有效将多智能体协同能力内化到单一模型中，其性能优于将不同能力分配给独立模型进行短链训练的方式。
- **内部知识价值**：实验表明，在强大的大模型上，利用内部参数化知识进行问答有时比使用检索信息更有效，CoCoA-zero能更好地平衡和利用这两种知识来源。
- **协同促进纠错**：定性分析发现，即使内部和外部回答同时失败，CoCoA-zero也能通过知识归纳和高层决策的交互，激发出正确回答。

## 优点
- **方法创新**：提出了一个新颖的“先归纳、后决策”多智能体协作框架，为知识协同问题提供了清晰的解决路径。
- **训练策略巧妙**：将多智能体的协作轨迹合成为长文本进行端到端训练，是一种优雅且有效的知识蒸馏和能力内化方式。
- **实验扎实全面**：实验设计覆盖了多种任务、对比了大量基线、进行了多维度的消融和鲁棒性分析，结论可信度高。
- **提供了新视角**：为推理时的知识增强和智能体协作训练领域提供了新的见解。

## 不足与局限
- **推理成本增加**：由于需要生成多段中间推理和归纳结果，CoCoA的推理成本（输出Token数）是常规RAG方法的数倍，在效率上存在劣势。
- **多智能体模式的泛化性**：当前的框架和训练策略专门针对其设计的特定协作模式，该模式是否能推广到更广泛或多样的多智能体架构仍待研究。
- **内部知识引入的幻觉风险**：尽管条件知识归纳有“二次验证”效果，但过程仍可能引入来自模型内部的幻觉，对最终决策产生负面影响。
- **规模化探索不足**：研究主要在8B规模的LLaMA3.1模型上进行，训练数据量也相对有限（约6.8k），其在更大规模模型和数据集上的表现未得到系统性探索。

（完）
