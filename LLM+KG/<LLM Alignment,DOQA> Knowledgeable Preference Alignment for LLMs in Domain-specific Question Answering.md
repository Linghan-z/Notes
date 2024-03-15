# Knowledgeable Preference Alignment for LLMs in Domain-specific Question Answering

## abstract

1. user-friendly
2. domain knowledge

认为以上两个需求都可以认为是model **preference** 问题，需要与人类**对齐**

**Know**ledgeable **P**reference **A**lignmen**T** **(KnowPAT)**：

- preference set：

  - style preference set

  - knowledge preference set

## 1 Introduction

**how can LLM be used to solve real-scenario QA problems that are supported by external knowledge graphs?**

**文章：Graph Neural Prompting with Large Language Models.**

- 首先为问题检索相关知识三元组作为参考知识，然后通过包含该知识的提示对LLM进行微调
- 问题：
  1. 由LLMs生成的答案需要用户友好，并避免生成不当内容，如不友好、低质量的回答
  2. 检索到的文章不是都有用
     1. <img src="./assets/CleanShot 2024-03-15 at 14.45.52@2x.png" alt="CleanShot 2024-03-15 at 14.45.52@2x" style="zoom:50%;" />

提出==**Know**ledgeable **P**reference **A**lignmen**T** **(KnowPAT)**==：

- preference set：

  - **style preference** set

  - **knowledge preference** set

- **knowledgeable preference set construction**：领域知识图谱整合到构建知识偏好数据集

**contributions**：

1. preference alignment for 领域问答，使用LLM和领域KG
2. knowledgeable prefernece alignment 知识偏好对齐框架

## 2 Related Works

### 2.1 KG-enhanced Question Answering

利用提示与（大型）语言模型进行对话以促进路径推理和细化知识图检索范围:

- [11] Zhuo Chen, Yufeng Huang, Jiaoyan Chen, Yuxia Geng, Yin Fang, Jeff Z. Pan, Ningyu Zhang, and Wen Zhang. 2022. LaKo: Knowledge-driven Visual Question Answering via Late Knowledge-to-Text Injection. In IJCKG. ACM, 20–29.
- [26] Jinhao Jiang, Kun Zhou, Zican Dong, Keming Ye, Wayne Xin Zhao, and Ji-Rong Wen. 2023. StructGPT: A General Framework for Large Language Model to Reason over Structured Data. CoRR abs/2305.09645 (2023). 
- [27] Jinhao Jiang, Kun Zhou, Xin Zhao, and Ji-Rong Wen. 2023. UniKGQA: Unified Retrieval and Reasoning for Solving Multi-hop Question Answering Over Knowledge Graph. In ICLR. OpenReview.net.
- [38] Haoran Luo, Haihong E, Zichen Tang, Shiyao Peng, Yikai Guo, Wentai Zhang, Chenghao Ma, Guanting Dong, Meina Song, and Wei Lin. 2023. ChatKBQA: A Generate-then-Retrieve Framework for Knowledge Base Question Answering with Fine-tuned Large Language Models. CoRR abs/2310.08975 (2023).
- [76] Lingxi Zhang, Jing Zhang, Yanling Wang, Shulin Cao, Xinmei Huang, Cuiping Li, Hong Chen, and Juanzi Li. 2023. FC-KBQA: A Fine-to-Coarse Composition Framework for Knowledge Base Question Answering. In ACL (1). Association for Computational Linguistics, 1002–1017.

### 2.2 Preference Alignment for LLMs

## 3 PROBLEM SETTING

- **目标**：使用QA数据集$\mathcal{D} = \{(𝑞_𝑖, 𝑎_𝑖 ) | 𝑖 = 1, 2, . . . , 𝑁 \}$微调LLM$\mathcal{M}$ 
  - qi和ai是QA对
- **Vanilla fine-tuning**：首先用提示模板$\mathcal{I}$包装QA对，模型$\mathcal{M}$ 通过autoregressive loss进行优化，表示为：
  - <img src="./assets/CleanShot 2024-03-15 at 15.54.16@2x.png" alt="CleanShot 2024-03-15 at 15.54.16@2x" style="zoom:50%;" />
    - aij：答案ai的第j个token
    - $P_\mathcal{M}$：模型$\mathcal{M}$预测的tokne的概率
  - 这是LLMs的基本调整方法。有了这样一个训练目标，训练QA数据就作为监督信息来调整模型$\mathcal{M}$以适应QA场景
- **domain-specific task**:基于文档构建**cloud product knowledge graph (CPKG)**$\mathcal{G}=(\mathcal{E},\mathcal{R},\mathcal{T})$ 
  - 分别是：实体集合、关系集合、三元组集合
  - 通过检索相关性更高的前k个知识，输入提示将包含已检索到的知识$\mathcal{K}$
  - 因此，$\mathcal{M}$可以在VFT过程中学习相关知识，这是用于特定领域LLM应用的通用流程

以上的这个过程不能有良好的结果：

1. 在实际场景中的应用应该用户友好，否则它们将无法带来商业价值，因此输出要用户可接受
2. 知识检索过程是**无监督的，难以保证检索到的知识的有效性**，这意味着模型$\mathcal{M}$需要获得判断和选择性利用知识三元组的能力

**apply preference alignment during LLM fine-tuning** 微调应用偏好对齐：

- preference set：$\mathcal{P} = \{b_1, b_2, . . . , b_𝑙 \}$  每个Qa对的l个不同的答案。我们将 𝑟𝑖 表示为每个答案 𝑏𝑖 的偏好分数，其中较高的 𝑟𝑖 表示人类更喜欢这个答案
- 训练过程中定义另一个目标$\mathcal{L}_{align}$ ，让模型M与偏好集合P对齐：<img src="./assets/CleanShot 2024-03-15 at 16.08.00@2x.png" alt="CleanShot 2024-03-15 at 16.08.00@2x" style="zoom:50%;" />

在这样一个多任务目标下，模型M被微调以适应黄金答案，同时避免不受欢迎的结果

## 4 KNOWLEDGEABLE PREFERENCE ALIGNMENT PIPELINE

KnowPAT的流程，包含三个主要部分：无监督三元组linking，知识偏好集构建，微调和训练

<img src="./assets/CleanShot 2024-03-15 at 16.17.08@2x.png" alt="CleanShot 2024-03-15 at 16.17.08@2x" style="zoom:50%;" />

### 4.1 Unsupervised Triple Linking

- 将CPKG $\mathcal{G}$中的三元组与每个问题 𝑞𝑖 相关联
  - 简单的基于语义相似性的retrieer$\mathcal{H}$
    - $sim(i, j) = Cosine(H(q_i ), H (h_j , r_j , t_j ))$
    - H 作为textual encoder
    - 相似性基于余弦函数
    - 为每个问题qi检索top-k个三元组
    - 检索的知识(RK) as $\mathcal{K}$
    - RK将被添加到输入提示中，作为当前问题的背景知识
    - **过程是无监督的，并且需要强大的零样本泛化能力，**但是检索到的知识 $\mathcal{K}$ 可能存在噪音，并且无法提供解决问题所需的背景知识，因此LLM需要**学习知识偏好**，从**检索到的知识 $\mathcal{K}$中选择有用的信息**。

### 4.2 Knowledgeable Preference Set Construction

the style preference set $\mathcal{P}_s$ and the knowledge preference set  $\mathcal{P}_k$

- style preference set (SPS) $\mathcal{P}_s$ 
  - 选择l − 1个LLM（性能不一，且不如golden answer），与人工标记的golden答案生成一个长度为l的**style preference set$\mathcal{P}_s=\{b_1,b_2,...,b_l\}$** 
- knowledge preference set (KPS) $\mathcal{P}_k$ 
  - 我假设具有高相似度但未达到前top-k的三元组更可能是对输入问题无用的知识，通过检索一些相对较差的知识并促使模型生成具有不同质量知识的响应，我们可以获得具有不同质量的偏好集
  - 检索三组三元组 $\mathcal{K}_1,\mathcal{K}_2,\mathcal{K}_3$ 
    - $\mathcal{K}_1$:检索的top-k三元组
    - $\mathcal{K}_2=\empty$:空集
    - $\mathcal{K}_3$：top k + 1 to 2k，容易误用的知识，语义相似度相对较高
  - 给LLM生成不同的答案
    - 这些生成的3个答案和黄金答案形成了一个风格偏好集合$\mathcal{P}_s=\{c_1,c_2,c_3,c_4\}$ 
- 通过这样做，可以为每个QA对获得两个偏好集
  - 让l=4，集合大小相等
  - 设计了一种基于规则的策略来决定每个答案的偏好分数 𝑟
    - **style preference set $\mathcal{P}_s$**:高质量的黄金答案 𝑏1 被分配了最高分数，并且其他LLM的答案根据它们的一般能力确定
      - ChatGPT > ChatGLM > Vicuna
      - $r_1 > r_2 > r_3 > r_4$
    - **knowledge preference set $\mathcal{P}_k$**:golden answer c1 分最高，top-k第二c2，没有用知识c3，误用的无关知识c49在我们的实际测试中发现，检索到的知识K3与问题𝑞之间的不匹配率非常高，并且很容易误导模型M，因此我们将其得分设置为低于空知识K2情况。）
      - $r_1 > r_2 > r_3 > r_4$
  - 保持这种相对顺序将简化代码的实现。
- 对于每个QA对，构建两个偏好集，并最终获得包含2𝑁偏好集的**整体偏好数据**，偏好数据参与微调过程以控制模型$\mathcal{M}$的风格偏好和知识偏好

### 4.3 Fine-tuning and Preference Alignment

设计了一个分数，表示偏好：

<img src="./assets/CleanShot 2024-03-15 at 18.03.30@2x.png" alt="CleanShot 2024-03-15 at 18.03.30@2x" style="zoom:50%;" />

- 分数Si每个答案的是**平均对数似然**，条件是给定的提示模板$\mathcal{I}$和问题查询qi

为了使模型偏好与我们的设想保持一致，我们为我们的场景设计了一个**新的对齐目标**，表示为：

<img src="./assets/CleanShot 2024-03-15 at 18.08.07@2x.png" alt="CleanShot 2024-03-15 at 18.08.07@2x" style="zoom:50%;" />

- 实现偏好对齐过程，该过程对比了preferred答案和unpreferred答案
  - **notice：**人类偏好评分 𝑟𝑖 仅确定与不同答案对应的排序，而不会直接参与计算和梯度累积
  - 现存的方法RRHF [71] and SLiC-HF [83]使用Margin-rank loss：<img src="./assets/CleanShot 2024-03-15 at 18.14.53@2x.png" alt="CleanShot 2024-03-15 at 18.14.53@2x" style="zoom:33%;" />实现偏好对齐，但是他们的设计只有在人类偏好答案的模型偏好分数S低于不受欢迎答案时才进行优化（更正式的表述为当𝑟𝑗 < 𝑟𝑖 时，S𝑖 < S𝑗）。
  - 本文认为，在应该以持续降低不受欢迎答案的发生概率
- 同时，由于不同答案具有不同的文本质量和偏好程度，进一步设计了一个自适应权重来控制每个首选答案的影响，该自适应权重表示为：
  - <img src="./assets/CleanShot 2024-03-15 at 18.17.34@2x.png" alt="CleanShot 2024-03-15 at 18.17.34@2x" style="zoom:50%;" />
  - S𝑚𝑎𝑥和S𝑚𝑖𝑛分别是偏好集合P中的最大和最小模型偏好分数
  - 具有这样一种自适应权重，不同偏好答案的影响可以动态调整。然后对齐损失变为：
    - <img src="./assets/CleanShot 2024-03-15 at 18.18.16@2x.png" alt="CleanShot 2024-03-15 at 18.18.16@2x" style="zoom:50%;" />
  - 最终的训练目标仍然是以多任务方式进行，我们添加了一个超参数 𝜆 作为对齐损失的系数：
    - <img src="./assets/CleanShot 2024-03-15 at 18.18.40@2x.png" alt="CleanShot 2024-03-15 at 18.18.40@2x" style="zoom:50%;" />
    - P − 1代表了偏好-不偏好对比的计数，以规范化对齐损失。
  - 针对在前一节构建的每个偏好集合，模型都会根据这样一个目标进行训练和优化。

## 5 EXPERIMENT SETTINGS

### 5.1 Dataset Information

- CPKG：which consists of 13995 entities, 463 relations, and 20752 triples
- The QA dataset consists of 8909 QA pairs and we split the dataset into 7909/500/500 for training/validation/test.
- For each data instance in the training, we construct two preference sets and finally get 15818 preference sets with 4 answers in each set.

### 5.2 Baseline Methods

1. Zero-shot approach：directly prompts the LLM
2. In-context learning approach ：sample a few (𝑘-shot) QA pairs as demonstrations from the training dataset
3. Vanilla fine-tuning approach：fine-tunes the LLM using the QA pairs with retrieved knowledge as Equation 1
4. Preference alignment approaches：additional preference alignment objectives during training
5. five existing state-of-the-art (SOTA)
   1. RRHF [71]
   2. SLiC-HF [83]
   3. PRO [48]
   4. AFT (both AFT-BC and AFT-DC) [58]

### 5.3 Evaluation Metrics

1. Traditional text generation metrics
   1. BLEU [43], ROUGE [32], CIDEr [56], and METEOR [3]————不能提供语意上的相关性和深入的理解
2. Model-based metrics.
   1. BERTScore [78]：Bert计算语意相似度
   2. perplexity (PPL)：LLM的能力理解并预测整个句子
   3. preference score：S mentioned in Equation 4，反应模型的preference degree
      1. <img src="./assets/CleanShot 2024-03-15 at 18.25.50@2x.png" alt="CleanShot 2024-03-15 at 18.25.50@2x" style="zoom:25%;" />

### 5.4 Implementation Details

- **LLM：**Atom-7B：fully open-source version of Llama2 with Chinese vocabulary extension
- **Retriever：**BGE-base-zh-v1.5 [67]

## 6 RESULTS ANALYSIS

- RQ1: How does the proposed method KnowPAT **perform** compared with the baseline methods? ————performance
- RQ2: Do the proposed **modules** in KnowPAT really benefit the performance of KnowPAT? ————design soundness
- RQ3: Are there some intuitive cases to demonstrate the **effectiveness** of KnowPAT? ————intuition
- RQ4: Does the LLM still keep the **general ability** rather than catastrophic forgetting? ————usability in real scenatios

### 6.1 Main Results (Q1)

  <img src="./assets/CleanShot 2024-03-15 at 18.32.36@2x.png" alt="CleanShot 2024-03-15 at 18.32.36@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-15 at 19.31.41@2x.png" alt="CleanShot 2024-03-15 at 19.31.41@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-15 at 19.33.28@2x.png" alt="CleanShot 2024-03-15 at 19.33.28@2x" style="zoom:50%;" />

- more acceptable to humans

### 6.2 Ablation Study (Q2)

fine-tuning objective$\mathcal{L}_{ft}$ and the alignment objective $\mathcal{L}_{align}$ are both contributing for the model performance

cloud product knowledge graph (CPKG)

- w/o RK removes the retrieved knowledge during the fine-tuning and preference alignment process
- w/o KG without KG in the whole process，**KPS(knowledge preference setting)** and RK (retrieved knowledge) in the input prompt are all removed
- 分析：CPKG does not only serve as an **external knowledge source during training** but also participates in the **preference set construction process**, which is **important** to the model performance.

<img src="./assets/CleanShot 2024-03-15 at 19.58.35@2x.png" alt="CleanShot 2024-03-15 at 19.58.35@2x" style="zoom:50%;" />

### 6.3 Case Study (Q3)

<img src="./assets/CleanShot 2024-03-15 at 19.59.02@2x.png" alt="CleanShot 2024-03-15 at 19.59.02@2x" style="zoom:50%;" />

- similar to the golden answer
- keeping a user-friendly tone and providing sufficient information（第二个）
- **retrieved knowledge in the first case is** (EIP, used for, IP Binding), (Select Box, belongs to, Alarm Management Component),都没用，但是**没有被误导**

### 6.4 Knowledge Retention Analysis (Q4)

<img src="./assets/CleanShot 2024-03-15 at 20.03.36@2x.png" alt="CleanShot 2024-03-15 at 20.03.36@2x" style="zoom:50%;" />

- five distinctive commonsense regions (history, clinical（临床）, politics, computer science, and economics)
- 出了临床，别的都还挺好的
- PRO在经济问题上意外地显示出显著改善，但在其他几个领域比KnowPAT表现更明显的性能下降

## 7 CONLUSION

In this paper, we introduce a novel framework, **knowledgeable preference alignment (KnowPAT)**, for **domain-specific QA tasks** in cloud product services, **leveraging LLMs and KGs in a practical application setting**. Our approach **constructs a knowledgeable preference set by retrieving** and **utilizing knowledge triples to generate answers with different quantities**. **A new alignment objective** is designed to unleash the power of the **preference set**. Comprehensive experiments demonstrate that our method surpasses existing solutions for this **real-world challenge**. Looking ahead, we aim to apply KnowPAT to additional business scenarios and further investigate the potential of KG-enhanced LLMs.