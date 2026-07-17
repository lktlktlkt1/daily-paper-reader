---
title: "Retrieval as Generation: A Unified Framework with Self-Triggered Information Planning"
title_zh: 检索即生成：一种具有自触发信息规划的统一框架
authors: "Bo Li, Mingda Wang, Gexiang Fang, Shikun Zhang, Wei Ye"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.196.pdf"
tags: ["query:agentic-rag"]
score: 9.0
evidence: GRIP通过自触发信息规划在生成中决定检索行为
tldr: 针对RAG中检索与生成分离导致的协调问题，提出GRIP框架，将检索决策嵌入生成过程。通过控制令牌的发射，模型在自回归解码中自主决定何时检索、如何改写查询以及何时终止，实现了检索即生成。这种自触发信息规划统一了检索与生成，实验表明能有效提升生成质量和效率，为RAG的闭环控制提供了新范式。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 835, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 810, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 644, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 717, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 802, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 806, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 802, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 807, \"height\": 702, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 643, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026.acl-long.196/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1628, \"height\": 834, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1690, \"height\": 925, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 824, \"height\": 329, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 751, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 734, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 804, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 757, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 802, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 775, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 762, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 753, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1439, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026.acl-long.196/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1647, \"height\": 626, \"label\": \"Table\"}]"
motivation: 传统RAG中检索作为外部干预，难以端到端协调检索与生成。
method: GRIP通过控制令牌实现自触发信息规划，在生成中自主决定检索时机、查询改写和终止。
result: 实验表明GRIP在保持灵活性的同时提升了生成质量和效率。
conclusion: 检索即生成范式实现了检索与生成的统一协调。
---

## Abstract
We revisit retrieval-augmented generation (RAG) by embedding retrieval control directly into generation. Instead of treating retrieval as an external intervention, we express retrieval decisions within token-level decoding, enabling end-to-end coordination without additional controllers or classifiers. Under the paradigm of Retrieval as Generation, we propose GRIP ( G eneration-guided R etrieval with I nformation P lanning), a unified framework in which the model regulates retrieval behavior through control-token emission. Central to GRIP is Self-Triggered Information Planning , which allows the model to decide when to retrieve, how to reformulate queries, and when to terminate, all within a single autoregressive trajectory. This design tightly couples retrieval and reasoning and supports dynamic multi-step inference with on-the-fly evidence integration. To supervise these behaviors, we construct a structured training set covering answerable, partially answerable, and multi-hop queries, each aligned with specific token patterns. Experiments on five QA benchmarks show that GRIP surpasses strong RAG baselines and is competitive with GPT-4o while using substantially fewer parameters. Code and resources are provided in the supplementary materials.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- 传统检索增强生成（RAG）通常将检索作为外部、一次性操作，基于初始查询检索文档后生成答案，无法适配推理过程中逐渐涌现的信息需求或歧义性查询。
- 现有动态检索方法仍多依赖外部控制器、启发式信号或多阶段流程，检索时机、查询改写和终止决策未统一为生成过程中可训练的显式动作。
- 本文提出“检索即生成”范式，将检索控制内化到语言模型的自回归解码中，通过统一的控制令牌实现端到端的检索规划，消除对外部模块的依赖。

### 2. 论文提出的方法论

**核心思想**：通过引入特殊控制令牌（control tokens），模型在单条自回归轨迹内自主决定何时检索、如何构建新的检索查询以及何时终止，实现检索与推理的紧密耦合。

**关键技术细节**：

- **控制令牌集**：定义了四种特殊令牌：
  - `[ANSWER]`：开始生成最终答案。
  - `[RETRIEVE]`：触发外部检索。
  - `[SOLVED]`：终止生成，表示任务完成。
  - `[INTERMEDIARY]`：输出部分推理或知识，作为中间状态。
- **自触发信息规划（Self-Triggered Information Planning）**：模型根据当前状态自主决定进入不同分支：
  - 若内部知识足够，则发出 `[ANSWER]` → 答案 → `[SOLVED]`。
  - 若不足，则发出 `[INTERMEDIARY]` → 部分推理 → `[RETRIEVE]` → 生成新查询，检索后再次判断。
  - 多跳情况下循环执行上述过程，直到发出 `[ANSWER]` 并最终以 `[SOLVED]` 结束。
- **结构化监督训练**：构建四种训练样本类型，对应不同检索行为轨迹：
  - **Type‑α（直接回答）**：模型内部知识直接回答，训练输出 `[ANSWER]... [SOLVED]`。
  - **Type‑β（需检索）**：模型产出部分正确但含噪声的答案，训练输出 `[INTERMEDIARY]...[RETRIEVE]...`。
  - **Type‑γ（多跳规划）**：模型和基本检索均失败，利用GPT‑4o‑mini生成改进的后续查询，训练迭代式 `[INTERMEDIARY]→[RETRIEVE]` 模式。
  - **Type‑θ（答案补全）**：检索到相关文档但需进一步推理提炼，训练输出 `[INTERMEDIARY]→[RETRIEVE]→[ANSWER]`。
- **训练目标**：
  - **第一阶段**：监督微调（SFT），最小化自回归交叉熵损失。
  - **第二阶段**：基于规则强化学习（RL），采用DAPO算法，定义两个奖励信号：
    - *答案忠实度奖励*：基于BLEU计算生成答案与参考答案的相似度。
    - *控制准确度奖励*：奖励正确发出控制令牌模式，惩罚缺失或错误令牌。
  - 最终奖励 = 答案忠实度奖励 + 控制准确度奖励。

**算法流程（文字描述）**：
1. 输入原始查询，模型根据内部知识决定是否直接回答。
2. 若不能直接回答，则输出中间推理并触发检索，生成新查询。
3. 检索器返回相关文档，追加到上下文中。
4. 模型再次判断信息是否充分，若充分则输出最终答案并终止；否则继续上述过程，直至达到最大检索步数预算（默认3）。
5. 达到预算后强制模型输出 `[ANSWER]` 并终止。

### 3. 实验设计

**数据集**：
- 五个开放域/多跳问答基准：HotpotQA、PopQA、Natural Questions (NQ)、WebQuestions (WebQ)、TriviaQA。
- 额外领域特异性测试：BioASQ（生物医学）。

**评估指标**：
- 精确匹配（EM）、ROUGE（平均ROUGE‑1/2/L）、F1（词元级F1），以及综合指标 Avg.Score（所有指标在所有数据集上的非加权均值）。
- 行为分析指标：CoverEM（预测覆盖参考答案的比例）。

**对比方法**：
- **无训练方法**：基础提示（Instruct）、单次RAG（Single RAG）、GPT‑3.5 Turbo、GPT‑4o、动态检索方法FLARE、DRAGIN、ETC。
- **基于训练的方法**：SFT‑RAG、Self‑RAG、INFO‑RAG、RobustRAG、GainRAG、R1‑Searcher、RetRobust、InsturctRAG。
- 所有开源基线均使用官方代码/检查点重新评估，保持相同骨干模型（LLaMA3‑8B）、相同语料库（Wikipedia）和检索器（BM25，top‑3段落）。

**实验设置**：
- 训练数据来自TriviaQA和NQ的训练集，构造40,000个结构化监督样本（涵盖四种类型）。
- RL阶段使用额外的5,000个样本。
- 骨干模型：LLaMA3‑8B，全参数监督微调，8个epoch，批量大小32，8块A800 GPU，学习率1e‑6，余弦调度。
- RL阶段：1个epoch，学习率1e‑7，DAPO算法。
- 推理时最大检索步数默认3，分析时测试了更大预算（5、7、10）。

### 4. 资源与算力

- 监督微调使用 **8块A800 GPU**，全参数训练，8个epoch，批量大小32（每GPU微批4）。
- 强化学习阶段同样在上述硬件上完成，但仅训练1 epoch。
- 未提及具体总训练时间或计算量（如GPU小时），但描述了硬件配置和训练epoch数。
- 推理时采用BM25检索器，不需要额外大规模计算。

### 5. 实验数量与充分性

**实验规模与维度**：
- 主实验覆盖5个QA基准，共涉及约20个基线方法。
- 报告了EM、ROUGE、F1和Avg.Score，性能比较较为全面。
- 深入的行为分析实验：
  - 检索深度适应性（如早期停止 vs. 深层检索的案例对比）
  - 跨任务自适应检索频率分析
  - 生成查询的检索质量评估（top‑1/top‑3覆盖率）
  - 检索预算可控性及外推能力（最大步数从3至10）
  - 教师信号替换（使用开源模型替代GPT‑4o‑mini）
  - 通用能力保留测试（MMLU、MBPP、CNN/DailyMail摘要）
  - 奖励度量消融（BLEU vs. ROUGE/F1/EM）
  - 检索器消融（BM25、DPR、混合检索）
  - 强化学习前后检索行为分布变化
  - 潜在状态可视化
  - 失败案例分析
  - 不同骨干模型（Qwen2.5‑7B）的复现

- **公平性**：所有开源基线均使用统一的LLaMA3‑8B骨干、Wikipedia语料、BM25检索器和top‑3设置进行复现，尽力消除评估差异。
- **客观性**：采用标准指标，自动评估，对比方法多样且包含强基线（如GainRAG、GPT‑4o）。
- **充分性**：实验数量充足，覆盖性能、效率、行为可控性、通用能力、公平消融等多维度，整体设计较为全面。

### 6. 论文的主要结论与发现

- GRIP在所有五个QA基准上均优于其他开源RAG方法，Avg.Score达到41.0，接近GPT‑4o。
- 模型学习到了任务感知的检索深度：在多跳数据集上检索更频繁，在简单数据集上减少不必要的检索。
- 通过自触发查询生成，GRIP能显著提高检索到的文档包含正确答案的比例（尤其top‑1）。
- RL阶段可进一步抑制冗余检索（相比无RL版本，平均检索次数从1.60降至1.24），同时保持性能。
- 检索行为展现出外推性：训练时最大检索步数为3，但测试时增大预算仍能有效按需增加检索深度。
- 令牌级控制使检索决策可解释，潜在空间分析显示 `[ANSWER]` 和 `[RETRIEVE`] 对应的隐藏状态明显分离。
- GRIP在保留通用能力（MMLU、MBPP、摘要等）方面优于其他微调的RAG基线。

### 7. 优点

- **范式统一**：将检索决策完全内化到生成过程，无需任何外部控制器或启发式信号，简化了系统设计。
- **行为可控**：通过简洁的控制令牌集，实现检索触发、查询改写和终止的精确控制，且可以通过解码时预算灵活调节。
- **训练方法创新**：四类结构化监督数据结合强化学习，使模型学会何时检索、如何改写查询，并抑制冗余行为。
- **实证充分**：在五个标准QA集上对比了多种强基线，进行了详尽的行为分析、消融研究和通用能力测试，结论可信度高。
- **资源友好**：在8B参数模型上取得接近GPT‑4o的性能，检索开销低（平均检索次数约1.24次），效率较高。
- **可外推检索深度**：训练中仅见最多3步检索，但测试时能泛化到更多步数，展示出学习到“何时需要更多信息”的原则，而非死记固定模式。

### 8. 不足与局限

- **检索接口设计敏感**：模型行为仍受最大检索预算、分块策略、top‑k等固定选择影响，文中未探索自适应调整这些参数的方法。
- **教师信号依赖**：Type‑γ数据的构建利用GPT‑4o‑mini生成改进查询，尽管替代实验显示可换用开源模型，但整体框架仍受益于较强的教师信号。
- **领域特异性验证有限**：仅额外测试了BioASQ，多数实验集中于开放域QA，其他类型任务（如事实核查、对话等）泛化性未知。
- **强化学习奖励简单**：控制奖励采用规则计数，可能无法完全捕捉复杂检索决策的质量，且对答案忠实度采用BLEU，存在一定的限度。
- **失败模式依然存在**：论文承认存在最终答案错误、冗余检索步数等失败案例，推理深度和冗余避免机制仍有改进空间。
- **训练数据构建成本**：结构化监督数据的构建需要多次采样和外部模型协助，可能增加训练前的预处理开销。

（完）
