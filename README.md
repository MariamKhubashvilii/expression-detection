# Real-Time Facial Expression Detection (Heuristic, dlib)

This project is a real-time facial expression detector built with OpenCV and dlib.  
It uses facial landmarks and simple geometric heuristics (not machine learning) to classify expressions and react to them with spoken comments.

The goal is to explore how far you can go with lightweight, interpretable rules instead of heavy emotion-classification models, while keeping everything fast and explainable.

---

## What It Does

- Captures live video from your webcam
- Detects faces using dlib’s frontal face detector
- Extracts 68 facial landmarks per face
- Computes simple geometric features (mouth, eyes, brows)
- Classifies expressions into:
  - happy
  - sad
  - angry
  - surprised
  - neutral
- Smooths predictions across frames to reduce flicker
- Reacts with short spoken comments using the macOS `say` command

This is not a trained emotion recognition model. All classification is rule-based and fully transparent.

---

## Why Heuristics (Not ML)?

Many emotion detection demos rely on black-box models that are hard to interpret, expensive to run, and tricky to debug. This project intentionally avoids that and instead focuses on:

- Interpretable facial geometry
- Simple ratios that scale across face sizes
- Clear thresholds you can tune yourself

---

## How It Works (High Level)

- Face detection using dlib’s frontal face detector
- Landmark extraction (68 facial points)
- Normalization using outer eye-corner distance
- Feature extraction (mouth, eyes/EAR, brow gap, curvature)
- Rule-based classification with threshold logic
- Temporal smoothing using majority vote across frames
- Audio feedback with a cooldown to prevent spam

---

## Requirements

- Python 3.8+
- macOS (for the built-in `say` command)
- Webcam

---

## Install Dependencies

```bash
pip install opencv-python dlib numpy pillow
