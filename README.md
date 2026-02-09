# Niriksh-Edge-AI-Defect-Classification-for-Semiconductor-Images

An **Edge-AI–ready deep learning system** for **automatic detection and classification of semiconductor wafer and die defects**.  
This project was developed for a hackathon and focuses on **high-accuracy, efficient inference** using **MobileNetV3** and export to **ONNX** for deployment.

---

## 📌 Problem Statement

Develop an Edge-AI capable system that can automatically detect and classify defects in semiconductor wafer and die images using AI/ML techniques. The solution must operate reliably in real time on low-power edge hardware, reflecting the practical constraints of semiconductor manufacturing environments.

---

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
     - `BRIDGES`, `CRACK`, `OPENS`, `CMP`, `LER`, `VIAS`, `GOOD`
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
   - Stage 2: Fine-tune full network

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

* **Accuracy**: **98.04%**
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
├── dataset/
│   ├── dataset_link.md
├── script/
│   ├── Niriksh_mobilenetv3.ipynb 
├── model/
│   └── Niriksh_mobilenetv3_int16.onnx
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
