---
title: Shifting from Ranking to Set Selection for Retrieval Augmented Generation
title_zh: 从排序到集合选择：面向检索增强生成的段落选择转变
authors: "Dahyun Lee, Yongrae Jo, Haeju Park, Moontae Lee"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.861.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 基于思维链推理的集合式段落选择用于多跳问答
tldr: 针对RAG中检索通常只关注单篇相关性而忽略集合完整性的问题，提出集合式选择方法SetR，通过思维链推理明确查询信息需求并选择最优段落集合，在多跳RAG基准上超越强基准。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1642, \"height\": 873, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1608, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 714, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.861/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 741, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 978, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.861/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1647, \"height\": 394, \"label\": \"Table\"}]"
motivation: 单篇排序式检索难以满足复杂查询的信息完整性需求。
method: 设计SetR，利用思维链推理显式界定查询信息需求，进行集合式段落优选。
result: 在多跳RAG基准上，SetR显著优于基于LLM的排序器和开源基准。
conclusion: 集合选择策略为复杂RAG任务提供了更全面的证据支撑。
---

## Abstract
Retrieval in Retrieval-Augmented Generation (RAG) must ensure that retrieved passages are not only individually relevant but also collectively form a comprehensive set.Existing approaches primarily rerank top- k passages based on their individual relevance, often failing to meet the information needs of complex queries in multi-hop question answering.In this work, we propose a set-wise passage selection approach and introduce SetR, which explicitly identifies the information requirements of a query through Chain-of-Thought reasoning and selects an optimal set of passages that collectively satisfy those requirements.Experiments on multi-hop RAG benchmarks show that SetR outperforms both proprietary LLM-based rerankers and open-source baselines in terms of answer correctness and retrieval quality, providing an effective and efficient alternative to traditional rerankers in RAG systems.The code is available at https://github.com/LGAI-Research/SetR

---

## 论文详细总结（自动生成）

# 论文核心问题与整体含义

- **研究动机**：在检索增强生成（RAG）系统中，传统段落重排序方法只关注单一段落的**个体相关性**，往往忽视检索结果作为一个**集合的整体性**——即段落之间是否互补、覆盖是否全面、是否有冗余。
- **问题聚焦**：对于多跳问答等复杂查询，仅凭相关性排序容易导致信息碎片化或关键证据缺失，影响最终答案的正确性。
- **整体含义**：把RAG中的段落选择从“排序并取Top‑k”转向“集合级选择”，能更有效地满足生成模型对信息**完整性、多样性与简洁性**的需求。

# 论文提出的方法论

## 核心思想
- 将段落检索定义为**基于信息需求的集合选择任务**，而非顺序重排序。
- 通过**思维链（Chain‑of‑Thought, CoT）推理**显式分解查询为若干信息子目标，再依据这些子目标筛选出最优段落集合。

## 关键技术细节（SetR）
1. **信息需求识别（IRI）**  
   设计提示词，引导大模型（教师模型）分三步推理：
   - 列出回答查询所需的关键信息需求；
   - 为每一需求在候选段落中寻找包含相关信息的段落；
   - 从整体出发，选出覆盖最全面、信息最多样的段落子集（节数不限）。
2. **模型蒸馏**  
   - 用 GPT‑4o 对 MS MARCO 的 40K 训练样本生成集合选择结果与推理过程，作为教师标签。
   - 以 Llama‑3.1‑8B‑Instruct 为基座，通过监督微调得到轻量级的 SetR。
   - 为消融分析，设计了三种变体：
     - `SetR‑Selection only`：直接输出最终选择，无推理过程；
     - `SetR‑CoT`：使用通用“Let’s think step by step”推理，但未显式识别信息需求；
     - `SetR‑CoT & IRI`：完整模型，融合 CoT 与显式信息需求识别。

## 公式或算法流程
- 输入：查询 \(q\) 和第一阶段检索得到的候选段落集合 \(C\)（通常为 top‑20）。
- 输出：一个有序或无序的段落子集 \(S^* \subseteq C\)，最大化集体信息覆盖。
- 推理步骤（在论文中以自然语言描述）：
  1. 列举需回答 \(q\) 的信息需求列表 \(\{r_1, r_2, \dots, r_m\}\)；
  2. 对每个需求 \(r_i\)，记录包含该信息的段落索引；
  3. 选择段落子集，使得不同需求的覆盖最大化且冗余最少，最终以“### Final Selection: [x] [y] …”形式输出。

# 实验设计

## 数据集 / 场景
- **多跳问答基准**：HotpotQA、2WikiMultiHopQA、MuSiQue、MultiHopRAG。
- 实验分为两类：
  - **端到端 QA 评估**：将检索/选择结果喂入生成模型，测量最终答案的正确性。
  - **检索质量评估**：在 MultiHopRAG 上单独评估段落选择本身的指标（MRR、NDCG、Precision、Recall），以及**信息覆盖率**（Hit@k、证据覆盖比例）。

## 对比方法
- 无重排序的纯检索：BM25、bge‑large‑en‑v1.5。
- 重排序器：
  - 小型交叉编码器：bge‑reranker‑large；
  - LLM 基重排序器：RankLlama、RankVicuna、RankZephyr、FirstMistral；
  - 闭源强基：RankGPT (gpt‑4o)。
- SetR 的三种变体（内部消融）。

## 实验设置
- 第一阶段检索固定为 bge‑large‑en‑v1.5 取 top‑20。
- 生成器固定为 Llama‑3.1‑8B‑Instruct（通用多跳 QA）或 gpt‑4o（MultiHopRAG 专用，因其对证据利用要求较高）。
- 公平对比：额外设计了**统一监督来源与基座模型**的对照实验，以排除蒸馏数据或模型容量的混淆。

# 资源与算力
- **训练资源**：16 张 A100 GPU。
- **训练时长**：5 个 epoch，有效 batch size 512，学习率 \(5\times10^{-6}\)，优化器 AdamW。
- **数据合成**：使用 GPT‑4o 为 40K 样本生成教师标签（推理过程 + 段落选择）。
- **推理效率**：SetR 平均仅选用 2‑3 个段落，远少于传统重排序的固定 5 个，显著降低生成器输入的 token 数。

# 实验数量与充分性
- **核心实验表**：
  - 表1：端到端 QA 主结果（4 数据集 × 多种重排/选择方法）。
  - 表2：MultiHopRAG 上的检索指标。
  - 表3：用 GPT‑4o 作为教师直接推理的方法级对比。
  - 表4：统一基座（Llama‑3.1‑8B‑Instruct）和训练数据的公平对比。
  - 表5：不同方法的 token 效率分析。
- **消融研究**：三种 SetR 变体全面对比，揭示了 CoT 和 IRI 各自的贡献。
- **深入分析**：
  - 信息覆盖率（Hit@k、证据累积）曲线；
  - 对不同数量输入段落的鲁棒性分析（增加段落能否带来提升）。
- **评价维度**：覆盖答案正确性（EM、F1、Accuracy）、检索质量（MRR、NDCG、Precision、Recall）、资源效率（输入/输出 token 量）。
- **充分性与公平性**：实验设计考虑周到，通过统一基座与教师标签的附加实验排除模型容量和蒸馏偏差，对比基线广泛且包含闭源上限，分析深入，实验相当充分和公平。

# 论文的主要结论与发现
- SetR 在几乎**所有多跳 QA 基准**上，均显著优于基于 LLM 的列表重排序器（包括 GPT‑4o）和传统重排序器，使用的段落数量却减少了 40‑50%。
- 检索质量上，SetR 在**召回率和精确率**方面提升明显（信息覆盖率从约 19% 提高到 36%），且弥补了传统重排序器不能有效累积新信息的缺陷。
- **推理组件的作用**：显式的信息需求识别（IRI）比单纯的 CoT 更能提升选择质量，两者结合达到最佳。
- **鲁棒性**：SetR 能有效过滤噪音段落，避免了传统方法中“输入段落越多、性能反而下降”的窘境。
- **效率与效果的协同**：集合选择在节约大量 token 的同时提高了最终答案的准确性。

# 优点
- **方法创新**：将 RAG 检索从段落排序范式推进到集合选择范式，更贴合生成模型对信息集合的真实需求。
- **显式推理**：通过 CoT 和信息需求列表显式地操纵段落筛选，具有可解释性和可控性。
- **轻量化与实用**：蒸馏为 8B 模型，实际推理开销小，可用于实时系统。
- **评估全面**：从 QA 正确率、检索指标、信息覆盖率到 token 效率，多维度验证方法优势。
- **实验公平**：通过统一基座、共享教师标签等设计消除混淆变量，结论可信度高。
- **开源**：发布了代码和完整复现配方，有利于社区进一步研究。

# 不足与局限
- **依赖初始检索质量**：若第一阶段检索未命中关键证据，集合选择无法弥补缺失，性能受前置模块限制。
- **任务范围较窄**：仅在多跳问答数据集上验证，未覆盖代码生成、对话式 RAG 等其他领域，泛化性待评估。
- **依赖 LLM 推理能力**：模型的集合选择效果依赖于基座模型的指令遵循与推理水平，小型模型或能力不足时可能退化。
- **候选规模受限**：当前基于 top‑20 候选进行选择，扩展到更大候选池（如 100+）的效率尚未实际验证，尽管论文提及并行潜力。
- **训练数据仅来自 MS MARCO**：蒸馏数据为单跳相关性判断，与多跳集合覆盖需求存在分布差异，可能限制模型在极端复杂推理中的表现。

（完）
