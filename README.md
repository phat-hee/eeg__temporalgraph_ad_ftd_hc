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

- Transforming EEG signals into **temporal graph representations**
- Extracting **signal-based**, **spectral**, and **topological** node and edge features
- Applying **Graph Neural Network (GNN)** models for **multi-class classification** (AD, FTD, HC)
- Evaluating model performance across temporal windows and frequency bands

---

## ⚙️ Features

- **EEG signal preprocessing** and transformation into **graph-based representations**
- **Feature extraction** across multiple domains:
  - **Statistical:** mean, std, min, max, slope, skewness, kurtosis, Shannon entropy  
  - **Spectral:** mean PSD, relative power, spectral entropy (Welch method)  
  - **Temporal/Dynamical:** Hjorth parameters (activity, mobility, complexity), RMS, zero crossings, SVD entropy  
  - **Topological:** hub score (HITS algorithm)  
  - **Edge-level:** phase lag, phase-locking value (PLV), spectral coherence, Pearson correlation, Granger causality, partial correlation  
- **Graph construction:**
  - Directed weighted graphs using **Granger causality** matrices  
  - Sparsification using the **95th percentile threshold**
  - Supports **4s and 6s windows** with **0% or 50% overlap**
- **Graph neural network models:**
  - GraphSAGE  
  - Graph Attention Network (GAT)  
  - Graph Convolutional Network (GCN)  
  - Temporal GNN extensions for sequential graph data
- **Cross-validation** and detailed performance reporting (**Accuracy**, **F1-score**, etc.)
- **Support for multi-band EEG inputs** (e.g., alpha, beta, theta, delta)

---

## 🔄 Pipeline Overview

```text
EEG Time Series
   │
   ├── Preprocessing (Filtering, Detrending, Normalization)
   │
   ├── Sliding Window Segmentation (4s / 6s, 0% / 50% overlap)
   │
   ├── Feature Extraction
   │     ├─ Node features: statistical, spectral, temporal, topological
   │     └─ Edge features: phase, coherence, causality, correlation
   │
   ├── Graph Construction (Granger causality + thresholding)
   │
   └── GNN-based Classification (GCN / GAT / GraphSAGE)


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


