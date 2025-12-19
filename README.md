# PCB Defect Inspection Using YOLO with Multi-Class Fault Localization

This repository contains a specialized implementation for detecting defects on Printed Circuit Boards (PCBs) using a custom *YOLO* architecture (configured as YOLOv12s) powered by the ultralytics framework. The model is trained on a specific PCB dataset to identify common manufacturing errors such as short circuits, missing holes, and scratches.

## Project Overview

The goal of this project is to provide a high-accuracy automated visual inspection (AVI) solution for PCB quality control. By leveraging transfer learning and custom backbone modifications, the model achieves near-perfect detection rates for critical defects.

### Key Performance Metrics (at 100 Epochs):

* *mAP50*: 0.979
* *mAP50-95*: 0.614
* *Inference Speed*: ~16.3ms per image (on Tesla T4)

## Tech Stack & Requirements

* *Framework*: [Ultralytics YOLO](https://github.com/ultralytics/ultralytics)
* *Environment*: Kaggle (Dual Tesla T4 GPUs)
* *Data Management*: [Roboflow](https://roboflow.com/)
* *Libraries*:
* numpy==1.26.4
* matplotlib==3.8.4
* ultralytics
* roboflow



## Dataset

The model is trained on the *PCB-ECJGA* dataset hosted on Roboflow. It includes 8 classes of defects:

1. falsecopper
2. missinghole
3. mousebite
4. opencircuit
5. pinhole
6. scratch
7. shortcircuit
8. spur

## Model Architecture

A custom configuration file customyolov12s.yaml was developed for this project. It features:

* *Backbone*: Modified layers including C3k2 and A2C2f modules for improved feature extraction.
* *Head*: Multi-scale detection head targeting P3, P4, and P5 feature maps.
* *Input Size*: 640x640.

## Training Results

The model was trained for *100 epochs* with an SGD optimizer and a batch size of 16.

| Class | Images | Instances | Box (P) | R | mAP50 | mAP50-95 |
| --- | --- | --- | --- | --- | --- | --- |
| *All* | *753* | *3852* | *0.974* | *0.959* | *0.979* | *0.614* |
| falsecopper | 142 | 601 | 0.99 | 0.968 | 0.985 | 0.661 |
| scratch | 138 | 363 | 0.955 | 0.937 | 0.981 | 0.838 |
| pinhole | 142 | 488 | 0.974 | 0.982 | 0.984 | 0.517 |

## 💻 Usage

1. *Clone the repository*:
bash
git clone https://github.com/your-username/yolo-pcb-detection.git




2. *Install dependencies*:
bash
pip install ultralytics roboflow numpy==1.26.4 matplotlib==3.8.4




3. *Run Training*:
The training script is provided in the Jupyter notebook yolo-modif.ipynb. Ensure you have your Roboflow API key configured to download the dataset version 2.

## Project Structure

* yolo-modif.ipynb: Core training and evaluation notebook.
* customyolov12s.yaml: Custom model configuration.
* runs/: (Generated) Contains training logs, weights (best.pt, last.pt), and validation plots.

## Credits

* *Ultralytics* for the YOLO implementation.
* *Roboflow* for the dataset hosting and conversion tools.
* *Hubei University of Technology* for the source data.
