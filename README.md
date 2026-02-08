# Niriksh-Edge-AI-Defect-Classification-for-Semiconductor-Images

An **Edge-AI–ready deep learning system** for **automatic detection and classification of semiconductor wafer and die defects**.  
This project was developed for a hackathon and focuses on **high-accuracy, efficient inference** using **MobileNetV3** and export to **ONNX** for deployment.

All training and experimentation were performed on **Google Colab using an NVIDIA T4 GPU**.

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

1. **Dataset Preparation**
   - Created a custom dataset with **7000+ images**
   - Classes:
     - `bridges`, `cracks`, `opens`, `cmp`, `ler`, `vias`, `good`
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
   - Used callbacks such as **EarlyStopping** to prevent overfitting

4. **Deployment Preparation**
   - Exported trained model to **FP32 ONNX**
   - Evaluated using **ONNX Runtime on CPU**

---

## 🗂️ Dataset Structure

The dataset is provided as a **single ZIP file** with the following structure:

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

* Total images: **7000+ (original + augmented)**

---

## 🧠 Model Details

* **Architecture**: MobileNetV3-Large
* **Input Resolution**: 224 × 224
* **Training Method**: Transfer Learning + Fine-Tuning
* **Model Format**: ONNX (FP32)
* **Training Platform**: Google Colab
* **GPU Used**: NVIDIA T4
* **Inference Platform**: CPU (ONNX Runtime)

---

## 📊 Model Results (Test Set – FP32 ONNX)

The model was evaluated on a held-out **test set of 902 images** covering all defect classes.

### 🔹 Overall Performance

* **Accuracy**: **98.07%**
* **Precision**: **0.9935**
* **Recall**: **0.9933**
* **F1-Score**: **0.9934**
* **Model Size**: **12.35 MB**

---

### 🔹 Per-Class Performance

| Class       | Precision | Recall   | F1-Score | Support |
| ----------- | --------- | -------- | -------- | ------- |
| Cracks      | 0.93      | 0.96     | 0.95     | 45      |
| LER         | 1.00      | 1.00     | 1.00     | 52      |
| Bridges     | 1.00      | 0.99     | 0.99     | 77      |
| CMP         | 1.00      | 1.00     | 1.00     | 354     |
| Good        | 0.99      | 0.98     | 0.98     | 140     |
| Opens       | 0.94      | 1.00     | 0.97     | 15      |
| Vias        | 1.00      | 1.00     | 1.00     | 219     |
| **Overall** | **0.99**  | **0.99** | **0.99** | **902** |

---

### 🔹 Confusion Matrix

The confusion matrix for the FP32 ONNX model is available in:

```
results/confusion_matrix_fp32.png
```

---

## 🗺️ Repository Structure

```bash
.
├── dataset/
│   └── dataset.zip
├── notebooks/
│   ├── training_colab.ipynb
│   └── evaluation_colab.ipynb
├── src/
│   ├── preprocess.py
│   ├── train.py
│   ├── export_onnx.py
│   └── infer.py
├── models/
│   └── mobilenetv3_fp32.onnx
├── results/
│   └── confusion_matrix_fp32.png
├── docs/
│   └── Final_Documentation.pdf
├── requirements.txt
└── README.md
```

---

## 🚀 How to Run

### 1️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

### 2️⃣ Preprocess Dataset

```bash
python src/preprocess.py
```

### 3️⃣ Train Model

```bash
python src/train.py
```

### 4️⃣ Export to ONNX

```bash
python src/export_onnx.py
```

### 5️⃣ Run Inference

```bash
python src/infer.py --image path/to/image.jpg
```

---

## 📄 Documentation

* 📘 **Final Report**: `docs/Final_Documentation.pdf`
* 🗂️ **Dataset**: `dataset/dataset.zip`
* 🧠 **Trained Model (ONNX)**: `models/mobilenetv3_fp32.onnx`
* 📊 **Results & Confusion Matrix**: `results/`
* 💻 **Complete Code**:

  * Preprocessing
  * Training
  * Evaluation
  * ONNX Export
  * Inference

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

## 📚 Learnings

* Building efficient CNNs using MobileNetV3
* Designing robust datasets with augmentation
* Transfer learning and fine-tuning for industrial vision tasks
* Exporting and validating models using ONNX Runtime
* End-to-end ML pipeline design for edge deployment

---

## 🏆 Hackathon Submission Checklist

* ✅ Filled PDF documentation
* ✅ Dataset ZIP with required folder structure
* ✅ Trained ONNX model (FP32)
* ✅ Metrics: Accuracy, Precision, Recall, F1-Score, Confusion Matrix, Model Size
* ✅ Training platform specified: Google Colab (NVIDIA T4)
* ✅ Complete code for preprocessing, training, and inference
* ✅ GitHub repository with README
