# Enhancing Temporal Knowledge Graph Forecasting with Large Language Models via Chain-of-History Reasoning

## Abstract

现在的方法：大多缺乏语义理解

现在的LLMs-based的方法也有缺点：

1. 只关注第一阶历史以进行预测，而忽略高阶历史信息，导致**给LLMs提供的信息有限**
2. LLMs在面对大量的历史信息时，会面临最优**推理性能**的挑战
3.  对于TKG预测，**单独使用LLM的时间推理能力有限**

Chain-of-History (CoH) reasoning：

- 组织历史信息，可以让LLMs在TKG外推的任务重利用高阶的信息
- 设计 CoH 作为一个即插即用模块，以提高基于图的模型在 TKG 预测方面的性能

## 1 Introduction

GNN：捕捉TKGs的结构依赖，对于语义的建模不足

LLMs-based：

- **Article：**Raghav Jain, Daivik Sojitra, Arkadeep Acharya, Sriparna Saha, Adam Jatowt, and Sandipan Dandapat. 2023. Do language models have a common sense regarding time? revisiting temporal commonsense reasoning in the era of large language models. In Pro- ceedings of the 2023 Conference on Empirical Meth- ods in Natural Language Processing, pages 6750– 6774.
- **Article：**Chenhan Yuan, Qianqian Xie, Jimin Huang, and Sophia Ananiadou. 2023. Back to the future: Towards explainable temporal reasoning with large language models. arXiv preprint arXiv:2310.01074.
- **Article：**TKG推理，以文本形式为LLMs提供历史。Dong-Ho Lee, Kian Ahrabian, Woojeong Jin, Fred Morstatter, and Jay Pujara. 2023. Temporal knowledge graph forecasting without knowledge using in- context learning. arXiv preprint arXiv:2305.10613.

**仍有一些重要的问题：**

1. 现有的LLMs-based的TKGs外推的方法**只关注了一阶历史**，如图：

   <img src="./assets/CleanShot 2024-03-09 at 18.53.06@2x.png" alt="CleanShot 2024-03-09 at 18.53.06@2x" style="zoom:50%;" />

2. LLM不能在利用大量历史数据的情况下**保持良好的性能**（长文本处理性能）：如图2所示，LLMs的性能并不一定随着历史长度的增加而改善或保持稳定，相反，在历史长度超过某个阈值后，无论模型大小如何，其性能都会急剧下降。

   - 过于复杂的历史信息会影响模型的性能
     - **Article：**Xiaoming Shi, Siqiao Xue, Kangrui Wang, Fan Zhou, James Y Zhang, Jun Zhou, Chenhao Tan, and Hongyuan Mei. 2023. Language models can improve event prediction by few-shot abductive reason- ing. arXiv preprint arXiv:2305.16646.

   <img src="./assets/CleanShot 2024-03-09 at 19.02.29@2x.png" alt="CleanShot 2024-03-09 at 19.02.29@2x" style="zoom:50%;" />

   - **探索一个有效的方法使LLMs有效利用高阶信息**

3. 仅依赖LLMs的推理能力在TKG预测方面仍然存在局限性

   - LLMs对于基于图的模型中的结构化数据的信息的处理能力不足
   - 但是LLMs能够为TKG的推理提供语义理解上的补足

本文提出了==**Chainof-History (CoH)**== reasoning method for TKG prediction

- 一步步（step-by-steps）为LLMs提供高阶历史：LLMs逐步探索重要的高阶历史链，并仅基于在最后一步推断出的历史链来推理查询的答案

- 一个两步的COH的推理步骤：

  - 在第一步中，LLMs 只提供了一阶历史，并被要求推断最重要的历史。在第二步中，LLMs 根据推断出的一阶历史提供了二阶历史链，并被要求推断给定查询的可能答案。然后，由LLMs 和基于图形的模型推断出来的答案会被自适应地融合以做出最终预测。

    <img src="./assets/CleanShot 2024-03-09 at 19.19.26@2x.png" alt="CleanShot 2024-03-09 at 19.19.26@2x" style="zoom:50%;" />

  - 通过这种方式，LLMs 只需要在每一步处理有限数量的历史记录，防止复杂信息的过度涌入，同时有效地利用更全面的高阶信息集合

  - 将CoH设计为TKG推理的即插即用模块，如图3所示，我们将LLMs和基于图的TKG模型获得的预测结果进行融合，以使最终预测更全面。

**summarization**：

- 使用LLMs，考虑高阶TKG的高阶历史，提出CoH
- 利用LLMs增强基于图的TKG模型性能，利用LLMs的语义理解能力增强基于图的模型的性能
- 在三个数据集上进行了实验

## 2 Problem Formulation 问题阐述

**TKG预测**

**TKG中的高阶历史链**（high-order history chains in TKG：<img src="./assets/CleanShot 2024-03-10 at 11.26.25@2x.png" alt="CleanShot 2024-03-10 at 11.26.25@2x" style="zoom:33%;" />

> - 按照我的理解其实就是：
>   - ----t3----t2----t1----t----
>   - 如果问t时刻实体1的什么问题，就从t时刻往前追溯
>   - 比如：
>     - 实体1 在t1时刻与实体2的那个四元组作为 实体1与实体2的一个一阶的历史
>     - 实体1 在t2时刻与实体3的那个四元组作为 实体1与实体3的一个一阶的历史
>     - 实体1 在t3时刻又和实体2和实体3都有过一个四元组，那么t3的这两个四元组就可以作为之前两个历史的高阶历史，组成一个**history chain**

## 3 Chain-of-History Reasoning over Temporal Knowledge Graph

- 3.1 四元组->text 给LLMs
- 3.2 如何合理地为LLMs提供历史，如何引导LLMs进行推理
- 3.3 如何把LLMs的输出转换为分数并与基于图的TKG模型的结果融合在一

### 3.1 History Processing

引入介词将四元组转化为句子

- 把具体的==日期==转换成==第x天==，因为**LLMs==容易直接用其先验知识进行预测==**

  - “(Germany, Sign agreement, Denmark, 2023-06-02)”->“(Germany Sign agreement with Denmark on the 153rd day)”.

  - > 这还是挺抽象的，但是LLMs好像确实无法利用先验知识了....

### 3.2 Reasoning Steps

<img src="./assets/CleanShot 2024-03-10 at 12.48.49@2x.png" alt="CleanShot 2024-03-10 at 12.48.49@2x" style="zoom:50%;" />

#### Step 1 to Step k-1 Reasoning.

- **step1** 只为LLMs提供关于q的一阶的历史，并被指示来推理对回答q最有帮助的n个一阶历史

  - > 这里好像把未来的预测都限制在了这n个一阶关系里了？

- **step2 ~ step k-1** 为LLMs提供i阶历史，然后推理n个最相关的历史链

  - 在这一系列步骤中，第i-1步的LLMs的输出是推断出来的(i-1)阶历史链，然后每个历史链都会与相应的i阶历史结合以形成i阶历史链

#### Step k Reasoning.

- 给LLMsk阶历史链，然后让其推理q的可能得答案，给出的结果具有排序**（numerical index）**

### 3.3 Results Processing and Fusion 结果处理与融合

- 在基于图的TKG模型中，实体和关系用id来表示，因此会丢失语义信息，而只关注结构信息
- 为了既考虑结构信息，又考虑语义信息——->融合LLMs和graph-based model的结果

处理过程：

1. 对于q，获得LLMs的结果的预测得分$A^q_{LLM}$

   1. 我们将每个答案 $e_i \in A^q_{LLM}$ 的序数转换为相应的分数，使用指数衰减函数为：

      <img src="./assets/CleanShot 2024-03-10 at 12.59.24@2x.png" alt="CleanShot 2024-03-10 at 12.59.24@2x" style="zoom:50%;" />

      1. $S^{e_i}_{LLM}$代表LLMs实体e对于q的结果的得分
      2. $\alpha$是一个超参数，用于控制具有不同序数的答案之间得分差异

   2. LLMs给出的答案不可能都包含在图模型的输出里，因此对于这一部分实体，$S^{e_i}_{LLM}=0$

2. 融合LLMs和graph-based model 的输出：

   <img src="./assets/CleanShot 2024-03-10 at 13.07.45@2x.png" alt="CleanShot 2024-03-10 at 13.07.45@2x" style="zoom:50%;" />

   1. $S^{e_i}_{Graph}$是基于图模型的输出
   2. $\omega$是超参数，平衡LLMs和基于图的模型的输出的权重

3. 最后，基于综合得分的候选名单被用来预测 q。

## 4 Experiments

### 4.1 Experimental Settings

#### 4.1.1 Evaluation

**MRR and Hits@{1, 3, 10}**

将TKG预测中LLM的评估机制与基于图形的模型中使用的评估机制完全一致，以确保更公平的比较

将关系反转的设置：reversing $(s, r, o, t)$ into $(o, r^{−1}, s, t)$

并且也用了reversed test sets来评估

#### 4.1.2 CoH Implementation Details

开源模型Mixtral-8x7B

- step1:100个一阶历史，设置n=30，让LLMs给出30个一阶的结果
- Step2：不限制LLMs的输出结果

### 4.2 Performance Comparison 性能比较

- 只用CoH
- 将LLMs插到3个SOTA TKG外推的模型，来看CoH的提升

<img src="./assets/CleanShot 2024-03-10 at 13.50.01@2x.png" alt="CleanShot 2024-03-10 at 13.50.01@2x" style="zoom:50%;" />

> 这提升也太少了。。。。。。。。。。。。。

- 在ICEWS18的提升最明显
  - 包含更多复杂的历史关系
- 只用LLMs的效果不行啊
  - 虽然不行，但是还是可以把LLMs的那部分作为一个即插即用的模块来增强graph-based model
- 在加上LLMs的方法的协助下，可以提升graph-based model的方法的结果
  - LLMs 的强大语义理解能力可能能够在一定程度上弥补基于图形模型的语义信息建模中固有的局限性

### 4.3 Ablation Study

<img src="./assets/CleanShot 2024-03-10 at 14.00.43@2x.png" alt="CleanShot 2024-03-10 at 14.00.43@2x" style="zoom:50%;" />

- **高阶历史信息**
  - 对于第二阶历史信息的使用可以比只用一阶的好
- **逐步的推理机制**
  - LR——通过两步CoH推理，LLMs对重要的一阶历史进行推理的步骤。
  - CoH w/o LR：通过将由LLMS推断的n个一阶历史记录 替换为 在最新时间戳中 n 个一阶历史记录
  - 通过这种方式，可以找出LLMs是否能够在逐步推理机制中推断出有意义的历史信息。
  - 结果：setp-by-step的推理过程是有帮助的
- **得分排名程序**
  - 在最后一步让LLMs给结果打分排名
  - 为了验证每个答案的输出索引是否与其正确性有关，我们对答案的索引顺序进行了混洗，这在表3中表示为“CoH w/o IS”.
  - 结果表明LLMs输出的指数对于TKG预测中的评分排名是有帮助的

### 4.4 Case Study

<img src="./assets/CleanShot 2024-03-10 at 14.09.31@2x.png" alt="CleanShot 2024-03-10 at 14.09.31@2x" style="zoom:50%;" />

- 从两个案例的推理过程中可以看出，LLMS具有推理与给定查询相关的重要历史的能力。
- LLMs的语义理解在一些特定的场合比较有用

### 4.5 Analysis of Data Leakage 

排除掉了LLMs的已知的事实，防止LLMs利用已知事实进行推理

### 4.6 Analysis on the effect of Prior Knowledge within LLMs

LLMs的先验知识的影响

<img src="./assets/CleanShot 2024-03-10 at 15.10.07@2x.png" alt="CleanShot 2024-03-10 at 15.10.07@2x" style="zoom:50%;" />

- Anon-CoH，用ID代替实体名称，实验效果不好，表明先验知识对LLMs的推理有帮助

- > 这也没有语义理解了啊，感觉很迷惑

### 4.7 Sensitivity Analysis 敏感度分析

- $\alpha  \& \omega $

<img src="./assets/CleanShot 2024-03-10 at 15.14.38@2x.png" alt="CleanShot 2024-03-10 at 15.14.38@2x" style="zoom:50%;" />

- $\alpha $值在非常小的范围内的变化对模型性能的影响微乎其微。
- $\omega $COH的结果对最终分数的贡献略大一些。我们分析了导致上述观察的潜在原因可能与基于图的模型的分数分布有关。

## 5 Related Work

**TKG外推 with supervised medels**：

- 经典方法：通过时间点过程（temporal point process, TTP）在TKGs中建模时间信息：
  - GHNN (Han et al., 2020) 
  - Know-Evolve (Trivedi et al., 2017)
- 复制生成机制copy-generation mechanism，探索重复历史中的模式：
  - CyGNet (Zhu et al., 2021)
- GNN， 捕获TKG的结构信息：
  - W. Jin, M. Qu, X. Jin, and X. Ren. 2020. Recurrent event network: Autoregressive structure infer- enceover temporal knowledge graphs. In EMNLP, pages 6669–6683.
  - Zixuan Li, Xiaolong Jin, Wei Li, Saiping Guan, Jiafeng Guo, Huawei Shen, Yuanzhuo Wang, and Xueqi Cheng. 2021b. Temporal knowledge graph reasoning based on evolutional representation learning. In SIGIR, pages 408–417.
  - Yujia Li, Shiliang Sun, and Jing Zhao. 2022. Tirgn: Time-guided recurrent graph network with localglobal historical patterns for temporal knowledge graph reasoning. In Proceedings of the Thirty-First International Joint Conference on Artificial Intelli- gence, IJCAI 2022, Vienna, Austria, 23-29 July 2022, pages 2152–2158.
  - Mengqi Zhang, Yuwei Xia, Qiang Liu, Shu Wu, and Liang Wang. 2023. Learning latent relations for tem- poral knowledge graph reasoning. In Proceedings of the 61st Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), pages 12617–12631.
  - Ke Liang, Lingyuan Meng, Meng Liu, Yue Liu, Wenxuan Tu, Siwei Wang, Sihang Zhou, and Xinwang Liu. 2023. Learn from relational correlations and periodic events for temporal knowledge graph reasoning. In Proceedings of the 46th International ACM SIGIR Conference on Research and Development in Infor- mation Retrieval, pages 1559–1568.
- 使用神经常微分方程来构建连续的时间信息：
  - TANGO (Han et al., 2021b)  Zhen Han, Zifeng Ding, Yunpu Ma, Yujia Gu, and Volker Tresp. 2021b. Learning neural ordinary equations for forecasting future links on temporal knowl- edge graphs. In EMNLP, pages 8352–8364.
- 对比学习以识别重要的非历史实体：
  - CENET (Xu et al., 2023b)  Yi Xu, Junjie Ou, Hui Xu, and Luoyi Fu. 2023b. Temporal knowledge graph reasoning with historical con- trastive learning. In AAAI.
- 元学习学习事件演化模式
  - MetaTKG (Xia et al., 2022)  Yuwei Xia, Mengqi Zhang, Qiang Liu, Shu Wu, and Xiao-Yu Zhang. 2022. Metatkg: Learning evolutionary meta-knowledge for temporal knowledge graph reasoning. In EMNLP, pages 7230–7240.
- 在TCK中搜索子图提出一个可解释的模型
  - xERTE (Han et al., 2021a)   Zhen Han, Peng Chen, Yunpu Ma, and Volker Tresp. 2021a. Explainable subgraph reasoning for forecast- ing on temporal knowledge graphs. In ICLR.
- 使用强化学习搜索重要路径
  - Haohai Sun, Jialun Zhong, Yunpu Ma, Zhen Han, and Kun He. 2021. TimeTraveler: Reinforcement learning for temporal knowledge graph forecasting. In EMNLP, pages 8306–8319.
  - Zixuan Li, Xiaolong Jin, Saiping Guan, Wei Li, Jiafeng Guo, Yuanzhuo Wang, and Xueqi Cheng. 2021a. Search from history and reason for future: Two-stage reasoning on temporal knowledge graphs. In Pro- ceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers), pages 4732– 4743.
- 通过时间逻辑规则提取路径以进行TKG预测
  - Tlogic (Liu et al., 2022)   Yushan Liu, Yunpu Ma, Marcel Hildebrandt, Mitchell Joblin, and Volker Tresp. 2022. Tlogic: Temporal logical rules for explainable link forecasting on temporal knowledge graphs. In Proceedings of the AAAI conference on artificial intelligence, volume 36, pages 4120–4127.

**TKG+LLMs**：

- 尝试利用预训练语言模型（PLMs）进行TKG推理，主要将历史记录以文本形式输入到PLMs中，以获得上下文化的知识嵌入
  - Zhen Han, Ruotong Liao, Beiyan Liu, Yao Zhang, Zifeng Ding, Jindong Gu, Heinz Koeppl, Hinrich Schuetze, and Volker Tresp. 2022. Enhanced temporal knowledge embeddings with contextualized language representations.
  - Yifu Gao, Yongquan He, Zhigang Kan, Yi Han, Linbo Qiao, and Dongsheng Li. 2023. Learning joint structural and temporal contextualized knowledge embeddings for temporal knowledge graph completion. In Findings of the Association for Computational Linguistics: ACL 2023, pages 417–430.
  - Wenjie Xu, Ben Liu, Miao Peng, Xu Jia, and Min Peng. 2023a. Pre-trained language model with prompts for temporal knowledge graph completion. arXiv preprint arXiv:2305.07912.
- LLMs在结构数据和时序数据上的推理能力的探索
  - Jinhao Jiang, Kun Zhou, Zican Dong, Keming Ye, Wayne Xin Zhao, and Ji-Rong Wen. 2023. Structgpt: A general framework for large language model to reason over structured data. arXiv e-prints, pages arXiv–2305.
  - Raghav Jain, Daivik Sojitra, Arkadeep Acharya, Sriparna Saha, Adam Jatowt, and Sandipan Dandapat. 2023. Do language models have a common sense regarding time? revisiting temporal commonsense reasoning in the era of large language models. In Pro- ceedings of the 2023 Conference on Empirical Meth- ods in Natural Language Processing, pages 6750– 6774.
  - Chenhan Yuan, Qianqian Xie, Jimin Huang, and Sophia Ananiadou. 2023. Back to the future: Towards explainable temporal reasoning with large language models. arXiv preprint arXiv:2310.01074.
  - Mohamed Aghzal, Erion Plaku, and Ziyu Yao. 2023. Can large language models be good path planners? a benchmark and investigation on spatial-temporal reasoning. arXiv preprint arXiv:2310.03249.
  - Yuqing Wang and Yun Zhao. 2023. Tram: Benchmarking temporal reasoning for large language models. arXiv preprint arXiv:2310.00835.
  - Qingyu Tan, Hwee Tou Ng, and Lidong Bing. 2023. Towards benchmarking and improving the temporal reasoning capability of large language models. arXiv preprint arXiv:2306.08952.
- 在TKG领域，
  - Ding等人将文本形式的关系输入LLMs中，生成相应的描述，然后作为零样本关系的语义信息补充引入基于嵌入的模型
    - Zifeng Ding, Heling Cai, Jingpei Wu, Yunpu Ma, Ruotong Liao, Bo Xiong, and Volker Tresp. 2023. Zero-shot relational learning on temporal knowledge graphs with large language models. arXiv preprint arXiv:2311.10112.
  - 李等人首次尝试使用LLMs进行TKG预测，他们将TKG预测转化为上下文学习（ICL）问题，向LLMs提供查询的文本形式的一阶历史以预测可能的答案（Lee等人，2023年）
    - Dong-Ho Lee, Kian Ahrabian, Woojeong Jin, Fred Morstatter, and Jay Pujara. 2023. Temporal knowledge graph forecasting without knowledge using in- context learning. arXiv preprint arXiv:2305.10613.

## 6 Conclusion

CoH 结合LLMs在TKG外推的任务上，利用LLMs的语义理解能力

## 7 Limitations

- 由于CoH推理是分步骤进行的，需要多次调用LLMS，从而增加了推理过程的复杂性
- 由于整个过程不涉及任何训练，融合权重只能由超参数w控制，因此无法实现**自适应融合**



