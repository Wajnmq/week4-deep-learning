⸻
Two-Stage Road Damage Detection Pipeline

This project implements a two-stage deep learning pipeline for analyzing road damage using pretrained CNN models.

The pipeline separates the task into:
	1.	Scene understanding
	2.	Damage severity estimation

This design helps avoid unnecessary processing by filtering out non-damage scenes early.

⸻

Pipeline Design


Stage 1 – Scene Filter (Model 1)

A CNN classifier is applied to the full image to identify the overall scene.

Classes:
	•	HMV
	•	LMV
	•	Pedestrian
	•	RoadDamages
	•	SpeedBump
	•	UnsurfacedRoad

Only images classified as RoadDamages are passed to the next stage.

⸻

Stage 2 – Damage Severity Estimation (Model 2)

This stage focuses only on road damage regions.

Process:
	•	Use YOLO bounding boxes provided with the dataset
	•	Select the largest RoadDamages bounding box
	•	Crop the damage region
	•	Estimate severity based on the relative size of the damaged area

Severity Levels:
	•	Low
	•	Medium
	•	High

Only high severity cases are included in the final output.

⸻

Dataset

The project uses a road anomaly dataset annotated in YOLO format.

Each image may contain one or more labeled objects from the following classes:
	•	HMV
	•	LMV
	•	Pedestrian
	•	RoadDamages
	•	SpeedBump
	•	UnsurfacedRoad

The dataset is already split into:
	•	train
	•	valid
	•	test

Each image has a corresponding .txt file containing bounding box annotations.

⸻

Output

The pipeline generates a CSV report containing only high-severity road damage cases.

Output file:

high_severity_road_damages.csv

Each record includes:
	•	Image name
	•	Estimated damage area ratio
	•	Severity level
	•	Model confidence

The report is intended for review and further inspection.

⸻

Repository Contents

This repository includes:
	•	A small set of supporting notebooks created during the bootcamp for experimentation and learning
	•	The main project notebook that implements the complete pipeline end to end
