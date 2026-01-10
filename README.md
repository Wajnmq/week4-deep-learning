# Two-Stage Road Damage Risk Detection Pipeline

This project implements a two-stage deep learning pipeline to detect **high-risk road damage cases** using pretrained CNN models.

The approach separates **scene understanding** from **risk assessment** to reduce false positives and focus computation on relevant road damage regions only.

---

## Pipeline Overview

### Stage 1 – Scene Classification (Model 1)

A CNN model is applied to the full image to classify the scene into one of the dataset classes:

- HMV  
- LMV  
- Pedestrian  
- RoadDamages  
- SpeedBump  
- UnsurfacedRoad  

Only images predicted as **RoadDamages** are forwarded to Stage 2.

---

### Stage 2 – Risk Classification (Model 2)

This stage focuses only on road damage regions.

**Process:**
- Use YOLO bounding boxes provided with the dataset
- Select the largest `RoadDamages` bounding box
- Crop the damage region
- Classify the crop into:
  - **No Risk**
  - **Risk**

**Risk labeling (training):**  
Risk labels are derived from the **damage bounding box area ratio** using a threshold computed from the **training split only** (percentile-based), to avoid leakage.

Only **Risk** cases are included in the final output report.

---

## Dataset

The project uses a road anomaly dataset annotated in **YOLO format** with predefined splits:

- `train`
- `valid`
- `test`

Each image has a corresponding `.txt` label file in YOLO format:
<class_id> <x_center> <y_center> <width> <height>

Classes:
- HMV
- LMV
- Pedestrian
- RoadDamages
- SpeedBump
- UnsurfacedRoad

---

## Models

- **Model 1:** EfficientNet-B0 — Scene Classification  
- **Model 2:** ResNet-34 — Risk Classification  

Both models use transfer learning with:
- Frozen backbone training
- Fine-tuning phase

---

## Evaluation

### Model 1 – Scene Classification (Validation)
Overall validation accuracy: **0.89**
### Model 2 – Risk Classification (Validation)
Overall validation accuracy: **0.92**

---

## Output

The pipeline generates a structured report containing **Risk** cases only, including:
- Image identifier
- Damage area ratio
- Risk label
- Model confidence score

---

## Repository Contents

- Supporting notebooks created during the bootcamp  
- Main project notebook implementing the final pipeline

