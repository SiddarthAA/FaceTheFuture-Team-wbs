
# 🧠 CIFAKE: AI vs Real Face Classification

**Team WBS** | Hackathon: *Face the Future*, IIIT Bangalore
**Team Members:** Siddartha A Y, Kushal B Gowda, Anish Kasetty

This repository contains our solution for the **CIFAKE binary classification challenge**, distinguishing **real vs AI-generated faces** using a robust **ensemble of vision models**.

---

## 📁 Dataset Structure

The dataset is preprocessed and split as follows:

```
cleaned/
├── train/       # 1600 images
│   ├── real/
│   └── fake/
├── val/         # 400 images
│   ├── real/
│   └── fake/
└── test/        # 500 unlabeled images
```

* **Training Set (1600 images):** Used to fine-tune models.
* **Validation Set (400 images):** Used to evaluate model performance during training.
* **Test Set (500 images):** Unlabeled; predictions are saved in `results.json`.

---

## 🧩 Our Approach

We trained **three state-of-the-art image classification models** independently and then combined their predictions using a **model ensemble** for higher accuracy and robustness:

1. **Vision Transformer (ViT-Base, Patch16-224-In21k)**

   * Captures long-range dependencies and global image context.

2. **ConvNeXt-Base-224-22k**

   * Excellent hierarchical feature extraction with modern convolutional design.

3. **EfficientNetV2-M**

   * Efficient scaling, fine-grained texture recognition, and lightweight architecture.

### 🔄 Ensemble Technique

* Each model performs **Test-Time Augmentation (TTA)** for stable predictions.
* Predictions from all three models are **averaged** to form the final ensemble output.
* This reduces variance, improves generalization, and leverages complementary strengths of different architectures.

---

## 📓 Colab Notebook

The **fully run Colab notebook** contains:

* Dataset preprocessing and augmentation
* Individual model fine-tuning (ViT, ConvNeXt, EfficientNetV2)
* Ensemble inference on validation and test datasets
* Visualization of loss and accuracy curves
* Generation of `results.json` for the test set

🔗 **Open Notebook:** [Face The Future | Team wbs](https://colab.research.google.com/drive/1cx4TYwsV8PXgJbzda-4LKv3AoL-QaoRq?usp=sharing)

> We highly recommend going through the notebook for a **step-by-step understanding** of the pipeline and code.

---

## 📊 Results

**Validation Set (400 images):**

| Model / Ensemble            | Accuracy   |
| --------------------------- | ---------- |
| ViT-Base                    | 94.76%     |
| ConvNeXt-Base               | 94.02%     |
| EfficientNetV2-M            | 92.27%     |
| **Ensemble (All 3 Models)** | **94.26%** |

> The ensemble improves consistency and ensures better reliability compared to individual models.

---

## 💾 Test Set Predictions

* Final predictions for the **500 test images** are stored in `results.json`.
* Each entry contains an **index** and predicted **label** (`real` or `fake`).

```json
[
  {"index": 1, "label": "real"},
  {"index": 2, "label": "fake"},
  ...
]
```

---

## ⚡ How to Use

1. Clone the repository:

```bash
git clone https://github.com/SiddarthAA/FaceTheFuture-Team-wbs.git
cd FaceTheFuture-Team-wbs
```

2. Open the **Colab notebook**: [FaceTheFuture | Team-wbs](https://colab.research.google.com/drive/1cx4TYwsV8PXgJbzda-4LKv3AoL-QaoRq?usp=sharing)

3. Follow the notebook cells to **train models, run ensemble, and generate predictions**.

---

## 📌 Notes

* Ensure your environment has **PyTorch, torchvision, timm, transformers, albumentations** installed.
* GPU acceleration is recommended for faster training and inference.
* The code is modular — you can replace or extend models for experimentation.

---

✅ **Conclusion:**
Our **ensemble approach** effectively combines ViT, ConvNeXt, and EfficientNetV2, achieving **high validation accuracy** and generating reliable predictions for the hackathon test set.

`results.json` contains the **final submission-ready predictions**.