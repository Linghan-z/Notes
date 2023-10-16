# High-level Concept

- RAG结合LLM和数据
- 用于组合自己的RAG流水线的LlamaIndex中的关键概念和模块。

## **Retrieval Augmented Generation (RAG)**检索增强生成

通过RAG，使用数据来增强LLM，两个阶段

1. indexing 索引：准备知识库
2. querying 查询：从知识中检索相关的内容来辅助LLM回答问题

<img src="/Users/zlh/Documents/Notes/LlamaIndex/assets/image-20230926233625556.png" alt="image-20230926233625556" style="zoom:50%;" />

### **Indexing Stage**

![image-20230926233818926](/Users/zlh/Documents/Notes/LlamaIndex/assets/image-20230926233818926.png)

1. Data connectors（reader）：从不同的数据源中抽取数据，并把数据格式化地存储为**Documents 表示**
2. Documents/Nodes：Documents是数据的容器，如PDF、API输出、从数据库检索的数据等。Nodes是llamaindex的数据原子单位，代表源文档的“块chunk”。它是一种丰富的表示形式，包括元数据和(与其他节点的)关系，以支持准确和富有表现力的检索操作。
3. Data indexes：拥有了抽取的数据之后，LlamaIndex可以帮助将数据index（索引）成一种容易retrieve（检索）的格式。LlamaIndex会将原始文档解析为中间表示形式，计算向量嵌入，并推断元数据

### Querying Stage

在查询阶段，RAG会根据用户的查询检索最相关的上下文，传递给LLM来生成响应。

查询阶段的关键挑战是在知识库上进行检索、编排和推理。

<img src="/Users/zlh/Documents/Notes/LlamaIndex/assets/image-20230926235635698.png" alt="image-20230926235635698" style="zoom:50%;" />

LlamaIndex提供了可以组合的模块来帮助构建以及继承RAG流水线用于QA、chatbot、as part of an agent。这些构建的模块可以根据排名偏好进行定制，也可以以结构化的方式组合来推理多个知识库。

#### building blocks 构建模块

**Retrivers 检索器：**定义如何在给定查询之后从知识库中有效地检索相关信息，具体的检索逻辑因不同的索引而异，最流行的是针对向量索引进行密集检索。

**Node Postprocessors 节点后处理器：**那一个节点的集合，然后对它们应用转换、过滤或重新排序的逻辑。

**Response Synthesizers 响应合成器：**从LLM生成响应，使用用户的查询以及给定的检索文本块集合

#### **piplines 流水线**

**Query Engines 查询引擎：**端到端的流水线，根据自己的数据问问题。接收自然语言查询，返回响应，以及检索到并传递给LLM的参考上下文

**Chat Engines 聊天引擎：**端到端的流水线，根据自己的数据进行对话（多轮对话）

**Agent 代理：**自动决策（LLM驱动），通过一组工具与世界交互。【An agent is an automated decision maker (powered by an LLM) that interacts with the world via a set of tools. 】代理可以像查询引擎或聊天引擎一样。主要区别在于代理程序动态决定最佳的行动顺序，而不是按照预先确定的逻辑进行操作。这使得它具备了处理更复杂任务的额外灵活性。