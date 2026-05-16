# Continuous Gesture Signal Classification via Triggered Spatial Extraction and Temporal Attention

## Authors
**Rhiane Miguel Veron Dalumpines**

**Niño Renzonald Driz**

**John Caleb Restituto** 

*Department of Computer Engineering, University of Science and Technology of Southern Philippines (USTP) — Cagayan de Oro, Philippines*

---

## Overview
This repository contains the implementation of a lightweight, stability-aware framework for real-time dynamic sign recognition. By integrating robust skeletal tracking with an intentionality-based activation trigger, high-fidelity spatial embeddings, and sequence-based temporal attention, the system successfully filters out background noise and casual movements for highly accurate continuous gesture classification.

## Architecture Pipeline

| Stage | Technology | Role in Pipeline |
| :--- | :--- | :--- |
| **1. Skeletal Tracking** | MediaPipe Hands (Tasks API) | Extracts 21 3D keypoints to compute a dynamic bounding box, isolating the hand region (ROI) from background clutter. |
| **2. Intentionality Trigger**| Open-Palm State Machine | Monitors for a static open-palm pose ($N$ frames). Transitions system from **IDLE** $\rightarrow$ **ARMED** $\rightarrow$ **RECORDING** to prevent false positives. |
| **3. Spatial Extraction** | EfficientNetB3 (PyTorch) | Processes cropped ROI frames into 1536-D feature vectors per frame, ensuring robustness to spatial variations and lighting. |
| **4. Temporal Classification**| Transformer Encoder | Analyzes the spatiotemporal sequence ($T=32$ frames) using self-attention to classify the gesture based on global trajectories. |

## Dataset & Scope
Trained on a curated subset of the **IPN Hand Dataset** to optimize for real-time inference and rapid iteration. The model specifically targets 5 robust gesture classes:
* `B0A` — Pointing (one finger)
* `G03` — Throw up
* `G04` — Throw down
* `G06` — Throw right
* `G07` — Open twice

## Performance Insights
The system utilizes **EfficientNetB3** as the spatial backbone, explicitly chosen to resolve mode collapse issues observed during earlier architectural testing.
* **Peak Training Accuracy:** 99.72%
* **Validation Accuracy:** 93.26%
* **Validation Loss:** 0.79
* **Real-World Detection:** Robust, stable real-time tracking and successful classification across all 5 target classes.