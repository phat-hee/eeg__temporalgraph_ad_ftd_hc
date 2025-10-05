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

# 🧠 EEG-Based Graph Neural Network Classification for AD, FTD, and HC

## 📘 Project Overview

This project focuses on:

- Constructing graphs from EEG signals  
- Extracting both signal-based and topological node features  
- Applying GNN-based models for multi-class classification  
- Evaluating model performance in distinguishing between **Alzheimer’s Disease (AD)**, **Frontotemporal Dementia (FTD)**, and **Healthy Controls (HC)**  

---

## 🧩 Dataset Description

This dataset contains **EEG resting-state (eyes-closed)** recordings from a total of **88 subjects**, divided into three groups:

- **36** with Alzheimer’s disease (AD)  
- **23** with Frontotemporal Dementia (FTD)  
- **29** healthy controls (HC)  

### Participant Information

- **Cognitive Assessment:** Mini-Mental State Examination (MMSE, range: 0–30)  
  - AD: 17.75 ± 4.5  
  - FTD: 22.17 ± 8.22  
  - HC: 30  
- **Age (mean ± SD):**  
  - AD: 66.4 ± 7.9  
  - FTD: 63.6 ± 8.2  
  - HC: 67.9 ± 5.4  
- **Disease duration:** Median 25 months (IQR: 24–28.5)

### Recording Details

- **Device:** Nihon Kohden EEG 2100  
- **Electrodes:** 19 scalp channels (Fp1–O2, 10–20 system) + 2 mastoid references (A1, A2)  
- **Montage:** Referential (Cz as common reference)  
- **Sampling rate:** 500 Hz  
- **Filters:** 0.3 s time constant, high-frequency cutoff at 70 Hz  
- **Recording duration:**  
  - AD: 13.5 min (5.1–21.3)  
  - FTD: 12 min (7.9–16.9)  
  - HC: 13.8 min (12.5–16.5)

### 🧼 Preprocessing Pipeline

Before separating signals into frequency bands and constructing graph representations, EEG data underwent the following preprocessing steps:

1. **Band-pass filtering (0.5–45 Hz)** using a Butterworth filter  
2. **Re-referencing** to A1–A2  
3. **Artifact Subspace Reconstruction (ASR)** using EEGLAB to remove noisy segments exceeding a 0.5-second window SD threshold of 17  
4. **Independent Component Analysis (ICA)** (RunICA algorithm)  
5. **Automatic artifact rejection** via *ICLabel* (eye/jaw artifacts removed)  

Even under eyes-closed conditions, minor eye movement artifacts were detected and removed automatically.  
Preprocessed files are provided in the `derivatives/` folder as `.set` files (BIDS-compatible format).  

For more details, refer to the published paper:  
> **A Dataset of Scalp EEG Recordings of Alzheimer’s Disease, Frontotemporal Dementia and Healthy Subjects from Routine EEG**  
> *Data, 8(6), 95 (2023)* — [https://doi.org/10.3390/data8060095](https://doi.org/10.3390/data8060095)

---

## ⚙️ Features

- EEG signal preprocessing and transformation to graph representations  
- Extraction of features such as:  
  - **Statistical:** mean, std, skewness, kurtosis  
  - **Temporal:** slope, ALFF  
  - **Topological:** degree, betweenness, clustering coefficient  
- Graph neural network models:  
  - **GraphSAGE**  
  - **Graph Attention Network (GAT)**  
  - **Graph Convolutional Network (GCN)**  
- Support for **multi-band** and **windowed** input sequences  
- **Cross-validation** and **performance reporting** (F1-score, accuracy, etc.)

---

## 📁 Repository Structure



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


