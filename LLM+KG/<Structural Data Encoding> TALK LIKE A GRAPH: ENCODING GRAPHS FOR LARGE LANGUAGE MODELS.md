# TALK LIKE A GRAPH: ENCODING GRAPHS FOR LARGE LANGUAGE MODELS

## Abstract

LLM performance on graph reasoning tasks varies on three fundamental levels:

1. the graph encoding method
2. the nature of the graph task itself
3. the very structure of the graph considered

## 1 INTRODUCTION

**研究问题：**reasoning over graph-structured data as text for consumption by LLMs.

- 分解成两个问题：
  - graph encoding：LLM的学习表示如何在图任务中发挥作用 how LLM’s learned representations are leveraged in graph tasks.
  - graph prompt engineering：find the most suitable way to get a desired solution to a question from an LLM.

**propose** a new set of **benchmarks** ==GraphQA== for measuring LLM performance <u>*reasoning over graph data*</u>.

**Contributions：**

1. An extensive study of <u>*graph-structure prompting techniques*</u> for use in LLMs. 
2. Insights and best practices for <u>*encoding graphs as text*</u> for use in LLMs. 
3. A new graph <u>*benchmark (GraphQA)*</u> to aid the community in studying the effects of graph structure on LLM prompting further.

## 2 PROMPTING LLMS FOR GRAPH REASONING

### 2.1 PROMPT ENGINEERING

goal is to provide the LLM f with **graph information**, so that it can better reason about question/answer pairs that require access to arbitrarily **structured relational information**. $A = f (G, Q)$ 

- answer $A, (Q ∈ W, A ∈ W ).$
- $W$ :LLMs' token space

**不进行微调**

introduce：

- graph encoding function $g(G)$
- question rephrasing function $q(Q)$ 问题重述

$A = f (g(G), q(Q))$

Our training input D to the graph-based prompt system is a **set of G, Q, S triples**, where G is a graph, Q is a question, and S, S ∈ W , is a solution to Q.

We seek to find a g(.) and q(.) that maximize the expected score from the model (scoref ) of the answers over the training dataset D.

<img src="./assets/CleanShot 2024-03-23 at 20.38.06@2x.png" alt="CleanShot 2024-03-23 at 20.38.06@2x" style="zoom:50%;" />

### 2.2 PROMPTING HEURISTICS启发式

- Zero-shot prompting (ZERO-SHOT)
- Few-shot in-context learning (FEW-SHOT)
- Chain-of-thought (CoT) prompting (COT)
- Zero-shot CoT prompting (ZERO-COT)
- Bag prompting (COT-BAG)：This technique is proposed to improve the performance of LLMs on **graph-related** tasks. It works by appending “Let’s construct a graph with the nodes and edges first” to the graph description.

迭代的prompt在这个task上表现很差，due to cascading errors.



## 3 TALK LIKE A GRAPH: ENCODING GRAPHS VIA TEXT

**graph encoding function g(.)**：maps graph data into tokens for consumption by an LLM.

- R1: LLMs perform poorly on <u>*basic*</u> graph tasks (§3.1).
- R2: The graph encoding function has a *<u>significant impact</u>* on LLM graph reasoning (§3.1).
- R3: <u>*Model capacity*</u> has a significant effect on graph reasoning capabilities of LLMs (§3.4).

**Graph encoding function.** 

1. First, the encoding of nodes in the graph
2. second the encoding of edges between the nodes.

<img src="./assets/CleanShot 2024-03-23 at 20.55.55@2x.png" alt="CleanShot 2024-03-23 at 20.55.55@2x" style="zoom:50%;" />

### 3.1 EXPERIMENT 1: VARYING GRAPH ENCODING FUNCTIONS

measure the performance of pre-trained LLMs on graph tasks: *edge existence, node degree, node count, edge count, connected nodes*, and *cycle check*.

#### 3.1.1 RESULTS

varying graph encoding and prompting techniques.

<img src="./assets/CleanShot 2024-03-23 at 21.00.34@2x.png" alt="CleanShot 2024-03-23 at 21.00.34@2x" style="zoom:50%;" />

- **LLMs perform poorly on basic graph tasks.**
- **Simple prompts are best for simple tasks.**
  - ZERO-COT prompting 在基础graph prompting任务上不如 ZERO-SHOT prompting —— 后者足够了，用不到多跳推理
    - ZERO-COT prompting对于简单问题没有提升，对于复杂问题会有效

- **graph encoding functions have significant impact on LLM reasoning.**
  - This is because different encoder functions <u>*capture different aspects of the graph structure*</u>.
  - incident encoder大多数情况下表现的好
    - This is likely because the incident encoder encodes the graph structure in a way that makes the relevant information more accessible i.e., in close proximity, to the LLM.
- **Integer node encoding improves arithmetic performance.**
  - integer encoding of nodes (e.g., node 0) can improve the performance of LLMs on integer output tasks, such as predicting node degree, node count, and edge count.这是因为LLM的输入和输出在同一空间中，使模型更容易学习两者之间的关系。

select a function carefully and appropriately for the specific task.

### 3.2 EXPERIMENT 2: VARYING PROMPT QUESTIONS

question encoder functions: 

1. the **graph question encoder**：对与图相关的任务进行编码
2. the **application question encoder**：在更实际、日常的背景下解释图问题
   1. edge existence became “assessing friendship existence”, 
   2. node degree became “counting the number of friends for an individual”, 
   3. node count became “counting the number of people mentioned”, 
   4. edge count became “counting the number of friendships mentioned”, 
   5. connected nodes became “listing friends”.

<img src="./assets/CleanShot 2024-03-24 at 10.39.00@2x.png" alt="CleanShot 2024-03-24 at 10.39.00@2x" style="zoom:50%;" />

- the **application encoder** outperforms the graph encoding on almost all tasks
- 结论：**it becomes important to translate a given task into more ==contextually meaningful textual information== when employing LLMs for inference.**

### 3.3 EXPERIMENT 3: MULTIPLE RELATION ENCODING

<img src="./assets/CleanShot 2024-03-24 at 10.41.51@2x.png" alt="CleanShot 2024-03-24 at 10.41.51@2x" style="zoom:50%;" />

- using multiple words to represent relationships did not hurt LLM performance and even improved it in some cases.
- multiple relation => 有更多的信息来让LLM解决问题

### 3.4 EXPERIMENT 4: MODEL CAPACITY AND GRAPH REASONING ABILITY

<img src="./assets/CleanShot 2024-03-24 at 10.43.27@2x.png" alt="CleanShot 2024-03-24 at 10.43.27@2x" style="zoom:50%;" />

- **Model capacity** has a significant effect on the graph reasoning ability of an LLM
  - larger model is generally better at graph reasoning tasks.

### 3.5 EXPERIMENT 5: REASONING IN THE ABSENCE OF EDGES 在没有边的情况下推理

- information that is not explicitly mentioned in the output of the graph encoding function.
- 结果：**LLMs lack a global model of a graph.**

## 4 DOES THE STRUCTURE OF THE GRAPH MATTER FOR THE LLM?

<img src="./assets/CleanShot 2024-03-24 at 10.47.15@2x.png" alt="CleanShot 2024-03-24 at 10.47.15@2x" style="zoom:50%;" />

### 4.1 RANDOM GRAPH GENERATION 随机图生成

- Cover a wide range of properties. 涵盖广泛的属性范围。
  - 比如：Erdős-Rényi graph：稀疏且具有较小的平均度数，Barabási-Albert graph：密集且具有幂律度分布。
- Avoid bias in graph problem evaluation.
  - 图问题的难度可能会因图的属性而有所不同，因此我们使用多样化的图来避免偏差
- Provide realistic benchmarks. 提供现实的基准。

### 4.2 RESULTS ON RANDOM GRAPH GENERATORS 

<img src="./assets/CleanShot 2024-03-24 at 10.53.40@2x.png" alt="CleanShot 2024-03-24 at 10.53.40@2x" style="zoom:50%;" />

- Graph structure has a **significant impact** on the LLM’s performance.
  - 这是因为LLM<u>*对具有循环的图具有强烈的先验偏好*</u>（cycle check 91.7----5.9）
  - 作为另一个例子，在边缘存在任务上，LLM 在路径图上实现了 60.0% 的准确率，这些图中两个节点之间不太可能有边，并且在完全图上实现了 19.8% 的准确率，这些图中所有节点对之间都有边。这表明 LLM 具有一个先验假设，*<u>即图中的两个节点更可能是断开连接的</u>*。
- 图编码函数中的干扰性语句会影响LLM的性能
  - The accuracy of *node degree*, *node count*, and *connected nodes* tasks is highest for <u>*star*</u> and <u>*path*</u> graphs.
    - 因为有更少的边 => encoding更短
  - complete graphs 性能最差，因为干扰项多
- Adding out-of-distribution few-shot examples helped the LLM.

**summary：**The performance of large language models (LLMs) on graph tasks is significantly impacted by the graph structure and the distracting statements in the graph encoding function. Graphs with fewer edges and less complex encodings tend to perform better on most tasks. Adding few-shot examples, even if they are out-of-distribution, can help the LLM to perform better on most tasks.

## 5 RELATED WORK

- In-context learning.
- Text-based reasoning with LLMs.
- Knowledge-Augmented LLMs.
- Reasoning on graphs using LLMs.
- Present work.

## 6 CONCLUSIONS

In this work, we have presented the first comprehensive study of **encoding graph-structured data as text** for consumption by LLMs. We show that LLM performance on graph reasoning tasks **varies on three fundamental levels**: 

1. the graph encoding method
2. the nature of the graph task itself
3. the very structure of the graph considered. 

These novel results provide valuable insight on strategies for encoding graphs as text – which can boost performance on graph reasoning tasks inside LLMs by 4.8% to 61.8%. We believe that this is a fruitful avenue for further investigation, and hope that our GraphQA benchmark tasks inspire additional work in the area.
