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

==Algorithms==

<img src="./assets/CleanShot 2024-03-18 at 20.40.06@2x.png" alt="CleanShot 2024-03-18 at 20.40.06@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-18 at 20.40.49@2x.png" alt="CleanShot 2024-03-18 at 20.40.49@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-18 at 20.41.02@2x.png" alt="CleanShot 2024-03-18 at 20.41.02@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-18 at 20.41.15@2x.png" alt="CleanShot 2024-03-18 at 20.41.15@2x" style="zoom:50%;" />

### 3.1 Problem Setting

A link prediction model usually needs to score all plausible entities as missing entity and then rank all entities in descending order.

### 3.2 Overview

<img src="./assets/CleanShot 2024-03-18 at 20.44.40@2x.png" alt="CleanShot 2024-03-18 at 20.44.40@2x" style="zoom:50%;" />

