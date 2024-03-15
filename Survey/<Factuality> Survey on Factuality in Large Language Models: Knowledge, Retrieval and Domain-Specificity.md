# Survey on Factuality in Large Language Models: Knowledge, Retrieval and Domain-Specificity

> - 论文链接：[https://arxiv.org/pdf/2310.07521.pdf](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/2310.07521.pdf)
> - 开源链接：[https://github.com/wangcunxiang/LLM-Factuality-Survey](https://link.zhihu.com/?target=https%3A//github.com/wangcunxiang/LLM-Factuality-Survey)
> - 作者单位：西湖大学、普渡大学、复旦大学、耶鲁大学、微软亚洲研究院等

## Abstract

重点讨论了事实性的定义和影响、大模型事实性的评估、大模型事实性机制和产生错误的原理、大模型事实性的增强等几个方面的内容，对大模型的事实性进行了详细的梳理和总结。这篇综述的目标是为了帮助学界和业界的研究开发人员更好得理解大模型的事实性，增加模型的知识水平和可靠程度。

关注两种主要的LLM配置——独立LLMs和利用外部数据的检索增强型LLM

## 1 INTRODUCTION

将LLMs用作知识库载体的优势：

- 减少了与构建和维护专用知识库相关的开销和成本
- LLMs提供了一种更灵活的知识处理和利用方法，可以进行上下文感知推理，并具有适应新信息或提示的能力。

**问题：**

- 非事实或误导性内容

提高准确性：策略范围从外部知识库中检索信息到持续的预训练和监督微调，但是涵盖LLM中所有事实的整体概览仍然难以捉摸。

> 提到的两个survey：(说研究的比较浅显)
>
> - A Survey on Evaluation of Large Language Models. arXiv preprint arXiv:2307.03109 (2023).
> - Aligning Large Language Models with Human: A Survey. arXiv preprint arXiv:2307.12966 (2023).

> 提到几个关于hallucination的Survey：
>
> - Lei Huang, Weijiang Yu, Weitao Ma, Weihong Zhong, Zhangyin Feng, Haotian Wang, Qianglong Chen, Weihua Peng, Xiaocheng Feng, Bing Qin, and Ting Liu. 2023. **A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions.** ArXiv abs/2311.05232 (2023). https://api.semanticscholar.org/CorpusID: 265067168
> - Vipula Rawte, Amit Sheth, and Amitava Das. 2023. A Survey of Hallucination in Large Foundation Models. arXiv:2309.05922 [cs.AI]
> - Hongbin Ye, Tong Liu, Aijia Zhang, Wei Hua, and Weiqiang Jia. 2023. Cognitive Mirage: **A Review of Hallucinations in Large Language Models**. arXiv:2309.06794 [cs.CL]
> - Yue Zhang, Yafu Li, Leyang Cui, Deng Cai, Lemao Liu, Tingchen Fu, Xinting Huang, Enbo Zhao, Yu Zhang, Yulong Chen, Longyue Wang, Anh Tuan Luu, Wei Bi, Freda Shi, and Shuming Shi. 2023. Siren’s Song in the AI Ocean: **A Survey on Hallucination in Large Language Models**. arXiv:2309.01219 [cs.CL]
> - Ziwei Ji, Nayeon Lee, Rita Frieske, Tiezheng Yu, Dan Su, Yan Xu, Etsuko Ishii, Ye Jin Bang, Andrea Madotto, and Pascale Fung. 2023. **Survey of Hallucination in Natural Language Generation**. ACM Comput. Surv. 55, 12, Article 248 (mar 2023), 38 pages. https://doi.org/10.1145/3571730
>
> **幻觉问题hallucination issue 和事实性问题factuality issue 不同 在2.2节**

关注**领域事实**以及**过时信息**的挑战

> Dmain-specific 的Survey
>
> - Domain Specialization as the Key to Make Large Language Models Disruptive: A Comprehensive Survey.



==**概览：**==这项调查旨在全面介绍LLM中的事实研究，深入探讨四个关键方面：

- 第2节：事实性问题的定义和影响
- 第3节：评估事实性及其定量评估的技术
- 第4节：分析LLMs中事实性的基本机制，并确定事实错误的根本原因
- 第5节：增强LLMs事实性的方法

<img src="./assets/CleanShot 2024-03-07 at 11.03.54@2x.png" alt="CleanShot 2024-03-07 at 11.03.54@2x" style="zoom:50%;" />

将LLM分为两个主要的的配置：

- LLMs without external knowledge
- Retrieval-Augmented LLMs：不仅涉及生成准确的回答，还有从众多检索到的来源中正确选择相关知识片段

## 2 FACTUALITY ISSUE

<img src="./assets/CleanShot 2024-03-07 at 15.30.19@2x.png" alt="CleanShot 2024-03-07 at 15.30.19@2x" style="zoom:50%;" />

> 实时性问题以及影响

### 2.1 Large Language Models

>  LLMs：
>
> - 对大型语言模型没有被广泛接受和确切的定义
> - 只考虑：
>   1. 具有emergent abilities涌现能力的decoder-only的预训练语言模型
>   2. 一些encoder-decoder架构的比如T5
> - 不考虑encoder-only的BERT等
>
> <img src="./assets/CleanShot 2024-03-07 at 11.09.03@2x.png" alt="CleanShot 2024-03-07 at 11.09.03@2x" style="zoom:50%;" />

### 2.2 Factuality

在LLM中，事实性指的是大型语言模型生成遵循事实信息的内容的能力，这包括常识、世界知识和领域事实。

事实信息可以基于可靠的来源，如词典、维基百科或来自不同领域的教科书。

事实性问题的一些表现：1. 领域知识不足； 2. LLM可能不知道上次更新后发生的事实（过时信息）；3. 掌握相关事实，但是推理错误；4. 忘记或无法回忆学习过的事实

- LLMS生成与某些事实相矛盾的内容的可能性，无论这些内容是凭空产生的、过时的信息，还是缺乏特定领域的知识。

==**factuality issue v.s. hallucination**==

- LLMs中的幻觉和事实问题都涉及生成内容的准确性和可靠性，它们**涵盖不同方面**。
  - 幻觉主要围绕着LLMs生成**毫无根据**或**不合理**的内容：幻觉可以被理解为模型倾向于“产生与某些来源无关的荒谬或不真实内容”的倾向。
    - "produce content that is nonsensical or untruthful in relation to certain sources."---OpenAI
  - 事实性强调模型**学习、获取和利用事实知识的能力**。
  - 例子：
    - **如果生成的内容包含准确信息但与提示的具体内容不符，那就是一种幻觉而非事实性问题**
      - 如果一个LLM在被要求编写“关于兔子和狼交朋友的童话故事”时，却创作了一个关于“兔子和狗成为朋友”的故事，那就是表现出幻觉。然而，这并不一定是一个事实错误。
      - 例如，如果LLM的输出包含比提示规定更多细节或不同元素，但仍然在事实上是正确的，则这是一种幻觉情况。
    - 如果**LLM避免直接回答，表示“我不知道”**，或者**提供一个准确但省略了一些正确细节的回应**，那么它是在处理**事实性**，而不是幻觉
    - 幻觉有时可能虽然**偏离了原始输入，但仍保持事实准确**。
      - 过时的信息侧重于以前准确的信息已被更新的知识取代的情况
      - 特定领域强调生成需要特定的专门知识的内容
  - <img src="./assets/CleanShot 2024-03-07 at 11.31.18@2x.png" alt="CleanShot 2024-03-07 at 11.31.18@2x" style="zoom:50%;" />

### 2.3 Impact

## 3 FACTUALITY EVALUATION

<img src="./assets/CleanShot 2024-03-07 at 15.30.38@2x.png" alt="CleanShot 2024-03-07 at 15.30.38@2x" style="zoom:50%;" />

### 3.1 Factuality Evaluation Metrics

分为四类：

<img src="./assets/CleanShot 2024-03-07 at 14.43.54@2x.png" alt="CleanShot 2024-03-07 at 14.43.54@2x" style="zoom:50%;" />

#### 3.1.1 Rule-based evaluation metrics 基于规则的评价

大型语言模型中对事实性的大多数评估使用基于规则的评估指标，因为它们具有一致性、可预测性和易于实施。

缺点：可能会过于死板，无法考虑语言使用、上下文解释或口头表达中的细微差别或变化。

- Exact Match：LLM生成的输出与提供的输入或参考文本一字不差地相同
- Common metrics：Accuracy, Precision, Recall, AUC, F-Measure, Calibration score, Brier score, and other common metrics  准确率、精度、召回率、AUC、F-度量、校准分数、Brier 分数以及其他常见指标
  - 包括使用正确预测的标签和基本事实标签，由于LLMS的输入和输出都是人类可读的句子，因此没有统一的方法将句子转换为标签。大多数评估将定义他们自己的方式。也就是说这些分数通常不是单独使用的，而是结合在一起
  - Calibration score 校准分数：**衡量预测概率与观察频率之间的一致性**。一个完全校准的模型应该在大量实例中，看到预测结果的概率与该结果的相对频率匹配。
  - Brier Score：在概率预测中用作度量概率预测准确性的指标。它计算了**分配给事件的预测概率与事件实际结果之间的均方差**。
    - Brier分数的范围从0到1，其中0表示完美预测，1表示最糟糕的预测。
    - 这个度量标准适用于二元和分类结果，但不适用于有序结果。
  - MC1 (Single-true) and MC2 (Multi-true)：在多选题回答中被广泛认可的度量标准，特别是在TruthfulQA中
    - MC1：对于**一个问题附带多个答案选择，目标是确定唯一正确的答案**。模型的选择取决于它分配最高完成对数概率的答案选择，与其他选项无关。得分计算为所有问题中直接准确性。
    - MC2：针对**一个问题和多个标记为真或假的参考答案**，得分是从分配给真实答案集合的归一化总概率中导出的。
  - BLEU：Bilingual Evaluation Understudy metric 通常用于事实性评估的背景下，该指标根据匹配的n-gram短语的加权平均值，计算两个句子中短语的共现频率。这有助于定量评估生成文本与其参考文本之间的事实一致性。
  - ROUGE：Recall-Oriented Understudy for Gisting Evaluation (ROUGE) metric 衡量生成文本与参考文本之间相似性的度量，相似性基于召回分数。
    - 主要用于**文本摘要领域**
    - 包括四种不同类型
      -  ROUGE-n 评估 n-gram 共现统计数据；
      - ROUGE-l，测量最长公共子序列；
      - ROUGE-w 基于加权最长公共子序列进行评估；
      - ROUGE-s 测量跳过二元组共现统计数据。
    - 这些多样化的指标共同提供了对生成文本事实准确性的全面度量。
  - METEOR Metric for Evaluation of Translation with Explicit Ordering (METEOR) ：旨在解决 BLEU 提出的几个不足之处。这些包括召回率不足、缺乏高阶 n 元组、生成文本与参考文本之间缺乏明确的词匹配，以及使用 n 元组的几何平均值。
    - METEOR通过引入一个综合度量来克服这些问题，该度量是基于单字精确率和召回率的调和平均值计算得出的。这可能会提供对生成文本中事实性的增强评估。
  - QUIP-Score.是一种n-gram重叠度量。它量化了生成的段落中包含在文本语料库中确切片段的程度 QUIP-Score用于评估LLM的“接地”能力，特别是评估模型生成的答案是否可以直接在基础文本语料库中找到。 它通过比较从生成输出中提取出来的字符n-gram与预训练语料库之间的精确性来定义

#### 3.1.2 Neural Evaluation Metrics.神经评估指标。

每个度量标准在评估上略有不同，但都旨在评估机器生成文本与其参考对应物之间的语义和词汇对齐，从而确保生成内容的事实性。、

- ADEM automatic Dialogue Evaluation Model (ADEM) metric
  - 衡量对话中语言模型生成的回应质量
- BERTScore：利用BERT中预训练的嵌入来衡量两个句子之间的相似性。
- BLEURT Bilingual Evaluation Understudy with Representations from Transformers (BLEURT)
- BARTScore.

#### 3.1.3 Human Evaluation Metrics.

缺点：主观性、不一致性和可能出现错误

- Attributable to Identified Sources (AIS)：是一种度量标准，用于验证LLMs的输出是否仅分享关于外部世界可验证的信息。
- Auto-AIS
- FActScore 评估由LLMs生成的长篇文本的事实准确性。

#### 3.1.4 LLM-based Metrics.

### 3.2 Benchmarks for Factuality Evaluation 事实性评估的基准

作者介绍了用于大模型事实性评估的基准测试，同时介绍了其任务类型、数据集、评价指标、以及目前代表性大模型在其上的表现，具体内容如下表所示：

<img src="./assets/CleanShot 2024-03-07 at 15.21.14@2x.png" alt="CleanShot 2024-03-07 at 15.21.14@2x" style="zoom:50%;" />

### 3.3 Factuality Evaluation Studies事实性评估研究

作者介绍了评估大模型事实性但没有引入新评价基准的工作，重点在于那些开创了评估技术、指标的工作，或为 LLMs 的事实性评估提供了独特见解的研究。

作者介绍了每个工作的任务、数据集、指标、是否有人类评估、被评估的大模型以及粒度，具体如下图所示：

Table 5：LLM的事实性评估研究。该表显示了专注于事实性评估的研究，以及提供有价值见解的研究。 “人类评估”列表示是否包含人类评估。 “粒度”列指定了评估级别，区分为标记级（T）和句子级（S）。

<img src="./assets/CleanShot 2024-03-07 at 15.27.25@2x.png" alt="CleanShot 2024-03-07 at 15.27.25@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-07 at 15.27.57@2x.png" alt="CleanShot 2024-03-07 at 15.27.57@2x" style="zoom:50%;" />

### 3.4 Evaluating Domain-specific Factuality 特定领域的事实性评估

针对特定领域事实性评估的基准。该表展示了领域、任务、数据集，以及在相应研究中评估的 LLMs：

<img src="./assets/CleanShot 2024-03-07 at 15.29.10@2x.png" alt="CleanShot 2024-03-07 at 15.29.10@2x" style="zoom:50%;" />

## 4 ANALYSIS OF FACTUALITY 事实性分析

在本节中，我们将深入探讨影响大型语言模型事实性的基本机制。

<img src="./assets/CleanShot 2024-03-07 at 15.31.56@2x.png" alt="CleanShot 2024-03-07 at 15.31.56@2x" style="zoom:50%;" />

### 4.1 Analysis of Factuality

探索LLMs处理、解释和产生事实内容的机制

#### 4.1.1 Knowledge Storage. 知识存储

#### 4.1.2 Knowledge Completeness and Awareness

探讨了LLM的自我意识领域，他们辨别知识空白的能力，以及内部生成知识和外部检索信息之间的平衡

##### Knowledge Awareness. 

大多数这些研究将LLMs视为“黑匣子”，促使模型报告其置信水平或计算模型输出的困惑度作为响应可能性的指标。

- 仅依赖自我纠正而没有外部反馈可能会导致边际改善甚至性能下降
- LLMs对自己的事实知识边界存在不准确的认识，并倾向于对自己的回答过于自信。
- “SelfAware" 实验表明，模型确实具有一定能力识别自己的知识空白，但它们仍远远不及人类水平。

##### Parametric Knowledge vs Retrieved Knowledge.

总的来说，虽然LLMs在处理知识密集型任务方面表现出潜力，但它们对预训练信息的依赖以及事实准确性方面的限制仍然是重要障碍。这强调了该领域需要进一步发展并且将检索增强等补充方法纳入其中以提升LLMs中长尾知识学习的重要性。

#### 4.1.3 Contextual Influence and Knowledge Conflict. 上下文影响和知识冲突

LLM固有的参数化知识与提供的上下文知识之间的相互作用，探讨了模型利用上下文信息的能力以及在面对冲突信息时的行为。

总体主题是需要采取一种平衡的方法，让LLMs有效地利用其内部知识和外部环境来产生准确连贯的输出

### 4.2 Causes of Factual Errors 事实错误的原因

#### 4.2.1 Model-level Causes.

模型内在的因素

- Domain Knowledge Deficit.
- Outdated Information.
- Immemorization：模型并不总是保留其训练语料库中的知识
- Forgetting：模型可能在训练阶段不保留知识，或者在进一步训练过程中忘记先前的知识。
- Reasoning Failure.

#### 4.2.2 Retrieval-level Causes.

几个检索层级的因素：

- Insufficient Information.信息不足
- Misinformation Not Recognized by LLMs. 检索到的数据中存在的错误信息，LLMs没识别出来是错的
- Distracting Information. 干扰信息 检索到的干扰信息
- 检索到的重要的信息的位置：信息模型对于长上下文的头尾的利用能力更高（Lost-in-the-middle）
- Misinterpretation of Related Information. 对相关信息的误解

#### 4.2.3 Inference-level Causes.

推理层级的因素：

- Snowballing. 滚雪球 在生成过程中，一开始的轻微错误或偏差可能会随着模型继续生成内容而累积。
- Erroneous Decoding. 错误解码。解码阶段对将模型的内部表示转换为人类可读内容至关重要，在这个阶段出现的错误，无论是由于诸如波束搜索错误或次优采样策略等问题引起的，都可能导致输出结果误代表模型实际的“知识”或意图。这可能表现为不准确、矛盾甚至毫无意义的陈述。
- Exposure Bias. 曝光偏差。在训练阶段如果LLMs更频繁地接触某些类型的内容或措辞，它们可能会倾向于生成类似的内容，即使这并不是最真实或相关的。

## 5 ENHANCEMENT 增强

本节讨论了增强LLMs在不同阶段的事实性的方法，包括LLM生成、检索增强生成、推理阶段增强以及领域特定事实性改进，如图2所示。

<img src="./assets/CleanShot 2024-03-07 at 16.47.50@2x.png" alt="CleanShot 2024-03-07 at 16.47.50@2x" style="zoom:50%;" />

表8提供了增强方法及其相对于基准LLMs的改进摘要。重要的是要认识到各种研究论文可能采用不同的实验设置，如零样本、少样本或完整设置。因此，在检查这个表格时，重要的是注意不同方法的性能指标，即使在评估相同数据集上相同指标时，也可能无法直接比较。

所选事实增强方法的性能。该表显示了各种数据集上基线模型和它们的增强对应模型的性能指标，用 → 表示。由于空间限制，每个工作中只呈现了一部分数据集、指标和模型。

<img src="./assets/CleanShot 2024-03-07 at 16.57.31@2x.png" alt="CleanShot 2024-03-07 at 16.57.31@2x" style="zoom:50%;" />

### 5.1 On Standalone LLM Generation

1. Improving Factual Knowledge from Unsupervised Corpora (Sec 5.1.1):从无监督语料库中获取事实知识，预训练期间优化训练数据，例如通过去重和强调信息性词语
2. Enhancing Factual Knowledge from Supervised Data (Sec 5.1.2)：从监督数据中增强事实知识，监督微调策略，重点是使用标记数据进行微调或集成结构化知识，如知识图谱（KGs），或对模型参数进行精确调整
3. Optimally Eliciting Factual Knowledge from the Model (Sec 5.1.3, 5.1.4, 5.1.5):从模型中以最佳方式获取事实知识，多智能体协作，prompt创新，新颖的解码方法，比如事实核心抽样，以进一步提高事实性

#### 5.1.1 Pretraining-based.

通过在这个阶段强调策略，模型的固有事实性可以得到显著增强。这种方法对于解决像遗忘和忘记等挑战尤为关键。

##### Initial Pretraining  模型基础预训练期间采用的方法。

- 去冗余

##### Continual Pretraining 迭代式的预训练过程，使模型能够逐步完善和更新其知识库。

#### 5.1.2 Supervised Finetuning.

监督微调利用标记的数据集来提高模型的性能。它向模型传授特定任务或知识基础导向信息，并解决了遗忘和忘记等挑战。

##### Continual SFT. 一种循环微调方法，模型通过连续的标记数据集进行持续改进。

##### Model Editing. 与直接微调模型不同，模型编辑是一种更精确的方法来增强模型的事实性。通过编辑与事实相关的特定区域，模型可以正确表达该事实，而不会影响其他无关知识。

#### 5.1.3 Multi-Agent.

通过以合作或竞争的方式利用多个模型，通过它们集体的能力增强事实性，有助于解决遗忘和推理失败问题。

- 提出一种方法，通过将不同的LLM视为参与多智能体辩论的智能代理来增强语言模型的性能。
  - 在这种方法中，多个语言模型的实例呈现并辩论各自的答案和推理过程，在经过多轮辩论后最终达成对最终答案的共识。如果辩论的答案未能收敛，提示会被修改以减少两个代理人的固执性。
  - 提高模型的数学能力和推理能力，同时增强生成内容的准确性
- fact-checking mechanism.
  - 与证人被询问其说法的真实性的场景相类似，他们利用LLM从QA数据集中收集陈述，这些陈述要么是事实正确的，要么是不正确的。在语句生成期间，模型被提供一个黄金答案，提示它生成准确和不准确的语句，并内在地标记每一条语句。

#### 5.1.4 Novel Prompt.

引入创新或定制的prompt，以从LLM中提取更多事实和准确的回应，可以更好地帮助模型引出其参数中的知识，并提高推理能力。

- Generate-then-Read (GENREAD)：

  - 文档检索器被LLM生成器取代。在本文中，LLM被促使生成关于给定问题的多个上下文文档。作者对这些文档嵌入进行了聚类，并从不同簇中抽样文档以确保上下文文件的多样性。通过这些生成的上下文演示，LLMs在知识密集型任务上取得了比从外部语料库（如维基百科）检索更好的结果。

  - > ？？？？什么阴间方法

- QUIP-Score

  - 测量对预训练数据的依赖性，他们索引维基百科以迅速确定LLM响应的依赖关系。

- Decomposed Prompting 分解prompting

  - 通过提示，将复杂任务分解为多个简单任务，然后可以由特定于任务的LLMs来处理

- Chain-of-Verification (CoVe)

  - 对于模型最初的回答，制定验证查询以评估其初始回答的草稿，独立回答这些查询以保持客观答案，并最终产生经过验证的回复
  - 包含四个关键的阶段：
    1. 根据query，LLms给出初始的回答的草稿
    2. 从查询和初始答案生成验证问题，以确定潜在错误。
    3. 回答每个验证问题，并将这些答案与初始回应进行比较，以检测差异
    4. 如果发现不一致，制定一个整合验证结果的修订答案

#### 5.1.5 Decoding.

解码方法，如束搜索和核心抽样，在引导模型产生既准确又连贯的输出方面发挥着关键作用。通过优化解码过程，可以有效应对雪球效应错误或错误解码等挑战，详见第4.2.3节。

### 5.2 On Retrieval-Augmented Generation

挑战：包括可能存在信息不足和相关数据误解的潜在风险

在检索增强生成的领域内，增强技术可以被广泛分类为几个关键领域：

1. the Normal Setting of Utilizing Retrieved Text for Generations (Sec 5.2.1): 利用检索到的文本进行生成的正常设置
2. Interactive Retrieval and Generation (Sec 5.2.2)交互式检索和生成
   1. 这里的例子包括将思维链步骤整合到查询检索中[92]，
   2. 以及利用基于LLM的代理框架来调用外部知识API [289]。
3. Adapting LLMs to the RAG Setting (Sec 5.2.3):微调LLMs适应RAG任务
4. (4) Retrieving from Additional Knowledge Bases (Sec 5.2.5 and Sec 5.2.4)从附加知识库检索
   1. 使用；外部参数化记忆、图谱

#### 5.2.1 Normal RAG Setting.

我们遵循LlamaIndex和LangChain的架，将过程分解为以下模块和步骤：

1. Document loaders 从不同源头加载文档，loader可以加载不同来源的各种类型的文档
2. Document transformers 用来提取文档中相关部分，涉及chunking 分块，对不同类型的文档有不同的优化算法
3. Text embedding models 用于到文本进行语义分析
4. Vector stores 高效存储和搜索embeddings
5. Retrievers 比如Parent Document Retriever, Self Query Retriever, Ensemble Retriever用于从数据库检索数据
   1. Parent Document Retrieve 为每个父文档创建多个embedding， 检索小的chunk的时候可以保持更多的上下文
   2. Self Query Retriever 将查询语义的部分与其他的元素数据过滤器分开，从而实现更加精确的检索
   3. Ensemble Retriever 从多个来源或使用不同的算法进行检索

#### 5.2.2 Interactive Retrieval.

##### CoT-based Retrieval.

- Rethinking with Retrieval： 介绍一种方法，该方法为每个查询生成多条推理路径及其相应的预测。这个过程涉及从外部来源（如Wikidata、WordNet和ConceptNet）检索相关知识。每条推理路径的忠实度根据蕴含分数、矛盾分数和与检索到的知识的MPNet相似性来确定。选择具有最高忠实度得分的预测作为最终结果。该方法在常识推理、时间推理和表格推理等任务中展现出卓越性能，优于基准的CoT推理和自一致性方法。
- IRCoT 它将CoT过程交织在一起。在这种方法中，CoT期间生成的每个句子都与问题结合形成一个检索查询。随后的推理步骤由语言模型使用检索结果和先前推理来产生。这种交错方法被发现可以增强开放领域QA中检索和CoT的性能。
- FLARE 动态确定“何时和何物进行检索”
  - “何时” 的决定基于当前句子是否包含生成概率低于设定阈值的标记。如果没有，则接受该句子并移至下一个生成步骤；否则，将进行RAG
  - “何物”当前句子被用作查询。为了解决低概率标记影响检索准确性的挑战，提出了两种解决方案：屏蔽低概率标记，并使用 LLM 为这些标记生成查询。


##### Agent-based Retrieval.

使用基于LLM的代理框架，利用外部知识API作为工具或将这些API请求为操作。

- ReAct：将思维链推理与行动相结合
- Reflextion
- Self-RAG：在检索增强生成（RAG）框架的基础上，融入了自我反思的方法
  - 按需检索，促使LLM考虑所检索到的文档是否与论点相关且支持性，从而提高LLM输出结果的事实性
  - 通过在输出过程中让模型生成特殊标记（即反思标记）来实现这一点
  - 采用端到端训练方法，使模型能够生成这些特殊标记。
  - 推理层面上，Self-RAG为每个输入和先前生成内容的每个部分解码一个检索标记。
    - 如果该标记是'否'，则模型继续进行正常输出；
    - 如果是'是'，则执行一次检索操作。
  - 然后将输入、先前输出以及每个已检索文档馈送到模型的另一个会话中，并评估每个文档的相关性。
  - 如果某个文档相关，则进一步评估其是否支持并应该用于生成过程中
  - 根据此文档，模型产生一个片段，并使用生成的反思标记应用软约束和硬约束来选择最合适的文档。
  - 然后将最合适的文档纳入内容持续生成之中，并根据需要提供引用信息。
  - 此过程重复直至整个内容被生成完成。

#### 5.2.3 Retrieval Adaptation.

仅仅使用LLMs中检索到的信息并不总是能够增强它们回答事实问题的能力

三种方法：

- 基于prompt的方法：利用提示来引导检索过程，确保提取相关和事实数据
- 基于SFT的方法：通过训练优化LLM或检索系统，以增强生成任务与检索内容之间的对齐
- 基于RLHF的方法：

#### 5.2.4 Retrieval on External Memory.

一些研究人员正在探索将知识存储在非文本形式中，并通过专门的方法将这些知识整合到模型中。

- 在内存中以键值对的形式存储知识
- 使用通用领域PLM作为外部存储器

微调方法和一些模型编辑方法通过持续的预训练将新知识存储在新的模型参数中。不同之处在于，微调方法将许多知识片段存储在矩阵参数中，而模型编辑为每个知识片段建立一个新神经元。

- Parameter-Efficient Transfer Learning for NLP.：增加Adapter（之前看过的PEFT的Adapter的那篇）
- 将编码的实体存储在外部内存中。在生成过程中，检索到的实体嵌入被整合到模型层中：
  - KALA：KALA 不仅为实体及其编码建立记忆，还使用知识图谱存储这些实体之间的关系
    - 对于输入中的给定提及，首先确定相应的实体。根据知识图谱（KG），从内存中检索该实体及其邻近实体的编码。通过GNN加权聚合，获得此提及对应实体的编码。最后，在模型层引入了基于知识条件特征调制（KFM），将编码结果整合到涉及提及的所有标记的表示中。
  - EaE：在模型训练过程中引入提及检测、实体链接和MLM。模型从与当前提及最接近的实体存储中查询前100个实体嵌入，并使用注意力机制将它们整合起来。
  - TOME：TOME模型是对EaE模型的改进。 TOME不是将实体嵌入存储在内存中，而是将实体提及的嵌入存储起来。 对于输入中标记的实体提及，TOME从内存中检索所有相关的实体提及嵌入，并通过一个记忆注意力层将它们整合到模型中。
  - knowledge plugin 引入了实体相关知识。然而，它们并没有直接将知识集成到模型层中，而是利用了一个预训练映射网络。该网络将实体嵌入映射到预训练语言模型（PLM）的标记嵌入空间。最终，映射后的实体嵌入被注入到输入嵌入级别，促进了知识插入过程
  - RARR：对于每个输入句子，生成一组问题，并搜索网页以验证信息是否与输入句子一致
  - Mention Memory

#### 5.2.5 Retrieval on Structured Knowledge Source.

检索结构化知识库和数据库等资源以获取事实数据

- Zhang等人[303]利用知识图谱（KG）进行检索以解决事实错误。他们观察到用户的请求与知识图谱中的内容之间可能存在不一致。例如，当用户提及全名时，知识图谱可能只有其缩写，导致检索结果不完整。为了纠正这一问题，他们提出了一种重新表述用户请求的方法。他们的方法涉及根据用户输入和数据库元数据使用LLM生成SQL查询。然后他们查询数据库，并要求LLM确定句子中哪个实体对应于数据库中的实体，从而创建映射关系。利用来自数据库的实体名称，LLM被提示重新构思问题。如果针对所选列和项目进行多行数据库查询，则使用贪婪方法生成新问题，并提示用户提供更具体细节直至得出结论性答案为止。实验证明，在减轻语言模型不准确性方面，该方法相比当代最先进技术表现出显著增强效果。
- StructGPT：支持LLMs在结构化数据库上进行推理
  - 这个框架的核心是构建专门的接口，从结构化数据中收集相关证据（即阅读），让LLMs基于收集到的信息进行推理任务（即推理）。特别地，他们提出了一种调用-线性化-生成过程，以支持LLMs在使用接口对结构化数据进行推理。通过与提供的接口迭代此过程，我们的方法可以逐渐接近给定查询的目标答案。在三种类型的结构化数据上进行实验，包括KGQA、TableQA和Text-to-SQL
- Baek等人建议将知识图中的事实知识注入(大型)语言模型(最高可达GPT-3.5)通过根据其与输入问题的文本相似性检索知识图谱中的相关事实，然后将它们作为语言模型的提示。与没有知识图谱基线相比，这种方法平均提高了48%左右的语言模型在知识图谱问答任务上的表现[224]。

### 5.3 Domain Factuality Enhanced LLMs

针对特定领域事实性增强的LLMs。在“领域”栏中，我们使用以下缩写：医疗保健/医学（H）、金融（F）、法律/法律（L）、地球科学/环境（G）、教育（E）、食品检测（FT）和家居装修（HR）。

<img src="./assets/CleanShot 2024-03-07 at 20.51.43@2x.png" alt="CleanShot 2024-03-07 at 20.51.43@2x" style="zoom:50%;" />

总结了几种常用于领域特定LLM的增强技术：

1. Continual Pretraining: 持续预训练 一种通过使用特定领域数据持续更新和微调预训练语言模型的方法。这个过程确保模型在特定领域或领域内保持最新和相关性。它从一个初始的预训练模型开始，通常是一个通用语言模型，然后使用特定领域的文本或数据对其进行微调。随着新信息的出现，模型可以进一步微调以适应不断发展的知识领域。持续预训练是维持 AI 模型在快速变化的领域，如技术或医学中的准确性和相关性的强大方法
2. Continual SFT: 持续SFT 另一种增强 AI 模型事实性的策略。在这种方法中，模型使用特定领域的标记或注释数据进行微调。这个微调过程使模型能够学习和适应领域的细微差别和特点，提高其提供准确和与上下文相关的信息的能力。当随着时间的推移可以获得特定领域的标记数据时，它尤其有用，例如在法律数据库、医疗记录或财务报告的情况下。
3. Train From Scratch: 从零开始训练 这涉及从最小的先验知识或预训练开始学习过程。这种方法可以类比为用一个空白的板子教机器学习模型。虽然它可能没有利用预先存在的知识的优势，但在处理完全新的领域或任务时，如果只有有限的相关数据可用，从零开始训练可能是有利的。它允许模型从头开始建立其理解，尽管它可能需要大量的计算资源和时间
4. External knowledge: 外部知识 这涉及用外部来源的信息增强语言模型的内部知识。这种方法允许模型访问数据库、网站或其他结构化数据存储库，以验证事实或在回应用户查询时收集额外的信息。通过整合外部知识，模型可以增强其事实检查能力，并提供更准确和与上下文相关的答案，特别是在处理动态或快速变化的信息时。

### 5.4 Healthcare domain-enhanced LLMs  医疗保健领域增强型LLMs

### 5.5 Legal domain enhanced LLMs 法律领域

### 5.6 Finance Domain-enhanced LLMs 金融领域

### 5.7 Other Domain-Enhanced LLMs 其他领域

## 6 CONCLUSION

在这次的综述中，作者系统地探索了大型语言模型（LLMs）中事实性问题的复杂景观。首先，作者定义了事实性的概念，然后讨论了其更广泛的影响。之后，作者进入事实性评估部分，包括基准测试、评估指标、特定的评估研究和特定领域的评估。随后，作者深入探讨了大模型事实性的内在机制。作者进行了事实性增强技术的讨论，无论是对于纯大模型还是检索增强的大模型，并关注了特定领域知识增强的大模型。

尽管这次综述中详细描述了许多进展，但仍然存在一些巨大的挑战。由于自然语言固有的复杂性，事实性的评估仍然是一个复杂的难题。此外，大模型如何存储、更新事实知识和产生事实性内容的核心过程尚未完全揭示。尽管某些事实增强技术，如持续训练和检索，显示出前景，但它们仍存在局限性。

展望未来，寻求忠实于事实的大模型既带来了挑战，也带来了机会。未来的研究可能会更深入地了解大模型的神经结构，开发更稳健的评估指标，并在增强技术上进行创新。随着大模型越来越多地融入数字生态系统，确保它们的事实可靠性将始终是至关重要的，这将对 AI 社区及其以外的领域产生影响。





