# kannada-handwritten-digits-recognition
Real-time Kannada Handwritten Digit Recognition using a custom CNN and OpenCV. Features a manually collected dataset and live webcam inference

![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)

A Deep Learning project capable of recognizing real-world handwritten Kannada numerals (0-9) in real-time. This project uses a custom Convolutional Neural Network (CNN) trained on a manually collected dataset and includes a live webcam interface for instant inference.



## Key Features
* *Custom CNN Architecture:* Built from scratch using TensorFlow/Keras with Dropout and MaxPooling layers to prevent overfitting.
* *Real-Time Detection:* Live webcam integration using OpenCV to detect and classify digits on the fly.
* *Smart Preprocessing:* Implements dynamic thresholding to clean noisy webcam feeds and handle varying lighting conditions.
* *Robust Data Augmentation:* Uses rotation, zoom, and shift augmentation to improve model generalization on small datasets.



##  Tech Stack & Versions
This project relies on specific library versions to ensure stability (avoiding NumPy/OpenCV version conflicts).

 Library: Version 
 *Python*: 3.x 
 *TensorFlow*: Latest 
 *NumPy*: 1.26.4 
 *OpenCV*: 4.9.0.80
 *Matplotlib*: Latest
 *Scikit-Learn*: Latest



##  Model Performance

### Training Results
The model was trained over *30-50 epochs* with Early Stopping.
* *Training Accuracy:* ~88%
* *Validation Accuracy:* ~82%

### Loss & Accuracy Graphs
(The model demonstrates healthy learning curves with no significant overfitting after tuning)

![Accuracy Graph]

![WhatsApp Image 2025-11-23 at 7 22 13 PM](https://github.com/user-attachments/assets/79cbe49e-36a2-494c-9890-f4f0b5bf0118)




##  Challenges & Solutions (The Dev Journey)

Building this project involved overcoming several significant technical hurdles. Here is how they were solved:

### 1: Overfitting (High Variance)
* *The Issue:* The model initially achieved ~99% training accuracy but only ~75% validation accuracy. The Loss graph showed a distinct "U-turn," indicating the model was memorizing the training data instead of learning features, and confidence level was 45%.
* *The Diagnosis:* The model was too complex for the dataset size, and lacked regularization.
* ![WhatsApp Image 2025-11-23 at 7 36 19 PM](https://github.com/user-attachments/assets/c3445d1b-f2c2-4c21-b92e-dac4cea42068)


### 2: Underfitting (High Bias)
* *The Attempt:* We introduced heavy Dropout(0.5) layers and reduced the number of filters significantly, condifence level was 12%
* *The Result:* Both training and validation accuracy stalled at around 60%. The model became "too dumb" to learn the complex curves of Kannada digits.
* ![WhatsApp Image 2025-11-23 at 7 38 34 PM](https://github.com/user-attachments/assets/a015f24c-3a55-4d3f-a6b5-a382533d4cc8)


### 3: The "Goldilocks" Balance (Final Model)
* *The Solution:* 1. Tuned Dropout rates to *0.2* (gentle regularization).
    2. Implemented *EarlyStopping* to prevent over-training.
    3. Fixed a critical *Double-Normalization bug* in the preprocessing pipeline that was feeding black images to the model.
* *Result:* Achieved a stable *88% Accuracy* with converging Loss curves.
  
### 4. The "Double Normalization" Bug
* *Problem:* During testing, the model predicted the same number (e.g., "2") for every single image with low confidence.
* *Root Cause:* The images were being divided by 255.0 in the preprocessing script, but the model already included a Rescaling layer. This turned all inputs into pitch-black images.
* *Solution:* Removed the external normalization step, allowing the model layer to handle the scaling internally.

### 5. DLL Load Failed (Version Conflicts)
* *Problem:* We encountered persistent ImportError: DLL load failed messages when importing OpenCV and NumPy.
* *Root Cause:* A version mismatch between the latest NumPy (2.0+) and the standard OpenCV binary wheels on Windows.
* *Solution:* Performed a clean wipe of the environment and pinned *NumPy to 1.26.4* and *OpenCV to <4.10*.

### 6. Webcam "Mode Collapse"
* *Problem:* The live webcam feed had low confidence (~60%) and struggled with shadows.
* *Solution:* Implemented *Binary Thresholding* (cv2.threshold) in the OpenCV loop. This forces the image to be strictly Black & White before the model sees it, removing background noise and boosting confidence to *99%*.


##  Dataset
The dataset consists of real-world images of Kannada digits collected manually.
*[https://www.kaggle.com/datasets/hsbharath/kannada-handwritten-digit-dataset]*

## contributor's
* **Bharath HS**
* **Gagan  M**
