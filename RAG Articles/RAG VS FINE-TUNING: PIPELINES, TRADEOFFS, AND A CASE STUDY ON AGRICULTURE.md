# RAG VS FINE-TUNING: PIPELINES, TRADEOFFS, AND A CASE STUDY ON AGRICULTURE

提出了一个用于微调和RAG的流程pipline，并展示了多个热门LLM（包括Llama2-13B、GPT-3.5和GPT-4）之间的权衡。

包含多个阶段：

1. 从PDFs中抽取信息
2. 生成问题和答案，用于微调
3. 利用GPT-4评估结果

农业领域数据集

## 1 Introduction

- 医疗保健：预测患者风险并提高诊断准确性。

  - J. Kim, S. Lee, S. Lee, and M. Kim. A deep learning–based approach for predicting anticancer drug response using gene expression profiles. Nature Computational Science, 3(1):1–11, 2023. doi: 10.1038/s43856-023-00370-1.

  - A J Thirunavukarasu, D S J Ting, K Elangovan, et al. Large language models in medicine. Nature Medicine, 29: 1930–1940, 2023. doi: 10.1038/s41591-023-02448-8. URL https://doi.org/10.1038/s41591-023-02448-8.

  - S.A. Alowais, S.S. Alghamdi, N. Alsuhebany, et al. Revolutionizing healthcare: the role of artificial intelligence in clinical practice. BMC Medical Education, 23:689, 2023. doi: 10.1186/s12909-023-04698-z.

- 制造业：提高运营效率，减少停机时间，并改善产品质量
  - Vanti. How llm applications are revolutionizing the manufacturing industry, 2023. URL https://www.vanti.ai/ how-llm-applications-are-revolutionizing-the-manufacturing-industry/.
  - Beibin Li, Konstantina Mellou, Bo Zhang, Jeevan Pathuri, and Ishai Menache. Large language models for supply chain optimization. arXiv preprint arXiv:2307.03875, 2023.
- 金融：欺诈检测、风险管理和投资决策
  - AI4Finance-Foundation. Fingpt. https://github.com/AI4Finance-Foundation/FinGPT, 2022.
  - Vena Solutions. Microsoft copilot impact on finance, 2022. URL https://www.venasolutions.com/blog/ microsoft-copilot-impact-on-finance.

例子 table-1：来自GPT-4和一位农学专家对同一查询在三个不同美国州提出的答案。

<img src="./assets/CleanShot 2024-03-03 at 15.57.23@2x.png" alt="CleanShot 2024-03-03 at 15.57.23@2x" style="zoom:33%;" />

尽管专家会根据各州特定的气候和农业传统提供具有背景的答案，但LLMs提供的是通用答案，虽然正确，但对于每个州来说并不像专家答案那样精确。

> GPT会提出通用的答案，但是无法精确，比如例子中的各个州的最佳种植时间

本文的重点：需要特定背景和适应性响应的行业，提出一个**LLM pipline，用于生成高质量的、特定领域的问答**

- 收集文件
- 清洗、结构化文件用于使用GPT模型生成QA对
- 对QA对进行评估和过滤

目标是为特定行业创建一个有价值的**知识资源**，最终旨在促进这一关键领域的发展。

在我们的农业研究中，我们的目标是产生特定地理位置的答案。

该数据集被输入到三个主要组件中：

- **问答生成**：根据农业数据集中可用的信息创建问题和答案对。
- **RAG**：用农业数据集作为知识源
- **微调**：生成的数据然后被精炼并用于微调多个模型

**contributions**：

- LLMs的全面评估：农业领域
- 检索技术和微调的影响：
  - RAG在数据具有上下文相关性的情况下被证明非常有效
  - 微调被发现在使模型学习农业领域特定的新技能以及提供更精确简洁的回应方面是有用的，但是成本高
- LLMs在不同行业的潜在用途：从问答生成过程开始导致更高效的模型

## 2 Methodology

**pipline**：figure 1

<img src="./assets/CleanShot 2024-03-03 at 16.25.17@2x.png" alt="CleanShot 2024-03-03 at 16.25.17@2x" style="zoom: 50%;" />

1. 数据收集
2. 信息抽取
3. 生成question 和 answer：
   1. 生成基于上下文、高质量、能够体现抽取的信息的问题
   2. 为问题生成答案：利用RAG
4. 用生成的QA对微调模型：LoRA

### 2.1 Data Acquisition

**收集高质量权威数据**

### 2.2 PDF Information Extraction

**组织文章结构、解析表格**

通过检索文档的组织结构，我们可以轻松地对信息进行分组，在表格中处理数值数据，并为问答生成步骤提供更一致的文本片段。同样重要的是，从文档中提取所有可用信息，并确保句子格式良好。

==**GROBID**==Grobid. https://github.com/kermitt2/grobid, 2008–2023.

- 一个专门针对从科学文献中提取和处理PDF格式数据的机器学习库。目标是将非结构化的PDF数据转换为**==TEI（文本编码倡议Text Encoding Initiative）==**格式的结构化数据，高效地管理大量文件。
- 使用在大量科学文章语料库上训练的GROBID，可以识别各种文档元素并提取相关的参考文献数据。

从由GROBID生成的TEI文件中，我们提取了TEI文件的部分章节，包括**文档元数据（标题、作者、摘要）**、章节、**表格**、**图表引用**、**参考文献**以及**内容**本身。

> 文本结构与内容同样重要

最终目标是将TEI文件转化为更加容易处理的json文件，不仅可以体现内容，还可以体现原PDF文件本身的结构

### 2.3 Question Generation

**从提取的文本生成问题时管理自然语言的固有复杂性和变异性**

==**Guidance framework**==Guidance framework. https://github.com/guidance-ai/guidance/tree/main, 2023.

- 其主要优势在于能够提供对输入和输出的结构组成具有无与伦比的控制能力，从而增强语言模型生成响应的整体效果
- 产生的输出不仅更精确，而且还表现出增强的连贯性和上下文相关性
- 将生成、提示和逻辑控制融合为一个统一的过程
- 通过上下文特定提示引导语言模型的方向，有助于提高生成文本的语义相关性水平



1. 首先，明确地从文本中**添加标签**来增强现有文档的内容和结构

   1. 定制Prompt从文旦中抽取地点、农业相关主题
   2. 让LLM基于从json中抽取的信息来进行回答

   - 目的是利用额外的信息（地点、提到的主题）来支撑回答

2. 将上下文和章节内容结合起来，LLM基于它们生成一组问题

### 2.4 Answer Generation

==**Retrieval-Augmented Generation (RAG)**==

检索方法：BM25, Dense Retrieval， etc.

- Embedding generation and index construction 嵌入生成和索引构建：**Facebook AI Similarity Search (FAISS) (Johnson et al., 2019)**构建数据库和embedding 
- retrieval：**FAISS retrieval tool**
- Answer Generation：从FAISS库检索的信息 + GPT-4 + custom prompt
  - answer以json格式
  - 和Question一起组成Q&A对

### 2.5 Fine-tuning

GPU：8个H100..

==**PyTorch’s fully-sharded data parallelism (FSDP) (Paszke et al., 2019).**==

- FSDP允许对参数、优化器状态和梯度进行分片，有效减少训练过程中的内存需求
- 模型中的每个transformer模块都作为一个带有激活检查点的FSDP模块运行
- 算了..看不懂

<img src="./assets/CleanShot 2024-03-04 at 20.36.10@2x.png" alt="CleanShot 2024-03-04 at 20.36.10@2x" style="zoom:50%;" />

**LoRA**微调**GPT-4**..

<img src="./assets/CleanShot 2024-03-04 at 20.45.57@2x.png" alt="CleanShot 2024-03-04 at 20.45.57@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-04 at 20.46.07@2x.png" alt="CleanShot 2024-03-04 at 20.46.07@2x" style="zoom:50%;" />



## 3 Dataset Overview

### 3.1 USA

美国数据集(USA)论文从美国农业部、各州农业部门以及农业研究机构等权威网站获取了23万个与农业相关的高质量文档。这些文档涵盖政策、法规、报告、指南等，内容涉及作物管理、疾病防治、最佳实践等多个方面。论文从中提取文本信息，构建了包含超过50M个词的数据集，覆盖了44个州。此外，论文还使用了华盛顿州相关的573个文档（约200万个词）作为评估数据集。

### 3.2 Brazil

巴西数据集(Brazil)论文使用了名为“500 Questions 500 Answers - Embrapa/SCT”的数据集，其中包含与巴西作物栽培和管理相关的问题和答案。这些问题是由生产者、农民和农业协会等不同利益相关者提出的，而答案则由Embrapa专家提供。该数据集的目的是帮助农民和农业专家提高对各种农业主题的知识水平。

### 3.3 India

印度数据集(India)论文从印度的农业咨询平台KVK获取了10万个农民问题及其答案。这些问题涵盖种植季节、作物类型、天气情况等多个方面。此外，论文还从Vikaspedia网站获取了更全面的农业知识，以丰富和完善KVK的答案。这两个数据源共同构成了印度数据集。

## 4 Metrics

要考虑的**关键因素**：

1. **问题质量固有的主观性**：由于人们对什么构成相关、信息丰富或引人入胜的问题存在不同看法，因此至关重要的是制定可以客观评估质量的度量标准，以应对这种主观性。
2. **问题的相关性和有用性对其上下文的依赖**：在一个情境中提供有价值见解的问题可能在另一个情境中被认为是无关紧要的，强调了需要**上下文感知**型指标。
3. 生成的问题的**多样性**和**新颖性**：一个强大的问题生成系统应该能够产生涵盖给定内容各个方面的广泛问题，量化多样性和新颖性可能具有挑战性，因为它涉及评估问题的独特性以及与内容和其他生成问题之间的相似度。语法正确性和流畅度也是问题质量中至关重要的元素。虽然自动工具可以评估语法正确性，但评估流畅度通常需要人类判断，这使得创建完全自动化指标变得困难。
4. 问题应该在给定的内容下可被回答：评估一个问题是否能够准确回答需要对内容有深刻理解，并具备识别相关信息以回答问题的能力。

现有的关于回答的评估的标准有很多，但是对于问题的质量的评估标准还差很多

### 4.1 Question Evaluation

**自动+人工**

- 自动
- 人工：相关性、新颖性和流畅性。

评价指标：

- 相关性(Relevance)：使用大语言模型评分问题在给定上下文下的相关性，评分范围为1-5，分数越高表示问题与农民相关度越高。
- 全局相关性(Global Relevance)：不考虑上下文，仅根据问题内容评估其与农民的相关性，评分范围为1-5。
- 覆盖率(Coverage)：评估答案是否可以从给定上下文中直接提取，评分范围为1-5，分数越高表示答案越可靠。
- 重叠度(Overlap)：利用KL散度评估问题与原文的语义相似度，分数越低表示问题与原文内容越接近。
- 多样性(Diversity)：利用Word Mover’s Distance评估问题之间的语义相似度，分数越低表示问题之间越多样化。
- 细节(Details)：统计问题和答案的词数，以评估其详细程度。
- 流畅性(Fluency)：利用大语言模型评估问题的流畅性和连贯性，评分范围为1-5。

### 4.2 Answer Evaluation

==**AzureML Model Evaluation (Microsoft, 2023)**==

- 一致性(Coherence)：评估答案与上下文的一致性，评分范围为1-5。
- 相关性(Relevance)：评估答案与问题相关性的程度，评分范围为1-5。
- 逻辑性(Groundedness)：评估答案是否基于上下文中的信息，评分范围为1-5。
- 完整性(Completion)：统计答案的词数。

### 4.3 Model Evaluation

GPT-4 as an evaluator

- 评估准则(Evaluation with Guideline)：利用大语言模型为每个问题生成评估准则，并根据准则评分答案的正确性。
- 简洁性(Succinctness)：根据大语言模型评估答案的简洁性，评分范围为1-5。
- 正确性(Correctness)：评估答案的正确性，分为完全正确、部分正确和完全错误。
- 计算量(Compute)：评估生成答案所需的计算量。
- 这些指标从多个维度评估了问答系统的性能，为模型优化提供了指导。

## 5 Experiments

### 5.1 Q&A Quality

- 问答质量评估(Q&A Quality)本实验使用GPT-3、GPT-3.5和GPT-4三种大语言模型，在不同上下文设置下评估生成的问答对的质量。上下文设置包括无上下文、内部上下文和外部上下文。通过计算覆盖率、多样性、相关性、流畅性等指标，比较了不同模型和上下文设置对问答质量的影响。

#### 5.1.1 Context Study

- 上下文研究(Context Study)该实验研究了不同上下文设置对模型生成问答的影响。实验结果显示，无上下文设置下，GPT-4的整体表现较好。当加入内部上下文后，GPT-3.5的覆盖率有所提升，但GPT-4仍保持领先。在外部上下文设置下，GPT-4的覆盖率和流畅性略高于其他模型。总体而言，GPT-4在不同上下文设置下表现最为稳定。

  <img src="./assets/CleanShot 2024-03-05 at 16.17.26@2x.png" alt="CleanShot 2024-03-05 at 16.17.26@2x" style="zoom:50%;" />

  <img src="./assets/CleanShot 2024-03-05 at 16.06.04@2x.png" alt="CleanShot 2024-03-05 at 16.06.04@2x" style="zoom:50%;" />

#### 5.1.2 Model to Metrics Calculation

- 模型计算指标(Model to Metrics Calculation)本实验比较了GPT-3.5和GPT-4在计算问答质量指标时的差异。结果显示，GPT-4在覆盖率、流畅性指标上给出了更高的分数，而在多样性、相关性指标上给出了较低的分数。这表明GPT-4更倾向于评估生成的问答对在上下文中的可靠性，而GPT-3.5更注重语义的丰富性。

  <img src="./assets/CleanShot 2024-03-05 at 16.06.34@2x.png" alt="CleanShot 2024-03-05 at 16.06.34@2x" style="zoom:50%;" />

#### 5.1.3 Combined vs Separated Generation

- 独立生成(Combined vs Separated Generation)实验对比了同时生成问题和答案与单独生成问题相比的优劣。结果显示，同时生成在覆盖率和相关性指标上表现更好，而单独生成在多样性和覆盖率指标上表现更优。因此，选择哪种方式取决于具体任务的需求。

  <img src="./assets/CleanShot 2024-03-05 at 16.07.17@2x.png" alt="CleanShot 2024-03-05 at 16.07.17@2x" style="zoom:50%;" />

### 5.2 Retrieval Ablation Study

- RAG检索能力(Retrieval Ablation Study)实验评估了RAG的检索能力。结果表明，当检索3个相关片段时，召回率可达80%以上。即使文档数量增加，RAG仍能以75%以上的召回率检索相关内容。

  <img src="./assets/CleanShot 2024-03-05 at 16.09.05@2x.png" alt="CleanShot 2024-03-05 at 16.09.05@2x" style="zoom:50%;" />

### 5.3 Fine-tuning

在准确而简洁地解决参考答案方面表现最佳的模型是Vicuna + RAG、GPT-4 + RAG、fine-tuned GPT-4 和fine-tuned GPT-4 + RAG。这些模型提供了精度、简洁性和信息深度的平衡组合。

#### 5.3.1 Evaluation with Guideline

- 模型微调(Fine-tuning)实验对比了微调模型和基模型在农业领域的表现。结果显示，微调后模型的准确率明显提升，且能学习跨区域知识。其中，微调后的GPT-4模型表现最优。

  <img src="./assets/CleanShot 2024-03-05 at 16.10.12@2x.png" alt="CleanShot 2024-03-05 at 16.10.12@2x" style="zoom:50%;" />

#### 5.3.2 Succinctness 简洁性

RAG集成可使响应更加简洁，由于回答通常集中在提供的上下文上，GPT-4+RAG倾向于提供最简洁的回答，但是微调GPT-4+RAG并没有简洁

<img src="./assets/CleanShot 2024-03-05 at 16.20.54@2x.png" alt="CleanShot 2024-03-05 at 16.20.54@2x" style="zoom:50%;" />

#### 5.3.3 Correctness 正确性

<img src="./assets/CleanShot 2024-03-05 at 16.23.28@2x.png" alt="CleanShot 2024-03-05 at 16.23.28@2x" style="zoom:50%;" />

### 5.4 Knowledge Discovery

知识发现(Knowledge Discovery)本实验旨在探讨微调对模型学习新知识的能力。实验选择了一个包含1000个在多个州中相似的问题的集合，并从训练集中删除这些问题。然后，我们评估了微调后的模型是否能够学习这些新知识。结果显示，未经微调的GPT-4模型仅能学习47%的新知识。然而，微调后的模型能学习72%的新知识，而微调后加入RAG的模型能学习74%的新知识。

表22的结果表明，GPT-4仅学到了这些新知识的47%，通过微调，我们成功将这一数字提高至72%，并且在RAG和经过微调的模型中达到74%。有趣的是，这可以被定义为模型可能学习到的上限。

<img src="./assets/CleanShot 2024-03-05 at 16.26.22@2x.png" alt="CleanShot 2024-03-05 at 16.26.22@2x" style="zoom:50%;" />

## 6 Conclusion

<img src="./assets/CleanShot 2024-03-05 at 16.29.39@2x.png" alt="CleanShot 2024-03-05 at 16.29.39@2x" style="zoom:50%;" />

RAG以提高大型模型准确性而闻名，在数据上下文相关的情况下非常有效，例如在解释农场数据方面。 创建嵌入式（即数据向量表示）的低初始成本使RAG成为一个有吸引力的选择。 但是，重要考虑输入令牌大小可能会增加提示大小，并且输出令牌大小往往更冗长且更难控制。

微调提供了一个精确、简洁的输出，适应简洁性。它非常有效，并提供学习特定领域新技能的机会。然而，由于需要在新数据上对模型进行大量工作，初期成本较高。此外，微调需要最小输入令牌大小，使其成为处理大数据集更高效的选项。

在这项研究中，我们还展示了如何利用结构化文档理解、结合 GPT-4 生成问题以及 RAG 生成答案，为特定行业的数据集生成相关问题和答案。所生成的问题与它们来源于的各个部分高度相关，并且模型能够利用整个文本来生成富有洞见和全面性的答案。我们的探索表明，==**将问题和答案分开生成**==可以有效利用令牌使用率，从而打开了为问答对每个组件使用不同模型或方法的可能性。我们还提出了一系列**指标**来正确评估所产生问题相对于原始文件中包含信息质量，并展示了多种衡量 RAG 生成答案质量的指标。

总之，虽然RAG和微调都是有效技术，但它们的适用性取决于特定应用、数据集的性质和规模以及可用于模型开发的资源。然而，这项工作为如何最佳结合这两种方法打下了基础，并进一步探索了面向行业特定LLM应用程序的数据集生成流程。

未来工作中，深入研究**经过微调模型获得何种知识**将变得重要，在从**文档中提取结构化信息并在使用LLM开发系统时利用方面**进行更多研究也很关键。另一个令人兴奋的方向是**如何将PDF文件中的结构化信息与相同文档中图像和标题相结合，以实现多模态微调机会**。