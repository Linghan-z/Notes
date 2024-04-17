# Language is All a Graph Needs

使用语言描述图的多尺度几何结构，然后微调一个LLM来执行图任务，从而实现生成式图学习

代码：https://github.com/agiresearch/InstructGLM

Framework：

<img src="./assets/CleanShot 2024-04-17 at 14.31.54@2x.png" alt="CleanShot 2024-04-17 at 14.31.54@2x" style="zoom:50%;" />

使用自然语言描述图结构，比GNN的优点：

1. Flexibility.
2. Scalability.
3. Compatibility.

系统地运用自然语言根据我们的提示描述图的拓扑结构，使得图的结构清晰直观地呈现给LLM，而无需针对图设计复杂的流程

<u>*Transformer和GNN之间缺乏解耦，导致需要训练多个模型并产生显著的计算开销。*</u>

## InstructGLM

<img src="./assets/CleanShot 2024-04-17 at 15.02.17@2x.png" alt="CleanShot 2024-04-17 at 15.02.17@2x" style="zoom:50%;" />

**Prompt Designing**：

1. 在prompt中，关于中心节点的邻居信息的最大跳数是多少？
2. 提示中是否包括元节点特征或边特征？
3. 对于多跳的节点，是否应该包含中间的信息？

<img src="./assets/CleanShot 2024-04-17 at 15.21.10@2x.png" alt="CleanShot 2024-04-17 at 15.21.10@2x" style="zoom:50%;" />

通过引入链接预测辅助任务可以增强模型对图的理解

## 实验

<img src="./assets/CleanShot 2024-04-17 at 15.32.54@2x.png" alt="CleanShot 2024-04-17 at 15.32.54@2x" style="zoom:50%;" />

单模型最先进的性能，超越了所有三个数据集中的所有单图学习者，包括代表性的GNN模型和图transformer模型，这表明大语言模型有望成为图学习的新基础模型。

### 4.3 Ablation Study

- **Structure-FreeTuning** indicates fine-tuning the model on titles and abstracts of the nodes, 
- **1-hop** and **Multi-hop** mean that we utilize prompts that merely include information from 1-hop neighbors and prompts that include information from neighbors with higher hop levels, respectively.

<img src="./assets/CleanShot 2024-04-17 at 15.37.48@2x.png" alt="CleanShot 2024-04-17 at 15.37.48@2x" style="zoom:50%;" />

## 5 Conclusions and Future Work

represent graph structure via natural language description and then further perform instruction-tuning on generative LLMs for graph learning tasks

Future works：

1. Leveraging LLMs to generate improved features
   1. 只用了图谱中的信息，可以增强信信息
   2. 利用CoT、structure information summary以及更多的data augmentation技术
2. Enhancing InstructGLM with knowledge distillation and iterative training frameworks
   1. 与GAN、GLEM集成
   2. 利用现成的GNN进行知识蒸馏
3. Deploying InstructGLM on more graph tasks such as question answering on knowledge graphs
4. 其他模态

## Limitations

- input token limit of the large language model---邻居采样
