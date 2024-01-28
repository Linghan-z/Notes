# LLM Powered Autonomous Agents 

LLM的潜力不仅限于生成写作流畅的副本、故事、论文和程序；它可以被视为一个强大的通用问题解决器。比如[AutoGPT](https://github.com/Significant-Gravitas/Auto-GPT), [GPT-Engineer](https://github.com/AntonOsika/gpt-engineer) 和 [BabyAGI](https://github.com/yoheinakajima/babyagi)

## Agent System Overview

### Planning

- Subgoal and decomposition 子目标和分解：agent将任务分解成更小、可管理的子目标，方便高效处理任务
- Reflection and refinement 反思和完善：agent对过去的行动进行自我批评和反思，并进行改进，从而提高最终结果的质量

### Memory

- Short-term memory 短期记忆：上下文学习（prompt engineering）视为短期记忆学习
- Long-term memory 长期记忆：agent在长时间内保留和回忆信息的能力

### Tool use

- 

![image-20230727224908723](/Users/zlh/Pictures/typoraPicture/image-20230727224908723.png)Fig. 1. Overview of a LLM-powered autonomous agent system.

## Component One: Planning

一个复杂的任务通常涉及许多的步骤，agent需要提前了解这些步骤并进行规划

### Task Decomposition 任务分解

- **Chain of Thought** (CoT; [Wei et al. 2022](https://arxiv.org/abs/2201.11903))

- **Tree of Thoughts** (ToT; [Yao et al. 2023](https://arxiv.org/abs/2305.10601))

**任务分解：**

1. 通过简单的prompt使用LLM进行分解，例如`"Steps for XYZ.\n1."` `"What are the subgoals for achieving XYZ?"`

2. 通过使用特定任务的指令，例如：`"Write a story outline."`用来写故事
3. 人工输入

**LLM+P** ([Liu et al. 2023](https://arxiv.org/abs/2304.11477))

利用外部的classical planner 进行长期的规划。该方法利用规划领域定义语言（Planning Domain Definition Language, PDDL）作为中间接口来描述规划问题。

在这个过程中，LLM的作用是：

1. 将问题转化为“Problem PDDL”
2. 请求 classical planner 根据现有的“Domain PDDL”来生成一个PDDL计划
3. 将PDDL计划转化为自然语言

基本上，计划步骤为使用外部工具完成

### Self-Reflection 自我反思

self-reflection 是一个较重要的方面，能够使agent通过改进过去的行动决策和纠正以前的错误来不断改进和提高

**ReAct** ([Yao et al. 2023](https://arxiv.org/abs/2210.03629))

ReAct通过将行动空间扩展为任务特定的离散行动和语言空间的组合，将推理和行动融合到LLM中。前者使LLM能够与环境进行交互（例如使用维基百科搜索API），而后者则促使LLM生成自然语言的推理轨迹。

ReAct prompt模板包含了LLM思考的明确步骤，大致格式如下：

``````shell
Thought: ...
Action: ...
Observation: ...
... (Repeated many times)
``````

![image-20230727224814584](/Users/zlh/Pictures/typoraPicture/image-20230727224814584.png)Fig. 2. Examples of reasoning trajectories for knowledge-intensive tasks (e.g. HotpotQA, FEVER) and decision-making tasks (e.g. AlfWorld Env, WebShop). (Image source: [Yao et al. 2023](https://arxiv.org/abs/2210.03629)). 

在对知识密集型任务 knowledge-intensive tasks和决策任务 decision-making tasks两个实验中，`ReAct`的表现均比仅使用`Act`的基准模型表现好（省略`Thought: ...`步骤）

**Reflexion** ([Shinn & Labash 2023](https://arxiv.org/abs/2303.11366))

Reflexion是一个框架，为agent提供动态记忆dynamic memory和自我反思Self-reflection能力，以提高推理能力。

Reflexion具有标准的强化学习设置，其中奖励模型提供简单的二进制奖励，行动空间遵循ReAct的设置，其中任务特定task-specific的行动空间通过语言扩展以实现复杂的推理步骤。

在每个动作$a_t$之后，agent计算一个**启发式Heuristic**函数$h_t$ ，并根据自我反思Self-reflection的结果选择是否重置环境以开始新的试验。

![image-20230727223726118](/Users/zlh/Pictures/typoraPicture/image-20230727223726118.png)Fig. 3. Illustration of the Reflexion framework. 

启发式函数确定轨迹是否**低效Inefficient**或包含**幻觉Hallucination**，并应停止。

- **低效**是指花费过长时间而没有成功的轨迹。
- **幻觉**被定义为遇到一系列连续相同的动作，导致环境中出现相同的观察。

自我反思Self-reflection是通过为LLM提供two-shot example来创建的，每个example都是一对（**失败的轨迹trajectory**，用于指导未来计划变化的**理想反思reflection**）。然后将反思添加到agent的工作记忆中（最多三个）以作为查询LLM的上下文。

![image-20230727224731226](/Users/zlh/Pictures/typoraPicture/image-20230727224731226.png)Fig. 4. Experiments on AlfWorld Env and HotpotQA. Hallucination is a more common failure than inefficient planning in AlfWorld. (Image source: [Shinn & Labash, 2023](https://arxiv.org/abs/2303.11366))

**Chain of Hindsight** (CoH; [Liu et al. 2023](https://arxiv.org/abs/2302.02676))

回顾链（Chain of Hindsight, CoH；刘等人，2023年）鼓励模型通过明确呈现一系列过去的输出序列，并附带反馈信息来改进自身的输出。

人工反馈数据集合$D_h = \{(x, y_i , r_i , z_i)\}_{i=1}^n$

- $x$是prompt
- $y_i$是模型的输出
- $r_i$是人工对$y_i$的打分
- $𝑧_𝑖$ 是相应的人工提供的事后反馈

假设反馈元组按奖励进行排名，$r_n \geq r_{n-1} \geq \dots \geq r_1$，这个过程是有监督的微调supervised fine-tuning的过程，数据是一个 $\tau_h = (x, z_i, y_i, z_j, y_j, \dots, z_n, y_n)$形式的序列，其中$\leq i \leq j \leq n$

该模型经过微调，仅用于预测$𝑦_𝑛$，在给定序列前缀的条件下，使得模型能够自我反思并根据反馈序列产生更好的输出。

该模型可以在测试时使用人工注释选择性地接收多轮指令。

- 为了避免过度拟合，COH增加了正则化项以最大化预训练数据集的对数似然。
- 为了避免捷径和复制（因为反馈序列中有许多常见词语），他们在训练过程中随机掩蔽0% - 5%的先前的标记。

训练数据集： [WebGPT comparisons](https://huggingface.co/datasets/openai/webgpt_comparisons), [summarization from human feedback](https://github.com/openai/summarize-from-feedback), [human preference dataset](https://github.com/anthropics/hh-rlhf).

![image-20230728223316693](/Users/zlh/Pictures/typoraPicture/image-20230728223316693.png)

Fig. 5. After fine-tuning with CoH, the model can follow instructions to produce outputs with incremental improvement in a sequence.

**CoH的理念是在上下文中呈现一系列逐步改进的输出历史，并训练模型跟随趋势产生更好的输出。**

**Algorithm Distillation** (AD; [Laskin et al. 2023](https://arxiv.org/abs/2210.14215))

算法蒸馏(AD；Laskin et al.2023)将同样的想法应用于强化学习任务中的跨情节轨迹，其中算法被封装在长期历史条件的策略中。考虑到一个agent与环境进行多次交互，并且在每个回合中，agent会变得稍微更好，AD将这个学习历史连接起来并输入模型。

因此，我们应该期望下一个预测的动作比之前的尝试表现更好。目标是学习强化学习的过程，而不是训练特定任务的策略本身。

![image-20230728223557991](/Users/zlh/Pictures/typoraPicture/image-20230728223557991.png)

Fig. 6. Illustration of how Algorithm Distillation (AD) works.

这篇论文假设，任何生成一组学习历史的算法都可以通过对动作执行行为克隆来提炼成神经网络。历史数据由一组源策略生成，每个源策略针对特定任务进行训练。

在训练阶段，每次强化学习运行期间会随机抽取一个任务，并使用多个历史片段子序列进行训练，从而使得所学策略不依赖于特定任务。

实际上，该模型具有有限的上下文窗口长度，因此片段应该足够短以构建多个历史片段。学习近似最优的上下文强化学习算法需要2-4个片段的上下文。上下文强化学习需要足够长的上下文。

与三个基准相比的实验：

- ED（expert distillation， 专家蒸馏，使用专家轨迹而非学习历史进行行为克隆）
- source policy 源策略， 用于通过UCB（Upper Confidence Bounds）生成蒸馏轨迹
- RL^2 ， 由于需要在线强化学习，将其用作上界。

AD展示了性能接近RL^2的上下文强化学习能力，尽管仅使用离线RL，并且学习速度比其他基准线快得多。当以源策略的部分训练历史为条件时，AD的改进速度也比ED基准线快得多。

![image-20230729111510193](/Users/zlh/Pictures/typoraPicture/image-20230729111510193.png)

Fig. 7. Comparison of AD, ED, source policy and RL^2 on environments that require memory and exploration. Only binary reward is assigned. The source policies are trained with [A3C](https://lilianweng.github.io/posts/2018-04-08-policy-gradient/#a3c) for "dark" environments and [DQN](http://lilianweng.github.io/posts/2018-02-19-rl-overview/#deep-q-network) for watermaze.

## Component Two: Memory

### Types of Memory

记忆可以定义为获取、存储、保留和后续检索信息所使用的过程。人类大脑中有几种类型的记忆。

1. **Sensory Memory**： 感觉记忆， 这是记忆的最早阶段，能够在原始刺激结束后保留感觉信息（视觉、听觉等）的印象。感觉记忆通常只持续几秒钟。子类包括图像记忆（视觉）、回声记忆（听觉）和触觉记忆（触感）。
2. **Short-Term Memory** (STM) or **Working Memory**：短期记忆（STM）或工作记忆， 它存储我们目前意识到并需要进行复杂认知任务（如学习和推理）所需的信息。短期记忆被认为具有大约7个项目的容量（米勒，1956年），并持续20-30秒。
3. **Long-Term Memory** (LTM)：长期记忆，长期记忆可以将信息储存很长时间，从几天到数十年不等，并且具有基本上无限的存储容量。长期记忆有两个子类型：
   1. Explicit / declarative memory：外显记忆或陈述记忆，这是关于事实和事件的记忆，指的是那些可以有意识地回忆起来的记忆，包括情景记忆（事件和经历）和语义记忆（事实和概念）。
   2. Implicit / procedural memory：内隐记忆或程序记忆，这种类型的记忆是无意识的，涉及到自动执行的技能和例行公事，比如骑自行车或者键盘打字。

![image-20230729112742046](/Users/zlh/Pictures/typoraPicture/image-20230729112742046.png)

Fig. 8. Categorization of human memory.

我们可以大致考虑以下映射：

- 感觉记忆作为学习嵌入原始输入的表征，包括文本、图像或其他形式；
- 短期记忆就像是上下文学习。它是短暂且有限的，因为它受到Transformer有限上下文窗口长度的限制。
- 长期记忆作为外部向量存储，agent可以在查询时关注，并通过快速检索进行访问。

### Maximum Inner Product Search (MIPS) 最大内积搜索

外部存储器可以缓解有限注意力跨度的限制。一个标准的做法是将信息的嵌入表示保存到一个向量存储数据库中，该数据库可以支持快速的最大内积搜索（MIPS）。为了优化检索速度，常见的选择是使用近似最近邻（ANN）算法，以在一定的精度损失下获得巨大的加速，返回大约前k个最近邻。

fast MIPS的几种常见ANN算法选择：

- [**LSH**](https://en.wikipedia.org/wiki/Locality-sensitive_hashing) (Locality-Sensitive Hashing)： 局部敏感hash，它引入了一种哈希函数，使得相似的输入项在很大概率下被映射到相同的桶中，而桶的数量远远小于输入项的数量。

- [**ANNOY**](https://github.com/spotify/annoy) (Approximate Nearest Neighbors Oh Yeah)：核心数据结构是随机投影树，一组二叉树，其中每个非叶节点表示将输入空间分成两半的超平面，每个叶节点存储一个数据点。树是独立且随机构建的，因此在某种程度上模拟了哈希函数。ANNOY搜索在所有树中进行，通过迭代搜索最接近查询的一半，并汇总结果。这个想法与KD树有很大的关联，但可扩展性更强。

- [**HNSW**](https://arxiv.org/abs/1603.09320) (Hierarchical Navigable Small World)：它受到小世界网络的启发，其中大多数节点可以在很少的步骤内到达任何其他节点；例如，社交网络中的“六度分隔”特性。HNSW构建了这些小世界图的分层结构，其中底层包含实际的数据点。中间的层创建了快捷方式以加快搜索速度。在执行搜索时，HNSW从顶层的一个随机节点开始，并向目标节点导航。当无法再靠近时，它会向下移动到下一层，直到达到底层。上层的每次移动都有可能在数据空间中覆盖较大的距离，而下层的每次移动则提高了搜索质量。

  https://zhuanlan.zhihu.com/p/397628955

- [**FAISS**](https://github.com/facebookresearch/faiss) (Facebook AI Similarity Search)：它的工作假设是在高维空间中，节点之间的距离服从高斯分布，因此应该存在数据点的聚类。FAISS通过将向量空间划分为多个簇，然后改进簇内的量化来应用向量量化。搜索首先查找具有粗量化的候选聚类，然后进一步查找具有较细量化的每个聚类。

- [**ScaNN**](https://github.com/google-research/google-research/tree/master/scann) (Scalable Nearest Neighbors)ScaNN中的主要创新是各向异性矢量量化。它将数据点$𝑥_𝑖$量化为$\tilde{x}_i$，使得内积$\langle q, x_i \rangle$尽可能与$\angle q, \tilde{x}_i$的原始距离相似，而不是选择最近的量化质心点。

![image-20230729115122602](/Users/zlh/Pictures/typoraPicture/image-20230729115122602.png)

Fig. 9. Comparison of MIPS algorithms, measured in recall@10. (Image source: [Google Blog, 2020](https://ai.googleblog.com/2020/07/announcing-scann-efficient-vector.html))

Check more MIPS algorithms and performance comparison in [ann-benchmarks.com](https://ann-benchmarks.com/).

## Component Three: Tool Use

工具使用是人类的一个显著和独特特征。我们创造、修改和利用外部物体来做超越我们身体和认知能力的事情。为LLMs配备外部工具可以显著扩展模型的功能。

**MRKL** ([Karpas et al. 2022](https://arxiv.org/abs/2205.00445))：Modular Reasoning, Knowledge and Language 模块化推理、知识和语言。是一种用于自主代理的神经符号架构。提出了一个MRKL系统，其中包含一组“专家”模块，通用的LLM作为路由器将查询路由到最合适的专家模块。这些模块可以是神经网络（例如深度学习模型）或符号化的（例如数学计算器、货币转换器、天气API）。

他们对LLM进行了一项实验，用算术作为测试案例，对其进行了微调，以便能够调用计算器。他们的实验表明，解决口头数学问题比明确陈述的数学问题更困难，因为LLMs（7B Jurassic1-large 模型）无法可靠地提取基本算术的正确参数。这些结果强调了在外部符号化工具能够可靠工作时，**了解何时以及如何使用这些工具非常重要**，这取决于LLM的能力。

**TALM** (Tool Augmented Language Models; [Parisi et al. 2022](https://arxiv.org/abs/2205.12255)) 和 **Toolformer** ([Schick et al. 2023](https://arxiv.org/abs/2302.04761)) 都通过微调语言模型来学习使用外部工具API。数据集根据新增的API调用注释是否能提高模型输出的质量来进行扩展。

ChatGPT [Plugins](https://openai.com/blog/chatgpt-plugins)和OpenAI API [function calling](https://platform.openai.com/docs/guides/gpt/function-calling)是LLM在实践中具有工具使用能力的很好例子。工具API的集合可以由其他开发者提供（如插件）或自定义（如函数调用）。

**HuggingGPT** ([Shen et al. 2023](https://arxiv.org/abs/2303.17580)) 是一个框架，使用ChatGPT作为任务规划器，根据模型描述选择HuggingFace平台上可用的模型，并根据执行结果总结响应。

![image-20230729121358716](/Users/zlh/Pictures/typoraPicture/image-20230729121358716.png)

Fig. 11. Illustration of how HuggingGPT works. (Image source: [Shen et al. 2023](https://arxiv.org/abs/2303.17580))

该系统由4个阶段组成：

1.  Task planning：任务规划，LLM作为大脑，将用户请求解析为多个任务。每个任务都有四个属性：任务类型、ID、依赖关系和参数。他们使用few-shot来指导LLM进行任务解析和规划。

   Instruction:

   ``````shell
   The AI assistant can parse user input to several tasks: [{"task": task, "id", task_id, "dep": dependency_task_ids, "args": {"text": text, "image": URL, "audio": URL, "video": URL}}]. The "dep" field denotes the id of the previous task which generates a new resource that the current task relies on. A special tag "-task_id" refers to the generated text image, audio and video in the dependency task with id as task_id. The task MUST be selected from the following options: {{ Available Task List }}. There is a logical relationship between tasks, please note their order. If the user input can't be parsed, you need to reply empty JSON. Here are several cases for your reference: {{ Demonstrations }}. The chat history is recorded as {{ Chat History }}. From this chat history, you can find the path of the user-mentioned resources for your task planning.
   ``````

2. Model selection：模型选择，LLM将任务分配给专家模型，其中请求被构建为一个多项选择问题。LLM被提供了一个模型列表供选择。由于上下文长度有限，需要基于任务类型进行筛选。

   Instruction:

   ``````shell
   Given the user request and the call command, the AI assistant helps the user to select a suitable model from a list of models to process the user request. The AI assistant merely outputs the model id of the most appropriate model. The output must be in a strict JSON format: "id": "id", "reason": "your detail reason for the choice". We have a list of models for you to choose from {{ Candidate Models }}. Please select one model from the list.
   ``````

3. Task execution：任务执行，专家模型在特定任务上执行并记录结果。

   Instruction:

   ``````shell
   With the input and the inference results, the AI assistant needs to describe the process and results. The previous stages can be formed as - User Input: {{ User Input }}, Task Planning: {{ Tasks }}, Model Selection: {{ Model Assignment }}, Task Execution: {{ Predictions }}. You must first answer the user's request in a straightforward manner. Then describe the task process and show your analysis and model inference results to the user in the first person. If inference results contain a file path, must tell the user the complete file path.
   
   ``````

4. Response generation：响应生成，LLM接收执行结果并向用户提供总结的结果。

要将HuggingGPT应用于现实世界中，需要解决几个挑战：（1）需要提高效率，因为LLM推理轮次和与其他模型的交互会减慢进程；（2）它依赖于一个长的上下文窗口来传达复杂任务内容；（3）需要改进LLM输出和外部模型服务的稳定性。

**API-Bank** ([Li et al. 2023](https://arxiv.org/abs/2304.08244))是评估工具增强型LLM（tool-augmented LLMs）性能的基准。它包含53个常用的API工具，一个完整的工具增强型LLM工作流程，以及264个包含568个API调用的注释对话。所选的API非常多样化，包括搜索引擎、计算器、日历查询、智能家居控制、日程管理、健康数据管理、账户认证工作流程等等。由于API数量众多，LLM首先通过API搜索引擎获取正确的API调用，并使用相应的文档进行调用。

<img src="/Users/zlh/Pictures/typoraPicture/image-20230729122310571.png" alt="image-20230729122310571" style="zoom:50%;" />

图12. LLM在API-Bank中进行API调用的伪代码。（图片来源：Li et al. 2023）

在API-Bank的工作流程中，LLMs需要做出一些决策，而在每个步骤中，我们可以评估这个决策的准确性。这些决策包括：

1. 是否需要进行API调用。
2. 确定要调用的正确API：如果不够好，LLMs需要迭代地修改API的输入（例如，决定搜索引擎API的搜索关键词）。
3. 根据API结果的反馈，如果模型对结果不满意，可以选择进行改进并重新调用。

这个基准评估了agent在三个层面上的工具使用能力：

- Level-1评估*调用API*的能力。根据API的描述，模型需要确定是否调用给定的API，正确地调用它，并对API返回做出适当响应。

- Level-2评估了*检索API*的能力。模型需要搜索可能解决用户需求的API，并通过阅读文档学习如何使用它们。
- Level-3评估的是*超越检索和调用的API规划能力*。鉴于用户请求不明确（例如，安排团队会议，为旅行预订航班/酒店/餐厅），模型可能需要进行多次API调用来解决问题。

## Case Studies

### Scientific Discovery Agent 科学发现代理

ChemCrow ([Bran et al. 2023](https://arxiv.org/abs/2304.05376))

### Generative Agents Simulation 生成代理模拟

Generative Agents ([Park, et al. 2023](https://arxiv.org/abs/2304.03442)) 

### Proof-of-Concept Examples 概念验证示例

[AutoGPT](https://github.com/Significant-Gravitas/Auto-GPT)引起了很多关注，因为它有可能建立起以LLM为主控制器的自主代理。鉴于自然语言界面，它存在相当多的可靠性问题，但仍然是一个很酷的概念验证演示。AutoGPT中有很多代码是关于格式解析的。

这是AutoGPT使用的系统消息，其中{{...}}表示用户输入内容：

``````python
You are {{ai-name}}, {{user-provided AI bot description}}.
Your decisions must always be made independently without seeking user assistance. Play to your strengths as an LLM and pursue simple strategies with no legal complications.

GOALS:

1. {{user-provided goal 1}}
2. {{user-provided goal 2}}
3. ...
4. ...
5. ...

Constraints:
1. ~4000 word limit for short term memory. Your short term memory is short, so immediately save important information to files.
2. If you are unsure how you previously did something or want to recall past events, thinking about similar events will help you remember.
3. No user assistance
4. Exclusively use the commands listed in double quotes e.g. "command name"
5. Use subprocesses for commands that will not terminate within a few minutes

Commands:
1. Google Search: "google", args: "input": "<search>"
2. Browse Website: "browse_website", args: "url": "<url>", "question": "<what_you_want_to_find_on_website>"
3. Start GPT Agent: "start_agent", args: "name": "<name>", "task": "<short_task_desc>", "prompt": "<prompt>"
4. Message GPT Agent: "message_agent", args: "key": "<key>", "message": "<message>"
5. List GPT Agents: "list_agents", args:
6. Delete GPT Agent: "delete_agent", args: "key": "<key>"
7. Clone Repository: "clone_repository", args: "repository_url": "<url>", "clone_path": "<directory>"
8. Write to file: "write_to_file", args: "file": "<file>", "text": "<text>"
9. Read file: "read_file", args: "file": "<file>"
10. Append to file: "append_to_file", args: "file": "<file>", "text": "<text>"
11. Delete file: "delete_file", args: "file": "<file>"
12. Search Files: "search_files", args: "directory": "<directory>"
13. Analyze Code: "analyze_code", args: "code": "<full_code_string>"
14. Get Improved Code: "improve_code", args: "suggestions": "<list_of_suggestions>", "code": "<full_code_string>"
15. Write Tests: "write_tests", args: "code": "<full_code_string>", "focus": "<list_of_focus_areas>"
16. Execute Python File: "execute_python_file", args: "file": "<file>"
17. Generate Image: "generate_image", args: "prompt": "<prompt>"
18. Send Tweet: "send_tweet", args: "text": "<text>"
19. Do Nothing: "do_nothing", args:
20. Task Complete (Shutdown): "task_complete", args: "reason": "<reason>"

Resources:
1. Internet access for searches and information gathering.
2. Long Term memory management.
3. GPT-3.5 powered Agents for delegation of simple tasks.
4. File output.

Performance Evaluation:
1. Continuously review and analyze your actions to ensure you are performing to the best of your abilities.
2. Constructively self-criticize your big-picture behavior constantly.
3. Reflect on past decisions and strategies to refine your approach.
4. Every command has a cost, so be smart and efficient. Aim to complete tasks in the least number of steps.

You should only respond in JSON format as described below
Response Format:
{
    "thoughts": {
        "text": "thought",
        "reasoning": "reasoning",
        "plan": "- short bulleted\n- list that conveys\n- long-term plan",
        "criticism": "constructive self-criticism",
        "speak": "thoughts summary to say to user"
    },
    "command": {
        "name": "command name",
        "args": {
            "arg name": "value"
        }
    }
}
Ensure the response can be parsed by Python json.loads
``````

[GPT-Engineer](https://github.com/AntonOsika/gpt-engineer)是另一个项目，旨在根据自然语言中指定的任务创建一个完整的代码库。 GPT-Engineer被指示思考一系列较小的组件来构建，并根据需要要求用户提供输入以澄清问题。

以下是一段示例对话，用于向GPT-Engineer的OpenAI ChatCompletion端点发送任务澄清请求，用户输入被包裹在 `{{user input text}}` 中。

``````json
[
  {
    "role": "system",
    "content": "You will read instructions and not carry them out, only seek to clarify them.\nSpecifically you will first summarise a list of super short bullets of areas that need clarification.\nThen you will pick one clarifying question, and wait for an answer from the user.\n"
  },
  {
    "role": "user",
    "content": "We are writing {{a Super Mario game in python. MVC components split in separate files. Keyboard control.}}\n"
  },
  {
    "role": "assistant",
    "content": "Summary of areas that need clarification:\n1. Specifics of the Super Mario game (e.g. level design, characters, gameplay mechanics)\n2. Details about the MVC components (e.g. which components are in each file)\n3. Keyboard control implementation (e.g. which keys to use, how to handle input)\n\nClarifying question:\nCan you provide more details about the Super Mario game, such as level design, characters, and gameplay mechanics?"
  },
  {
    "role": "user",
    "content": "{{There are 10 levels in total. The main character is a plumber named Mario, who can walk and jump. It is a classical platform game just like Super Mario. The main character moves from left to right, trying to get to the destination, where there are many obstacles and attacks from enemies in the process.}}\n\nIs anything else unclear? If yes, only answer in the form:\n{remaining unclear areas} remaining questions.\n{Next question}\nIf everything is sufficiently clear, only answer \"Nothing more to clarify.\"."
  },
  {
    "role": "assistant",
    "content": "Remaining unclear areas: 2 remaining questions.\nCan you provide more information about how the MVC components are split into separate files?"
  },
  {
    "role": "user",
    "content": "{{Make your own assumptions and state them explicitly before starting}}"
  }
]
``````

在这些澄清之后，代理人进入了一个不同的系统消息的代码编写模式。系统消息：

You will get instructions for code to write. You will write a very long answer. Make sure that every detail of the architecture is, in the end, implemented as code. Make sure that every detail of the architecture is, in the end, implemented as code.

Think step by step and reason yourself to the right decisions to make sure we get it right. You will first lay out the names of the core classes, functions, methods that will be necessary, as well as a quick comment on their purpose.

Then you will output the content of each file including ALL code. Each file must strictly follow a markdown code block format, where the following tokens must be replaced such that FILENAME is the lowercase file name including the file extension, LANG is the markup code block language for the code’s language, and CODE is the code:

FILENAME

```LANG
CODE
```

You will start with the “entrypoint” file, then go to the ones that are imported by that file, and so on. Please note that the code should be fully functional. No placeholders.

Follow a language and framework appropriate best practice file naming convention. Make sure that files contain all imports, types etc. Make sure that code in different files are compatible with each other. Ensure to implement all code, if you are unsure, write a plausible implementation. Include module dependency or package manager dependency definition file. Before you finish, double check that all parts of the architecture is present in the files.

Useful to know: You almost always put different classes in different files. For Python, you always create an appropriate requirements.txt file. For NodeJS, you always create an appropriate package.json file. You always add a comment briefly describing the purpose of the function definition. You try to add comments explaining very complex bits of logic. You always follow the best practices for the requested languages in terms of describing the code written as a defined package/project.

Python toolbelt preferences:

- pytest
- dataclasses

对话样本：

``````json
[
  {
    "role": "system",
    "content": "You will get instructions for code to write.\nYou will write a very long answer. Make sure that every detail of the architecture is, in the end, implemented as code.\nMake sure that every detail of the architecture is, in the end, implemented as code.\n\nThink step by step and reason yourself to the right decisions to make sure we get it right.\nYou will first lay out the names of the core classes, functions, methods that will be necessary, as well as a quick comment on their purpose.\n\nThen you will output the content of each file including ALL code.\nEach file must strictly follow a markdown code block format, where the following tokens must be replaced such that\nFILENAME is the lowercase file name including the file extension,\nLANG is the markup code block language for the code's language, and CODE is the code:\n\nFILENAME\n```LANG\nCODE\n```\n\nYou will start with the \"entrypoint\" file, then go to the ones that are imported by that file, and so on.\nPlease note that the code should be fully functional. No placeholders.\n\nFollow a language and framework appropriate best practice file naming convention.\nMake sure that files contain all imports, types etc. Make sure that code in different files are compatible with each other.\nEnsure to implement all code, if you are unsure, write a plausible implementation.\nInclude module dependency or package manager dependency definition file.\nBefore you finish, double check that all parts of the architecture is present in the files.\n\nUseful to know:\nYou almost always put different classes in different files.\nFor Python, you always create an appropriate requirements.txt file.\nFor NodeJS, you always create an appropriate package.json file.\nYou always add a comment briefly describing the purpose of the function definition.\nYou try to add comments explaining very complex bits of logic.\nYou always follow the best practices for the requested languages in terms of describing the code written as a defined\npackage/project.\n\n\nPython toolbelt preferences:\n- pytest\n- dataclasses\n"
  },
 #  … same conversation as earlier, ended with "Make your own assumptions and state them explicitly before starting".
  {
    "role": "assistant",
    "content": "Assumptions:\n1. Model: The model will contain the game's data, such as level information, character states, and enemy positions.\n2. View: The view will handle the game's visuals, including rendering the game objects, backgrounds, and updating the display.\n3. Controller: The controller will manage user input, such as keyboard controls, and update the model accordingly.\n\nWith these assumptions in mind, is there any specific aspect of the keyboard control implementation you would like me to clarify?"
  },
  {
    "role": "user",
    "content": "Please now remember the steps:\n\nThink step by step and reason yourself to the right decisions to make sure we get it right.\nFirst lay out the names of the core classes, functions, methods that will be necessary, As well as a quick comment on their purpose.\n\nThen you will output the content of each file including ALL code.\nEach file must strictly follow a markdown code block format, where the following tokens must be replaced such that\nFILENAME is the lowercase file name including the file extension,\nLANG is the markup code block language for the code's language, and CODE is the code:\n\nFILENAME\n```LANG\nCODE\n```\n\nPlease note that the code should be fully functional. No placeholders.\n\nYou will start with the \"entrypoint\" file, then go to the ones that are imported by that file, and so on.\nFollow a language and framework appropriate best practice file naming convention.\nMake sure that files contain all imports, types etc. The code should be fully functional. Make sure that code in different files are compatible with each other.\nBefore you finish, double check that all parts of the architecture is present in the files.\n"
  }
]
``````

## Challenges

在经历了构建以LLM为中心的代理人的关键思想和演示之后，我开始看到一些共同的局限性：

- Finite context length： 有限的上下文长度，受限的上下文容量限制了历史信息、详细指令、API调用上下文和响应的包含。系统的设计必须在这种有限的通信带宽下运作，而像自我反思这样的机制可以从长或无限的上下文窗口中获益良多。虽然向量存储和检索可以提供对更大知识库的访问，但它们的表示能力不如全注意力强大。
- Challenges in long-term planning and task decomposition：长期规划和任务分解中的挑战：在漫长的历史中进行规划并有效地探索解决方案空间仍然具有挑战性。LLMs在面对意外错误时很难调整计划，使它们相对于能够通过试错学习的人类来说不够稳健。
- Reliability of natural language interface：自然语言接口的可靠性：当前的代理系统依赖于自然语言作为LLMs与内部组件（如内存和工具）之间的接口。然而，模型输出的可靠性值得怀疑，因为LLMs可能会出现格式错误，并偶尔表现出叛逆行为（例如，拒绝遵循指令）。因此，大部分代理演示代码都集中在解析模型输出上。



https://zhuanlan.zhihu.com/p/639964649
