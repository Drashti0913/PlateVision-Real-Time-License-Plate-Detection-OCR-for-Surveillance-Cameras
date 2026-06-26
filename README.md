# PlateVision — Real-Time License Plate Detection & OCR for Surveillance Cameras

> YOLOv5 + Tesseract OCR · Haar Cascade detection · Real-time video processing · Multiple environment conditions

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green?style=flat-square)
![YOLOv5](https://img.shields.io/badge/Detection-YOLOv5-red?style=flat-square)
![OCR](https://img.shields.io/badge/OCR-Tesseract-orange?style=flat-square)

---

## Overview

PlateVision is an end-to-end license plate detection and recognition pipeline built for surveillance camera footage. It combines **YOLOv5 object detection** with **Tesseract OCR** and **Haar Cascade classifiers** to locate, extract, and read alphanumeric plate text from real-time or recorded video — across varying lighting and weather conditions.

Includes Indian state identification from plate character patterns.

---

## Pipeline

```
Video / Image Input
        │
        ▼
┌───────────────────────┐
│  Plate Detection       │
│  YOLOv5 + Haar        │
│  Cascade (haarcascade │
│  _russian_plate.xml)  │
└───────────┬───────────┘
            │ bounding box crop
            ▼
┌───────────────────────┐
│  Image Preprocessing  │
│  Grayscale → Thresh   │
│  → Noise filtering    │
│  → Contour detection  │
└───────────┬───────────┘
            │ cleaned plate ROI
            ▼
┌───────────────────────┐
│  Tesseract OCR        │
│  Alphanumeric         │
│  character extraction │
└───────────┬───────────┘
            │
            ▼
   Plate text + State ID
   Bounding box overlay
   Saved output image/video
```

---

## Results

| Input | Detection |
|---|---|
| ![Result](Result.png) |
---

## Features

- Real-time detection from surveillance video streams (`video.mp4`)
- Works across diverse lighting, angles, and weather conditions
- Alphanumeric OCR with Indian state code identification
- Bounding box overlay with extracted text display
- Multiple detection scripts for different scenarios (`main.py` → `main5.py`)

---

## Iteration History

The repo contains 6 progressive implementations (`main.py` through `main5.py`) representing the development journey:

| Version | Approach |
|---|---|
| `main.py` | Haar Cascade only, static images |
| `main2.py` | Added Tesseract OCR pipeline |
| `main3.py` | Preprocessing improvements (adaptive threshold) |
| `main4.py` | Multi-plate detection (multiple cars) |
| `main5.py` | Video stream processing, real-time output |

---

## Quick Start

```bash
git clone https://github.com/Drashti0913/Numberplate-Recognition-SurvilalnceCameras.git
cd Numberplate-Recognition-SurvilalnceCameras

pip install opencv-python numpy pytesseract

# Install Tesseract OCR engine
# Mac: brew install tesseract
# Ubuntu: sudo apt install tesseract-ocr
# Windows: https://github.com/UB-Mannheim/tesseract/wiki

# Run on image
python main.py --source car1.jpeg

# Run on video
python main5.py --source video.mp4
```

---

## Tech Stack

| Component | Technology |
|---|---|
| Object detection | YOLOv5 + Haar Cascade |
| OCR engine | Tesseract (`pytesseract`) |
| Image processing | OpenCV (grayscale, threshold, contours) |
| Video processing | OpenCV VideoCapture |
| Language | Python 3.8+ |

---

## Key Challenges Solved

**Variable lighting:** Adaptive thresholding instead of fixed binary threshold — handles shadows, glare, and night footage better than a static value.

**Skewed plates:** Contour-based rotation correction before OCR — plates at an angle produce garbage text without this step.

**Multiple plates in frame:** Contour area filtering to isolate individual plate regions when multiple vehicles appear simultaneously.

**OCR noise:** Post-processing to strip non-alphanumeric characters and apply Indian plate regex patterns for validation.

---

## License

MIT
