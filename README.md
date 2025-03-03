# Installing minBERT and Enhancing with Knowledge Injection and Contrastive Learning

## Team Members:
- Tăng Vĩnh Hà, Student ID: 22028129
- Vũ Nguyệt Hằng, Student ID: 22028079
- Ngô Tùng Lâm, Student ID: 22028092

This repository is for the Natural Language Processing course project, class 7, Semester 1, Academic Year 2024 - 2025. Project details are included in the final report.

## Project Details

### Installing minBERT:
- **Tokenizer and BERT Base Files**:
    - The `tokenizer` and `bert_base` files are used to tokenize input sentences into `input_ids` based on the predefined vocabulary of `google/bert_uncased_L-4_H-256_A-4` from HuggingFace and initialize parameters for the minBERT model (`init_weights` method).
- **BERT File (`bert`)**:
    - Implements the components of the BERT architecture (detailed explanations are provided in the comments).
- **Classifier File (`classifier`)**:
    - Adds extra layers to BERT for downstream classification tasks. In this project, the focus is on text classification.

### Enhancement with Knowledge Injection:
- Integrates **author embeddings** obtained from **PyTorch-BigGraph pretrained embeddings** of the **Wikidata Knowledge Graph**.
- Controlled by the argument `--use_author` in `classifier.py`.

### Enhancement with Contrastive Learning:
The team further pretrains BERT using the **SimCSE framework**:

- **SimCSE Unsupervised Contrastive Learning**:
    - Uses contrastive data where batches of sentences are forwarded through the `bert` model twice (generating embeddings) with two different `attention_mask` applications to form positive pairs, while other sentences in the same batch serve as negative pairs.
    - The optimization function is **contrastive loss**.
    - The dataset used is **wiki1m**, taking **38% of the original dataset size**.
    - Implemented in `classifier_unsupervised_CL`, modified from `classifier` by adjusting the data loading and `train` function (defining a different loss function).

- **SimCSE Supervised Contrastive Learning**:
    - Uses contrastive data in triplets: **anchor - positive - negative** from the **NLI dataset**.
    - The optimization function is **contrastive loss**.
    - Implemented in `classifier_supervised_CL`, modified from `classifier` by adjusting the data loading and `train` function (defining a different loss function).

### Experimental Results:
- Detailed results are included in the final report.

### How to Run Experiments:
- Please refer to the **Kaggle notebook appendix** in the final report.

## Repository Structure
- **`data/`**: Contains datasets for experiments.
- **`data_small/`**: Contains smaller datasets for quick debugging on a laptop.

## Acknowledgement
- This project references the original [`minBERT`](https://github.com/neubig/minbert-assignment) repository.
