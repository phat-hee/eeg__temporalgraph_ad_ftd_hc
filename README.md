# 🧠 EEG Graph Classification Using GNNs (AD / FTD / HC)

This repository contains code for graph-based classification of EEG signals using Graph Neural Networks (GNNs). The goal is to distinguish between:

- **Alzheimer’s Disease (AD)**
- **Frontotemporal Dementia (FTD)**
- **Healthy Controls (HC)**

---

## 📊 Dataset Used

We use a publicly available EEG dataset from the following publication:

> **A Dataset of Scalp EEG Recordings of Alzheimer’s Disease, Frontotemporal Dementia and Healthy Subjects from Routine EEG**  
> 📄 [DOI: 10.3390/data8060095](https://doi.org/10.3390/data8060095)

This dataset includes resting-state, eyes-closed EEG recordings from:

| Group | Subjects | MMSE (Mean ± SD) | Age (Mean ± SD) |
|-------|----------|------------------|-----------------|
| AD    | 36       | 17.75 ± 4.5      | 66.4 ± 7.9      |
| FTD   | 23       | 22.17 ± 8.22     | 63.6 ± 8.2      |
| CN    | 29       | 30               | 67.9 ± 5.4      |

We do **not** own or redistribute the dataset. Please access and cite the original paper if you intend to use the data.

---

## 🧠 Project Overview

This project focuses on:

- Constructing graphs from EEG signals
- Extracting both signal-based and topological node features
- Applying GNN-based models for multi-class classification
- Evaluating model performance in distinguishing between AD, FTD, and HC groups

---

## ⚙️ Features

- EEG signal preprocessing and transformation to graph representations
- Extraction of features such as:
  - Statistical (mean, std, skewness, kurtosis)
  - Temporal (slope, ALFF)
  - Topological (degree, betweenness, clustering coefficient)
- Graph neural network models:
  - GraphSAGE
  - Graph Attention Network (GAT)
  - Graph Convolutional Network (GCN)
- Support for multi-band and windowed input sequences
- Cross-validation and performance reporting (F1, accuracy, etc.)

---

📁 **Repository Structure**  
`data/` (EEG data)  
`graphs/` (Graph representations)  
`models/` (GNN model definitions)  
`utils/` (functions)  
`train.py` (Main training script)  
`requirements.txt` (Python dependencies)  
`README.md`



---

## 🚀 Getting Started

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```
### 2. Download the Dataset
Please obtain the EEG dataset from the original source:
👉 https://doi.org/10.3390/data8060095

### 3. Run the Training Script
```bash
python train.py
```
arguments (e.g., model type, frequency band, window length) can be configured inside the script or passed as CLI flags.

## 📖 Citation
If you use this codebase or reproduce results, please cite: ///

The original dataset paper:
A Dataset of Scalp EEG Recordings of Alzheimer’s Disease, Frontotemporal Dementia, and Healthy Subjects from Rest-state EEG
📄 https://doi.org/10.3390/data8060095


## 📬 Contact
For questions, suggestions, or collaboration opportunities, feel free to open an issue or reach out to the maintainer.

## 📄 License
This repository is released under the MIT License.

Note: The EEG dataset is not included. Please refer to the original authors and publication for access and licensing.


