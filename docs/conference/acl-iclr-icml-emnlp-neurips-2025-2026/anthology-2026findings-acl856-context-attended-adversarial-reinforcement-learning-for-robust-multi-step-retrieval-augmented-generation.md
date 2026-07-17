---
title: Context-attended Adversarial Reinforcement Learning for Robust Multi-step Retrieval Augmented Generation
title_zh: 上下文注意的对抗强化学习用于鲁棒多步检索增强生成
authors: "Yingtao Ren, Xiao Luo, Yu-Cheng Chang, Chin-teng Lin"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.856.pdf"
tags: ["query:agentic-rag"]
score: 8.0
evidence: 通过对抗强化学习增强多步RAG的抗噪鲁棒性
tldr: 多步RAG系统易受检索噪声和伪造文档影响，现有微调方案应对长文本场景适应性差，提出上下文注意的对抗强化学习框架CARE，通过对抗训练增强系统鲁棒性，在长上下文RAG中取得更好表现。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.856/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1667, \"height\": 820, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.856/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.856/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 811, \"height\": 423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026.findings-acl.856/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 705, \"height\": 294, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 737, \"height\": 1077, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1667, \"height\": 1169, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1604, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 799, \"height\": 1028, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 1202, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 610, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026.findings-acl.856/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 531, \"label\": \"Table\"}]"
motivation: 多步RAG在真实场景中面临检索噪声和伪造文档的挑战。
method: 提出CARE，结合上下文感知的对抗强化学习，提升多步RAG系统面对噪声的自适应能力。
result: 在含噪长文档RAG任务中，CARE比基于微调的方法更鲁棒。
conclusion: 对抗强化学习为多步RAG的鲁棒性提升提供了新的范式。
---

## Abstract
Multi-step retrieval-augmented generation has attracted increasing attention due to its capacity to improve the factuality of large language models with iterative retrieved knowledge. However, the performance of multi-step RAG systems is susceptible to potential retrieval noise and fabricated documents in real-world scenarios. Current approaches usually utilize supervised fine-tuning on predetermined noisy contexts to enhance the robustness. However, their performance remains inadequate when it comes to more complicated long-context scenarios due to the lack of adaptability. Towards this end, we propose a novel framework named Context-attended Adversarial Reinforcement Learning (CARE) for multi-step RAG systems against attacks. The core of our CARE is to conduct reinforcement learning on adversarial samples which are alternatingly enhanced with text gradients. In particular, our CARE includes a reward model to identify the accuracy of responses, which is minimized for the generation of adversarial samples with text gradients. These context-attended noisy samples are then utilized for reinforcement learning to maximize the rewards. The whole framework is conducted alternatingly from easy to hard samples to ensure the smoothness of the optimization. Extensive experiments on multi-step RAG benchmark datasets are conducted to validate the superiority of our proposed CARE in multiple noisy scenarios. Our code is available at https://github.com/yingtaoren/CARE.

---

## 论文详细总结（自动生成）

好的，我将以资深学术论文分析助手的身份，使用中文、以 Markdown 形式，对该论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

本文聚焦于**多步检索增强生成（Multi-step RAG）系统的鲁棒性问题**。

*   **研究背景**：RAG 通过检索外部知识来提升 LLM 的事实准确性，已在单步检索中取得成功。为了处理复杂的、需要多步推理的信息寻求任务，多步 RAG 系统应运而生，它们会进行迭代检索，形成更长的上下文。
*   **核心问题**：在真实世界场景中，多步检索过程会**不可避免地引入并累积噪声、错误信息甚至恶意的伪造文档**。
    *   现有的防御方法（如基于监督微调、多智能体验证、思维链自反思）主要针对**单步检索、短上下文**场景，在复杂的长上下文多步场景中因缺乏**适应性**而表现不佳。
    *   此外，现有工作大多关注无关噪声，对**复杂的、专门设计以误导模型的对抗攻击**缺乏足够的防御能力。
*   **研究动机与目标**：作者旨在提出一个新的框架，以增强多步 RAG 生成器在面对复杂长上下文中的噪声和对抗攻击时的鲁棒性，实现低成本的后训练增强。

### 2. 论文提出的方法论

论文提出了一个名为**上下文注意的对抗强化学习 (Context-attended Adversarial Reinforcement Learning, CARE)** 的框架。其核心是将鲁棒的生成建模为一个动态对抗博弈，通过交替优化攻击者和生成器，实现共同进化。

*   **核心思想**：建立一个闭环优化系统。一个基于文本梯度的**动态攻击者**不断生成具有欺骗性的对抗样本，试图最大化生成器的错误率；一个基于强化学习的**鲁棒生成器**学习从混合了真实和对抗文档的上下文中辨别事实，忽略对抗扰动。
*   **关键技术细节**：
    1.  **数据构建与课程学习**：为确保对抗训练的稳定性，本文设计了三阶段课程。
        *   **难度划分**：通过让模型对同一问题和真实上下文进行多次采样回答，根据回答的**一致性和正确率**将样本分为简单样本（ `Qeasy`）和困难样本（ `Qhard`）。
        *   **阶段一 (热身)**：仅使用 `Qeasy` 的样本，通过简单的静态攻击注入训练生成器，建立基础对齐。
        *   **阶段二 (过渡)**：混合使用 `Qeasy` 和 `Qhard`，并**激活文本梯度驱动的动态攻击者**。
        *   **阶段三 (深度鲁棒)**：仅使用 `Qhard`，在**最激烈的动态攻击**下训练，最大化模型的辨别能力。
    2.  **基于文本梯度的对抗样本生成 (动态攻击者)**：
        *   **目标**：将对抗上下文 `C_adv` 视为一个可学习的变量，通过优化 `C_adv` 来最大化生成器在真实答案 `y*` 上的损失 `L`。公式表示为 `C*_adv = argmax_{C_adv} L(π_θ(y | q, C_real, C_adv), y*)`。
        *   **实现 (文本梯度反向传播)**：由于 `C_adv` 是离散文本，无法进行标准微分，因此采用三步文本梯度机制：
            1.  **前向传播**：生成器基于当前对抗上下文产生回答 ŷ。若攻击失败（ŷ 正确），则触发优化。
            2.  **梯度计算**：提示一个评论家（Critic）LLM，分析当前对抗上下文 `C^(k)_adv` 和失败输出 ŷ 之间的因果关系，生成一个**文本梯度** `∇text = Critic(C^(k)_adv | ŷ = y*)`。该梯度是一段自然语言指令，指出如何修改输入才能改变输出（例如，“生成器注意到了伪造文档中的时间戳不一致，请更新日期以匹配问题的时间范围”）。
            3.  **优化步骤**：提示一个优化器 LLM，依据文本梯度来更新对抗内容，生成新的、更具欺骗性的文档 `C^(k+1)_adv = ApplyGradient(C^(k)_adv, ∇text)`。
    3.  **基于上下文的交替强化学习 (鲁棒生成器)**：
        *   **算法**：使用**分组相对策略优化 (Group Relative Policy Optimization, GRPO)** 来优化生成器策略 `π_θ`。GRPO 通过组内采样的统计量来估计基线，无需训练额外的价值模型，更适合非平稳的对抗环境。
        *   **奖励函数**：设计了一个上下文注意的奖励函数 `R(y)`，旨在显式惩罚攻击者引起的幻觉。它不仅对完全正确的答案 (`y = y*`) 给予正奖励 (`α`)，还对落入目标毒性答案 (`y = y_tox`) 的行为给予惩罚 (`β`)，并在其他情况下使用 F1 分数来引导模型向真实答案靠拢。

### 3. 实验设计

*   **数据集与场景**：
    *   **领域内数据集**：HotpotQA， 2WikiMultiHopQA。
    *   **领域外数据集**：Musique, Bamboogle。
    *   **检索设置**：对每个问题进行最多4轮的多步检索，每轮检索前3个文档，构建长上下文场景。
    *   **攻击场景**：
        1.  **反事实攻击 (Counterfactual Attack)**：生成与事实相反的伪造文档。
        2.  **毒性攻击 (Poisoned Attack)**：为每个问题生成一个预设的错误答案，并合成多个支持该错误答案的对抗文档，混入检索结果中。
*   **评价指标**：
    *   **EM (Exact Match)**：衡量答案的生成准确性。
    *   **ASR (Attack Success Rate)**：衡量模型输出被误导至特定错误答案的百分比。
*   **对比基线 (Baselines)**：
    *   **基础 LLM**：Qwen3-4B-Instruct, Llama3.1-8B-Instruct, 以及更强大的 Qwen3-30B-Thinking。
    *   **鲁棒 RAG 方法**：ATM-RAG (对抗微调)、AstuteRAG (冲突感知框架)、InstructRAG (基于理由引导的去噪)、RbFT (鲁棒微调)。这些方法涵盖了数据增强、多智能体推理和训练时的鲁棒策略。

### 4. 资源与算力

*   **模型**：
    *   **生成器（训练对象）**：Llama-3.1-8B-Instruct 和 Qwen-2.5-3B-Instruct 作为骨干网络。
    *   **攻击 LLM 和 TextGrad 优化模型**：Qwen3-30B-Instruct。
*   **训练数据**：从 HotpotQA 和 2Wiki 的训练集中构建了 **12,000 个样本**的数据集。
*   **算力资源**：所有实验在**单个计算节点**上进行，该节点配备有**两块 Nvidia L40S GPU**。
*   **关键超参数**：奖励函数系数 α = 1.05， β = -0.3。训练批次大小为 512，rollout 批次大小为 16。论文未明确提及总训练时长。

### 5. 实验数量与充分性

本论文的实验设计**较为全面和充分**，具体体现在：
*   **多组主实验**：在 **4 个多跳问答数据集**上，针对 **2 种不同的攻击类型**，对比了包含基础模型、通用鲁棒策略在内的 **7 个基线**。这是一个综合性的性能评估。
*   **消融实验**：通过移除动态攻击（仅用静态攻击）和分阶段评估，系统性地验证了 **“文本梯度攻击者”** 和 **“三阶段课程学习”** 这两个关键组件的有效性。
*   **鲁棒性分析实验**：通过**改变注入的伪造文档数量**来分析模型的鲁棒性，证明了 CARE 在不同攻击强度下的稳定性。
*   **训练过程分析**：**可视化**了跨阶段的奖励曲线和攻击成功率统计，直观地展示了对抗训练过程中的共同进化动态，为理解模型行为提供了洞见。
*   **案例分析**：提供了一个具体的多步检索案例，定性地展示了 CARE 如何在两轮攻击下成功抵制欺骗性上下文并找到真实答案。

这些实验从定量和定性、组件与整体、动态过程等多个维度验证了方法的有效性，客观且充分。

### 6. 论文的主要结论与发现

*   **优越的性能**：CARE 在所有基准测试和攻击场景下，**均显著优于所有基线**，实现了更高的答案准确性 (EM) 和更低的攻击成功率 (ASR)。
*   **高效的鲁棒路径**：CARE 使用 4B 和 8B 的小模型，其性能常超过参数量大得多的 30B 推理模型。这表明，通过**迭代对抗训练培养的判别能力**，是实现 RAG 鲁棒性的更有效途径，而非简单地扩大模型规模或增加推理算力。
*   **强大的泛化能力**：在未见过的领域外数据集上，CARE 同样展现出最佳性能，证明了其学习到的防御策略具有**良好的泛化性**。
*   **攻击与防御的共同进化**：实验分析证实，动态攻击者能够有效扩展威胁边界，发现潜在漏洞；而生成器则在对抗中不断适应，变得更加强健。三阶段课程学习对于避免优化崩溃、实现平滑过渡至关重要。

### 7. 优点

*   **问题新颖**：首次系统性地研究和解决了**多步长上下文 RAG 场景下**的鲁棒性问题，填补了该领域的空白。
*   **方法论创新**：巧妙地将**文本梯度优化 (TextGrad)** 和 **强化学习 (GRPO)** 结合，形成了一个创新的**共同进化对抗训练框架**，使攻击者能动态适应生成器的防御水平。
*   **设计精巧**：
    *   利用模型生成的**回答一致性作为无监督的信号来划分样本难度**，设计了三阶段课程学习，保证了从易到难的平滑训练。
    *   **三阶段课程学习策略**有效地防止了对抗训练中常见的模式崩溃和过拟合问题。
*   **实现成本低、效率高**：整个训练过程仅需2张L40S GPU和1.2万个训练样本，就能显著增强4B/8B模型的鲁棒性，是低成本实现高性能的典范。
*   **实验扎实且全面**：多数据集、多攻击类型、多基线对比、消融、鲁棒性分析、案例研究，立体化地验证了方法的优越性。

### 8. 不足与局限

*   **攻击类型覆盖有限**：
    *   论文**假设检索器是静态的、安全的**，仅关注上下文注入攻击。未考虑对检索索引本身的投毒攻击或直接针对查询的攻击。
    *   攻击类型聚焦于**事实性误导**，没有覆盖更广泛的威胁，如观点操纵、越狱（Jailbreaking）或认知操纵。
*   **对黑盒攻击的依赖性**：攻击样本的生成和文本梯度计算均依赖于一个“白盒”的大模型 (LLM)，需通过 API 或本地调用，这可能引入额外的成本和延迟，且攻击效果受限于攻击模型自身的能力。
*   **缺乏对检索-生成端到端联合防御的探究**：当前框架仅训练生成器，未来可探索联合优化检索器与生成器，以防御更多样化的攻击，避免在检索阶段就出现错误累积。
*   **实验的局限性**：
    *   未讨论在多语言或跨语言场景下的表现。
    *   训练仅在两个新闻/百科类问答数据集上进行，对于其他领域（如医疗、法律）的泛化能力有待验证。

（完）
