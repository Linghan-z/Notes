# Give Us the Facts: Enhancing Large Language Models with Knowledge Graphs for Fact-aware Language Modeling

> Key Points：
>
> - knowledge graph-enhanced large language models (KGLLMs)
>   - before-training enhancement
>   - during-training enhancement
>   - post-training enhancement
>
> 

<img src="./assets/CleanShot 2024-04-22 at 16.50.49@2x.png" alt="CleanShot 2024-04-22 at 16.50.49@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-04-22 at 16.50.33@2x.png" alt="CleanShot 2024-04-22 at 16.50.33@2x" style="zoom:50%;" />

## III. KGPLMS

<img src="./assets/CleanShot 2024-04-22 at 16.52.03@2x.png" alt="CleanShot 2024-04-22 at 16.52.03@2x" style="zoom:50%;" />

- A. Before-training Enhancement KGPLMs

  - two challenges: heterogeneous embedding space and knowledge noise.

    - Before-training enhancement methods resolve these issues by <u>*unifying text and KG triples into the same input format*</u>

      <img src="./assets/CleanShot 2024-04-22 at 16.54.33@2x.png" alt="CleanShot 2024-04-22 at 16.54.33@2x" style="zoom:50%;" />

  - methods：

    - **Expand Input Structures.** expand the input text into graph structure to merge the structured knowledge of KGs and then convert the merged graph into text for PLM training.
    - **Enrich Input Information.** 通过将实体的嵌入与文本嵌入相结合，将实体合并为辅助信息。
    - **Generate New Data** inject knowledge into PLMs by generating artificial text based on KGs
    - **Optimize Word Masks.** 优化MLM的mask 策略

  - 优点

    - improve the <u>*semantic standardization*</u> and <u>*structural level of the corpus*</u>, which is helpful for improving the reasoning ability of PLMs [117] <u>*without improving the model size and training time*</u>.
    - the training data enhanced by KGs can better describe commonsense knowledge, which helps to improve LLMs’ <u>*commonsense knowledge*</u> modeling ability.

  - 缺点

    - requires <u>*additional computational resources and time*</u>, making the pre-training process more complex and cumbersome
    - may introduce noise

- B. During-training Enhancement KGPLMs

  - enable PLMs to learn knowledge directly during training by improving their encoder and training task.

    <img src="./assets/CleanShot 2024-04-22 at 16.58.49@2x.png" alt="CleanShot 2024-04-22 at 16.58.49@2x" style="zoom:50%;" />

  - methods：

    - **Incorporate Knowledge Encoders.** 如图
    - **Insert Knowledge Encoding Layers.** insert additional knowledge encoding layers <u>*in the middle of PLMs*</u> or adjust the encoding mechanism to enable PLMs to process knowledge.
    - **Add Independent Adapters.** add independent adapters to process knowledge, which are <u>*easy to train*</u> and whose <u>*training process does not affect the parameters of the original PLM*</u>.
    - **Modify the Pre-training Task.** The most commonly used method is to change MLM to <u>*masked entity modeling (MEM)*</u> based on entities marked in texts.

  - 优点：

    - <u>*adaptively incorporate external knowledge*</u> while learning parameters, often leading to improved performance on various downstream tasks.
    - allow for <u>*customization to specific domains or tasks*</u> by introducing special information or modules

  - 缺点：

    - increase training <u>*time*</u>
    - be <u>*limited by the scope of knowledge*</u> included in the training data
    - more <u>*complex architecture and more parameters*</u>，LLMs are more susceptible to <u>*overfitting*</u> and require more training to maintain generalization.

  - During-training enhancement methods are **more suitable for those scenarios that require dealing with multiple complex tasks**, and they often perform better on knowledge-grounded tasks than other methods.

- C. Post-training Enhancement KGPLMs

  - inject domainspecific knowledge into PLMs through fine-tuning them on additional data and tasks

  - 最近的几项研究建议自动生成提示来改善PLM的输出。

    <img src="./assets/CleanShot 2024-04-22 at 17.03.03@2x.png" alt="CleanShot 2024-04-22 at 17.03.03@2x" style="zoom:50%;" />

  - methods

    - **Fine-tune PLMs with Knowledge.**
    - **Generate Knowledge-based Prompts **transforms structured knowledge into textual descriptions

  - 优点：

    - <u>*low-cost and easy to implement*</u>,
    - effectively improve LLMs’ performance on <u>*specific tasks*</u>
    - guide LLMs to generate text of <u>*specific styles*</u> and improve the <u>*quality and security of LLMs’ output.*</u>

  - 缺点：

    - labeling of fine-tuning data and the design of prompts rely on <u>*prior knowledge and external resources.*</u>
    - Moreover, these methods may impose certain <u>*limitations on the flexibility of LLMs’ generations.*</u> The generated text may be <u>*constrained by prompts*</u> and may not be able to be fully freely created.

  - more suitable for <u>*domain-specific tasks and text generation scenarios*</u> that require sensitive information filtering and risk control

- D. Effectiveness and Efficiency of KGPLMs

## IV. APPLICATIONS OF KGPLMS

<img src="./assets/CleanShot 2024-04-22 at 17.34.36@2x.png" alt="CleanShot 2024-04-22 at 17.34.36@2x" style="zoom:50%;" />

## V. CAN LLMS REPLACE KGS?

<img src="./assets/CleanShot 2024-04-22 at 17.35.27@2x.png" alt="CleanShot 2024-04-22 at 17.35.27@2x" style="zoom:50%;" />

## VI. ENHANCING LLMS WITH KGS

### A. Overall Framework

<img src="./assets/CleanShot 2024-04-22 at 17.36.19@2x.png" alt="CleanShot 2024-04-22 at 17.36.19@2x" style="zoom:50%;" />

### B. Discussion and Future Directions

- **Improving the efficiency of KGLLMs.** 
  - preprocessing and encoding knowledge from KGs
  - smaller KGPLMs can even outperform larger PLMs，所以KGLLMs可能也是这样
    - scaling law of KGLLMs
- **Merging different knowledge in different ways.**
  - 一些常见且明确定义的知识可以存储在知识图谱中以便轻松访问，而很少使用或无法通过三元组表达的隐含知识应该纳入到LLMs的参数中。特别是领域特定知识，尽管访问频率较低，但由于其相关语料库稀疏性，仍可能需要大量人力来构建关联的知识图谱。
- **Incorporating more types of knowledge**
  - multimodal and temporal KGs
- **Improving the effectiveness of knowledge incorporation**
  - the selection of valuable knowledge and avoiding catastrophic forgetting when faced with vast and clashing knowledge
- **Enhancing the interpretability of KGLLMs.**
  - relevant reasoning path in KGs based on the generated content and then generating an explanatory text based on the reasoning path. 基于生成的内容在知识图谱中找到相关推理路径，然后根据推理路径生成解释性文本。
- **Exploring domain-specific KGLLMs.**
  - 尽管已经有大量研究将标准KG与通用PLM结合起来，但有限的工作集中在特定领域的KGLLM上。然而，人工智能在科学领域的兴起将导致对特定领域KGLLM的需求不断增加。与一般的LLM相比，特定领域的LLM在融入领域知识方面需要更高的精确性和具体性。因此，构建准确的特定领域KG并将其与LLM集成值得进一步探索。为了开发特定领域的KGLLM，首先构建领域KG并在领域专家的帮助下收集相关的文集数据至关重要。考虑到语言模式的通用性，建议将常见的KG与特定领域的KG混合进行增强。

## VII. CONCLUSION

(1) What is the value of KGs in the era of LLMs? 

(2) How to incorporate KGs into LLMs to improve their performance? 

(3) What do we need to do for the future development of KGLLM?
