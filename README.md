# Weapon Detection System Using YOLOv8

A deep learning-based **weapon detection system** built with **YOLOv8** for detecting **Handguns** and **Knives** in images and videos.

This project was trained and evaluated on a custom weapon dataset in **YOLO format** and tested on both validation data and external images/videos.

---

## Project Overview

This project uses **YOLOv8s** as the base object detection model and fine-tunes it to detect two weapon classes:

- **Knife**
- **Handgun**

The complete workflow includes:

1. Dataset preparation
2. Model training
3. Validation and evaluation
4. External image testing
5. Video inference

This repository is useful for:

- Academic mini-projects
- Object detection learning
- Computer vision practice
- Security/surveillance prototype demonstrations

---

## Features

- Detects **Handguns** and **Knives**
- Built using **YOLOv8**
- Supports **image inference**
- Supports **video inference**
- Includes **evaluation metrics**
- Includes **confusion matrix**
- Includes **precision-recall / F1 / confidence curves**
- Tested on **external real-world images and video**

---

## Model

- **Framework:** Ultralytics YOLOv8
- **Model used:** `yolov8s.pt`
- **Task:** Object Detection
- **Classes:** 2
  - Knife
  - Handgun

---

## Dataset

This project was trained on a weapon detection dataset in YOLO format containing:

- **2 classes**
  - Knife
  - Handgun

### Dataset Structure

```text
dataset/
├── images/
│   ├── train/
│   └── val/
├── labels/
│   ├── train/
│   └── val/
└── dataset.yaml
```

### Dataset YAML

```yaml
path: /path/to/dataset
train: images/train
val: images/val

names:
  0: Knife
  1: Handgun
```

---

## Training Setup

The model was trained with the following configuration:

- **Model:** YOLOv8s
- **Image size:** 640
- **Batch size:** 16
- **Epochs:** 50
- **Platform:** Kaggle Notebook with GPU

### Training Code

```python
from ultralytics import YOLO

model = YOLO("yolov8s.pt")

model.train(
    data="weapon_data.yaml",
    epochs=50,
    imgsz=640,
    batch=16,
    project=".",
    name="weapon_detection_yolov8s"
)
```

---

## Evaluation Results

The trained model was evaluated on the validation set.

### Overall Performance

| Metric | Value |
|--------|------:|
| Precision | 0.676 |
| Recall | 0.692 |
| mAP@0.50 | 0.680 |
| mAP@0.50:0.95 | 0.371 |

### Class-wise Performance

| Class | Precision | Recall | mAP@0.50 | mAP@0.50:0.95 |
|------|----------:|-------:|---------:|--------------:|
| Knife | 0.590 | 0.644 | 0.600 | 0.222 |
| Handgun | 0.763 | 0.740 | 0.760 | 0.519 |

---

## Result Analysis

### Key Observations

- The model performs **better on Handguns** than on Knives.
- **Knife detection is weaker**, especially in cluttered or complex scenes.
- The model shows **limited confusion between Knife and Handgun**, which is a positive sign.
- Some **false positives** occur in background regions.
- Based on the **F1-Confidence Curve**, a confidence threshold around **0.30** provides a good balance between precision and recall.

### Practical Conclusion

The model is suitable for:

- Academic demonstration
- Proof-of-concept systems
- Basic surveillance/object detection prototypes

It is **not yet a production-ready real-world surveillance model**, especially because knife detection still needs improvement.

---

## Validation Visualizations

This project includes the following evaluation outputs:

- Confusion Matrix
- Normalized Confusion Matrix
- Precision-Recall Curve
- Precision-Confidence Curve
- Recall-Confidence Curve
- F1-Confidence Curve
- Validation batch predictions

Example files:

```text
confusion_matrix.png
confusion_matrix_normalized.png
BoxPR_curve.png
BoxP_curve.png
BoxR_curve.png
BoxF1_curve.png
val_batch0_pred.jpg
val_batch1_pred.jpg
val_batch2_pred.jpg
```

---

## External Testing

The trained model was also tested on **external images** and **video**.

### External Image Testing Observations

- Handguns were detected more consistently.
- Knife detection worked in some cases, but failed in cluttered scenes.
- Some images produced extra or duplicate handgun detections.
- Complex scenes remain challenging for the model.

### Video Inference

The model was successfully run on an external test video, and the predicted output video was generated with bounding boxes.

---

## Project Structure

```text
Weapon-Detection-System-Using-YOLOv8/
├── README.md
├── requirements.txt
├── weapon_detection.ipynb
├── best.pt
└── sample_outputs/
    ├── confusion_matrix.png
    ├── confusion_matrix_normalized.png
    ├── BoxPR_curve.png
    ├── BoxP_curve.png
    ├── BoxR_curve.png
    ├── BoxF1_curve.png
    ├── val_batch0_pred.jpg
    ├── val_batch1_pred.jpg
    ├── val_batch2_pred.jpg
    ├── external_image_result_1.jpg
    ├── external_image_result_2.jpg
    └── output_video.avi
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/SibtainAbbas1965/Weapon-Detection-System-Using-YOLOv8.git
cd Weapon-Detection-System-Using-YOLOv8
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Requirements

Example `requirements.txt`:

```txt
ultralytics
torch
torchvision
opencv-python
matplotlib
numpy
PyYAML
Pillow
```

---

## How to Run

### 1. Train the Model

Use the training notebook or Python script to train YOLOv8 on the dataset.

### 2. Validate the Model

Run validation on the saved `best.pt` weights.

### 3. Run Image Inference

```python
from ultralytics import YOLO

model = YOLO("best.pt")
results = model.predict(source="test.jpg", conf=0.30, save=True)
```

### 4. Run Video Inference

```python
from ultralytics import YOLO

model = YOLO("best.pt")
results = model.predict(source="test_video.mp4", conf=0.30, save=True)
```

---

## Future Improvements

Possible future improvements for this project:

- Improve knife detection performance
- Train on a larger and more diverse dataset
- Reduce false positives in background regions
- Add real-time webcam inference
- Deploy as a web application
- Test on CCTV-style surveillance data
- Compare YOLOv8n / YOLOv8s / YOLOv8m models

---

## Limitations

- Knife detection is weaker than handgun detection.
- The model may miss small or partially visible weapons.
- False positives may occur in cluttered scenes.
- Performance may drop on unseen real-world conditions.

---

## License

This project is licensed under the **MIT License**.

---

## Author

**Sibtain Abbas**  
GitHub: [SibtainAbbas1965](https://github.com/SibtainAbbas1965)
