# Evidence-Focused Fact Summarization for Knowledge-Augmented Zero-Shot Question Answering

## Abstract

利用KG来增强LLM的QA的性能，在三元组形式或者三元组事实的自由文本形式的转换方面有问题：

- 由于重复实体或关系而导致的证据密度降低
- 由于无法强调关键证据而导致的证据清晰度降低

提出EFSUM，**E**vidence-focused **F**act **Sum**marization framework for enhanced QA with knowledge-augmented LLMs.

**通过蒸馏和偏好对齐来优化一个开源的LLM作为事实摘要器**

EFSUM提高了LLM的 zero-shot QA性能，并且可以确保摘要的有用性和忠实度

## 1 Introduction

基于KG的RAG的挑战在于KG中的都是三元组，因此现有的方法主要是涉及根据与给定问题的语义**相似性**检索一组相关事实，然后通过将其转化为文本形式以用于LLM提示的过程

对于检索到的相关的三元组：

- 以三元组的形式

- 使用LLMs转换成文本描述的形式

- > 有一说一，这一段看见过好多次了..

现有的以语言表达的文本的形式为LLMs提供上下文的方法的缺陷：

1. **Low density of evidence 证据密度低：**由于灵活性有限，事实的串联和线性化很可能包含重复的实体或关系，这最终会降低上下文知识中有用证据的密度，阻碍有效回答问题的能力
2. **Low clarity of evidence 证据清晰度低：**尽管语境知识描述了事实信息，但它们通常未能突出回答问题所需的证据，这种缺乏焦点可能导致**来自无关事实的干扰**，从而对LLM提供准确答案的能力产生不利影响。因此，即使在知识背景中提供了足够的证据（或确切的答案范围），LLM也可能难以正确识别它。

本文提出了**EFSUM**，关键思想是将事实集转化为合理和连贯的**摘要**，同时**突出证据**并**过滤噪音**以回答问题，这确保了**摘要保持高密度和清晰的证据**，促进有效的问答（图1）。

<img src="./assets/CleanShot 2024-03-11 at 22.38.28@2x.png" alt="CleanShot 2024-03-11 at 22.38.28@2x" style="zoom:50%;" />

- 这个summarization的最直接解决方案是用详细说明提示LLMs，**但是LLMs生成的摘要经常省略关键信息**(such as answer spans)，导致==**信息丢失 information loss**==，或者包括无法从检索到的事实中推断出来的信息，导致==**外在幻觉 extrinsic hallucination**==

- **enhanced summary quality**，将一个**开源的LLM优化为事实总结器**，分两步进行：

  1. ***LLM distillation：***使用通过LLM提示获得的参考摘要来训练事实摘要生成器

  2. ***preference alignment：***优化摘要生成器，以更好地与QA相关的任务特定偏好保持一致

     - 为此，引入了两个摘要候选项的偏好标准：

       1. ***helpfulness：*** 帮助性 LLMs可以根据摘要正确地回答问题
       2. ***faithfulness：*** 可靠性 评估摘要和提供的事实集合的事实一致性

     - 通过根据这些标准选择**首选 preferred**和**不好的 dispreferred**摘要对，我们进一步通过**直接偏好优化（DPO**）（Rafailov等人，2023年）来微调摘要生成器

       - > Direct Preference Optimization: Your Language Model is Secretly a Reward Model 2023.5.29

<img src="./assets/CleanShot 2024-03-11 at 22.44.58@2x.png" alt="CleanShot 2024-03-11 at 22.44.58@2x" style="zoom:50%;" />

## 2 Preliminaries 准备工作

KG-augmented zeroshot QA pipeline

### 2.1 KG-Augmented LLM Prompting for QA

三个阶段：retrieve-verbalize（用语言表达）-inject

#### Fact retrieval from knowledge graph

通过entity linking，从KG中找到问题相关的事实

- span detection 跨度检测
- entity disambiguation 实体消歧
- relation classification 关系分类

链接的实体及其邻居组成的三元组包含了相关的事实，或根据预测的路径采样三元组

计算语义相似性

- 使用预训练的句子编码器
- 直接针对直接事实检索微调

#### Fact verbalization into various form text

将事实言辞化为各种形式的文本

**符号->文本**->给大模型

- 线性 linear verbalization：链接 头、关系、尾，保持结构化的格式(i.e., triple-form text)
- 使用预定制的模板和启发式的方法进行线性化
- 使用微调的模型
- prompt给LLMs

#### Fact injection for question answering

knowledge-augmented LLM prompting for zeroshot QA

### 2.2 Analysis on Verbalized Facts

对事实文本化方法获得的上下文知识进行了初步分析，评估它们的**密度**和证据**清晰度**

<img src="./assets/CleanShot 2024-03-12 at 11.20.29@2x.png" alt="CleanShot 2024-03-12 at 11.20.29@2x" style="zoom:50%;" />

1. 重复token的比率
   1. 对于线性的方法（KAPING和Rewrite），重复的token多，表明他们的输出包含了源自知识图谱中预定义关系的冗余信息
2. 原始fact与言语话fact的长度之比
   1. （KAPING和Rewrite）要么保持长度，要么甚至增加长度，尽管保持相同的信息量，因此，他们的证据密度较低，甚至可能会下降
3. 最佳答案的平均位置
   1. 线性方法往往会在上下文知识中随机分散明显的证据（答案范围），他们的位置似乎依赖于从事实检索中获得的排名，而不是被放置在文本的前沿以**强调**
4. 语义相似度
   1. 线性的方法也比别的方法低，他们的输出可能包含噪音或无关信息，或者他们可能没有清晰地突出语义相关证据。

**实质上，线性的方法不能充分解决证据的清晰性问题**

## 3 EFSUM: Proposed Method

### 3.1 LLM Prompting for EFSUM

直接的方法是prompt给LLMs question和relevant fact，让LLMs进行summarization

==**EFSum_prompt**==：利用LLMs的zero-shot的能力生成摘要，指导LLMs将输入的事实转化为摘要，摘要作为上下文以促进问答任务的情况下进行

LLMs：GPT-3.5-turbo

### 3.2 LLM Fine-Tuning for EFSUM

**图3**

==**EFSum_distill**==：一种基于开源LLM的事实描述模型，对于evidence-focused fact summarization任务微调

两个优化步骤：

1. LLM distillation 蒸馏
2. Preference alignment 偏好对齐

LLMs：LLaMa2-7B

#### 3.2.1 Distillation of Fact Summarization

##### **首先优化开源的模型在给定question和符号事实集合的情况下生成evidence-focused摘要**

- 将问题-答案对(q,a)的QA训练数据集扩充到$X = \{(q, a, F)\}$ 
  - $F=\{f_k\}^K_{k=1}$ 是检索的top-k个与问题相关的facts

##### Reference summary generation 参考摘要生成

用GPT-3.5-turbo来获得参考摘要，用于训练summarizer

- 对于每个tuple (q, a, F)，prompt给LLMs将facts集合转换为文本描述s，并标记question的evidence
- 得到训练集$D = {(q, a, F, s)}$

##### Supervised fine-tuning SFT

对于数据集 $D$ 中的每个四元组 $(q, F, s, a)$，summarizer $θ$ 被优化为在给定 $q$ 和 $F$ 的情况下生成 $s$，使用因果语言建模目标：

<img src="./assets/CleanShot 2024-03-12 at 14.54.42@2x.png" alt="CleanShot 2024-03-12 at 14.54.42@2x" style="zoom:50%;" />

#### 3.2.2 Alignment with Summary Preference 与摘要偏好对齐

刚才是根据question和relevant facts生成evidence-focused 摘要，但是生成的摘要可能没有帮助unhelpful或者不可信unfaithful

采用偏好微调来增强EFSUM_distill，使其摘要能够与在知识增强的zero-shot QA背景下的任务特定偏好保持一致----即生成有帮助且可靠的摘要

- 一组偏好对$(q, a, F , s^+, s^−)$
  - s+和s-分别是好的和不好的摘要
  - 区分摘要的好与坏：
    1. 使用summarizer $\theta$ 对于每个tuple $(q, a, F, s) ∈ D$ 采样 $M$ 摘要候选集合 ${s^′_m ∼ p_θ(·|q, F )}^M_{m=1}$
    2. 为了构建偏好对，我们采用两个摘要过滤器filter（用于检查帮助性和可靠性）以及额外的释义过程
    3. 选择能够通过两个过滤器的答案感知释义候选项作为preferred，以及不能通过其中一个过滤器的候选项作为dispreferred来形成偏好对。

**Helpfulness filter** 帮助性过滤器

- 摘要在问答准确程度的帮助性————摘要是否真的帮助了LLMs来生成正确的答案（通过比较$a^′ ∼ p_{LLM}(·|q, s^′)$和正确答案$a$ ）

**Faithfulness filter** 忠实性（可靠性）过滤器

- G-Eval approach (Liu et al., 2023)： **G-eval: NLG evaluation using gpt-4 with better human alignment**
  - 利用LLMs从幻觉方面评估输入事实与给定摘要之间的**一致性**，即LLMs评估摘要是否包含无法从给定的符号推导出来的无用的信息

**Broad-to-specific paraphrasing** 从宽泛到具体的改写

这种改写的目的是通过将广泛关注点broad focus细化为具体关注点specific focus来获得高质量摘要

- prompt 给LLMs来改写摘要候选集合$s^′$到$s^{′′}$; ${s^{′′}_m ∼ p_{LLM}(·|t_{paraphrase}, s^′, a)}^M_{m=1}$
  - t_paraphrase是改写的prompt 
- $s^{′′}$ 再次经过helpfulness 和 faithfullness的filter

**Direct Preference Optimization** 直接偏好优化

使用偏好对preference pairs $P =\{(q, a, F , s^+, s^−)\}$，使用直接偏好优化**Direct Preference Optimization (DPO)** (Rafailov et al., 2023)

使用summarizer θ 来训练一个经过偏好调整的summarizer $θ^∗$，最小化以下目标： 

<img src="./assets/CleanShot 2024-03-12 at 15.35.56@2x.png" alt="CleanShot 2024-03-12 at 15.35.56@2x" style="zoom:50%;" />

- 其中<img src="./assets/CleanShot 2024-03-12 at 15.36.15@2x.png" alt="CleanShot 2024-03-12 at 15.36.15@2x" style="zoom:50%;" />
- 通过使用偏好-非偏好摘要对对模型进行优化，得到的模型$θ^∗$被训练成更偏向有用和忠实的摘要s+
- θ已针对每个问答模型进行了专门训练，因为不同的问答模型在总结帮助性方面有不同的偏好。

## 4 Experiments

- RQ1：言语化事实中的证据密度高是否有助于问答准确性？
- RQ2：言语化事实中证据的清晰度高是否有助于问答准确性？
- RQ3：偏好对齐能增强生成更有帮助和可靠的摘要吗？

### 4.1 Experimental Settings

#### Datasets

- WebQuestionsSP (WebQSP) (Yih et al., 2016)：包括那些可以通过Freebase回答的问题，并为它们提供了SPARQL查询
  - WebQSP-WD (Sorokin and Gurevych, 2018)：来自WebQSP的每个问题都预链接到Wikidata知识图谱
- Mintaka (Sen et al., 2022)：包含八种不同复杂性类型的QA数据集。为了主要关注零样本QA事实表达方法的有效性，我们仅使用测试集中的795个“通用”类型问题进行评估，共有4,000个问题

#### LLMs for zero-shot QA

- GPT-3.5-turbo
- Flan-T5-XL
- Llama2-7BChat

#### Baseline methods

- No knowledge：没有上下文知识
- KAPING (Baek et al., 2023a)：检索三元组，并以三元组的的形式 **triple-form**
- Rewrite (Wu et al., 2023)：利用关系路径将三元组转化为**free-form** 文本
- KG2Text (Ribeiro et al., 2021)：在KG-to-text 任务上微调encoder-decoder 模型，本文中利用的是T5-large

#### Evaluation metrics

- accuracy：如果问答模型的响应文本中至少有一个正确答案，则得分为1；否则得分为0。

#### Relevant fact retrieval

- 在检索与问题相关的事实时，利用由问题中的实体的一跳邻居组成的三元组
  - 但是一跳邻居的信息并不一定都是相关的
  - MPNet (Song et al., 2020)
    - 仅检索与问题表示具有最高语义相似度的前K个三元组
- 在计算语义相似性时，我们使用线性文本化方法，该方法涉及将将三元组中的主语、关系和宾语文本进行组合

### 4.2 Effectiveness of Dense Evidence (RQ1)

对上下文知识的最大令牌长度L施加限制——这意味着包含在上下文知识中的事实数量会根据事实表达方法而变化

#### Effect of knowledge augmentation 知识增强

对于零样本问答来说，知识增强并不总是能产生积极的结果

两个场景：

1. 模型在基础的输入知识方面的能力不足
2. 检索到的知识是有噪声的，但是QA模型内部的知识充足

<img src="./assets/CleanShot 2024-03-12 at 15.58.43@2x.png" alt="CleanShot 2024-03-12 at 15.58.43@2x" style="zoom:50%;" />

- LLaMa-7B作为模型的时候，它在两个数据集上的“无知识”条件下展示出更高的性能
  - LLaMa-7B在利用所提供的知识的方面表现有限
- 此外，在Mintaka上的GPT-3.5-turbo情况下，“无知识”条件表现出比其他基线更优越的性能
  - 这是因为Mintaka数据集相比WebQSP包含更具体和具有挑战性的问题
- 在一些复杂问题上，无法准确检索相关的信息的时候，引入噪声会影响性能（并且gpt-3.5-turbo本身就有解决一些问题的能力）

#### Comparison with other baselines

<img src="./assets/CleanShot 2024-03-12 at 16.09.47@2x.png" alt="CleanShot 2024-03-12 at 16.09.47@2x" style="zoom:50%;" />

- 看图2  EFSUM可以在**更短的摘要中封装更密集和更有用的信息**
- 当知识长度从L = 400减少到200时，我们方法的有效性更加明显。这表明即使在需要利用极为简洁知识的情况下，EFSUM仍然保持高效

#### Compatibility with various retrievers 与各种检索器兼容

评估在各种知识质量方面的稳健性

- randomly selected knowledge (Random)
- 最频繁出现关系的知识（Popular）
- 问题相关的知识question-relevant knowledge (MPNet)

<img src="./assets/CleanShot 2024-03-12 at 16.27.12@2x.png" alt="CleanShot 2024-03-12 at 16.27.12@2x" style="zoom:50%;" />

EFSUM在大多数数据集和问答模型中实现了最高的准确性。这些结果表明，**无论使用哪种检索器，EFSUM都具有优势**。考虑到基本检索器所展示的稳健性，预计**通过更复杂的检索器可以进一步提升EFSUM的性能**

### 4.3 Effectiveness of Clear Evidence (RQ2) 清晰证据的有效性

test tuples (q, a, F) F完全包含真实fact a

- 研究每种事实言语话表达方法如何将F转换为文本字符串而不忽视证据a，从而使正确答案成为可能

#### Comparison with other baselines.

<img src="./assets/CleanShot 2024-03-12 at 16.33.13@2x.png" alt="CleanShot 2024-03-12 at 16.33.13@2x" style="zoom:50%;" />

- 当Llama2-7B-Chat被用作WebQSP数据集的QA模型时，KAPING始终表现出最高性能
  - 这可能是因为该模型倾向于特定的知识格式
  - 某些QA模型可能更好地理解特定数据集中的特定知识格式

#### Robustness of EFSUM across various K

**K from 10 to 150**

- *answer-level*：我们评估答案在使用摘要生成的QA模型响应中包含的程度
- *summarylevel*：我们评估答案是否包含在该方法产生的口头知识中

### 4.4 Effect of Preference Alignment (RQ3) 偏好对齐的影响

#### Helpfulness and faithfulness

- helpfulness：在摘要级别计算
- faithfulness：1-发生幻觉的概率

<img src="./assets/CleanShot 2024-03-12 at 16.43.57@2x.png" alt="CleanShot 2024-03-12 at 16.43.57@2x" style="zoom:50%;" />

## 5 Related Work

### 5.1 KG-Augmented LLM Prompting

还是那两个..

### 5.2 Knowledge Graph Question Answering

探索从知识图谱中提取的额外知识（表示为子图）整合的方法分为两种主要方式

1. 语义解析技术：(Bao et al., 2016; Luo et al., 2018) ，通过使用上下文信息作为解析引用来从KG提取可执行查询。
2. 信息检索：涉及使用图神经网络（GNNs）等技术对同花信息进行编码：(Yasunaga et al., 2022a; Zhang et al., 2022; Yasunaga et al., 2022)
   1. 提出的方法 结合GNN和LMs，同时利用文本数据和知识图谱

## 6 Conclusion

在本文中，我们探讨了通过从知识图谱中增强知识来提高LLMs的零样本QA性能的方法。我们引入了一种新颖的总结框架，称为EFSUM，它将一组事实转化为具有高密度和清晰证据以回答问题的摘要。为了实现这一目标，我们优化一个开源LLM作为事实摘要器，利用teacher LLM的总结能力并使其输出与QA特定偏好对齐。我们的实验表明，与其他事实表达方法相比，EFSUM显著提高了各种LLMs的QA准确性。此外，作为独立的总结模块，它基于相关事实和目标问题生成有用且忠实的摘要。

## 7 Limitation

1. accuracy作为评估标准，即使回答不准确也有可能误判：仅验证答案实体的存在，而不考虑其在语境中是否合适
2. LLM倾向于偏爱某种事实表达方法的趋势，难以控制

- 在WebQSP数据集上的Llama2-7B-Chat，倾向于特定数据集中的特定知识格式

3. 摘要生成器的性能可能会受到检索器性能的影响





