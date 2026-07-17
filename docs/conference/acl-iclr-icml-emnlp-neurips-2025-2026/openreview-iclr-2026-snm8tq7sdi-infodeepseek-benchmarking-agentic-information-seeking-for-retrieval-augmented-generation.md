---
title: "InfoDeepSeek: Benchmarking Agentic Information Seeking for Retrieval-Augmented Generation"
title_zh: "InfoDeepSeek: 面向检索增强生成的智能体信息搜索基准测试"
authors: "Yunjia Xi, Jianghao Lin, Menghui Zhu, Yongzhao Xiao, Zhuoying Ou, Jiaqi Liu, Tong Wan, Te Gao, Bo Chen, Weiwen Liu, Yasheng Wang, Ruiming Tang, Yong Yu, Weinan Zhang"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=snm8tq7sdI"
tags: ["query:agentic-rag"]
score: 9.0
evidence: 面向RAG中智能体信息搜索的基准测试
tldr: 本文针对现有RAG基准仅支持静态、封闭环境和简单查询的问题，提出InfoDeepSeek基准测试。该基准模拟真实开放网络环境，要求LLM代理进行自主信息搜索和迭代检索，从而评估智能体RAG系统的动态决策能力。实验表明，InfoDeepSeek能有效区分不同代理策略的性能，为推进智能体信息搜索研究提供了标准化平台。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG基准无法评估代理在动态开放环境中的自主信息搜索能力。
method: 构建模拟开放网络环境的新基准，评估LLM代理的智能体信息搜索行为。
result: 该基准能有效区分不同代理策略的性能，揭示动态检索行为特征。
conclusion: 为智能体RAG研究提供了标准化且更具挑战性的评估平台。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances large language models (LLMs) by grounding responses with retrieved information. As an emerging paradigm, Agentic RAG further enhances this process by introducing autonomous LLM agents into the information seeking process. However, existing benchmarks fall short in evaluating such systems, as they are confined to a static retrieval environment with a fixed, limited corpus and simple queries that fail to elicit agentic behavior. Moreover, their evaluation protocols assess information seeking effectiveness by pre-defined gold sets of documents, making them unsuitable for the open-ended and dynamic nature of real-world web environments. To bridge this gap, we present InfoDeepSeek, a new benchmark with challenging questions designed for assessing agentic information seeking in real-world, dynamic web environments. We propose a systematic methodology for constructing challenging queries satisfying the criteria of determinacy, difficulty, and diversity. Based on this, we develop the first evaluation framework tailored to dynamic agentic information seeking, including fine-grained metrics about the accuracy, utility, and compactness of information seeking outcomes. Through extensive experiments across LLMs, search engines, and question types, InfoDeepSeek reveals nuanced agent behaviors and offers actionable insights for future research

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：现有面向检索增强生成（RAG）的基准测试存在两大不足：
  - **静态封闭环境**：仅依赖固定的、有限的文档集，无法模拟真实世界的开放网络环境。
  - **简单查询设计**：查询类型单一，难以诱发和衡量智能体的自主信息搜索行为（Agentic behavior）。
  - **评估协议局限**：采用预定义的“金标准”文档集评估效果，不适用于开放、动态的检索场景。
- **整体含义**：随着智能体RAG（Agentic RAG）成为新兴范式，迫切需要一个新的基准来评估LLM智能体在真实、动态的网络环境中进行自主信息搜索的能力。本文提出**InfoDeepSeek**基准，填补了这一空白，旨在推动智能体信息搜索研究向前发展。

## 2. 论文提出的方法论

- **核心思想**：构建一个模拟真实开放网络的动态检索环境，设计具有挑战性的查询，来考察 LLM 智能体的迭代检索与自主决策能力。
- **关键技术细节**（基于摘要推断）：
  - **查询构建方法论**：提出一套系统性的方法，确保查询满足三个标准：确定性（determinacy）、困难性（difficulty）、多样性（diversity）。
  - **评估框架**：首次专门为动态智能体信息搜索量身定制评估体系，包含细粒度指标：
    - **准确性（accuracy）**：衡量信息搜索结果在事实层面的正确程度。
    - **效用性（utility）**：衡量检索信息对于回答问题的实际帮助大小。
    - **紧凑性（compactness）**：衡量智能体检索到的信息是否精简、不冗余。
  - 该框架不依赖静态的“金标准”文档集，而是适配于开放式的动态网络环境。
- **无明确公式**：摘要未披露具体算法流程或数学公式，主要以框架与指标设计为主。

## 3. 实验设计

- **使用的数据集/场景**：基于所提方法论构建的**InfoDeepSeek 基准**本身即为数据集。其场景设定为真实、动态的网络环境（模拟真实搜索引擎与网页交互）。
- **基准（Benchmark）**：**InfoDeepSeek** 自身就是提出的新基准，包含高难度、多类型的查询。
- **对比的方法**：
  - 跨不同 **LLM**（大语言模型）进行实验。
  - 涉及不同 **搜索引擎**（或信息检索后端）。
  - 考察不同 **问题类型**（difficulty、diversity 的体现）下的表现。
  - 目的是分析“nuanced agent behaviors”（细微的智能体行为差异），而非简单对比已有系统。

## 4. 资源与算力

- 摘要及所提供的元数据均**未明确提及**所使用的 GPU 型号、数量、训练时长或推理算力开销。
- 文中实验侧重于评估，可能主要涉及 LLM API 调用和搜索引擎交互，算力需求可能主要体现在 API 费用和工程实现上，但无具体数据。

## 5. 实验数量与充分性

- **实验组数**：摘要中提到“extensive experiments across LLMs, search engines, and question types”，说明实验覆盖了多种维度（模型、检索源、问题类型），但未给出确切组数。
- **充分性与公平性**：
  - 所提出的基准本身就是为评估智能体信息搜索而专门设计的，因此实验维度（模型、搜索后端、问题类型）与评估目标高度匹配，设计较为充分。
  - 使用了统一的评估框架（准确性、效用性、紧凑性），保证了比较的公平性。
  - 由于基准是新建的，不存在与旧基准直接比较的问题，其公平性体现在横向对比各系统在同一平台下的差异。
  - **局限**：摘要仅定性描述，缺乏定量结果佐证区分度；实验覆盖面需结合全文判断（如是否涉及多种智能体策略、消融实验等）。

## 6. 论文的主要结论与发现

- **有效区分能力**：InfoDeepSeek 基准能有效揭示不同 LLM 智能体策略在信息搜索过程中的细微行为差异（“reveals nuanced agent behaviors”）。
- **提供行动洞察**：实验结果为未来的 Agentic RAG 研究提供了可操作的见解（“offers actionable insights”），但摘要未具体说明是何类洞察。
- **平台价值**：该基准为推进智能体信息搜索研究提供了一个标准化、且更具挑战性的评估平台。

## 7. 优点

- **问题新颖且紧迫**：精准捕捉到 Agentic RAG 评估缺失这一空白，理由充分，动机清晰。
- **贴合真实场景**：突破静态封闭环境的限制，模拟真实开放网络，使评估更具现实意义。
- **评估框架细致**：提出多维度、细粒度的评估指标（准确性、效用性、紧凑性），超越传统单一匹配度指标。
- **方法论系统**：查询构建遵循确定性、困难度、多样性的三原则，保证基准质量。
- **分析视角深入**：实验不仅做排名，还致力于揭示智能体行为特点，具有分析深度。

## 8. 不足与局限

- **仅见摘要**：详细的方法实现、实验定量结果、智能体架构细节（如工具使用、记忆机制）等均未知，可能隐蔽重要实现细节。
- **基准普适性待验证**：所设计的查询是否对当前所有主流 Agentic RAG 策略都具有合理的挑战度与区分度，无数据支撑。
- **评估指标可行性**：准确性、效用性、紧凑性在开放环境下的自动评测如何实现（是否需要人工评判、LLM 评判等），摘要未提，可能存在评估成本或可靠性问题。
- **环境真实性**：“模拟开放网络”的具体实现（如使用预设网页库还是实时抓取、如何处理网页更新）不清楚，可能影响生态效度。
- **算力与成本未讨论**：未提及运行该基准的典型成本，对研究者的复现与采纳决策参考不足。

（完）
