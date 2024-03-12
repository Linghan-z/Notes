# Beyond Isolation: Multi-Agent Synergy for Improving Knowledge Graph Construction

> 2023.12.29

## Abstract：

图谱构建包含实体抽取、关系抽取、事件抽取，传统上，大型语言模型（LLMs）被视为在这个复杂的领域中独立解决任务的代理

==**CooperKGC**==:与传统方法不同，CooperKGC建立了一个协作处理网络，组建了一个能够同时处理实体、关系和事件提取任务的KGC协作团队。

- 在CooperKGC内促进多样化代理之间的**协作和信息交互**，与独立运行在孤立环境中的个体认知过程相比，产生了更优异的结果。重要的是，由CooperKGC促进的协作增强了跨多轮互动中对**知识选择、修正和聚合能力**。

## 1 INTRODUCTION

KG construction不仅需要理解语言，还需要**在预定义模式的限制范围内精确提取元素**，因此LLMs在KG construction领域的使用还比较有挑战性，当面对知识图谱构建任务的复杂要求时，LLMs 仍然存在性能不足的问题。

用于训练大型语言模型的原始文本数据可能缺乏特定任务的模式，导致对底层模式的语义理解和结构分析减弱

CoT的思路：将信息提取任务分解为不同阶段，不仅减少了搜索空间，还降低了计算复杂性，从而为改进知识图谱构建开辟了一个有前途的途径。



Society of Mind (SOM) 将心智概念化为由简单组件相互作用而形成的复杂系统，本研究探讨了基于LLM代理在多代理系统中的转变潜力。



multi-agent debate framework 多智能体辩论，在任务中进行合作的自我反思 self-reflection

- 一个迭代完善的过程，在每一轮中，根据先前的答案和自我反思生成新的答案
- 通过迭代的反馈来进行持续的改善



<img src="./assets/CleanShot 2024-03-11 at 14.18.27@2x.png" alt="CleanShot 2024-03-11 at 14.18.27@2x" style="zoom:50%;" />

- 包含NER、EE、RE
- 在图中的例子里，NER和RE在EE事件抽取的时候丢失了时间信息的时候协助补充上缺失的时间信息

multi-agent 合作：

1. 具有不同专业知识的代理人的参与提高了协作结果
2. 减轻幻觉
3. 增强抽取结果

**一个有趣的观察结果：==增加合作轮次并不总是会产生更好的结果==**

**contribution**：

- 提出**cooperKGC**，利用LLMs的推理能力，协调多智能体协作过程以提高模型的性能
- 深入研究多代理团队内合作的机制 识别在协作中的具有不同专业知识的LLMs所展示的能力细微差异  借鉴社会学理论来将专家代理在多轮对话互动中的行为和决策倾向置于背景之中
- 模拟通过LLM代理反映了人类社会中微妙的协作能力，揭示了为多智能体系统配置熟练团队成员和采用高效协作策略的重要性

## 2 RELATED WORK

### 2.1 LLM-based Knowledge Graph Construction

> 这部分抄到项目的背景里了，可以参考

知识图谱的构建已经从早期对监督学习方法的依赖显著发展。近年来，人们对在知识图谱领域取得的卓越进展利用LLMs表现出了极大兴趣。Zhu等[1]深入探讨了LLMs在知识图谱构建和推理任务中的应用，揭示了它们在推理和问题回答等任务中出色的能力。在此基础上，Zhang等[2]通过将知识图谱结构信息整合到LLMs中，利用自监督结构嵌入预训练来让LLMs学习图的结构。Wei等[3]认为LLMs本质上具有在交互环境中实现统一的零样本信息抽取能力，因此提出一个两阶段的框架，将信息提取转化为多轮问答结构。Pang等[4]指出任务描述不明确是影响上下文信息提取的性能关键因素，为了解决这个问题，引入了一个引导学习框架来增强模型与指定规则的对齐。Ye等提出CooperKGC框架，建立了一个协作处理网络，组建了一个能够同时处理实体、关系和事件提取任务的KGC协作Agent团队，在CooperKGC框架下促进多样化代理之间的合作和信息交互比单独运行于孤立状态下的认知过程产生更优异结果。目前，在NLP领域更广泛的背景下，已经探索了多种方法来增强LLMs的推理能力，包括从Verification [5]、CoT [6, 7]、Self-Refine [8]、Self-Reflection [9]到Fine-Tuning[10, 11],诸如RLHF [12]，检索增强生成[13, 14]和基于似然估计的无监督训练方法[15]等技术也被用来加强事实一致性。

[1] ZHU Y, WANG X, CHEN J, et al. Llms for knowledge graph construction and reasoning: Recent capabilities and future opportunities [J]. arXiv preprint, 2023, doi: 10.48550/arXiv.2305.13168.

[2] ZHANG Y, CHEN Z, ZHANG W, CHEN H. Making large language models perform better in knowledge graph completion [J]. arXiv preprint, 2023, doi: 10.48550/arXiv.2310.06671.

[3] WEI X, CUI X, CHENG N, et al. Zero-shot information extraction via chatting with chatgpt [J]. arXiv preprint, 2023, doi: 10.48550/arXiv.2302.10205.

[4] PANG C, CAO Y, DING Q, LUO P. Guideline learning for in-context information extraction [C]. In Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing, 2023, doi: 10.18653/v1/2023.emnlp-main.950.

[5] COBBE K, KOSARAJU V, BAVARIAN M, et al. Training verifiers to solve math word problems [J]. arXiv preprint, 2021, doi: 10.48550/arXiv.2110.14168.

[6] KOJIMA T, GU S S, REID M, et al. Large language models are zero-shot reasoners [J]. Advances in neural information processing systems, 2022, 35: 22199-22213.

[7] WEI J, WANG X, SCHUURMANS D, et al. Chain-of-thought prompting elicits reasoning in large language models [J]. Advances in neural information processing systems, 2022, 35: 24824-24837.

[8] MADAAN A, TANDON N, GUPTA P, et al. Self-refine: Iterative refinement with self-feedback [J]. Advances in Neural Information Processing Systems, 2024, doi: 10.48550/arXiv.2303.17651.

[9] SHINN N, LABASH B, GOPINATH A. Reflexion: an autonomous agent with dynamic memory and self-reflection [J]. arXiv preprint, 2023, doi: 10.48550/arXiv.2303.11366.

[10] ZELIKMAN E, WU Y, MU J, GOODMAN N. Star: Bootstrapping reasoning with reasoning [J]. Advances in Neural Information Processing Systems, 2022, 35: 15476-15488.

[11] LEWKOWYCZ A, ANDREASSEN A, DOHAN D, et al. Solving quantitative reasoning problems with language models [J]. Advances in Neural Information Processing Systems, 2022, 35: 3843-3857.

[12] ZIEGLER D M, STIENNON N, WU J, et al. Fine-tuning language models from human preferences [J]. arXiv preprint, 2019, doi: 10.48550/arXiv.1909.08593.

[13] LEWIS P, PEREZ E, PIKTUS A, et al. Retrieval-augmented generation for knowledge-intensive nlp tasks [J]. Advances in Neural Information Processing Systems, 2020, 33: 9459-9474.

[14] GUU K, LEE K, TUNG Z, et al. Retrieval augmented language model pre-training [C]. proceedings of the International conference on machine learning, 2020, doi: 10.48550/arXiv.2002.08909.

[15] KADAVATH S, CONERLY T, ASKELL A, et al. Language models (mostly) know what they know [J]. arXiv preprint 2022, doi: 10.48550/arXiv.2207.05221.

[16] YE H, GUI H, ZHANG A, et al. Beyond Isolation: Multi-Agent Synergy for Improving Knowledge Graph Construction [J]. arXiv preprint, 2023, doi: 10.48550/arXiv.2312.03022.

### 2.2 Interactive Collaboration of Multiple Agents 多代理协作

在促进多个代理之间合作方面值得注意的进展包括开发各种互动架构，通常将代理分配到静态角色中。

- Du等人[6]采用了一个双模型代理设置，参与**多轮辩论**，导致事实性和推理能力增强，但同时也增加了计算开销
- Cohen等人[4]引入了一个**检验LLM**来验证原始LLM生成的结果，利用不同的劳动分工来发现事实错误
- Hao等人[13]的贡献在于ChatLLM网络，使基于对话的语言模型能够**互动、分享反馈，共同讨论问题，在系统内培养多元化观点**
- 此外，引入一名judge参与决策过程，负责**总结辩论并得出最终结论**[27, 66]，展示了引导性辩论提升表现的潜力
- 为了解决自我增强偏见，李等人[23]提出了一个**结合同行评审和讨论的框架**
- Wang等人[59]探讨了多个代理在自我协作轮次中的作用，重点是提高**解决一个复杂任务的问题能力**。

## 3 PRELIMINARIES 准备工作

### 3.1 Task Definition

**Named Entity Recognition**:命名实体

**Relation Extraction**：三元组

**Event Extraction**：为了详细说明该程序，术语的定义如下

- trigger word 触发词：表示最能描述事件的单词或短语
- event argument 事件参数：代表与事件相关联的实体或属性，例如地点或时间
- “Li Shaomin was convicted of espionage and deported.”李少民被判间谍罪并被驱逐出境。
  - 描述的是由convicted词触发的*Convict*事件
  - 事件包含两个参数角色：
    - 被告*Defendant*(Li Shaomin)和罪行*Crime*(espionage)
- 模型应该能够识别事件触发词、类型、参数以及相应的角色

### 3.2 Problem Formulation 问题阐述

在原始文本X的背景下，目标是提取必要的元素Y = {Y1, ..., Y𝑛}，并与模式S所规定的**预定义约束保持一致**

请注意，Y𝑖，𝑖 ∈ 𝑡表示要提取的第i种类型的信息，而𝑛代表类型数量。

- 命名实体识别：Y𝑖的形式为元组 Y𝑖=(𝑒𝑛𝑡𝑖𝑡𝑦−𝑡𝑦𝑝𝑒，𝑒𝑛𝑡𝑖𝑡𝑦−𝑠𝑝𝑎𝑛)
- 关系抽取：Y𝑖的形式是三元组Y𝑖=(𝑒ℎ，𝑟，𝑒𝑡)
- 事件抽取：Y𝑖包含了句子中的事件记录，可以表示为 Y𝑖={𝑒𝑣𝑒𝑛𝑡−𝑡𝑦𝑝𝑒, 𝑒𝑣𝑒𝑛𝑡−𝑡𝑟𝑖𝑔𝑔𝑒𝑟, 𝑎𝑟𝑔𝑢𝑚𝑒𝑛𝑡−𝑠𝑝𝑎𝑛, 𝑎𝑟𝑔𝑢𝑚𝑒𝑛𝑡−𝑟𝑜𝑙𝑒}

## 4 METHODOLOGY 方法

框架：4.1 利用multi-agent来协作； 4.2 为每个Agent赋予专家背景； 4.3 多轮协作互动完善抽取结果； 
这种适应性和协作性的方法致力于“走出孤立”，促进多代理协同作用，改善和细化知识图谱构建过程

<img src="./assets/CleanShot 2024-03-11 at 17.28.58@2x.png" alt="CleanShot 2024-03-11 at 17.28.58@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-11 at 17.28.14@2x.png" alt="CleanShot 2024-03-11 at 17.28.14@2x" style="zoom:40%;" />

### 4.1 Construction of Multi-expert Agent Collaboration Network 多专家智能体协作网络的构建

通过多轮互动进行文本消息的动态交流

传统的方法：将不同的专家代理视为协作网络中的孤立节点，这些节点通过独立的思维链分别为任务解决做出贡献，而中央裁定节点将它们的响应汇集并纠正

- 两个缺点：
  - 中央枢纽的裁定节点表现出**较低的容错能力**，并**需要大量推理能力来吸收分布在不同协作网络中的节点意见**，这种集中负载对系统提出了更高要求；
  - 团队严重依赖**管理节点作为唯一的共识机制**，阻碍了KGC任务参与者之间的有效互动。
- ==**去中心化**==
  - 每一个agent处理某个特定的任务，并建立其他的agent的双向沟通机制
  - 采用轮次来作为交互的基本单位来完成指定任务，并促进专家代理之间的**replica communication**通信（agent产生消息是异步的）
  - 不同的agent保存的消息记录的不同的
    - 是由于LLMs固有的与令牌长度和推理性能瓶颈相关的限制而产生的
  - 在复制通信replica communication过程中，我们实施**消息简化**，提取符合模式约束的结果。
    - 增强信息交换的效率
    - 确保在构建知识图谱方面进行更无缝、更有组织的协作工作

抽象协作网络的形式化包括**三个基本组成部分**：

- **Expert Nodes**：专家节点体现了在KGC中特定子任务上熟练的代理，前一轮中的别的agent的输出的信息+输入x
  - 专家节点可以采取各种形式，包括
    - 由明确指令引导的普通LLM
    - 具有一系列思考链的自我反思代理
    - 通过外部知识库或工具库明确利用领域知识的代理
  - 有了这个基础，本文重点转向代理之间的协作功能
    - 输入文本x，第t轮第i个agent， prompt p-it，之前的agent的回复R-t-1： <img src="./assets/CleanShot 2024-03-11 at 17.15.04@2x.png" alt="CleanShot 2024-03-11 at 17.15.04@2x" style="zoom:33%;" />
- **Communication Edges**：一个双向通信渠道促进KGC协作网络中专家节点间的交流
  - 定向边缘：<img src="./assets/CleanShot 2024-03-11 at 17.19.20@2x.png" alt="CleanShot 2024-03-11 at 17.19.20@2x" style="zoom:33%;" />
    - 𝑎-𝑛 𝑡 可以感知从 𝑎-𝑚 𝑡 −1 传递过来的副本作为其上下文输入
- **Replicas Delivery**:在交互通信单元C中，复制传递充当了从第(𝑡 − 1)轮的代理到第𝑡轮另一个代理的输入消息队列中信息流的导管

### 4.2 Customized Expert Knowledge Background. 定制专家知识背景

三个关键部分：

1. Opening statement P𝑜:开场陈述 P𝑜，每位专家代理人都被提出一个指令，阐明它如何能够贡献其独特的专业知识来解决 KGC 任务。
2. Task definition P𝑡:任务定义 P𝑡，概述了知识图谱提取的具体内容，包括目标元素和指导模式
   1. 比如 RE agent
      1. 第一句话任务描述
      2. 第二句话输出格式
      3. 第三句指向一个特定的关系类型列表
3. In-context demonstration P𝑐:在上下文演示 P𝑐 中，涉及选择一组有限的 M 个实例。这种上下文演示的主要目标是为 LLMs 提供说明性示例
   1. few-shot demonstrations

### 4.3 Collaborative Interaction Optimization 协同交互优化

为了设计智能代理优化方法，ChatIE [62] 提出了一种创新的方法，重点放在任务分解和通过两阶段人工模板选择相关提取对象上。

在团队协作优化的背景下，对于细致分解设计的需求减少了，因为专业代理人在不同领域进行反思性互动，自然地磨练他们的回应。

通过其他专家代理收集复制品后，我们进一步提供协作提示 Pv：`The relation extraction answer you gave in the last round of collaboration was "##LAST_ROUND_RESULT##". The answer given by the NER expert agent in the knowledge graph construction team was "##NER_RESULT##". The EE expert agent gave The answer that comes out is "##EE_RESULT##". You should refer to the answers of other team members to add or delete some of your answers, and give credible reasons. If no modification is needed, please copy the answers from the previous round."`

## 5 EXPERIMENTS

1. RQ1: vs SOTA？
2. RQ2：专家代理和多轮互动中的沟通对团队合作有什么影响？
3. RQ3：复制品交付简化和定制专家知识背景的好处是什么？
4. RQ4：CooperKGC在提取不同类型的实体、关系和事件方面的效果？

### 5.1 Experiment Settings

#### 5.1.1 Dataset

**NER:**

- Conllpp [60]
  - 四种类型的实体
- OntoNotes5.0 [42]
  - 包含18种命名实体类型的英语NER数据集。
- MSRA [19]
  - 用于新闻领域的中文命名实体识别数据集，包含3种实体类型。

**RE:**

- NYT11-HRL [52]
  - 12种预定义的关系
- Re-TACRED [49]
  - 包含超过91,000句子分布在40种关系中的关系抽取
- DuIE2.0 [24]
  - 行业中最大的基于模式的中国房地产数据集，包含48种预定义关系类型

**EE：**

- ACE05 [55]
  - ACE05数据集通过定义33种事件类型和35种角色类型，在文档和句子级别提供了各个领域的事件注释。
- DuEE1.0 [25]
  - DuEE1.0数据集是百度发布的一个中文事件抽取数据集，包含65种事件类型。

#### 5.1.2 Baselines 

- AutoKG [74]：它通过手动模板定义了端到端的提取工作流程
- ChatIE [62]：使用两轮方法优化提取过程。 以RE为例，该方法包括首先提取关系，然后输出相关实体范围。
  - 这种顺序方法反映了认知模型的思维过程，明确划分了任务分解的步骤
- CoT-ER [32]：引入了一种明确的证据推理方法，其特点是三轮处理
  - 在第一轮和第二轮中，需要LLM输出与头实体和尾实体对应的概念级实体
  - 在第三轮中，提取相关实体跨度，建立这两个实体之间具有明确证据的特定关系

#### 5.1.3 Evaluation Protocols 

> micro F1 计算所有样本中正确分类的比例

- NER：micro F1，预测的实体范围应与真实值精确对齐，并且实体类型应该是准确匹配
- RE：standard micro F1，正确性取决于主体和客体实体范围的准确性，以及正确识别关系类型
- EE：ACE05，micro F1，需要预测的事件触发器和参数与地面真相精确对齐。DuEE1.0，F1度量依赖于单词级匹配，确保事件触发器和参数的识别和分类一致性

### 5.2 Performance Comparison with SOTA (RQ1)

- 0-shot & 1-shot
- 100 samples from the test/valid set
- standard micro F1
- gpt-3.5-turbo
- temperature=0
- maximum of rounds to 4

<img src="./assets/CleanShot 2024-03-11 at 18.06.54@2x.png" alt="CleanShot 2024-03-11 at 18.06.54@2x" style="zoom:50%;" />

1. CooperKGC 在各种任务中提高了整体性能
   - 协作架构的优势
   - 与单一执行相比，团队协作提示策略显示了关联不同信息提取任务的好处
   - 部分改进可归因于提取的信息的共享的架构
   - 相比之下，对于像AutoKG这样只进行一轮LLM调用的简单提取方法，一方面，任务理解和规则约束所需的过多信息输入给单个模型带来了挑战。另一方面，缺乏足够的推理步骤进行自我调试过程。
2. 团队合作是一种有效的隐性推理链（以RE的NYT11-HRL为例子）
   1. ChatIE相对于AutoKG的提升来源于对任务的分解
   2. COT-ER利用侧面信息来诱导LLM生成关系推理的明确证据，效果提升更多
      - 直观地，三元组提取可以被视为从头实体到尾实体跨度到关系型推理的映射，因此我们认为收益来自于**对LLM特定任务级别和概念级别知识更加深入的引导**。
   3. 通过在**每一轮互动中收集其他成员的证据**，虽然LLM没有计划好的推理路径，但这种**主动优化**显示出比被动方法更令人鼓舞的前景


### 5.3 Analysis of Team Members and Interaction Rounds (RQ2)

#### 1. knowledge backgrounds：

通过替换NER代理、RE代理和EE代理的专家知识背景，我们分析哪种专家知识背景（主要是任务描述P𝑡中的模式约束）能够为团队建设目标带来更好的效益

<img src="./assets/CleanShot 2024-03-11 at 18.27.11@2x.png" alt="CleanShot 2024-03-11 at 18.27.11@2x" style="zoom:50%;" />

我们观察到组合b（OntoNotes5.0+RE-TACRED+ACE05）使EE专家代理人实现了最佳的提取性能，并且由RE-TACRED引导的更丰富的关系类型允许EE代理人发现与组合a相比更多潜在参数。此外，与组合c相比，组合b实现了更全面的改进

我们分析了OntoNotes5.0与Conllp的模式，发现三个实体类别是相同的(“PER”、“LOC”、“ORG”)，而其余15个更专门的实体类别细化了Conllp中的“MISC”类别，这导致了RE-TACRED和ACE05数据集的提取性能的提升

**更专业的专家代理人，即配备了细粒度模式约束的代理人，可以提供更具洞察力的信息来指导团队合作**。

#### 2. whether it is possible to equip with more agents to make more gains for our team.

<img src="./assets/CleanShot 2024-03-11 at 18.33.06@2x.png" alt="CleanShot 2024-03-11 at 18.33.06@2x" style="zoom:50%;" />

结果：上面一种是在原始团队中添加附加代理，结果表明

- 团队(3-代理+两者)通过增加一个NER代理和一个RE代理使ACE05的提取结果有所改善。
- 然而，另一种风险也被证明，在团队(3-代理+OntoNotes)和团队(3-代理+RE-TACRED)中，观察到当引入更多权威的专家代理时，导致代理对同一任务的提取结果降低，这种无意识的意见整合与社会学中的自我呈现概念[11]是一致的"Presentation of Self"
- 此外，受“self-consistency”[58]的启发，在表3底部我们探讨了自洽投票方法和Coop-erKGC在单个任务上表现差异。
  - 尽管一定程度上的一致性方法减轻了单个代理产生虚构事实的随机性，但仍然比我们在所有三个代表性数据集上的结果要弱。
  - 我们认为，单一视角无法获取其他专家提供的互动信息，并因此遭受“信息茧房”[51]。

#### 3. impact of the number of collaboration rounds on multi-agent teams.

<img src="./assets/CleanShot 2024-03-11 at 18.38.59@2x.png" alt="CleanShot 2024-03-11 at 18.38.59@2x" style="zoom:50%;" />

**对于具有简单提取结构的任务来说，太多互动可能会引入不良幻觉**，因此需要根据特定任务实现性能和合作成本之间的平衡。

### 5.4 Ablation Study of CooperKGC (RQ3)

<img src="./assets/CleanShot 2024-03-11 at 19.24.46@2x.png" alt="CleanShot 2024-03-11 at 19.24.46@2x" style="zoom:50%;" />

- 过滤信息方法还增强了团队内部决策的稳健性，避免个人思维过程中的噪音干扰，并使团队协作更加简洁高效。
- 缺乏自我认知提示会导致代理人在从文本中定位信息方面不熟练
- 具有不同专业化的代理人可以有效地相互协作执行复杂任务

### 5.5 Case Study of Collaboration Process (RQ4)

为了说明我们提出的 CooperKGC 在 KGC 团队中协作互动方面的有效性，表4提供了一个定性示例，展示了中间过程。

<img src="./assets/CleanShot 2024-03-11 at 19.29.15@2x.png" alt="CleanShot 2024-03-11 at 19.29.15@2x" style="zoom:50%;" />

我们将EE代理的结果与标准答案进行比较，而NER代理和RE代理的结果仅供参考，因为没有标准答案

- Knowledge Selection：在第2轮中，EE代理借用了NER代理在上一轮中新发现的LOC实体“border”，并向原始答案添加（Destination，Border）
- Knowledge Correction：在第一轮互动中，EE代理纠正了错误的触发词“taken over”，这表明团队成员有能力提供自我反馈
- Knowledge Aggregation：EE代理在第3轮中提出了错误的argument（Destination，Border）），但通过在互动过程中引发LLM语义理解来纠正期间产生的幻觉事实

## 6 CONCLUSION AND FUTURE WORK

在这项工作中，我们首次尝试聚合具有不同专业知识的代理人形成KGC团队。我们的研究揭示了LLM代理人令人印象深刻的协作能力，展示了代理网络在相互增强任务表现方面的可能性。在协作过程中出现的类似于人类行为 resonates with sociological theories 并有效地提高了LLM在事实性、知识整合和智力推理方面的表现。未来，从社会学角度派生出来的架构可能会提供富有启发性的灵感。CooperKGC 的丰富变体可以应用于多学科认知团队以解决更加灵活多样化的协作任务。此外，随着LLM 的演进，了解团队成员之间适应性组合模式将对指导更多协作代理网络至关重要。
