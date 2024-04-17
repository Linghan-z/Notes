# Graph Language Models

## Method

<img src="./assets/CleanShot 2024-04-16 at 16.23.53@2x.png" alt="CleanShot 2024-04-16 at 16.23.53@2x" style="zoom:50%;" />

提出了Graph language model，早期融合文本和结构信息，解决GNN和LLM对于TAG中的结构和文本信息的语意空间不同的问题

- 修改Transformer中的positional encoding和self-attention，让LM（sequence transformers）转变为graph trasformers，能够处理图信息，并且保留其LM的能力
  - 在LM的self-attention模块中采用non-invasice变换，将LM变成graph transformers（GT），并且保持对之前的LM的参数的兼容
  - 在encoding图的时候
    - LM-like attention模式对每个独立的triplet线性学习文本信息
    - GT-link 注意力模式通过图结构聚合信息
- 对于文本序列可以看作是一种特殊的图，因此GLM可以同时处理文本和图的输入

### 3 Preliminary: Graph Transformers (GT)

<img src="./assets/CleanShot 2024-04-16 at 16.39.45@2x.png" alt="CleanShot 2024-04-16 at 16.39.45@2x" style="zoom:50%;" />

- **Positional Encoding 位置编码**

  - absolute PE：absolute token positions are encoded
  - relative PE：encodes the relative position between pairs of tokens

  GTs需要利用PT来encode 图结构

  - 利用节点之间的跳数定义距离（signed distance）（sigh可以是边的方向）

- Masked Attention 
  - 引入 图的先验，设置一个参数，setting elements of M to **$0$** for pairs of tokens that should be connected, and to **$-\infin$** otherwise.

### 4 Graph Language Model

#### GLM vs. GT

- GTs can offer desired graph priors, but they <u>*lack language understanding.*</u>

By initializing a **GT** with parameters from a compatible LM, we obtain our Graph Language Model (**GLM**)

#### Graph preprocessing

让GLM可以学习graph的信息

- 将三元组转化为Levi graph
  - <img src="./assets/CleanShot 2024-04-16 at 17.14.36@2x.png" alt="CleanShot 2024-04-16 at 17.14.36@2x" style="zoom:50%;" />
    1. replace each edge with a node that contains the relation name as text feature, and connect the new node to the head and tail of the original edge via unlabeled edges, preserving the direction of the original edge.用包含关系名称作为文本特征的节点替换每条边，并通过未标记的边将新节点连接到原始边的头部和尾部，保留原始边的方向。
    2. tokenize each node and split each node into multiple nodes, such that every new node corresponds to a single token 将每个节点标记化并将每个节点拆分为多个节点，使得每个新节点对应一个单独的token
  - 这样可以让通过sequence of tokens的方式表示每个triplet

#### Positional Encodings

- 直接在**同一个三元组**中使用encode the relative position between pairs of tokens的方法（simply considering the triplet as a piece of text, and counting the token distance in this text.）
- 在不同的三元组中，考虑最短路径，但是这一点在LM中是没有的，因此设计了两个方案：a local ($\mathscr{l}$GLM) and a global ($\mathit{g}$GLM) one.
  - 如果用最短路径以错误的方向遍历三元组（For example, cat would see the graph as the following sequence: cat is a animal a is dog a is poodle black.）

#### Local and global GLM

- $\mathscr{l}$GLM
  - <u>*不考虑triplet之间的attention*</u>（attention to any token located beyond the local triplet is set to 0 – and hence does not require PE.）
  - messages can propagate through the graph across multiple layers（For example, the representation of dog is contextualized by the triplets black poodle is a dog and dog is a animal after the first ℓGLM layer. Hence in the second layer, when animal attends to dog, the animal embedding gets impacted by black poodle, even though there is no direct connection from animal to black poodle.）
  - 与GNN里面的信息传播相似

<img src="./assets/CleanShot 2024-04-16 at 17.42.06@2x.png" alt="CleanShot 2024-04-16 at 17.42.06@2x" style="zoom:50%;" />

- $\mathit{g}$GLM
  - global view can have benefits
  - <u>*self-attention can connect any node to every other node*</u>.
  - graph-to-graph (**G2G**) relative position.
  - LM不学习这样的特征，因此初始化为正无穷**$+\infin$**(在LM中正无穷表示很远）

<img src="./assets/CleanShot 2024-04-16 at 17.42.18@2x.png" alt="CleanShot 2024-04-16 at 17.42.18@2x" style="zoom:50%;" />

- 加入文本：

<img src="./assets/CleanShot 2024-04-16 at 17.42.55@2x.png" alt="CleanShot 2024-04-16 at 17.42.55@2x" style="zoom:50%;" />

#### Joint graph and text encoding

- (i) graph-tograph, (ii) text-to-text, (iii) text-to-graph and (iv) graph-to-text.

#### Uni- and Bidirectional LMs

- 添加反向边
- 使用双向的模型

#### T5

## 5 Experiments

### 5.1 Representing and reasoning over Graphs

- **任务：**关系预测

- 模型的输入是ConceptNet的子图，The relation to be predicted is replaced with **<extra_id_0>**.
  - The GLM encodes the graphs as in §4, **producing an embedding for each token**. <u>*A linear classification head gives the final prediction from the mask’s embedding*</u>.
- In a finetuning setting we train the GLM and the classification head jointly.
- order the triplets either randomly (**T5 set**) or alphabetically字母顺序 (**T5 list**)

在长程连接至关重要时评估模型有效性，我们会遮蔽围绕待预测关系的完整子图。被遮蔽的子图大小为 m，其中 m = 0 表示无遮蔽，m = 1 表示遮蔽相邻概念，m = 2 表示遮蔽相邻概念和下一个关系。

在掩盖子图时，我们会掩盖围绕待预测目标的特定大小的完整子图。被掩盖的子图大小由m表示，其中m = 0表示不进行掩盖，m = 1表示掩盖相邻概念，m = 2表示同时掩盖相邻概念和下一个关系，依此类推。形式上，m代表Levi表示中被遮蔽图的半径，在这里应该注意不要与扩展Levi图或普通图表达混淆。我们用不同的屏蔽token替换被屏蔽子图中的每个概念和关系。原则上这使得LM基线能够内部重建该图。

#### Linear probing

只训练the classification head

<img src="./assets/CleanShot 2024-04-16 at 21.26.33@2x.png" alt="CleanShot 2024-04-16 at 21.26.33@2x" style="zoom:50%;" />

- r = 1
  - GLM和LM的唯一区别是LM baselines have an end-of-sentence token，没有这个token要好
- r ≥ 3
  - LM的性能下降，但是GLM可以利用额外的信息，性能提升
  - GLM具有良好的inductive graph biases能力（学习结构信息，相近的更相关，远的就注意力评分低）
- larger m --when larger sub-structures are masked.
  - 表现不佳
- gGLM能够采取的全局视图的优势，比lGLM好

#### Finetuning

- GLMs可以调整参数以更好地匹配新的输入结构
  - 和linear probing 相比有效
- GLMs perform best, while GTs perform the worst.
  - Finally we compare GLMs to models with the <u>*same architecture*</u>, but <u>*random weight*</u> initialization (normal graph transformers).
  - only difference between the two model groups is weight initialization，the **GLMs are initialized from T5**, while the GTs are **randomly** initialized.
- LMs刚开始行，但是r增大的时候与GLM差距变大，m增大的时候差距更大，说明LM具有处理简单的图推理的能力，但是复杂或者图变大就没那么好了
- m ≥ 1，gGLM比lGLM好，说明可以利用长信息

#### Impact of model size

- larger models perform better.

### 5.2 Jointly representing Graph and Text

- **子任务1**执行文本引导的关系分类，其中一些关系可能可以从文本中推断出来，而其他关系可能利用图知识进行预测。
- **子任务2**，模型对预测关系的来源进行分类，即是否可以从文本中推断出来，或者是否需要（额外的）图知识。

For a given text, subgraph, head and tail entity, models will jointly predict the **relation** and the **source**.

- source labels we have 3 classes: <u>*entailed by the text*</u>, *<u>not entailed</u>* and <u>*no-relation*</u>.

receive text and graph data as input.

<img src="./assets/CleanShot 2024-04-16 at 22.00.35@2x.png" alt="CleanShot 2024-04-16 at 22.00.35@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-04-16 at 22.00.53@2x.png" alt="CleanShot 2024-04-16 at 22.00.53@2x" style="zoom:50%;" />

- gGLM performs the best overall, followed by ℓGLM.
- 结果显示，GLM可以有效地推理图形和文本交错输入，尤其是在有限的训练数据情况下。

<img src="./assets/CleanShot 2024-04-16 at 22.01.42@2x.png" alt="CleanShot 2024-04-16 at 22.01.42@2x" style="zoom:50%;" />

- GLMs utilize both text and graph modalities.

<img src="./assets/CleanShot 2024-04-16 at 22.03.33@2x.png" alt="CleanShot 2024-04-16 at 22.03.33@2x" style="zoom:50%;" />

- GLM先学的用text，然后学会利用graph信息

<img src="./assets/CleanShot 2024-04-16 at 22.06.11@2x.png" alt="CleanShot 2024-04-16 at 22.06.11@2x" style="zoom:50%;" />

- 对于文本中包含的三元组，文本比图更具影响力，而其他三元组则相反（参见表9）

## 6 Conclusion

- 提出了图形语言模型（GLM）—— 一个用LM的权重初始化的graph Transformer
  - 像LM一样同时编码graph和triplet，弥补LM和GNN之间的gap
  - GLM可以本地化地推理文本和图形的联合输入，利用并增强每种模态。

## Limitation

- limited to English knowledge graphs
- 不同的语言、domains and tasks
- 最合适的模型

