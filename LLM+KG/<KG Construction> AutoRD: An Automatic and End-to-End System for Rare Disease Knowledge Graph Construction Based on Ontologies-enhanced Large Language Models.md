# AutoRD: An Automatic and End-to-End System for Rare Disease Knowledge Graph Construction Based on Ontologies-enhanced Large Language Models

## Abstract

**AutoRD**: automates extracting information from clinical text about rare diseases

pipeline: data preprocessing, entity extraction, relation extraction, entity calibration 实体校准, and knowledge graph construction

## AutoRD Framework

<img src="./assets/CleanShot 2024-03-20 at 10.24.49@2x.png" alt="CleanShot 2024-03-20 at 10.24.49@2x" style="zoom:50%;" />

#### Task Definition

<img src="./assets/CleanShot 2024-03-20 at 10.28.26@2x.png" alt="CleanShot 2024-03-20 at 10.28.26@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-20 at 10.28.47@2x.png" alt="CleanShot 2024-03-20 at 10.28.47@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-20 at 10.29.09@2x.png" alt="CleanShot 2024-03-20 at 10.29.09@2x" style="zoom:50%;" />

<img src="./assets/CleanShot 2024-03-20 at 10.29.25@2x.png" alt="CleanShot 2024-03-20 at 10.29.25@2x" style="zoom:50%;" />

#### Data Preprocessing

divide lengthy input documents into segments containing fewer than 2,000 tokens to adhere to the token limit.

#### Entity Extraction

<img src="./assets/CleanShot 2024-03-20 at 10.48.17@2x.png" alt="CleanShot 2024-03-20 at 10.48.17@2x" style="zoom:50%;" />