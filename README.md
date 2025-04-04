# Full_Train_BERT_MNLI
Full training "bert-base-uncased" checkpoint on "glue-mnli" dataset

## 🧠 GLUE MNLI Dataset
The Multi-Genre Natural Language Inference (MNLI) dataset is part of the GLUE Benchmark, designed to evaluate a model's ability to perform natural language understanding tasks.

## 📘 Task Definition
The task is to determine the semantic relationship between a premise and a hypothesis sentence. Each example is labeled as one of the following:

**entailment (0)**: The hypothesis logically follows from the premise.  
**neutral (1**): The hypothesis might be true, but is not guaranteed.  
**contradiction (2)**: The hypothesis contradicts the premise.  

| Premise                                           | Hypothesis                                      | Label         |
|--------------------------------------------------|-------------------------------------------------|---------------|
| A soccer game with multiple males playing.       | Some men are playing a sport.                   | Entailment    |
| An older and younger man smiling.                | Two men are smiling at the cats playing around. | Neutral       |
| A man inspects the uniform of a figure.          | The man is sleeping.                            | Contradiction |

## 📊 Dataset Structure
The MNLI dataset contains examples drawn from a wide range of genres to test generalization across domains.

| Split                 | Description                                        | Labels Available |
|----------------------|----------------------------------------------------|------------------|
| train                | Training data from multiple genres (~392k samples) | ✅ Yes           |
| validation_matched   | Validation data from the same genres as train      | ✅ Yes           |
| validation_mismatched| Validation data from different genres              | ✅ Yes           |
| test_matched         | Test data from same genres (for leaderboard use)   | ❌ No (labels = -1) |
| test_mismatched      | Test data from new genres (for leaderboard use)    | ❌ No (labels = -1) |

### ✅ Matched vs Mismatched:  
**Matched** = in-domain (same genre as training)  
**Mismatched** = out-of-domain (unseen genres, testing robustness)

## 📦 Features
**premise** *(string)*: The original sentence.  
**hypothesis** *(string)*: Sentence to compare against the premise.  
**label** *(int)*: 0 = entailment, 1 = neutral, 2 = contradiction.  
**genre** *(string)*: Source genre (e.g., fiction, government).  
**idx** *(int)*: Unique index of the example.

## 🔗 Resources
Official GLUE page: https://gluebenchmark.com/tasks

### Dataset on Hugging Face 🤗 Datasets:  
```python
from datasets import load_dataset

# Load the MNLI dataset
raw_datasets = load_dataset("glue", "mnli")
```
## ⚡ Training and Evaluation

### Model:
- Pretrained model: `bert-base-uncased`
- Task: Sequence Classification (MNLI)
- Framework: Hugging Face Transformers

### Evaluation Setup:
- Combined the **matched** and **mismatched** evaluation datasets for a more comprehensive evaluation.

### Results:
- **Accuracy on evaluation data**: **83.11%** (combined matched and mismatched evaluation datasets)

```python
eval_results = {'accuracy': 0.8310683564920853}
```
This result was achieved by combining both validation_matched and validation_mismatched datasets, which provides a more generalized view of model performance across both in-domain and out-of-domain examples.
