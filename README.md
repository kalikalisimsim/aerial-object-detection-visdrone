# Aerial Object Detection Using YOLO11n and VisDrone

## Project Overview

This project implements an aerial object detection system using **YOLO11n** and the **VisDrone2019-DET dataset**.

The objective is to detect people and vehicles in images captured from aerial platforms, such as drones.

The project also investigates how occlusion affects person detection performance.

## Objectives

- Prepare and convert VisDrone annotations into YOLO format.
- Train a YOLO11n object detection model.
- Detect people and vehicles in aerial images.
- Evaluate model performance using precision, recall and mAP.
- Explore the effect of occlusion on person detection.

## Technologies Used

- Python
- PyTorch
- Ultralytics YOLO11n
- OpenCV
- NumPy
- Google Colab
- VisDrone2019-DET

## Dataset

**VisDrone2019-DET**

The dataset contains aerial images with annotations for multiple object categories.

For this project, the categories were consolidated into two classes:

| Original categories | New class |
|---|---|
| Pedestrian, People | Person |
| Car, Van, Truck, Bus, Motor, Tricycle, Awning-tricycle | Vehicle |

Ignored regions, bicycles and the Others category were excluded.

### Dataset split

- Training images: 6,471
- Validation images: 548

## Methodology

1. Downloaded and explored the VisDrone dataset.
2. Examined the original bounding-box annotations.
3. Converted VisDrone annotations into normalized YOLO format.
4. Created the dataset configuration file (`data.yaml`).
5. Loaded pretrained YOLO11n weights.
6. Trained the model for three pilot epochs using a Tesla T4 GPU.
7. Generated predictions on validation images.
8. Analysed person detection performance across different occlusion levels.

## Model Training

Model: YOLO11n  
Image size: 640 × 640  
Epochs: 3  
Batch size: 8  
Device: NVIDIA Tesla T4 GPU  
Classes: Person, Vehicle

## Pilot Training Results

| Metric | Result |
|---|---:|
| Precision | 58.7% |
| Recall | 41.4% |
| mAP@50 | 44.6% |
| mAP@50–95 | 22.1% |

These are preliminary results from a three-epoch pilot experiment, not a fully optimized model.

## Occlusion Analysis

The original VisDrone annotations were used to examine person instances at three occlusion levels.

### Validation dataset distribution

| Occlusion level | Instances |
|---|---:|
| Level 0 – No occlusion | 6,337 |
| Level 1 – Partial occlusion | 6,807 |
| Level 2 – Heavy occlusion | 825 |

### Preliminary detection recall

Using an IoU matching threshold of 0.5, the initial evaluation produced:

| Occlusion level | Recall |
|---|---:|
| Level 0 | 53.48% |
| Level 1 | 44.38% |
| Level 2 | 30.67% |

These results suggest that person detection becomes more difficult as occlusion increases.

**Evaluation limitation:** The initial evaluation script produced a very high false-positive count, and changing the intended confidence threshold did not change the reported results. Therefore, the occlusion-wise recall figures are exploratory and require validation before being treated as final benchmark results.

## Project Structure

```text
aerial-object-detection-visdrone/
│
├── README.md
├── requirements.txt
│
├── models/
│
├── notebooks/
│   └── YOLO_Aerial_Object_Detection_VisDrone.ipynb
│
└── results/
    ├── training_graphs/
    ├── predictions/
    └── evaluation/
```

## Future Improvements

- Train for more epochs and compare performance.
- Improve small-object detection.
- Validate occlusion-wise evaluation.
- Investigate methods for detecting heavily occluded people.
- Explore deployment in a simulated UAV environment.

## Research Relevance

This project provides a baseline for aerial perception in applications such as disaster monitoring and search-and-rescue operations.

It explores the challenges of detecting people from aerial viewpoints, particularly under partial and heavy occlusion.

## Acknowledgements

Dataset: VisDrone2019-DET.

Model framework: Ultralytics YOLO.

