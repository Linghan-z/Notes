# KICGPT: Large Language Model with Knowledge in Context for Knowledge Graph Completion

> 2023.12
>
> EMNLP

## Abstract

KGC:

- triple-based(基于embedding的）:struggle with long-tail entities due to limited **structural information** and **imbalanced entity distributions** 利用结构信息
  - Given the typical imbalance of entities in KGs, long-tail entities are prevalent and the KGC task has limited structural information about them.鉴于知识图谱中实体的典型不平衡性，长尾实体普遍存在，并且知识图谱构建任务对它们的结构信息有限。
- text-based（基于PLM的）:require costly training for language models and specific **finetuning** for knowledge graphs, which limits their efficiency.
  - this is resource-intensive and requires task-specific finetuning for each downstream task.

提出：==**KICGPT**==——integrates a large language model (**LLM**) and a **triple-based KGC retriever**

- uses an in-context learning strategy called **Knowledge Prompt**, encodes **structural knowledge** into demonstrations to guide the LLM.

## 1 Introduction

利用LLMs做KGC的缺陷：

1. First, the LLM outputs can be unconstrained and may **fall outside the scope of** entities in the KGs.
2. Second, LLMs impose **length limits** on the input tokens, and the limits are **far from sufficient for describing a complete KGC task**.
3. Lastly, there is **no effective in-context learning prompt** design for LLM on KGC tasks.

提出==**K**nowledge **I**n **C**ontext with **GPT** (KICGPT) framework.==

- integrates LLMs with a **traditional structure-aware KG model** (which is called a ==**retriever**==).
  - 对于预测实体的链接预测任务，the retriever first processes the **query q independently** and generates an ordered **candidate entity list** $R_{retriever}$ that ranks all entities in the KG based on their retrieval scores.
  - The LLM then performs **re-ranking** on the top $m$ entities returned by $R_{retriever}$, and replaces these $m$ entities with re-ranked ones returned by the LLM as the final result $R_{KICGPT}$ .
    - **Knowledge Prompt** for re-ranking, using ICL, encode the KG knowledge into demonstrations in prompts.
- 与现有的基于三元组的方法相比，KICGPT 能够同时利用知识源（即 KG 和 LLM 的知识库），并促进它们的对齐和丰富化，以减轻长尾实体信息稀缺问题。
- formalizing link prediction as a re-ranking task for the given sequence Rretriever.==>不会结果不可控
- standard link prediction task requires ranking for all the entities, which is not feasible for LLM due to the length limit on input tokens.
  - KICGPT allows LLM to perform re-ranking the entities which in the triple-based model's output set.

**Contributions:**

- KICGPT
- knowledge prompting
- experiments

## 2 Related Work

KGC

- triple-based KGC:
  - 基础方法
    - KGE
    - translation-based(TransE)
    - emantic matching models(RESCAL (Nickel et al., 2011) and DistMult (Yang et al., 2014))
  - 由于使用浅层网络结构，它们受限于表达能力有限。
    - GNN
    - CNN
    - Transformer
  - 可以解决长尾实体的问题的方法：
    - Meta-learning
    - logical rules
    - 利用的是KG内部的信息，而本方法用的是来自LLM的外部信息
- Text-based KGC:
  - CNN(DKRL (Xie et al., 2016) first introduces textual descriptions into entity embeddings produced by a convolutional neural network.)
  - PLM

LLM4KG

ICL for LLMs

## 3 Methodology

### 3.1 Problem Setting

A link prediction model usually needs to score all plausible entities as missing entity and then rank all entities in descending order.

### 3.2 Overview

<img src="./assets/CleanShot 2024-03-18 at 20.44.40@2x.png" alt="CleanShot 2024-03-18 at 20.44.40@2x" style="zoom:50%;" />

#### two components:

- a triple-based KGC retriever 
  - For each query triple (h, r, ?), the retriever first generates the score of (h, r, e) for each entity e ∈ E. The ranking (in descending score) of all the entities is denoted $R_{retriever} = [e_{1st}, e_{2nd}, e_{3rd}, . . . , e_{|E|th}]$.
- a LLM
  - performs a **re-ranking** of the **top-m** entities based on its knowledge and demonstrations in the proposed ==**Knowledge Prompt**==.
  - The re-ranking $R_{LLM} = [e^′_{1st}, e^′_{2nd}, e^′_{3rd}, . . . , e^′_{mth}]$ is a permutation(排列组合) of$[e_{1st}, e_{2nd}, e_{3rd}, . . . , e_{|E|th}]$.

By replacing the m leading entities in $R_{retriever}$ by $R_{LLM}$ , the KICGPT outputs $R_{KICGPT}=[e^′_{1st}, e^′_{2nd}, e^′_{3rd}, . . . , e^′_{mth},e_{m+1th},  . . . , e_{|E|th}]$

### 3.3 Knowledge Prompt

- an **in-context learning strategy** specially designed for KGC tasks. 
  By **encoding part of the KG into demonstrations**, Knowledge Prompt boosts the performance of LLM on link prediction.

#### 3.3.1 Demonstration Pool

For each query (h, r, ?), we **construct two pools of triples, $D_a$ and $D_s$**, from the KG as demonstrations.

**Analogy Pool** 类比 pool

> 相同的关系，用于类比，让LLM理解query的语意

- contains triples that help the LLM to better understand the semantics of the query by analogy.
- Let $G_{train}$ and $G_{valid}$ be the sets of KG triples for training and validation, respectively.
- $D_a = {(e^′, r, e^{′′}) ∈ G_{train} ∪ G_{valid}|e^′, e^{′′} ∈ E}$ includes triples with the **same relation** as the query (h, r, ?).

**Supplement Pool** 补充pool

> 其他头实体参与的三元组

- The supplement pool Ds contains triples which provide supplementary information about the query’s head entity h.

<img src="./assets/CleanShot 2024-03-18 at 20.40.06@2x.png" alt="CleanShot 2024-03-18 at 20.40.06@2x" style="zoom:50%;" />

#### 3.3.2 Demonstration Ordering

propose **different ordering strategies** for the analogy and supplement pools.（两个pool不同的排序策略）

**analogy pool Da**

- all its triples are **similar to the query** because they share the **same relation**.

- ==**Diversity**====>LLM learn different analogy demonstrations

  - promotes diversity.

  - 对于Da中的每个Triple，先随机取一个triple，然后把triple中的head和tail的计数器counter都+1，然后取Da中的头和尾之和最少的triple，同时取出来的头尾实体的counter+1（tie --- random)，直到Da空。==> ordered list

  - > 减少analogy的重复的实体（尽量不重复）

<img src="./assets/CleanShot 2024-03-18 at 20.40.49@2x.png" alt="CleanShot 2024-03-18 at 20.40.49@2x" style="zoom:50%;" />

**supplement pool Ds**

- provide supplementary information on the query’s head entity h, we prefer related demonstrations to the query.

- ==**related**==

  - Specifically, we rank **all triples** in Ds according to their **BM25 scores**

  - > This score is used to evaluate the correlation between texts in each demonstration and query.

  - <img src="./assets/CleanShot 2024-03-18 at 20.41.02@2x.png" alt="CleanShot 2024-03-18 at 20.41.02@2x" style="zoom:50%;" />

在数据预处理阶段就把demonstration pool还有排序搞好了

#### 3.3.3 Prompt Engineering

1. a unified prompt template-- **query and demonstrations** => **plain text with the same format**

2. **multi-round interactions** =>LLM re-ranking

3. For each link prediction query (h, r, ?), KICGPT creates an independent conversational prompt--四个阶段：

   1. responsibility description：任务说明

   2. question and demonstration description：提出问题，说明demonstration（两部分demonstration不同）

   3. multiple demonstrations：给出具体的demonstration

      > To include more KG information and demonstrations, we repeat this step as many times as possible subject to the input token length limit.
      >
      > 文中给了好长的上下文，这样是否合理呢？

   4. final query：回答（re-ranking）

   <img src="./assets/CleanShot 2024-03-18 at 21.33.37@2x.png" alt="CleanShot 2024-03-18 at 21.33.37@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-18 at 20.41.15@2x.png" alt="CleanShot 2024-03-18 at 20.41.15@2x" style="zoom:50%;" />

### 3.4 Text Self-Alignment

KG text cleaning---It transforms the **raw text in the KG** to **more understandable descriptions** by the LLM.

- 关系描述一般都比较难懂，比如：“/tv/tv_program/country_of_origin”，以往的方法有：去除符号

- KICGPT原始用的方法：用of链接“country of origin of tv program of tv”

  - > 确实是看不懂这关系描述是说啥呢...

  - 创新的解决方法：使用ICL并让LLM从给定的使用原始描述的演示中总结自然文本描述

    - 前一部分不是用了一个analogy poll，生成了一个diversity的list么，用那个给LLM让LLMsummarize the semantics of the relation **into a sentence** (the self-aligned text description of r).
    - LLM的self-aligned text description是：“[T] is the country where the TV program [H] originated from.”
      - where [T ] and [H] are placeholders for the tail and head entities, respectively.

数据预处理阶段就用了text self-alignment来处理了关系

## 4 Experiment

### 4.1 Setup

#### Datasets.

- FB15k-237 (Toutanova et al., 2015)：commonsense knowledge about topics such as movies, sports, awards, and traveling.
- WN18RR (Dettmers et al., 2018)：knowledge about English morphology（更加稀疏）

<img src="./assets/CleanShot 2024-03-18 at 21.53.49@2x.png" alt="CleanShot 2024-03-18 at 21.53.49@2x" style="zoom:50%;" />

#### Baselines

#### Implementation details.

- Retriever：RotatE (Sun et al., 2019)
- LLM：ChatGPT (gpt-3.5-turbo)
- hyperparameter：
  - m：{10, 20, 30, 40, 50}
  - baych size：{4, 8, 16, 32}
- For the ChatGPT API, we set temperature, presence_penalty, and frequency_penalty to 0, and top_p to 1 to avoid randomness.

### 4.2 Experimental Results

<img src="./assets/CleanShot 2024-03-18 at 21.59.07@2x.png" alt="CleanShot 2024-03-18 at 21.59.07@2x" style="zoom:50%;" />

- 两个KGCGPT的方法都挺好的
  - text alignment 和 analogy demonstration是**相互支撑**的，让LLM更好的理解含义
  - *但对于LLM不太理解的关系，经过text alignment处理后的文本（关系描述）可能无法传达真实的语义*
- text alignment在WN18RR更好，因为**关系少**，demonstration例子样式多，增进了LLM对于关系的理解，生成更准确的描述
  - <img src="./assets/CleanShot 2024-03-18 at 22.07.21@2x.png" alt="CleanShot 2024-03-18 at 22.07.21@2x" style="zoom:50%;" />
  - 并且从图中可以看出WN18RR的**关系更简洁，语意更佳直接** => 对齐更加高质量、准确
- 比triple-based和text-based方法效果好
  - 说明**利用LLM的内部信息有效**
- 比只用LLM好
  - 在KGC任务上，结合KG到LLM好（结合KG内部的信息）
- 耗时也少，还不用微调

### 4.3 Ablation Study

<img src="./assets/CleanShot 2024-03-18 at 22.14.23@2x.png" alt="CleanShot 2024-03-18 at 22.14.23@2x" style="zoom:50%;" />

1. shuffle the top-m entities in $R_{retriever}$ before feeding into the LLM.
   1. Recently, Sun et al. (2023) also noted the significance of the **initial order in search re-ranking**.
2. randomize the demonstration orders from the analogy and supplement pools.
   1. 前面提出的**demonstration ordering**可以改善
3. retrieve random triples from the KG as demonstrations.
   1. shows usefulness of the construction of **demonstration pools**
4. exclude all demonstrations, while still providing the top-m candidates to constrain the ChatGPT output.
   1. demonstrating the **necessity of the proposed ICL strategy**
   2. Hit@3 without ICL is superior to Hit@3 with random demonstrations. 
      1. This may be attributed to the **vast number of triples in the KG**, rendering the **random** demonstrations to have **insignificant semantic relevance** to the query.
      2. 无关的triple还会有噪音，误导LLM
5. without the prompt engineering component, still uses the proposed demonstration pools and ordering
   1. the specially designed prompts can make use of the properties of the KGC task to boost performance.

### 4.4 Analysis on Long-Tail Entities

effectiveness of KICGPT and KICGPTtsa to handle long-tail entities

- we follow (Wang et al., 2022a) and group entities by their logarithm degrees in the knowledge graph. Entities with lower degrees (and hence more likely to be long-tail entities) are assigned to groups with lower indexes. A triple (h, r, t) is considered relevant to group d if h or t belongs to d.

<img src="./assets/CleanShot 2024-03-18 at 22.59.16@2x.png" alt="CleanShot 2024-03-18 at 22.59.16@2x" style="zoom:50%;" />

- Text-based methods demonstrate slightly better performance than triple-based methods on long-tail entries. However, this improvement is not significant since it only applies to a small portion of long-tail entities (specifically, groups 0, 1, 2). 
- Compared with these baselines, the proposed models achieve performance improvement on almost all groups and perform significantly better on long-tail entities, which confirms the benefits of combining the LLM with KG.

