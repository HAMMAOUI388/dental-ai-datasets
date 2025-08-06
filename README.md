# 🦷 Dental AI Datasets

This repository manages datasets and training materials for deep learning models aimed at dental diagnostics using **X-ray** and **camera images**. It supports tasks such as tooth health classification (e.g., healthy, cavity, broken) and object detection using YOLO models.

---

## 📁 Project Structure

```bash
.
├── README.md                 # Project overview and documentation
├── data.yaml                 # YOLOv8 config for dataset training
├── dataset-sources.md        # Notes on dataset sources and curation
├── datasets/                 # All training/validation/test data
│   ├── X-rays/               # Cleaned and labeled dental X-ray images
│   │   ├── train/
│   │   ├── valid/
│   │   └── test/
│   └── camera/               # RGB images from intraoral cameras
│       ├── train/
│       ├── valid/
│       └── test/
├── models/                   # Saved YOLO models (trained weights)
├── notebooks/                # Jupyter notebooks for training & inference
│   ├── detect_xrays.ipynb    # Main detection/inference pipeline
│   ├── predictions/          # Output predictions (images with boxes)
│   ├── yolov8n.pt            # Pretrained or fine-tuned YOLO model
│   └── *.md                  # Notes and progress tracking
├── reports/                  # Analysis reports and model evaluation
```

---

## 🧠 Dataset Overview

Each dataset is organized into:
- `broken/`: Images of fractured or damaged teeth
- `cavities/`: Images showing caries or visible cavities
- `healthy/`: Images with normal, healthy teeth

Both **X-ray** and **camera** datasets follow the same directory structure:
```
datasets/{X-rays,camera}/{train,valid,test}/{broken,cavities,healthy}
```

### 📊 Label Summary (YOLO format)

- `healthy` – class ID `0`
- `cavities` – class ID `1`
- `broken` – class ID `2`

> Annotations are provided in YOLO format alongside the images during training.

---

## 🚀 Getting Started

### Install dependencies (Ultralytics YOLOv8)

```bash
pip install ultralytics
```

### Training Example

```bash
yolo detect train model=yolov8n.pt data=data.yaml epochs=50 imgsz=640
```

### Inference Example

```bash
yolo detect predict model=models/best.pt source=datasets/X-rays/test
```

> Output predictions will be saved to `notebooks/predictions/`.

---

## 📓 Notebooks

- `detect_xrays.ipynb` – Run inference on new X-ray images.
- `search-progress.md` – Notes on experiments and iterations.
- `challenges.md` – Challenges and considerations in labeling and preprocessing.

---

## 🗂️ models/

Trained YOLOv8 models (`best.pt`, `last.pt`) are stored here after training for future inference or fine-tuning.

---

## 📊 reports/

Any evaluation metrics, result summaries, and model performance charts go here.

---

## ⚠️ Notes

- If you're seeing labels like `person` or `sports ball`, it likely means you're using the COCO-trained YOLOv8 model. Train or fine-tune it on this dataset to detect dental-specific classes.
- All predicted images should be saved directly to `notebooks/predictions/`.