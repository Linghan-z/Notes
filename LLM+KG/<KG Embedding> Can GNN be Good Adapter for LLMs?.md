# Can GNN be Good Adapter for LLMs?

Thus, this paper explores how to utilize LLMs to model TAGs.

> TAG-text-attribute graph (the nodes in graphs have textual features) -> KG

提出==**GraphAdapter**== 利用GNN+LLMs

- The entire framework is trained using auto-regression on node text (next token prediction).
- 训练之后可以针对下游任务进行预训练

KG中的结构信息和节点的文本信息的联系：图可以通过结构邻近性（structural proximity）.来补充节点上的文本属性

- 利用GNN提取KG中的文本信息和结构信息

GNN+LMs的挑战：消息传递机制带来的极大额外计算成本

**==GraphAdapter==** offers several advantages:

- Lightweight
- Language-aware graph pre-training：Using <u>*language to supervise the modeling of graph structur*</u>e, which can help LLMs comprehend <u>*both textual and structural information*</u>.
- Convenient tuning：Once a graph-specific adapter is <u>*pretrained*</u>, it can be fine-tuned for <u>*multiple downstream tasks.*</u>

模型的细节介绍：

- 为了捕获图的数据分布，我们采用节点文本上LLMs的参数高效调整
  - GNN is the tuning parameter,
  - helps reduce the distribution discrepancy between the pre-training corpus and target data.减少预训练语料库和目标数据之间的分布差异
- 只在transformer的最后一层利用GNN adapter
- 此外，我们对来自GNN适配器和LLMs的预测logits执行均值池化，然后优化它们的下一个词预测的最终结果，这可以帮助适配器更多地关注与图相关的token 

**PLMs with Prompts：**Since the last token is used to predict the next token distribution in the pre-training stage, it can naturally combine the inserted prompt information into the original sentence and extract the prompt-related semantics.

## METHOD

<img src="./assets/CleanShot 2024-04-10 at 10.02.14@2x.png" alt="CleanShot 2024-04-10 at 10.02.14@2x" style="zoom:50%;" />

during the pre-training process：

1. GNN models the node structure information
2. integrates the structural information with the corresponding context hidden-states modeled by PLM
3. predicts the next token.

**Align GNN with the language model.**：GNN得到的节点表示与语言模型建模的不同表示不断地结合起来进行推理，整个过程自然地将两者对齐

**Enhance GNN in modeling graph structure.**：在整个预训练阶段，文本数据中的语义信息监督GNN对图的结构信息进行建模

**Better understanding the semantics in TAG.**：GraphAapter can learn how to combine LLM and GNN to model the semantic information on TAG.

### 4.2 Pre-training on TAGs

#### Pipeline of pre-training

- 给定节点i和它的文本信息$\mathbb{S}_𝑖 = {𝑠_{𝑖,0}, ..., 𝑠_{𝑖,𝐿_𝑖} }$
- 使用$\mathbb{S_i}$监督
  - 对于k-th个token，
    - 首先抽取前k-1个tokens$\mathbb{S}_𝑖 = {𝑠_{𝑖,0}, ..., 𝑠_{𝑖,k-1} }$
    - GNN学习第k个节点的结构信息$z_i$
    - 结构信息和前k-1个token的信息结合起来来预测下一个token
    - groundtruth：$s_{i,k}$

#### Structural representation:

- 使用GNN抽取zi
  - massage-passing framework的GNN
  - <img src="./assets/CleanShot 2024-04-10 at 10.26.23@2x.png" alt="CleanShot 2024-04-10 at 10.26.23@2x" style="zoom:50%;" />
  - xi0:初始节点 A：邻接矩阵

#### Context hidden-states.

- 使用预训练的**Transformer** 来encode $S_{i,k}$
  - <img src="./assets/CleanShot 2024-04-10 at 10.34.30@2x.png" alt="CleanShot 2024-04-10 at 10.34.30@2x" style="zoom:50%;" />
  - **Transformer** 预训练且冻结
  - hik是$S_{i,k}$ 的context hidden state
  - in the pretraining stage of PLM, h𝑖,𝑘 is directly used to predict the next token, so h𝑖,𝑘 contains both the context information and a certain of PLMs’ prediction result.

#### Fusion block:

- 融合结构信息和语意信息
  - <img src="./assets/CleanShot 2024-04-10 at 10.37.14@2x.png" alt="CleanShot 2024-04-10 at 10.37.14@2x" style="zoom:50%;" />
  - The Fusion(*) function is trainable with parameters $Θ_{fuse}$ 
  - concat $h_{i,k}$ 和 $z_i$
  - 给MLP

#### Residual connection

- not every token’s prediction requires the graph structure.
- reuse hik
  - 分别计算LM的语意的概率以及结构+语意的概率
  - <img src="./assets/CleanShot 2024-04-10 at 10.46.26@2x.png" alt="CleanShot 2024-04-10 at 10.46.26@2x" style="zoom:50%;" />
  - $\sigma$：softmax

#### Optimization

- cross-entropy loss
  - <img src="./assets/CleanShot 2024-04-10 at 10.51.34@2x.png" alt="CleanShot 2024-04-10 at 10.51.34@2x" style="zoom:50%;" />

#### GNN as Adapter:

In the whole pre-training stage, the GNN <u>*combines*</u> with the frozen LM’s hidden states outputted from the transformer block. The <u>*combined hidden states are then input into the PLM’s prediction head*</u>. Thus, the GNN acts as an adapter, altering the language model’s predictions. Since the hidden states outputted by the transformer block can be pre-processed and stored in advance. Therefore, the entire training process <u>*only requires training the GNN*</u>. Therefore, GraphAdpater can efficiently pre-train based on different scales of PLMs.

### 4.3 Fine-tuning with Prompts

GraphAdapter is pre-trained by token-level semantic understanding tasks

**prompt-aware fine-tuning.**

- 更好地利用learned knowledge of GraphAdapter

  - inserts prompts in textual data to get task-specific sentence embedding of each node.

  - Prompts把下游任务转化为next token prediction

  - given textual data $\mathbb{S_𝑖}$ of node $𝑖$

    1. combine a sequence of tokens with task-specific prompts behind textual data

    - $\mathbb{S}_{i|\mathbb{P}} = [\mathbb{S}_i, \mathbb{P}]$

    2. get its sentence hidden states $h_{i|\mathbb{P}}$ through the transformer of PLM.

    3. The resulting hidden state is then **fused with the node’s structural representation** as node representation in a specific downstream task.

    - <img src="./assets/CleanShot 2024-04-10 at 11.05.27@2x.png" alt="CleanShot 2024-04-10 at 11.05.27@2x" style="zoom:50%;" />

  - This node representation can be used in various tasks.

    - node classification:append a new linear transformation to output the result
      - <img src="./assets/CleanShot 2024-04-10 at 11.07.12@2x.png" alt="CleanShot 2024-04-10 at 11.07.12@2x" style="zoom:50%;" />
      - In fine-tuning stage, the whole parameters$\{\Theta_g, \Theta_{fuse}, \theta_{new}\}$ in GraphAdapter are trainable.

## 5 EXPERIMENT

GNN:GraphSAGE [11]

- **Q1: How well is GraphAdapter in modeling TAGs?** 
  - **A1: GraphAdapter can effectively model TAGs and surpass current state-of-the-art baselines on node classification tasks.**
    - <img src="./assets/CleanShot 2024-04-10 at 13.40.30@2x.png" alt="CleanShot 2024-04-10 at 13.40.30@2x" style="zoom:50%;" />
      1. Frozen LLMs are effective on TAGs.
         - prompts can bring a 0.42% improvement on average for LLM, but they could not improve the performance of LM.
      2. Directly fusing GNN and LLM results in unstable improvements.
         - *GraphAdapter (w/o Pre)* only adds one fusion component to fuse the semantic representation from the LM and structural representation from the GNN.
           - training samples may have an impact on GNNs to understand and effectively incorporate the representations inferred by LLMs with prompts.
      3. GraphAdapter can effectively combine GNN and LLM, surpassing existing state-of-the-art baselines in terms of performance.
- **Q2: Whether GraphAdapter can adapt to other PLMs?** 
  - **A2: GraphAdapter can be effectively pre-trained based on RoB-ERTa, GPT-2, and Llama 2, resulting in performance improvements.**
    - <img src="./assets/CleanShot 2024-04-10 at 13.44.31@2x.png" alt="CleanShot 2024-04-10 at 13.44.31@2x" style="zoom:50%;" />
      - **GraphAdapter is a general and scalable method.**
- **Q3: Are all components comprising GraphAdapter valid?** 
  - **A3: As Table 4 shows, removing any component of GraphAdapter results in performance drops.**
    - <img src="./assets/CleanShot 2024-04-10 at 13.49.51@2x.png" alt="CleanShot 2024-04-10 at 13.49.51@2x" style="zoom:50%;" />
      - removing the residual learning (“w/o Res Label” that is stated in Equation 12) leads to a 1.02% drop (more than removing pre-training), suggesting that training GNNs directly on all text may introduce excessive noise and hurt performance.(残差连接)
- **Q4: What exactly does GraphAdapter’s pre-training learn?** 
  1. **GNN can obtain stronger expressive power through pre-training.**
     - <img src="./assets/CleanShot 2024-04-10 at 13.52.53@2x.png" alt="CleanShot 2024-04-10 at 13.52.53@2x" style="zoom:50%;" />
     - GNNs are training their ability to model the graph structure during pre-training
  2. **Fusion block is learning how to fuse the knowledge from the language model and GNN during pre-training**
     - <img src="./assets/CleanShot 2024-04-10 at 13.53.59@2x.png" alt="CleanShot 2024-04-10 at 13.53.59@2x" style="zoom:50%;" />
  3. **Graph structure is the basis of pre-training.**
     - <img src="./assets/CleanShot 2024-04-10 at 14.00.45@2x.png" alt="CleanShot 2024-04-10 at 14.00.45@2x" style="zoom:50%;" />
       - the MLP-based GraphAdapter shows no significant change before and after pre-training (average improvement of 0.19%), and even decreases in performance on Instagram and Reddit (drops of 0.05% and 0.62% respectively).
- Q5: How efficient is GraphAdapter?

## 6 CONCLUSION

This paper proposes GraphAdapter to harness LLMs for TAGs without fine-tuning. A GNN adapter is trained to reduce LLM next-word errors on node texts. This adapts LLMs for graphs efficiently. Across node classification tasks, GraphAdapter improves accuracy by 5% over baselines. We validate with RoBERTa, GPT-2, and Llama 2, efficiently leveraging LLMs for interconnected text-graph data.
