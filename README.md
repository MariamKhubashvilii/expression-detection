# Real-Time Facial Expression Detection (Heuristic, dlib)

This project is a real-time facial expression detector built with OpenCV and dlib. It uses facial landmarks and simple geometric heuristics (not machine learning) to classify expressions and react to them with spoken comments.

The goal is to explore how far you can go with lightweight, interpretable rules instead of heavy emotion-classification models, while keeping everything fast and explainable.

What It Does

Captures live video from your webcam

Detects faces using dlib’s frontal face detector

Extracts 68 facial landmarks per face

Computes simple geometric features (mouth, eyes, brows)

Classifies expressions into: happy, sad, angry, surprised, neutral

Smooths predictions across frames to reduce flicker

Reacts with short spoken comments using the macOS say command

This is not a trained emotion recognition model. All classification is rule-based and fully transparent.

Why Heuristics (Not ML)?

Many emotion detection demos rely on black-box models that are hard to interpret, expensive to run, and tricky to debug. This project intentionally avoids that and instead focuses on:

Interpretable facial geometry

Simple ratios that scale across face sizes

Clear thresholds you can tune yourself

How It Works (High Level)

Face detection using dlib’s frontal face detector

Landmark extraction (68 facial points)

Normalization using outer eye-corner distance

Feature extraction (mouth, eyes/EAR, brow gap, curvature)

Rule-based classification with threshold logic

Temporal smoothing using majority vote across frames

Audio feedback with a cooldown to prevent spam

Requirements

Python 3.8+

macOS (for the built-in say command)

Webcam

Install Dependencies

Install required Python packages:

pip install opencv-python dlib numpy pillow

Notes on dlib Installation

dlib may require CMake and a C++ compiler

On macOS, installing CMake via Homebrew often helps if pip install dlib fails:

brew install cmake

Required Model File (Not Included)

This project requires a pretrained dlib facial landmark model:

shape_predictor_68_face_landmarks.dat


Due to its size, this file is not included in the repository.

How to Set It Up

Download the model from:

http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2


Extract the .dat file

Create a folder called models in the project root (if it does not exist)

Place the file here:

models/shape_predictor_68_face_landmarks.dat


The code checks for this file at startup and exits early with a clear error message if it is missing.

Running the Project

Open and run the notebook:

Expressions.ipynb

Notes

Running inside Jupyter may reduce FPS due to output rendering

For best performance, this logic can be moved into a standalone script using:

cv2.imshow("frame", frame)


instead of notebook display.

Limitations

Thresholds are calibrated to a single face and camera

Lighting conditions affect results

Expressions are simplified and non-clinical

No face tracking between frames

Speech output is macOS-only

This project is intended as an exploratory and educational prototype, not a production emotion-recognition system.
