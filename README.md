# VisionSentinel-RealTime-Anomaly-Detection
# 🚁 VisionSentinel — Real-Time Anomaly Detection

**VisionSentinel** is a vision-based anomaly detection system designed to analyze drone video and identify potentially dangerous events in near real time.

Instead of blindly trusting an AI model's prediction, VisionSentinel uses **Evidence Validation** and **Temporal Verification** to reduce false-positive alerts.

---

## 🎯 Problem

Drone cameras can continuously monitor roads, cities, and large public areas, but manually monitoring video streams is difficult and time-consuming.

A useful automated system should be able to:

* Detect potentially dangerous events
* Analyze video efficiently
* Reduce false positives
* Use multiple frames to verify an event
* Provide an understandable final decision

---

## 💡 Our Solution

VisionSentinel combines a **Vision-Language Model (Qwen)** with two verification layers:

### 1. 🧠 Vision Analysis

Sampled frames from the drone video are analyzed using Qwen to understand the visual scene.

### 2. 🔍 Evidence Gate

The system checks whether the model's anomaly prediction is supported by concrete visual evidence.

For example, the following are **not considered sufficient evidence** by themselves:

* Headlights
* Brake lights
* Reflections
* Shadows
* Normal traffic
* Normal vehicle clustering
* Wet roads

### 3. ⏱️ Temporal Verification

An anomaly must appear consistently across multiple frames before the system confirms it.

This prevents a single incorrect model prediction from immediately becoming an alert.

---

## 🏗️ System Architecture

```text
                 🚁 DRONE VIDEO
                       │
                       ▼
                🎞️ FRAME SAMPLING
                       │
                       ▼
               🧠 QWEN VISION MODEL
                       │
                       ▼
                 🔍 EVIDENCE GATE
                       │
                       ▼
              ⏱️ TEMPORAL VERIFICATION
                       │
                       ▼
                🎯 DECISION ENGINE
                  /           \
                 /             \
                ▼               ▼
          ✅ NORMAL       🚨 ANOMALY
                            CONFIRMED
                       │
                       ▼
                 🖥️ GRADIO UI
```

---

## 🚨 Potential Anomalies

VisionSentinel can be configured to detect visually significant events such as:

* 🚗 Vehicle accidents or collisions
* 🚧 Traffic obstructions
* 🛑 Stopped or stranded vehicles
* 🔥 Fire or smoke
* 👥 Unusual crowding
* ⚠️ Dangerous road activity

---

## 🛡️ Key Innovation

### Prediction ≠ Alert

A major challenge with Vision-Language Models is that they can produce false-positive predictions.

VisionSentinel therefore follows:

```text
AI Prediction
     ↓
Is there concrete visual evidence?
     ↓
Does the event persist across frames?
     ↓
🚨 Confirmed Anomaly
```

This makes the detection pipeline more conservative and reliable.

---

## 🧪 Example

During testing, Qwen initially classified several frames of normal traffic as potential vehicle accidents.

The model's explanations were based on things such as:

* Headlights
* Brake lights
* Multiple vehicles
* Vehicle clustering

VisionSentinel rejected these predictions through the Evidence Gate.

The final result was:

```text
Frames analyzed: 6
Anomalous frames: 0
Normal frames: 6

Evidence Gate: ACTIVE
Temporal Verification: ACTIVE

FINAL DECISION: ✅ NORMAL
```

This demonstrates the system's ability to **suppress false positives rather than blindly forwarding model predictions as alerts**.

---

## ⚙️ Technologies

| Technology                 | Purpose                         |
| -------------------------- | ------------------------------- |
| Python                     | Core development                |
| OpenCV                     | Video and frame processing      |
| PyTorch                    | Model inference                 |
| Qwen Vision-Language Model | Visual reasoning                |
| PIL                        | Image processing                |
| Gradio                     | Interactive demonstration       |
| Google Colab               | Development and GPU environment |

---

## 📂 Project Structure

```text
VisionSentinel-RealTime-Anomaly-Detection/
│
├── README.md
├── notebooks/
│   └── VisionSentinel.ipynb
│
├── data/
│   └── frames/
│
├── demo/
│   └── ...
│
└── requirements.txt
```

> The exact structure can be adjusted depending on how the final notebook and submission files are organized.

---

## 🚀 Workflow

### Step 1 — Video Input

A drone video is provided to the system.

### Step 2 — Frame Sampling

Instead of processing every frame unnecessarily, representative frames are extracted from the video.

### Step 3 — Visual Analysis

Qwen analyzes the sampled frames and proposes whether an anomaly is present.

### Step 4 — Evidence Validation

The Evidence Gate checks whether the prediction is supported by meaningful visual evidence.

### Step 5 — Temporal Verification

Predictions are compared across multiple frames.

### Step 6 — Final Decision

The system produces one of two outcomes:

```text
✅ NORMAL
```

or

```text
🚨 ANOMALY CONFIRMED
```

### Step 7 — Visualization

The result can be displayed through a Gradio dashboard.

---

## 📊 Current Prototype

The current prototype successfully demonstrates:

* Video loading
* Frame extraction
* Representative frame sampling
* Qwen-based visual analysis
* False-positive filtering
* Evidence validation
* Temporal verification
* Final anomaly decision
* Gradio-based visualization

The prototype is designed as a **near-real-time MVP** and can be further optimized for production deployment.

---

## 🔮 Future Improvements

Future versions could include:

* Real-time video stream processing
* Lightweight object detection before VLM analysis
* GPU optimization
* Adaptive frame sampling
* Event tracking across longer video sequences
* Confidence scoring
* Automatic timestamp generation
* Multi-camera monitoring
* Edge-device deployment
* Alert notifications
* Advanced anomaly classes

---

## 🏆 Hackathon Focus

VisionSentinel focuses on an important principle for safety-oriented AI systems:

> **An AI prediction should not automatically become an alert.**

By combining visual evidence with temporal consistency, the system aims to produce **more trustworthy anomaly alerts while reducing false positives**.

---

## 👩‍💻 Built For

**AHC Visual Intelligence Hackathon — Real-Time Video Anomaly Detection**

---

## 📜 License

This project is intended as a hackathon prototype. Add an appropriate open-source license if you plan to publish the repository for public use.
