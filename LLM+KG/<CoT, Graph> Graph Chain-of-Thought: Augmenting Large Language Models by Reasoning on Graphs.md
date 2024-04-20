# Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs

RAG在图上的一些困难：

1. Structure Context: RAG都是找到individual nodes/text，无法capture更多的信息
2. Graph Size Explosion：即使可以通过将子图转成文本给LLM，但是会引入长上下文

文章：

- Benchmark:Graph Reasoning Benchmark dataset called GRBENCH containing 1,740 questions that can be answered with the knowledge from 10 domain graphs.

- Graph Chain-of-thought (GRAPH-COT) three sub-steps:

  <img src="./assets/CleanShot 2024-04-19 at 15.10.43@2x.png" alt="CleanShot 2024-04-19 at 15.10.43@2x" style="zoom:50%;" />

  - LLM reasoning：LLM提出可以利用当前信息得出什么结论以及需要从图中得到哪些进一步信息

    - 与大模型进行推理。给定问题或之前的迭代上下文，第一步是让大模型进行推理，判断需要从图中获取哪些进一步的外部信息来回答问题，或者问题是否可以用图中的当前上下文来回答。例如，给出问题“谁是《语言模型是无监督多任务学习者》的作者？”。

      大模型预计会推理“我们需要首先在图表上找到论文节点{语言模型是无监督多任务学习者}”。

      整个的GRAPH-COT在prompt侧包括三个部分: graph description, interaction function description, and demonstrations，如下：

      <img src="./assets/CleanShot 2024-04-19 at 15.13.18@2x.png" alt="CleanShot 2024-04-19 at 15.13.18@2x" style="zoom:50%;" />

      - 其中：graph description表示的是对当前图谱描述的定义，如下对于MAG、DBLP以及Literature的描述
        - <img src="./assets/CleanShot 2024-04-19 at 15.14.02@2x.png" alt="CleanShot 2024-04-19 at 15.14.02@2x" style="zoom:50%;" />

  - LLM-graph interaction：大模型生成从外部获取信息所需的交互，例如，查找节点、检查邻居等

    - 基于之前LLM推理步骤的输出结果，下一步是让LLM知道如何与图交互并从图中获取相关信息，在这一步，预先定义了四个图函数来覆盖图上的语义信息和结构信息

      - RetrieveNode(Text):通过语义搜索识别图中的相关节点
      - NodeFeature(NodeID,FeatureName)：从图中提取特定节点的文本特征信息；
      - NeighborCheck(NodeID,NeighborType)：返回图中特定节点的邻居信息；
      - NodeDegree(NodeID,NeighborType)：返回图中特定节点的特定邻居类型的度；

    - 然后，要求大模型根据之前的推理结果生成准确的图函数调用，以有效地与图进行交互。在给定的示例中，LLM预计会生成“RetrieveNode（语言模型是无监督多任务学习器）”。

      对应的prompt如下：

      <img src="./assets/CleanShot 2024-04-19 at 15.17.48@2x.png" alt="CleanShot 2024-04-19 at 15.17.48@2x" style="zoom:50%;" />

  - graph execution:在图上执行交互步骤的请求并返回相应的信息

    - 该步骤是调用上一步给出的函数并从图中获取相关信息。对于前面的示例，该图将执行RetrieveNode(·)函数并返回“最相关的节点的ID是p-4123”，

      然后，当前迭代的过程结束，从“LLM推理”开始新的迭代，整个框架会不断迭代，直到LLM完成推理并输出最终答案。

      这里，为了提升大模型的指令遵循能力，提供了一个feweshot的例子，prompt如下：

      <img src="./assets/CleanShot 2024-04-19 at 15.19.14@2x.png" alt="CleanShot 2024-04-19 at 15.19.14@2x" style="zoom:50%;" />

- 总结

  - <img src="./assets/CleanShot 2024-04-19 at 15.20.28@2x.png" alt="CleanShot 2024-04-19 at 15.20.28@2x" style="zoom:50%;" />
  - 在进行子图检索时，节点/文本的数量会随着跳数线性增长而呈指数增长。尽管子图越大，它包含的信息越多，但将导致超长的上下文，甚至超过LLM的最大输入长度，并会导致LLM在中间丢失，在这种情况下，GRAPH-COT可以作为从图中提取更多有用信息的更好方法；
  - 但很明显的是，因为这个涉及到函数的调用问题，调用的能力又取决于大模型能力本身，因此，本质上又需要提升大模型的能力，例如上图中就明显存在错误的交互。


### Limitations

尽管我们使用GPT-4重新表述问题模板，但它们仍然大多是<u>*手动*</u>设计的，因此在问题多样性和难度方面可能还有改进空间。 

对于GRAPH-COT，所使用的LLM backbone 是一个无法微调（或者非常昂贵才能微调）的API模型。 未来方法可能需要考虑如何明确<u>*训练LLMs以在图上navigate*</u>。
