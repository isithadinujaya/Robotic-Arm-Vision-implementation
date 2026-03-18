# 🍬 Candy YOLOv7 - Pick & Place Robot Vision System

Real-time candy detection using YOLOv7 trained on a custom candy dataset.
Part of a 6-DOF robotic arm vision system.

---

## 📦 Detected Classes

| ID | Class            |
|----|------------------|
| 0  | MMs_peanut       |
| 1  | MMs_regular      |
| 2  | airheads         |
| 3  | gummy_worms      |
| 4  | milky_way        |
| 5  | nerds            |
| 6  | skittles         |
| 7  | snickers         |
| 8  | starbust         |
| 9  | three_musketeers |
| 10 | twizzlers        |

---

## ⚙️ Requirements

- Python 3.10+
- torch
- torchvision
- opencv-python
- numpy
- Pillow

---

## 🚀 Setup & Run

### Step 1 — Clone YOLOv7

    git clone https://github.com/WongKinYiu/yolov7

### Step 2 — Install dependencies

    pip install torch torchvision
    pip install opencv-python numpy Pillow
    pip install -r yolov7/requirements.txt

### Step 3 — Download weights

Download best.pt from this repo and place it in the root folder.

Your folder structure should look like this:

    candy_robot/
    ├── yolov7/
    ├── best.pt
    └── README.md

### Step 4 — Patch YOLOv7 for PyTorch 2.6+

Required if you have PyTorch 2.6 or newer.

    python -c "
    filepath = 'yolov7/models/experimental.py'
    with open(filepath, 'r') as f:
        content = f.read()
    content = content.replace(
        'torch.load(w, map_location=map_location)',
        'torch.load(w, map_location=map_location, weights_only=False)'
    )
    with open(filepath, 'w') as f:
        f.write(content)
    print('Patched!')
    "

### Step 5 — Run on webcam

    python yolov7/detect.py --weights best.pt --source 0 --conf-thres 0.25 --img-size 640 --view-img

### Step 6 — Run on image or video

    # On an image
    python yolov7/detect.py --weights best.pt --source image.jpg --view-img

    # On a video
    python yolov7/detect.py --weights best.pt --source video.mp4 --view-img

### Step 7 — Stop detection

Press Q on the webcam window
OR press Ctrl+C in Command Prompt

---

## 🎯 Detection Parameters

| Parameter      | Default | Description                            |
|----------------|---------|----------------------------------------|
| --conf-thres   | 0.25    | Confidence threshold (higher = stricter)|
| --iou-thres    | 0.45    | NMS IoU threshold                      |
| --img-size     | 640     | Input image size                       |
| --source       | 0       | 0 = webcam, or path to image/video     |

---

## 🏋️ Training Details

Training was done on Kaggle using free GPU Tesla T4.

| Setting    | Value                              |
|------------|------------------------------------|
| Dataset    | Custom candy (~200 images + GAN)   |
| Epochs     | 100                                |
| Batch size | 16                                 |
| Image size | 640x640                            |
| Base model | YOLOv7 pretrained on COCO          |
| Classes    | 11                                 |

---

## 📁 Files

| File      | Description           |
|-----------|-----------------------|
| best.pt   | Trained YOLOv7 weights|
| README.md | This file             |

---

## 🔧 Part Of

This vision system is part of a larger 6-DOF robotic arm pick and place system that includes:

- YOLOv7 object detection
- GAN data augmentation
- Camera calibration
- Coordinate transformation (pixel to mm)
- Inverse kinematics (mm to joint angles)
- Arduino stepper motor control

---

## 📚 References

- YOLOv7 by WongKinYiu: https://github.com/WongKinYiu/yolov7
- Vision-Based Pick and Place Control System for Industrial Robots
  Using an Eye-in-Hand Camera, IEEE Access 2025
  https://doi.org/10.1109/ACCESS.2025.3536496
