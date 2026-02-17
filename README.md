# Niriksh-Edge-AI-Defect-Classification-for-Semiconductor-Images

An **Edge-AI–ready deep learning system** for **automatic detection and classification of semiconductor wafer and die defects**.  
This project was developed for a hackathon and focuses on **high-accuracy, efficient inference** using **MobileNetV3** and export to **ONNX** for deployment.

---

## 📌 Problem Statement

Develop an Edge-AI capable system that can automatically detect and classify defects in semiconductor wafer and die images using AI/ML techniques. The solution must operate reliably in real time on low-power edge hardware, reflecting the practical constraints of semiconductor manufacturing environments.

---
# Phase 1

## 🧠 Problem Understanding

Semiconductor manufacturing requires **fast, accurate, and reliable inspection** of wafers and dies to improve yield and reduce waste.  
Manual inspection or cloud-based systems introduce:
- Latency
- Higher operational cost
- Limited scalability

This project aims to design a **compact, accurate, and deployable AI model** that can:
- Perform defect classification automatically
- Be exported to ONNX for edge deployment
- Maintain high accuracy with low computational overhead

---

## 🏗️ Approach

<img width="1256" height="497" alt="Screenshot 2026-02-09 044937" src="https://github.com/user-attachments/assets/3c4ec538-2bb6-4ef0-8c21-42b97f3239e3" />


1. **Dataset Preparation**
   - Created a custom dataset with **7000+ images**
   - Classes:
     - `BRIDGES`, `CRACK`, `OPENS`, `CMP`, `LER`, `VIAS`, `GOOD`, `OTHERS`
   - Applied data augmentation:
     - Brightness variation
     - Contrast adjustment
     - Rotation
   - Images resized to **224×224**

2. **Model Selection**
   - Chosen **MobileNetV3-Large** due to:
     - Low parameter count
     - High efficiency on edge devices
     - Strong accuracy–latency trade-off

3. **Training Strategy**
   - Transfer learning using pre-trained MobileNetV3
   - Stage 1: Train classification head with frozen backbone
   - Stage 2: Fine-tune the full network

4. **Deployment Preparation**
   - Exported trained model to **INT16 ONNX**
   - Evaluated using **ONNX Runtime on CPU**

---

## 🗂️ Dataset Structure

* The dataset is designed with the following structure:

```bash
dataset.zip
└── Niriksh2.0/
    ├── GOOD/
    ├── BRIDGES/
    ├── CRACK/
    ├── OPENS/
    ├── CMP/
    ├── LER/
    ├── OTHERS/
    └── VIAS/
    
````
#### **Access the dataset here:** https://drive.google.com/drive/folders/1IJQq4K5m4Q3ggibhiM3BFa9Ulwhy0yNn?usp=drive_link
* Total images: **7000+ (original + augmented)**

---

## 🧠 Model Details

* **Architecture**: MobileNetV3-Large + INT16 ONNX Quantization
* **Input Resolution**: 224 × 224
* **Training Method**: Transfer Learning + Fine-Tuning
* **Model Format**: ONNX (INT16)
* **Training Platform**: Google Colab
* **GPU Used**: NVIDIA T4
* **Inference Platform**: CPU (ONNX Runtime)

---

## 📊 Model Results (Test Set – INT16 ONNX)

* The model was evaluated on a held-out **test set of 1376 images** covering all defect classes.

### 🔹 Overall Performance

* **Accuracy**: **98.04%** (May vary between 95-98)
* **Precision**: **0.9812**
* **Recall**: **0.9804**
* **F1-Score**: **0.9803**
* **Model Size**: **6.74 MB**

---

### 🔹 Per-Class Performance

| Class       | Precision | Recall | F1-Score | Support |
|------------|-----------|--------|----------|---------|
| Cracks     | 0.99      | 1.00   | 1.00     | 185     |
| LER        | 0.92      | 1.00   | 0.96     | 191     |
| Bridges    | 0.98      | 0.93   | 0.95     | 216     |
| CMP        | 0.99      | 1.00   | 0.99     | 197     |
| Good       | 1.00      | 0.95   | 0.97     | 193     |
| Opens      | 0.98      | 1.00   | 0.99     | 201     |
| Vias       | 1.00      | 1.00   | 1.00     | 193     |
| **Overall**| **0.98**      | **0.98**   | **0.98**     | **1376**    |


---

### 🔹 Confusion Matrix

The confusion matrix for the INT16 ONNX model is available in:


<img width="720" height="520" alt="Screenshot 2026-02-09 043747" src="https://github.com/user-attachments/assets/26179f5c-7f5d-42d9-8c72-8663587f6bda" />



---

## 🗺️ Repository Structure

```bash
├── Phase2/
│   ├── hackathon_test_dataset_predictions.ipynb
│   ├── hackathon_test_dataset_predictions.py
├── dataset/
│   ├── dataset_link.md
├── idea_submission/
│   ├── Niriksh_phase1.pdf
├── model/
│   └── Niriksh_mobilenetv3_int16.onnx
├── script/
│   ├── Niriksh_mobilenetv3.ipynb 
└── README.md
```

---

## 🚀 How to Run

### 1️⃣ Setting Dataset
* Make a shortcut of the provided dataset on your Google Drive account.

### 2️⃣ Running the Model
* Download the script file "Niriksh_mobilenetv3.ipynb".
* Open Google Colab and upload it.
* Make the respective file paths changes.
* Hit Run all.

---

## 🏭 Deployment Perspective

* Designed for:

  * Inline wafer inspection
  * Die-level quality control
  * Embedded vision systems
  
* Benefits:

  * High accuracy
  * Compact model size
  * ONNX compatibility for edge runtimes
  * Scalable to new defect classes

---

# Phase 2

## 📊 Model Results (Test Set – INT16 ONNX)

### 🔹 Overall Performance

| Metric               | Value        |
|---------------------|-------------|
| Overall Accuracy     | 40.62%      |
| Average Confidence   | 88.80%      |
| Total Images         | 256         |

---

### 🔹 Per-Class Accuracy

| Class      | Accuracy   |
|-----------|-----------|
| CMP       | 63.33%    |
| LER       | 63.33%    |
| BRIDGES   | 31.25%    |
| GOOD      | 54.55%    |
| CRACK     | 51.61%    |
| OPENS     | 53.33%    |
| VIAS      | 3.33%     |
| OTHERS    | 6.25%     |

### 🔹 Classification Report

| Class      | Precision | Recall | F1-Score | Support |
|-----------|-----------|--------|----------|---------|
| BRIDGES   | 0.40      | 0.33   | 0.36     | 30      |
| CMP       | 0.36      | 0.68   | 0.47     | 28      |
| CRACK     | 0.80      | 0.53   | 0.64     | 30      |
| GOOD      | 0.41      | 0.56   | 0.47     | 32      |
| LER       | 0.73      | 0.63   | 0.68     | 30      |
| OPENS     | 0.50      | 0.55   | 0.52     | 29      |
| VIAS      | 0.03      | 0.06   | 0.04     | 16      |
| OTHERS    | 0.20      | 0.08   | 0.12     | 61      |
| **Accuracy** | -       | -      | 0.41     | 256     |
| **Macro Avg** | 0.43   | 0.43   | 0.41     | 256     |
| **Weighted Avg** | 0.42 | 0.41  | 0.40     | 256     |

### 🔹 Confusion Matrix for **hackathon_test_dataset**

<img width="652" height="497" alt="confusion_matrix_hackathon_dataset" src="https://github.com/user-attachments/assets/eabbd9d9-59bd-46ce-b76f-d7e08626053f" />




