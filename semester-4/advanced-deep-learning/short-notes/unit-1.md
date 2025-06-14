# Unit 1

### ✅ **Review of Deep Learning Algorithms**

* **CNN (Convolutional Neural Network)**: Best for images; uses convolution layers to capture spatial hierarchies (edges → textures → shapes → objects).
* **Pooling layers** (Max/Average): Reduce dimensions while retaining important features. Helps reduce overfitting and computation.
* **Activation Functions**:

  * **ReLU**: Common for hidden layers; makes model non-linear.
  * **Softmax**: Used in final classification layer to get class probabilities.
* **Backpropagation**: Propagates error backward to update weights using **gradient descent**.
* **Optimizers**: SGD, Adam, RMSProp used to speed up convergence.
* **Overfitting Handling**:

  * **Dropout**: Randomly drops nodes during training.
  * **Batch Normalization**: Normalizes activations to stabilize training.
  * **Data Augmentation**: Flips, crops, rotates images to simulate variety.

---

### 📷 **Introduction to Object Detection**

* **What & Where**: Predict both **object classes** and their **locations** in images.
* Input: Full image → Output: List of bounding boxes + labels + confidence scores.
* Supports **multiple objects** in the same image.
* **Applications**: Face detection, vehicle tracking, person detection, security surveillance.
* Core models:

  * **Two-stage**: Region proposals first (e.g., R-CNN, Faster R-CNN).
  * **One-stage**: Direct predictions (e.g., YOLO, SSD).

---

### 📍 **Object Localization**

* Task: **Detect only one object** in an image.
* Output: 4 values (x, y, width, height) + label.
* **Combines classification and bounding box regression**.
* Example: An image with a single dog → predict "dog" and box.
* Simpler than object detection (which handles **multiple** objects).

---

### 🧠 **Image Classifier as Object Detector (Sliding Window)**

* Turn a classifier into a detector using a **sliding window** over the image.
* At each window, apply the classifier (e.g., dog? cat?).
* Use at **different scales** to detect small and large objects.
* **Drawbacks**:

  * Computationally slow & inefficient.
  * High redundancy: overlapping regions tested repeatedly.
  * No shared computation → solved later by CNN-based detection models.

---

### 📏 **Object Detection as Regressor Problem**

* Reframe detection as a **regression problem**:

  * Predict box coordinates + object class in one go.
* Used in **YOLO** (divides image into grid cells) and **SSD** (uses anchor boxes).
* Single forward pass → extremely fast (**real-time detection**).
* Challenges:

  * **Localization error**: small offset in boxes.
  * **Class imbalance**: many background vs. few objects.
* Solution: Use **anchor boxes**, **focal loss**, **NMS (Non-Max Suppression)**.

---

### 📊 **Metrics for Object Detection**

* Evaluates both **classification** (correct object label) and **localization** (correct bounding box).
* Key metrics:

  * **IoU (Intersection over Union)**: Measures overlap.
  * **Precision**: Accuracy of positive predictions.
  * **Recall**: Coverage of actual objects.
  * **mAP**: Combines all and gives one score.
* Also useful:

  * **Confusion matrix** (class-wise errors).
  * **F1-score** (harmonic mean of precision and recall).

---

### 🔲 **Intersection Over Union (IoU)**

* Formula:
  `IoU = Area of Overlap / Area of Union`
* **Threshold (e.g., IoU > 0.5)** used to decide if detection is correct (True Positive).
* Values:

  * IoU = 1 → perfect overlap.
  * IoU = 0 → no overlap.
* Crucial in model evaluation (used in mAP and PR curve).

---

### ⚖️ **Dice Coefficient**

* Formula:
  `Dice = 2 * |A ∩ B| / (|A| + |B|)`
* Very similar to IoU but more **sensitive to class imbalance** and **small objects**.
* Used often in **semantic segmentation** and **medical imaging**.
* Value ranges from 0 (no match) to 1 (perfect match).
* Helps when evaluating masks or region-based predictions (not just boxes).

---

### 🎯 **Precision-Recall Curve & Mean Average Precision (mAP)**

* **Precision** = TP / (TP + FP): Are the detected boxes correct?
* **Recall** = TP / (TP + FN): Did the model find all objects?
* **PR Curve**: Plots Precision vs. Recall at different confidence thresholds.
* **AP (Average Precision)**:

  * Area under the PR curve for one class.
  * Measures both precision and recall performance.
* **mAP (mean AP)**:

  * Average of AP across **all classes** and sometimes **IoU thresholds** (like COCO uses mAP@\[0.5:0.95]).
  * **Most widely used detection metric.**

---

Let me know if you'd like this in a PDF/print-friendly format, visual infographic, or in Tamil as well for easier memorization.
