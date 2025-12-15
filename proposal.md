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
- **Source:** Roboflow Universe – *New Pothole Detection Dataset*  
  https://universe.roboflow.com/smartathon/new-pothole-detection
- **Dataset Characteristics:**
  - Annotated road images containing potholes under varying lighting, weather, and road conditions
  - Bounding box annotations suitable for object detection
- **Classes:**
  - *Pothole*
- **Acquisition & Preparation:**
  - Dataset download via Roboflow API
  - Automatic train/validation/test split provided by Roboflow
  - Optional manual inspection and refinement of annotations
  - Export format compatible with YOLO models

## 5. Technical Approach
### Model Architecture
- **Primary Model:** YOLOv12 (latest YOLO architecture optimized for accuracy and speed)
- **Weights:** Custom-trained weights (`best.pt`) from the Roboflow pothole dataset
- **Deployment Style:** Server-side inference using Flask for real-time visualization

### Frameworks & Tools
- **Deep Learning Framework:** PyTorch
- **Detection Framework:** Ultralytics YOLO
- **Backend:** Flask (Python)
- **Computer Vision:** OpenCV
- **Visualization & Annotation:** Supervision
- **Dataset Management:** Roboflow
- **Training Environment:** Google Colab with GPU acceleration (T4 / L4)

### System Architecture
The system follows a client–server architecture:
- The **Flask backend** handles video ingestion, YOLOv12 inference, and annotation rendering.
- A **web-based dashboard** displays the live video stream and detection statistics.
- The model processes each frame, detects potholes, and overlays bounding boxes and labels before streaming the output to the client.

## 6. Expected Challenges & Mitigations
- **Challenge:** Variability in road texture, lighting, and weather conditions  
  **Mitigation:** Extensive data augmentation and transfer learning with pretrained weights
- **Challenge:** False positives caused by shadows, oil stains, or road cracks  
  **Mitigation:** Inclusion of hard negative samples and refinement of bounding box annotations
- **Challenge:** Computational limitations during training or inference  
  **Mitigation:** Use of lightweight YOLOv12 variants and reduced input resolution
  
## 7. Expected Outcome
A fully functional pothole detection model that can detect potholes in road videos in real time and display them with bounding boxes, providing useful information for road maintenance planning and safety monitoring.
