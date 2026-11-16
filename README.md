# Quantum-Classical Hybrid Model for Sentence Similarity
# OVERLEAF: https://www.overleaf.com/project/6af871f9c678325bec5e5c4e/share#e06c7c602fa32096e124306d11790807a3c70fed712da814

## 1. Project Overview

This project explores the integration of classical Natural Language Processing (NLP) and quantum computing for Semantic Textual Similarity (STS).

The objective is to determine how similar two sentences are based on their meaning, even when they contain different words or sentence structures.

The proposed model combines Sentence-BERT (SBERT) embeddings with quantum-derived features and uses Ridge Regression to predict a similarity score between **0 and 5**.

## 2. Problem Statement

Traditional sentence similarity approaches commonly use pretrained sentence embeddings and cosine similarity to measure semantic relationships between sentences.

Although these approaches provide strong results, this project explores whether quantum-derived features can complement classical sentence representations and contribute useful information to similarity prediction.

The proposed approach combines classical feature extraction, dimensionality reduction and a fixed four-qubit quantum feature map to develop a hybrid quantum-classical sentence similarity model.

## 3. Project Objectives

- Generate meaningful sentence embeddings using SBERT.
- Represent sentence pairs using element-wise absolute differences.
- Reduce embedding dimensions using Principal Component Analysis (PCA).
- Extract additional features using a four-qubit quantum circuit.
- Combine classical and quantum-derived features.
- Predict semantic similarity scores using Ridge Regression.
- Compare the hybrid approach with classical machine learning baselines.

## 4. Proposed Methodology

The proposed workflow consists of the following stages:

1. **Sentence Encoding:** Both input sentences are independently passed through the pretrained SBERT model (`all-MiniLM-L6-v2`) to generate 384-dimensional embeddings.

2. **Pair Representation:** The element-wise absolute difference between the two sentence embeddings is calculated to obtain an order-independent pair representation.

3. **Standardization and PCA:** The features are standardized and reduced from 384 dimensions to four principal components using PCA.

4. **Quantum Feature Extraction:** The four PCA components are encoded into a fixed four-qubit quantum circuit using RY rotation gates and a chain of CNOT gates.

5. **Quantum Measurements:** Four Pauli-Z expectation values are obtained to generate quantum-derived features.

6. **Feature Fusion:** The four classical PCA features and four quantum features are combined into an eight-dimensional hybrid representation.

7. **Similarity Prediction:** Ridge Regression with a regularization parameter of alpha = 10 predicts the final similarity score between 0 and 5.

### Workflow

```text
        Input Sentence 1
                |
        Input Sentence 2
                |
                v
          SBERT Encoder
          (384 dimensions)
                |
                v
       Absolute Difference
                |
                v
       Standardization + PCA
          (4 components)
                |
          +-----+-----+
          |           |
          v           v
    Classical       Quantum
     Features       Circuit
       (4)          (4 Qubits)
          |           |
          |           v
          |      Pauli-Z Measurements
          |           |
          +-----+-----+
                |
                v
         Feature Fusion
        (8-dimensional)
                |
                v
        Ridge Regression
             alpha=10
                |
                v
       Similarity Score
             (0-5)
```

## 5. Dataset

**Dataset Name:** Semantic Textual Similarity Benchmark (STS-B)

The STS-B dataset is used to train and evaluate the proposed sentence similarity model.

It contains sentence pairs annotated with human similarity scores ranging from 0 to 5.

| Dataset Split | Number of Pairs |
|---|---:|
| Training | 5,749 |
| Validation | 1,500 |
| Test | 1,379 |
| **Total** | **8,628** |

### Dataset Usage

- Training split: Used for fitting preprocessing transformations and regression models.
- Validation split: Used for model comparison and reported experimental results.
- Test split: Not evaluated in this study.

Dataset source: [GLUE Benchmark – STS-B](https://gluebenchmark.com/tasks)

## 6. Technologies and Tools

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Sentence-BERT | Sentence embedding generation |
| all-MiniLM-L6-v2 | Pretrained sentence encoder |
| Scikit-learn | PCA, standardization and Ridge Regression |
| PennyLane | Quantum circuit simulation |
| NumPy | Numerical computations |
| Pandas | Dataset handling |
| SciPy | Statistical evaluation |
| Hugging Face Datasets | Loading the STS-B dataset |

## 7. Installation and Setup

### Prerequisites

- Python 3.9 or later
- pip package manager
- Internet connection for downloading the pretrained model and dataset

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

### Step 2: Navigate to the Project Directory

```bash
cd YOUR-REPOSITORY
```

### Step 3: Create a Virtual Environment (Recommended)

```bash
python -m venv venv
```

Activate it:

**Windows:**
```bash
venv\Scripts\activate
```

**Linux / macOS:**
```bash
source venv/bin/activate
```

### Step 4: Install Dependencies

```bash
pip install numpy pandas scipy scikit-learn sentence-transformers datasets joblib
```

## 8. Running the Project

Run the Python implementation:

```bash
python quantum_classical_sentence_similarity_test.py
```

The script loads the STS-B dataset, generates SBERT embeddings, performs feature extraction, trains the regression models and evaluates their validation performance.

### Testing Custom Sentence Pairs

After training and saving the model, you can test your own sentence pairs:

```python
from quantum_classical_sentence_similarity_test import predict_similarity

predict_similarity(
    "A man is playing guitar.",
    "A person is playing a musical instrument."
)
```

The model returns a predicted semantic similarity score between 0 and 5.

## 9. Experimental Results

The proposed hybrid model was compared with four other configurations using the STS-B validation dataset.

| Model | Pearson | Spearman | MSE | MAE | RMSE |
|---|---:|---:|---:|---:|---:|
| SBERT + calibrated cosine | 0.873208 | 0.867035 | 0.535449 | 0.568250 | 0.731744 |
| Classical Ridge (384 features) | 0.852310 | 0.850050 | 0.616945 | 0.620917 | 0.785458 |
| PCA + Ridge | 0.865240 | 0.863226 | 0.567633 | 0.595598 | 0.753414 |
| Quantum features + Ridge | 0.467841 | 0.425057 | 1.875000 | 1.149208 | 1.369306 |
| **Quantum-Classical Hybrid** | **0.872322** | **0.863873** | **0.538345** | **0.570337** | **0.733720** |

### Results Summary

- The proposed hybrid model achieved a Pearson correlation of **0.872322**.
- Its performance was competitive with the calibrated SBERT baseline.
- The calibrated SBERT baseline achieved a slightly higher Pearson correlation of 0.873208.
- The quantum-only configuration performed considerably worse than the other approaches.
- The results do not establish quantum advantage.

## 10. Conclusion

This project demonstrates an experimental integration of classical NLP techniques and quantum-derived feature extraction for sentence similarity prediction.

By combining SBERT embeddings, PCA-based dimensionality reduction and a fixed four-qubit feature map, the proposed system generates a hybrid representation for predicting semantic similarity.

The experimental results show that the hybrid model achieves competitive validation performance. However, it does not outperform the calibrated SBERT baseline.

Further research is required to investigate alternative quantum circuit configurations, evaluate matched classical nonlinear models and test the approach on the held-out STS-B test dataset.

## 11. Limitations and Future Work

### Limitations

- The quantum circuit uses a fixed, non-trainable architecture.
- Quantum-only features show comparatively weak performance.
- The experiments do not establish quantum computational advantage.
- The held-out test dataset has not been evaluated.
- Further controlled experiments are required.

### Future Work

- Experiment with different quantum circuit architectures.
- Explore trainable quantum circuits.
- Compare against additional classical nonlinear models.
- Evaluate performance on the held-out test split.
- Investigate execution on actual quantum hardware.

## 12. Group Members

**Research Project: Quantum-Classical Hybrid Model for Sentence Similarity**

| Name | Role |
|---|---|
| Mayuresh Kharmate | Research, implementation and experimentation |
| Jay Wagh | Research, analysis and documentation |

## 13. References

1. Cer, D., et al. (2017). SemEval-2017 Task 1: Semantic Textual Similarity. *Proceedings of SemEval-2017*.
2. Reimers, N., and Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks.
3. Gao, T., Yao, X., and Chen, D. (2021). SimCSE: Simple Contrastive Learning of Sentence Embeddings.
4. Relevant quantum NLP and hybrid quantum-classical research works cited in the research paper.

---

**Note:** The experimental results presented in this repository correspond to the validation results reported in the research paper. The test split has not been evaluated.

