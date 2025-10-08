# 🕳️ Pothole Detection using YOLOv4

## 📌 Overview

This project focuses on detecting potholes on roads using the **YOLOv4 (You Only Look Once)** object detection model. The goal is to automate the process of identifying and localizing potholes from road images or video feeds, which can help in road maintenance and accident prevention.

The system is built using the **Darknet framework** and trained on a custom dataset containing annotated images of potholes. The trained model can then be used to perform real-time pothole detection and mark them with bounding boxes.

---

## 🎯 Objective

* To develop an automated system capable of detecting potholes using deep learning.
* To enhance road safety and assist municipal authorities in efficient road maintenance.
* To leverage YOLOv4 for real-time, accurate object detection on custom datasets.

---

## ⚙️ Technologies Used

| Component       | Description                                                                  |
| --------------- | ---------------------------------------------------------------------------- |
| **Model**       | YOLOv4 (You Only Look Once v4)                                               |
| **Framework**   | Darknet (Open-source neural network framework)                               |
| **Language**    | Python                                                                       |
| **Environment** | Google Colab / VS Code                                                       |
| **Libraries**   | OpenCV, NumPy, Matplotlib                                                    |
| **Dataset**     | Custom dataset of pothole images (annotated in `.txt` format using LabelImg) |

---

## 📂 Project Structure

```
Pothole-Detection-YOLOv4/
│
├── cfg/                          # YOLOv4 configuration files
├── data/                         # Dataset, obj.names, and obj.data files
├── backup/                       # Trained model weights
├── scripts/                      # Utility scripts for training and testing
├── results/                      # Output images/videos after detection
├── yolov4-custom.cfg             # Custom configuration for training
├── train.txt / test.txt          # Dataset paths
├── requirements.txt              # Dependencies
├── detect.py                     # Detection script
├── README.md                     # Project documentation
└── darknet/                      # Darknet framework folder
```

---

## 🧠 Model Training Steps

### 1️⃣ Prepare the Dataset

* Collect road images containing potholes (at least 500–1000 images recommended).
* Annotate each image using **LabelImg** and save in **YOLO format (.txt)**.
* Split data into `train.txt` and `test.txt`.

### 2️⃣ Configure YOLOv4

* Update `obj.names` with class labels (e.g., `pothole`).
* Edit `obj.data` with paths to dataset and number of classes.
* Modify `yolov4-custom.cfg`:

  * Set `classes=1` (for single class)
  * Adjust `filters=(classes + 5) * 3 = 18` in the convolutional layers before each YOLO layer.
  * Set appropriate batch and subdivisions.

### 3️⃣ Train the Model

Run the following command in Google Colab or terminal:

```bash
!./darknet detector train data/obj.data cfg/yolov4-custom.cfg yolov4.conv.137 -dont_show -map
```

### 4️⃣ Test the Model

After training, use:

```bash
!./darknet detector test data/obj.data cfg/yolov4-custom.cfg backup/yolov4-custom_best.weights data/test.jpg -thresh 0.3
```

The output image with detected potholes will be saved as `predictions.jpg`.

---

## 🧪 Results

* The model successfully detects potholes in various lighting and road conditions.
* Achieved high accuracy after sufficient training iterations.
* Detected potholes are highlighted with bounding boxes in the output.

Example:

```
Pothole detected with confidence: 92%
```

---

## 🚀 Future Enhancements

* Deploy model in real-time on Raspberry Pi or edge devices.
* Integrate with Google Maps API to mark GPS coordinates of detected potholes.
* Extend dataset with more environmental variations.
* Develop a web interface or mobile app for live pothole reporting.

---

## 🧾 References

* YOLOv4 Paper: *Bochkovskiy, Wang, Liao – "YOLOv4: Optimal Speed and Accuracy of Object Detection" (2020)*
* Darknet GitHub: [https://github.com/AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)
* LabelImg Tool: [https://github.com/heartexlabs/labelImg](https://github.com/heartexlabs/labelImg)

---
