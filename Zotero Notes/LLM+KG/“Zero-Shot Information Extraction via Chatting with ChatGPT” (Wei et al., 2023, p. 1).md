---
tags: []
parent: 'Zero-Shot Information Extraction via Chatting with ChatGPT'
collections:
    - LLM+KG
version: 13310
libraryID: 1
itemKey: INLVCUZ6

---
# <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B106.505%2C749.141%2C489.247%2C762.038%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=1">“Zero-Shot Information Extraction via Chatting with ChatGPT”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 1</a></span>)</span>

Referred in <a href="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=34" rel="noopener noreferrer nofollow" zhref="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=34" ztype="znotelink" class="internal-link">LLM</a>ç

**Zero-shot information extraction (IE)：**零样本信息提取（IE）旨在从未标注的文本中构建IE系统。

将<span style="color: #ff2020">零样本信息抽取任务转化为一个两阶段框架（ChatIE）的多轮问答问题</span>。

凭借ChatGPT的能力，对框架在三个信息抽取任务上进行了广泛评估：

1.  实体关系三元组提取 entity-relation triple extract (RE)
2.  命名实体识别 named entity recognition (NER)
3.  事件抽取 event extraction (EE)

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B70.866%2C284.283%2C153.68%2C295.031%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=1">“1 Introduction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 1</a></span>)</span>

在一个统一的框架下，促使LLMs进行零样本信息抽取任务是否可行？

包含多个依赖元素的结构化数据很难通过一次预测来提取，尤其对于一些复杂任务如关系抽取而言。

*   将这些复杂任务分解为不同的部分，并训练多个模块来解决每个部分。

    *   首先识别两个实体，然后预测它们之间的关系。
    *   通过先提取主语，然后根据关系模板提取宾语，将关系抽取看作是一个问答过程

将<span style="color: #ff2020">零样本信息抽取任务转化为一个两阶段框架（ChatIE）的多轮问答问题</span>。

1.  找出句子中可能存在的对应成分类型。
2.  对阶段1中的每个元素类型执行链式信息提取。

每个阶段都采用了多轮问答的流程来实施。在每个回合中，我们根据设计的模板和先前提取的信息构建提示作为输入来询问ChatGPT。最后，我们将每个轮次的结果组合成结构化数据。

经验证实，当没有使用ChatIE的普通ChatGPT在解决原始任务指令中的信息提取时失败，而我们提出的<span style="color: #ff7700">基于ChatGPT实例化的两阶段框架在将信息提取任务分解为多个更简单、更容易的子任务</span>时成功。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B70.866%2C311.291%2C126.661%2C322.039%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=2">“2 ChatIE”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%222%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 2</a></span>)</span>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%222%22%2C%22position%22%3A%7B%22pageIndex%22%3A1%2C%22rects%22%3A%5B%5B70.866%2C290.009%2C283.932%2C299.816%5D%2C%5B95.412%2C276.46%2C106.932%2C286.267%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%222%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=2">“2.1 Multi-Turn QA framework for zero-shot IE”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%222%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 2</a></span>)</span>

**第一阶段**：目标是分别在三个任务中找出句子中<span style="color: #ff7700">已存在的实体、关系或事件类型</span>。

*   <span style="color: #ff7700">筛选掉不存在的元素类型，以减少搜索空间和计算复杂度，有助于提取信息。</span>

*   对于一个样品，这一阶段通常只包括一轮QA

*   为了找到句子中呈现的元素类型，我们首先利用

    <span style="color: #ff7700">特定任务的TypeQuesTemplates</span>

    和

    <span style="color: #ff7700">元素类型列表</span>

    来构建问题。

*   将问题和句子结合作为输入传递给ChatGPT。

*   为了方便提取答案，我们要求系统以列表形式回复。

*   如果句子中不包含任何元素类型，则返回NONE

**第二阶段**：我们根据第一阶段提取的元素类型以及相应的任务特定方案进一步提取相关信息。

*   这个阶段通常包括多个问答环节。

*   针对元素类型设计了一系列特定的ChainExtractionTemplates。

    *   定义了一系列

        <span style="color: #ff7700">模板链</span>

        ，链的长度通常为1

    *   但对于复杂的方案，例如在实体关系三元组提取中进行复杂对象值提取，链的长度大于一。

    *   在这一点上，元素的提取可能取决于另一个先前的元素，因此我们称之为链式模板。

*   我们按照先前提取的元素类型和ChainExtractionTemplates的顺序进行多轮问答。

*   生成问题时，我们需要检索带有元素类型的模板，并在必要时填充相应的插槽。

*   然后通过ChatGPT来生成相应

*   最后，我们根据每个回合中提取的元素组成结构化信息。

*   同样地，为了方便提取答案，我们要求系统以表格形式回复。如果没有提取到任何内容，系统将生成一个NONE响应。

![\<img alt="" data-attachment-key="G6SEBGAV" width="1726" height="1076" src="/attachments/G6SEBGAV.png" ztype="zimage">](/attachments/G6SEBGAV.png)

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C707.939%2C265.637%2C717.746%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“2.2 Applying the Framework to IE tasks”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C628.333%2C259.146%2C638.14%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“2.2.1 Entity-Relation Triple Extraction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

**output triple (s, r, o):**![\<img alt="" data-attachment-key="KYN9X7DP" width="300" height="60.705882352941174" src="/attachments/KYN9X7DP.png" ztype="zimage">](/attachments/KYN9X7DP.png)

*   语句x
*   问题prompt p
*   q1是使用关系类型列表R和阶段I中相应模板生成的问题。
*   qr是在第二阶段中使用与先前提取的关系类型相关的模板生成的问题。

值得注意的是，在第二阶段我们省略了x，因为ChatGPT可以记录每个问答环节的相关信息。

此外，我们还需要对具有复杂对象值（复杂对象值是指具有多个属性的对象）的样本进行进一步的几轮QA

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C325.521%2C227.226%2C335.328%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“2.2.2 Named Entity Recognition”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

*   第一阶段是根据所需类型列表过滤出句子中的现有实体类型。
*   第二阶段，每一轮的目标是提取一种类型的实体。

因此，<span style="color: #ff7700">第二阶段的轮次取决于第一阶段获得的实体数量</span>，如果第一阶段没有获取到任何类型，则省略第二阶段。ChatGPT对BIO标注有些困难，所以没有考虑。

> <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">BIO annotation 是一种常用于命名实体识别 (Named Entity Recognition, NER) 的标注方法。在这种标注方法中，每个词都被标注为以下三种类别之一：</span></span>
>
> *   **<span style="color: var(--tw-prose-bold)"><span style="background-color: rgb(247, 247, 248)">B</span></span>**
>
>     <span style="background-color: rgb(247, 247, 248)">: 表示实体的开始 (Beginning)。例如，在实体 "New York" 中，"New" 会被标注为 "B"。</span>
>
> *   **<span style="color: var(--tw-prose-bold)"><span style="background-color: rgb(247, 247, 248)">I</span></span>**
>
>     <span style="background-color: rgb(247, 247, 248)">: 表示实体的内部 (Inside)。继续上面的例子，"York" 会被标注为 "I"。</span>
>
> *   **<span style="color: var(--tw-prose-bold)"><span style="background-color: rgb(247, 247, 248)">O</span></span>**
>
>     <span style="background-color: rgb(247, 247, 248)">: 表示这个词不是任何实体的一部分 (Outside)。</span>
>
> <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">例如，对于句子 "Alice lives in New York."，其BIO标注可能是：</span></span>
>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">Alice: B-PERSON</span></span>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">lives: O</span></span>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">in: O</span></span>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">New: B-LOCATION</span></span>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">York: I-LOCATION</span></span>
> *   <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">.: O</span></span>
>
> <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">这里，"Alice" 被标注为一个人名的开始，而 "New York" 被标注为一个地点名的开始和内部。</span></span>
>
> <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">BIO标注方法的主要优点是它可以轻松地标注多词实体，并且可以轻松地将其转换为其他格式。此外，它还可以用于标注嵌套的实体，尽管这需要更复杂的标注策略。</span></span>
>
> <span style="color: rgb(55, 65, 81)"><span style="background-color: rgb(247, 247, 248)">总的来说，BIO标注是NER任务中的一种简单而有效的标注策略。</span></span>

#### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C98.346%2C183.175%2C108.153%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“2.2.3 Event Extraction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

以流水线方式分为两个阶段解决：

*   事件分类

    *   进行事件分类，将其形式化为从给定文本中获取事件类型的文本分类问题。

*   论元argument extraction抽取

    *   形式化为一种抽取式机器阅读理解（MRC）问题，该问题可以从第一阶段预测的事件类型中识别出特定事件的论元

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B306.142%2C620.359%2C384.508%2C631.107%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“3 Experiment”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B306.142%2C596.054%2C357.36%2C605.861%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=3">“3.1 Setup”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 3</a></span>)</span>

**Datasets**

**Evaluation Metrics**

*   RE

    *   F1
    *   border evaluation (BE)：边界评估（BE），如果提取的关系三元组（主语，关系，宾语）中的整个实体跨度以及关系都是正确的，则被视为正确。
    *   strict evaluation (SE)：严格评估（SE）：除了边界评估所要求的内容外，主语和宾语的类型也必须正确。

*   NER

    *   F1
    *   complete matching

*   EE

    *   F1 word-level matching
    *   F1 entity-level matching

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B70.866%2C381.342%2C156.928%2C391.149%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=4">“3.2 Main Results”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 4</a></span>)</span>

![\<img alt="" data-attachment-key="94B7Z4T9" width="1710" height="730" src="/attachments/94B7Z4T9.png" ztype="zimage">](/attachments/94B7Z4T9.png)

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%224%22%2C%22position%22%3A%7B%22pageIndex%22%3A3%2C%22rects%22%3A%5B%5B306.142%2C321.289%2C381.531%2C332.037%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%224%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=4">“4 Case Study”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%224%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 4</a></span>)</span>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B70.866%2C255.065%2C268.473%2C265.813%5D%2C%5B88.799%2C241.117%2C127.761%2C251.865%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=5">“5 Vanilla Prompt vs. Our Chat-based Prompt”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 5</a></span>)</span>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B70.866%2C164.431%2C159.956%2C175.179%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=5">“6 Related Work”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 5</a></span>)</span>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2F7WRJNNXP%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B306.142%2C501.864%2C381.209%2C512.612%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/7WRJNNXP?page=5">“7 Conclusion”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FDRPPNSAS%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/DRPPNSAS">Wei et al., 2023, p. 5</a></span>)</span>

我们提出了ChatIE，这是一个基于ChatGPT的多轮问答框架，用于零-shot信息抽取。通过交互模式，ChatIE可以将复杂的信息抽取任务分解为几个部分，并将每一轮的结果组合成最终的结构化结果。我们将该框架应用于关系抽取（RE）、命名实体识别（NER）和事件抽取（EE）任务，并在两种语言下对六个数据集进行了广泛实验以验证其有效性。令人惊讶的是，ChatIE在几个数据集上表现出色，甚至超过了一些全样本模型。这项工作为零-shot信息抽取开辟了新的范式，在这种范式中，专家们将信息抽取任务分解为多个更简单、更容易处理的子任务，并定义类似聊天对话的提示语句，直接运行这些规格说明而无需进行训练和微调。
