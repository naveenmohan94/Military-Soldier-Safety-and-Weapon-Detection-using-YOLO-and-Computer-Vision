# 🛡️ Military Object Detection and Analysis

An AI-driven system designed to detect and classify both military and civilian objects using a custom-trained YOLOv5 model. This solution supports battlefield intelligence, surveillance, and real-time threat assessment through a user-friendly Streamlit interface.

---

## 📌 Project Highlights

* 🎯 **Smart Detection**: Recognizes and localizes 12 unique object classes.
* ⚠️ **Threat Classification**: Real-time differentiation of threats and non-threats.
* 🔊 **Audio Alerts**: Immediate sound alerts for high-risk detections.
* 📊 **Visual Reporting**: Bar and pie charts to summarize detection stats.
* 📥 **Export Features**: Download detection results (CSV, annotated images).

---

## 🗃️ Dataset Overview

Trained on a custom dataset annotated with 12 classes of military and civilian objects.

### 🔍 Object Classes

1. camouflage\_soldier
2. weapon
3. military\_tank
4. military\_truck
5. military\_vehicle
6. civilian
7. soldier
8. civilian\_vehicle
9. military\_artillery
10. trench
11. military\_aircraft
12. military\_warship

### 📊 Class Distribution

| Category           | Class               | Instances |
| ------------------ | ------------------- | --------- |
| Highly Represented | military\_tank      | 20,059    |
|                    | military\_aircraft  | 8,636     |
|                    | soldier             | 7,807     |
|                    | camouflage\_soldier | 5,376     |
| Underrepresented   | trench              | 44        |
|                    | civilian            | 53        |
|                    | civilian\_vehicle   | 586       |

---

## 🧪 Data Preprocessing & Augmentation

* CLAHE applied for contrast enhancement
* All images resized to **640×640**
* Empty and malformed annotation files removed
* Blurriness measured via Laplacian variance
* Brightness levels assessed
* Bounding box size and aspect ratio evaluated
* Co-occurrence and frequency of classes analyzed

---

## 🧠 Model Details

* **Architecture**: YOLOv5m
* **Input Size**: 640×640
* **Batch Size**: 8
* **Epochs**: 3 (demo; recommend more for production)
* **Weights**: Pretrained yolov5m.pt
* **Config File**: `military.yaml`
* **Enhancements**: CLAHE images used
* **Environment**: Google Colab

### 📈 Performance Metrics (Example)

| Metric    | Value |
| --------- | ----- |
| mAP\@0.5  | 0.78  |
| Precision | 0.82  |
| Recall    | 0.76  |

> **Note**: Best results for tanks, weapons, and soldiers. Low performance on trench and civilian due to imbalance.

---

## 🌐 Streamlit Web App

An interactive interface for detection, classification, and reporting.

### 💡 App Features

* 🖼️ **Image Upload**: Users can upload custom images
* 🚀 **Real-Time Detection**: YOLOv5 inference
* ⚠️ **Threat Flagging**: Immediate visual labels
* 🔊 **Audio Alerts**: Triggered if threats detected
* 📊 **Reporting**: Pie/bar charts, detection table
* 📥 **Exports**: CSV + processed image downloads

---

## ⚙️ Setup & Installation (Google Colab)

### ✅ Requirements

* Google Colab (recommended)
* `best.pt` (custom YOLOv5 weights)
* Optional: `military_image.png`

### 📦 Install Libraries

```bash
pip install streamlit pyngrok torch torchvision pillow pydub ffmpeg-python
```

### 🧬 Clone YOLOv5

```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

### 🔊 Generate Audio Alert

```python
from pydub.generators import Sine
sound = Sine(1000).to_audio_segment(duration=1000)
sound.export("/content/alert.mp3", format="mp3")
```

### 🌐 Run Streamlit App

```bash
streamlit run app.py &
npx localtunnel --port 8501
```

---

## 📁 Project Structure

```
Military_Object_Detection/
├── app.py                # Streamlit frontend
├── best.pt               # YOLOv5 model weights
├── alert.mp3             # Audio alert file
├── yolov5/               # YOLOv5 repo
└── runs/                 # Output results
```

---

Feel free to expand training, add more threat rules, or integrate video input for real-time surveillance!
