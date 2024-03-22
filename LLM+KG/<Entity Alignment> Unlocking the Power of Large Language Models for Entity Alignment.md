# Unlocking the Power of Large Language Models for Entity Alignment

## Abstract

传统的EA方法主要是 comparing entity embeddings，受限：1. KG data 2. capabilities of the representation learning techniques

提出==**ChatEA**==

- 解决KG data的限制的问题：KG-code translation module 将KG的结构化的数据转化为自然语言
- 解决对于entity embedding comparisons的依赖：2-stage EA 策略，对话形式利用多步推理

## 1 Introduction

传统的EA方法主要是 comparing entity embeddings， knowledge representation learning **(KRL)** techniques

- 通过entity embedding学习KG的拓扑结构和语意

  - **缺点：**未能纳入实体的外部世界知识；KLR也是黑盒比较实体相似度..
  - 特别是在对齐高度异构的知识图谱对时，基于KRL的方法**难以捕捉知识图谱之间复杂的相关性**

- ==**ChatEA**==：旨在通过利用LLMs的广泛背景知识和推理能力来增强基于KRL的EA方法

  <img src="../../../Library/Application Support/CleanShot/media/media_w1oKSYNUtl/CleanShot 2024-03-13 at 16.26.54@2x.png" alt="CleanShot 2024-03-13 at 16.26.54@2x" style="zoom:50%;" />

  - Chatea在特征预处理阶段集成了基于KRL的EA方法，以帮助LLMS后续选择候选实体
  - **克服输入的图谱的数据的限制**，ChatEA首先集成了一个KG-Code translation模块，将KG转化为Code的形式，考虑实体定义对LLMs理解图结构KG数据的影响，促进了利用LLMs的背景知识生成实体描述
    - (Yang et al., 2024) If LLM Is the Wizard, Then Code Is the Wand: A Survey on How Code Empowers Large Language Models to Serve as Intelligent Agents
  - **克服EA对比较实体嵌入的过度依赖并提高推理透明度**，2-stage EA 策略，对话形式利用多步推理
    - candidate collecting stage：在候选收集阶段，比较早期特征预处理阶段得到的嵌入来识别潜在实体
    - reasoning and rethinking stage：全面考虑名称、结构、实体描述和时间信息来评估实体对之间的一致性可能性，然后决定是否扩大搜索范围并继续后续迭代

- 数据集：
  - DBP15K(EN-FR) and DBP-WIKI
  - ICEWS-WIKI and ICEWS-YAGO：高度异构，获取KG间相关性复杂

- contributions：
  - 解决KRL的EA的方法的缺陷
  - 设计ChatEA
  - 实验

## 2 Preliminaries and Related Works

### 2.1 Preliminaries

- KG、TKG：$(e_{head}, r, e_{tail}, t)$
- Entity alignment：determine the identical entity set $S = (ei, ej)|ei ∈ E1, ej ∈ E2$

### 2.2 Related Works

**translation-based**:MTransE (Chen et al., 2017), BootEA (Sun et al., 2018), and AlignE (Sun et al., 2018), founded on TransE’s framework (Bordes et al., 2013), excel in knowledge representations.

**GNN-based**:

- GCN (Kipf and Welling, 2016)——通过聚合邻域信息生成实体嵌入向量，标志着在EA方面取得了显著进展
- 使用GCN 结构信息和实体embedding：GCN-Align (Wang et al., 2018), RDGCN (Chen et al., 2022), and Dual-AMN (Mao et al., 2021)
- 加入时序信息：TEA-GNN (Xu et al., 2021), TREA (Xu et al., 2022), and STEA (Cai et al., 2022)

**other methods**:

- 利用辅助信息解决KG中的异构性   Fualign (Wang et al., 2023), Simple-HHEA (Jiang et al., 2023a), and BERT-INT (Tang et al., 2020)

## 3 Method

<img src="./assets/CleanShot 2024-03-19 at 17.17.55@2x.png" alt="CleanShot 2024-03-19 at 17.17.55@2x" style="zoom:50%;" />

### 3.1 Overview of the ChatEA Framework

围绕三个目标设计ChatEA的架构

1. **O1:利用基于KRL的方法作为基础**：同时规避其对实体嵌入相似性比较的过度依赖
   - 利用knowledge representation learning KRL的方法学习实体的特征：名称、结构、时间属性，**在候选实体选择方面辅助LLM**
2. **O2:理解KG并在利用LLM中的知识增强**：让LLM有效地理解Kg并利用LLM的内部的知识来增强EA任务
   - 通过类和函数，然后采用LLMs进行描述生成，从而将知识图谱与LLM的背景知识联系起来。将KG转化为code格式。
3. **O3:利用LLMs的推理能力增强EA**：
   - two-stage EA strategy：entity embedding来选择候选实体，然后利用LLMs，以对话的形式来迭代地推理和重思考目标和候选集合的对齐概率

### 3.2 Entity Feature Pre-processing 实体特征预处理（O1）

- entity information：Simple-HHEA (Jiang et al., 2023a)
- 实体名称语意embedding：BERT，通过feature whitening 降维(Su et al., 2021).
- 时序表示：Time2Vec (Goel et al., 2020)
- 结构信息：有偏随机游走(Wang et al., 2023),这种方法在精确的一跳和多跳关系分析中，最佳地平衡了BFS和DFS技术。

这种多视图预处理策略通过**边际排名损失**进行训练和**跨领域相似性局部缩放（CSLS）**（Conneau等，2017年）用于相似度测量，帮助LLMs在随后选择候选实体时。

### 3.3 KG Input and Understanding in LLMs（O2）

#### 3.3.1 Understanding Knowledge Graphs

**KG-Code translation module**

python-style class，5 functions：这些函数专门设计用于将实体属性转换为独特的数据结构和随后的访问

- \__init__()
- get_neighbors()
- get_relations()
- get_temporal()

#### 3.3.2 Activating LLM’s Inherent Knowledge 

- get_description() ：获取LLMs内部的对于实体的详细的描述

### 3.4 Two-Stage EA Strategy in ChatEA（O3）

#### 3.4.1 Stage 1: Candidate Collecting

利用从预处理中获得的实体嵌入来过滤候选实体

- Cross-Domain Local Scaling (CSLS) metric：度量相似性，选择候选实体
- 在第一个迭代，只选择最相似的实体，在后续的迭代会增加

#### 3.4.2 Stage 2: Reasoning and Rethinking

<img src="./assets/CleanShot 2024-03-13 at 18.16.00@2x.png" alt="CleanShot 2024-03-13 at 18.16.00@2x" style="zoom:50%;" />

利用KG-Code translation模块

以对话的形式对每个候选实体与目标实体的多维度详细评估

- **reasoning：**计算对齐分数（从实体名称、结构、时序、llm生成的实体描述的角度）
- **rethink：**重新思考获得的结果
  - 分数达到threshold -> ok了
  - otherwise：增加候选

## 4 Experiments

- **RQ1: Whether ChatEA overcomes the current EA limitations?**
- **RQ2: What is the effectiveness of ChatEA’s each component?**
- **RQ3: Does the ChatEA framework successfully balance accuracy and efficiency in EA?**

### 4.1 Experiment Settings

#### 4.1.1 dataset

<img src="./assets/CleanShot 2024-03-13 at 18.24.25@2x.png" alt="CleanShot 2024-03-13 at 18.24.25@2x" style="zoom:50%;" />

- DBP15K(EN-FR) and DBP-WIKI (Sun et al., 2020)：两个简单的实体对齐数据集，KG对结构相似、实体数量相等，结构特征也相似（事实数量、密度）
- ICEWS-WIKI and ICEWS-YAGO (Jiang et al., 2023a)：两个复杂的EA数据集，异质（实体数量、结构特征）

#### 4.1.2 Baselines

- KRL：MTransE (Chen et al., 2017) AlignE (Sun et al., 2018), and BootEA (Sun et al., 2018)
- GNN：GCN-Align (Wang et al., 2018), RDGCN (Chen et al., 2022), TREA (Xu et al., 2022), TEA-GNN (Xu et al., 2021), STEA (Cai et al., 2022), Dual-AMN (Mao et al., 2021),
- other：BERT-INT (Devlin et al., 2018) and FuAlign (Wang et al., 2023)

#### 4.1.3 Model Configuration

LLM：llama2-70bchat

#### 4.1.4 Initial Feature Setup

在文本特征提取之后，我们使用带有白化策略的BERT来获得初始名称嵌入

#### 4.1.5 Evaluation Metrics

- Hits@k
- Mean Reciprocal Rank (MRR)反映正确结果的平均倒排名

Hits@k 和 MRR 中较高的值表明 EA 的性能更优秀。

### 4.2 Main Experiment Results

<img src="./assets/CleanShot 2024-03-13 at 18.55.12@2x.png" alt="CleanShot 2024-03-13 at 18.55.12@2x" style="zoom:50%;" />

尤其是基于GNN的方法在面对高度异质的KG时暴露出其局限性，其根本问题在于它们对输入KG数据的依赖，缺乏上下文信息的广度，以及KRL方法不具备处理这种复杂性的约束

**ChatEA**不仅丰富了实体描述与广泛的背景知识，还引入了创新的两阶段EA策略。这种方法显著减少了对输入KG数据的依赖，并解决了对实体嵌入比较过度依赖的问题。

### 4.3 Ablation Study

#### 4.3.1 Effectiveness of Each Component

<img src="./assets/CleanShot 2024-03-13 at 19.14.29@2x.png" alt="CleanShot 2024-03-13 at 19.14.29@2x" style="zoom:50%;" />

- ChatEA (w/o llm) 只用entity embedding
- ChatEA (w/o code) 不使用code，直接给llm实体名和元组
- ChatEA (w/o desc) 不用LLm的实体描述

#### 4.3.2 Performance with Different LLMs

<img src="./assets/CleanShot 2024-03-13 at 19.19.09@2x.png" alt="CleanShot 2024-03-13 at 19.19.09@2x" style="zoom:50%;" />

#### 4.3.3 Influence of Entity Embeddings

<img src="./assets/CleanShot 2024-03-13 at 19.22.11@2x.png" alt="CleanShot 2024-03-13 at 19.22.11@2x" style="zoom:50%;" />

- 在entity embedding dimension中加入噪声（0%～80%）
- 对比了只用embedding的方法
- 结果：
  - 单纯基于表征学习的SIMPLE-HHEA，随着噪声水平的提高，其性能会急剧下降
  - ChatEI可以减轻embedding质量下降的影响
    - （ChatEA 主要利用实体嵌入比较作为候选集合的手段。在此基础上，它利用 LLM 的推理能力进行次要推断，整合来自知识图谱和上下文知识的信息）

### 4.4 Case Study

ChatEA 可以通过显式推理过程改进实体嵌入比较的对齐结果

- Prompt：

<img src="./assets/CleanShot 2024-03-13 at 19.28.29@2x.png" alt="CleanShot 2024-03-13 at 19.28.29@2x" style="zoom:50%;" />

- Output：

  <img src="./assets/CleanShot 2024-03-13 at 19.28.45@2x.png" alt="CleanShot 2024-03-13 at 19.28.45@2x" style="zoom:50%;" />

### 4.5 Efficiency Analysis

<img src="./assets/CleanShot 2024-03-13 at 19.33.44@2x.png" alt="CleanShot 2024-03-13 at 19.33.44@2x" style="zoom:50%;" />

- 在实体特征预处理过程表现良好的情况下，ChatEA往往会更快地收敛，从而更好地利用资源并提高效率
  - （简单数据集效率高，复杂数据集需要对比更多的候选）--> 平衡效率和准确性

<img src="./assets/CleanShot 2024-03-13 at 19.37.02@2x.png" alt="CleanShot 2024-03-13 at 19.37.02@2x" style="zoom:50%;" />

## 5 Conclusion

在这篇论文中，我们专注于利用LLMs的能力进行EA，从而开发了ChatEA。这一创新框架旨在解决三个关键挑战：（1）增强LLMs解释和理解KGs的能力，（2）利用LLMs内在知识实现更有效的EA，以及（3）提高LLMs在EA环境中的效率。我们进行了全面的实验，在四个代表性数据集上进行了测试，突显出ChatEA尤其在需要高精度EA应用方面的优越性。这些发现进一步阐明了LLMs在探索型任务中对EA任务具有重要潜力。

## 6 Limitations

- 资源消耗
- LLMs效率
  - 对于准确率要求没有那么高的情况，LLMs的效率低，因此不适用
  - 仍有改进的空间，例如模型蒸馏
- 小规模模型中的性能约束
  - 应用于参数规模较小的模型时，其性能明显受限
  - 未来：整合稀疏微调（SFT）等技术，以优化性能而不依赖于大规模模型















