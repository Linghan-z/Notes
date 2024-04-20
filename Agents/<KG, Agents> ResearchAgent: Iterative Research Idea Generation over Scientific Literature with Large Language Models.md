# ResearchAgent: Iterative Research Idea Generation over Scientific Literature with Large Language Models

> Key Points：
>
> 

## Research Questions

large language modelpowered research idea writing **agent**

<u>*research idea generation*</u>

- conceptualizing new scientific questions, methodologies, and experiments,

## Methods

==**ResearchAgent**==

<img src="./assets/CleanShot 2024-04-20 at 11.16.43@2x.png" alt="CleanShot 2024-04-20 at 11.16.43@2x" style="zoom:50%;" />

- augmented not only with relevant publications through connecting information over an **academic graph**

  - 找到相关的论文：
    - the core paper is selected based on its citation count (e.g., exceeding 100 over 3 months) typically indicating high impact
    - relevant papers（可能很多，基于abstract再减少数量）

- **entity-centric knowledge store**——but also entities retrieved from an **entity-centric knowledge store** based on their underlying concepts, mined and shared across numerous papers.

  - 学术文章中共同出现的实体——捕捉不同实体之间的相关性

  - 在形式上，将知识存储设计为一个二维矩阵K∈Rm×m，其中m是已识别的唯一实体总数，K以稀疏格式实现

  - **ResearchAgent**三个步骤：

    1. identifying problems：p=LLM(Tp(L))

       <img src="./assets/CleanShot 2024-04-20 at 14.45.25@2x.png" alt="CleanShot 2024-04-20 at 14.45.25@2x" style="zoom:50%;" />

    2. developing methods：m=LLM(Tm(p,L))

       <img src="./assets/CleanShot 2024-04-20 at 14.45.55@2x.png" alt="CleanShot 2024-04-20 at 14.45.55@2x" style="zoom:50%;" />

    3. designing experiments：d=LLM(Te(p,m,L))

       <img src="./assets/CleanShot 2024-04-20 at 14.46.30@2x.png" alt="CleanShot 2024-04-20 at 14.46.30@2x" style="zoom:50%;" />

       - <img src="./assets/CleanShot 2024-04-20 at 14.52.45@2x.png" alt="CleanShot 2024-04-20 at 14.52.45@2x" style="zoom:50%;" />
       - <img src="./assets/CleanShot 2024-04-20 at 14.53.55@2x.png" alt="CleanShot 2024-04-20 at 14.53.55@2x" style="zoom:50%;" />
       - <img src="./assets/CleanShot 2024-04-20 at 14.54.05@2x.png" alt="CleanShot 2024-04-20 at 14.54.05@2x" style="zoom:50%;" />

- **multiple reviewing agents**——<u>*iteratively refining*</u> the generated ideas through collaborative efforts with LLM-powered multiple reviewing agents.

  - generates a review and feedback on the developed ideas

  - **ReviewingAgents**

    - each of the generated research ideas (problem, method, and experiment design) is separately evaluated

    - few-shots with human annotated evaluations

    - evaluation criteria

      - <img src="./assets/CleanShot 2024-04-20 at 14.52.09@2x.png" alt="CleanShot 2024-04-20 at 14.52.09@2x" style="zoom:50%;" />

      



## Results

data：

<img src="./assets/CleanShot 2024-04-20 at 14.57.43@2x.png" alt="CleanShot 2024-04-20 at 14.57.43@2x" style="zoom:50%;" />

result：

<img src="./assets/CleanShot 2024-04-20 at 14.58.03@2x.png" alt="CleanShot 2024-04-20 at 14.58.03@2x" style="zoom:50%;" />

## Conclusions

## Limitations & Future Works

- build a more comprehensive entity-centric knowledge store
  - extend the content (including the main texts of the publications) and the volume of papers for entity extraction
  - improve the capability of the entity linker itself to more accurately extract scientific terms within the literature.

