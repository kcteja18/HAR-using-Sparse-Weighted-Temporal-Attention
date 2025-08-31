# HAR-using-Sparse-Weighted-Temporal-Attention
A B.Tech project by Koppolu Charan Teja (Roll No: 120AD0005) submitted to the Department of Computer Science and Engineering at the IIITDM Kurnool. Guide: Dr. Korra Sathya Babu, Associate Professor, Dept. of CSE, IIITDM Kurnool.

***

## Abstract

Human Activity Recognition (HAR) is a crucial field for enabling machines to understand human actions from sensor data. This project introduces a **Sparse Weighted Temporal Attention Mechanism** to enhance HAR, particularly for data from drone cameras. This technique allows the model to focus on the most important moments in a sequence of actions, which improves the accuracy and efficiency of the recognition process. By integrating this mechanism, the system can better interpret human actions, leading to more precise and reliable results for applications in healthcare, surveillance, and human-computer interaction.

***

## Methodology

The core of this project is a novel approach that integrates a Sparse Weighted Temporal Attention (SWTA) module with a robust backbone network to classify human activities from video frames.

![Methodology Overview](https://i.imgur.com/P5e6B2p.png)
[cite_start]*Figure 3.1: Overview of Methodology [cite: 31]*

The workflow is as follows:
1.  [cite_start]**Temporal Frame Sampling**: Video frames are extracted and divided into segments using a **Temporal Segment Network (TSN)** to capture long-range temporal information efficiently[cite: 229, 243].
2.  **Attention Mechanism**: A **Sparse Weighted Temporal Attention (SWTA)** module is applied. [cite_start]This module calculates optical flow between sparsely sampled frames and uses it to create an attention map, effectively highlighting motion changes[cite: 268, 271, 272]. This map is then fused with the original RGB frames.
3.  [cite_start]**Human Detection**: The **YOLOv8** model is used to detect and crop the human subjects from the frames, isolating them from the background for more focused analysis[cite: 289].
4.  [cite_start]**Feature Extraction**: The processed frames are fed into a backbone network, an **Inception V3** architecture pre-trained on ImageNet, to extract high-level features[cite: 310].
5.  [cite_start]**Classification**: Finally, fully connected layers and a Softmax activation function classify the action into one of the predefined categories[cite: 313, 318, 319].

### Key Components

| Component | Description | Visual Representation |
| :--- | :--- | :--- |
| **Temporal Segment Network (TSN)** | [cite_start]Divides video into segments and sparsely samples frames to model temporal structure[cite: 243, 248]. | [cite_start]![Temporal Segment Network Diagram](https://i.imgur.com/s6Wp7kK.png) <br> *Figure 3.2: Temporal Segment Network [cite: 32]* |
| **SWTA Module** | [cite_start]Fuses optical flow with RGB frames to focus on key temporal information[cite: 268]. | [cite_start]![SWTA Module Diagram](https://i.imgur.com/jM8V83Q.png) <br> *Figure 3.5: Sparse weighted Temporal Attention (SWTA) Module [cite: 35]* |
| **Human Detection (YOLOv8)** | [cite_start]Accurately detects and crops persons in each frame[cite: 289, 290]. | [cite_start]![Human Detection and Cropping](https://i.imgur.com/E9tY50c.png) <br> *Figure 3.9: Human Detection and cropping using YOLOv8 [cite: 39]* |
| **Backbone Network (InceptionV3)**| [cite_start]Extracts intricate features from the processed frames[cite: 310, 311]. | [cite_start]![Inception Network Architecture](https://i.imgur.com/5J3X2qF.png) <br> *Figure 3.10: Overview of Inception network [cite: 329]* |

***

## Datasets

The model was trained and evaluated on two challenging drone-based video datasets.

1.  [cite_start]**Drone Action Dataset**: A total of 13 actions performed by 10 subjects, captured from a drone in hovering and following modes[cite: 163, 175].
    ![Drone Action Dataset Examples](https://i.imgur.com/4z82hKk.png)
    [cite_start]*Figure 2.1: Drone Action Dataset [cite: 69]*

2.  [cite_start]**Okutama Action Dataset**: Features 43 video sequences with 12 action categories, recorded by two drones at varying heights and angles[cite: 182, 183].
    ![Okutama Action Dataset Examples](https://i.imgur.com/B9BwA5K.png)
    [cite_start]*Figure 2.2: Sample frames of Okutam-Action dataset [cite: 69]*

### Dataset Comparison

| Feature | Okutama-Action | Drone-Action |
| :--- | :--- | :--- |
| **Number of actions** | [cite_start]12 [cite: 188] | [cite_start]13 [cite: 188] |
| **Number of subjects**| [cite_start]9 [cite: 188] | [cite_start]10 [cite: 188] |
| **Number of videos** | [cite_start]43 [cite: 188] | [cite_start]220 [cite: 188] |
| **Total duration** | [cite_start]43 min [cite: 188] | [cite_start]44.6 min [cite: 188] |
| **Resolution** | [cite_start]$3840 \times 2160$ [cite: 188] | [cite_start]$1920 \times 1080$ [cite: 188] |
| **Dataset size** | [cite_start]5.3GB [cite: 188] | [cite_start]7.56GB [cite: 188] |
[cite_start]*Source: Figure 2.3: Datasets Info [cite: 189]*

***

## 📊 Results and Performance

[cite_start]The model was trained for 50 epochs with a batch size of 32, using the Adam optimizer and Categorical Crossentropy loss function[cite: 340, 339, 341, 350].

### Training Performance

[cite_start]The model achieved a final **training accuracy of 85.01%** and a **validation accuracy of 87.40%**[cite: 41]. [cite_start]The training loss was 0.6433 and the validation loss was 0.6068[cite: 42].

| Training Accuracy & Loss Plots |
| :---: |
| [cite_start]![Model Training and Validation Accuracy Graph](https://i.imgur.com/U2FfHll.png) <br> *Figure 4.1: Model Accuracy variations [cite: 41]* |
| [cite_start]![Model Training and Validation Loss Graph](https://i.imgur.com/JbW7b4s.png) <br> *Figure 4.2: Model Loss variations [cite: 42]*|

### Test Set Evaluation

[cite_start]On the test set, the model demonstrated strong performance with an **overall accuracy of 87%**[cite: 540, 547].

| Confusion Matrix | Classification Report |
| :---: | :---: |
| [cite_start]![Confusion Matrix for Test Results](https://i.imgur.com/83u6G6U.png) <br> *Figure 4.3: Confusion matrix [cite: 43]* | [cite_start]![Classification Report for Test Results](https://i.imgur.com/97y0uC6.png) <br> *Figure 4.4: Classification report [cite: 44]* |

[cite_start]The classes **'running'** and **'stabbing'** were perfectly classified with a precision and recall of 1.00[cite: 520, 521, 525, 526]. [cite_start]Actions like **'clapping'** (recall 0.46) and **'walking'** (recall 0.58) proved more challenging[cite: 501, 531].

### Prediction Examples

Here are some sample predictions from the model on test videos.

**Drone Action Dataset:**

| Correct Predictions | Incorrect Prediction |
| :---: | :---: |
| [cite_start]![Predicted Kicking, Actual Kicking](https://i.imgur.com/G5rR88h.png) <br> **Predicted: Kicking, Actual: Kicking** [cite: 555] | [cite_start]![Predicted Hitting, Actual Running](https://i.imgur.com/Gk9z05l.png) <br> **Predicted: Hitting, Actual: Running** [cite: 559, 560, 561] |
| [cite_start]![Predicted Punching, Actual Punching](https://i.imgur.com/C7Q2D6B.png) <br> **Predicted: Punching, Actual: Punching** [cite: 556] | [cite_start]![Predicted Walking, Actual Stabbing](https://i.imgur.com/c43j0i8.png) <br> **Predicted: Walking, Actual: Stabbing** [cite: 557] |

**Okutama Action Dataset:**

| Correct Prediction | Incorrect Prediction |
| :---: | :---: |
| [cite_start]![Predicted Walking, Actual Walking](https://i.imgur.com/yvC9sYV.png) <br> **Predicted: Walking, Actual: Walking** [cite: 568] | [cite_start]![Predicted kicking, Actual Walking](https://i.imgur.com/b6b5M6o.png) <br> **Predicted: kicking, Actual: Walking** [cite: 569] |

***

## 🛠️ Libraries and Modules Used

This project relies on several key Python libraries:
-   [cite_start]**TensorFlow** & **Keras**: For building and training the deep learning model[cite: 193, 196].
-   [cite_start]**OpenCV (cv2)**: For video processing, frame extraction, and calculating optical flow[cite: 199, 200].
-   [cite_start]**NumPy**: For efficient numerical operations and array manipulation[cite: 205, 206].
-   [cite_start]**Pandas**: For manipulating and analyzing data[cite: 209].
-   [cite_start]**Matplotlib**: For creating visualizations and plots[cite: 213].
-   [cite_start]**SciPy**: Used to process MATLAB annotation files for the Drone Action dataset[cite: 217, 219].
