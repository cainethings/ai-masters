# 🎯 **Siamese Networks – Detailed Notes**

---

## 📌 1. **Basic Architecture and Working of Siamese Networks**

### ➤ **Definition**:
A **Siamese Network** is a neural network architecture that uses **two (or more) identical subnetworks** (with shared weights and parameters) to compare two inputs by learning a **similarity function**.

### ➤ **Key Components**:
- **Twin networks**: Two identical networks with **shared weights**.
- **Embedding layer**: Outputs vector representations (features) of each input.
- **Distance layer**: Measures similarity between embeddings using a **distance function** (e.g., Euclidean, Cosine).
- **Loss function**: Learns to **minimize distance** for similar pairs and **maximize** for dissimilar pairs.

### ➤ **Working**:
1. Inputs: A **pair of data samples** (e.g., two face images).
2. Each input is passed through the **same network** to get their feature embeddings.
3. A **distance metric** is applied to the embeddings to get a similarity score.
4. Loss is computed and used to update the network to distinguish between similar/dissimilar pairs.

---

## 📌 2. **Applications in Different Domains**

| Domain              | Application |
|---------------------|-------------|
| **Computer Vision** | Face verification, Signature verification, Object similarity |
| **Natural Language Processing** | Sentence similarity, Paraphrase detection |
| **Healthcare** | Medical image retrieval, Patient record matching |
| **Biometrics** | Iris, fingerprint, and voice verification |
| **One-shot/Few-shot Learning** | Classify with very few examples |
| **Recommendation Systems** | Find similar items/users |

---

## 📌 3. **Role of Embeddings and Distance Metrics**

### ✅ **Embeddings**:
- Learned **feature vectors** that capture the essence of input data.
- Ideally, **similar inputs have closer embeddings**, dissimilar ones are far apart.

### ✅ **Distance Metrics**:
Used to compute similarity between embeddings.
![image](https://github.com/user-attachments/assets/355f259a-dc7b-46c8-9a9c-3e52a7edf799)


---

## 📌 4. **Different Loss Functions in Siamese Networks**

### ➤ **1. Contrastive Loss**
- Works on **pairs** of samples.
- Minimizes the distance between similar pairs and maximizes for dissimilar.
- **Formula**:
![image](https://github.com/user-attachments/assets/bab6465a-467c-4f48-9767-5e8f54233be4)


### ➤ **2. Triplet Loss**
- Uses **anchor (A), positive (P), negative (N)**.
- Pulls **A and P** close, pushes **A and N** apart.
- **Formula**:
![image](https://github.com/user-attachments/assets/60f06cec-189f-4ab5-aa0a-43932959053b)


### ➤ **3. Binary Cross-Entropy Loss (when used with similarity scores)**
- Treats similarity prediction as a binary classification task.
- Common in **pre-sigmoid output** similarity scoring.

### 📊 **Comparison Table**:

| Loss Function | Input Type | Strength | Weakness |
|---------------|------------|----------|----------|
| **Contrastive Loss** | Pairs | Simple and intuitive | Sensitive to choice of margin |
| **Triplet Loss** | Triplets (A, P, N) | Stronger control on distances | Needs hard-negative mining |
| **BCE** | Pairs + similarity score | Easy integration in classification pipeline | Doesn't explicitly separate positive/negative pairs in embedding space |

---

## 📌 5. **One-Shot Learning**

### ✅ **Definition**:
Learning to recognize **a new class from a single example**.

### ✅ **Siamese Role**:
- Learns a **general similarity function**, not dependent on the number of classes.
- During inference, compare new input with the one-shot sample from each class.
- Pick the one with **minimum distance**.

### ✅ **Example**:
- Given one photo of a person, recognize them among many unseen individuals by comparing similarities.

---

## 📌 6. **Training Strategies for Siamese Network**

### 🧠 **Data Preparation**:
- Create **positive pairs** (same class) and **negative pairs** (different class).
- Use **balanced** batches of positives and negatives.

### 🔍 **Hard Negative Mining**:
- Focus training on **most difficult negative pairs** that are close in the embedding space.
- Improves convergence and performance.

### 🔁 **Batch Construction Tips**:
- **Few-shot task simulation**: Construct batches like test-time few-shot classification.
- **Augmentation**: Enhance generalization, especially for one-shot tasks.

### ⚙️ **Regularization & Transfer Learning**:
- Use pretrained encoders (e.g., ResNet, VGG) to extract embeddings.
- Fine-tune on your dataset using contrastive/triplet loss.

---

## 🎓 Summary

| Concept | Key Idea |
|--------|----------|
| Siamese Network | Compares pairs using shared-weights networks |
| Embedding | Vector that captures input features |
| Distance Metrics | Measure similarity between embeddings |
| Loss Functions | Contrastive, Triplet, or BCE for training |
| One-shot Learning | Classify from a single example |
| Training Strategy | Pair/triplet generation, hard mining, transfer learning |
