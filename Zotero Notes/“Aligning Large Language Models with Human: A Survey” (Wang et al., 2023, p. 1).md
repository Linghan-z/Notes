---
tags: []
parent: 'Aligning Large Language Models with Human: A Survey'
collections:
    - LLM
version: 9118
libraryID: 1
itemKey: DMY8B9GF

---
# <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B121.863%2C749.141%2C473.402%2C762.038%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Aligning Large Language Models with Human: A Survey”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

Comment: work in progress

Referred in <a href="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=2" rel="noopener noreferrer nofollow" zhref="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=2" ztype="znotelink" class="internal-link">LLM</a>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B157.758%2C615.833%2C202.243%2C626.581%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Abstract”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

LLMs容易受到某些限制：

*   误解人类指令
*   生成潜在有偏见的内容
*   事实上不正确（产生幻觉）信息

因此，将LLMs与人类期望保持一致已成为研究界的一个活跃领域。

本文提供了对这些对准技术的全面概述，包括以下方面：

1.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B233.633%2C440.616%2C273.782%2C449.642%5D%2C%5B87.874%2C428.66%2C116.324%2C437.686%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Data collection”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

    数据收集：有效收集LLM对齐的高质量指令的方法，包括使用NLP基准、人工标注和利用强大的LLM。

2.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B87.545%2C380.84%2C187.909%2C389.866%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Training methodologies”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

    训练方法：详细回顾了用于LLM对齐的主流训练方法。包括有监督微调、在线和离线人类偏好训练，以及参数高效训练机制。

3.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B87.874%2C309.109%2C166.039%2C318.135%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Model Evaluation”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

    模型评估：评估这些与人类对齐的LLM模型效果的方法，提出了一种多方面的评估方法。

相关论文链接：

<https://github.com/GaryYufei/AlignLLMHumanSurvey>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B70.866%2C143.16%2C153.68%2C153.908%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“1 Introduction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

基础的大型语言模型（LLM）如GPT-3是在一个庞大的文本语料库上进行预训练，其目标是<span style="background-color: #ffd40080">预测后续的标记。</span>

问题：

1.  产生与人类期望不符的输出。
2.  产生幻觉

因此，最近的自然语言处理研究工作集中在赋予LLMs理解指令并与人类期望保持一致的能力。

使LLMs遵循人类指令的最初方法是：使用指令集，通过将手工制作的任务指令模板与标准NLP任务的实例相结合编译而成的。<span style="background-color: #2ea8e580">但是往往无法捕捉到实际用户指令的复杂性，</span>

1.  因为这些指令往往源自于设计用来测试机器能力特定方面的人工NLP任务。
2.  另一方面，现实世界的用户说明更加多样化和复杂。

因此，OpenAI通过由多样化的人类用户注释的指令来探索LLM的监督微调（<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B497.556%2C344.993%2C526.22%2C354.451%5D%2C%5B305.869%2C331.443%2C387.833%2C340.901%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Supervised Fine-Tuning”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>，SFT）。通过这个过程开发的模型，比如InstructGPT（Ouyang等人，2022年）和ChatGPT 1，在理解人类指令和解决复杂任务方面表现出显著改进。

<https://blog.csdn.net/zzPaulmn/article/details/128684731>

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B413.516%2C236.599%2C524.411%2C246.057%5D%2C%5B306.142%2C223.05%2C447.77%2C232.508%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=1">“Reinforcement Learning from Human Feedback (RLHF)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 1</a></span>)</span>

该方法通过使用经过人工评级的输出来训练奖励模型，从而学习人类偏好。

在对齐过程和随后的评估中存在的挑战：

1.  数据：收集SFT和RLHF阶段的高质量数据可能是昂贵且耗时的。
2.  训练策略：训练策略需要进行优化，因为SFT培训消耗资源较多，并且RLHF中的强化学习常常缺乏稳定性。
3.  评估方法：全面评估LLMs是具有挑战性的，因为有限的NLP基准可能无法完全展示LLMs的多方面能力。

![\<img alt="" data-attachment-key="QS7VWJYE" width="1640" height="1830" src="attachments/QS7VWJYE.png" ztype="zimage">](attachments/QS7VWJYE.png)

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B70.866%2C269.794%2C524.406%2C278.432%5D%2C%5B70.866%2C257.838%2C258.282%2C266.476%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2">“Figure 1: Taxonomy of research in aligning Large Language Models (LLMs) with human that consists of alignment data, training strategy, and evaluation methods.”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 2</a></span>)</span> 图1：将大型语言模型（LLMs）与人类对齐的研究分类，包括对齐数据、训练策略和评估方法。

对于方面（a）数据，重点是有效地收集大规模、高质量的数据，用于LLM对齐训练。

研究人员建议利用现有的自然语言处理基准、人工标注和最先进的LLM（例如ChatGPT和GPT-4）来生成训练指导。

为了解决方面(b)训练方法，解决方案涉及优化训练方法，以提高效率和稳定性，并将人类偏好纳入其中。为了减少LLM对齐的计算量和提高效率，已经提出了参数高效的训练方法。此外，一些研究人员将人类偏好视为基于<span style="background-color: #ffd40080">排名</span>的训练信号，或者用基于语言的反馈取代标量奖励，以提高训练的稳定性和性能。

关于(c)方面，已经提出了各种以人为中心的LLM评估基准和自动评估协议（例如，用于评估的LLMs），以获得对齐LLMs的全面评价。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C530.893%2C224.945%2C541.641%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“2 Alignment Data Collection”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 3</a></span>)</span>

$$
l_k = (x_k, y_k)
$$

其中xk表示指令输入，yk表示相应的回复

数据来源：1. 人工生成；2. 强大的LLMs生成

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C325.886%2C215.215%2C335.693%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“2.1 Instructions from Human”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 3</a></span>)</span>  人工生成指令

两个主要来源：

1.  现有的人工标注的自然语言处理基准测试数据集
2.  精心手工制作的指令

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C247.18%2C186.928%2C256.987%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“2.1.1 NLP Benchmarks”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 3</a></span>)</span>  人工标注的NLP基准数据集

直观的方法：将基准数据集调整为自然语言指令，例子：

![\<img alt="" data-attachment-key="ACTPXNEM" width="790" height="538" src="attachments/ACTPXNEM.png" ztype="zimage">](attachments/ACTPXNEM.png)

相关的工作：

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B254.466%2C176.904%2C290.941%2C186.362%5D%2C%5B70.866%2C163.355%2C195.525%2C172.813%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“PromptSource (Bach et al., 2022)”</a></span>
*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B203.748%2C163.355%2C290.496%2C172.813%5D%2C%5B70.866%2C149.805%2C195.665%2C159.263%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“FLAN (Wei et al., 2022a; Longpre et al., 2023)”</a></span>
*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B219.708%2C149.805%2C290.95%2C159.263%5D%2C%5B70.866%2C136.256%2C289.863%2C145.714%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“SuperNaturalInstruction (Wang et al., 2022b; Mishra et al., 2022)”</a></span>

这些基准代表了在语言指令框架下统一的各种不同的自然语言处理任务，如对话、推理任务和编码任务。

人工指定模板将数据整合成文本，目标是增强LLMs在训练任务中的多任务学习能力，并促进对未知任务的泛化。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B385.224%2C516.553%2C503.495%2C526.011%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“OIG (Nguyen et al., 2023)”</a></span>

     将FLAN类似的NLP基准测试中的指令与其他类型的开放式指令相结合，例如如何操作、数学和编码指令。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B354.178%2C448.807%2C453.265%2C458.45%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“Unnatural Instructions”</a></span>

    利用LLMs生成与原始指令相似但具有显著差异的新模板或实例。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B306.142%2C262.882%2C460.986%2C272.689%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=3">“2.1.2 Hand-crafted Instructions”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 3</a></span>)</span> 手工制作的指令

从NLP基准构建指令可能是有效的，<span style="background-color: #2ea8e580">但是许多数据集是专注于某个领域的，所以生成的指令范围也相对小，因此，它们可能无法满足现实世界应用的复杂需求，比如进行对话。</span>

可以通过有意识的手动注释来构建指令。

*   “databricks-dolly-15k (Conover et al., 2023)” 众包收集

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B166.942%2C649.315%2C231.235%2C658.958%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4">“OpenAssistant”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 4</a></span>)</span> 多语言注释，注释过程包括：

    *   编写对话的初始prompt

    *   作为助手或用户进行回复

    *   将对话质量排名以明确提供人类偏好

        因此，这个语料库可以用于监督微调SFT和LLMs的人工偏好对齐训练。

*   COIG：从现有的英文指令集中构建高质量的中文指令

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B147.544%2C446.077%2C193.9%2C457.581%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4">“ShareGPT”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 4</a></span>)</span>

    众包人工撰写指令集，鼓励用户分享他们的ChatGPT和GPT-4的对话内容，这样的机制可以有效地收集大量多样化且由人类撰写的指令，很可能触发高质量的ChatGPT/GPT4回复。一些研究人员认为可以将这些资源作为种子指令，来使得GPT-3.5生成高质量的多轮对话

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B70.866%2C205.467%2C246.23%2C215.274%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4">“2.2 Instructions From Strong LLMs”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 4</a></span>)</span>

随着强大的闭源LLM（例如ChatGPT/GPT4）的出现，通过向这些LLM提供适当的提示，自动化收集过程以获取各种类型的合成指令（例如单轮、多轮和多语言指令）也是可行的。

主要挑战是如何有效地促使LLMs生成多样且高质量的指令。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B306.142%2C430.683%2C412.2%2C440.49%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4">“2.2.1 Self-Instruction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 4</a></span>)</span> 自我指导

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B305.869%2C414.604%2C451.756%2C424.247%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4"><span style="color: #eb52f7">“Self-Instruct (Wang et al., 2022a)”</span></a></span>

自动化指令收集，它利用ChatGPT的上下文学习能力，从预定义的人工注释指令集中生成大规模指令，涵盖了各种主题和任务类型，如图3所示。

![\<img alt="" data-attachment-key="N3SCECWX" width="400" height="454" src="attachments/N3SCECWX.png" ztype="zimage">](attachments/N3SCECWX.png)

但是使用self-instruction的指令微调的大模型比2.1中的1. 基于基准数据集的人工标注的指令以及手工制作的指令的效果好。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B464.168%2C197.816%2C524.408%2C207.274%5D%2C%5B306.142%2C184.267%2C507.805%2C193.725%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4">“Aplaca (Taori et al., 2023) and its variants (Cui et al., 2023a)”</a></span>

    遵循这一自我指导框架

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B306.142%2C109.158%2C422.248%2C119.041%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=4"><strong>“Improving Input Quality”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 4</a></span>)</span>**

强大的LLM合成指令常常受到多样性问题的限制。比如生成笑话

*   <span style="color: #eb52f7">“Self-Instruct“</span> <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B239.077%2C730.61%2C291.042%2C740.068%5D%2C%5B70.506%2C717.061%2C105.112%2C726.519%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Wang et al. (2022a)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 5</a></span>)</span> 针对不同类型的指令提出了不同的输入和输出生成策略。

    *   首先prompt ChatGPT来将任务分成分类任务和非分类任务
    *   然后，分别针对分类任务和非分类任务采用输出优先和输入优先的策略。

在输入prompts中添加各种外部信息，以增强多样性和真实性。比如

*   维基百科的类别关键词

    <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2218%22%2C%22position%22%3A%7B%22pageIndex%22%3A17%2C%22rects%22%3A%5B%5B317.051%2C440.589%2C360.14%2C449.227%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2218%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=18"><span style="color: #eb52f7">“Lamini-lm”</span></a></span>

    “Wikipedia Category Keywords (Wu et al., 2023)”

*   网络社区中的用户问题

    <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B327.914%2C705.858%2C341.282%2C710.949%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2"><span style="color: #eb52f7">“Baize”</span></a></span>

    <span style="color: #eb52f7"> </span>

    “(Xu et al., 2023c; Anand et al., 2023)”

*   基准测试指令

    <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B327.914%2C691.275%2C381.069%2C696.365%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2"><span style="color: #eb52f7">“Unnatural Instructions”</span></a></span>

    “SuperNaturalInstruction benchmark (Honovich et al., 2022)”

*   在数据生成中添加元信息，比如：长度、主题、样式等，可以有效地消除生成的数据中的偏差，并且可以提高合成数据的多样性

    <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B391.337%2C705.858%2C418.084%2C710.949%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2"><span style="color: #eb52f7">“AttrPrompt”</span></a></span>

    “Yu et al. (2023b)”

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B97.811%2C446.077%2C156.127%2C455.72%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Evol-Instruct”</a></span>  逐步获得复杂且困难的指令。

    *   在EvolInstruct中，没有使用现有的指令来提示LLM通过情境学习产生新的指令，而是有五个不同的手动设计的提示，以明确地指示LLM使用深度方法(即，包括关于特定主题的更多信息)或广度方法(即，提高主题/信息覆盖率)将现有的简单指令重写为复杂的指令。

    *   生成的

        <span style="color: #eb52f7">WizardLM</span>

        <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B355.719%2C698.567%2C398.764%2C703.657%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2">“(Xu et al., 2023b)”</a></span>

        模型在MTBench（Zheng等，2023）和AlpacaEval（Dubois等，2023）中排名靠前。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B69.961%2C242.839%2C128.924%2C252.482%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5"><span style="color: #eb52f7">“WizardCoder”</span></a></span>

    “(Luo et al., 2023)”

    从简单的代码和编程指令生成复杂的代码和编程指令

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B444.409%2C691.275%2C457.131%2C696.365%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=2"><span style="color: #eb52f7">“Phi-1”</span></a></span> “Gunasekar et al. (2023)” <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 5</a></span>)</span> 生成类似教科书的指导，提供足够的背景知识来促进LLMs的推理和基本算法技能。

    *   他们发现，由此产生的13亿个LLMs phi-1成功地超越了各种规模更大的LLMs，显示出数据质量的重要性。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B70.866%2C109.158%2C194.137%2C119.041%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5"><strong>“Improving Output Quality”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 5</a></span>)</span>**

除了提供高质量的教学输入之外，一个关键要求是巧妙地促使LLMs产生高质量的回应。提高响应质量的传统方法是在LLM提示后附加额外条件，包括以下方面:

1.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B334.209%2C714.126%2C492.55%2C724.009%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Reasoning-Provoking Conditions”</a></span> 引发推理的条件:

    1.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B443.442%2C700.577%2C524.415%2C710.035%5D%2C%5B305.782%2C687.028%2C332.284%2C696.486%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5"><span style="color: #eb52f7">“Chain-of-Thought (CoT)”</span></a></span>

        提示中加入推理过程

    2.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B348.67%2C619.282%2C370.291%2C628.74%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5"><span style="color: #eb52f7">“Orca”</span></a></span>

        <span style="color: #eb52f7"> </span>

        不仅学习了LLMs的表面响应文本，还捕捉到了复杂的推理过程信号，即他们引导LLMs使用一系列预定义的系统提示（例如，“逐步思考并证明你的回答”）来回应需要推理能力的FLAN指令，从而促使LLMs（例如GPT4）披露他们的推理过程信息。

2.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B334.12%2C467.306%2C493.174%2C477.189%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Hand-crafted Guiding Principles”</a></span>  手工制作的指导原则

    1.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B414.2%2C453.757%2C475.373%2C463.4%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5"><span style="color: #eb52f7">“self-alignment”</span></a></span>

        Sun等人（2023b）引入了自对齐框架，将16个手动设计的原则规则纳入输入提示中，从而引导LLMs生成有用、道德和可靠的回答。采用了CoT的技术

3.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B335.711%2C328.88%2C453.928%2C338.763%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Role-playing Conditions”</a></span> 角色扮演条件

    1.  <span style="color: #eb52f7">Phoenix</span>

        <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B472.61%2C328.88%2C526.321%2C338.763%5D%2C%5B305.782%2C315.33%2C339.913%2C324.788%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Chen et al. (2023e)”</a></span>

        使用ChatGPT和手动努力的结合来生成一组角色配置文件。他们为每个角色配置创建了种子指令，并将自我指导应用于角色配置和指令的组合，以获取来自LLMs的细致回应。

    2.  <span style="color: #eb52f7">Expert Prompting </span>

        <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B449.784%2C247.584%2C525.138%2C257.042%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Xu et al. (2023a)”</a></span>

        徐等人（2023a）提出了一个两阶段的指令响应框架，首先根据待回答的指令生成专家概要文件，然后使用专家概要文件和实际指令来促使LLMs产生高质量的响应。

4.  <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B333.219%2C149.805%2C489.724%2C159.688%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Difficulty-monitoring Conditions”</a></span> 困难监测条件

    1.  <span style="color: #eb52f7">Lion</span>

        <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B500.92%2C149.805%2C524.41%2C159.688%5D%2C%5B306.142%2C136.256%2C362.001%2C145.714%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=5">“Jiang et al. (2023)”</a></span>

        基于外部LLM评估监测指令反馈质量。首先使用指令数据来对基础的LLM进行微调，获得“student LLM”，然后对于每个指令，从 teacher LLM和 student LLM收集相应，促使LLMs对两种响应的质量进行成对评估。只有当student LLMs的反应低于teacher LLMS的反应时，才会保留指令。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B70.866%2C680.879%2C212.826%2C690.686%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“2.2.2 Multi-turn Instructions”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 6</a></span>)</span> 多轮指令

与人类很好地结合的LLMS应该能够在基于对话的环境中与用户交互

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B70.473%2C568.925%2C195.289%2C578.383%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Vicuna (Chiang et al., 2023)”</a></span>

    从ShareGPT获取指示，这是一个托管有趣的人类-LLM联合对话的网站。

    <span style="color: #05a2ef">但是需要人类上传很多他们的对话数据</span>

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B105.308%2C501.179%2C164.626%2C510.637%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Self-Chatting”</a></span>

    Baize 使用流行的QA网站上的问题作为开始话题，然后Chat-3.5被提示以四轮对话的形式自聊这个问题。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B174.922%2C446.982%2C211.397%2C456.625%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“CAMEL”</a></span> 一种角色扮演框架，首先由人工注释员提供一个主题，然后LLM被分别提示为“AI用户”和“AI助手”来讨论这个主题。

    *   Jiet al.(2023)更进一步，提示LLMS首先确定对话主题，然后让LLMS自聊以产生对话语料库。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B188.125%2C284.392%2C216.547%2C294.035%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“SelFee”</a></span>

    “Ye et al. (2023a)”

     revision-based多人对话语料库，在初始回复之后，进一步prompt LLMs来生成反馈并且必要时回答进行修正。使用这个语料库训练了SelFee模型

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B117.076%2C243.744%2C175.825%2C253.202%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“UltraLLaMA”</a></span> 利用了广泛的现实世界的信息，制作初始问题和说明，以指导LLMS生成多样化和高质量的多轮对话。

    1.  来自LLMs和Wikipedia的现实世界的知识
    2.  各种文本生成任务
    3.  高质量的文本语料库

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B70.866%2C139.816%2C220.888%2C149.623%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“2.2.3 Multilingual Instructions”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 6</a></span>)</span> 多语种指令

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B413.387%2C744.16%2C503.34%2C753.618%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Chen et al. (2023e)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 6</a></span>)</span> <span style="color: #eb52f7">Phoenix</span> 翻译输入和输出，策略：

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B457.952%2C730.61%2C524.41%2C740.253%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Post-answering”</a></span>

        ：翻译输入指令，再将翻译结果给LLMs作为prompt，会影响质量，但是能保留文化信息

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B306.142%2C635.766%2C375.383%2C645.224%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Post-translating”</a></span>

        ：首先，强制LLMs用英语回答指示，然后翻译输入和输出。这种方法可以获得高质量的输出文本，但会丢失特定的文化信息。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B420.319%2C581.569%2C493.091%2C591.027%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Li et al. (2023b)”</a></span>

    <span style="color: #eb52f7">BactrianX</span>

    <span style="background-color: #e56eee80"> </span>

    遵循Postanswering策略，使用Google translate构建指令数据，然后用这些数据微调LLAMA

*   另一种解决方案是在多轮对话中混合使用几种语言。<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B348.916%2C500.274%2C477.432%2C509.732%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“<span style="color: #eb52f7">BayLing</span> (Zhang et al., 2023c)”</a></span>引入了一套多轮交互式翻译指令，以同时提高LLMs的多语言和遵循指令能力。

    *   首先用户让LLM进行翻译，然后逐步增加其他要求
    *   这个过程自然地将不同的语言以及人类偏好与LLMs联系在一起。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B306.142%2C313.369%2C471.884%2C323.176%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“2.3 Instruction Data Management”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 6</a></span>)</span> 指令数据管理

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B306.142%2C217.551%2C420.641%2C227.434%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6"><strong>“Instruction Implications</strong>”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 6</a></span>)</span> 指令含意

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B492.635%2C204.002%2C526.318%2C213.46%5D%2C%5B305.782%2C190.453%2C335.447%2C199.911%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Ji et al. (2023)”</a></span>

     

    <span style="color: #eb52f7">BELLE </span>

    增加训练指令数量可以提升标准NLP任务的性能，如：信息提取、分类、封闭型问答、摘要，但是对于复杂推理任务影响很小，如：数学、代码、CoT、头脑风暴

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B411.35%2C109.158%2C525.137%2C118.616%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=6">“Muennighoff et al. (2023)”</a></span>

    <span style="color: #eb52f7">Data-Constrained LM </span>

    增加约50%的编程指令不仅不会影响一般对话表现，还能提升LLMs的推理能力。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B95.315%2C744.16%2C182.745%2C753.618%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Ghosal et al. (2023)”</a></span>

    <span style="color: #eb52f7">FLACUNA</span>

    将FLAN风格的指令与ChatGPT/GPT-4中的合成指令相结合，有效地增强了LLM的推理和问题解决能力。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B81.775%2C688.983%2C171.795%2C698.441%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Wang et al. (2023d)”</a></span>  <span style="color: #eb52f7">TULU</span> 与COT和编码有关的指令对于增强LLMS的推理能力至关重要。

    *   不同的指令可以影响不同的LLM能力。
    *   因此，所有指令类型的综合使相应的LLMs能够达到更好的整体性能
    *   暗示着需要更先进的指令收集技术和技术。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B70.866%2C502.084%2C168.595%2C511.967%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7"><strong>“Instruction Quantity”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span> 指令质量**

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B122.279%2C461.437%2C212.403%2C470.895%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“AlShikh et al. (2023)”</a></span> <span style="color: #eb52f7">IFS</span> IFS的前提是基于以下观察：

    *   在给定输入文本前缀的情况下，基础LLM foundation LLMs 通常会预测接下来的标记并生成"continuation-like"的输出，

    *   而完全指令调整的LLM fully instruction-tuned LLMs 则将输入前缀解释为问题，并生成

        <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B75.268%2C298.846%2C125.275%2C308.304%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“answer-like”</a></span>

        的输出。

    *   IFS被量化为在给定指令的所有输出中，“answer-like”的输出所占比例。研究人员训练了一个外部分类器来区分“continuation-like”和“answer-like”输出，并得出结论，LLaMA需要大约8K个指令才能达到较高的IFS得分。

    *   更多的指令有可能引发基础LLMs中的语义转变。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B105.361%2C244.65%2C189.049%2C254.108%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Zhou et al. (2023)”</a></span>

    <span style="color: #eb52f7">LIMA </span>

    仅仅6K个高质量的指示就足以与人类偏好保持一致。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B158.182%2C190.453%2C233.68%2C199.911%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Cao et al. (2023)”</a></span>

    <span style="color: #eb52f7">Instruction Mining </span>

    旨在确定高质量指令的预测特征。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B97.456%2C82.059%2C181.781%2C91.517%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Chen et al. (2023b)”</a></span>

     

    <span style="color: #eb52f7">Alpagasus</span>

    使用ChatGPT直接评估指令的质量

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B306.142%2C693.784%2C425.156%2C704.532%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“3 Alignment Training”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>

使用收集到的指令数据来微调现有的基础LLM，使其与人类保持一致。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B385.891%2C632.998%2C523.536%2C642.456%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7"><strong>“Supervised Fine-Tuning (SFT)”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>**

*   给定指令x，SFT计算对于ground-truth回答的交叉熵损失

*   ![\<img alt="" data-attachment-key="A93UEST2" width="642" height="80" src="attachments/A93UEST2.png" ztype="zimage">](attachments/A93UEST2.png)

*   SFT

    <span style="color: #4eb31c">帮助LLMs理解提示的语义含义并做出有意义的回应。</span>

*   <span style="color: #05a2ef">SFT的主要局限性是：它只教LLM关于最佳响应的知识，而不能提供与次优响应的细粒度比较。</span>

*   然而，值得注意的是，SFT目标或SFT模型参数也已经被整合到许多人类偏好训练目标中，以规范和稳定LLM的训练过程。

*   总结了基于SFT的研究工作：

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B414.782%2C405.616%2C524.413%2C415.259%5D%2C%5B306.142%2C392.067%2C341.838%2C401.71%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Online human preference training”</a></span>

        <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B349.073%2C392.067%2C504.232%2C401.71%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Offline human preference training”</a></span>

        <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B305.804%2C378.518%2C485.845%2C388.161%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“Parameter-effective fine-tuning solutions.”</a></span>

        <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B306.142%2C356.84%2C495.851%2C366.647%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7">“3.1 Online Human Preference Training”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span> 3.1 在线人类偏好训练

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B306.142%2C339.287%2C524.682%2C348.745%5D%2C%5B305.782%2C325.738%2C436.953%2C335.196%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=7"><span style="color: #eb52f7">“Reinforcement learning from Human Feedback (RLHF)</span> (Ouyang et al., 2022)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 7</a></span>)</span>

    *   旨在在

        <span style="color: #ffcb00">PPO</span>

        框架下从外部奖励模型中学习人类偏好信号。

    *   三个主要阶段；

        1.  收集高质量的指令集，并对预训练的LLMs进行SFT。
        2.  收集人工排序的比较响应对，并训练奖励模型IR以证明所生成的响应的质量。
        3.  在PPO强化学习框架下，通过使用IR计算的奖励来优化SFT模型（策略）。

    *   在第三阶段，为了缓解过拟合问题，当前模型权重和步骤1中的SFT模型权重之前KL引入了散度正则化

    *   <span style="color: #05a2ef">然而，尽管PPO训练在学习人类偏好方面非常有效，但其实施和稳定的训练却很困难。</span>

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B163.968%2C730.61%2C289.139%2C740.068%5D%2C%5B70.506%2C717.061%2C105.339%2C726.704%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“<span style="color: #eb52f7">Reward rAnked FineTuning (RAFT</span>)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 8</a></span>)</span>

    *   去掉了上述的PPO训练过程

    *   根据模型输出，使用现有的奖励模型来选择最佳的训练样本集。

        *   首先对一大批指令进行取样
        *   然后使用当前的LLMs来进行respond
        *   然后，这些数据将根据奖励模型进行排名，并且只有前1/k个实例被应用于SFT。

    *   RAFT也可以用于

        <span style="color: #ffcb00">离线人类偏好学习</span>

        ，其中全局指令集会不断更新为每个批次中排名靠前的指令。连续地更新全局指令集以提高每个步骤的训练数据质量。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B70.866%2C539.776%2C261.175%2C549.583%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“3.2 Offline Human Preference Training”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 8</a></span>)</span> 离线人类偏好训练

在线训练比较难，因为需要在行为策略、奖励、评估模型等过程的交互，需要调整超参数来活的更好的稳定性和性能

因此提出了离线方式学习人类偏好

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B70.866%2C383.656%2C222.841%2C393.463%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“3.2.1 Ranking-based Approach”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 8</a></span>)</span>基于排名的方法

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B165.295%2C309.978%2C290.941%2C319.621%5D%2C%5B70.866%2C296.429%2C120.893%2C306.072%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“Direct Preference Optimization (DPO)”</a></span> 由于人类的偏好通常以一组回应的排名结果来表达，因此一些研究工作直接将排名信息纳入到LLMs微调阶段中。

    *   隐式优化与现有的RLHF算法相同的目标，即具有KL散度项的奖励函数

    *   DPO的训练目标：

        *   ![\<img alt="" data-attachment-key="WLDT3HWR" width="776" height="160" src="attachments/WLDT3HWR.png" ztype="zimage">](attachments/WLDT3HWR.png)

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B259.431%2C148.838%2C290.943%2C159.612%5D%2C%5B70.866%2C136.256%2C222.41%2C145.899%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“Preference Ranking Optimization (PRO)”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 8</a></span>)</span> 进一步微调LLM来对齐人类偏好

    *   ![\<img alt="" data-attachment-key="S7A6U8IV" width="714" height="136" src="attachments/S7A6U8IV.png" ztype="zimage">](attachments/S7A6U8IV.png)
    *   PRO还为正则化目的添加了SFT训练目标。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B388.569%2C664.99%2C467.404%2C674.448%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“Zhao et al. (2023)”</a></span> <span style="color: #eb52f7">SLiC</span> 使用损失函数排名来训练，包括 rank loss、margin loss、list rank loss、 expected rank loss等。使用SFT训练目标和KL散度作为正则化项。

    *   使用KL散度项的排名损失表现最好。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B420.894%2C475.301%2C503.836%2C484.759%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“Yuan et al. (2023)”</a></span> <span style="color: #eb52f7">RRHF</span> 进一步优化LLaMA-7B，使用上述类似的框架来与人类偏好保持一致。

    *   基于list rank loss，但是根据经验去除了边界项
    *   RRHF发现，相对于KL散度，SFT训练目标在防止LLMs过拟合方面更加有效和高效。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B306.142%2C111.688%2C464.171%2C121.495%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=8">“3.2.2 Language-based Approach”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 8</a></span>)</span> 基于语言的方法

由于强化学习算法难以优化且LLMs具有较强的文本理解能力，一些研究提出通过SFT直接使用自然语言来注入人类偏好。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B74.356%2C730.61%2C203.755%2C740.068%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9"><span style="color: #eb52f7">“conditional behavior cloning”</span></a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 9</a></span>)</span> 训练LLMs以区分高质量和低质量的指导性回答。

    *   具体来说，他们为不同的质量回应设计了不同的基于语言的前缀。
    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B167.373%2C662.864%2C289.139%2C672.322%5D%2C%5B70.473%2C649.315%2C289.137%2C658.773%5D%2C%5B70.473%2C635.766%2C176.932%2C645.224%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“(e.g., high-quality response with “Assistant GPT4:” and low-quality response with “Assistant GPT3:”)”</a></span>
    *   这种方法可以有效地利用低质量和高质量的训练数据，将LLMs与人类对齐。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B223.41%2C608.668%2C290.941%2C618.126%5D%2C%5B70.866%2C595.118%2C205.595%2C604.576%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“Chain of Hindsight (CoH) (Liu et al., 2023b)”</a></span>

    *   ![\<img alt="" data-attachment-key="2NAJ6IQJ" width="764" height="592" src="attachments/2NAJ6IQJ.png" ztype="zimage">](attachments/2NAJ6IQJ.png)
    *   在将人工反馈分配给每个模型输出之后，COH将输入指令、LLMS输出和相应的人工反馈串联在一起作为LLMS的输入。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B273.683%2C258.199%2C289.139%2C267.657%5D%2C%5B70.866%2C244.65%2C128.42%2C254.108%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“Liu et al. (2022b)”</a></span>

    <span style="color: #eb52f7">Second Thoughts</span>

    训练语言模型生成源序列（即低质量回答）和目标序列（即高质量回答）之间的编辑操作，并将其整合到动态规划框架中。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B248.825%2C190.453%2C291.042%2C199.911%5D%2C%5B70.506%2C176.904%2C105.251%2C186.362%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“Liu et al. (2023d)”</a></span>

    <span style="color: #eb52f7">Stable Alignment </span>

    提出一种称为realignment的新型指令，根据先前生成的低质量反馈和指示进行修订

*   <span style="color: #eb52f7">SelFee (Ye et al., 2023a)</span>

    利用使用ChatGPT模型构建的自我纠正机制积累了一个多轮对话语料库。每个对话都以标准指示开始，在ChatGPT回应初始指令后，明确要求进行进一步的修订，直到ChatGPT选择终止。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B306.142%2C653.255%2C467.597%2C663.062%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“3.3 Parameter-Effective Training”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 9</a></span>)</span> 参数高效训练

直接微调大型语言模型（LLM）中的所有参数理论上可以使这些模型遵循提供的指令。然而，这种方法不仅需要大量的计算资源，如巨大的GPU内存，还需要广泛的指导训练数据集。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B410.092%2C513.273%2C526.216%2C522.916%5D%2C%5B306.142%2C499.724%2C333.635%2C509.367%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“Parameter-Effective Fine-tuning”</a></span> <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">(PEFT) 具体来说，这些方法冻结了大部分LLM参数，并只训练一组有限的额外参数。</span></span>

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B306.142%2C450.864%2C432.967%2C460.747%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9"><strong>“Supplementary Parameters”</strong></a></span>** 附加参数**

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B347.246%2C437.315%2C504.619%2C446.773%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“<span style="color: #eb52f7">prefix tuning (Li and Liang, 2021)</span>”</a></span> 和“<span style="color: #eb52f7">prompt tuning (Lester et al., 2021)</span>” 受到预训练语言模型中文本提示的成功应用的启发

    *   这些方法要么在输入层或每个隐藏层前添加可训练的标记，使得在微调期间 LLMs 的参数保持冻结状态。

*   <span style="color: #eb52f7">Unified Prompt </span>

    <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B424.469%2C342.471%2C505.014%2C351.929%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“Chen et al. (2023a)”</a></span>

    将这些策略整合到统一的框架中，促进了参数高效微调的更有效解决方案。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B306.142%2C280.062%2C401.77%2C289.945%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9"><strong>“Shadow Parameters”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 9</a></span>)</span>**

侧重于在推理过程中训练代表模型参数方差的权重，而不修改总模型参数数量。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B479.228%2C212.316%2C524.686%2C221.774%5D%2C%5B305.749%2C198.766%2C467.976%2C208.224%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=9">“<span style="color: #eb52f7">Low-Rank Adaptation (LoRA)</span> (Hu et al., 2022)”</a></span> 建议在现有的权重上添加一对可训练的秩分解权重矩阵（即更新矩阵），而这些权重保持冻结状态。

    *   尽管LoRA很有效，但它

        <span style="color: #05a2ef">在整个LLMs上平均分配参数预算，忽视了不同权重参数的重要性差异。</span>

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B174.528%2C703.512%2C220.884%2C712.97%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">AdaLoRA</span>”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span>

    AdaLoRA首先使用训练梯度计算参数重要性，然后确定不同参数矩阵的r值。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B70.866%2C635.766%2C106.718%2C645.224%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">QLoRA</span>”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span>

    通过减少内存使用量，进一步改进了LoRA，使得可以使用单个48G GPU对65B LLM进行微调。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B70.866%2C547.531%2C289.139%2C557.338%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><strong>“Trade-offs For Parameter-efficient Training”</strong></a></span>** <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span> 参数高效训练的权衡**

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B272.497%2C425.512%2C289.132%2C434.97%5D%2C%5B70.866%2C411.963%2C129.46%2C421.421%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“Sun et al. (2023a)”</a></span>

    Sun等人（2023a）发现，在相同的训练指令集下，具有LoRA的LLMs表现不如完全微调的模型。

*   在使用LoRA时，使用更大的LLMS比使用更大的训练指令集更好，因为前者解决方案所需的训练成本更低，并且比后者实现了更好的性能。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B70.866%2C293.558%2C201.273%2C304.306%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“4 Alignment Evaluation”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span> 评估

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B70.866%2C196.977%2C207.742%2C206.784%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“4.1 Evaluation Benchmarks”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span> 评估标准

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B162.672%2C152.326%2C268.782%2C161.969%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“Closed-set Benchmarks”</a></span>

    侧重于评估对齐的LLM的技能和知识

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B70.473%2C138.777%2C169.127%2C148.42%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“Open-set Benchmarks”</a></span>

    侧重于没有标准化答案的开放式情景

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B306.142%2C757.785%2C448.255%2C767.592%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“4.1.1 Closed-set Benchmarks”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 10</a></span>)</span>

其可能的答案是预先定义并限制在有限集合内，比如多选

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B306.142%2C634.541%2C399.448%2C644.424%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><strong>“General Knowledge”</strong></a></span>  常识

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B410.359%2C634.541%2C525.779%2C644.424%5D%2C%5B306.142%2C620.992%2C332.102%2C630.45%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">MMLU (Hendrycks et al., 2021)</span>”</a></span> 以英语为基础，用于评估零样本和少样本设置下的LLMs的知识

    *   它全面包含了来自57个学科的从初级水平到高级专业水平的问题，包括STEM、人文学科、社会科学等。
    *   MMLU的主题细致和广泛性使其成为识别LLM盲点的理想选择。

*   还有几个基准试图评估中文LLM的常识。

    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B438.505%2C499.049%2C525.776%2C508.507%5D%2C%5B306.142%2C485.5%2C337.042%2C494.958%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><span style="color: #eb52f7">“C-MMLU (Li et al., 2023c)”</span></a></span>
    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B342.729%2C485.5%2C466.408%2C494.958%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><span style="color: #eb52f7">“C-Eval (Huang et al., 2023)”</span></a></span>
    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B472.094%2C485.5%2C524.415%2C494.958%5D%2C%5B306.142%2C471.951%2C361.991%2C481.409%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><span style="color: #eb52f7">“M3KE (Liu et al., 2023a)”</span></a></span>
    *   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B382.817%2C471.951%2C508.66%2C481.409%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><span style="color: #eb52f7">“AGIEval (Zhong et al., 2023)”</span></a></span>
    *   都是MMLU的中文的对应版本，包含了来自多个学科、不同难度级别的各种问题，这些问题来自于中国各类标准化考试，包括高考、数学竞赛和法律考试。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B398.999%2C390.655%2C525.772%2C400.113%5D%2C%5B306.142%2C377.106%2C337.042%2C386.564%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">KoLA</span> benchmark (Yu et al., 2023a)”</a></span>

    用于评估LLMs的一般现实世界知识

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B306.142%2C339.494%2C355.603%2C349.377%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<strong>Reasoning</strong>”</a></span> 推理

在评估LLMs的算术、常识和符号推理能力方面有几个基准。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B450.374%2C244.65%2C524.415%2C254.108%5D%2C%5B306.142%2C231.1%2C360.744%2C240.558%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10"><span style="color: #eb52f7">“GSM8K (Cobbe et al., 2021)”</span></a></span><span style="color: #eb52f7">“Maths (Hendrycks et al., 2021)”</span>

    *   评估LLMs的算术推理能力。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B385.16%2C204.002%2C524.414%2C213.46%5D%2C%5B306.142%2C190.453%2C449.372%2C199.911%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">CSQA (Talmor et al., 2019)</span> and <span style="color: #eb52f7">StrategyQA</span> (Geva et al., 2021)”</a></span>

    *   常识推理能力要求LLMs在新颖的情境中运用日常生活常识进行推断。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B324.167%2C122.707%2C364.782%2C132.165%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“<span style="color: #eb52f7">Coin Flip</span>”</a></span>抛硬币 “<span style="color: #eb52f7">Last Letter Concatenation</span>”尾字母连接 （Wei et al. (2022b)）

    *   符号推理

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B432.103%2C95.609%2C525.772%2C105.067%5D%2C%5B306.142%2C82.059%2C331.797%2C91.517%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=10">“BBH (Suzgun et al., 2022)”</a></span>

    *   专注于评估广泛的推理技能，如日期理解、词语分类和因果判断。

<span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C720.097%2C105.494%2C729.98%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11"><strong>“Coding”</strong></a></span>** 代码**

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B116.403%2C720.097%2C264.997%2C729.98%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">HumanEval</span> (Chen et al., 2021)”</a></span> “<span style="color: #eb52f7">HumanEval+ </span>(Liu et al., 2023c)” “<span style="color: #eb52f7">MBPP</span> (Austin et al., 2021)”

    *   是广泛使用的基准测试来评估LLMs的编码技能。
    *   它们涵盖了大量的Python编程问题和相应的测试用例，以自动验证Code LLMs生成的代码。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B273.62%2C638.801%2C290.948%2C648.259%5D%2C%5B70.048%2C625.252%2C216.214%2C634.71%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">DS-1000</span>  (Lai et al., 2022)”</a></span>

    <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 11</a></span>)</span>

    包括1000个不同的数据科学工作流程，涵盖了七个库。它根据测试用例评估代码生成的性能，并支持两种评估模式：完成和插入。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C547.068%2C222.088%2C556.875%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“4.1.2 Open-ended Benchmarks”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 11</a></span>)</span> 开放式基准

开放式基准的回答可以更加灵活多样，通常给予对齐的语言模型聊天式问题或没有固定参考答案的主题。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B218.904%2C461.437%2C290.945%2C470.895%5D%2C%5B70.866%2C447.888%2C141.86%2C457.346%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">Vicuna-80 </span>(Chiang et al., 2023)”</a></span> “<span style="color: #eb52f7">Open-Assistant-953 </span>(Kopf et al., 2023)” “<span style="color: #eb52f7">User-Instructions-252</span> (Wang et al., 2022a)”

    *   通常利用来自LLMS的少量语法指令作为测试实例。
    *   所有评估候选的LLM都会收到相同的指示来提供回答，然后这些回答将与基于人类或基于LLMs的评估者进行比较评估。
    *   然而，这些类型的基准测试只能同时比较几个LLM，很难揭示在广泛范围的LLM中进行公平比较以及新的LLM可用时的增量更新。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B115.234%2C285.297%2C256.569%2C294.755%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">AlpacaEval</span> (Dubois et al., 2023)”</a></span>

    通过将LLMs候选人的胜率Win Rate报告给参考LLM text-davinci-003来解决这个问题。具有更高胜率的LLMs通常比胜率较低的LLMs更好。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C217.551%2C211.526%2C227.009%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">MT-Bench</span> (Zheng et al., 2023)”</a></span>

    通过提出80个多轮评估实例，进一步增加了评估的难度，并希望LLMs能够有效地捕捉前几轮的上下文信息。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C163.355%2C181.036%2C172.813%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“<span style="color: #eb52f7">FLASK</span> (Ye et al., 2023b)”</a></span> 对对齐的LLMs进行细粒度评估。

    *   FLASK包含来自120个数据集的1,700个实例。
    *   每个测试实例都标有一组12项基础和必要的“对齐技能”（例如，逻辑思维、用户对齐等）。
    *   因此，很容易单独评估LLMS在这些技能上的能力。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B306.142%2C757.785%2C430.178%2C767.592%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“4.2 Evaluation Paradigm”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 11</a></span>)</span> 评估范式

由于开放式基准往往没有参考答案，因此依赖外部人类或LLMs评估者是至关重要的。在本节中，我们将介绍基于人类和LLMs的评估范式。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B306.142%2C664.469%2C457.877%2C674.276%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“4.2.1 Human-based Evaluation”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 11</a></span>)</span> 基于人类的评估

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B358.83%2C553.279%2C525.138%2C562.737%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“Wang et al. (2022a); Wu et al. (2023)”</a></span>  <span style="color: #eb52f7">Ordinal Classification</span>

    *   指示人类注释员将每个回答分别归类为四个级别中的一个(即，可接受、小错误、重大错误和不可接受)。
    *   然而，其他一些研究发现，这种分类标注策略严重依赖注释者的主观性，这可能导致评分者之间的可靠性较差

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B425.68%2C417.788%2C505.092%2C427.246%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“Taori et al. (2023)”</a></span> <span style="color: #eb52f7">Pairwise Comparison</span>

    *   使用成对比较框架来评估两个LLMS系统的输出质量。
    *   给定指令输入和两个模型输出，人类注释员被要求选择一个更好的。

*   <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B339.044%2C336.492%2C525.139%2C345.95%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“Zheng et al. (2023); Dettmers et al. (2023)”</a></span>  <span style="color: #eb52f7">Elo</span>

    *   基于每次成对比较的结果和当前玩家分数来更新玩家分数。

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B306.142%2C233.897%2C451.811%2C243.704%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=11">“4.2.2 LLMs-based Evaluation”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 11</a></span>)</span> 基于LLMs的评估

*   人类评估效率低下，价格昂贵
*   将LLMS融入到各种自然语言处理任务的输出文本评估中，而不需要额外的昂贵参考和人力。

**Reference-Free Evaluation**

*   <span style="color: #eb52f7">GPTEval </span>(Liu et al., 2023e), <span style="color: #eb52f7">GPTScore</span> (Fu et al., 2023), <span style="color: #eb52f7">Explicit Score</span> (Chen et al., 2023d), <span style="color: #eb52f7">LM Examiner</span> (Chiang and Lee, 2023)

    *   建议在广泛的自然语言生成(NLG)任务中直接使用LLMS来评估生成的文本质量，而不需要单一的参考。
    *   具体地说，他们构建了复杂的输入指令，包括任务背景和评价规则，并提示LLMS遵循这些评价指令为输出文本提供分数。
    *   也有一些研究为特定的NLG任务提出了基于LLMS的评估框架，包括文本摘要、代码生成、开放式QA、和对话。
    *   由于prompt的灵活性，也有可能对生成的文本进行多维评估(Lin和Chen，2023；Fu等，2023)。

*   <span style="color: #eb52f7">FactScore</span> (Min et al., 2023), <span style="color: #eb52f7">Alignscore</span> (Zha et al., 2023)

    *   对生成的文本进行多维评估

*   两个LLMs成对进行比较

    *   为了比较两个LLM的能力，Dubois等人（2023）和Zheng等人（2023）明确要求GPT-4根据相同的指令输入选择更好的回应，而不是分别给出评分。

**LLMs Bias in Evaluation**

*   <span style="color: #eb52f7">Positional Bias</span> (Wang et al., 2023b)

    *   基于LLM的评估范式存在

        <span style="background-color: #ff666680">位置偏差</span>

    *   并且那些强大的LLMs（即GPT-4）倾向于给首次出现的候选者分配更高的分数。

    *   修正位置偏差：

        *   用不同的候选排序多次重复LLM评估过程
        *   在分配实际得分之前明确要求LLMs提供评估的chain of thought

*   <span style="color: #eb52f7">Multi-Elo</span> (Wu and Aji, 2023)

    *   基于LLM的评估更倾向于选择存在

        <span style="background-color: #ff666680">事实错误</span>

        的候选，而不是较短或者有语法错误的候选，尽管前者可能带来比后者更大的危险。

    *   解决：

        *   提出了多维度的Elo评级系统，从准确性、帮助性和语言角度分别评估候选
        *   这种方法可以比以前的一次性评估更全面地了解候选的质量

*   <span style="color: #eb52f7">LLM-as-a-Judge</span> (Zheng et al., 2023)

    *   除了位置偏见和长度偏差之外，他们还发现了

        <span style="background-color: #ff666680">自我增强偏差</span>

        ，这意味着LLMs更喜欢自己的回答而不是来自其他来源的回答。

    *   解决：

        *   交换回答
        *   添加少样本示例
        *   利用CoT和参考信息。

**LLMs for Evaluation**

尽管取得了高质量的自动评估结果，上述方法严重依赖于最先进的闭源LLM（例如GPT-4），这可能导致数据隐私问题。

*   <span style="color: #eb52f7">LLM-as-a-Judge</span> (Zheng et al., 2023)

    *   提出训练特定于评估的LLM。

*   PandaLM (Wang et al., 2023c)

    *   通过使用从GPT-3.5生成的约300K个高质量合成评估指令对LLaMA-7B进行微调，从而得到专门评估LLMs的工具。
    *   具体来说，他们首先收集了大量的指令以及来自各种开源LLM（如LLaMA-7B和Bloom-7B）的输出。
    *   然后他们提示GPT-3.5分析和评估一对输出的质量。
    *   他们在人工注释的元评估上的结果显示，尽管规模要小得多，PandaLM 在评估性能方面与 GPT-3.5 和 GPT-4 相当。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2212%22%2C%22position%22%3A%7B%22pageIndex%22%3A11%2C%22rects%22%3A%5B%5B306.142%2C370.642%2C495.333%2C381.39%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2212%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=12">“5 Challenges and Future Directions”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2212%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 12</a></span>)</span>

LLM对齐的发展仍处于初级阶段，因此还有很大的改进空间。

在本节中，我们将在表1中总结与人类对齐LLMs的现有重要研究工作。

![\<img alt="" data-attachment-key="FQKMQB2Y" width="1564" height="950" src="attachments/FQKMQB2Y.png" ztype="zimage">](attachments/FQKMQB2Y.png)

接下来，我们将讨论一些挑战以及相应的未来研究方向。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2212%22%2C%22position%22%3A%7B%22pageIndex%22%3A11%2C%22rects%22%3A%5B%5B306.142%2C244.726%2C524.415%2C254.533%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2212%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=12">“Fine-grained Instruction Data Management”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2212%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 12</a></span>)</span> 细粒度指令数据管理

利用来自不同来源的训练指令，在不同方法之间进行公平比较变得具有挑战性

FLAN和编程指令可以提高与LLMs（Ghosal等人，2023年）对齐的推理能力，并且ShareGPT在各种基准测试中表现良好

在其他方面的指令数据管理中仍存在许多问题尚不清楚，包括对指令数据的最佳质量控制、最佳指令训练顺序以及如何有效地混合不同的指令。

这些研究工作最终可以实现精细化的指导管理

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2213%22%2C%22position%22%3A%7B%22pageIndex%22%3A12%2C%22rects%22%3A%5B%5B70.866%2C360.032%2C289.139%2C369.839%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=13">“LLMs Alignment for non-English Languages”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 13</a></span>)</span> 非英语语言的LLMs对齐

*   这些对齐技术在各种语言中特别是低资源语言中的表现如何
*   如何有效地将LLMs对齐效果跨不同语言进行转移。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2213%22%2C%22position%22%3A%7B%22pageIndex%22%3A12%2C%22rects%22%3A%5B%5B70.866%2C163.355%2C265.86%2C173.238%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=13">“LLMs Alignment Training Technologies”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 13</a></span>)</span> LLMs对齐训练技术

*   大多数现有的对齐LLMs都是基于简单的SFT技术。

*   然而，

    <span style="color: #05a2ef">SFT并没有明确地将人类偏好纳入到LLMs中</span>

    。

*   因此，仅基于SFT来对齐LLMs可能需要更多的指导数据和培训资源。

*   总的来说，对于将人类偏好融入到LLMs中的各种训练技术的影响缺乏全面的调查。

*   <span style="color: #ff2020">提出资源受限的LLM比对培训框架至关重要</span>

*   随着越来越多的指令数据可用，这种探索可以进一步促进有效且环保友好的LLM对齐解决方案。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2213%22%2C%22position%22%3A%7B%22pageIndex%22%3A12%2C%22rects%22%3A%5B%5B306.142%2C285.373%2C526.225%2C295.18%5D%2C%5B306.142%2C271.748%2C340.136%2C281.631%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=13">“Human-in-the-loop LLMs Alignment Data Generation”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2213%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 13</a></span>)</span> 人在循环中的LLMs对齐数据生成

*   ShareGPT数据已被广泛用于LLMs对齐，ShareGPT在各种自然语言处理任务中表现一致良好

*   这些结果表明，

    <span style="color: #ff2020">人类</span>

    仍然是提高LLMs对齐质量的关键因素。

*   ShareGPT是一种以人为中心的对齐解决方案，其中人类可以自由确定LLMs应该生成什么内容。

*   这显示了以人为中心的数据生成解决方案在LLMs对齐中具有巨大潜力。

*   未来：探索其他类型的以人为中心的解决方案进一步促进LLMs对齐

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2214%22%2C%22position%22%3A%7B%22pageIndex%22%3A13%2C%22rects%22%3A%5B%5B70.866%2C757.785%2C289.439%2C767.592%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2214%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=14">“Human-LLM Joint Evaluation Framework”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2214%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 14</a></span>)</span> 人类-LLM联合评估框架

*   现有的LLM评估框架要么使用LLMS进行有效评估，要么利用众包进行高质量评估
*   可以将LLMs作为特殊的评估标注者，并开发LLM-人类联合评价框架，在此框架中根据它们自身的优势分配不同的评价任务给LLMs和人类，以保持对于LLM对齐过程既高效又具有质量。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FXWFBI4XF%22%2C%22pageLabel%22%3A%2214%22%2C%22position%22%3A%7B%22pageIndex%22%3A13%2C%22rects%22%3A%5B%5B70.866%2C570.097%2C145.933%2C580.845%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2214%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/XWFBI4XF?page=14">“6 Conclusion”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FMPND5R5Z%22%5D%2C%22locator%22%3A%2214%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/MPND5R5Z">Wang et al., 2023, p. 14</a></span>)</span>

该调查提供了对最新的LLMs对齐技术进展的综述。我们将这些研究努力总结为对齐指令收集、对齐训练和对齐评估。最后，我们指出了几个有前景的未来方向，以改善LLMs的对齐。希望这项调查能够提供深入的观点，并激发进一步研究，改善LLMs的对齐。
