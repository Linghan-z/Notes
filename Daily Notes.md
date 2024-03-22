## Memorandum

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

**Article:**KICGPT: Large Language Model with Knowledge in Context for Knowledge Graph Completion

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

**Article:**Let Your Graph Do the Talking: Encoding Structured Data for LLMs

> 这篇文章的思路就是encode 结构化信息，放在prompt的前面，然后给LLM让其decode
>
> 思路类似于之前的那个[triple classification](#2024.03.18)
>
> 记录：
>
> - 把KG通过Encoder进行编码（GNN），
> - 然后根据不同的情景取出（read out）相应的编码
> - 将编码通过全链接层投影到LLM的token的空间中
>
> 还是看不懂CNN这里的知识点，去学一下





