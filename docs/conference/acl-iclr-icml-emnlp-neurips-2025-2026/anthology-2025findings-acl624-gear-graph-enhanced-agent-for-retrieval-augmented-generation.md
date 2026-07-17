---
title: "GeAR: Graph-enhanced Agent for Retrieval-augmented Generation"
title_zh: GeAR：面向检索增强生成的图增强代理
authors: "Zhili Shen, Chenxin Diao, Pavlos Vougiouklis, Pascual Merita, Shriram Piramanayagam, Enting Chen, Damien Graux, André Melo, Ruofei Lai, Zeren Jiang, Zhongyang Li, Ye Qi, Yang Ren, Dandan Tu, Jeff Z. Pan"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.624.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 图增强代理RAG利用图扩展与多步检索框架解决多跳问答
tldr: "针对传统检索器难以处理多跳检索的问题，提出GeAR系统。通过图扩展机制增强任意基检索器，并设计代理框架进行多步图检索。在三个多跳问答数据集上取得领先结果，特别是在MuSiQue上提升超10%，同时所需检索次数更少。"
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 937, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1522, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 742, \"height\": 141, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 182, \"height\": 186, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 182, \"height\": 187, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 178, \"height\": 190, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 894, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 173, \"height\": 186, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 181, \"height\": 187, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 182, \"height\": 188, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 176, \"height\": 190, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.624/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1649, \"height\": 578, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 1407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 722, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 560, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1661, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1673, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1656, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1656, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1660, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1630, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1677, \"height\": 1029, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1669, \"height\": 1195, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1640, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.624/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1680, \"height\": 1300, \"label\": \"Table\"}]"
motivation: 稀疏与稠密检索器内在无法胜任多跳场景，需要结构化扩展与自主决策。
method: 结合图扩展增强任意检索器，并在代理框架中实现多步图检索流程。
result: "多跳问答上性能全面领先，尤其MuSiQue上相对提升超10%，且检索效率更高。"
conclusion: GeAR展示了图结构与代理协作的巨大潜力，为复杂推理中的RAG提供了新的高性能范式。
---

## Abstract
Retrieval-augmented Generation (RAG) relies on effective retrieval capabilities, yet traditional sparse and dense retrievers inherently struggle with multi-hop retrieval scenarios. In this paper, we introduce GeAR, a system that advances RAG performance through two key innovations: (i) an efficient graph expansion mechanism that augments any conventional base retriever, such as BM25, and (ii) an agent framework that incorporates the resulting graph-based retrieval into a multi-step retrieval framework. Our evaluation demonstrates GeAR’s superior retrieval capabilities across three multi-hop question answering datasets. Notably, our system achieves state-of-the-art results with improvements exceeding 10% on the challenging MuSiQue dataset, while consuming fewer tokens and requiring fewer iterations than existing multi-step retrieval systems. The project page is available at https://gear-rag.github.io .

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **核心问题**：在检索增强生成（RAG）中，传统的稀疏与稠密检索器（如BM25、SBERT）难以胜任多跳问答（multi‑hop QA）任务，无法在一次检索中获取完成推理所需的所有文档。
- **研究动机**：现有图增强方法（如HippoRAG、GraphReader、TRACE）虽利用结构化知识改进多跳检索，但普遍依赖大语言模型（LLM）进行昂贵的图遍历与节点探索，迭代次数多、token消耗大。
- **整体含义**：提出 **GeAR (Graph‑enhanced Agent for Retrieval‑augmented generation)** 系统，通过高效的图扩展机制和代理框架，以更低的计算开销实现更优的多跳检索性能，尤其针对复杂的MuSiQue数据集取得超过10%的相对提升。

## 2. 论文提出的方法论
### 2.1 核心思想
- **图扩展增强任意基检索器**：在离线阶段将文档与抽取出的三元组对齐，形成相互连接的索引；在线阶段利用LLM定位初始图节点，再通过小型语义模型进行多样化的三元组束搜索，扩展出多跳相关文档。
- **代理化多步检索**：模拟人类信息搜索过程，维护一个紧凑的“要点记忆”（gist memory），在迭代中不断累积已有证据，并判断是否需要继续检索或重写查询。

### 2.2 关键技术细节
- **知识同步（Sync）**：
  1. 用LLM读取基检索器返回的段落集合 \(C'_q\)，总结出近端三元组（proximal triples）\(T'_q\)。
  2. 通过 `tripleLink` 函数将每个近端三元组链接到离线索引 \(T\) 中最相似的三元组，得到初始节点 \(T_q\)。
- **多样化三元组束搜索（Diverse Triple Beam Search）**：
  - 以 \(T_q\) 为起点，每一步仅考虑共享头/尾实体的邻居三元组，禁止重复访问。
  - 使用小型稠密嵌入模型（如SBERT）计算查询与候选三元组序列的余弦相似度作为得分。
  - 在每个束内部，对候选序列按得分降序排序后，施加基于排名的多样性权重 \(\exp(-\min(n,\gamma)/\gamma)\)，使最终选出的 top‑b 束更不易重叠，提升检索召回率。
  - 输出序列扁平化后按广度优先映射到原文段落，再与初始段落列表做倒数秩融合（RRF），得到 **SyncGE** 的检索结果 \(C_q\)。
- **代理框架（GeAR）**：
  - **要点记忆构建**：在第 \(n\) 轮，LLM结合当前轮次检索到的段落（以及上一轮的要点记忆）读取并提取近端三元组 \(T_G^{q(n)}\)，累积到记忆 \(G^{(n)}\) 中。
  - **推理终止**：LLM判断 \(G^{(n)}\) 是否足以回答原问题，给出可回答性标志与推理 \(r^{(n)}\)。若可回答则停止迭代。
  - **查询重写**：若不可回答，基于原问题、记忆和推理结果生成下一轮查询 \(q^{(n+1)}\)。
  - 终止后，将最终要点记忆中的每个三元组通过 `passageLink` 链接到文档，并与所有迭代的检索结果进行RRF，得到最终排序列表。

## 3. 实验设计
- **数据集与场景**：三个开放域多跳问答数据集
  - **MuSiQue**（2–4跳，500条测试，139k文档，148k块）
  - **2WikiMultihopQA**（2跳，500条测试，430k文档，490k块）
  - **HotpotQA**（2跳，1k条测试，9k文档，10k块，采用HippoRAG的小型子集）
- **评测指标**：
  - 检索：Recall@5, @10, @15
  - 问答：Exact Match (EM) 和 F1
- **对比方法**：
  - **单步检索**：BM25、SBERT、Hybrid（BM25+SBERT）、HippoRAG；以及各自结合 NaiveGE 或 SyncGE 的变体。
  - **多步检索**：IRCoT (BM25)、IRCoT (ColBERTv2)、HippoRAG w/IRCoT，以及本文的 **GeAR**。
- **实现细节**：所有LLM组件统一使用 GPT‑4o mini（温度0），检索基座用Elasticsearch，SBERT用 all‑mpnet‑base‑v2，束搜索宽度=10、长度=2，邻居上限100。

## 4. 资源与算力
- **文中未明确说明**：论文没有提及使用的GPU型号、数量、训练时长或具体的推理开销硬件。
- 因方法完全基于推理（无训练），算力消耗主要在调用LLM API（GPT‑4o mini、GPT‑3.5‑turbo、Llama‑3.1‑8B 等）和运行检索系统（Elasticsearch + 稠密向量相似度计算）。作者仅展示了 **LLM 输入/输出 token 数量**（图4、图2），未给出具体的硬件配置或延迟数据。

## 5. 实验数量与充分性
- **实验组数众多**：
  - 三大数据集上的主实验（单步与多步对比，6种基方法及其变体）
  - 消融实验：NaiveGE vs SyncGE、多样性束搜索的有/无、不同束长与最大迭代次数的配置、不同LLM（闭源 vs 开源）下的表现、不同三元组抽取方式的影响
  - 分析与鲁棒性：按跳数类型划分的召回率分析、按文档三元组密度的鲁棒性测试、性能随迭代次数增加（直至20次）的走势、端到端QA性能表
  - 效率对比：各方法所需LLM token量随迭代轮次的变化曲线
  - 定性研究：成功/失败案例的手动分析、来自HippoRAG的案例域外测试（书籍、电影、大学、生物医学）
- **充分性与公平性**：实验覆盖了主要竞争对手，使用统一LLM、统一测试集、统一评估指标，并复现了多个基线以确保对比公平。消融实验多角度验证了各组件的作用，实验设计具备说服力。

## 6. 论文的主要结论与发现
1. **GeAR在多个多跳QA数据集上达到SOTA**，特别是MuSiQue上Recall@15提升超10%（58.4% vs 55.9%），问答EM/F1亦显著领先。
2. **SyncGE单步即可取得极具竞争力的性能**，在MuSiQue和HotpotQA上超越HippoRAG等多步方法，展示了图扩展的潜力。
3. **多样化束搜索** 相较于标准束搜索在所有数据集上均有稳定提升（如MuSiQue R@5 从47.0%→48.7%），说明多样性对多信息需求检索的重要性。
4. **效率优势显著**：GeAR通常在一两次迭代内达到或超越其他多步检索器的最终性能，且LLM token消耗明显更少；即使在单步设置下，SyncGE消耗的token也远低于HippoRAG w/IRCoT。
5. **兼容开源模型**：使用Llama‑3.1‑8B或Qwen‑2.5‑8B等开源模型时，GeAR仍能大幅超越原有SOTA，降低了对闭源LLM的依赖。
6. **鲁棒性**：对文档中三元组稀疏或稠密的情形，SyncGE和GeAR的性能波动远小于NaiveGE和HippoRAG w/IRCoT。
7. **失败分析**表明主要错误来自LLM阅读器（reader）的幻觉，数据质量问题次之，纯粹的图构建缺陷较少。

## 7. 优点（方法或实验亮点）
- **创新性强**：将图扩展与代理记忆结合，利用小型语义模型替代LLM进行昂贵的图遍历，大幅度降低计算开销。
- **通用性好**：SyncGE可叠加在任何基检索器（稀疏、稠密、混合）之上，且代理框架兼容多种LLM。
- **仿生学视角**：模拟海马体与皮层在情景记忆形成中的协同机制，赋予方法以认知科学的解释深度。
- **实验周密**：多数据集、多指标、多层次消融与鲁棒性分析，且进行了细致的失败模式解剖，增强了结论的可信度。
- **效率评估突出**：不仅关注精度，还用 token 量对比实际消耗，贴近工业应用需求。

## 8. 不足与局限
- **图构建未深入优化**：完全沿用HippoRAG的三元组抽取方法，未解决实体消歧、知识补全等固有问题，可能成为性能瓶颈。
- **评分函数较单一**：束搜索中的评分仅基于稠密向量的余弦相似度，未探索如自然语言推断等更精细的语义匹配方式。
- **代理组件设计简约**：要点记忆、推理器、查询重写器等均采用较简单的提示工程实现，无记忆压缩、自适应策略等高级设计。
- **应用场景有限**：仅在多跳事实型问答上评测，未扩展到对话、多文档摘要等其他RAG应用，泛化性有待验证。
- **计算资源透明度不足**：未报告硬件配置与具体推理延迟，难以直接评估实际部署的成本。
- **对LLM质量敏感**：错误分析显示大量失败源于阅读器的幻觉，说明方法强依赖LLM的抽取与总结能力。
- **数据集偏差风险**：部分数据集（如HotpotQA子集）经过严重下采样，可能简化任务；且MuSiQue中本身存在不可答问题，影响性能天花板。

（完）
