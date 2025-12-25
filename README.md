# Real-Time Facial Expression Detection (Heuristic, dlib)

This project is a real-time facial expression detector built with OpenCV and dlib. It uses facial landmarks and simple geometric heuristics (not machine learning) to classify expressions and react to them with spoken comments.

The goal is to explore how far you can go with lightweight, interpretable rules instead of heavy emotion-classification models, while keeping everything fast and explainable.

## What It Does
- Captures live video from your webcam
- Detects faces using dlib’s frontal face detector
- Extracts 68 facial landmarks per face
- Computes simple geometric features (mouth, eyes, brows)
- Classifies expressions into: happy, sad, angry, surprised, neutral
- Smooths predictions across frames to reduce flicker
- Reacts with short spoken comments using the macOS `say` command

This is **not** a trained emotion recognition model. All classification is rule-based and fully transparent.

## Why Heuristics (Not ML)?
Many emotion detection demos rely on black-box models that are hard to interpret, expensive to run, and tricky to debug. This project intentionally avoids that and instead focuses on:
- Interpretable facial geometry
- Simple ratios that scale across face sizes
- Clear thresholds you can tune yourself

## How It Works (High Level)
1. Face detection (dlib frontal face detector)
2. Landmark extraction (68 points)
3. Normalization (distances normalized by outer eye-corner distance)
4. Feature extraction (mouth, eyes/EAR, brow gap, curvature)
5. Rule-based classification (threshold rules)
6. Temporal smoothing (majority vote across recent frames)
7. Audio feedback (async speech + cooldown)

## Requirements
- Python 3.8+
- macOS (for built-in `say` command)
- Webcam

Install packages:
```bash
pip install opencv-python dlib numpy pillow
