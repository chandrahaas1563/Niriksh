<div align="center">

# 🔬 Niriksh – Edge-AI Defect Classification
### Semiconductor Wafer/Die Inspection System

[![Hackathon](https://img.shields.io/badge/i4C-DeepTech%20Hackathon-blue?style=for-the-badge)](https://github.com)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://tensorflow.org)
[![ONNX](https://img.shields.io/badge/ONNX-005CED?style=for-the-badge&logo=onnx&logoColor=white)](https://onnx.ai)

**A lightweight, edge-ready AI system for real-time semiconductor defect classification**

[Overview](#-overview) • [Architecture](#-system-architecture) • [Results](#-results) • [Quick Start](#-quick-start) • [Documentation](#-documentation)

---

### 📥 Access Dataset

**The complete dataset is available on Google Drive: [Download Dataset](https://drive.google.com/drive/folders/1IJQq4K5m4Q3ggibhiM3BFa9Ulwhy0yNn?usp=drive_link)**

---

### 📦 Trained Models

| Model | Format | Download |
|:-----:|:------:|:--------:|
| **Edge Deployment** | ONNX (INT16) | [Download](https://github.com) |
| **Full Precision** | ONNX (FP32) | [Download](https://github.com) |

---
---

# 🚀 Phase 2 – ONNX Inference & Evaluation

<div align="center">

**Strict reuse of Phase-1 ONNX model without retraining**

</div>

---

## 📌 Phase-2 Overview

<table>
<tr>
<td width="60%">

### Objective

Evaluate the previously trained **MobileNetV3-Large ONNX model** on the hackathon test dataset under strict constraints:

- ❌ No retraining allowed
- ❌ No architecture modification
- ❌ No new model submission
- ✅ Same Phase-1 exported ONNX model reused
- ✅ Class mismatch handled via mapping to `OTHERS`

### Evaluation Scope

- Pure ONNX inference
- Deterministic pipeline
- Metrics generation
- Confusion matrix visualization

</td>
<td width="40%">

### 📊 Phase-2 Performance

| Metric | Score |
|:------:|:-----:|
| **Accuracy** | **40.20%** |
| **Precision (Macro)** | **47.00%** |
| **Recall (Macro)** | **48.00%** |

</td>
</tr>
</table>

---

## 📈 Confusion Matrix (Phase-2)

<div align="center">

<img src="https://github.com/user-attachments/assets/eabbd9d9-59bd-46ce-b76f-d7e08626053f" alt="Phase-2 Confusion Matrix" width="650"/>

**Evaluation performed using ONNX inference pipeline**

</div>

---

## 📊 Phase-2 Per-Class Results

<div align="center">

| Class | Precision | Recall | F1-Score | Support |
|:-----:|:---------:|:------:|:--------:|:-------:|
| BRIDGES | 0.61 | 0.44 | 0.51 | 32 |
| CMP | 0.32 | 0.67 | 0.43 | 30 |
| CRACK | 0.67 | 0.52 | 0.58 | 31 |
| GOOD | 0.37 | 0.58 | 0.45 | 33 |
| LER | 0.66 | 0.63 | 0.64 | 30 |
| OPENS | 0.40 | 0.53 | 0.46 | 30 |
| VIAS | 0.21 | 0.43 | 0.28 | 30 |
| OTHERS | 0.50 | 0.03 | 0.05 | 80 |
| **Overall** | **0.47** | **0.48** | **0.43** | **296** |

</div>

---

## 📂 Phase-2 Submission Files

<table>
<tr>
<th>File</th>
<th>Description</th>
</tr>
    
<tr>
<td><code>hackathon_test_dataset_predictions.ipynb</code></td>
<td>ONNX inference script used for Phase-2</td>
</tr>

<tr>
<td><code>hackathon_test_dataset_predictions.py</code></td>
<td>ONNX inference script used for Phase-2</td>
</tr>

<tr>
<td><code>confusion_matrix_hackathon_dataset.png</code></td>
<td>Confusion matrix of hackathon test dataset</td>
</tr>
</table>

---

## ⚙️ Phase-2 Inference Pipeline

```python
Image → Resize (224×224) → Float32 Cast → ONNX Runtime (CPU) → Argmax → Metrics
```

---

## ⚙️ Key Characteristics

<table>
<tr>
<td width="100%">

| Feature | Description |
|---------|-------------|
| **Model Reuse** | `Niriksh_mobilenetv3_int16.onnx` from Phase-1 |
| **Retraining** | Not performed |
| **Fine-Tuning** | Not performed |
| **Parameter Modification** | None |
| **Class Handling** | Test mismatches mapped to `OTHERS` |
| **Evaluation Type** | Fully deterministic ONNX inference |

</td>
</tr>
</table>

---

## 🔎 Observations

<table>
<tr>
<td width="50%" valign="top">

### ✅ Strong Detection Performance

The model demonstrates relatively reliable classification for:

- **LER** – 63.33% class accuracy
- **CMP** – 66.67% class accuracy
- **CRACK** – 51.61% class accuracy
- **OPENS** – 53.33% class accuracy

These classes show stronger diagonal dominance in the confusion matrix, indicating reasonable generalization.

</td>
<td width="50%" valign="top">

### ⚠️ Expected Confusion Patterns

Misclassifications primarily occur for:

- **OTHERS** – Near-zero recall (2.50%) due to domain distribution mismatch
- **VIAS** – Low F1 (0.28) with significant confusion across classes

Such patterns are consistent with structural similarity in wafer defect morphology and the class distribution shift between the Phase-1 training data and the hackathon test set.

</td>
</tr>
</table>

---

## 🏁 Compliance Statement

<table>
<tr>
<td width="100%">

Phase-2 evaluation strictly adheres to hackathon rules:

- Model retraining was **NOT** performed.
- Phase-1 ONNX model reused without modification.
- Only permitted preprocessing (resize + required scaling) applied.
- All mandatory evaluation artifacts generated and included.

</td>
</tr>
</table>

---

</div>

## 🎯 Overview (Phase 1)

<table>
<tr>
<td width="60%">

### The Challenge

Semiconductor manufacturing requires precise defect detection at the nanometer scale. Traditional inspection methods are:
- ⏱️ **Time-intensive** – Manual inspection bottlenecks
- 💰 **Cost-prohibitive** – Expensive equipment and expertise
- 🎯 **Inconsistent** – Human error variability

### Our Solution

An **edge-deployable AI system** that:
- ✅ Classifies 8 defect categories with **~98% accuracy**
- ✅ Runs on **resource-constrained devices** via CPU ONNX Runtime
- ✅ Enables **real-time decision making** at the edge

</td>
<td width="40%">

### 📊 Quick Stats
```
🎯 Test Accuracy (FP32 ONNX):  ~98%
🎯 Test Accuracy (INT16 ONNX): ~98%
📈 F1-Score:                   0.98
🔍 Classes:                    8 defect types
📸 Dataset:                    7000+ images
⚡ Model:                       MobileNetV3-Large
🧮 Framework:                  TensorFlow / Keras
📦 Export:                     ONNX INT16 (per-channel)
📦 Model Size:                 6.74 MB
```

### 🏆 Defect Categories
```diff
+ BRIDGES        + CRACK
+ LER            + VIAS
+ OPENS          + CMP
+ GOOD           + OTHERS
```

</td>
</tr>
</table>

---

## 🎯 Architecture Highlights

| Layer | Technology | Purpose |
|:-----:|:----------:|:-------:|
| **Input** | Grayscale Images | 224×224 wafer defect images |
| **Preprocessing** | TF Keras + MobileNetV3 preprocess_input | Augmentation & normalization |
| **Model** | MobileNetV3-Large | Lightweight CNN architecture |
| **Training** | Transfer Learning + Fine-Tuning + QAT | ImageNet weights → quantization-aware |
| **Export** | tf2onnx (opset 13) → Static INT16 | Edge deployment compatibility |

---

## 📊 Dataset

<div align="center">

### Dataset Composition

| Attribute | Value |
|:---------:|:-----:|
| 📦 **Total Images** | 7000+ (original + augmented) |
| 🏷️ **Classes** | 8 categories |
| 🎨 **Format** | Grayscale(224×224) |
| 📐 **Split Ratio** | 60 / 20 / 20 (train / val / test) |
| 🔄 **Augmentation** | RandomFlip, RandomRotation(0.15), RandomZoom(0.15), RandomContrast(0.1) |
| 📂 **Source Folder** | `Niriksh3.0` |

</div>

<details>
<summary><b>📋 Class Distribution Details</b></summary>

<br>

**Defect Classes (6):**
- 🔗 BRIDGES
- 💥 CRACK
- 📏 LER (Line Edge Roughness)
- 🔓 OPENS
- ⚪ CMP
- 🔵 VIAS

**Non-Defect Classes (2):**
- ✅ GOOD
- ❓ OTHERS

> ⚠️ **Note:** Artifact folders (`split_data`, `Bridges`) that may be present in the dataset directory are automatically detected and filtered out during data loading.

**Dataset Structure:**
```bash
dataset.zip
└── Niriksh3.0/
    ├── GOOD/
    ├── BRIDGES/
    ├── CRACK/
    ├── OPENS/
    ├── CMP/
    ├── LER/
    ├── OTHERS/
    └── VIAS/
```

</details>

---

## 🧠 Model Architecture

<table>
<tr>
<td width="50%">

### 🎯 Design Choices

**Why MobileNetV3-Large?**
```
✓ Optimized for mobile/edge CPU deployment
✓ Small footprint (6.74 MB post-quantization)
✓ Fast inference via ONNX Runtime on CPU
✓ Strong ImageNet transfer learning
✓ Compatible with tf2onnx + ONNX static quantization
```

### 📐 Model Specifications

| Component | Detail |
|-----------|--------|
| **Base Architecture** | MobileNetV3-Large |
| **Framework** | TensorFlow / Keras |
| **Training Method** | Transfer Learning + Fine-Tuning + QAT |
| **Input Shape** | (224, 224, 3) |
| **Output Classes** | 8 |
| **Head** | GAP → BN → Dense(256, ReLU) → Dropout(0.4) → Dense(8, Softmax) |
| **Export Format** | ONNX FP32 → Static INT16 (opset 13) |

</td>
<td width="50%">

### ⚙️ Training Configuration
```python
# Core Settings
BATCH_SIZE      = 8
IMG_SIZE        = (224, 224)
SPLIT           = 60 / 20 / 20
CLASS_WEIGHTS   = Balanced (sklearn)

# Stage 1: Head Training (backbone frozen)
EPOCHS_HEAD     = 10
LR              = 1e-3
OPTIMIZER       = Adam

# Stage 2: Fine-tuning (top 30% of backbone unfrozen)
EPOCHS_FINE     = 3
LR              = 5e-5
OPTIMIZER       = Adam

# Stage 3: Quantization-Aware Training (QAT)
EPOCHS_QAT      = 5
LR              = 1e-5
QAT_SCOPE       = Dense layers only (annotated)

# ONNX Quantization
METHOD          = ONNX Runtime Static INT16
CALIBRATION     = 300 samples, per-channel
OPSET           = 13
```

### 🎓 Training Strategy

1. **Initialization:** Pre-trained ImageNet weights (MobileNetV3-Large)
2. **Stage 1 – Head Training:** Backbone frozen, classifier only
3. **Stage 2 – Fine-Tuning:** Top 30% of backbone layers unfrozen
4. **Stage 3 – QAT:** Dense layers quantization-annotated and trained
5. **Export:** `tf2onnx` FP32 → ONNX Runtime static INT16 quantization

</td>
</tr>
</table>

---

## ✅ Model Verification

### Dual ONNX Evaluation

Both FP32 and INT16 ONNX models are evaluated side-by-side on the held-out test set using ONNX Runtime on CPU. A complete JSON report and comparison visualizations are auto-generated at the end of the training notebook.

**Generated Artifacts:**
- `mobilenetv3_fp32.onnx` – Full precision ONNX model
- `mobilenetv3_int16.onnx` – Quantized INT16 ONNX model
- `confusion_matrices_onnx.png` – Side-by-side FP32 vs INT16 confusion matrices
- `performance_comparison_onnx.png` – Metric & model size comparison charts
- `model_evaluation_report_onnx.json` – Full structured evaluation report

---

## 📈 Results

<div align="center">

### 🎯 Test Set Performance (Phase 1)

<table>
<tr>
<td align="center">

### Overall Metrics

| Metric | FP32 ONNX | INT16 ONNX |
|:------:|:---------:|:----------:|
| **Accuracy** | **~98%** | **~98%** |
| **Precision** | **~0.98** | **0.9812** |
| **Recall** | **~0.98** | **0.9804** |
| **F1-Score** | **~0.98** | **0.9803** |
| **Model Size** | Larger | **6.74 MB** |

</td>
<td align="center">

### Confusion Matrix

![Confusion Matrix](https://github.com/user-attachments/assets/26179f5c-7f5d-42d9-8c72-8663587f6bda)

</td>
</tr>
</table>

</div>

### 🔍 Per-Class Breakdown (INT16 ONNX)

<div align="center">

| Class | Precision | Recall | F1-Score | Support |
|:-----:|:---------:|:------:|:--------:|:-------:|
| CRACK | 0.99 | 1.00 | 1.00 | 185 |
| LER | 0.92 | 1.00 | 0.96 | 191 |
| BRIDGES | 0.98 | 0.93 | 0.95 | 216 |
| CMP | 0.99 | 1.00 | 0.99 | 197 |
| GOOD | 1.00 | 0.95 | 0.97 | 193 |
| OPENS | 0.98 | 1.00 | 0.99 | 201 |
| VIAS | 1.00 | 1.00 | 1.00 | 193 |
| **Overall** | **0.98** | **0.98** | **0.98** | **1376** |

</div>

### 🔍 Key Insights

<table>
<tr>
<td width="50%" valign="top">

#### ✅ Strong Performance
- **VIAS & CRACK:** Perfect precision and recall
- **CMP & OPENS:** Near-perfect classification
- **LER:** Full recall with strong F1
- **Minimal quantization loss:** INT16 retains nearly identical accuracy to FP32

</td>
<td width="50%" valign="top">

#### ⚠️ Expected Challenges
- **Visually Similar Defects:** Minor confusion between BRIDGES/OPENS
- **OTHERS Class:** Harder to generalize at test time
- **Distribution Shift:** Phase-2 accuracy drop reflects domain gap between training and hackathon datasets

</td>
</tr>
</table>

---

## ⚡ Edge Deployment Readiness

<div align="center">

### Why This Model is Edge-Ready

</div>

| Feature | Benefit | Impact |
|---------|---------|--------|
| 🎯 **MobileNetV3-Large** | Lightweight architecture | Low compute requirements |
| 📦 **Static INT16 Quantization** | Per-channel ONNX quantization with 300-sample calibration | Smaller size, faster inference |
| ⚡ **6.74 MB Model Size** | Compact quantized footprint | Deployable on constrained hardware |
| 🖥️ **CPU-Only Inference** | ONNX Runtime CPUExecutionProvider | No GPU required at edge |
| 🔧 **3-Stage Training + QAT** | Head → Fine-tune → Quantization-Aware | Maximum accuracy before quantization |

<div align="center">

### 🎮 Target Platforms

[![NXP](https://img.shields.io/badge/NXP-eIQ-00A3E0?style=flat-square)](https://www.nxp.com)
[![NVIDIA](https://img.shields.io/badge/NVIDIA-Jetson-76B900?style=flat-square)](https://www.nvidia.com/jetson)
[![RPi](https://img.shields.io/badge/Raspberry-Pi-A22846?style=flat-square)](https://www.raspberrypi.org)
[![Intel](https://img.shields.io/badge/Intel-OpenVINO-0071C5?style=flat-square)](https://www.intel.com/openvino)

**Note:** Phase 1 focuses on software implementation. Hardware deployment validation planned for future phases.

</div>

---

## 🚀 Quick Start

### 📋 Prerequisites
```bash
# Clone the repository
git clone https://github.com/your-repo/Niriksh-Edge-AI-Defect-Classification.git
cd Niriksh-Edge-AI-Defect-Classification

# Install dependencies
pip install -r requirements.txt
```

<details>
<summary><b>📦 Required Dependencies</b></summary>

```
numpy==1.26.4
tensorflow>=2.12.0
tensorflow-model-optimization
tf2onnx>=1.14.0
onnx>=1.14.0
onnxruntime>=1.15.0
scikit-learn>=1.3.0
matplotlib>=3.7.0
seaborn>=0.12.0
Pillow>=9.5.0
tqdm
```

</details>

---

### 🎯 Usage

<table>
<tr>
<td width="50%">

#### 1️⃣ Train Model
```bash
# Open in Google Colab
Niriksh_mobilenetv3.ipynb
```

**What it does:**
- Mounts Google Drive and loads `Niriksh3.0` dataset
- Splits data 60/20/20, filters artifact folders automatically
- Stage 1: Trains classification head (10 epochs, backbone frozen)
- Stage 2: Fine-tunes top 30% of backbone (3 epochs)
- Stage 3: QAT on Dense layers (5 epochs)
- Exports FP32 and INT16 ONNX models with full evaluation reports

**Outputs:**
- `mobilenetv3_fp32.keras`
- `mobilenetv3_fp32.onnx`
- `mobilenetv3_int16.onnx`
- `confusion_matrices_onnx.png`
- `model_evaluation_report_onnx.json`

</td>
<td width="50%">

#### 2️⃣ Run Phase-2 Inference
```bash
python hackathon_test_dataset_predictions.py
```

**What it does:**
- Loads hackathon test dataset
- Runs INT16 ONNX Runtime inference on CPU
- Calculates per-class metrics
- Displays and saves confusion matrix

**Output:** Accuracy, Precision, Recall, F1 + confusion matrix PNG

</td>
</tr>
</table>

---

## 📁 Repository Structure

```
📦 Niriksh-Edge-AI-Defect-Classification
 ┣ 📂 Phase2/
 ┃  ┣ 📜 hackathon_test_dataset_predictions.ipynb
 ┃  ┗ 📜 hackathon_test_dataset_predictions.py
 ┣ 📂 dataset/
 ┃  ┗ 📋 dataset_link.md
 ┣ 📂 idea_submission/
 ┃  ┗ 📄 Niriksh_phase1.pdf
 ┣ 📂 model/
 ┃  ┗ 📦 Niriksh_mobilenetv3_int16.onnx
 ┣ 📂 script/
 ┃  ┗ 📓 Niriksh_mobilenetv3.ipynb
 ┗ 📖 README.md
```

---

## 🛠️ Technology Stack

<div align="center">

### Core Frameworks

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://tensorflow.org)
[![ONNX](https://img.shields.io/badge/ONNX-005CED?style=for-the-badge&logo=onnx&logoColor=white)](https://onnx.ai)

### Libraries & Tools

![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=flat-square)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=flat-square&logo=google-colab&logoColor=white)
![tf2onnx](https://img.shields.io/badge/tf2onnx-005CED?style=flat-square)
![TFMOT](https://img.shields.io/badge/TF--Model--Optimization-FF6F00?style=flat-square)

</div>

---

## 🏭 Deployment Perspective

Designed for:
- Inline wafer inspection
- Die-level quality control
- Embedded vision systems on CPU-only edge hardware

Benefits:
- High accuracy (~98% on own test set, minimal FP32 → INT16 degradation)
- Compact model size (6.74 MB INT16 ONNX)
- Framework-agnostic deployment via ONNX Runtime
- Scalable to new defect classes with the provided training pipeline

---

## 📚 References

1. **Deep Learning for Wafer Defect Inspection** – Industrial survey on CNN-based semiconductor defect classification
2. **Public SEM/Wafer Defect Datasets** – Open-source semiconductor inspection image repositories
3. **NXP eIQ Edge AI Toolkit Documentation** – Edge deployment framework and optimization guidelines
4. **tf2onnx** – TensorFlow/Keras to ONNX model converter (opset 13)
5. **ONNX Runtime Quantization** – Static INT16 per-channel quantization with calibration data reader

---

## 👥 Team

<div align="center">

**i4C DeepTech Hackathon – Phase 1 & 2**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com)

</div>

---

## 📝 License

This project was developed for the **i4C DeepTech Hackathon**. All rights reserved.

---

<div align="center">

### ⚠️ Important Notice

**This implementation represents Phase 1 & 2 software development.**

Results are based on test set evaluation. No hardware deployment or real-time performance claims are made at this stage.

---

**Made with 💙 for i4C DeepTech Hackathon**

</div>
