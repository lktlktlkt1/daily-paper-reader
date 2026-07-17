---
title: Fine-grained Knowledge Enhancement for Retrieval-Augmented Generation
title_zh: 检索增强生成的细粒度知识增强
authors: "Jingxuan Han, Zhendong Mao, Yi Liu, Yexuan Che, Zheren Fu, Quan Wang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.522.pdf"
tags: ["query:agentic-rag"]
score: 7.0
evidence: 通过思维链提示检索细粒度知识并增强解码的RAG方法
tldr: 传统RAG通常基于文档语义相似度检索，忽略句子级细粒度信息。本文提出FKE方法，通过解耦思维链提示从外部语料中检索句子级知识，并设计解码增强模块将其融入生成过程。实验显示，细粒度知识的注入有效提升了答案的事实准确性和完整性，为解决RAG中的知识粒度问题提供了实用方案。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.522/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.522/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1629, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.522/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.522/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.522/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 609, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1619, \"height\": 587, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 789, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 710, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 783, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.522/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 490, \"label\": \"Table\"}]"
motivation: 文档级检索忽略关键句子信息，导致知识利用不充分。
method: 通过解耦思维链提示检索句子级知识，并增强解码融入生成。
result: 细粒度知识增强了答案的事实一致性与完整性。
conclusion: 挖掘细粒度信息是提升RAG效果的有效途径。
---

## Abstract
Retrieval-augmented generation (RAG) effectively mitigates hallucinations in large language models (LLMs) by filling knowledge gaps with retrieved external information. Most existing studies primarily retrieve knowledge documents based on semantic similarity to assist in answering questions but ignore the fine-grained necessary information within documents. In this paper, we propose a novel fine-grained knowledge enhancement method (FKE) for RAG, where fine-grained knowledge primarily includes sentence-level information easily overlooked in the document-based retrieval process. Concretely, we create a disentangled Chain-of-Thought prompting procedure to retrieve fine-grained knowledge from the external knowledge corpus. Then we develop a decoding enhancement strategy to constrain the document-based decoding process using fine-grained knowledge, thereby facilitating more accurate generated answers. Given an existing RAG pipeline, our method could be applied in a plug-and-play manner to enhance its performance with no additional modules or training process. Extensive experiments verify the effectiveness and generality of our method.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：检索增强生成（RAG）通过检索外部知识缓解大语言模型（LLM）的幻觉，但现有方法大多基于文档语义相似度检索整个文档，忽略了文档内部的句子级细粒度信息。
- **核心问题**：文档级检索容易受关键词匹配、无关句子干扰，导致选中的文档虽表面相关却缺乏回答问题所需的关键事实，从而生成错误答案。句子级别的必要信息常被埋没在长篇文档中。
- **整体含义**：提出**细粒度知识增强方法（FKE）**，从文档中提取句子级的关键信息，并将其融入生成过程，以提升RAG答案的准确性和事实完整性。

## 2. 论文提出的方法论
- **核心思想**：在现有RAG管道上“即插即用”地叠加两个组件——细粒度知识检索与解码增强。
- **关键技术细节**：
  - **解耦式的细粒度知识检索**  
    - 采用“解耦思维链提示”（disentangled Chain-of-Thought prompting）：先让LLM显式识别文档中有利于回答问题的知识片段，再基于这些片段提取查询聚焦的句子作为细粒度知识 S = (s₁, s₂, …, sₘ)。  
    - 使用生成器模型（如 Llama2-7B-chat）以 one-shot 方式执行，无需额外训练。
  - **解码增强策略**  
    - 分别基于原始文档 D 和细粒度句子 S 计算 logits \(z_{d,t}\)、\(z_{s,t}\)，得到两个概率分布。  
    - 通过公式融合两种分布（α 为控制强度，τ 为温度）：  
      \[
      p_\theta(y_t) = \frac{\text{softmax}(z_{d,t}/\tau_d) + \alpha \cdot \text{softmax}(z_{s,t}/\tau_s)}{1+\alpha}
      \]  
    - 对 logits 进行 top-k 截断，保证生成流畅性。  
    - 最终从增强分布中采样，使生成结果兼顾文档上下文完整性与细粒度关键信息。
  - **即插即用**：无需新增模块或额外训练，可直接嵌入已有的 RAG 管道。

## 3. 实验设计
- **数据集**：
  - 多跳问答：2WikiMultihopQA（192k 样本）、HotpotQA（113k 样本）
  - 单跳问答：PopQA（14k 样本）、ARC-Challenge（2.5k 样本）
- **基础 RAG 管道**：
  - 多跳：DRAGIN（基于自注意力动态触发检索）
  - 单跳：CRAG（轻量检索评估器 + 纠正策略）
- **对比方法**：
  - 多跳：wo-RAG, SR-RAG, FL-RAG, FS-RAG, FLARE, DRAGIN
  - 单跳：LLaMA2-7B/13B, Alpaca-7B/13B, Self-RAG, CRAG
- **评价指标**：EM（精确匹配）、F1（token 重叠）、Accuracy（答案包含正确信息）

## 4. 资源与算力
- 论文明确指出实验可在 **1 块 NVIDIA A800 GPU** 上完成。
- 由于方法不需要训练，故未提及训练时长；细粒度知识检索和生成增强均为推理阶段操作。

## 5. 实验数量与充分性
- **主实验**：在 2 个基础管道 × 4 个数据集的组合上对比管道原始性能与加入 FKE 后的性能（共 8 组结果）。
- **消融实验**：
  - 消融提示方式（标准提示 vs. 解耦提示）及其对检索知识准确率的影响（表2）
  - 消融知识使用方式（仅文档、仅细粒度、解码增强融合）（表3）
  - 消融控制强度 α 和温度 τₛ 的影响（图4、图5）
  - 消融模型规模（7B 和 13B）（表4）
- **案例分析**：针对 CRAG 在 PopQA 上的错误案例展示 FKE 的修正效果（表5）
- **人工评估**：从两个数据集随机采样共 400 条输出，3 位标注者评估正确性和相关性，并报告 Fleiss' Kappa 一致性系数。
- **评估充分性**：覆盖多跳/单跳、多指标、自动+人工评估、多种消融维度，对比公平、全面。

## 6. 论文的主要结论与发现
- FKE 在 2WikiMultihopQA 上将 DRAGIN 的 EM 提升 **2.8**，F1 提升 **3.2**；在 HotpotQA 上 EM 提升 **4.9**，F1 提升 **3.5**。
- 在单跳任务上，FKE 使 CRAG 的准确率在 PopQA 上提高 **6.3**，在 ARC 上提高 **5.4**。
- 解耦提示获得的细粒度知识比标准提示更精确且更紧凑，解码增强融合细粒度和文档级知识优于任何单一来源。
- 方法对模型规模具有鲁棒性，在 7B 和 13B 模型上均稳定提升。
- 细粒度知识有效解决了文档级检索中关键信息缺失或被干扰的问题。

## 7. 优点
- **创新性**：首次通过解耦思维链显式提取问答必需的句子级知识，并设计解码阶段对比融合策略，思路新颖且实用。
- **即插即用**：不改变原有 RAG 流程，无需训练或额外模块，易于部署和推广。
- **实验全面**：覆盖多跳和单跳两大类 RAG 基线，多组自动指标、消融实验、案例分析和人工评估，论证扎实。
- **效果提升明显**：在所有测试场景下均获得可观的性能增益，且超参数敏感性合理。

## 8. 不足与局限
- **未在大规模模型上验证**：仅测试了 7B 和 13B 的 Llama2，未涉及 70B 或其它强大模型，扩充性存疑。
- **依赖 LLM 提取质量**：细粒度句子提取完全依赖生成器自身能力，可能引入幻觉或偏差，但文中未对此风险进行量化讨论。
- **语料缺失时无效**：当外部知识库中根本不存在答案信息时，方法无法提供帮助。
- **缺少与同期细粒度 RAG 方法的直接比较**：如 FILCO、REAR 等，虽声明差异但未在统一实验设置下对比性能。
- **潜在外部语料风险**：论文承认外部文档可能包含偏见、错误或攻击性内容，RAG 技术面临的安全性问题依然存在。
- **应用限制**：假设需要先文档检索再句子抽取，可能增加推理延迟和计算开销，未分析效率。

（完）
