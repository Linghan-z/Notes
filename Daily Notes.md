## Memorandum

<img src="./assets/CleanShot 2024-03-22 at 22.06.43@2x.png" alt="CleanShot 2024-03-22 at 22.06.43@2x" style="zoom:50%;" />

1. [T-RAG](#2024.02.29):实体图（树），增强领域QA的实体对齐（比较偏领域）
2. [KnowledGPT](#2024.03.02):用GPT-4生成搜索的代码，搜索知识作为上下文增强LLM问答
3. [RAG VS FINE-TUNING](#2024.03.05):<微软>GPT-4生成用于微调的问题和答案（分步生成更好）；针对领域进行数据集和微调指令构建、微调、RAG，很完整，还包括了GPT-4生成的问题的评估标准，可以参考
4. [Survey on Factuality in Large Language Models](#2024.03.07):模型的事实性
5. [Chain-of-History](#2024.03.10):逐步探索TKG中的高阶历史信息，给LLMs用于TKG的外推
6. [Beyond Isolation](#2024.03.11):multi-agent进行图谱的构建（三个agent，分别ner、re、ee）按论次进行
7. [ChatIE](#2024.03.11):任务分解进行IE（NER、RE、EE）
8. [Evidence-Focused Fact Summarization](#2024.03.12):感觉这个方法有点问题，但是思路可取，就是从helpfulness和faithfulness两个角度出发，优化summarizer，对于普通的或者是大的上下文还是可以的吧，KG的结构化信息好像有点别扭
9. [Knowledge Representation Learning](#2024.03.13):使用KRL的方法来选择候选；用LLM来进行推理判断（还有LLM的知识增强）；这个用**代码**的这个感觉效果真的不错呀
10. [MPIKGC](#2024.03.14_2024.03.15):从实体信息、关系、结构三个角度使用LLMs扩充信息，并还用KGC模型完成KGC的任务
11. [KnowPAT](#2024.03.14_2024.03.15):KG+LLM 微调——偏好对齐+领域QA任务（偏好分成style+knowledge）
12. [Contextualization Distillation](#2024.03.16):蒸馏，用LLM生成上下文描述，增强基于PLM的KGC模型
13. [KG-LLM](#2024.03.17):multi-hop 链接预测，只用了CoT和ICL，prompt用的是实体和关系的id，没有用语意信息，鉴定为史
14. [KoPA](#2024.03.18):只有KGC的triple classification，没有link prediction。先encode结构信息，然后通过adapter把涉及到的三元组的embedding映射到virtual token中，通过预训练，让LLM学习到利用这个virtual token的模式
15. [KICGPT](#2024.03.18):利用传统的embedding-based的方法（文中分的更清楚，triple-based）选出candidate，然后通过定义方法设置demonstration和prompt，让LLM对传统方法的输出进行reranking，得到最终的结果
16. [GraphToken](#2024.03.20):learns an encoding function that generates fine-tuned soft-token prompts.使用encoder（GNN）来将KG的编码，通过对于GraphToken的参数进行训练，把KG的信息映射到latent prompt space，再加上初始prompt的embedding的空间中，让LLM进行decode
17. [GraphQA](#2024.03.24):LLMs对于图的推理，将图结构编码成text，增强LLM的推理
18. [GraphAdapter](#2024.04.09)：训练一个Graph Adapter，融合PLM encode 的语意信息和GNNencode的结构信息
19. [Advancing Graph Representation Learning](#2024.04.12):关于graph representation learning for LLMs的短综述
20. [Exploring the Potential of Large Language Models (LLMs) in Learning on Graphs](#2024.04.15):LLM如何学习图谱的信息，结合GNN？
21. [Graph Language Models](#2024.04.16) 提出graph language model，利用LM的初始化参数，调整了位置编码方式以及self-attention
22. [MoE](#2024.04.17)
23. [Mamba](#2024.04.18)
24. [Graph Chain-of-Thought](#2024.04.19):三个阶段利用LLM在图上进行推理：LLM reasoning，LLM-graph interaction，Graph execution
25. [ResearchAgent](#2024.04.20):利用两个Agent：Research Agent 和Reviewing Agent来做文章idea生成，结合了图谱的检索
26. [LLM-GNN](#2024.04.21)：label-free node classification、使用llm annotate
27. [GenTKGQA](#2024.04.22): Subgraph Retrieval: utilize LLM’s intrinsic knowledge；Answer Generation: virtual knowledge indicators: fuse gnn+textual representataion
28. [KGLLMs](#2024.04.22):KG和PLM结合的综述，从pretraining，during training 和 posttraining三个角度出发分析



----

## 每天的记录

----

### 2024.02.29{#2024.02.29}

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

### 2024.03.02{#2024.03.02}

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

### 2024.03.05{#2024.03.05}

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

### 2024.03.07{#2024.03.07}

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

### 2024.03.08

> 改了一天的本子
>
> 学了一下EndNote
>
> 我发现ConnectedPaper还挺好用的

----

### 2024.03.09

> 又又又又又又又又改了一天的本子，感觉老饶的思路真的清晰..

----

### 2024.03.10{#2024.03.10}

**Article：**Enhancing Temporal Knowledge Graph Forecasting with Large Language Models via Chain-of-History Reasoning

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

----

### 2024.03.11{#2024.03.11}

**Article:** Beyond Isolation: Multi-Agent Synergy for Improving Knowledge Graph Construction

> 这sb文章用一堆华丽辞藻，真的难读
>
> - Multi-agent方法，进行KG construction
> - 三个agent互相支撑
>   - NER
>   - RE
>   - EE
> - 按轮次来进行

一些地方总结一下就是：

1. 这种multi-agent并且按照轮次互相补充的方法涉及团队协作，肯定要比使用LLMs进行仅仅一轮的生成的效果要好

1. **去中心化**而不至于太依赖某一个Agent的发挥

1. 在Agent交流的时候，通过优化（简化）输入，可以有更好的效果

   1. > 所以给LLMs的一些信息还是要尽量的言简意赅，过多描述反而不好

1. 提供一定程度的背景知识，效果会更好

1. 这种本来任务之间就有一定的相互支撑，再设置多个agent，也可以让agent虽然在执行不同的任务，但是也在相互支撑

> 思考：
>
> 1. 是否可以提供更多的专业背景知识，或者说利用领域模型，或者针对某个任务特别训练过的模型，或者再增加一些增强方法呢？
>    1. 比如对于NER任务，如果提供本体网络给LLMs，或者以RAG的方法让其把NER分成：1. 定位本体 2. 实体抽取，是否可以呢？（但是也不知道这样是否合理，考虑可行性）
> 2. 针对上面的5. 如果只有单一任务，比如只有NER任务的话，Agent的技术应该如何使用呢？

**Article：**Zero-Shot Information Extraction via Chatting with ChatGPT

> ChatIE
>
> 这文章不知道啥时候看过啊...本来还说这篇文章被提到的挺多的，去看一下，结果在Zotero里面发现有我的浏览历史记录。。。
>
> （多谢Zotero style）
>
> ChatIE核心的思想就是任务分解，也没有多余的验证工作，即两阶段的多轮问答框架来完成信息抽取的工作（其实就是KG construction的那些），包括NER、RE、EE
>
> - 在第一阶段找出相应的元素类型（在三个任务中分别找出句子中的实体、关系或事件的现有类型）
> - 在第二阶段对每个元素类型进行链式信息提取（根据第一阶段提取的元素类型以及相应的任务特定方案，进一步提取相关信息）
> - 利用该框架进行信息提取的效果很明显
> - RE：
>   - 这里其实是三元组的输出，第一阶段是抽取关系，第二阶段根据关系抽取三元组
>     - <img src="./assets/CleanShot 2024-03-11 at 21.00.39@2x.png" alt="CleanShot 2024-03-11 at 21.00.39@2x" style="zoom:33%;" />
>     - 这里的r指的是第一阶段提取到的关系，q1指第一阶段的问题，qr指根据第一阶段得到的关系提出的第二阶段的问题，也就得到(s,r,o)
> - NER：第一阶段实体类型，第二阶段根据实体类型抽取实体
> - EE：第一阶段事件类型并分类（进行事件分类，形式化为从给定文本中获取事件类型的文本分类问题），第二阶段*抽取事件吧*（第二阶段致力于论点提取，形式化为一个抽取式机器阅读理解（MRC）问题，该问题识别与第一阶段预测的事件类型相关联的特定角色的论点）【说得这么看不懂呢。。。。】
>   - **实体（Entity）**：具有特定语义的基本单元，如时间、人物、地点、数量、组织机构等；
>   - **事件触发词（Event Trigger）：**标志了某种类型事件发生的词汇。
>   - **事件类型（Event Type）**：所发生的事件的类别；
>   - **事件论元（Event Argument）**：参与事件发生的要素，由实体构成
>   - **论元角色（Argument Role）**：事件论元在事件中扮演的角色, 每种事件类型均预定义了多个不同的论元角色域。

思考：

1. 感觉利用LLMs的主要的强化方法就是：
   1. 任务分解
   2. 反思、纠正
   3. 多智能体协作
2. 一般情况下，即使分解任务，他也输出不稳定的

-----

### 2024.03.12 {#2024.03.12}

**Article**：Evidence-Focused Fact Summarization for Knowledge-Augmented Zero-Shot Question Answering

> 主要是利用了摘要的技术，从helpfulness和faithfulness两个角度出发，优化summarizer
>
> summarizer的作用就是将KG的检索结果变成一段文本摘要
>
> 可以学习一下summarizer的微调的方法，还有他的观点，从helpfulness和faithfulness出发进行偏好filter
>
> - helpful主要就是summarization里的东西是否真的帮助了答案的生成
> - faithful就是摘要的生成的效果（是否包含无效信息或者幻觉信息）
>
> 思考：
>
> 1. 摘要确实是可以简化上下文，一定程度提升LLMs响应的性能，但是主要还是看检索的能力吧，感觉看她的誓言来说，摘要确实是有一定的效果，但是对于KAPING和Rewrite的方法的提升好像并不多，那两种方法都是简洁地将三元组要么不加工要么简单通过关系路径转化成文本，也许这种简单的信息模式才是更加适合LLMs的呀。。。
> 2. 感觉在normal RAG+KG RAG的情况下，确实可以用这个方法来优化最后给LLMs的上下文，但是如何权衡从文档里检索的结果和KG里检索的结果呢？
> 3. 清晰的上下文（证据清晰）+偏好对齐，可能在这个KG的方法上效果没有那么好，但是对于文本的话确实蛮重要的
>    1. 没有研究过文本摘要技术，也许这几个点早就不新鲜了
>    2. 这作者真是走了歪门邪道了..看这篇但也不算毫无收获吧
> 4. 对知识蒸馏也了解的不多，这个什么LLMs distillation以后再说吧...

---

### 2024.03.13{#2024.03.13}

**Article：**Unlocking the Power of Large Language Models for Entity Alignment

> 2024.2.23 的一个最新的LLMs来做实体对齐的文章
>
> 可以了解一下这个作者的其他的文章，都是LLM+KG的
>
> - 指出了knowledge representation learning(KRL)的方法的不足之处
> - 思路是：
>   - 使用KRL的方法来选择候选
>   - 用LLM来进行推理判断（还有LLM的知识增强）
>
> tips：
>
> - KG-code translation，使用代码，==**看看那个文章吧**==
>
>   - If LLM Is the Wizard, Then Code Is the Wand: A Survey on How Code Empowers Large Language Models to Serve as Intelligent Agents
>
> - 使用迭代来平衡效率和准确性
>
> - 使用llms的内部知识来扩展实体的相关信息
>
>   - > 这一步我想知道会不会用了llm来扩展，又用llm来判断会有影响呢，或许有别的扩展信息的方法么，或者用不同的llm
>     >
>     > - 有没有可能在这里加入检索的那些东西，比如从文本里面获取更多的信息，这样好像更慢了？
>
> - 。。我真的觉得这个策略挺好的，呜呜



> 腾讯的一篇文章 More Agent is all you need
>
> 机器之心的介绍，主要的观点：
>
> 1. 多数投票的方法，agent越多，效果越好
> 2. 问题越复杂，效果越明显
> 3. 解决问题的步骤数量越多，性能提升效果越好
> 4. 正确答案的先验概率越高，性能提升越大，这意味着在正确答案更有可能的情况下，增加 agent 数量更有可能带来显著的性能提升。
>
> 两种优化策略：
>
> 1. 逐步采样和投票（Step-wise Sampling-and-Voting）：这种方法将任务分解为多个步骤，并在每个步骤中应用采样和投票，以减少累积错误并提高整体性能。
> 2. 分层采样和投票（Hierarchical Sampling-and-Voting）：这种方法将低概率任务分解为多个高概率子任务，并分层解决，同时可以使用不同模型来处理不同概率的子任务以降低成本。

---

### 2024.03.14_2024.03.15{#2024.03.14_2024.03.15}

> 3.14 改了一下LLMs+KGC的一个图，还需要再扩展一下思路，临时看了个KGC的文章..
>
> <img src="./assets/CleanShot 2024-03-15 at 10.52.50@2x.png" alt="CleanShot 2024-03-15 at 10.52.50@2x" style="zoom:50%;" />
>
> - ==**想到的可以改进的点：**==
>
>   - 用代码，参考 [2024.03.13](#KG-Code_LLM_KRL)
>
> - 结合KGC模型，是不是也可以用[2024.03.13](#KG-Code_LLM_KRL)，使用LLMs做决策，而KGC的模型作为候选的筛选？
>
> - > 为啥都是那篇文章的想法啊...想不到别的



**Article：**Multi-perspective Improvement of Knowledge Graph Completion with Large Language Models

> - 这篇文章的思路就是从实体信息、关系、结构三个角度使用LLMs扩充信息，并还用KGC模型完成KGC的任务
>
>   - 实体：获取相关的信息（还被我抄走了哈哈）
>
>   - 关系：
>
>     - 关系定义——对应Global，缩小关系的选择范围，
>
>       - >  其实我刚开始看到prompt的时候没感觉出来他在缩小范围....
>
>     - 关系组成的三元组的定义——对应local，用于定位可能的头尾实体
>
>       - > 讲道理，有没有可能他的这一块比较乱，没有想好策略，总感觉prompt和解释的不太一样
>
>     - 关系reverse——对应reverse，反转关系
>
>       - > 这个反转属实是没太看明白，那个reverse prediction反向预测？后面有机会再了解一下
>
> 一点想法：
>
> - 对于关系的加工有点复杂了，而且他这个prompt我觉得设计思路挺好的，**缩小关系范围、定义头尾实体**可能的范围，但是这prompt我确实是么太看明白是为啥这样写呀
> - 感觉最近的一个实体对齐一个这个kgc都是用LLM的知识扩展信息，尤其是实体的自己的定义，这个思路可以
> - 使用LLMs做决策，而KGC的模型作为候选的筛选，这样不知道效果如何
> - prompt还是得写好
> - 多看看别的kgc增强的方法

**Article：**Knowledgeable Preference Alignment for LLMs in Domain-specific Question Answering

> 知识型偏好**对齐**
>
> 记录：
>
> - 讲了在微调中如何应用这个偏好对齐：preference set，一给QA对给多个回答（l个），然后标记ri作为偏好分数，训练L_align 对齐的损失函数，并和之前的领域QA的训练的损失函数结合在一起作为最终的训练目标
> - 感觉是一个不错的微调策略，既针对了QA任务，又针对了偏好，对偏好分成style（简洁，人类更容易接受）、knowledge（不接受无用知识，减轻检索的错误带来的误导）
>   - 在偏好设置的时候，有打分机制
>     - golden answer和不同能力的LLM给出的答案从高到低排名
>     - golden answer和不同的知识排序（检索的top-k -> 空，没有检索结果 -> topk+1到top2k被视为误导信息，相关却没用，排名最后，影响也最大）
> - 他们这个图是真的好看又清晰
>   - <img src="./LLM+KG/assets/CleanShot 2024-03-15 at 16.17.08@2x.png" alt="CleanShot 2024-03-15 at 16.17.08@2x" style="zoom:50%;" />

- 如果可以用得到的话，还是可以参考他们的对齐的思路的

---

### 2024.03.16{#2024.03.16}

**文章：**Contextualization Distillation from Large Language Model for Knowledge Graph Completion

> KGC 
>
> 代码：https://github.com/DavidLi0406/Contextulization-Distillation

记录：

- 知识蒸馏，用LLM生成上下文描述，增强基于PLM的KGC模型
- entity和triplet的都有用LLM生成description
- 路径用$T$ --> ($ED$, $TD$)：同时生成实体描述和三元组描述（主要方法）
  - 分析是因为PLM模型对于处理复杂的上下文的能力不够，即使用分解的方法，$T$ --> $ED$ --> $TD$，也不行
  - 自己对于这一块还比较陌生...

---

### 2024.03.17{#2024.03.17}

**Article：**Knowledge Graph Large Language Model (KG-LLM) for Link Prediction

> 多跳链接预测
>
> 只用了CoT和ICL
>
> > 真的服了，感觉一点收获都没有，下次就该及时止损不看了.....
>
> 预测还是用的entity和relation的id，如果用上语意关系难道不会更好吗
>
> 唉啥啊这是
>
> 算了，今天就看视频看代码吧，服了服了

---

### 2024.03.18{#2024.03.18}

**Article:**Making Large Language Models Perform Better in Knowledge Graph Completion

> 这文章我觉得思路挺好的，就是问题在于它做的KGC，但是只在triple classification任务上做的
>
> 思路：
>
> 1. self-supervised structural embedding pre-training 学习KG的结构嵌入，得到structural embeddings
> 2. 通过knowledge prefix adapter，将prompt的那个triple的头、关系、尾的刚刚学习的结构的embedding映射到virtual knowledge token 中，放在prompt的最前面
>    1. 放最前面因为decoder-only的LLMs可以良好地利用前面的信息（单向）
>    2. 通过映射可以在prompt中加入当前的节点的结构信息，文中的长度是头、关系、尾都是3个token
> 3. 预训练，让LLM学习到利用这个virtual knowledge的模式，利用这个里面的结构信息来进行任务
>
> 一点点想法：
>
> 1. 这样encode 图谱的结构信息然后映射到prompt中的想法挺好的，但是好像也不是第一个这样做的
>    1. MiniGPT-4: Enhancing Vision-Language Understanding with Advanced Large Language Models.他引用了这篇文章
> 2. 是不是可以借鉴这个思路来在KGC的link prediction的任务上也用上这样的结构信息，还是多看看文章，link prediction了解的太少了
> 3. 有没有其他的创新的方法可以引入结构信息的？

**Article**: Large Language Model with Knowledge in Context for Knowledge Graph Completion

> 2023.12
>
> EMNLP
>
> 方法：
>
> - 因为KGC补尾实体需要输入所有的尾实体来进行比较，直接用LLM不行
> - 因此利用一个Triple-based 模型作为retriever，先选择已经排序好的top-m个candidate
> - 然后把candidate给LLM进行re-rank，得到更好的结果
> - 给LLM的出了candidate，还有一些demonstration
>   - 一种是analogy，相同的关系作为demonstration，还加入了一个方法进行排序，增强demonstration里面的例子的diversity
>   - 一种是supplement，给相同的头实体的triple作为demonstration，要求相近，通过BM25分数排序
> - 在prompt阶段也分了四个阶段来进行
>
> 思考：
>
> - 过多的上下文会不会不好，感觉还有优化的余地
> - 这个做法挺完善的，我反正是想不到什么了，不仅仅想到了利用基础方法进行排序，还想到了如何制作demonstration
>
> 

----

### 2024.03.20{#2024.03.20}



**Article:**AutoRD: An Automatic and End-to-End System for Rare Disease Knowledge Graph Construction Based on Ontologies-enhanced Large Language Models

> 感觉思路简单，没啥参考价值

#### Let Your Graph Do the Talking

**Article:**Let Your Graph Do the Talking: Encoding Structured Data for LLMs

> 这篇文章的思路就是encode结构化信息，放在prompt的embedding的前面，然后给LLM让其decode
>
> 思路类似于之前的那个[triple classification](#2024.03.18)
>
> 记录：
>
> - 把KG通过Encoder进行编码（GNN），
> - 然后根据不同的情景取出（read out）相应的编码
> - 将编码通过全链接层投影到LLM的token的embedding的空间中
>
> 还是看不懂GNN这里的知识点，去学一下

---

### 2024.03.24{#2024.03.24}

#### TALK LIKE A GRAPH

文章：TALK LIKE A GRAPH: ENCODING GRAPHS FOR LARGE LANGUAGE MODELS

> 用不同的方式将图编码为文本，让LLMs学习并进行图的推理
>
> - 不同的场景、思路，比如用Integer encoding (e.g., Node 0).、名字、甚至是Game of Thrones的人物
> - 把问题question也encoding 成具有一定的北京的，比如人物关系：node degree->朋友数量、node->count 人物数量、edge->count 朋友关系数量、connected nodes->listing friends
>
> 这个只是研究的图
>
> 一些关键的结论：
>
> - 对于基础的basic Graph task，LLM的能力不太行
> - 对于简单的任务，simple prompt要比cot来的好，就是说如果不涉及multi-step的话，还硬用cot反而不行
> - graph encoding可以提升LLM的graph task的能力，不同的encoding方法，对于图的结构的侧重不同，因此提升也不同
> - 对于问题进行编码可以提供上下文背景，提升任务的性能
> - 将关系赋予更多的语意（multiple relation），可以丰富上下文，有更多的信息让LLM解决问题
> - 模型越大，graph reasoning ability越好
> - 不同的图结构会影响，过多的边（过于复杂的图结构）会引入无关的信息，阻碍LLM推理

---

### 2024.04.09{#2024.04.09}

> 我又来看文章了！

#### GraphAdapter

文章：Can GNN be Good Adapter for LLMs?

> WWW'24
>
> 提出了GraphAdapter
>
> - 使用GNNencode结构信息
> - 使用PLM encode语意信息
> - concat两个
> - 在PLM的语意的哪里加一个residual Connect 因为不是所有的场景结构信息都有用

---

### 2024.04.12{#2024.04.12}

#### graph representation learning for LLMs

Advancing Graph Representation Learning with Large Language Models: A Comprehensive Survey of Techniques

> 一篇关于graph representation learning for LLMs的短综述
>
> - <img src="./LLM+KG/assets/CleanShot 2024-04-12 at 10.02.06@2x.png" alt="CleanShot 2024-04-12 at 10.02.06@2x" style="zoom:50%;" />
> - 如何更好地结合KG以及LLM
>   - knowledge extractors：抽取KG中的信息
>     - attribute：利用LLM增强文本信息以及encode more comprehensive semantic features
>     - structure：
>       - 增强图的结构
>       - 利用图的结构 
>         - **InstructGLM [Ye et al., 2023]**
>         - **GraphGPT [Tang et al., 2023]**
>       - 问题：对于全局的信息的处理
>     - label：
>       - 利用LLM处理kg的label
>       - 问题：没有考虑结构信息
>   - knowledge organizers：融合（学习）KG的信息
>     - GNN-centric
>       - 用LLM来initializeGNN的输入、optimize输入结构、生成label
>     - LLM-centric
>       - 难点：graph信息要transfer into textual info
>         - 图和描述连接的信息
>     - GNN+LLM
>       - integration
>       - <img src="./LLM+KG/assets/CleanShot 2024-04-12 at 14.10.19@2x.png" alt="CleanShot 2024-04-12 at 14.10.19@2x" style="zoom:50%;" />
>       - input-level
>         - 基于llm的：graph -> textual
>         - 基于GNN的：使用LLM生成virtual nodes
>       - hidden-level
>         - merge LLM的文本的语意表示以及GNN的结构信息的表示
>         - **如何全面利用两种模态的表征来生成具有更强表现能力的高阶表示仍然是一个需要解决的重要问题。**
>       - alignment-based
>         - 对齐对同一个实体的GNN和LLM的特征表示
>           - contrastive alignment：对比学习
>           - iterative：在知识传递的学习过程中节点和图之间进行迭代交互
>           - distillation：**Train your own gnn teacher: Graph-aware distillation on textual graphs.**

>  我在想有没有什么方法可以通过更短的上下文来让LLMs的一次prompt中有更多的信息呢？
>
> - GNN 加层聚合邻域信息？

---

### 2024.04.15{#2024.04.15}

Exploring the Potential of Large Language Models (LLMs) in Learning on Graphs

- 分了两个部分介绍如何让llm学习graph
- 还是关注如何与gnn进行联合
- <img src="./LLM+KG/assets/CleanShot 2024-04-15 at 14.38.46@2x.png" alt="CleanShot 2024-04-15 at 14.38.46@2x" style="zoom:50%;" />
- <img src="./LLM+KG/assets/CleanShot 2024-04-15 at 14.42.26@2x.png" alt="CleanShot 2024-04-15 at 14.42.26@2x" style="zoom:50%;" />
- 介绍了LLM如何处理KG信息，主要有两个方向：处理数据（特征）、生成结果
- 值得考虑的是如何更好地结合GNN，来让LLM有效地学习到结构信息
  - 一个值得记录的地方是：在聚合了不同的标签的邻居之后，会影响判断，这岂不就是说明不能有效地处理结构信息吗....


#### graphSAGE

> 提到了一个方法
>
> GraphSAGE，17年的方法，理解是更好地处理大的图
>
> - 是Induction框架
> - GraphSage不为图中每一个节点学习单独的embedding，而是学习一个聚合函数，该函数通过从节点的本地邻域中抽样和聚合特征来生成节点embedding
> - GraphSage利用节点特征信息（例如，文本属性、节点配置文件信息、节点度）来学习泛化到不可见节点的嵌入函数
> - GraphSage可以利用所有图中存在的结构特征（如节点度），所以也可以应用于没有节点特征的图
> - GraphSage设计了一个无监督损失函数，允许在没有特定任务监督的情况下进行训练
> - <img src="./assets/CleanShot 2024-04-15 at 15.36.55@2x.png" alt="CleanShot 2024-04-15 at 15.36.55@2x" style="zoom:50%;" />
>
> **GraphSAGE算法**
>
> - Embedding生成算法
>
> - <img src="./assets/CleanShot 2024-04-15 at 15.38.01@2x.png" alt="CleanShot 2024-04-15 at 15.38.01@2x" style="zoom:50%;" />
>   - 在每次迭代或搜索深度时，节点从它们的局部邻居那里聚合信息，随着这个过程的迭代，节点从图中以自身为中心的更远处逐渐获得越来越多的信息。
>   - 算法1描述了在整个图$\mathcal{G=(V,E)}$和所有节点的特$\bold{x}_v,\,\forall v\in \mathcal{V}$作为输入的情况下，embedding生成过程。下面将描述如何将其推广到mini-batch的情况。
>     - **输入：**
>       - $k$表示当前外循环的step（步数，也表示搜索深度，即搜索了$k$阶邻居）；
>       - $\bold{h}^k$表示在$k$step 上的节点表示，其中$\bold{h}_v^0=\bold{x}_v$
>     - **第1步：** (第4行) 每个节点$v\in\mathcal{V}$将它的直接邻居节点的表示$\{\bold{h}_u^{k-1},\,\forall u\in\mathcal{N}(v)\}$聚合为一个向量$\bold{h}_{\mathcal{N(v)}}^{k-1}$。这个聚合步骤依赖于在外循环的先前迭代中生成的表示(即$k−1$)，并且$k=0$表示被定义为输入节点特征。
>     - **第2步：** (第5行) 将聚合的邻居表示$\bold{h}_{\mathcal{N(v)}}^{k-1}$与当前节点的表示 $\bold{h}_v^{k-1}$进行concat并送入全连接层中（权重为 $\bold{W}^k$），生成下一次循环需要的节点表示$ \bold{h}_v^{k}$。
>     - **第3步：** 如果内循环未结束，则进入第1步，直接使用$\bold{h}_v^{k}$作为节点$v$的特征用于生成其他节点表示(如作为其他节点的邻域节点)；如果是内循环结束，(第7行) 则将$\bold{h}_v^{k}$进行原地标准化$ \bold{h}_v^{k}/\lVert \bold{h}_v^{k} \rVert_2$，进入第4步。
>     - **第4步：** 如果外循环未结束，将第3步生成的$\bold{h}_v^{k}$用于$k+1$阶节点表示的生成，进入第1步。如果外循环结束，(第9行) 则将第3步生成的节点表示作为节点的最终输出。
>   - 第3步聚合邻居节点所用到的聚合函数$AGGREGATE_k$
>   - **扩展到mini-batch：**给定一组输入节点，首先采样 $K$ 阶邻居集合，然后执行内循环，与第3行不同的是，不是遍历所有节点，而是只计算满足每个深度递归所需的节点表示。
>
> 
>
> #### inductive v.s. transductive learning 
>
> 涉及到了一个inductive learning以及transductive learning
>
> - <img src="./assets/CleanShot 2024-04-15 at 15.08.39@2x.png" alt="CleanShot 2024-04-15 at 15.08.39@2x" style="zoom:50%;" />
>
>   - >半监督学习可进一步分为纯(pure)半监督学习和直推学习(transductive learning)，前者假定训练数据中的未标记样本并非带预测的数据，而后者则假定学习过程中所考虑的未标记样本恰是待预测数据，学习的目的就是在这些未标记样本上获得最优泛化性能。换言之，纯半监督学习是基于“开放世界”假设，希望学到的模型能适用于训练过程中未观察到的数据；直推学习是基于“封闭世界”假设，仅试图对学习过程中观察到的未标记样本进行预测。
>
>   - <img src="./assets/CleanShot 2024-04-15 at 15.11.07@2x.png" alt="CleanShot 2024-04-15 at 15.11.07@2x" style="zoom:50%;" />
>
> - `transductive learning`，翻译为直推学习
>   - ==**Transduction** 是从观察到的、特定的训练样本到特定的测试的推理。==
>   - Transductive learning 事先看到了所有数据，包括训练和测试数据集。通常训练集是带标签的数据，测试集是不带标签的数据。从已经观察到的训练集和测试集中学习，然后预测测试数据集的标签。在训练过程中，使用的是测试集中除了标签以外的其他信息，比如在图中测试数据的结构信息（参见kipf-GCN）。
>
> - (纯)半监督学习，可以理解为 `Inductive Learning`。
>   - ==**Induction** 是从观察到的训练样本生成规则推理，然后将规则推理应用于测试样本。==
>     - Inductive learning 与我们通常所知的传统监督学习相同。基于已经拥有的标记训练数据集构建和训练机器学习模型。然后我们使用这个训练过的模型来预测以前从未遇到过的测试数据集的标签
>
> https://blog.csdn.net/u012762410/article/details/127213748

#### **拉普拉斯矩阵**

> - https://blog.csdn.net/qq_45448654/article/details/122692366?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171316420416800185812503%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171316420416800185812503&biz_id=0
>
> - https://blog.csdn.net/weixin_45884316/article/details/117431134?depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-8-117431134-blog-122692366.235%5Ev43%5Epc_blog_bottom_relevance_base7
>
> <img src="./assets/CleanShot 2024-04-15 at 15.18.07@2x.png" alt="CleanShot 2024-04-15 at 15.18.07@2x" style="zoom:50%;" />
>
> - 拉普拉斯矩阵的定义与性质
>
>   - 对于一个有n个顶点的图G，它的拉普拉斯矩阵(Laplacian Matrix)定义为：$L=D−A$
>
>     - 其中，D是图G的度矩阵，A是图G的邻接矩阵。L中的元素可定义为：
>       - <img src="./assets/CleanShot 2024-04-15 at 15.19.01@2x.png" alt="CleanShot 2024-04-15 at 15.19.01@2x" style="zoom:50%;" />
>
>   -  通常， 我们需要将拉普拉斯矩阵进行归一化。常用的有两种方式。
>
>     1. 对称归一化的拉普拉斯矩阵(Symmetric Normalized Laplacian Matrix)
>
>        ​	<img src="./assets/CleanShot 2024-04-15 at 15.19.46@2x.png" alt="CleanShot 2024-04-15 at 15.19.46@2x" style="zoom:50%;" />
>
>     2. 随机游走归一化的拉普拉斯矩阵(Random Walk Normalized Laplacian Matrix)
>
>        ​	<img src="./assets/CleanShot 2024-04-15 at 15.20.07@2x.png" alt="CleanShot 2024-04-15 at 15.20.07@2x" style="zoom:50%;" />
>
>   -  从这个L矩阵中可以观察到拉普拉斯矩阵的以下几条性质。
>
>     - L是对称的
>     - L是半正定矩阵（每个特征值$ \lambda_i{\geq}0$）
>     - L的每一行每一列的和为0
>     - L的最小特征值为0。给定一个特征向量$v_0=(1,1,\cdots,1)^T$ ，根据上一条性质，L的每一行之和为0，所以$Lv_0=0$
>
> - 拉普拉斯矩阵的推导与意义

---

### 2024.04.16{#2024.04.16}

#### Graph Language Models

- 利用语言模型的参数初始化，调整位置编码的方式以及自注意力

- 利用Levi graph

  - <img src="./assets/CleanShot 2024-04-17 at 11.24.30@2x.png" alt="CleanShot 2024-04-17 at 11.24.30@2x" style="zoom:50%;" />

  - > 好像类似的工作比如graph2text，都要把图变成这种一个token一个节点的形式，然后像处理序列一样处理图

- 能够同时处理图信息和文本信息

- 除了在单个triplet中有相对位置编码

  - 还在global的设定中学习了triplet之间（G2G）的注意力
  - 在有文本的情况下，还有G2T、T2G

---

### 2024.04.17{#2024.04.17}

#### Language is All a Graph Needs

使用自然语言描述图结构，然后指令微调LLM来学习相关的信息

<img src="./assets/CleanShot 2024-04-17 at 16.12.13@2x.png" alt="CleanShot 2024-04-17 at 16.12.13@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-04-17 at 16.12.33@2x.png" alt="CleanShot 2024-04-17 at 16.12.33@2x" style="zoom:50%;" />

> Google那个文章，Talk like a graph，通过文本描述图结构可以让LLM更好地学习图结构
>
> 二者都是通过natural language来让LLM学习图中的知识的
>
> - 有一个任务是**Graph-to-text**，转换图到文本，如果这个思路可行的话那么可以研究一下
> - `但是我在想对于一个图谱来说里面重要的本身就是文本知识，图谱的结构是为了帮助更好地理解和聚合信息用的，那么确实文本这一块是比较重要的...感觉如果只用结构来预处理递给LLM的信息这个思路是否可行呢`
> - ***如果可以有效地利用一个小模型以及相关的规则，在图谱中找到足够解决当前问题的有效信息，再让LLM进行推理，那么效果应该会很不错***
>   - *这里的话，给LLM的时候应该还可以用这个方法给他结构信息*
>   - ***那么如何<u>在图谱的支持下</u>推理并找到解决当下问题所需要的信息呢？***



---

### 2024.04.17{#2024.04.17}

Mixtral of Experts

- Mixtral 8 x 7B
- Decoder-only
- 在transformer的FFN之前，添加一个routing neural network，用来route输入的token到不同的Expert中（可以理解为分类问题）
- 每一个expert都是一个FFN

---

### 2024.04.18{#2024.04.18}

Mamba: Linear-Time Sequence Modeling with Selective State Spaces

- SSM 状态空间模型 state space model
  - RNN-like
  - 核心思想是在隐状态的转移上没有非线性，不依赖于输入（矩阵A）--->可以提前预计算，打破RNN的必须递归地计算每一个中间状态
    - 可以转换为矩阵的乘法
- Mamba selective state space model
  - 最重要的矩阵A不依赖于输入会导致无法根据输入做针对性推理（即没有选择性，模型无法捕捉到重要的输入）
    - BC、Lambda矩阵变为输入数据驱动
    - 最终计算得到的Aba和Bba矩阵都有Lambda矩阵参与，因此也是输入数据驱动
  - 硬件感知算法
    - parallel scan
    - 定义prefix sum
    - 更简单的SSM结构

---

### 2024.04.19{#2024.04.19}

#### Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs

- <img src="./LLM+KG/assets/CleanShot 2024-04-19 at 15.10.43@2x.png" alt="CleanShot 2024-04-19 at 15.10.43@2x" style="zoom:50%;" />
- 三个阶段利用LLM在图上进行推理：LLM reasoning，LLM-graph interaction，Graph execution

---

### 2024.04.20{#2024.04.20}

#### ResearchAgent: Iterative Research Idea Generation over Scientific Literature with Large Language Models

<img src="./Agents/assets/CleanShot 2024-04-20 at 11.16.43@2x.png" alt="CleanShot 2024-04-20 at 11.16.43@2x" style="zoom:50%;" />

利用两个Agent：Research Agent 和Reviewing Agent来做文章idea生成，结合了图谱的检索

- 每个Agent都分三个阶段进行：
  - Problem identification
  - Method Development
  - Experiment Design

---

### 2024.04.21{#2024.04.21}

#### LABEL-FREE NODE CLASSIFICATION ON GRAPHS WITH LARGE LANGUAGE MODELS (LLMS)

Key Points：label-free node classification、使用llm annotate

- 聚类方法结合其他方法进行node selection
- 用llm对选择的node进行标注
- 筛选掉效果差的
- 使用GNN进行任务

---

### 2024.04.22{#2024.04.22}

#### Two-stage Generative Question Answering on Temporal Knowledge Graph Using Large Language Models

> Key Points：
>
> **GenTKGQA**: generative temporal knowledge graph question answering framework
>
> - Subgraph Retrieval: utilize LLM’s intrinsic knowledge
> - Answer Generation: 
>   - virtual knowledge indicators: fuse gnn+textual representataion

> 思考：
>
> - 在这个文章里GNN真的有用吗？
>   - subgraph是比较小的
>   - 消融实验中，甚至只保留的时间信息都效果不错啊
> - 确实可以看到LLM对于implicit temporal information的处理能力是不足的，尤其是相对的那些信息

#### Give Us the Facts: Enhancing Large Language Models with Knowledge Graphs for Fact-aware Language Modeling

Key Points：

- knowledge graph-enhanced large language models (KGLLMs)
  - before-training enhancement
  - during-training enhancement
  - post-training enhancement
