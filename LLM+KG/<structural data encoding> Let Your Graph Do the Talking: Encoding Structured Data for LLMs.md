# Let Your Graph Do the Talking: Encoding Structured Data for LLMs

## Abstract

将结构化数据编码为序列形式，以供大型语言模型（LLMs）使用？

==**GraphToken**==:learns an encoding function to extend prompts with explicit structured information.

致力于通用结构化数据编码，以用于各种推理任务

## 1. Introduction

- As Kadavath et al. (2022) showed, when LLMs are supplied with new and supporting information, they are capable of adapting their parametric beliefs to effectively incorporate new evidence.
- RAG
- *structured data* - data that has complex dependencies between different, *discrete* parts of the whole.
  - 如：private relational databases, social networks, or molecules

The predominant主流 mode of **encoding structured data for LLMs** is to use various types of **hand-crafted**, **textbased serialization**

- 如：

  - Guo, J., Du, L., and Liu, H. Gpt4graph: Can large language models understand graph structured data? an empirical evaluation and benchmarking. arXiv preprint arXiv:2305.15066, 2023. Cited on page 1.

  - Wang, H., Feng, S., He, T., Tan, Z., Han, X., and Tsvetkov, Y. Can language models solve graph problems in natural language? In NeurIPS, 2023b. Cited on pages 1, 3, and 5.

  - Stechly, K., Marquez, M., and Kambhampati, S. Gpt4 doesn’t know it’s wrong: An analysis of iterative prompting for reasoning problems. arXiv preprint arXiv:2310.12397, 2023. Cited on page 1.

- impose significant decoding complexity for the language model：模型必须在利用信息之前先正确decode并理解结构

- Fatemi, B., Halcrow, J., and Perozzi, B. Talk like a graph: Encoding graphs for large language models. In ICLR, 2024. 表明了结构化数据的纯文本表示对于使用LLMs进行图推理是不足够的————当面临常见的推理任务时，LLMs 无法有效利用结构，这些任务往往可以通过经典图算法轻松回答

==**GraphToken**==：learns an **encoding function** that **generates fine-tuned soft-token prompts** 学习生成微调的soft-token提示的编码函数

- The soft-token prompt extends a textual prompt with explicit **GraphToken encoded structural information**, allowing us to train only a trivial number of GraphToken parameters when compared to the total LLM parameter budget.

**Contributions**

- GraphToken, a novel parameter-efficient encoder for structured data inclusion in LLMs.
- experiments
- demonstration：GraphToken encoder generalizes to both unseen tasks and graphs.

<img src="./assets/CleanShot 2024-03-20 at 13.34.52@2x.png" alt="CleanShot 2024-03-20 at 13.34.52@2x" style="zoom:50%;" />

## 2. Background

### 2.1. Large Language Models

#### Pre-Trained Large Language Models (LLMs):

#### Parameter-Efficient Fine-Tuning:

- **Adapter-based** approaches (Houlsby et al., 2019; He et al., 2021) hold the LLM parameters <u>*frozen*</u> and add new trainable parameters to various parts of the model, with the main differentiating factor between different approaches being where the adapter parameters are added.
- **LoRA** and its variants (Hu et al., 2021; Edalati et al., 2022; Valipour et al., 2022) similarly hold the LLM parameters frozen and add new trainable parameters, however these *<u>trainable parameters are added to the frozen LLM</u>* parameters* such that the fine-tuned LLM is identical in architecture to the initial LLM, but with only those added parameters update.
- **Partial fine-tuning** and **partial masking** approaches (Zhao et al., 2020; Zaken et al., 2021) only fine-tune or mask <u>*a subset of the LLM parameters – no new parameters are introduced*</u>.
- **soft-prompt** approaches (Li & Liang, 2021; Lester et al., 2021) <u>*prepend tokens with learnable parameters to the beginning of the LLM input or to the beginning of every LLM layer*</u> – like adapter-based and LoRA approaches, they hold the actual LLM parameters <u>*frozen*</u>.

本文：encoding structured data input via a **GNN** to produce the LLM soft-prompt.

### 2.2. Graph Encoding with Neural Networks

### 2.3. Graphs and LLMs

while there is a growing body of work in pre-training, finetuning, and prompt-tuning with **GNNs** by themselves (Fang et al., 2023; Liu et al., 2023)

- GNN-based approaches *<u>lack the textual understanding capabilities</u>* that are central to the integration of LLMs with graph learning and reasoning.

## 3. GraphToken

pass structured data to an LLM：

1. encoding it as **lexical tokens** for LLM embedding
   - 可解释性
   - 但是没有明确的方法来合理地组织并描述结构数据】
   - 作者认为a text encoding of structured data prohibits妨碍 **rich**, **concise**, and **expressive** representations.
2. encoding it directly to a **continuous representation via a neural network** – skipping any LLM token embedding.

直接生成directly producing：**使用 GNN 作为编码器为 LLM 输入产生连续表示**

We refer to these <u>*new graph encoder learned soft-tokens in the LLM embedding space*</u> as “==**graph tokens**==.”

To maintain the **reasoning and language capabilities** of the LLM, we **freeze** its parameters and **teach the graph encoder to align its output representations with the LLM embedding space**: we learn only those parameters of the graph encoder during the training process.

在我们的测试中，LLM被prompt来利用图形编码器的输出和关于图形的任务（LLM is prompted with the output of the graph encoder and a task about the graph），例如：‘Does this graph contain a cycle?’ 因此，结果的质量完全取决于**图形编码器如何表示任务答案**以及**LLM如何解释该输出**

### 3.1. Architecture

<img src="./assets/CleanShot 2024-03-20 at 15.00.12@2x.png" alt="CleanShot 2024-03-20 at 15.00.12@2x" style="zoom:50%;" />

At a high level, our model only has **two components**

1. the graph encoder takes a graph as input and outputs a fixed number of token embeddings.
2. These tokens are then prepended to the sequence of initial token embeddings in the prompt for an LLM, which is then decoded to produce an answer as text.

#### Graph Encoder.

GNN 模型的范围从简单的平均方法到具有多头注意力的复杂模型，因此there are a wide variety of graph representations possible.

- Our graph encoder takes the **relational structure of the graph as input**, using some form of **graph positional encoding** 图位置编码 as node features (either learned, Laplacian, or a combination thereof)
- Next, we apply a **GNN** to obtain a **representation of the graph**, which we read out using one of a few different techniques techniques depending on the task.
  - For **graph-level** tasks (e.g., cycle check) we do **global pooling** for readout, <u>*taking the mean or sum of the representations over all of the nodes.*</u>
  - For **node-level** tasks (e.g., node degree) we **separately output the representation of each node**. This can be **optionally   concatenated** with a graph-level pooling. 
  - For **edge-level** tasks (e.g., edge existence), we use **a global representation or the two node-level representations concatenated.**

- exact option for readout used (e.g. mean or sum pooling) is a **hyper-parameter** chosen during model selection.
- 无论用哪种readout方法，表示都通过全链接层dense layer被映射到LLM的token 的空间中

#### LLM

PaLM 2，其他的也行

### 3.2. Training procedure

The training **input** consists of **triples (G, T, A)** 

- where G is a graph structure
- T is a statement or question describing the task (e.g., ‘Does this graph contain a cycle?’ for cycle check) 
- A is the ground truth answer (‘Yes, there exists a cycle in this graph.’).

forward pass：

we compute the **augmented query $Q = \mathcal{E}(G)||\mathcal{T} (T )$,** concatenating the <u>*GraphToken encoding of the graph $\mathcal{E}(G)$*</u> with the <u>*initial embedding of the task textual representation,*</u> $\mathcal{T} (T )$.

We train by optimizing the final LLM perplexity (total loglikelihood), **$\mathcal{L}(A | Q)$**, of the expected answer A with respect to the augmented query, Q.

We minimize this loss, **back-propagating the gradient of $\mathcal{L}$ with respect to $\mathcal{E}(G)$ to the parameters of the GraphToken encoder** – keeping all LLM parameters **frozen**. We use the Lion optimizer (Chen et al., 2023a) with a learning rate α = 0.05.

## 4. Experiments

- R1: GraphToken demonstrates **superior performance** compared to established baselines across a comprehensive range of graph reasoning tasks, including graphlevel, node-level, and edge-level tasks.
- R2: The performance of **different graph convolution architectures** varies across tasks. This highlights the importance of carefully <u>*choosing the right*</u> architecture for the specific graph reasoning problem at hand.
- R3: By **intentionally breaking equivariance**, we enhance GraphToken’s graph reasoning capabilities.



#### Datasets

GraphQA (Fatemi et al., 2024). This dataset presents multiple graph reasoning problems with different difficulty levels. These tasks can be categorized as follows.

- **Graph-level.** node count (counting the number of nodes in a graph), edge count (counting the number of edges in a graph), cycle check (determining whether a graph contains a cycle), and triangle counting (counting the number of triangles in a graph).
- **Node-level.** node degree (calculating the degree of a given node in a graph), and connected nodes (finding all the nodes that are connected to a given node in a graph)
- **Edge-level.** reachability (finding if there is a path from one node to another), edge existence (whether a given edge exists in a graph, and shortest path (finding the length of the shortest path from one node to another).

#### Setting

- We implemented GraphToken in Tensorflow (Abadi et al., 2015) using the **TF-GNN** library (Ferludin et al., 2023).
- The LLM used in our experiments is the instruction-fine-tuned Flan (Chung et al., 2022) checkpoint of PaLM 2 S (Anil et al., 2023).
- Experiments were carried out on Google TPUv3 and TPUv5e

### 4.1. Experiment 1: GraphToken Performance

<img src="./assets/CleanShot 2024-03-20 at 21.10.50@2x.png" alt="CleanShot 2024-03-20 at 21.10.50@2x" style="zoom:50%;" />

### 4.2. Experiment 2: Encoder Design

the **choice of graph encoders** has a significant effect on task performance

#### 4.2.1. CHOICE: GRAPH CONVOLUTION

- **Graph Convolutional Network (GCN):** One of the earliest GNNs, this model does mean pooling of neighbor features, followed by a non-linear transformation. (Kipf & Welling, 2017)
- **Message Passing Neural Network (MPNN):** A generalization of the GCN, this model allows for more flexible aggregation of neighbor features, and has additional nonlinear feature transformations possible. (Gilmer et al., 2017)
- **Graph Isomorphism Network (GIN):** A GNN designed specifically to maximize the expressiveness of the model, with respect to a classic graph isomorphim(同构) test. (Xu et al., 2018)
- **Multi-Head Attention (Graph Transformer):** This GNN adapts transformer style attention, allowing it to learn different ways of passing messages (based on the attention mask). (Dwivedi & Bresson, 2021)
- **Heterogeneous Graph Transformer (HGT)**: Another adoption of transformer style attention (we note that it can be applied to non-heterogeneous graphs as well). (Hu et al., 2020)
- **Linear Aggregation** we also evaluated a family of models which use linear aggregation of features, as this has been shown to work surprisingly well on a number of tasks (Bojchevski et al., 2020).
  - Node Set: This model simply pools all the node features in the graph together. 
  - Edge Set: This model simply pools all the edge features together (edge features are defined as the concatenation of its two nodes’ features).

<img src="./assets/CleanShot 2024-03-20 at 21.21.39@2x.png" alt="CleanShot 2024-03-20 at 21.21.39@2x" style="zoom:50%;" />

- different graph encoder architectures have strengths and weaknesses advantages
  - simple linear GNN models perform quite strongly at their respective **counting tasks** (i.e. NodeSet does well at node count, EdgeSet does well at edge count). 

#### 4.2.2. CHOICE: GNN FEATURES

Recently, positional node encodings (Wang et al., 2022; Dwivedi et al., 2023; Lim et al., 2023) were proposed to enhance the expressivity of GNNs. 另一方面，在分子建模中最近已经表明，非等变编码器可以匹配或超过等变编码器的质量(Wang et al., 2023c).

问题：do GNNs need to be equivariant in order to generalize, especially with extremely powerful decoders, such as LLMs?

We investigate this question by testing the graph reasoning capability of GraphToken with three distinct node featurization settings:

- LPE: Laplacian positional encodings using the normalized Laplacian matrix, as in (Dwivedi et al., 2023).
- IDX: unique identity encoding designed to break the GNN equivariance. 
- LPE+IDX: a concatenation of the above two strategies.

**Setting.**  Node features of dimensionality d = 4 are evaluated for LPE and IDX featurization. Models using LPE+IDX contains node features of size d = 8.

**Result.**

<img src="./assets/CleanShot 2024-03-20 at 21.35.28@2x.png" alt="CleanShot 2024-03-20 at 21.35.28@2x" style="zoom:50%;" />

- These results show that **breaking equivariance surprisingly adds additional capabilities for graph reasoning when powerful decoders are present.**
- 其他发现：
  - **Counting Tasks.** Learned features seem to **provide essential lift 提供了必要的支持** for basic counting tasks (node count, edge count, and node degree) in many encoders.
  - **Combination**. In some very interesting cases of task and encoder, the combination of both types of features **greatly improved model performance** (Fig. 3c). For example, **GCN** and **NodeSet** significantly improved at the **node count task**.
  - **Linear models.** NodeSet (an encoder which does not use the graph edges) generally benefited from spectral features as they added previously unseen information about the graph structure.

#### 4.2.3. PARAMETER USAGE IN GRAPHTOKEN

<img src="./assets/CleanShot 2024-03-20 at 21.42.06@2x.png" alt="CleanShot 2024-03-20 at 21.42.06@2x" style="zoom:50%;" />

- Here ‘body’ refers to the number of parameters **in the graph encoder itself**
- ‘Head’ refers to the parameters **in the transformation layer to the higherdimensional LLM token space**.

我们注意到，这个大小主要由投影层到token空间中参数的总数所决定（大约11M）。

- **attention-based** ones (MHA and HGT) add the most encoder-based parameters.

## 5. Discussion

1. What exactly are the encoders doing？
2. does it generalize?

### 5.1. Graph Encoder Analysis

properties learned by GraphToken’s graph encoders

evaluation steps：

1. 首先在GraphQA的一个任务上训练一个编码器（例如cycle check）
2. 为了评估不同编码器的跨任务泛化能力，我们训练a kNN classifier (or regressor)，使k = 5在
   1. 一个包含8个节点的连通图的详尽集合表示
   2. 一个包含15个节点的树图的详尽集合

因为生成大量的图（例如，大小为8的图形有11117个），并且只在GraphQATrain上进行了训练（1000个实例），因此在这里使用的大多数图都是未见过的。

使用两个GNN encoder的8 node graph的嵌入的 UMAP可视化 (McInnes et al., 2018)

<img src="./assets/CleanShot 2024-03-20 at 21.58.16@2x.png" alt="CleanShot 2024-03-20 at 21.58.16@2x" style="zoom:50%;" />

**Results**

任务：predicting whether a graph is bipartite 二部图

- 有三角形或环形，则肯定不是二部图，因此预测在triangle counting 和 cycle check在这项任务中表现好，实验结果也是这样的
- **generalization from the graph encoders to a new task.**
- <img src="./assets/CleanShot 2024-03-20 at 22.01.40@2x.png" alt="CleanShot 2024-03-20 at 22.01.40@2x" style="zoom:50%;" />
- Overall, there is a significant performance gap between different graph encoders,
- in-distribution learning
  - GraphToken trained on **edge count** performs the best on **edge count** prediction.有趣的是，**node count**在这里表现相当。 这表明图编码器学习了一些适用于许多不同下游任务的通用特征

### 5.2. Future Work

- 设计图卷积算法，最好地支持LLM的图推理任务
- 能否使用prompting over KG的方法提高LLM回答关于数据的问题的能力？能否通过给LLM提供GNN产生的表示来让其回答对应分子的问题
- GraphToken通过破坏等变性来提高性能。这个结果能否指导其他具有非常强解码器模型的问题？
- 我们可以使用LLM来询问GNN，以更好地解释其结果或提供更高质量的答案吗？

## 6. Conclusions

In this work we have studied the structured data encoding problem for LLMs. Our novel method, GraphToken, learns a graph embedding function through the gradients provided by a frozen LLM. GraphToken is especially well suited for projecting structured data into latent ‘prompt space’. It is a parameter-efficient method as it requires only training the graph encoder and does not update LLM parameters. Our extensive experimental analysis across 9 graph reasoning tasks shows that GraphToken greatly improves graph reasoning in LLMs – we observe up to a 73% improvement on the GraphQA benchmark.

There is still much to do! We believe that our approach is fundamental for adapting new structured data sources to LLMs (which are expensive and time consuming to train), and presents a very attractive way of improving fundamental problems in LLMs, including hallucinations, factuality, and freshness.