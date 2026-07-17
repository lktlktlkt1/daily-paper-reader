---
title: "MASS-RAG: Multi-Agent Synthesis Retrieval-Augmented Generation"
title_zh: "MASS-RAG: 多智能体合成检索增强生成"
authors: "Xingchen Xiao, He-Yan Huang (黄河燕), Runheng Liu, Jincheng Xie"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.480.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 多智能体合成RAG，使用角色专用代理处理证据
tldr: 检索增强生成中，若上下文噪声多或异构，单一模型整合证据常显不足。MASS-RAG将证据处理分解为摘要、抽取、推理三个角色智能体，分别生成中间视图，再通过合成模块整合。这种多智能体协同暴露多种证据视角，有助于对比和集成。实验证明，该方法在多个数据集上优于传统RAG，为提高复杂信息下的答案质量提供了有效途径。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.480/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.480/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1634, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.480/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.480/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1646, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.480/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 1371, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1567, \"height\": 1249, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 582, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 615, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 617, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 819, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 782, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1648, \"height\": 1413, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 1459, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1655, \"height\": 1332, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1658, \"height\": 1371, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1647, \"height\": 2149, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.480/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1653, \"height\": 1451, \"label\": \"Table\"}]"
motivation: 噪声或异构检索上下文时，单一生成过程难以有效整合证据。
method: 使用摘要、抽取、推理三个角色智能体协同处理证据并合成答案。
result: 多智能体合成在多个数据集上优于单智能体RAG，答案更一致。
conclusion: 为RAG中的多证据源整合提供了角色分工的协同框架。
---

## Abstract
Large language models (LLMs) are widely used in retrieval-augmented generation (RAG) to incorporate external knowledge at inference time. However, when retrieved contexts are noisy, incomplete, or heterogeneous, a single generation process often struggles to reconcile evidence effectively. We propose MASS-RAG, a multi-agent synthesis approach to retrieval-augmented generation that structures evidence processing into multiple role-specialized agents. MASS-RAG applies distinct agents for evidence summarization, evidence extraction, and reasoning over retrieved documents, and combines their outputs through a dedicated synthesis stage to produce the final answer. This design exposes multiple intermediate evidence views, allowing the model to compare and integrate complementary information before answer generation. Experiments on four benchmarks show that MASS-RAG consistently improves performance over strong RAG baselines, particularly in settings where relevant evidence is distributed across retrieved contexts.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

**研究背景与动机**  
- 大语言模型(LLM)在推理时结合外部知识的检索增强生成(RAG)方法广泛应用，但检索到的上下文常存在噪声、信息不完整或来源异构等问题。  
- 传统的单代理生成模式难以有效协调和整合这些复杂证据。尽管已有方法尝试通过代理过滤上下文（如MAIN-RAG），但仅依赖单一“法官”代理，缺乏从互补视角提取和融合证据的能力。  
- 因此，**核心问题**是如何在免训练的情况下，通过多代理协同对检索文档进行多角度证据筛选与合成，从而提升答案的鲁棒性与事实准确性。

**整体含义**  
- 提出MASS-RAG，将证据处理分解为摘要、抽取、推理三个专门角色代理，并引入合成代理集成多视图信息，实现更可靠的最终预测。

## 2. 方法论

### 核心思想
- 将RAG的证据处理与答案生成过程划分为三个阶段：证据蒸馏、候选答案生成（可选）和最终答案合成。  
- 由三种**过滤代理**分别从不同视角提炼与查询相关的证据：  
  - **摘要代理(Summarizer)**：对检索文档进行抽象式浓缩，保留语义一致性并突出查询相关信息。  
  - **抽取代理(Extractor)**：以严格抽取方式复制事实性文本片段，直接支撑答案。  
  - **推理代理(Reasoner)**：对跨文档的隐含联系进行推理，阐明证据如何支持查询，包含推理步骤。  
- **答案代理(Answer Agent, 可选)**：独立为每个过滤响应生成候选答案，形成多个答案假设。  
- **合成代理(Synthesis Agent)**：比较并整合过滤证据或候选答案，解决矛盾，生成最终统一答案。

### 关键技术细节与算法流程
1. **证据蒸馏**  
   - 对查询 \( q_i \) 和检索文档集 \( D \)，三个过滤代理分别输出：  
     - 摘要式响应 \( R^{(s)}_i = A_{\text{sum}}(q_i, D) \)  
     - 抽取式证据片段 \( R^{(e)}_i = A_{\text{ext}}(q_i, D) \)  
     - 推理式响应 \( R^{(r)}_i = A_{\text{rea}}(q_i, D) \)  
   每个代理输出遵循特定的格式约束，不直接回答查询。

2. **候选答案生成（可选）**  
   - 若启用答案代理，则对每个过滤响应生成候选答案 \( A^{(j)}_i = A_{\text{ans}}(q_i, R^{(j)}_i), j \in \{s, e, r\} \)。  
   - 该步骤适用于事实类QA，对于选择题（如ARC-C）通常跳过，直接将过滤证据送入合成代理。

3. **最终答案合成**  
   - 启用答案代理时：\( \hat{Y}_i = A_{\text{syn}}\left(q_i, \{A^{(s)}_i, A^{(e)}_i, A^{(r)}_i\}\right) \)  
   - 禁用答案代理时：\( \hat{Y}_i = A_{\text{syn}}\left(q_i, \{R^{(s)}_i, R^{(e)}_i, R^{(r)}_i\}\right) \)  
   - 合成代理执行显式比较、整合互补信息并解决不一致。

整个框架以**免训练**方式运行，代理角色由轻量指令定义，可跨不同骨干模型复用。

## 3. 实验设计

### 数据集与评估指标
- **开放域QA (ODQA)**  
  - TriviaQA-unfiltered（使用验证和测试集）  
  - PopQA（长尾子集，1399个稀有实体查询）  
  - 指标：准确率(Accuracy)
- **长文本模糊问答**  
  - ALCE-ASQA（948样本，包含多个可能答案）  
  - 指标：str-em (精确匹配), ROUGE, MAUVE
- **封闭集推理**  
  - ARC-Challenge（1172个多选题）  
  - 指标：准确率

### 对比基线
- **无检索基线**：Llama2 7B/13B, Mistral 7B, Llama3 8B, Qwen3 8B  
- **有检索训练式方法**：Llama2-FT 7B, Self-RAG 7B  
- **有检索免训练方法**：  
  - 标准RAG（各骨干模型+检索文档）  
  - MAIN-RAG（前SOTA多代理RAG）  
- 所有实验使用相同的检索器（Contriever）和检索结果（Self-RAG发布的文档集合），top-5（Llama2 7B）或top-10（其他模型）文档。

## 4. 资源与算力

- 论文明确说明实验设备：4块NVIDIA RTX 4090 GPU（每块24GB显存）。  
- 7B/8B模型可在单块24GB GPU上运行；大于13B的模型需2块GPU。  
- 所有实验使用bfloat16精度，解码采用贪婪生成（temperature=0, top-p=1.0），以确保确定性输出和可复现性。  
- 未报告总训练时长（因方法免训练），推理成本在附录中以“每次调用代理为100 token，含答案代理需8倍单次运行成本，不含答案代理需4倍”形式给出。

## 5. 实验数量与充分性

### 实验组数概览
- **主实验**：在4个数据集上评估，对比超过10种基线（含不同骨干模型和版本），每种设置都报告了MASS-RAG的结果。  
- **消融实验**  
  - 不同检索文档数量（top5 vs top10）对性能的影响。  
  - 答案代理的开关对比（在TriviaQA, PopQA, ASQA两种骨干上）。  
- **分析性实验**  
  - 构建“唯一可归因子集”分析不同过滤代理的互补贡献（Evidence Coverage Rate, ECR）。  
  - 聚合效应分析：对比各过滤响应与合成答案的准确率，检验多代理合成是否提升最终性能。  
- **案例研究**：附录中提供6个详细案例，展示各代理捕捉不同证据的情况。

### 评估充分性与公平性
- 在同一检索结果和骨干模型下与SOTA基线进行系统比较，控制变量良好。  
- 消融研究覆盖关键模块（答案代理、检索深度），结论明确。  
- 分析性实验专门设计子集来量化代理互补性，加强了方法可解释性。  
- 总体上实验设计**充分、客观且公平**，但仅使用了Contriever一种检索器，未探索不同检索器或重排序策略的影响。

## 6. 主要结论与发现

- **多代理过滤有效提升性能**：MASS-RAG在所有基准上均超越训练式与免训练基线，特别是当证据分散在多个文档中时优势更明显。例如在Llama3 8B上，相对MAIN-RAG在TriviaQA和ARC-C上分别提升最高3.5%和27.1%。  
- **代理贡献互补**：摘要、抽取、推理代理捕捉到互不重叠的事实证据，各自在不同问题子集上表现突出。任一代理缺失都会导致证据覆盖下降。  
- **合成代理的角色**：合成代理虽不一定拥有最高证据覆盖率，但能整合多源信息并消解歧义，产出更统一可靠的最终答案。  
- **答案代理的效用具任务依赖性**：在事实类QA中有效提升准确率，但在长文本模糊QA或选择题中效果有限甚至略降，因此可灵活选择启用。  
- **对检索深度的鲁棒性**：在文档数量减少时，MASS-RAG仍优于对比方法，显示其过滤与合成机制提升了对不完美检索的鲁棒性。

## 7. 优点

- **创新的多代理协同设计**：将证据处理明确分解为摘要、抽取、推理三种角色，并通过合成代理整合，促进了多视角互补信息的利用。  
- **完全免训练**：不依赖任何微调或参数更新，部署灵活性高，可直接适配不同骨干LLM。  
- **实验全面**：覆盖多种任务类型（ODQA、长文本QA、推理），对比丰富基线，并提供大量消融和定性分析。  
- **任务自适应配置**：答案代理的开关机制提供了根据任务特性调整流程的灵活性。  
- **分析深入**：通过唯一可归因子集和ECR指标量化了各代理的独立贡献，强化了方法可解释性与说服力。

## 8. 不足与局限

- **检索器固定**：仅采用Contriever一种检索器，未与其它检索或重排序策略结合，结论的泛化性可能受限。  
- **解码策略单一**：仅使用贪婪解码，未探索其他解码方式（如采样）对合成效果的影响。  
- **推理成本**：多代理调用增加了推断延迟，论文未详细衡量实际时间开销，仅在附录估算相对成本。  
- **任务适配需人工判断**：答案代理的启用需根据任务类型决定，缺乏自动化判定机制。  
- **评价指标局限**：长文本QA仅使用str-em等指标，可进一步分析答案覆盖率和忠实度。  
- **未涉及多语言或低资源场景**，应用范围尚待拓展。  
- **合成代理可能受骨干模型能力限制**，较弱模型可能难以有效调和矛盾证据，论文中Mistral 7B部分指标已显下降。

（完）
