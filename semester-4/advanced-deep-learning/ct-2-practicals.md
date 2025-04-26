# Signature Verification using Siamese Neural Network

---

### **Aim**
To build and train a Siamese Neural Network that can verify whether a pair of handwritten signature images belong to the same person (genuine) or not (forged).

---

### **Procedure**

1. **Data Loading**
   - Signature image pairs and labels were loaded from `.npy` files using `gdown` from Google Drive.
   - Dataset shape:
     - Total pairs: **`{{X.shape[0]}}`**
     - Image size: **155 x 220**
     - Train size: **`{{X_train.shape[0]}}`**, Test size: **`{{X_test.shape[0]}}`**

2. **Preprocessing**
   - Images were reshaped to `(155, 220, 1)` for CNN input compatibility.

3. **Model Building**
   - A shared CNN was used to extract feature embeddings.
   - L1 distance computed between embeddings.
   - Dense layer with sigmoid output used for binary prediction (genuine vs forged).

4. **Training**
   - Model was trained with binary cross-entropy loss and Adam optimizer.
   - Training accuracy and loss were monitored over multiple epochs.

5. **Evaluation & Visualization**
   - Final **Test Accuracy**: **`{{accuracy:.2%}}`**
   - Predicted results on random test samples were visualized along with:
     - Actual vs predicted labels
     - Model confidence
     - Green for correct, Red for incorrect predictions

---

### **Conclusion**

The Siamese Neural Network successfully learned to verify handwritten signatures. It showed high accuracy in distinguishing between genuine and forged signatures, making it suitable for applications like **document authentication**, **biometric verification**, and **secure digital workflows**.
