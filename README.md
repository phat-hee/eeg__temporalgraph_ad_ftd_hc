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

## 📘 Overview
This project implements a **multi-band, attention-based Temporal Graph Neural Network (GNN)** framework for classifying EEG data into clinical groups (e.g., AD, FTD, and HC).  
The model integrates **spatio-temporal graph processing** and **multi-band fusion** to capture both neural dynamics and functional connectivity patterns.

---

## ⚙️ Key Features

- **EEG Signal Preprocessing**
  - Spike removal, NaN interpolation, detrending, and bandpass filtering
  - Sliding window segmentation to generate temporal graph sequences
  - Multi-band decomposition (e.g., Delta, Theta, Alpha, Beta, Gamma)

- **Graph Construction**
  - EEG channels represented as graph nodes  
  - Edges based on statistical or functional connectivity (e.g., correlation, coherence)
  - Temporal graphs generated per time window per frequency band

- **Feature Extraction**
  - **Statistical:** Mean, standard deviation, skewness, kurtosis  
  - **Temporal:** Linear slope, ALFF (Amplitude of Low-Frequency Fluctuations)  
  - **Topological:** Node degree, betweenness centrality, clustering coefficient  

---

## 🧩 Model Architecture

### 1. **BandSpecificGraphSAGE**
Each EEG frequency band is modeled independently using:
- Two **GraphSAGE** layers for spatial feature extraction  
- **LSTM** layers for temporal dynamics  
- **Attention mechanism** to emphasize important temporal states  
- **Layer normalization** and dropout for stable training  

### 2. **MultiBandAttentionFusion**
- Combines representations from all frequency bands  
- **Band-level attention** learns the relative contribution of each frequency band  
- Fully connected layers for classification into multiple classes (e.g., AD vs HC)  
- **L1 regularization** promotes sparse and interpretable attention weights  

---

## 🧪 Training and Evaluation

- **Cross-validation:** Stratified k-fold (default: 5 folds)
- **Optimizer:** AdamW with cosine annealing scheduler  
- **Loss:** Weighted CrossEntropy with adaptive class weighting  
- **Metrics:** F1-score, Accuracy, Precision, Recall  
- **Additional Features:**
  - Gradient clipping for stability  
  - Confidence tracking (average softmax confidence)  
  - Attention-based explainability (band importance tracking)  
  - Ensemble averaging across folds for robust inference  

---

## 📊 Outputs

- Cross-validation results (average and per-fold metrics)
- Band-level attention weights (importance analysis)
- Confusion matrices per fold
- Ensemble model combining best fold checkpoints

---

## 📁 Repository Structure

```plaintext
├── data/                # Raw and preprocessed EEG data
├── graphs/              # Graph representations per subject and band
├── models/              # Model definitions (GraphSAGE, Attention Fusion)
├── utils/               # Utility functions (preprocessing, metrics, plotting)
├── train.py             # Main training and cross-validation script
├── requirements.txt     # Python dependencies
└── README.md

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


