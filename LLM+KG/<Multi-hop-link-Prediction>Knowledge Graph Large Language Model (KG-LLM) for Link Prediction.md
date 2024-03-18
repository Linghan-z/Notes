# Knowledge Graph Large Language Model (KG-LLM) for Link Prediction

> 2024.3.13
>
> 多跳的链接预测...不像是补全啊呜呜呜
>
> 看都看了

## Abstract

**chain-of-thought (CoT) prompting and in-context learning (ICL), to enhance ==multi-hop link prediction== in KGs.**

## 1 Introduction

3 major challenges：

1. 主要方法是判别模型，而非生成模型，需要具备利用推理能力来解决知识图谱中多跳链接预测问题的模型
2. 现有的链接预测主要关注的是一阶，对于高阶的链接预测不足，影响对于多跳的推理
3. 传统的方法缺乏生成能力，对于未见的任务能力不足

==Knowledge Graph Large Language Model Framework (KG-LLM Framework)==

- **multi-hop prediction**
- 

<img src="./assets/CleanShot 2024-03-17 at 11.18.27@2x.png" alt="CleanShot 2024-03-17 at 11.18.27@2x" style="zoom:50%;" />

1. takes input of the **original KG dataset**
2. After preprocessing, a path in the KG is **transformed into a chain-of-thought (CoT) prompt**, enclosing through a series of relational statements, which can be represented as **{Node 1 (has relation_x with) Node 2, Node 2 (has relation_y with) Node 3, etc.}.**
   1. **CoT prompt的复杂度取决于：路径长度、节点数量、连接数，与它所代表的多跳问题的复杂程度直接相关**

**contributions**：

- 提升KG的生成式多跳推理
- 通过将多跳链接预测从传统的分类范式重新定位为生成模型，我们的框架显著简化了用户的调试工作
- 提高了LLMs对未见提示的泛化能力。

## 2 Related Work

- large-scale language models
- Chain-of-Thought (CoT) reasoning ability
- In-Context Learning (ICL)

## 3 Methodology

### 3.1 Knowledge Graph Definition

#### Multi-hop Link Prediction：

多跳链接预测的任务不仅仅是简单的边预测，而是旨在识别知识图中多个关系步骤内丢失的连接

connected path:$P_{obs} = (e_1, r_1, e_2), (e_2, r_2, e_3), . . . , (e_{n−1}, r_{n−1}, e_n) ⊆ L$

objective is to **predict whether a missing link $l_{miss} = (e_1, ?, e_n)$ by answering True or False**

#### Multi-hop Relation Prediction

this task delves into **specifying the relationship**

识别实体的关系

### 3.2 Knowledge Prompt

conversion of a given sequence of observed triples **$P_{obs}$ => natural language**

通过在训练过程中利用知识提示，模型能够更有效地理解知识图谱中存在的潜在关系和模式，从而提高多跳链接预测任务的整体性能

two types of knowledge prompts：

- standard knowledge prompt
  - <img src="./assets/CleanShot 2024-03-17 at 15.03.42@2x.png" alt="CleanShot 2024-03-17 at 15.03.42@2x" style="zoom:50%;" />
  - 清晰简洁，提供对知识图谱的深入理解，并促进预测准确性的提高
- KG-LLM knowledge prompt
  - <img src="./assets/CleanShot 2024-03-17 at 15.03.55@2x.png" alt="CleanShot 2024-03-17 at 15.03.55@2x" style="zoom:50%;" />
  - 包括指令和输入的结构化形式，把复杂问题分解成简单的小过程

<img src="./assets/CleanShot 2024-03-17 at 15.17.36@2x.png" alt="CleanShot 2024-03-17 at 15.17.36@2x" style="zoom:50%;" />

### 3.3 KG-LLM Framework

- <img src="./assets/CleanShot 2024-03-17 at 11.18.27@2x.png" alt="CleanShot 2024-03-17 at 11.18.27@2x" style="zoom:50%;" />

- In the **initial stage**, the original KG is taken as input.

  - The preprocess function randomly selects a unique path in the KG and converts it into the KG-LLM knowledge prompt.

- During the **fine-tuning phase**：Flan-T5-Large, LlaMa2-7B, and Gemma-7B

  - A **global fine-tuning strategy** is employed on Flan-T5 to boost its performance
  - For LlaMa2 and Gemma, a 4-bit quantized **LoRA** (Low-Rank Adaptation) modification

- During the **training process**

  - **cross-entropy loss function L**：它计算了模型预测的token概率与期望输出序列中实际token概率之间的差异
  - In the following equation, n represents the length of the expected output sequence, x stands for the input instruction, and yi denotes the i-th token in the expected output sequence：
    - <img src="./assets/CleanShot 2024-03-17 at 15.16.48@2x.png" alt="CleanShot 2024-03-17 at 15.16.48@2x" style="zoom:50%;" />

- 虽然在图中，LLM用在分类，但是通过在说明中列出所有可能的选项，LLMs可以更有效地遵循并根据给定选择生成响应

  - > .?

## 4 Experiments

- Q1: Which framework demonstrates superior efficacy in multi-hop link prediction tasks in the absence of ICL?
- Q2: Does incorporating ICL enhance model performance on multi-hop link prediction tasks?
- Q3: Is the KG-LLM framework capable of equipping models with the ability to navigate unseen prompts during multi-hop relation prediction inferences?
- Q4: Can the application of ICL bolster the models’ generalization ability in multihop relation prediction tasks?

### 4.1 Experimental Setup

#### Datasets.

<img src="./assets/CleanShot 2024-03-17 at 15.23.14@2x.png" alt="CleanShot 2024-03-17 at 15.23.14@2x" style="zoom:50%;" />

#### Task splits.

#### Comparing Baselines.

- TransE [2]
- Analogy [9] 
- CompleX [20]
- DistMult [30]
- RESCAL [12]

#### Implementation Details.

#### Metrics for Multi-hop Link Prediction

- Area Under the ROC Curve (AUC) metric :
  - AUC measures the area under the Receiver Operating Characteristic (ROC) curve
  - 该曲线在不同分类阈值下绘制真正例率与假正例率
  - 较高的AUC值表示模型区分正面和负面示例的能力更好
- F1 score

#### Metrics for Multi-hop Relation Prediction.

- accuracy

### 4.2 Multi-hop Link Prediction without In-Context Learning

<img src="./assets/CleanShot 2024-03-17 at 15.28.20@2x.png" alt="CleanShot 2024-03-17 at 15.28.20@2x" style="zoom:50%;" />

### 4.3 Multi-hop Link Prediction with In-Context Learning

<img src="./assets/CleanShot 2024-03-17 at 15.28.49@2x.png" alt="CleanShot 2024-03-17 at 15.28.49@2x" style="zoom:50%;" />

关于**第二个数据集**中**Flan-T5模型**在**标准框架**下，性能在ICL整合后*没有改善甚至略有下降*

- This phenomenon could be attributed to the increased length and complexity of the testing prompts induced by the added ICL context.

KG-LLM的框架可以提高LLM的ICL的能力

### 4.4 Multi-hop Relation Prediction without In-Context Learning

<img src="./assets/CleanShot 2024-03-17 at 15.36.48@2x.png" alt="CleanShot 2024-03-17 at 15.36.48@2x" style="zoom:50%;" />

在检查预测结果时，我们发现模型更倾向于负面关系的预测而不是正面关系的预测，在这种情况下，模型为负实例生成了“无关系”的输出，这种趋势在两个框架下的模型中保持一致。

- **两个框架之间性能差异主要来自于KG-LLM模型更擅长准确识别某些正向关系这一事实**



<img src="./assets/CleanShot 2024-03-17 at 15.36.59@2x.png" alt="CleanShot 2024-03-17 at 15.36.59@2x" style="zoom:50%;" />

### 4.5 Multi-hop Relation Prediction with In-Context Learning

**significant improvement in the generalization abilities** of the models both under the standard framework and the KG-LLM framework

## 5 Conclusions and Future Work

。。

