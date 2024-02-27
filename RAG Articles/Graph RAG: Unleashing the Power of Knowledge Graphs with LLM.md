# Graph RAG: Unleashing the Power of Knowledge Graphs with LLM

> Author: [NebulaGraph Database](https://medium.com/@nebulagraph?source=post_page-----e1e902c504ed--------------------------------)
>
> URL: https://arc.net/l/quote/gfeysfiu

利用知识图谱与大型语言模型（LLMs）相结合，为搜索引擎提供更全面的上下文理解。

RAG的短板：

- 需要大量训练数据
- 文本理解能力：RAG需要理解查询query的意图，对于复杂或多义的查询就会有歧义或者不准确

## Graph RAG

<img src="./assets/CleanShot 2024-02-26 at 16.27.25@2x.png" alt="CleanShot 2024-02-26 at 16.27.25@2x" style="zoom:33%;" />

基于知识图谱的检索增强技术，它使用知识图谱来展示实体和关系之间的关联，然后利用大型语言模型LLM（Large Language Model）进行检索增强。

图数据库自然适合通过以图格式组织和连接信息来存储和表达复杂的上下文信息。通过使用图技术构建知识图谱来增强上下文学习，用户可以提供更多上下文信息，帮助大型语言模型（LLM）更好地理解实体之间的关系，并提高其表达和推理能力。

Graph RAG将知识图谱等同于大规模词汇，实体和关系对应于单词。通过这种方式，Graph RAG可以在检索过程中联合建模实体和关系作为单位，从而更准确地理解查询意图并提供更精确的搜索结果。

### Graph RAG vs. Graph + Vector RAG

### Graph RAG vs. Text2Cypher

另一种基于知识图谱的有趣方法是Text2Cypher，它是一种自然语言生成图查询。这种方法不依赖于实体子图检索，而是将任务或问题转化为面向答案的图查询，本质上与我们通常称之为Text2SQL的方法相同。

Text2Cypher和Graph RAG主要在其检索机制上有所不同。Text2Cypher根据知识图谱模式和给定任务生成图模式查询，而(Sub)Graph RAG获取相关子图以提供上下文。两者都有各自的优势，您可以通过以下演示更直观地了解它们的特点。

