# Object Tracking with YOLOv8

This project demonstrates how to perform **object tracking** on video data using the YOLOv8 model from [Ultralytics](https://github.com/ultralytics/ultralytics). Two object tracking approaches are implemented:

* **Single Object Tracking**: Tracks the first detected person across frames.
* **Multiple Object Tracking (MOT)**: Tracks multiple persons using ByteTrack tracker.

---

## 🔧 Installation

Run the following command to install the required dependencies:

```bash
!pip install ultralytics
```

Also make sure OpenCV and NumPy are available:

```python
import cv2
import numpy as np
```

---

## 📁 Google Drive Setup

Mount Google Drive to access input videos and save output:

```python
from google.colab import drive
drive.mount('/content/drive')
```

---

## 🎯 Single Object Tracking

* Loads the YOLOv8n model.
* Detects the first person and tracks them based on closest movement.
* Draws the path of the tracked person using red lines.

### Input

`/content/drive/MyDrive/Traking_video/input_video1.mp4`

### Output

`/content/drive/MyDrive/output_video.mp4`

### Highlights

* Tracks **only one person**.
* Uses Euclidean distance to follow the nearest person to the last tracked location.
* Saves the tracking result as a video with a drawn path.

---

## 👥 Multiple Object Tracking (MOT)

* Uses YOLOv8 with `ByteTrack` to detect and assign unique IDs to multiple people.
* Tracks each person’s movement path using distinct colors.

### Input

`/content/drive/MyDrive/Traking_video/input_video1.mp4`

### Output

`/content/drive/MyDrive/Traking_video/output_video.mp4`

### Highlights

* Tracks **multiple persons** simultaneously.
* Draws unique colored paths for each individual.
* Uses `ByteTrack` tracker integrated with YOLOv8.

---

## 📽️ Video Properties Extracted

```python
frame_width = int(cap.get(3))
frame_height = int(cap.get(4))
fps = int(cap.get(5))
```

These are used to define the video writer:

```python
fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter(<output_path>, fourcc, fps, (frame_width, frame_height))
```

---

## 📌 Notes

* The model used: `yolov8n.pt` (YOLOv8 Nano for faster inference).
* All frames are processed using `model(frame)` for detection or `model.track(frame)` for MOT.
* Ensure paths to videos are correct when running on Google Colab.

---
