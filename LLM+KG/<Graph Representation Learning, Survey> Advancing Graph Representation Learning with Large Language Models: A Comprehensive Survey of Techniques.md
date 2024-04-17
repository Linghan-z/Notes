# Advancing Graph Representation Learning with Large Language Models: A Comprehensive Survey of Techniques

#### Graph Representation Learning (GRL):

- graph embedding
- Graph Neural Networks (GNNs)
- graph Transformers

**Can the powerful capabilities of LLMs be harnessed to significantly enhance graph representation learning?**



**primary components：**

- **knowledge extractors：**concerned with extracting knowledge from graph data (e.g., graph encoders),
- **knowledge organizers：**arranging and storing this knowledge (e.g., multi-layer transformers).

**operation techniques：**

- **integration strategies：**combining graph learning models (e.g., GNNs) with LLMs —— how to manage and integrate modules by integration strategies
- **training strategies：**effectively training the unified model.—— how to achieve effective and efficient training by training strategie

<img src="./assets/CleanShot 2024-04-12 at 10.02.06@2x.png" alt="CleanShot 2024-04-12 at 10.02.06@2x" style="zoom:50%;" />

## 3 Knowledge Extractor

three dimensions: graph **attributes**, graph **structures**, and **label** information.

<img src="./assets/CleanShot 2024-04-12 at 10.10.24@2x.png" alt="CleanShot 2024-04-12 at 10.10.24@2x" style="zoom:50%;" />

### 3.1 Attribute Extractor

using LLMs to <u>*generate more complete textual statements*</u> and <u>*encode more comprehensive semantic features*</u>, corresponding to the Textlevel Extractor and Feature-level Extractor

#### Text-level Extractor.

利用LLM的生成能力来增强incomplete textual attributes

- **TAPE [He et al., 2023]** 利用LLM生成额外的解释，让丰富GNN输入的节点的特征
- **Knowledge-Enhanced Attention**  让LLM 生成 relevant knowledge entities

#### Feature-level Extractor.

leverages LLMs to encode the textual representations of nodes in GRL——————<u>*more nuanced and context-aware feature encoding*</u>

- **OFA [Liu et al., 2023a]** converts all nodes, edges and task information into human-readable texts and uniformly encodes them across various domains.

### 3.2 Structure Extractor

两个关键方面：

- noisy graph structure refinement based on LLMs
- graph structure utilization with LLMs

#### Graph Structure Refinement.

leverage the powerful textual semantic representation capabilities of LLMs to uncover implicit, effective graph structural relationships,

- Sun et al. [2023] enables the LLM to assess the **semantic-level similarity between pairs** of nodes in the TAGs through meticulously crafted prompts with textual attributes.
- ENG [Yu et al., 2023] 利用LLMs在TAGs中生成有效节点和相应的图结构，提高GNN模型在fewshot场景中的性能。

#### Graph Structure Utilization.

transforming graph structures or contexts into natural language descriptions

利用LLMs在表示语言输入方面的广泛能力，可以实现有效的信息提取，减少对图结构化输入的依赖。

通过自然语言描述表达特定图结构信息

- **InstructGLM [Ye et al., 2023]** creates templates to describe <u>*each node’s local ego-graph structure*</u> (up to 3-hop connections)
- **GraphGPT [Tang et al., 2023]** introduces special <u>*GraphTokens*</u>, refined through Graph Instruction Tuning, to convey graph structural information, significantly reducing the length of token sequences required to describe structural information.
- **GraphText [Zhao et al., 2023a]** introduces a <u>*syntax tree-based*</u> approach to convert graph structure into text sequences.

全局的图信息

### 3.3 Label Extractor

A key obstacle in GRL, especially in real-world applications, is the scarcity of high-quality annotated data. GRL或者说实际应用的关键的阻碍：高质量标注数据的稀缺

- **LLM-GNN [Chen et al., 2023b]**通过混合提示进行0-shot 输入，标注选定节点并使用置信度分数来丢弃低质量标签。这种策略使得图神经网络能够在没有真实标签的情况下很好地完成节点分类任务。
- using LLMs for label annotation

However, current annotation methods **primarily rely on LLMs’ ability to understand textual features, without considering the structural relationships between nodes.** 没有考虑结构信息

## 4 Knowledge Organizer

**integration of GNNs and LLM architectures.**

- GNN-centric
- LLM-centric
- GNN+LLM

<img src="./assets/CleanShot 2024-04-12 at 11.05.12@2x.png" alt="CleanShot 2024-04-12 at 11.05.12@2x" style="zoom:50%;" />

### 4.1 GNN-centric Organizer

using structured encoding ability of GNNs for the final organization and refinement of knowledge.

LLM的作用：

- initializers for node features in GNN inputs
- optimizers for the graph structures used by GNNs
- sources of labels for GNN input data

method：

- **TAPE [He et al., 2023]** LLMs are used to generate additional explanatory and predictive features as inputs for the GNN, with the GNN model ultimately producing the final node representations.
- **OFA [Liu et al., 2023a]** LLMs’ versatility is harnessed to encode data from different domains and tasks, enabling GNNs to undergo unified training across various domains and tasks.

### 4.2 LLM-centric Organizer

utilizing LLMs as the core and sole backbone

难点：complexity of transforming graph data into a sequential text format.

method：

- **Chen et al. [2023a]** extract contextual information about a target node using an LLM by constructing the neighbor summary prompt. The output text from this process is then used as a prompt to assist the LLM in tasks related to GRL.

  - <u>*Structural information*</u> is depicted either through the <u>*textual features of adjacent nodes*</u> or through <u>*linguistic descriptions of connectivity relationships*</u> 

    - > 如何用语言描述connectivity relationships？

- **GPT4Graph [Guo et al., 2023].** 

  - the Graph Modeling Language and Graph Markup Language are used to describe graph structure

- **GraphText [Zhao et al., 2023a]**

  - based on tree structures for converting graphs to texts

### 4.3 GNN+LLM Organizer

- GNN-based models, while <u>*adept at structural analysis*</u>, <u>*fall short in processing textual data and interpreting natural language instructions*</u>.
- LLM-based models, despite their <u>*linguistic prowess*</u>, <u>*struggle with precise mathematical calculations and multi-hop logical reasoning.*</u>

the language understanding capabilities of LLMs and the structural analysis proficiency of GNNs.

## 5 Integration Strategies

<img src="./assets/CleanShot 2024-04-12 at 14.10.19@2x.png" alt="CleanShot 2024-04-12 at 14.10.19@2x" style="zoom:50%;" />

### 5.1 Input-level integration

在input stage 融合图结构和文本信息，与llm的input对齐

- 基于llm的：将图结构convert to textual narratives
  - **Chen et al. [2023a]** first aggregating the textual information of nodes within a neighborhood and then integrating this summarized description into the textual input using a prompt format.
  - **InstructGLM [Ye et al., 2023]** integrates diverse hop-level contextual node information with a node sampling strategy into the input of the LLM model.
- 基于GNN的：使用llms forming virtual nodes that  同化 textual information
  - **OFA [Liu et al., 2023a]** using GNNs as the knowledge organizer, incorporates textual information into the graph data in the form of prompting <u>*virtual nodes*</u>. It initializes these virtual nodes with additional task description text, providing not only extra semantic information but also enabling cross-domain multi-task model training integration.

### 5.2 Hidden-level Integration

merging the textual semantic representations encoded by LLMs with the graph information representations encoded by GNNs

- **TAPE [He et al., 2023]** 将原始文本特征、解释性文本特征和预测性文本特征作为GNN的输入。然后融合三个GNN的输出
- cascading [Chandra et al., 2020]
- concatenation [Edwards et al., 2021]

**TODOs：**integration of textual and graph representations

### 5.3 Alignment-based Integration

- 对齐对同一个实体的GNN和LLM的特征表示
- 基于对齐的集成的目标在于<u>*在特定阶段保持每种模态的独特功能，同时同步它们的嵌入空间*</u>。

基于对齐的知识整合包括三个主要类别：

- contrastive alignment
  - **[Brannon et al., 2023]** 将同一节点的图形表示和文本表示视为正例，进行对比学习以实现知识整合。
  - **G2P2 [Wen and Fang, 2023]** 在预训练期间进行多层次对比学习，包括节点-文本、文本-摘要和节点-摘要，从而加强文本和图表示之间的对齐。
- iterative alignment
  - 对于迭代对齐，允许在知识传递的学习过程中节点和图之间进行迭代交互
  - **GLEM [Zhao et al., 2022]** 将一种新型的伪似然变分框架引入到迭代训练过程中，其中E步骤涉及优化LLM，M步骤侧重于训练GNN。
- distillation alignment
  - **GRAD [Mavromatis et al., 2023]** 具体来说，它采用GNN作为教师模型来生成LLM的软标签，从而促进聚合信息的传输。

然而，由于LLM的训练引起的**效率问题**限制了在现实场景中应用对齐融合技术。

## 6 Training Strategies

### 6.1 Model Pre-training

- 对比
- 生成

When incorporating LLMs into GRL, pre-training can also include textual knowledge from language models, and textual pretraining tasks like <u>*network-contextualized masked language modelin*</u>g **[Jin et al., 2023b]** and <u>*context graph prediction*</u> **[Zou et al., 2023].**

- **few studies focusing on injecting graph structure knowledge into LLMs during pre-training.**
  - 在LLM预训练的过程中inject 图结构的知识
  - **InstructGLM [Ye et al., 2023]**：利用self-supervised link prediction task作为辅助训练的任务来让LLM理解图结构
  - 混合GNN和LLM预训练的方法是可行的

### 6.2 Prompt-based Training

大规模的训练的数据都很稀疏， prompt-based training还是个待解决的关键问题

### 6.3 Instruction Tuning

enhancing model performance in few-shot and zero-shot scenarios.

- **InstructGLM [Ye et al., 2023]** directs the LLM to generate responses for various graph learning tasks within a unified language modeling framework. 
- **GraphGPT [Tang et al., 2023]** proposes a two-stage instruction tuning approach for graph learning.
  - Initially, it uses self-supervised tasks to teach the LLM graph structure knowledge. 
  - Then, it applies task-specific tuning to improve the LLM’s performance on downstream tasks, aligning it with graph domain knowledge and specific task requirements.

As research on GRL with LLMs progresses, instruction tuning will play an increasingly crucial role in fine-tuning LLMs.

## 7 Future Directions

#### Generalization of knowledge extractor.

- challenges arise with **graph data lacking rich text**.
- 将LLMs调整为解释非文本图形数据对于GRL的进展至关重要，特别是考虑到现实场景中非文本图形的普遍存在。

#### Effectiveness of knowledge organizer.

- GNNs, Graph Transformers, and LLMs.

how to **design** an effective knowledge organizer for GRL, and a **unified theoretical framework** to analyze the strengths and weaknesses of these various architectures is lacking.

#### Transferability of integration strategies.

- Transferability：不同图的不同的大小、结构、连通性、拓扑结构
  - LLM的泛化行一定程度上可以解决
  - 推进可转移性不仅需要微妙的整合策略，还需要对图领域中知识传递的更深入理解。

#### Adaptability of training strategies.

- 在图数据上关于LLM的预训练和微调技术的研究很少
  - consider LLMs’ methods and structures and how to integrate graph information

## 8 Conclusions