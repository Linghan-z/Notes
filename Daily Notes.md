----

## 每天的记录

----

### 2024.02.29

论文：T-RAG: LESSONS FROM THE LLM TRENCHES

> T-RAG方法基于将RAG架构与开源的经过微调的LLM和实体树向量数据库相结合。
>
> 实验是基于一个组织的问答，所示用实体树表达组织结构，但是确实也可以参考这个方法在别的领域，即：
>
> - 同时对文档和KG进行检索，合并两个的检索结果
> - 对LLMs进行微调，以适应当前任务
>
> **下一步思考：**
>
> 1. 用在领域QA更好，哪个领域合适（有合适的数据生成KG）
> 2. 考虑是否可以像本文一样延伸到复杂QA
> 3. KG构建方法
>    1. 目前的简单构思是：基于领域，构建本体网络，在根据本体网络来用LLMs辅助生成KG
> 4. 实体对齐方法，参考老饶发的那篇
> 5. 合适的微调方法

<img src="./RAG Articles/assets/CleanShot 2024-02-28 at 12.43.49@2x.png" alt="CleanShot 2024-02-28 at 12.43.49@2x" style="zoom:50%;" />

---

### 2024.03.02

论文：KnowledGPT: Enhancing Large Language Models with Retrieval and Storage Access on Knowledge Bases

> LLMs+KG 实现KG增强LLMS（至少方向对了）
>
> 文章偏向于QA领域，尤其是还涉及了一个PKG，私人的记录历史问题的图谱，但是可以参考他同时检索两个知识库并且融合检索结果的方法（类比前天看的T-RAG）

- 原理：

  1. 生成搜索代码
     1. PoT（program of thought）的思路，定义了几个方法用于生成代码
  2. 在KG中搜索
  3. 问答

- 涉及到的细节有：

  - ==实体、关系抽取与对齐==

    - > 处理同义实体及关系
      >
      > （有空还是要在这方面参考一下老饶之前发的那个文章）

  - 检索获取实体的详细信息

  - 检索相关实体，对关系和问题计算相似度来匹配

  - 找到目标实体

- 除此之外，还涉及了一个私人的KG，用于记录历史问题

---

### 2024.03.03

> 开题开毁了。。。还是多看文章吧

---

### 2024.03.03

交了开题、看了电影、还让写本子..

---

### 2024.03.05

论文：RAG VS FINE-TUNING: PIPELINES, TRADEOFFS, AND A CASE STUDY ON AGRICULTURE

> 微软的一篇文章，看了两天
>
> 涉及到农业领域的RAG+Finetune
>
> 做了大量的实验（也没好好看）

值得记录的一些点：

- 对于PDF转文本的处理方面（转为TEI格式）

- 问题生成的方法

- 答案生成的技术（RAG, FAISS retrieval tool）+ GPT-4 + custom Prompt

  - > 问题和答案分着生成效果更好

- 微调的技术（现在都看不懂）

- 提出的很完整的评估标准（包括对于LLMs生成的问题的评估）

- 很完整的实验（虽然没仔细看）

> **加油ヾ(◍°∇°◍)ﾉﾞ**

---

2024.03.07

论文：Survey on Factuality in Large Language Models: Knowledge, Retrieval and Domain-Specificity

>  西湖大学的关于LLMs事实性的综述
>
> 挺庞大的60多页，粗略看看吧，争取今天看完，大致了解一下

值得记录的一些东西：

- 2.2 hallucination 和 factuality issue 不同
- 3.1.1 有很多评价指标的总结，后续需要的话再看着搜索吧

- 看麻了。。。。。
  - 前面是介绍的事实性问题和一些指标
  - 后面是一些方法
  
    - 探索LLMs幻觉的事实性错误的研究
    - 增强LLMs的研究
  - > 心乱如麻 这样吧就，回头有需要再看笔记吧

---

2024.03.08

> 改了一天的本子
>
> 学了一下EndNote
>
> 我发现ConnectedPaper还挺好用的

----

2024.03.09

> 又又又又又又又又改了一天的本子，感觉老饶的思路真的清晰..

----

2024.03.10

Article：Enhancing Temporal Knowledge Graph Forecasting with Large Language Models via Chain-of-History Reasoning

> 利用LLMs的语义理解能力，设计了CoH，逐步探索TKG中的高阶历史信息，给LLMs用于TKG的外推
>
> - ==利用LLMs的方法只能作为Graph-based model的一个补充部分，因为效果差的挺多，可见还是GNN的分析结构的方法效果好一些==
>
> 后面的实验的分析比较乱，感觉挺一般的
>
> 问题：
>
> 1. 在step1好像把未来的预测都限制在了这n个一阶关系里了，不知道会不会有问题
> 1. 实验效果性能的提升很小
> 1. 消融实验把名字给消了，说是为测试先验知识，但是没有了语义理解这还一样吗？
>
> Tips：
>
> 1. 为了防止LLMs利用先验知识，把日期改成了第xxx天
>
> 思考：
>
> - 可以看到LLMs在TKG外推的领域还是差的不少，以后可以研究一下