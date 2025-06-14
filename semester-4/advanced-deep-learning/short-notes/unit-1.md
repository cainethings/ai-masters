# Unit 1

## **Review of Deep Learning Algorithm**

* **CNNs**: Backbone of object detection, use filters to extract spatial features.
* **Backpropagation**: Learns weights through error minimization.
* **Activation Functions**: ReLU (non-linearity), Softmax (classification).
* **Overfitting Solutions**: Dropout, Data Augmentation, Batch Norm.


## 📷 **Introduction to Object Detection**

* **Goal**: Find *what* object is *where* in an image.
* **Output**: Class labels + bounding box coordinates (x, y, w, h).
* Combines **classification + localization**.


## 📍 **Object Localization**

* Predict **single object’s** location in an image.
* Output: **One class + one bounding box**.
* Used when the image has only *one main object*.


## 🧠 **Image Classifier as Object Detector**

* Slide a **window** across image → run classifier on each window.
* Limitations: **Slow**, redundant computation, not scale-invariant.
* Used in early methods like **R-CNN**.


## 📏 **Object Detection as Regressor Problem**

* CNN directly **regresses** to bounding box coordinates.
* Predict: `[x_center, y_center, width, height]` + class probabilities.
* Used in **YOLO**, **SSD**, etc.


## 📊 **Metrics for Object Detection**

* Evaluate **how well** predictions match ground truth.
* Combines classification & localization quality.
* Common metrics: **IoU**, **Precision**, **Recall**, **mAP**.


## 🔲 **Intersection Over Union (IoU)**

* **IoU = Area of Overlap / Area of Union**
* Measures how much predicted box overlaps with actual box.
* **Threshold (e.g., 0.5)** used to determine if detection is correct.


## ⚖️ **Dice Coefficient**

* **Dice = 2 \* Overlap / (Pred + Ground Truth Areas)**
* Similar to IoU, but more **sensitive to small objects**.
* Often used in **medical imaging**.


## 🎯 **Precision and Recall Curve + mAP**

* **Precision** = TP / (TP + FP): Accuracy of positive predictions.
* **Recall** = TP / (TP + FN): Coverage of actual positives.
* **PR Curve**: Trade-off between precision & recall.
* **mAP (mean Average Precision)**: Average precision across classes and IoU thresholds.
