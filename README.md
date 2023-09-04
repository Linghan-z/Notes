---
tags: []
parent: ""
collections:
    - 'My Notes'
version: 11172
libraryID: 1
itemKey: LJSU8E3B

---
# LLM

## <span style="color: rgb(0, 0, 0)"><span style="background-color: rgb(255, 255, 255)">Aligning Large Language Models with Human: A Survey</span></span>

<a href="zotero://note/u/DMY8B9GF/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/DMY8B9GF/" ztype="znotelink" class="internal-link">“Aligning Large Language Models with Human: A Survey” (Wang et al., 2023, p. 1)</a>

## Prompt engineering

### chain of thought CoT

### concepts：

*   **<span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">system-1：</span></span>**

    <span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">比较直观的任务，</span></span>

    例如：reading comprehension, translation, and summarization

*   **system-2:**

    <span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">需要很慢而且是很仔细的考虑，比如一些设计逻辑、常识的推理任务</span></span>

<!---->

*   **<span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">Flat Scaling Curves</span></span>**

    *   <span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">即便语言模型的规模达到了几百B的参数量，也很难在 system-2 这类任务上获得很好的表现</span></span>
    *   <span style="color: rgb(77, 77, 77)"><span style="background-color: rgb(255, 255, 255)">如果将语言模型参数量作为横坐标，在 system-2 这类任务上的表现作为纵坐标，则折线就会变得相当平缓，不会像在 system-1 这类任务上那么容易就实现模型的性能随着模型参数量的增长而提升，也就是说，在 system-2 这类任务上语言模型就很难大力出奇迹了</span></span>

*   **<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Discrete Prompts离散提示，</span></span>**<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">提示依然是实际的文本字符串包括了5种prompts</span></span>

    *   <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Prompt Mining 是一种基于挖掘的方法，从大型文本语料库（如维基百科）中提取出prompt。</span></span>
    *   <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Prompt Paraphrasing 基于释义的方法采用现有的种子提示（例如手动构建或挖掘），并将其释义为一组其他候选提示，然后选择在目标任务上达到最高训练精度的提示。如翻译、短语替换等。</span></span>
    *   <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Gradient-based Search 对实际token进行了基于梯度的搜索，以找到可以触发基础预训练LM生成所需目标预测的短序列。此搜索以迭代方式完成，在提示符中单步搜索标记</span></span>
    *   <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Prompt Generation 将提示的生成视为文本生成任务，并使用标准的生成模型来执行此任务生成prompt。</span></span>
    *   <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">Prompt Scoring 首先手工制作一组模板作为潜在的候选，然后填充输入和答案槽，形成一个填充提示。然后，他们使用单向LM对已填写的提示进行评分，选择LM概率最高的提示。这将为每个单独的输入生成自定义模板。</span></span>

*   **<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">continuous prompts连续提示，</span></span>**<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">prompt不在提示为文本，而是一些连续的值（如向量等），包括了3类</span></span>

    *   **<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">前缀调整 </span></span>**

        <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">是一种将连续的任务特定向量序列预先添加到输入的方法。</span></span>

    *   **<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">离散提示初始化 </span></span>**

        <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">使用离散的方法来创建或发现的prompt来作为向量的初始化，然后微调。</span></span>

    *   **<span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">软硬提示混合调整 </span></span>**

        <span style="color: rgb(18, 18, 18)"><span style="background-color: rgb(255, 255, 255)">将一些可调的嵌入插入到硬提示模板中，如P-tuning。</span></span>

#### COT

<a href="zotero://note/u/I4LBC33B/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/I4LBC33B/" ztype="znotelink" class="internal-link">CHAIN OF THOUGHT</a>

#### <span style="color: rgba(15,23,42,var(--tw-text-opacity))"><span style="background-color: rgb(255, 255, 255)">Zero-shot COT Prompting</span></span>

<a href="zotero://note/u/QIA6EBEA/?ignore=1" rel="noopener noreferrer nofollow" zhref="zotero://note/u/QIA6EBEA/?ignore=1" ztype="znotelink" class="internal-link">“Large Language Models are Zero-Shot Reasoners” (Kojima et al., 2023, p. 1)</a>

#### **<span style="color: rgba(15,23,42,var(--tw-text-opacity))"><span style="background-color: rgb(255, 255, 255)">Automatic Chain-of-Thought (Auto-CoT)</span></span>**

<a href="zotero://note/u/PM9HKGJJ/?ignore=1" rel="noopener noreferrer nofollow" zhref="zotero://note/u/PM9HKGJJ/?ignore=1" ztype="znotelink" class="internal-link">“AUTOMATIC CHAIN OF THOUGHT PROMPTING IN LARGE LANGUAGE MODELS” (Zhang et al., 2022, p. 1)</a>

### **<span style="color: rgba(15,23,42,var(--tw-text-opacity))"><span style="background-color: rgb(255, 255, 255)">Self-Consistency</span></span>**

<a href="zotero://note/u/E83SMUMJ/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/E83SMUMJ/" ztype="znotelink" class="internal-link">“SELF-CONSISTENCY IMPROVES CHAIN OF THOUGHT REASONING IN LANGUAGE MODELS” (Wang et al., 2023, p. 1)</a>

### **<span style="color: rgba(15,23,42,var(--tw-text-opacity))"><span style="background-color: rgb(255, 255, 255)">Generated Knowledge Prompting</span></span>**

<a href="zotero://note/u/AQ8U3R7W/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/AQ8U3R7W/" ztype="znotelink" class="internal-link">“Generated Knowledge Prompting for Commonsense Reasoning” (Liu et al., 2022, p. 1)</a>

### Tree of Thoughts

<a href="zotero://note/u/RL9P2ARK/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/RL9P2ARK/" ztype="znotelink" class="internal-link">“Tree of Thoughts: Deliberate Problem Solving with Large Language Models” (Yao et al., 2023, p. 1)</a>

### <span style="color: rgba(15,23,42,var(--tw-text-opacity))"><span style="background-color: rgb(255, 255, 255)">Retrieval Augmented Generation (RAG)</span></span>

<a href="zotero://note/u/MVHHAXTD/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/MVHHAXTD/" ztype="znotelink" class="internal-link">“Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks” (Lewis et al., 2021, p. 1)</a>

### SELF-REFINE

<a href="zotero://note/u/XFEJJ7RI/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/XFEJJ7RI/" ztype="znotelink" class="internal-link">“SELF-REFINE: Iterative Refinement with Self-Feedback” (Madaan et al., 2023, p. 1)</a>

## Knowledge Graph

### Unifying Large Language Models and Knowledge Graphs: A Roadmap

<a href="zotero://note/u/ISBU6M4E/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/ISBU6M4E/" ztype="znotelink" class="internal-link">“Unifying Large Language Models and Knowledge Graphs: A Roadmap” (Pan et al., 2023, p. 1)</a>

### <span class="highlight" data-annotation="%7B%22attachmentURI%22%3A%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FRPZK4VAG%22%2C%22pageLabel%22%3A%221%22%2C%22position%22%3A%7B%22pageIndex%22%3A0%2C%22rects%22%3A%5B%5B119.345%2C758.141%2C478.316%2C771.038%5D%2C%5B157.09%2C742.201%2C438.189%2C755.098%5D%5D%7D%2C%22citationItem%22%3A%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FN8T77YMQ%22%5D%2C%22locator%22%3A%221%22%7D%7D" ztype="zhighlight"><a href="zotero://open-pdf/library/items/RPZK4VAG?page=1">“LLMs for Knowledge Graph Construction and Reasoning: Recent Capabilities and Future Opportunities”</a></span> <span class="citation" data-citation="%7B%22citationItems%22%3A%5B%7B%22uris%22%3A%5B%22http%3A%2F%2Fzotero.org%2Fusers%2F10290592%2Fitems%2FN8T77YMQ%22%5D%2C%22locator%22%3A%221%22%7D%5D%2C%22properties%22%3A%7B%7D%7D" ztype="zcitation">(<span class="citation-item"><a href="zotero://select/library/items/N8T77YMQ">Zhu et al., 2023, p. 1</a></span>)</span>

<a href="zotero://note/u/78BVHR8K/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/78BVHR8K/" ztype="znotelink" class="internal-link">“LLMs for Knowledge Graph Construction and Reasoning: Recent Capabilities and Future Opportunities” (Zhu et al., 2023, p</a>

## <span style="color: rgba(0, 0, 0, 0.9)"><span style="background-color: rgb(255, 255, 255)">PEFT(Parameter-Efficient Fine-Tuning）</span></span>

### TOWARDS A UNIFIED VIEW OF PARAMETER-EFFICIENT TRANSFER LEARNING

<a href="zotero://note/u/R4YY5VXF/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/R4YY5VXF/" ztype="znotelink" class="internal-link">“TOWARDS A UNIFIED VIEW OF PARAMETER-EFFICIENT TRANSFER LEARNING” (He et al., 2022, p. 1)</a>

### Prefix-Tuning: Optimizing Continuous Prompts for Generation

<a href="zotero://note/u/WFZGUQVG/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/WFZGUQVG/" ztype="znotelink" class="internal-link">“Prefix-Tuning: Optimizing Continuous Prompts for Generation” (Li and Liang, 2021, p. 1)</a>

### The Power of Scale for Parameter-Efﬁcient Prompt Tuning

<a href="zotero://note/u/BZ7NXSJY/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/BZ7NXSJY/" ztype="znotelink" class="internal-link">“The Power of Scale for Parameter-Efficient Prompt Tuning” (Lester et al., 2021, pp. -)</a>

> <span style="color: rgb(0, 0, 0)"><span style="background-color: rgb(255, 255, 255)">为什么上面prefix-tuning只微调embedding层效果就不好，放在prompt-tuning这里效果就好了呢？因为评估的任务不同无法直接对比，个人感觉有两个因素，一个是模型规模，另一个是继续预训练，前者的可能更大些</span></span>
>
> 通过这两篇论文的学习可以看到gap都会随着模型的规模增大而消失的，在prefix tuning中，只在embedding层进行微调的实验，建立在GPT-2中， 模型规模是 1.5B。但是prompt tuning的实验是在T5 11B中中
>
> 继续预训练：<span style="color: rgb(0, 0, 0)"><span style="background-color: rgb(255, 255, 255)">T5本身的Span Corruption预训练目标和掩码词，并不适合冻结LM的场景，因为在微调中模型可以调整预训练目标和下游目标的差异，而只使用prompt可能无法弥合差异。其实这里已经能看出En-Dn框架在生成场景下没有GPT这样的Decoder来的自然。因此作者基于LM目标对T5进行继续预训练</span></span>

### Adapter

<a href="zotero://note/u/NJK8CNGD/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/NJK8CNGD/" ztype="znotelink" class="internal-link">“Parameter-Efficient Transfer Learning for NLP” (Houlsby et al., 2019, p. 1)</a>

### LORA: LOW-RANK ADAPTATION OF LARGE LANGUAGE MODELS

<a href="zotero://note/u/87CG67EE/" rel="noopener noreferrer nofollow" zhref="zotero://note/u/87CG67EE/" ztype="znotelink" class="internal-link">“LORA: LOW-RANK ADAPTATION OF LARGE LANGUAGE MODELS” (Hu et al., 2021, p. 1)</a>
