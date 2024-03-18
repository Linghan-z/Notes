# Making Large Language Models Perform Better in Knowledge Graph Completion

> 这篇文章准备粗读一下，只做了一个三元组的分类，利用的策略概括一下就是把图谱的结构的embedding映射然后放在prompt的前面作为一个前缀，通过微调让LLM学习到图谱的结构信息
>
> 重点是对于图谱的**结构信息**的处理

1. first transfer the existing LLM paradigms to structural-aware settings and further propose a **kn**owledge **p**refix **a**dapter (**KoPA**)
2. KoPA employs **structural embedding pre-training** to capture the structural information of entities and relations in the KG.
3. KoPA **informs the LLMs of the knowledge prefix adapter which projects the structural embeddings into the textual space and obtains virtual knowledge tokens as a prefix of the input prompt**

#### embedding-based KGC

基于嵌入的方法[4, 43, 46, 56]旨在将知识图谱中的实体和关系嵌入到一个或多个连续表示空间中。这些方法充分利用了知识图谱中的结构信息，通过设计良好的评分函数来建模三元组可信度，并以自监督方式学习实体/关系嵌入，其中应用了负采样[4]。此外，根据评分函数的设计，基于嵌入的方法可以分为三个子类别：

1. (1) 基于平移的方法如TransE [4]和RotatE [43]
2. [(2) 张量分解方法如DistMult [56]和ComplEx [46]
3. [(3) 基于神经网络的方法如ConvE [38]。

基于嵌入的知识图谱补全（KGC）方法学习了用于三元组区分性能力但忽略了知识图谱中文本信息方面表征。

#### PLM-based KGC

此外，基于PLM的方法将KGC视为文本任务，通过微调预训练语言模型（如BERT [12]）来考虑。实体和关系的简短文本描述被组织成输入序列，并由PLMs编码。KG-BERT [58]是第一个将KGC建模为二元文本分类任务的基于PLM的方法。后续如MTL-KGC [21]和StAR [48]通过引入更多训练任务（如关系分类和三元组排序）以及更复杂的三元组编码策略进一步改进了KG-BERT。PKGC [28]利用手动提示模板捕获三元组语义。其他方法如KGT5 [37]和KG-S2S [7]在使用类似T5[35]这样的编码器-解码器PLMs进行序列到序列范式中对生成式KGC[61]迈出了一步。基于PLM的方法利用了PLM的强大功能，但将训练过程转化为基于文本学习，难以捕捉知识图谱中复杂结构信息。



### Notations

LLMs serves as a text decoder

The input textual sequence S of the model M consists of several parts: the **instruction prompt I**, **the triple prompt X**, and **the optional auxiliary demonstration prompt U**.

The triple prompt X contains the **textual information** about the triples that need to be processed, which can be denoted as:

<img src="./assets/CleanShot 2024-03-18 at 15.11.51@2x.png" alt="CleanShot 2024-03-18 at 15.11.51@2x" style="zoom:50%;" />

- D is the description set of each entity and relation. We denote D (𝑒), D (𝑟 ) as the short textual description of each entity 𝑒 ∈ E and each relation 𝑟 ∈ R

objective：**triple classification**

### 3.3 Instruction Tuning Approach

how to incorporate the KG information into IT approaches.

#### 3.3.1 vanilla instruction tuning

To train the model M, the input sequence is organized as $S𝑖𝑡 = I𝑖𝑡 ⊕ X ⊕ A𝑖𝑡$ . where $A𝑖𝑡$ is the predicted answer of the training data. The model $M $ is fine-tuned with the next word prediction task [67] which is a universal approach to training LLMs. The training objective can be formulated as:

<img src="./assets/CleanShot 2024-03-18 at 15.31.57@2x.png" alt="CleanShot 2024-03-18 at 15.31.57@2x" style="zoom:50%;" />

- where 𝑠𝑖 (𝑖 = 1, 2, . . . , |S𝑖𝑡 |) represents the textual tokens of the input sequence S𝑖𝑡

In the inference stage, the model M is employed to predict the answer A𝑖𝑡 of the test data like Equation 2. 

<img src="./assets/CleanShot 2024-03-18 at 15.32.55@2x.png" alt="CleanShot 2024-03-18 at 15.32.55@2x" style="zoom:50%;" />

- input sequence S𝑧𝑠𝑟 .
- I𝑧𝑠𝑟 is the instruction template for ZSR

Besides, negative sampling [28] is also applied as training KG only consists of positve triples.

**vanilla it的缺点：**Vanilla IT only fine-tunes the LLM to learn the knowledge in the single triple to discriminate. Such an approach makes it difficult to fully utilize the rich semantics present in a KG and the model performance is limited

#### 3.3.2 Structural-aware Instruction Tuning.

**local structural information of the entities is added into the input sequence in the form of neighborhood triples.**

To incorporate such KG information during the finetuning stage, we achieve this goal by adding the neighborhood descriptions of the input triple.

Specifically, we can sample the neighborhoods of the head ℎ and tail 𝑡 and put the textual descriptions of neighborhood triples in the demonstration prompt **U𝑖𝑡** .

<img src="./assets/CleanShot 2024-03-18 at 15.37.10@2x.png" alt="CleanShot 2024-03-18 at 15.37.10@2x" style="zoom:50%;" />

## 4 KNOWLEDGE PREFIX ADAPTER FOR LLM-BASED KGC

However, **representing the KG structural information in the form of text is not a good choice**, which may bring in more invalid or redundant information to the prompt.

问题：

1. 长上下文影响能力
2. 难找到KG结构中的对于triple classification 关键的信息

**K**n**o**wledge **P**refix **A**dapter (**KoPA** for short)

<img src="./assets/CleanShot 2024-03-18 at 15.44.12@2x.png" alt="CleanShot 2024-03-18 at 15.44.12@2x" style="zoom:50%;" />

1. **extract the structural information of entities and relations from the KG through structural embedding pre-training**
2. **inject this structural information through a structural prefix adapter into the input sequence $\mathcal{S}$**
   1. **The LLM $\mathcal{M}$ is further fine-tuned with the structural-injected sequence.**

### 4.1 Structural Embedding Pre-training

KoPA extracts the structural information of the entities and relations by **self-supervised structural embedding pre-training**

For each entity 𝑒 ∈ E and each relation 𝑟 ∈ R, we learn a structural embedding $𝒆 ∈ \mathbb{R}^{𝑑_𝑒}$ , $𝒓 ∈ \mathbb{R}^{𝑑_𝑟}$ respectively, where 𝑑𝑒, 𝑑𝑟 are the embedding dimensions.

We encode the KG structural information in the embeddings and **further adapt them into the textual representation space of LLMs**.



score function F (ℎ, 𝑟, 𝑡) to measure the plausibility of the triple (ℎ, 𝑟, 𝑡).

self-supervised pre-training objective by negative sampling:

<img src="./assets/CleanShot 2024-03-18 at 16.04.10@2x.png" alt="CleanShot 2024-03-18 at 16.04.10@2x" style="zoom:50%;" />

where 𝛾 is the margin, 𝜎 is the sigmoid activation function and (ℎ′ 𝑖,𝑟′ 𝑖,𝑡′ 𝑖 )(𝑖 = 1, 2, . . . , 𝐾) are 𝐾 negative samples [4] of (ℎ, 𝑟, 𝑡). The weight 𝑝𝑖 is the self-adversarial weights proposed in RotatE.



By minimizing such a pre-training loss, the structural embeddings of each entity and relation are optimized to fit all its relative triples thus the KG structural information such as subgraph structure and relational patterns is captured in the embeddings.这种方法已被证明在许多基于嵌入的KGC方法中是有效的[4, 43, 46, 56]，在早期也被称为分布式表示[17]。

### 4.2 Knowledge Prefix Adapter

After structural embedding pre-training, we could obtain the structural embeddings (𝒉, 𝒓, 𝒕) of a triple (ℎ, 𝑟, 𝑡) where the KG structural information is encoded in.

结构的embedding是在与LLM的文本表示的语意空间不同的语意空间中学习的，因此LLM不能直接理解，**因此用knowledge prefix adapter$\mathcal{P}$来把结构的embedding映射到textual token representation space of M**

Specifically speaking, the structural embeddings are converted to several virtual knowledge tokens K by P:

<img src="./assets/CleanShot 2024-03-18 at 16.14.52@2x.png" alt="CleanShot 2024-03-18 at 16.14.52@2x" style="zoom:50%;" />

In practice, the adapter P would be a simple projection layer【MiniGPT-4: Enhancing Vision-Language Understanding with Advanced Large Language Models.】

Then we put K in the front of the original input sequence S serving as a prefix of the instruction and triple prompt $S_{𝑘𝑝𝑎} = K ⊕ I_{𝑖𝑡} ⊕ X$  这样，由于**仅解码器LLM中的单向注意力**，所有以下文本标记都可以看到前缀K，通过这样做，文本标记可以单向关注输入三元组的结构嵌入。这种结构感知提示将在微调和推理期间使用。

**During training**：

- froze the pre-trained structural embeddings
- The adapter is optimized to learn the mapping from structural knowledge toward textual representation and will have the generalization to new triples in the inference stage, which will benefit the textual description and provide the triple information from another perspective to make enhanced predictions.

### 4.3 Complexity Analysis

<img src="./assets/CleanShot 2024-03-18 at 16.22.10@2x.png" alt="CleanShot 2024-03-18 at 16.22.10@2x" style="zoom:50%;" />

- length of virtual tokens generated by the structural prefix adapter is fixed to 3 for head/relation / tail respectively.
- ZSR（zero-shot reasoning）

## 5 EXPERIMENTS

#### dataset

<img src="./assets/CleanShot 2024-03-18 at 16.25.09@2x.png" alt="CleanShot 2024-03-18 at 16.25.09@2x" style="zoom:50%;" />

#### settings

- **For embedding-based KGC methods**:we reproduce the results with OpenKE we set the embedding dimension 𝑑𝑒 = 𝑑𝑟 = 512 and sample 𝐾 = 32 negative samples during training. The margin 𝛾 is tuned among {0, 4, 6, 8, 12}. After training KGC models, we search for the best classification score threshold on the validation set for test data following the traditional setting
- **For PLM-based methods**, the backbone model for PLM-based KGC methods is BERT.We **fine-tune the KG-BERT** according to the official code implementation
- **For all LLM-based methods**, we employ Alpaca-7B [44] as the LLM backbone.

#### main result

<img src="./assets/CleanShot 2024-03-18 at 16.25.23@2x.png" alt="CleanShot 2024-03-18 at 16.25.23@2x" style="zoom:50%;" />

#### transferbility

<img src="./assets/CleanShot 2024-03-18 at 16.25.59@2x.png" alt="CleanShot 2024-03-18 at 16.25.59@2x" style="zoom:50%;" />

#### ablation

<img src="./assets/CleanShot 2024-03-18 at 16.27.22@2x.png" alt="CleanShot 2024-03-18 at 16.27.22@2x" style="zoom:50%;" />

- two part ablation study
  - The first part is designed to verify the **effectiveness of structural embedding**
    - removing the structural embeddings or replacing them with random initialized embeddings both lead to *performance decline*
    - the model is *compatible with different types of structural embeddings*.
      - However, the performance gain depends on whether the embedding was originally powerful in the triple classification task or not.
      - TransE [4] 和 RotatE [43] 是比 DistMult [56] 和 ComplEx [46] 更好的基于嵌入的知识图谱模型。这表明语义丰富的结构信息是性能提升的关键，而 KoPA 充分利用了它。
    - 
  - the second part is designed to verify the **effectiveness of prefix adapter**.
    - putting the virtual knowledge tokens generated by the adapter **in the middle (infix)** or **in the last (suffix)** of the input sequence will also *decrease the performance*.
    - **putting tokens in the front of the sequence will make all the text pay attention to them as LLMs are usually decoder-only architectures with unidirectional self-attention.**
      - the LLM can make a better decision with the structural embeddings that fully interact with the text.