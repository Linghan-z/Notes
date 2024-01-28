---
tags: []
parent: 'Lost in the Middle: How Language Models Use Long Contexts'
collections:
    - LLM+KG
version: 13020
libraryID: 1
itemKey: 3FU8FQ3T

---
# <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B106.591%2C749.141%2C488.688%2C762.038%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=1">“Lost in the Middle: How Language Models Use Long Contexts”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 1</a></span>)</span>

Comment: 19 pages, 18 figures

Referred in <a href="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=35" rel="noopener noreferrer nofollow" zhref="zotero://note/u/LJSU8E3B/?ignore=1&#x26;line=35" ztype="znotelink" class="internal-link">LLM</a>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B157.758%2C615.833%2C202.243%2C626.581%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=1">“Abstract”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 1</a></span>)</span>

使用更长的上下文

本文分析了语言模型在两个任务上的性能，这两个任务要求在输入上下文中识别相关信息：

1.  多文档qa
2.  键值检索

实验发现：

1.  信息在输入上下文的头尾处， 性能高，在输入上下文的中间明显下降
2.  上下文变长，性能显著降低

语言模型如何使用其输入上下文，并为未来长上下文模型提供了<span style="color: #ffcb00">新的评估</span>方法。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B70.866%2C353.47%2C153.68%2C364.218%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=1">“1 Introduction”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 1</a></span>)</span>

Transformer对于长序列来说，<span style="color: #05a2ef">可伸缩性比较差，因为自注意力机制的复杂度与输入序列长度呈二次关系</span>

因此语言模型通常使用相对<span style="color: #ffcb00">较小的</span>上下文窗口进行训练。

有些改进的方法可以使语言模型使用长的上下文窗口，但是在执行下游任务时，这些扩展上下文语言模型如何利用其输入上下文仍然不清楚。

实验：

*   开源：MPT-30B-Instruct, LongChat-13B (16K)

*   闭源：OpenAI’s GPT-3.5-Turbo and Anthropic’s Claude-1.3

*   多文档问答：需要模型通过对提供的文档进行推理，找到相关信息并使用它来回答给定的问题。他的任务模仿了许多商业生成式搜索和问答应用程序（例如Bing Chat）背后的检索增强生成设置。

    *   改变输入的上下文的大小和位置，研究对模型的性能的影响
    *   结果就是相关的上下文信息在最开始和在最后性能好，在中间性能差很多
    *   GPT-3.5-Turbo的实验中，把相关的上下文放在中间，甚至不如不提供上下文性能好
    *   在较长的上下文中，模型的性能会下降
    *   具有扩展上下文的模型extended-context models并不一定更擅长利用其输入上下文
    *   ![\<img alt="" data-attachment-key="ERHJFP67" width="400" height="383" src="/attachments/ERHJFP67.png" ztype="zimage">](/attachments/ERHJFP67.png)

<span style="color: #ff2020">语言模型能从其输入上下文中检索到什么程度？</span>

*   通过一个合成的键值检索任务来研究这个问题

    *   从输入上下文中检索匹配token的基本能力的最小测试平台
    *   模型被赋予一组以JSON格式编码的键值对集合，并且必须返回与特定键相关联的值。
    *   控制输入上下文的长度以及相关信息的位置

<span style="color: #ff7700">为啥语言模型对于中间的输入上下文的检索能力差？</span>

分析：

*   模型架构：(decoder-only vs. encoder-decoder)
*   query-aware contextualization查询感知的上下文化（文中解释的是：在文档或键值对之前和之后放置查询**）**
*   指令微调

发现：

*   encoder-decoder架构的模型，在其训练的指令长度内的上下文输入中，对于位置变化是具有鲁棒性的，但是当长度再提升，就又有了U型的现象
*   查询感知的上下文化：对于key-value检索的任务提升比较大，但是对于多文档检索来说没啥用
*   base language models（没有指令微调的）语言模型，在改变上下文的位置的时候也会有U型曲线

案例研究：<span style="color: #ff2020">检索读取模型</span>可以更好地理解将<span style="color: #ff7700">更多信息添加到输入上下文</span>和<span style="color: #ff7700">增加模型需要推理的内容量</span>之间的权衡

*   在开放域问答环境中，与问题相关的前k个文档可能没有或有很多相关答案。
*   当从wikipedia检索NaturalQuestions-Open中的问题时，发现模型性能在检索器召回率达到稳定之前就已经饱和了，表明模型未能有效地利用额外检索到的文档——使用超过20个检索到的文档只能稍微提高性能(∼1.5% for GPT-3.5-Turbo and ∼1% for claude-1.3)

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C638.029%2C179.467%2C648.777%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=3">“2 Language Models”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 3</a></span>)</span>

<span style="color: #ff2020">Transformer的时间和内存的复杂度都是与上下文长度成二次方，所以限制了训练的toklen长度</span>

**Increasing language model maximum context length.**

*   GPT-4 最大的上下文窗口context window 为32K token

*   Claude 从8K提升到了100K

*   GPT-3.5-Turbo 16K

*   开源：

    *   MPT-30B 8K
    *   LongChat-7B 16K

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B70.866%2C123.363%2C280.74%2C134.111%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=3">“3 Multi-Document Question Answering”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 3</a></span>)</span>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%223%22%2C%22position%22%3A%7B%22pageIndex%22%3A2%2C%22rects%22%3A%5B%5B306.142%2C649.475%2C423.72%2C659.282%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=3">“3.1 Experimental Setup”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%223%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 3</a></span>)</span>

多文档问答任务与<span style="color: #ff7700">商业搜索</span>和<span style="color: #ff7700">问答应用程序基础上的检索增强生成（Bing Chat）</span>设置密切相关

在他们的实验设置中，模型的输入：

1.  一个需要回答的问题
2.  k个文档（例如，来自维基百科的段落），其中恰好有一个文档包含问题的答案，而k-1个“干扰”文档则不包含。

执行此任务需要模型访问包含答案的文档，并在其输入上下文中使用它来回答问题。

![\<img alt="" data-attachment-key="6BI4CDR4" width="1750" height="750" src="/attachments/6BI4CDR4.png" ztype="zimage">](/attachments/6BI4CDR4.png)

实验设计：

*   NaturalQuestions-Open

*   在输入上下文中，使用维基百科的段落（最多100个token）作为文档

*   只有一个文档包含答案（wikipedia中的包含答案的段落）

*   剩下的k-1的文档不包含答案信息

    *   Contriever retrieval system 检索k-1个与问题最相关但是不包含答案（NaturalQuestions-annotatedanswer）
    *   输入的时候，k-1个文档的相关性逐渐降低
    *   Appendix A：包含歧义的信息的文档
    *   Appendix B：随机的文档
    *   Appendix C：干扰文档随机排序

*   改变上下文长度：

    *   添加不包含答案的文档

*   改变相关信息的位置：

    *   调整包含答案的文档的位置![\<img alt="" data-attachment-key="QNCSPV7J" width="400" height="418" src="/attachments/QNCSPV7J.png" ztype="zimage">](/attachments/QNCSPV7J.png)

*   evaluation metric评估指标：

    *   准确率 acc：输出中是否出现正确的答案（取自NaturalQuestions注释）

*   为了防止模型通过简单地复制输入上下文中的文档来利用度量标准，我们会删除第一个生成的换行符之后的模型输出。

    *   在实践中，模型的回答通常是一个句子或段落；生成过程会在不产生任何换行符的情况下终止（通过生成一个序列结束标记）。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B70.866%2C509.629%2C129.35%2C519.436%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=5">“3.2 Models”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 5</a></span>)</span>

开源：

*   MPT-30B-Instruct——8K

    *   最初使用2048个token序列在1t个token上进行预训练
    *   然后使用8192个token序列进行的50btoken上进行预训练

*   LongChat-13B ——16K

    *   这是在LLaMA-13B的基础上构建的（原始最大上下文窗口为2048个token）
    *   在16384个token 序列的微调之前使用condensed rotary positional embeddings，将其上下文窗口扩展到16384个token的长度

闭源：

*   GPT-3.5-Turbo——4K
*   GPT-3.5-Turbo——16K（0613）
*   Claude-1.3——8K
*   Claude1.3 ——100K

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%225%22%2C%22position%22%3A%7B%22pageIndex%22%3A4%2C%22rects%22%3A%5B%5B306.142%2C493.868%2C436.768%2C503.675%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%225%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=5">“3.3 Results and Discussion”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%225%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 5</a></span>)</span>

![\<img alt="" data-attachment-key="REZENQ4A" width="1744" height="738" src="/attachments/REZENQ4A.png" ztype="zimage">](/attachments/REZENQ4A.png)

closed-book setting：不给任何的上下文，根据经验进行作答

oracle setting：只给包含相关信息的上细纹，并且要求必须根据上下文进行作答

**GPT-3.5-Turbo and GPT-3.5-Turbo (16K) have the<span style="color: #ff2020"> highest </span>closedbook (55%) and oracle (88%) performance**

Appendix E：**closed-book\&oracle**

![\<img alt="" data-attachment-key="4D4LSVYW" width="400" height="203" src="/attachments/4D4LSVYW.png" ztype="zimage">](/attachments/4D4LSVYW.png)

Appendix D：**GPT-4**\
![\<img alt="" data-attachment-key="XFXUNKAK" width="400" height="465" src="/attachments/XFXUNKAK.png" ztype="zimage">](/attachments/XFXUNKAK.png)

实验结果比别的模型好很多，但是也有U型的趋势

**结论**：

1.  **<span style="color: #ff2020">Model performance is highest when relevant information occurs at the beginning or end of its input context. 当相关信息出现在输入上下文的开头或结尾时，模型性能最高。</span>**

    1.  在20和30个文档的设置中的性能低于没有任何输入文档的性能（56.1%）
    2.  **在执行下游任务时，当前模型无法有效地推理整个上下文窗口，并且模型在检索和使用输入上下文的开头或结尾处的信息时更容易。**

2.  **<span style="color: #ff2020">Model performance substantially decreases as input contexts grow longer.模型性能随着输入上下文的增加而显著降低。</span>**

    1.  使用上下文增强的模型也不行，比如使用GPT-3.5-Turbo，20个文档的时候（相关的上下文在10-20之间），最低是52.9%，但是超过20个文档，就超过了限制了，于是使用GPT-3.5-Turbo 16K，30个文档（相关的上下文10-30之间），最低是49.5%。说明：**3**

        ![\<img alt="" data-attachment-key="QFQQPNAZ" width="400" height="449" src="/attachments/QFQQPNAZ.png" ztype="zimage">](/attachments/QFQQPNAZ.png)

3.  **<span style="color: #ff2020">Extended-context models are not necessarily better at using input context.扩展上下文模型并不一定更擅长利用输入的上下文。</span>**

    1.  GPT-3.5-Turbo 和 GPT-3.5-Turbo (16K) 几乎结果是重叠的（

        <span style="color: #ff7700">紫色和棕色，最上面的那两条（看起来像一条）</span>

        ）

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B306.142%2C557.606%2C491.89%2C568.354%5D%2C%5B324.075%2C543.659%2C483.928%2C554.407%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=6">“4 How Well Can Language Models Retrieve From Input Contexts?”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 6</a></span>)</span>

通过一个合成的键值检索任务来研究这个问题，以隔离和研究从输入上下文中匹配和检索相关信息的基本能力。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%226%22%2C%22position%22%3A%7B%22pageIndex%22%3A5%2C%22rects%22%3A%5B%5B306.142%2C400.383%2C423.72%2C410.19%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%226%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=6">“4.1 Experimental Setup”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%226%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 6</a></span>)</span>

输入：

1.  一个包含k个键值对的字符串序列化JSON对象，其中每个键和值都是唯一的、随机生成的UUID。
2.  前面提到的JSON对象的特定键

目标是返回key所对应的value

每一个json对象包含一个相关的键值对，以及k-1个不相关的键值对

![\<img alt="" data-attachment-key="SRR8Q7SI" width="1718" height="800" src="/attachments/SRR8Q7SI.png" ztype="zimage">](/attachments/SRR8Q7SI.png)

评估标准：准确率

通过尽可能<span style="color: #ff7700">去除自然语言语义</span>（使用随机UUID代替）来提炼和简化任务，因为自然语言的特征有可能目前存在潜在混杂因素（由于Transformer语言模型对输入上下文中的不同语言特征可能具有不同的敏感性。）

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%227%22%2C%22position%22%3A%7B%22pageIndex%22%3A6%2C%22rects%22%3A%5B%5B70.866%2C127.102%2C201.492%2C136.909%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%227%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=7">“4.2 Results and Discussion”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%227%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 7</a></span>)</span>

![\<img alt="" data-attachment-key="HDY38YF6" width="1734" height="868" src="/attachments/HDY38YF6.png" ztype="zimage">](/attachments/HDY38YF6.png)

*   claude-1.3 and claude-1.3-100k在所有评估的输入上几乎完美，但是别的模型就会差一些，尤其是超过140个kv对之后

*   与多文档问答任务的结果大致呈现相似趋势（除了Claude）

    *   ——U型曲线
    *   ——上下文变多之后下降

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B70.866%2C430.492%2C286.454%2C441.24%5D%2C%5B88.799%2C416.545%2C255.287%2C427.293%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=8">“5 Why Do Language Models Struggle To Use Their Entire Input Context?”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 8</a></span>)</span>

*   模型架构：(decoder-only vs. encoder-decoder)
*   query-aware contextualization查询感知的上下文化（文中解释的是：在文档或键值对之前和之后放置查询**）**
*   指令微调

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B70.866%2C263.162%2C229.212%2C272.969%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=8">“5.1 Effect of Model Architecture”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 8</a></span>)</span>

之前的实验都是decoder-only的模型：<span style="color: #ff2020">在每个时间步 timestep，它们只能关注之前的标记</span>

encoder-decoder：

*   Flan-UL2

    *   initially：

        *   encoder：512 tokens
        *   decoder：512 tokens

    *   pre-trained for extre 100K steps：

        *   encoder：1k tokens
        *   decoder：1k tokens

    *   instruction-tunig：

        *   encoder：2k tokens
        *   decoder：512 tokens

*   Flan-T5-XXL

    *   encoder：512 tokens
    *   decoder：512 tokens

然而，由于这些模型使用<span style="color: #ff7700">相对位置嵌入</span>relative positional embeddings，它们（原则上）可以超出这些最大上下文长度进行外推；

实验结果：

*   Flan-UL2 在小于2k的上下文长度的时候，对于相关信息的位置的表现相对稳定，超过2k之后就有了相同的趋势
*   Flan-T5-XXL 具有相同的表现

我们推测编码器-解码器模型可能<span style="color: #ff7700">更好地利用其上下文窗口</span>，因为它们的双向编码器<span style="color: #ff7700">允许在未来文件的上下文中处理每个文件</span>，从而潜在地增强了文件之间的相对重要性估计。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%228%22%2C%22position%22%3A%7B%22pageIndex%22%3A7%2C%22rects%22%3A%5B%5B306.142%2C156.051%2C521.891%2C165.858%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=8">“5.2 Effect of Query-Aware Contextualization”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%228%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 8</a></span>)</span>

之前的实验都是在输入中，把query放在上下文数据之后，这样的话<span style="color: #ff2020">decoder-only的模型文档或键值对进行上下文化时无法关注query</span><span style="color: #ff7700">（因为query永远在prompt的最后，但是decoder-only的模型只能在每一个timestep关注之前的tokens）</span>

但是encoder在使用双向编码器的时候，看起来可以更好的利用上下文来解决query中的问题（对于相关信息的位置具有一定的鲁棒性）

所以<span style="color: #ff7700">：通过将查询放置在数据之前和之后，可以实现对文档（或键值对）进行查询感知的上下文化，进一步提高仅解码模型的性能吗？</span>

实验结果：

*   查询感知的上下文化极大地<span style="color: #ff7700">提高了键值检索任务的性能</span>。（但是也没给实验结果啊。。）

    *   比如：GPT-3.5-Turbo (16K)在这种实验设计下，在评估300个键值对时，实现了完美的性能。相比之下，如果没有查询感知的上下文化处理，它在相同环境中的性能最低为45.6%。

*   相比之下，查询感知的上下文化对<span style="color: #ff7700">多文档问答任务的性能趋势影响较小</span>。

    *   当相关信息位于输入上下文的开头时，它可以提高性能

    *   <span style="color: #05a2ef">但在其他情况下略微降低性能</span>

        ![\<img alt="" data-attachment-key="EHYDISNF" width="400" height="455.2631578947368" src="/attachments/EHYDISNF.png" ztype="zimage">](/attachments/EHYDISNF.png)

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%229%22%2C%22position%22%3A%7B%22pageIndex%22%3A8%2C%22rects%22%3A%5B%5B306.142%2C333.161%2C461.804%2C342.968%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%229%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=9">“5.3 Effect of Instruction-Tuning”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%229%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 9</a></span>)</span>

之前的实验都是在指令调优之后的模型上进行训练的——在初始预训练之后，它们会在<span style="color: #ff7700">一组指令和回应的数据集上进行监督微调</span>。

在这种受监督的指导调整数据中，<span style="color: #ff7700">任务规范和/或指令通常放置在输入上下文的开头</span>，这可能会导致经过指令调整的语言模型更加重视输入上下文的开头部分。

模型：

*   MPT-30B-Instruct
*   MPT-30B

实验结果：

*   都有U型的现象，所以指令微调本身应该不是导致这个表现趋势的因素
*   指令微调之后的表现更好

![\<img alt="" data-attachment-key="NIHNGPX6" width="400" height="558.2938388625593" src="/attachments/NIHNGPX6.png" ztype="zimage">](/attachments/NIHNGPX6.png)

*   （非指导调整的）语言模型对最近的标记有偏见（即输入上下文的结尾）

*   语言模型在使用以指令格式提供的数据时能够利用更长范围的信息（即输入上下文的开头部分）

*   我们假设语言模型学会使用这些上下文是

    <span style="color: #ff7700">通过类似格式的数据进行预训练时在网页文本中出现的</span>

    ，例如StackOverflow的问题和答案。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2210%22%2C%22position%22%3A%7B%22pageIndex%22%3A9%2C%22rects%22%3A%5B%5B306.142%2C757.566%2C500.82%2C768.314%5D%2C%5B323.644%2C743.618%2C517.713%2C754.366%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2210%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=10">“6 Is More Context Is Always Better? A Case Study With Open-Domain QA”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2210%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 10</a></span>)</span>

为指令微调的语言模型提供更多信息<span style="color: #4eb31c">可能有助于改善下游任务性能</span>，但<span style="color: #05a2ef">也会增加模型需要推理的内容量</span>。

如何权衡呢？

*   取决于附加上下文的边际值和模型有效利用长输入上下文的能力。

实验：opendomain question answering

*   我们在标准的检索器-阅读器设置中使用模型：

    *   检索系统：Contriever, fine-tuned on MS-MARCO，从NaturalQuestions-Open获取输入查询，并从维基百科返回k个文档。

    *   为了将指令调整的语言模型与这些检索到的文档相结合，我们只需

        <span style="color: #ff7700">将它们包含在提示中</span>

        。

    *   我们根据检索文档数量k来评估

        <span style="color: #ff2020">检索器的召回率</span>

        和

        <span style="color: #ff2020">阅读器的准确性</span>

        （即预测输出中是否出现任何注释答案）。

实验结果：<span style="color: #ff2020">模型性能在检索器召回饱和之前就已经达到饱和，这表明模型难以利用额外的检索文档。</span>

*   在超过20个检索文档的时候，性能提升就很小了，但是会增加很多成本

![\<img alt="" data-attachment-key="RI3SK37K" width="400" height="470.14218009478674" src="/attachments/RI3SK37K.png" ztype="zimage">](/attachments/RI3SK37K.png)

这些结果与观察到的模型在<span style="color: #ff7700">检索和使用输入上下文开头或结尾的信息方面更好</span>的事实相结合，表明<span style="color: #ff2020">有效地重新排列检索到的文档</span>（<span style="color: #ff7700">将相关信息推向输入上下文开头</span>）或<span style="color: #ff2020">对排序列表进行截断</span>（<span style="color: #ff7700">必要时返回较少的文档</span>）可能是改进基于语言模型读者如何使用检索到的上下文的有希望方向。

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C466.83%2C159.956%2C477.578%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=11">“7 Related Work”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 11</a></span>)</span>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B70.866%2C442.601%2C237.23%2C452.408%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=11">“7.1 Long-context language models”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 11</a></span>)</span>

相关综述：Yi Tay, Mostafa Dehghani, Dara Bahri, and Donald Met-zler. 2022. Efficient transformers: A survey. ACM Computing Surveys, 55(6).

*   追求具有注意力修改（如循环）的Transformer变体
*   将注意力分解为计算强度较低的近似方法
*   低秩近似

还有：

*   而是通过精心设计的IO感知CUDA内核提供更快准确的注意力

*   通常通过卷积和/或线性RNN，例如在

    <span style="color: #ff7700">RWKV(</span>

    Peng，2023)、S4(Gu等人，2022)或Hyena(Poli等人，2023)中，尝试完全取消对去除二次序列长度复杂性的关注。

在长篇上下文下进行精确的知识获取可能是一个额外的挑战。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B306.142%2C627.125%2C506.64%2C636.932%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=11">“7.2 How do language models use context?”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 11</a></span>)</span>

*   Khandelwal等人的开创性工作表明小型LSTM语言模型在使用长期上下文时变得越来越粗略。

*   Sankar et al. (2019)在对话模型中发现了相似的结果

*   Daniluk等人（2017）发现专注的LSTM语言模型倾向于主要使用最近的历史。

*   Petroni等人（2020年）是最早展示了将信息检索系统的上下文与预训练语言模型相结合用于无监督问答的潜力。

*   O'Connor和Andreas（2021）发现许多破坏信息的操作对Transformer LMs的预测有边际效应（影响很小）。

*   Krishna等人（2022年）发现，在规模适中的Transformer语言模型中，长上下文神经生成会退化，因为模型未能正确地对长上下文进行条件设置。

*   最后，Sun等人（2021）研究了长上下文模型，并发现更长的上下文只能改善少数标记的预测，这一经验性发现与Sharan等人（2018）的理论一致。他们证明具有有界互信息的序列分布必然导致从越来越长的上下文中获得边际平均预测效益。

*   秦等人（2023年）分析了长上下文转换器在各种下游自然语言处理任务中的效率表现，发现长上下文转换器存在<span style="color: #ff7700">最近偏见</span>，并且不能有效地利用远程上下文。

    *   此外，他们还观察到查询感知的上下文化可以提高性能，尽管他们的分析主要集中在具有双向编码器的微调模型上（而我们主要研究仅具有解码器的零样本提示语言模型）。

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2211%22%2C%22position%22%3A%7B%22pageIndex%22%3A10%2C%22rects%22%3A%5B%5B306.142%2C126.71%2C445.822%2C136.517%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=11">“7.3 The serial-position effect”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2211%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 11</a></span>)</span>串行位置

*   我们在这项工作中观察到的U形曲线与心理学中的串联效应有关（Ebbinghaus, 1913; Murdock Jr,1962）

    *   这表明在从列表中自由联想回忆元素时，人类倾向于最好记住列表的第一个和最后一个元素。
    *   串行位置效应在理解人类如何发展短期和长期记忆方面起着作用。

*   在LLMs中观察到类似于序列位置效应可能令人惊讶，

    <span style="color: #ff2020">因为Transformer LLMs底层的自注意机制在技术上理论上来说能够在上下文中同等的检索任何token</span>

## <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FNGUXQUDS%22%2C%22pageLabel%22%3A%2212%22%2C%22position%22%3A%7B%22pageIndex%22%3A11%2C%22rects%22%3A%5B%5B70.866%2C624.581%2C145.933%2C635.329%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2212%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/NGUXQUDS?page=12">“8 Conclusion”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FBL4HK77X%22%5D%2C%22locator%22%3A%2212%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/BL4HK77X">Liu et al., 2023, p. 12</a></span>)</span>

我们通过一系列受控实验对两个需要在上下文中识别和使用相关信息的任务进行了经验研究：多文档问答和键值检索。我们发现，语言模型通常难以利用长输入上下文中的信息，并且性能会随着输入上下文变得更长而降低。

我们对(I)模型架构、(Ii)查询感知语境化和(Iii)指令调整的作用进行了初步调查，以更好地了解这些因素中的每一个可能如何影响语言模型使用语境。

最后，我们以一个开放领域问答的实际案例研究作为结论，发现语言模型阅读器的性能在检索召回之前就已经达到饱和。我们的结果和分析更好地理解了语言模型如何利用其输入上下文，并为未来长篇内容模型提供了新的评估协议。
