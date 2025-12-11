# CSC173 Deep Computer Vision Project Proposal
**Student:** Shir Keilah T. Connor, 2022-5474
**Date:** December 11, 2025

## 1. Project Title
Road Pothole Detection Using Deep Learning-Based Computer Vision

## 2. Problem Statement
Road potholes are a major factor contributing to vehicle damage, traffic slowdowns, and roadway accidents. Manual pothole reporting is inefficient and often delayed, which results in unaddressed hazards. This project aims to develop an automated computer vision system capable of detecting potholes on roads using real‑time or recorded images. By leveraging deep learning, the system can support more efficient maintenance planning and enhance road safety.

## 3. Objectives
- Develop a deep learning model capable of detecting potholes with high accuracy and low false‑positive rate.
- Build a complete pipeline including dataset preprocessing, annotation validation, model training, testing, and performance evaluation.
- Implement a lightweight model suitable for real‑time deployment on resource‑limited devices.
- Produce visual inference outputs highlighting detected potholes.

## 4. Dataset Plan
- **Source:** Kaggle – *Pothole Image Dataset* (approx. 5,000–10,000 images) or *India Pothole Detection Dataset*
- **Classes:**  
  - *Pothole*  
  - *Normal Road*
- **Acquisition:**  
  - Download from Kaggle  
  - Additional Google Street View extraction if needed  
  - Manual annotation refinement using tools like LabelImg or Roboflow

## 5. Technical Approach
### Model Architecture
- Base model: **YOLOv8n** or **YOLOv11n** (lightweight, fast inference)
- Alternative: **EfficientDet‑D0** for balanced performance

### Frameworks & Tools
- **Framework:** PyTorch  
- **Training Environment:** Google Colab (T4/L4 GPU)  
- **Preprocessing:** Data augmentation (random crop, brightness/contrast adjust, blur, weather simulations)

### Pipeline Overview
1. Dataset cleaning and augmentation  
2. Label normalization  
3. Train/val/test splitting  
4. Model training with monitored metrics (mAP50, precision, recall)  
5. Hyperparameter tuning (LR scheduling, mosaic augmentation, batch size optimization)  
6. Inference testing and visualization

## 6. Expected Challenges & Mitigations
- **Challenge:** Variability in road conditions (lighting, weather, camera angle)  
  **Mitigation:** Extensive augmentation and using pretrained weights  
- **Challenge:** Small or imbalanced dataset  
  **Mitigation:** Oversampling, synthetic augmentation, and transfer learning  
- **Challenge:** Model confusion between dark patches and potholes  
  **Mitigation:** Add negative samples and refine annotations  
- **Challenge:** Computational constraints  
  **Mitigation:** Use YOLO‑nano versions and reduce input resolution

## 7. Expected Outcome
A fully functional pothole detection model with clear performance metrics, annotated inference outputs, and a deployment‑ready pipeline applicable for road monitoring and maintenance systems.
