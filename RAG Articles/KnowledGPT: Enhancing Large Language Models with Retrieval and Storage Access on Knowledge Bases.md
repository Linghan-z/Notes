# KnowledGPT: Enhancing Large Language Models with Retrieval and Storage Access on Knowledge Bases

## Abstract

KnowledGPT，这是一个全面的框架，用于将LLMs与各种知识库连接起来，促进知识的检索和存储。

检索：采用思维提示程序，该程序以代码格式生成知识库的搜索语言，并具有预定义的知识库操作能力

知识存储：在个人知识库存储知识——用户个人需求

## 1 Introduction

**问题：**

1. 复杂问题、多跳（Kg的搜索）
2. 实体抽取、实体对齐
3. KG对知识的表达形式简洁，与自然语言有区别

**KnowledGPT：**

- LLMs+KBs
  - 公开db
  - 私人db（个人知识库）
- complex question
- ambiguation
- knowledge representation
  - 实体描述
  - 关系三元组
- **步骤**
  1. 生成搜索代码
  2. 执行搜索
  3. 生成回答
- 如果KnowledGPT判断问题不需要来自知识库的知识，或者检索到的知识不足或缺失，该问题将由LLM直接回答。

## 3 Methods

### 3.1 Task Definition

- 输入：user input in natural language
- 子任务：
  - knowledge retrieval：根据用户输入检索知识
  - knowledge storage：从用户输入抽取知识插入personalized KB

### 3.2 Knowledge Retrieval

**步骤**

1. 生成搜索代码
   - program of thought (PoT)
   - 方法：
     1. get_entity_info：实体->实体描述
     2. find_entity_or_value：包含实体和关系的输入->实体或值
     3. find_relationship：两个实体->实体间关系的列表
   - 处理同义词：每个实体或关系都被表示为候选别名列表，而不是单一名称，以有效处理同义词。
2. 执行搜索
   - 搜索功能分别在每个KB上并行执行，并将它们的结果连接起来。
3. 生成回答

#### 3.2.1 Code Implementation

#### 3.2.2 Entity Linking

实体、关系对齐

#### 3.2.3 Get Entity Information

#### 3.2.4 Find Entity or Value

1. 和知识库中的实体进行关联
2. 检索返回实体相关的所有三元组
3. 根据三元组的关系的相似度进行排名（用的cos）
4. 如果没有找到三元组，我们将在实体描述中进行进一步搜索

#### 3.2.5 Find Relationship

ind_relationship方法旨在访问知识图谱，以预测两个实体之间的关系，其输入通常为问题形式，例如“"What's the relationship between Steve Jobs and Apple Inc?"