# Road Pothole Detection Using Deep Learning-Based Computer Vision
**CSC173 Intelligent Systems Final Project**  
*Mindanao State University – Iligan Institute of Technology*  

**Student:** Shir Keilah Connor, 2022-5474  
**Semester:** AY 2025-2026 Sem 1  
**GitHub Repo:** `kunnow/CSC173-DeepCV-Connor`  

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://python.org) [![Ultralytics](https://img.shields.io/badge/Ultralytics-YOLO-orange)](https://docs.ultralytics.com) [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)](https://jupyter.org)

---

## Abstract
Potholes are a common road hazard that can cause vehicle damage and increase accident risk, especially in areas where roads deteriorate quickly due to weather and heavy traffic. This project develops a **pothole detection system** using the **Ultralytics YOLO object detection framework** and deploys it as a **Flask-free Jupyter Notebook dashboard** for real-time demonstrations. The model is trained using the Roboflow Universe **“New pothole detection”** dataset (9,240 labeled images) [2][3]. After training for **50 epochs**, the model achieves an overall **mAP@0.50 = 0.62** and **mAP@0.50:0.95 = 0.36**, with the best performance on **large potholes** (mAP@0.50 = 0.77). The dashboard loads the trained weights (`best.pt`), runs inference on a video file or webcam stream, draws bounding boxes with confidence scores (e.g., `pothole 0.82`), and displays live statistics such as detection count and inference behavior. By packaging both training and deployment inside notebooks (`train.ipynb` and `pothole_detection.ipynb`), the project remains reproducible, presentation-ready, and aligned with course submission requirements.

---

## Table of Contents
- [Introduction](#introduction)
- [Related Work](#related-work)
- [Methodology](#methodology)
- [Experiments & Results](#experiments--results)
- [Discussion](#discussion)
- [Ethical Considerations](#ethical-considerations)
- [Conclusion](#conclusion)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Demo](#demo)
- [References](#references)s

---

## Introduction

### Problem Statement
Road potholes reduce driving safety and comfort and can lead to costly vehicle repairs. Manual inspection is slow and inconsistent, especially across large road networks. A computer vision model can help automatically detect potholes from road video (dashcam/phone/roadside cameras), supporting quicker reporting and maintenance prioritization.

### Objectives
- Train an object detector to identify **potholes** in road images/videos.
- Evaluate performance using standard detection metrics (precision/recall and mAP) [4].
- Deploy a **Jupyter Notebook dashboard** for interactive, real-time inference.
- Provide demo-ready outputs (annotated frames/video + summary stats).

---

## Related Work
- **YOLO** is a widely used real-time object detection approach that predicts bounding boxes and classes in a single forward pass, enabling fast inference [1].
- **Ultralytics YOLO** provides practical training/validation/prediction workflows and standardized reporting of detection metrics such as mAP@0.50 and mAP@0.50:0.95 [4][5].
- **Roboflow Universe** hosts open datasets and tooling for computer vision training pipelines, including pothole detection datasets used for this project [2][3].

---

## Methodology

### Dataset
- **Source:** Roboflow Universe – *New pothole detection* (Smartathon) [2][3]  
- **Size:** 9,240 labeled pothole images [2][3]  
- **Task:** Object detection (bounding boxes)  
- **Splits:** As provided by the dataset export (train/valid/test)
- **Preprocessing:** Standard YOLO resizing/augmentation pipeline during training.

### Architecture
- **Detector:** Ultralytics YOLO detection model (custom-trained weights: `best.pt`)  
- **Output:** Bounding boxes + confidence score + class label (pothole)

### Training (Notebook)
Training and evaluation are implemented in:
- `train.ipynb`

The training run in the notebook uses **50 epochs**, and produces:
- `loss_curve.png` (training/validation losses + precision/recall + mAP curves)
- `map_curve.png` (mAP summary plot)

---

## Experiments & Results

### Training Curves (50 Epochs)
> These images are generated from `train.ipynb` and should be committed to the repo so they render on GitHub.

![Training Curves](images/final%20(50%20epoch)/loss_curve.png)  
![mAP Summary](images/final%20(50%20epoch)/map_curve.png)

### Metrics (from `train.ipynb`)
Ultralytics reports and common definitions:
- **mAP@0.50** = Average Precision at IoU 0.50  
- **mAP@0.50:0.95** = COCO-style average across IoU thresholds from 0.50 to 0.95 [4][6]

**Overall mAP:**
| Metric | Value |
|---|---:|
| **mAP@0.50:0.95** | **0.36** |
| **mAP@0.50** | **0.62** |
| **mAP@0.75** | **0.38** |

**mAP by Object Size:**
| Object Size | mAP@0.50:0.95 | mAP@0.50 | mAP@0.75 |
|---|---:|---:|---:|
| **Small** | 0.13 | 0.34 | 0.07 |
| **Medium** | 0.30 | 0.57 | 0.31 |
| **Large** | 0.49 | 0.77 | 0.55 |

### Demo (Notebook Dashboard)
Inference is deployed as a notebook dashboard using `ipywidgets`:
- `pothole_detection.ipynb`

The dashboard supports:
- Start/Stop controls (responsive Stop)
- Video or webcam input
- Confidence and IoU sliders
- On-frame labels with confidence (e.g., `pothole 0.82`)
- Optional export of annotated output video

---

## Discussion
**Strengths**
- Notebook-first deployment is ideal for academic submissions and live demos.
- Results show strong performance for **medium/large potholes**, with lower performance for **small potholes** (a known challenge in detection due to fewer pixels and weaker features).

**Limitations**
- Small potholes and low-contrast scenes (shadows, glare, wet roads) can reduce detection reliability.
- Performance depends on dataset diversity (lighting, camera angle, road texture) and annotation quality.

**Insights**
- The per-size mAP breakdown suggests future improvements should focus on increasing small-object examples or using higher-resolution training/inference for small potholes.

---

## Ethical Considerations
- **Privacy:** Road videos may capture people/vehicles. Use data responsibly and avoid sharing identifiable information.
- **Bias / Coverage:** The dataset may not represent all road types or weather conditions equally; this can affect real-world generalization.
- **Intended Use:** This project is for pothole detection; repurposing for surveillance is discouraged.

---

## Conclusion
This project demonstrates a YOLO-based pothole detector trained on an open pothole dataset and deployed in a clean, interactive Jupyter dashboard suitable for final project presentation. The model achieves solid mAP@0.50 performance and shows higher reliability on medium/large potholes. Future work can improve small pothole detection, expand dataset diversity, and optimize inference speed for edge deployment.

---

## Installation
```bash
# 1) Clone the repository
git clone https://github.com/kunnow/CSC173-DeepCV-Connor.git
cd CSC173-DeepCV-Connor

# 2) Create and activate a virtual environment
python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# 3) Install dependencies
pip install -r requirements.txt
```

---

## Usage

### 1) Training
Open and run:
- `train.ipynb`

This produces training outputs and weights in the Ultralytics `runs/` directory, including:
- `runs/detect/train/weights/best.pt`

### 2) Inference Dashboard
Open and run:
- `pothole_detection.ipynb`

Inside the notebook:
1. Set `best.pt` path (or copy it to project root)
2. Choose video file (e.g., `demo.mp4`) or webcam
3. Click **Start**
4. Click **Stop** to end safely

---

## Project Structure
```txt
CSC173-DeepCV-Connor/
├─ dataset/                               # gitignored
│  └─ New-pothole-detection-2/
│
├─ images/
│  ├─ final_50_epoch/
│  │  ├─ loss_curve.png
│  │  └─ map_curve.png
│  └─ initial_10_epoch/
│     ├─ loss_curve.png
│     └─ map_curve.png
│
├─ notebooks/
│  ├─ pothole_detection.ipynb
│  └─ train.ipynb
│
├─ videos/
│  ├─ pothole_demo1.mp4
│  └─ pothole_demo2.mp4
│
├─ weights/
│  ├─ 10_epoch/
│  │  └─ best.pt
│  └─ 50_epoch/
│     ├─ best.pt
│     └─ last.pt
│
├─ .gitignore
├─ best.pt                                 # trained weights
├─ demo.mp4                                # test video
├─ progress.md
├─ proposal.md
├─ README.md
└─ requirements.txt
```

---

## Demo
**Video:** [CSC173_Connor_Final.mp4](https://drive.google.com/drive/folders/12YFozZykcpD-kANAYplqiISvTK19Qlrz?usp=sharing)

---

## References
[1] J. Redmon, S. Divvala, R. Girshick, A. Farhadi. “You Only Look Once: Unified, Real-Time Object Detection,” CVPR 2016. https://arxiv.org/abs/1506.02640  
[2] Roboflow Universe. “New pothole detection” dataset (Smartathon). https://universe.roboflow.com/smartathon/new-pothole-detection  
[3] Roboflow Universe. “New pothole detection (v2)” dataset version page. https://universe.roboflow.com/smartathon/new-pothole-detection/dataset/2  
[4] Ultralytics Docs. “Performance Metrics Deep Dive” (Precision, Recall, mAP50, mAP50-95). https://docs.ultralytics.com/guides/yolo-performance-metrics/  
[5] Ultralytics Docs. “Model Validation (Val mode).” https://docs.ultralytics.com/modes/val/  
[6] Roboflow Blog. “Mean Average Precision (mAP) explained” (COCO-style AP@[.5:.95]). https://blog.roboflow.com/mean-average-precision/
