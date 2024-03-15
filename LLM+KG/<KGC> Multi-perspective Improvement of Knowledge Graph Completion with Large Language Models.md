# Multi-perspective Improvement of Knowledge Graph Completion with Large Language Models

> arXiv:2403.01972v1 [cs.CL] 04 Mar 2024
>
> 关于用大模型进行图谱补全的文章
>
> 这篇就略读了（甚至用的是arxiv的html）

核心的思路就是用LLM扩展一下信息，而补全的方法用的还是文中所说的"Description-based KGC"

- Description-based按照我的理解其实就是embedding了图谱的实体以及关系的语意，也就是既考虑了语意信息，也考虑了结构信息

<img src="./assets/CleanShot 2024-03-14 at 15.44.54@2x.png" alt="CleanShot 2024-03-14 at 15.44.54@2x" style="zoom:50%;" />

方法是==**MPIKGC**==，从三个角度使用LLM扩展信息：

- Entity：
- Relation：
- Structure：

Prompt要Clarity、Universality（普适）、Diversity

<img src="./assets/CleanShot 2024-03-14 at 15.48.00@2x.png" alt="CleanShot 2024-03-14 at 15.48.00@2x" style="zoom:50%;" />

## 3.  Methodology

### 3.1.  Problem Definition

- triplet classification：确定给定三元组的准确性（是否真实？）
- link prediction

### 3.2.  Multi-perspective Prompting 多角度prompt

- Clarity: 对于LLM来说，严格遵守我们的指示至关重要。 过于复杂的提示可能会导致指示上的误解，特别是对于小型LLM（参数少于100亿个）而言，会导致降低沟通效果
- Universality: 们设计的提示应与各种LLM兼容，并且这些LLM生成的文本在多个KGC模型上始终表现出改进，无论是链接预测还是三元组分类任务
- Diversity:实体、关系和结构

#### 3.2.1.  Description Expansion 实体

利用CoT的策略

==**MPIKGC-E**==：要求LLMs在回答之前提供全面的实体描述和理由，这将作为答案的合理性依据，并提高KGC模型的召回率

#### 3.2.2.  Relation Understanding 关系

知识图谱中存在异构关系对区分两个实体起着至关重要的作用，只依赖关系名字会有歧义

- ==**MPIKGC-R Global**==：从整个图谱的角度判断关系的意义（对于主题无关的关系就不考虑了，缩小关系范围）
  - 比如：*“produced by”* and *“director”*和电影行业相关，*“release region”* and *“place of birth”* 和国家相关
- ==**MPIKGC-R Local**==：从三元组的角度判断关系的意义，从而增强理解并提出可能的头/尾实体类型，同时预测缺失的事实
  - 比如：*“(head entity, release region, tail entity)”*->films, country
- ==**MPIKGC-R Reverse**==：用LLMs表示动词并转换为被动语态，从而增强理解能力，并实现更好的逆向预测。生成的文本将附加到关系名称，并根据每个KGC模型处理关系名称的工作流程进行处理。
  - 比如：*“produce”* -> *“produced by”*

#### 3.2.3.  Structure Extraction 结构

- KGC模型能够从训练三元组中学习结构模式，并推广到测试三元组中缺失的环节
  - 比如：一个和发行人或者导演有关系的人，大概率会与电影实体有关
- 然而，从图结构中学习模式**受到稀疏链接的限制，特别是对于长尾实体**
-  ==**MPIKGC-S**==：利用LLMs生成额外的结构信息增强KG
  - 将LLMs的生成文本转换为graph-based的数据，我们利用LLMs的总结能力从描述中抽取关键词，然后**根据匹配关键词数量计算实体之间的匹配分数$s$**：
    - $s=len(m)/min(len(k_h),len(k_t)),$
    - $m=interdection(k_h,k_t)$
      - $k_h$和$k_t$代表头尾实体的关键词，$m$是$k_h$和$k_t$的交集
  - 在对匹配分数进行排序后，我们选择了前k对，并以*(head, Same As, tail)*的形式创建新的三元组，然后将其附加到训练集中。
  - 除了这些基于相似性的三元组之外，我们还考虑为每个实体添加一个带有关系“SameAs”的自环三元组：*(head, Same As, head)*，以增强KGC模型对于SameAs关系的学习 **==Self-loop==**

## 4.  Experiments

### 4.1.  Experimental Setup

#### Datasets.

<img src="./assets/CleanShot 2024-03-14 at 22.17.40@2x.png" alt="CleanShot 2024-03-14 at 22.17.40@2x" style="zoom:50%;" />

#### Metrics.

- Link prediction：Mean Rank (MR)【越低越好】, Mean Reciprocal Rank (MRR), and Hits@n (H@n, n={1,3,10}) 
- triplet classification：Accuracy

#### Baselines.

四个方法，比较了原始的KG和改进后的KG

- KG-BERT Yao et al. ([2019](https://arxiv.org/html/2403.01972v1#bib.bib35))
- SimKGC Wang et al. ([2022a](https://arxiv.org/html/2403.01972v1#bib.bib26))
- LMKE Wang et al. ([2022b](https://arxiv.org/html/2403.01972v1#bib.bib28))
- CSProm-KG Chen et al. ([2023](https://arxiv.org/html/2403.01972v1#bib.bib5))

由于KGC要求对所有候选实体进行排名，我们优先考虑了使用1对n评分方法的基准线。

还比较了传统的方法：

- TransE Bordes et al. ([2013](https://arxiv.org/html/2403.01972v1#bib.bib3))
- DistMult Yang et al. ([2014](https://arxiv.org/html/2403.01972v1#bib.bib34))
- RotatE Sun et al. ([2019](https://arxiv.org/html/2403.01972v1#bib.bib24))
- ConvE Dettmers et al. ([2018](https://arxiv.org/html/2403.01972v1#bib.bib6))
- ConvKB Nguyen et al. ([2018](https://arxiv.org/html/2403.01972v1#bib.bib16))
- ATTH Chami et al. ([2020](https://arxiv.org/html/2403.01972v1#bib.bib4))

#### Backbones.

- Llama-2 (Llama-2-7b-chat) 
- ChatGLM2-6B
- ChatGPT (gpt-3.5-turbo-0613)
- GPT4 (gpt-4-0613)
- 设置：
  - temperature：0.2
  - maximum length：256
  - single-precision floating-point (FP32) for inference.

我们使用BERT (bert-based-uncased) Yao et al. ([2019](https://arxiv.org/html/2403.01972v1#bib.bib35))来编码生成文本，用于所有基于描述的KGC模型，超参数设置与相应模型一致

#### Settings.

 “bert-based-uncased” version Yao et al. ([2019](https://arxiv.org/html/2403.01972v1#bib.bib35)) as the backbone for all KGC models

确保不同的扩充实验具有相同的最大标记长度和数据处理流程

### 4.2.  Main Results

<img src="./assets/CleanShot 2024-03-15 at 10.06.11@2x.png" alt="CleanShot 2024-03-15 at 10.06.11@2x" style="zoom:50%;" />

1. FB15k237上基于**结构**的方法表现的好一些，因为都是普通的world facts
   1. 在MPIKGC-S方法的影响下效果好，因为15K entities and 237 kinds of relations
2. WN18RR上基于**描述**的方法表现好一些，因为具有丰富的语言知识，适合PLM
   1. 40K entities with **only 11 relations**.将额外的关系添加到WN18RR可能会过度**改变知识图谱的稀疏性和三元组分布**，导致性能不佳。
3. CSProm-KG 在 FB15k237表现的好，在WN18RR表现的不好
   1. MPIKGC-S 提升了对于结构的学习，在FB15k237达到了最佳
4. LMKE SimKGC 这两种方法都以文本为中心，并且具有学习丰富信息的能力
   1. MPIKGC-R 在WN18RR提升1%～2%
   2. MPIKGC-E
   3. MPIKGC-S在WN18RR没有带来提升，关系类型较少，这可能会在添加新关系时误导模型，但是在FB15k237有效果

### 4.3. Triplet Classification

<img src="./assets/CleanShot 2024-03-15 at 10.22.32@2x.png" alt="CleanShot 2024-03-15 at 10.22.32@2x" style="zoom:50%;" />

### 4.4. Parameter Analysis of Structure Extraction

<img src="./assets/CleanShot 2024-03-15 at 10.25.14@2x.png" alt="CleanShot 2024-03-15 at 10.25.14@2x" style="zoom:50%;" />

- 增加 k 的值意味着向训练集中添加更多的三元组（建立的那个*SameAS*的关系）
- 结构上的增强确实提高了KGC在FB15k237数据集上的性能
- 当 k 达到 4 或 5 时，性能开始下降。这一趋势表明训练集包含过多的无关三元组，可能会对其他数据的学习产生负面影响

### 4.5. Ablation of Multi-perspective Prompts

<img src="./assets/CleanShot 2024-03-15 at 10.24.55@2x.png" alt="CleanShot 2024-03-15 at 10.24.55@2x" style="zoom:50%;" />

- 结果表明，增强后从实体、关系和结构的角度来看，知识图谱模型在所有四个指标上均取得了近0.5%的改进
- MPIKGC-E＆R将生成的实体描述与关系的描述文本相结合，从而略微提高了使用任一单独元素时的效果
- 各种增强方法是兼容的，并且可以集成以提升整体性能

### 4.6. Ablation of Relation Understanding

<img src="./assets/CleanShot 2024-03-15 at 10.34.46@2x.png" alt="CleanShot 2024-03-15 at 10.34.46@2x" style="zoom:50%;" />

- 全局和局部prompt有互补的效果
- 其他组合策略表现不佳->包含过多的关系描述可能会增加学习关系含义的难度

### 4.7. Comparison of LLMs

<img src="./assets/CleanShot 2024-03-15 at 10.36.08@2x.png" alt="CleanShot 2024-03-15 at 10.36.08@2x" style="zoom:50%;" />

- 与Llama-2相比，ChatGLM2在MPIKGC-E和MPIKGC-S方面取得了更好的结果，表明ChatGLM2在推理和总结能力上具有优势。
- Llama-2和ChatGPT在理解关系方面优于ChatGLM2

## 5. Conclusion

在未来，我们计划探索将“SameAs”关系细化为更精细的类别的可能性，而不会添加太多三元组。另一方面，通过LLMs生成知识图数据可能会遇到幻觉、有毒和偏见等问题，我们计划开发限制提示或微调LLMs以增强文本生成的可控性和可解释性。









