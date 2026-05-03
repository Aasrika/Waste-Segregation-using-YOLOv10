# Waste Segregation using YOLOv10

> Published at **IEEE ICICT 2025** | DOI: [10.1109/ICICT64420.2025.11004951](https://doi.org/10.1109/ICICT64420.2025.11004951)

An end-to-end real-time waste detection and classification system using YOLOv10, trained on a custom-annotated dataset to classify waste into **Recyclable**, **Biodegradable**, and **Non-Biodegradable** categories.

---

## Overview

Improper waste disposal contributes to greenhouse gas emissions, soil contamination, and public health hazards. This project proposes an automated waste segregation framework using YOLOv10, achieving **88% overall accuracy** and **20 FPS real-time inference** — 2× faster than Faster R-CNN — enabling practical deployment in automated sorting pipelines.

---

## Results

Category - Precision 
Recyclable -91% 
Biodegradable - 84% 
Non-Biodegradable - 86% 
**Overall Accuracy**  **88%** 

- **Inference Speed:** 20 FPS on NVIDIA GPU (vs. 10 FPS for Faster R-CNN)
- **Training:** 200 epochs, batch size 32, Adam optimizer
- **Dataset:** 1,387 images — 1,093 train / 200 validation / 94 test

---

## Dataset

Custom dataset built and annotated using **Roboflow**, divided into 3 classes:

- **Recyclable** — plastics, glass, metals
- **Biodegradable** — food waste, paper, organic material
- **Non-Biodegradable** — synthetic fibres, certain plastics

Augmentation strategies applied:
- Random horizontal/vertical flips
- Random rotations
- Brightness and contrast variation

---

## Model Architecture

- **Base Model:** YOLOv10 (Ultralytics)
- Convolutional feature extraction layers → Detection head for bounding box regression and classification
- Transfer learning from pretrained COCO weights
- INT8-compatible for edge deployment

---

## Installation

```bash
git clone https://github.com/KANlKA/waste-segregation-yolov10
cd waste-segregation-yolov10
pip install -r requirements.txt
```

**Requirements:**
```
ultralytics
torch>=2.0.0
roboflow
opencv-python
numpy
matplotlib
```

---

## Usage

### Training
```python
from ultralytics import YOLO

model = YOLO("yolov10n.pt")  # load pretrained weights
model.train(
    data="waste_dataset.yaml",
    epochs=200,
    batch=32,
    imgsz=640,
    lr0=0.001
)
```

### Inference
```python
from ultralytics import YOLO
import cv2

model = YOLO("runs/train/weights/best.pt")
results = model.predict(source="test_images/", conf=0.5, save=True)
```

### Real-time Detection
```python
model.predict(source=0, show=True, conf=0.5)  # webcam
```



## Experimental Setup

| Component | Details |
|---|---|
| Hardware | Intel Core i7, 16GB RAM |
| Framework | YOLOv10 (Ultralytics), Python 3.10 |
| Annotation Tool | Roboflow |
| Epochs | 200 |
| Batch Size | 32 |
| Optimizer | Adam |

---


## Publication

If you use this work, please cite:

```bibtex
@INPROCEEDINGS{11004951,
  author={Aasrika, Kambhampati and P, Mehak Naaz and Karthikeyan, P},
  booktitle={2025 International Conference on Inventive Computation Technologies (ICICT)}, 
  title={Waste Segregation Using YOLOv10 for Sustainable Waste Management}, 
  year={2025},
  volume={},
  number={},
  pages={13-19},
  keywords={YOLO;Waste reduction;Accuracy;Buildings;Water conservation;Water pollution;Recycling;Greenhouse gases;Water resources;Sorting;Waste management;Machine learning;YOLOv10(You Only Look Once);Waste Separation;Object Detection;Multi-object detections},
  doi={10.1109/ICICT64420.2025.11004951}}

```

---

## Authors

- **Kambhampati Aasrika** — RV University
- **Mehak Naaz P** — RV University
- **P Karthikeyan** — RV University (Faculty Supervisor)

---

