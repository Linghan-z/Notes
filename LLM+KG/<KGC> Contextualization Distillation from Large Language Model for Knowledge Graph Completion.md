# Contextualization Distillation from Large Language Model for Knowledge Graph Completion

Code: https://github.com/DavidLi0406/Contextulization-Distillation

## Abstract

PLM-based KGC models 问题：

1. **static and noisy** nature of existing corpora collected from Wikipedia articles
2. **synset definition 同义词**

==**Contextualization Distillation** 情景化（上下文）蒸馏==

- 辨别和生成KGC都可以
- 1. instructing LLMs 把triples -> context-rich segments
  2. 两个定制的辅助任务，让smaller KGC模型可以从这些丰富的三元组中吸收见解
     1. reconstruction
     2. contextualization

## 1 Introduction

先前尝试通过维基百科文章(Zhong et al., 2015)或同义词集定义(Yao et al., 2019)来增强PLM-based KGC模型的文本数据遇到了一定的限制：

1. 实体描述通常简洁且静态，可能会阻碍在知识图谱模型中对实体形成全面理解
2. 整合三元组的描述可能会丰富信息，但可能会引入大量噪音，尤其是通过自动实体对齐(Sun et al., 2020)

- 例子：

  <img src="./assets/CleanShot 2024-03-16 at 13.44.08@2x.png" alt="CleanShot 2024-03-16 at 13.44.08@2x" style="zoom:50%;" />

对比了ChatGPT 和PaLM2在KGC问题上的性能，表示差异很大，并且虽然直接利用LLMs进行KGC任务是直观的，但通过微调更小、专门化的KGC模型表现更好

==**Contextualization Distillation**==————**plug-in-and-play**

1. extracts descriptive contexts from LLMs -> securing **dynamic**, **high-quality context** for each **entity and triplet**
2. 两个辅助任务auxiliary tasks，使用这些信息丰富、描述性的上下文训练较小的KGC模型

**Contribution：**

1. 分析现阶段PLMs-based KGC模型的语料库的不足，提出了Contextualization Distillation，利用LLM的知识增强KGC模型的能力
2. 实验
3. 我们深入研究了我们提出的方法，并就为**蒸馏生成路径选择**以及**适当的蒸馏任务选择**提供宝贵见解和指导。

## 2 Related Work

### 2.1 Knowledge Graph Completion

PLMs：

- **Yao et al. (2019)** first propose to use BERT (Kenton and Toutanova, 2019) to encode the entity and relation’s name and adopt a binary classifier to predict the validity of given triplets.
- **Wang et al. (2021a)** leverage the Siamese network to encode the head-relation pair and tail in a triplet separately, aiming to reduce the time cost and make the inference scalable
- **Lv et al. (2022)** convert each triple and its textual information into natural prompt sentences to fully inspire PLMs’ potential in the KGC task.
- **Chen et al. (2023a)** design a conditional soft prompts framework to **maintain a balance between structural information and textual knowledge** in KGC.
- 也有一些工作试图利用生成的PLM以序列到序列的方式执行KGC，并取得了令人满意的结果：**(Xie et al., 2022; Saxena et al., 2022; Chen et al., 2022a)**

### 2.2 Distillation from LLMs

**transferring expertise from** larger, highly competent **teacher models **to **smaller**, affordable student models

LLM -> smaller PLMs

- One of the most common methods is to **prompt LLMs to explain their predictions** and then use such rationales to **distill their reasoning abilities into smaller models**

Distilling conversations from LLMs

- 构建对话dataset
- 增强已有
- 领域知识

## 3 Contextualization Distillation

<img src="./assets/CleanShot 2024-03-16 at 14.38.27@2x.png" alt="CleanShot 2024-03-16 at 14.38.27@2x" style="zoom:50%;" />

### 3.1 Extract Descriptive Context from LLMs

1. **entity description (ED)**
2. **triplet description (TD)**

Given triplets of a **knowledge graph $t_i ∈ T$** , we first curate **prompt $p_i$** for the $i^{th}$ triplet by filling the pre-defined template:

<img src="./assets/CleanShot 2024-03-16 at 20.06.26@2x.png" alt="CleanShot 2024-03-16 at 20.06.26@2x" style="zoom:50%;" />

where hi, ri, ti are the head entity, relation, and tail entity of the ith triplet.

Then, we use $p_i$ as the **input** to prompt the LLM to generate **the descriptive context $c_i$** for each triplet:

<img src="./assets/CleanShot 2024-03-16 at 20.07.52@2x.png" alt="CleanShot 2024-03-16 at 20.07.52@2x" style="zoom:50%;" />

### 3.2 Generating Path

- T --> (ED, TD)：同时生成实体描述和三元组描述（主要方法）
- T --> ED：
- T --> TD
- T --> RA：促使LLM生成理由而不是描述性背景
- T --> ED --> TD：以两步方式生成实体描述和三元组描述。通过连接文本的两个部分获得最终的描述性上下文

### 3.3 Multi-task Learning with Descriptive Context 使用描述性上下文进行多任务学习

设计了一个多任务学习框架，让它们可以从知识图谱任务和辅助描述性上下文任务中学习

- reconstruction：判别模型
- contextualizatioin：生成模型

#### 3.3.1 Reconstruction

任务的目标是**训练模型以==恢复损坏的描述性上下文==**

- follow the implementation of Kenton and Toutanova (2019) and use **masked language modeling (MLM)**
- **such auxiliary selfsupervised tasks in the domain-specific corpus can benefit downstream applications**

MLM 在描述性上下文中随机识别了 15% 的token，在这些token中，80%被战术性地**隐藏**起来，使用特殊的标记“< *Mask* >”，10%被无缝**替换为随机token**，而剩下的10%保持不变

对于每个选择的token，MLM 的目标是在该特定位置恢复原始内容，通过交叉熵损失实现

<img src="./assets/CleanShot 2024-03-16 at 19.54.00@2x.png" alt="CleanShot 2024-03-16 at 19.54.00@2x" style="zoom:50%;" />

final loss of **discriminative KGC models**is the combination of the **KGC loss**（模型原本的设计的损失函数） and the proposed **reconstruction loss**：

<img src="./assets/CleanShot 2024-03-16 at 19.55.11@2x.png" alt="CleanShot 2024-03-16 at 19.55.11@2x" style="zoom:50%;" />

$\alpha$是超参

#### 3.3.2 Contextualization

上下文化的目标**是在提供原始三元组$ t_i = h, r, t$ 时，指导模型==生成描述性上下文 $c_i$==**

与reconstruction相比，contextualization要求PLM具有更加细致和复杂的能力,需要PLM准确把握涉及的两个实体的含义以及将它们联系在一起的固有关系，以生成流畅且准确的描述

将头部、关系和尾部用特殊标记“< *Sep* >”连接起来作为输入：

<img src="./assets/CleanShot 2024-03-16 at 20.02.41@2x.png" alt="CleanShot 2024-03-16 at 20.02.41@2x" style="zoom:50%;" />

然后，我们将它们输入到生成式PLM中，并训练模型使用交叉熵损失来生成描述性上下文ci：

<img src="./assets/CleanShot 2024-03-16 at 20.03.03@2x.png" alt="CleanShot 2024-03-16 at 20.03.03@2x" style="zoom:50%;" />

final loss of **discriminative KGC models**is the combination of the **KGC loss**（模型原本的设计的损失函数） and the proposed **contextualization loss**：

<img src="./assets/CleanShot 2024-03-16 at 20.03.36@2x.png" alt="CleanShot 2024-03-16 at 20.03.36@2x" style="zoom:50%;" />

## 4 Experiment

### 4.1 Experimental Settings

#### Datasets

- WN18RR (Dettmers et al., 2018)：删除WN18中的逆向关系，防止数据泄露
- FB15k-237N (Lv et al., 2022)：消除源自Freebase中介节点的级连关系（Akrami等，2020年），以避免笛卡尔乘积关系问题

#### Baselines

- KG-BERT (Yao et al., 2019)：first to suggest utilizing PLMs for the KGC task
- CSPromKG (Chen et al., 2023a)：combines PLMs with traditional Knowledge Graph Embedding (KGE) models, achieving a balance between efficiency and performance in KGC
- GenKGC (Xie et al., 2022)：is the first to accomplish KGC in a sequence-to-sequence manner, with a fine-tuned BART (Lewis et al., 2020) as its backbone
- KGS2S (Chen et al., 2022a)：adopt soft prompt tuning and lead to a new SOTA performance among the generative KGC models

#### Implementation details

- RTX A6000
- PaLM2-540B
- $α ∈ {0.1, 0.5, 1.0}$
- measure matrics
  - Mean Reciprocal Rank (MRR)
  - Hits@1, Hits@3 and Hits@10

### 4.2 Main Result

<img src="./assets/CleanShot 2024-03-16 at 20.27.47@2x.png" alt="CleanShot 2024-03-16 at 20.27.47@2x" style="zoom:50%;" />

- 提升了context-based KGC模型的能力

### 4.3 Ablation Study on Generating Path

<img src="./assets/CleanShot 2024-03-16 at 20.30.12@2x.png" alt="CleanShot 2024-03-16 at 20.30.12@2x" style="zoom:50%;" />

- RA那个提供解释的路径，往往是难理解的和结构复杂的，因此效果不好
- T --> ED --> TD：也效果不好，归因于由三个描述段落串联而成导致的文本不连贯
- 总结：**smaller models can benefit more from comprehensive, descriptive and coherent content generated by LLMs.**

### 4.4 Ablation Study on Descriptive Context

<img src="./assets/CleanShot 2024-03-16 at 20.39.12@2x.png" alt="CleanShot 2024-03-16 at 20.39.12@2x" style="zoom:50%;" />

大型语言模型生成的语料库有效地解决了先前知识图谱补全中存在的限制，从而为KGC模型带来更显著的改进

### 4.5 Ablation Study on ==Generative== KGC Models

<img src="./assets/CleanShot 2024-03-16 at 20.42.36@2x.png" alt="CleanShot 2024-03-16 at 20.42.36@2x" style="zoom:50%;" />

contextualization是生成式KGC模型必须掌握的关键能力，以提高KGC性能

### 4.6 Efficiency Analysis

<img src="./assets/CleanShot 2024-03-16 at 20.44.44@2x.png" alt="CleanShot 2024-03-16 at 20.44.44@2x" style="zoom:50%;" />

辅助蒸馏任务带来的**额外培训成本**可能对我们的方法构成潜在限制

很明显，具有上下文蒸馏的CSProm-KG实现了**更快的收敛**，并在较早时（大约在125个epochs）达到最佳检查点，而不使用我们方法的变体则需要更长时间（大约在220个epochs）

**辅助蒸馏损失也可以加快KGC模型的学习**

trade-off between batch processing time and training steps（批处理时间和训练步骤）

### 4.7 Case Study

<img src="./assets/CleanShot 2024-03-16 at 20.49.18@2x.png" alt="CleanShot 2024-03-16 at 20.49.18@2x" style="zoom:50%;" />

## 5 Conclusion

在这项工作中，我们提出了上下文蒸馏（Contextualization Distillation）的概念，通过促使语言模型生成描述性上下文来解决现有知识图谱补全（KGC）文本数据的局限性。为确保我们的方法能够适用于各种基于预训练语言模型（PLM）的KGC模型，我们设计了一个多任务学习框架。在这个框架内，我们结合了两个辅助任务：reconstruction和contextualization，在训练更小规模的KGC模型时提供信息丰富的描述性上下文。我们对几个主流KGC基准进行实验，并结果表明，我们的上下文蒸馏一直能够增强基线模型的性能。此外，我们进行深入分析以使得方法效果更易解释，并指导如何有效利用语言模型改进KGC。未来，我们计划将该方法应用到其他知识驱动任务中，比如实体链接和知识图问题回答等领域。

## 6 Limitation

由于计算资源的限制，我们在两个KGC数据集上评估了我们的方法，同时忽略了诸如时间知识图谱补全（Garcia-Duran等人，2018年）、少样本知识图谱补全（Xiong等人，2018年）和常识知识图谱补全（Li等人，2022年）等场景。在未来研究中，我们计划调查我们的方法在更广泛的情况下的有效性。