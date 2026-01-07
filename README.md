# Video Background Removal using MediaPipe Selfie Segmentation

This repository demonstrates a simple and fast approach to removing backgrounds from short-form, human-centric videos (e.g. Shorts, Reels, talking-head clips) using **semantic segmentation**.

The goal of this project is to showcase **applied AI decision-making**, not to build a heavy production pipeline.

---

## Problem Statement

Remove the background from short-form videos where:
- A single human subject is clearly visible
- The camera is mostly front-facing
- Real-time or near-real-time performance matters

At a pixel level, the task reduces to:
> For each pixel in each frame — does it belong to a human or the background?

---

## Approach

### Why Semantic Segmentation?
- Background subtraction fails for dynamic scenes
- Object detection provides bounding boxes, not pixel-accurate cutouts
- Full matting models are computationally expensive and overkill for demos

**Semantic segmentation** provides the right balance of speed, accuracy, and simplicity.

---

## Model Used

**MediaPipe Selfie Segmentation**
- Pretrained human segmentation model by Google
- Optimized for portrait/selfie-style videos
- Real-time capable on CPU

The model outputs a **per-pixel probability mask** indicating how likely each pixel belongs to a person.

---

## Pipeline Overview

1. Read the input video frame-by-frame  
2. Convert each frame from BGR → RGB  
3. Run MediaPipe Selfie Segmentation  
4. Threshold the probability mask (`> 0.5`)  
5. Keep foreground pixels and replace background pixels  
6. Write processed frames to a new video  

Each frame is processed independently to keep the pipeline simple and fast.

---

## Tradeoffs & Limitations

- Minor edge flickering may occur (especially around hair)
- No temporal smoothing across frames
- Assumes one dominant human subject
- Designed for short-form videos, not cinematic matting

These are **intentional tradeoffs** for speed and clarity.

---

## Requirements

- Python 3.10 or 3.11
- OpenCV
- MediaPipe
- NumPy

Install dependencies:
pip install -r requirements.txt


## Usage
Place an input video named input.mp4 in the project directory

Run:
code.py

Output will be saved as:
output_no_bg.mp4




