## **Image Segmentation**

### **1. Object Detection vs. Segmentation**
- **Object Detection**: Identifies and localizes objects using bounding boxes. Outputs: class label + box coordinates.
- **Segmentation**: Classifies each pixel in the image.
  - More precise than detection.
  - Types: **Semantic** and **Instance** segmentation.

### **2. Semantic Segmentation vs. Instance Segmentation**
- **Semantic Segmentation**: Labels each pixel with a class (e.g., all cats as "cat").
- **Instance Segmentation**: Labels each object instance separately (e.g., Cat 1, Cat 2, etc.).

### **3. U-Net Architecture and Working**
- Designed for **biomedical image segmentation**.
- **Symmetric U-shaped architecture** with **skip connections**.
- Consists of:
  - **Encoder** (downsampling): Extracts features.
  - **Decoder** (upsampling): Reconstructs pixel-level predictions.
- **Skip connections** pass spatial information directly from encoder to decoder.

### **4. Encoder and Decoder Architecture**
- **Encoder**:
  - Repeated **Conv -> ReLU -> MaxPool** blocks.
  - Extracts deep features and reduces spatial size.
- **Decoder**:
  - **Upsampling/Transposed Conv** to increase resolution.
  - Combines encoder features via **skip connections** to refine output.

### **5. U-Net vs. FCNs (Fully Convolutional Networks)**
| Feature | U-Net | FCNs |
|--------|------|------|
| Skip Connections | Yes (explicit) | Limited or optional |
| Architecture | Symmetric U-shaped | Encoder-heavy |
| Performance | Better on small datasets | Good for large datasets |
| Use Case | Medical imaging | General segmentation |

### **6. Mask R-CNN Architecture and Limitations**
- **Extension of Faster R-CNN** for instance segmentation.
- Adds a **segmentation mask branch** to the bounding box detection.
- Architecture:
  - Backbone (e.g., ResNet) + RPN + ROIAlign + mask prediction.
- **Limitations**:
  - Heavy and slow.
  - Requires lots of labeled data.
  - Poor performance on overlapping/transparent objects.

### **7. Metrics and Losses for Segmentation**
- **Metrics**:
  - **IoU (Intersection over Union)**
  - **Dice Coefficient**
  - **Pixel Accuracy**
- **Losses**:
  - **Cross-Entropy Loss**
  - **Dice Loss**
  - **Focal Loss** (for class imbalance)

---

## **Siamese Network**

### **1. Basic Architecture and Working**
- Two **identical neural networks** with **shared weights**.
- Input: **pair of images**.
- Output: **Similarity score** based on **distance between embeddings**.

### **2. Applications**
- **Face recognition/verification**
- **Signature verification**
- **One-shot learning**
- **Medical image matching**
- **Document matching**

### **3. Role of Embeddings and Distance Metrics**
- **Embeddings**: Feature vectors that represent the input.
- **Distance Metrics**:
  - **Euclidean Distance**
  - **Cosine Similarity**
  - Used to compare embeddings and infer similarity.

### **4. Loss Functions**
- **Contrastive Loss**:
  - Encourages similar pairs to have low distance, dissimilar to have high.
- **Triplet Loss**:
  - Anchor, positive, negative: Pull positive closer and push negative away.
- **Binary Cross-Entropy**:
  - Used if you treat the similarity as a binary classification problem.
- **Comparison**:
  - **Contrastive** is simpler.
  - **Triplet** gives better control but needs more careful sampling.

### **5. One-Shot Learning**
- Learn from **only one example**.
- Siamese networks are well-suited since they learn **distance/similarity**, not just class.

### **6. Training Strategies**
- Use **pair generation** (positive & negative).
- **Hard negative mining**: Train on difficult examples to improve performance.
- **Data augmentation**: Critical for limited-data problems.
- Can be **pretrained** on larger tasks and **fine-tuned**.
