# MM-Text2SQL-Bench

**MM-Text2SQL-Bench** is a benchmark for **image-grounded Text-to-SQL** and **multimodal database reasoning**. It studies a setting in which answering a natural-language question requires joint reasoning over an **image**, a **database schema**, a **database instance**, and the **question itself**.

Unlike conventional Text-to-SQL, where the query can often be inferred from text and schema alone, MM-Text2SQL-Bench focuses on cases where part of the SQL semantics is determined by **visual evidence**. The benchmark is designed to evaluate whether models can identify image-conditioned constraints, connect them to database fields, and generate executable SQL queries that return correct answers.

---


## Overview

Each example in MM-Text2SQL-Bench contains:

- an **image**
- a **natural-language question**
- a **database schema**
- a **database instance**
- a **gold SQL query**
- the **execution answer**
- optional **structured visual evidence**

A simplified JSON-style representation is shown below:
{
  "id": "sample_0001",
  "image": "images/sample_0001.jpg",
  "question": "Which store has the highest sales among the products shown in the image?",
  "schema": "schemas/sample_0001_schema.json",
  "database": "databases/sample_0001.sqlite",
  "sql": "SELECT store_name FROM sales ...",
  "answer": ["Downtown Store"],
  "evidence": {
    "visual_entities": ["product_A", "product_B"],
    "candidate_columns": ["product_name", "category"],
    "grounded_conditions": ["product_name IN (...)"]
  }
}

The benchmark is built to study multimodal reasoning beyond standard visual question answering and beyond standard Text-to-SQL. In our setting, the image is not decorative side information. Instead, it provides part of the grounding signal required to construct the correct SQL query.

---

## Why This Benchmark?

MM-Text2SQL-Bench is motivated by the observation that many real-world analytical questions require both **visual understanding** and **structured data access**. Existing Text-to-SQL benchmarks assume that the full query intent is recoverable from text and schema, while conventional multimodal QA benchmarks often do not require executable database querying.

This benchmark fills that gap by introducing a task where the model must jointly:

1. identify visually grounded conditions,
2. map those conditions to relevant schema elements,
3. generate executable SQL, and
4. retrieve the correct answer through database execution.

---

## Task Definition

Given an image `I`, a natural-language question `q`, a database schema `S`, and a database instance `D`, the goal is to generate a SQL query `y` such that:

- `y` is **syntactically valid**,
- `y` is **executable** on `D`,
- `y` correctly captures the semantics of `q`, and
- at least part of `y` is grounded in the visual content of `I`.

---

## Benchmark Protocols

We evaluate models under three protocols:

### P1: Text-only SQL Generation
The model receives the **question** and the **schema** only. This protocol measures how far a model can go without explicit visual grounding.

### P2: Evidence-augmented SQL Generation
The model receives the **question**, **schema**, and **structured visual evidence** extracted from the image. This protocol evaluates whether intermediate visual grounding improves SQL generation.

### P3: End-to-end Multimodal Reasoning
The model directly receives the **image**, **question**, and **schema**. This protocol evaluates integrated multimodal reasoning without manually curated intermediate evidence.

---


## Repository Structure

```text
MM-Text2SQL-Bench/
├── README.md
├── LICENSE
├── CITATION.cff
├── docs/
│   ├── index.md
│   ├── dataset.md
│   ├── examples.md
│   ├── baselines.md
│   ├── download.md
│   ├── ethics.md
│   └── assets/
├── data/
│   ├── sample/
│   └── README.md
├── dataset_card/
│   └── DATASET_CARD.md
├── baselines/
├── scripts/
├── supplementary/
└── paper/
---
## Dataset Access

Due to file size and storage limitations, the full dataset is not directly hosted in this repository.  
If you need the complete dataset, please download it from the following Google Drive link:

**Google Drive:** https://drive.google.com/drive/folders/1SUGDUgZI2FJ_nVGUP5DpmXBKo6sj5vcj?usp=sharing
This repository only provides the dataset description, schema files, sample examples, and related documentation.  
For full experiments, training, or evaluation, please use the complete dataset from Google Drive.
