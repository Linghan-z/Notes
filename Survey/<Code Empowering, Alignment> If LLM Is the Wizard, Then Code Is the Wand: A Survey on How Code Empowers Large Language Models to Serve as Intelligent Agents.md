# If LLM Is the Wizard, Then Code Is the Wand: A Survey on How Code Empowers Large Language Models to Serve as Intelligent Agents

> 2024.01.08
>
> 代码赋能LLMs 
>
> 介绍：https://zhuanlan.zhihu.com/p/677149809

<img src="./assets/CleanShot 2024-03-14 at 10.35.35@2x.png" alt="CleanShot 2024-03-14 at 10.35.35@2x" style="zoom:50%;" />

图1中的**code 特指机器可执行且人类可读的形式语言**，如编程语言、预定义函数集等。类似于我们指导 LLMs 理解、生成传统自然语言，让 LLMs 精通 code，仅需要将相同的语言建模训练目标应用在 code 数据上

将 code 纳入 LLMs 训练数据的各种优点。具体来说，code 的独特属性有助于：

1. 增强 LLMs 的 code **编写能力、推理能力，以及结构化信息处理能力**，使其能够应用于更复杂的自然语言任务
2. 引导 LLMs 产生结构化的、精确的**中间步骤**，这些步骤可以**通过函数调用与外部执行端连接**
3. 利用 code 的编译、执行环境，为模型自主改进提供多样化反馈

<img src="./assets/CleanShot 2024-03-14 at 10.37.03@2x.png" alt="CleanShot 2024-03-14 at 10.37.03@2x" style="zoom:50%;" />

## 3 Code Pre-Training Boosts LLMs’ Performance Code预训练提升了LLMs的性能

<img src="./assets/CleanShot 2024-03-14 at 10.40.18@2x.png" alt="CleanShot 2024-03-14 at 10.40.18@2x" style="zoom:50%;" />

在第一个部分中，研究人员发现 LLMs 在 code 上的预训练，已将 LLMs 的任务范围扩展到自然语言之外。这些模型能够支持多样化的应用，包括为数学理论生成 code、常规编程任务，以及数据检索等。Code 需要产生逻辑上连贯、有序的步骤序列，这对于有效执行至关重要。此外，code 中每个步骤的可执行性允许逐步验证逻辑。在预训练中利用并嵌入这些 code 属性提高了 LLMs 在许多传统自然语言下游任务中的思维链（CoT）表现，验证了它们在复杂推理技能上的改进。同时，通过对 code 结构化格式的隐式学习，codeLLMs 在常识性结构化推理任务上表现更佳，如与标记语言、HTML 和图表理解相关的任务。

## 4 Code Connects LLMs to Other Function Ends Code连接LLMs与其他执行端

<img src="./assets/CleanShot 2024-03-14 at 10.43.09@2x.png" alt="CleanShot 2024-03-14 at 10.43.09@2x" style="zoom:50%;" />

如图 4 所示，将 LLMs 与其他功能端相连接（即通过外部工具和执行模块扩展 LLMs 能力）有助于 LLMs 更准确、可靠地执行任务。

在第二个部分中，如表 1 所示，研究人员观察到一种普遍趋势：LLMs 通过生成编程语言或利用预定义函数与其他功能端建立连接。这种 “以 code 为中心的范式” 不同于严格在 LLMs 推理机制中硬编码工具调用的刻板做法，它允许 LLMs 动态生成调用执行模块的令牌，具有可调整的参数。

<img src="./assets/CleanShot 2024-03-14 at 10.43.58@2x.png" alt="CleanShot 2024-03-14 at 10.43.58@2x" style="zoom:50%;" />

这种范式为 LLMs 与其他功能端的互动提供了一种简单明确的方式，增强了它们应用的灵活性和可扩展性。更为重要的是，它也允许 LLMs 与涵盖多种模态和领域的众多功能端进行互动。通过扩展 LLMs 可访问的功能端的数量和种类，LLMs 能够处理更复杂的任务。

## 5 Code Provides LLM with an Executable Environment for Automated Feedback Code习得为LLM提供了一个可执行的自动反馈环境



<img src="./assets/CleanShot 2024-03-14 at 10.42.28@2x.png" alt="CleanShot 2024-03-14 at 10.42.28@2x" style="zoom:50%;" />

如图 5 所示，将 LLMs 嵌入 code 执行环境可以实现自动化反馈和模型自主改进。LLMs 的表现超出了其训练参数的范围，部分原因是它们能够接纳反馈。然而，必须谨慎选择反馈，因为嘈杂的提示输入可能会妨碍 LLMs 在下游任务上的表现。此外，由于人力资源代价高昂，反馈需要在保持真实性的同时满足自动收集。在第三个部分中，研究人员发现将 LLMs 嵌入 code 执行环境可以获得满足所有这些标准的反馈

首先，由于 code 执行是确定性的，从执行 code 的结果中获取反馈能够直白忠实反映 LLM 执行的任务。此外，code 解释器为 LLMs 提供了一种自动查询内部反馈的途径，消除了在利用 LLMs 调试或优化错误 code 时需要昂贵的人工注释的需求。Code 编译与执行环境也允许 LLMs 纳入多样化和全面的外部反馈形式，如简单的生成二值的正确和错误评价、稍复杂的对执行结果的自然语言解释，以及各种带有回馈值的排名方法，他们都使得提高性能的方法高度可定制化。

## 6 Application: Code-empowered LLMs Facilitate Intelligent Agents 应用：Code赋能的LLM促进智能代理构建

<img src="./assets/CleanShot 2024-03-14 at 10.45.27@2x.png" alt="CleanShot 2024-03-14 at 10.45.27@2x" style="zoom:50%;" />

通过分析 code 训练数据集成如何增强 LLMs 能力的各种方式，研究人员进一步发现，code 赋能 LLMs 的优势在 Intelligent Agent 的研发这项关键的 LLM 应用领域尤为明显。

图 6 显示了一个智能助理的标准工作流程。研究人员观察到，通过 code 训练在 LLMs 中带来的改进，也同时一一作用于它们作为智能助理时的实际步骤。

这些步骤包括：(1) 增强 IA 在环境感知和规划方面的决策能力， (2) 通过将行动落实于模块化动作原语和高效组织记忆来优化策略执行，以及 (3) 通过从 code 执行环境自动派生的反馈优化性能。

## 总结

总的来说，在本篇综述中，研究人员分析并阐明了 code 如何赋予 LLMs 强大能力，以及 code 如何协助 LLMs 作为 Intelligent Agents 决策中心工作。

通过全面的文献回顾，研究人员观察到经过 code 训练后，LLMs 提高了它们的编程技能和推理能力，获得了实现与跨模式和领域的多种功能端的灵活连接能力，以及强化了与 code 执行环境中集成的评估模块进行互动并实现自动自我提升的能力。

此外，code 训练带来的 LLMs 能力提升有助于它们作为 Intelligent Agent 在下游应用中的表现，体现于如决策、执行和自我提升等特定操作步骤。回顾以往的研究之外，研究人员也提出了该领域的几个挑战，作为未来潜在发展方向的指导要素。