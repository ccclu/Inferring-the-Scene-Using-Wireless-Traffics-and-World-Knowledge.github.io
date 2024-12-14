---
layout: default
title: [Inferring the Scene Using Wireless Traffic and World Knowledge Final Report]
permalink: /report/
---
[Project Website](https://ccclu.github.io/Inferring-the-Scene-Using-Wireless-Traffics-and-World-Knowledge.github.io/)


# Table of Contents
* [Abstract](#abstract)
* [Introduction](#introduction)
* [Related Work](#related-work)
* [Technical Approach](#technical-approach)
* [Evaluation and Results](#evaluation-and-results)
* [Discussion and Conclusions](#discussion-and-conclusions)
* [References](#references)

# Abstract
With the rise of smart home IoT devices and low-cost wireless sensors, privacy leakage has become a significant concern. In this project, we aim to design an attack methodology that can infer human movement within a specific room by analyzing the wireless traffic from camera sensors combined with world knowledge, thereby demonstrating the serious privacy threats these wireless sensors pose to users.

# Introduction

## 1. Motivation & Objective

With the rise of smart home IoT devices and low-cost wireless sensors, privacy leakage has become a significant concern. In this project, we aim to design an attack methodology that can infer human movement within a specific room by analyzing the wireless traffic from camera sensors combined with world knowledge, thereby demonstrating the serious privacy threats these wireless sensors pose to users.

## 2. State of the Art & Its Limitations

In order to figure out the risk of privacy leakage in IoT devices, there are many essays try to imitate the technological means that attackers can use to obtain the user information.
### 2.1 RF-based Localization and Tracking
In a Wi-Fi environment, it is possible to achieve coarse-grained localization of signal sources using RF receiving devices, either by actively sensing the location of entities in the area with signal transmitters or by passively sniffing RF signals to infer the position of objects. However, this kind of research can not be used in analyzing the user behavior.
### 2.2 Wireless Signal-based Human Activity Recognition
WiFi received signal strength indicator (RSSI) and Channel State Information(CSI)
has been widely used in human activity recognition combined with machine learning models. But these approaches may require an extra device to capture RSSI or CSI signals and they are trained based on a specific environment. 
### 2.3 User Behavior Analysis in IoT Devices
Some researchers access sensor data, such as app usage history or movement patterns, to analyze user behavior. However, these methods are limited because attackers cannot obtain information from encoded data. As a result, other researchers have attempted to analyze user behavior from encrypted traffic in smart home scenarios. They use a set of simple sensors, whose patterns are identified, and combine them to infer user activity. However, higher-level sensors, such as cameras, are also commonly used in users’ homes, which may offer more accurate insights.

## 3. Novelty & Rationale
### 3.1 Wi-Fi Packet-Based Approach
In our project, our method is based on how the transmission of Wi-Fi packets changes in response to the images captured by the camera sensor, which simplifies the detection process. Compared to RSSI- and CSI-based methods, detecting Wi-Fi packets requires no additional receiver other than a computer to capture the Wi-Fi traffic. According to the 802.11 protocol, we can filter packets transmitting video information, allowing us to analyze specific characteristics such as packet length and transmission frequency.


### 3.2 H.264 Camera Transmission Protocol
We use a camera as our detection sensor because it is the most commonly used sensor in cases of privacy concerns, and it exhibits a predictable pattern when transmitting data. H.264 is a widely used video compression standard that reduces file size while maintaining high video quality through techniques like motion compensation and transformation coding. As a result, the transmission rate varies depending on the video type, including static and dynamic scenarios.


### 3.3 No Wi-Fi Access Required
In a real-world scenario, an attacker cannot be guaranteed Wi-Fi access. Therefore, our project will test our method using an encrypted Wi-Fi network. We will use a laptop as a sniffer to capture Wi-Fi traffic transmitted by the camera to the router.


### 3.4 Leveraging World Knowledge
The differences in packets between different scenarios can be very subtle, so leveraging the world knowledge embedded in large language models can be a rational choice.



## 4. Potential Impact

This project captures traffic packets between cameras and routers to simulate user privacy leakage. It highlights the potential risks associated with current IoT devices and could support future efforts by manufacturers and researchers to develop stronger privacy protection technologies.
Data collected from cameras in this project can be combined with data from other sensors. Using neural networks and similar methods, this approach enables more detailed insights into user behaviors.



## 5. Challenges

The main challenges lie in identifying the correlation between changing scenarios and the variation in Wi-Fi packet characteristics. According to the H.264 protocol, the camera transmits an I-frame as the keyframe, followed by several P-frames and B-frames.
I-frames contain complete image data.\
A P-frame only includes data about changes from the previous I-frame or P-frame. It uses motion compensation to predict content based on the preceding frame. P-frames are smaller than I-frames because they only store the differences (or residuals) between frames.\
A B-frame is more complex, using both previous and future frames (either I or P) to predict its content. It leverages both past and future frame information to compress video data more efficiently. B-frames are typically smaller than both I- and P-frames.\
The camera automatically adjusts the ratio between I-frames and PB-frames to maintain a balance between high compression and video quality. Therefore, it is crucial for us to identify the signal when there is an abrupt change in video content or when an object is in constant motion.\
Although we know the camera uses H.264, the compression process is encrypted, making it act like a black box, preventing us from determining the exact compression algorithm or recovering the original data. Therefore, we must rely on extracting information and discover the transmission pattern from the characteristics of the Wi-Fi packets.




## 6. Requirements for Success
### 6.1 Verifying Changes in Traffic Package I/O Flow During Motion Transitions
We aim to confirm that sudden motion changes in user behavior result in alterations to the I/O flow patterns of traffic packages. This includes identifying transitions such as:
* Shifting from a static state to an active state;
* Moving from slow to fast-paced activities;
* Transitioning from small-scale motions (e.g., hand gestures) to large-scale movements (e.g., walking).
By analyzing the I/O flow patterns of traffic packages, we can further validate whether motion changes correspond to variations in network traffic characteristics, thereby enhancing the model's understanding and classification capabilities for multi-modal data.

### 6.2 The intensity of the movement: Velocity
### 6.2 Motion Intensity: Speed  

After confirming changes in the traffic flow graph, we need to utilize the model to conduct an in-depth analysis of the updated motion information, focusing primarily on movement speed. We adopt a classic four-class classification task, categorizing different motion states based on speed into static, slight movement, movement, and intense movement.  
This approach enables the model to more accurately capture changes in speed following a motion state transition, such as moving from slow to fast or transitioning from a static state to an active state. This detailed classification and analysis provide a more precise understanding of user behavior patterns and state changes, offering robust support for future intelligent applications.  


## 7. Metrics of Success

To evaluate the model's performance, we will employ traditional machine learning metrics, focusing on four key aspects: accuracy, precision, recall, and confidence.
* ***Accuracy***: This metric reflects the overall effectiveness of the model by measuring the proportion of correct predictions out of all predictions made. High accuracy indicates that the model consistently makes correct classifications, providing a reliable overview of its general performance across the dataset.
* ***Precision***: Precision assesses the model’s ability to correctly identify positive instances among the instances it has classified as positive. It is especially crucial in scenarios where false positives (incorrectly labeling an instance as positive) have significant consequences. A high precision score demonstrates that the model is effective at minimizing false positives.
* ***Recall***: Also known as sensitivity or true positive rate, recall measures the model’s capacity to identify all relevant instances within the dataset. It evaluates the proportion of actual positives that the model successfully detects. High recall is essential when it is critical to capture all positive cases, as it reduces the risk of missing any relevant instance.
* ***F1 Score***:The F1 score is the harmonic mean of precision and recall, providing a balanced evaluation of the model's performance when both false positives and false negatives are equally important. It is particularly useful in scenarios with imbalanced datasets, where one class significantly outweighs others. A high F1 score indicates that the model achieves a good balance between precision and recall, making it effective in handling complex classification tasks where both metrics are critical.
  
By systematically evaluating the model using these metrics, we can gain a comprehensive understanding of its strengths and areas for improvement, ensuring that it meets the necessary performance standards for accurate, dependable predictions.


## 8. Execution Plan

***1.*** Identify the correlation between traffic packet flow and the target’s movement, confirming the differences in packet flow patterns across various movement modes.\
***2.*** Extract IPB-related information from the traffic flow data and analyze the relationship between the target’s movements and the IPB data.\
***3.*** Train a large language model (LLM) to take traffic flow data over a specific time period as input and output the transition times between different movement modes of the target, along with detailed movement information for each mode.

# Related Work

### a. Papers
Some works[2] and [3] use encrypted trafffc to analyze user behavior in smart home scenarios. And the work[1] identify a new end-to-end attack surface using IoTBeholder, a system that performs device localization, classiffcation, and user activity identiffcation, which can predict the user behavior by generating a branch of sensors’ information from traffic package.

### b. Datasets
The process of collecting data from videos to traffic packages is highly customized, making existing public datasets insufficient for our needs. Therefore, we must manually collect the data. This process involves multiple tasks, including designing experimental scenarios, configuring collection equipment, and synchronizing video data with traffic data.
During data collection, we first use video recording devices to capture different motion states, while simultaneously using network packet capture tools to record traffic packages associated with these movements. Ensuring precise timestamp alignment is critical, as it allows us to correlate motion information from the videos with network characteristics from the traffic packages in subsequent analyses. Additionally, we design specific experimental setups to cover various motion states (e.g., static, slight movement, movement, and intense movement), ensuring that the data is representative and diverse.
This custom-collected dataset provides strong support for our research, enabling us to better reflect user behavior characteristics in real-world scenarios. Although manual data collection requires significant time and effort, the resulting high-quality and highly targeted data form a solid foundation for model training and validation, ensuring the reliability and applicability of our experimental results.

### c. Software

* **Wireshark[4]**\: Analyze captured traffic packages and extract key features (e.g., timestamps, data length, etc.).
* **Macbook wifi sniffer[5]**\: Capture wireless network traffic to provide data for analysis.
* **Pytorch**: Build, train, and optimize classification models to accurately classify and analyze traffic features and motion states.

# Technical Approach

## 1. Transmission Pattern Verification

### Goal
Use traffic info from sensors to indicate some of human activities.\
If FOSCAM camera can infer the number of people in a single room.

### Steps

1. Identify the connection between packets traffic for camera and human motion
   ![image](https://github.com/user-attachments/assets/1198b501-2a46-45af-a3b0-5a7d8f57b7e6)
  Test for total 40s swithcing between static and move for every 10s.
2. Identify the FOSCAM camera use IPB method(H.264) to send messages
   R4 Manuals: https://www.foscam.com/Uploads/usermanual/2020-05-29/User%20Manual%20for%20R2%20R4%20User%20Manual%20V2.5_English.pdf
   ![image](https://github.com/user-attachments/assets/a76f29a3-2201-4104-aa8c-b9351a8fe09e)
   ![image](https://github.com/user-attachments/assets/fb24b5d0-c716-4e6e-a067-4bae05302b61)
3. Clearify how FOSCAM transport H.264 in traffic package.
4. Find what kind of info from FOSCAM can be used to infer the number of people in the room. Begin it in a small sofa and two working people.


### Prior Knowledge
#### 802.11b
1. https://www.cnblogs.com/rougungun/p/14340489.html

#### H.264 IPB Frames
1. I frames(Intra-coded picture) hold complete image information
2. P frames(Predicted picture) only contain changes in the image from previous frames
3. B frames(Bi-directionally predicted pictures) can construct the image from wither direction using either changes from the I or P frames before them, changes from I and P frames after them, or interpolation between the I/P frames before and after them.

#### Test Result
1. keep static for first 20s, then moving object for 20s, without motion detection
   <img width="1678" alt="image" src="https://github.com/user-attachments/assets/a19e45c2-c7a9-4787-879b-d80f5f6d4b10">
2. keep static for first 20s, then moving object for 20s, with motion detection
<img width="1678" alt="image" src="https://github.com/user-attachments/assets/6ce04627-a3f7-4d68-b56a-3dbd7b4a21db">
3. remain silent for 20s, sending control signal for 20s
    <img width="1678" alt="image" src="https://github.com/user-attachments/assets/13899a1c-eb1c-46ad-ab2c-bcd4cc1a66f0">
    
### Conclusion 
There is a significant difference in the transmission patterns across various scenarios captured by the camera sensor, which confirms that using Wi-Fi traffic to infer the scene is a valid approach.


## 2. Dataset Collection
There is no public dataset for our project, thus, we created our own dataset.
The dataset consists of two primary components:

1.Simulation of human living environment
Includes:
* The dataset includes 5 distinct background settings, representing various indoor environments
* It features 5 different figures, simulating a diverse range of individuals
* Each figure performs 4 movement states: static, slightly move, move, and intensive move
  
2.Captured Surveillance camera corresponding  Wi-Fi packets.

A total of 100 samples. Each with 40 seconds.\
This dataset offers a robust foundation for studying the relationship between human activities, environments, and Wi-Fi signal patterns.



We simulated a real living environment by playing a simulated video on a screen, with the camera positioned to face the screen. At the same time, we used the camera’s software to capture its live stream and employed a laptop to capture the Wi-Fi packets.

**SIMULATION CODE** can be found at: [Simulation Code](https://drive.google.com/file/d/15o04rU0c32uxdAb3nhUy2VRNA9IiGjgN/view?usp=share_link)

**DATASET** can be found at: [Dataset Link](https://drive.google.com/drive/folders/1Pzd6_ZqU6EvLfg4jY3ojDCq4nHZRYo3U?usp=share_link)

<img width="1289" alt="image" src="https://github.com/user-attachments/assets/ec855e8a-6425-4ac6-a364-d3d452efc4c5">
<p align="center">Data Collection Scenario</p>

### Four states of movement captured by camara:
<video src="https://github.com/user-attachments/assets/c2c94872-3491-4c22-9bd7-c4550e55b351" controls width="900">
  Your browser does not support the video tag.
</video>
<p align="center">Static</p>


<video src="https://github.com/user-attachments/assets/b7c5c723-7759-4c50-8483-9b4a90828ea2" controls width="900">
  Your browser does not support the video tag.
</video>
<p align="center">Slightly Move</p>

<video src="https://github.com/user-attachments/assets/03fc8dc3-e5eb-469c-9d34-68d492397d48" controls width="900">
  Your browser does not support the video tag.
</video>
<p align="center">Move</p>


<video src="https://github.com/user-attachments/assets/cd31f717-b8ad-4133-bff8-fc1e02554cb7" controls width="900">
  Your browser does not support the video tag.
</video>
<p align="center">Intensive Move</p>

## 3. Feature Extraction
Extracted Features from Samples:
1. Packet Length:
* When encoding video with H.264, I-frames will produce larger packets because they encode complete frames.
* P-frames and B-frames, on the other hand, typically result in smaller packets due to their compression of differences between frames.
* This means that in scenes with significant motion (which requires more complex encoding), we’ll likely observe larger packet sizes. In static scenes with little change from frame to frame, the resulting packets will be smaller as fewer differences need to be encoded.
  
2. Relative Timestamp:
* The relative timestamp between packets may show a more consistent interval for static scenes, as the data rate remains relatively stable when fewer differences need to be encoded. In contrast, during scenes with motion, the frequency of larger packets (I-frames) may increase, resulting in a less regular timestamp pattern.
  
3. Timing Difference Between Packets:
* The timing differences between packets are influenced by the scene’s complexity. For scenes with significant motion, more packets need to be transmitted quickly to maintain the video’s fluidity, resulting in shorter timing differences between packets.
* In static scenes, since fewer packets are needed to represent the scene, the timing differences might be larger, with packets being sent at less frequent intervals.
  
4. Raw Data:
* Although the raw data is encrypted, it still contains valuable patterns that can be used by neural networks for learning.

Since the dataset we created is not large enough, overfitting occurred in our experiment. Therefore, we applied Principal Component Analysis (PCA) to reduce the dimensionality of the input raw data, as it is likely to contain redundant information and noise.

<img width="1014" alt="image" src="https://github.com/user-attachments/assets/4335275e-6705-4e3f-94ae-bd72272b9ad4">


## 4. Wi-Fi Packet Analysis with LSTM
We analyzed the characteristics of Wi-Fi packets, focusing on their sequential nature, time dependencies, and transmission patterns.

1. Sequential Nature:
Wi-Fi packets arrive in a specific order, forming a sequential flow of data.

3. Time Dependencies:
The timing between packets indicates network activity, such as congestion or delays.

4. Transmission Patterns:
Packet transmission often shows periodic bursts and changes in packet size, reflecting network behavior.

To model these characteristics, we used Long Short-Term Memory (LSTM) networks, which are well-suited for sequential data. LSTM networks capture both short-term and long-term dependencies, allowing us to detect patterns in packet arrival and size changes over time.

![LSTM_Cell svg](https://github.com/user-attachments/assets/c2d4a918-2eca-4df3-b9ff-fd09e18e30a4)
<p align="center">By Guillaume Chevalier - File:The_LSTM_Cell.svg, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=109362147</p>

Our code for **LSTM** can be found at: [LSTM Code](https://drive.google.com/file/d/1pprDRGJ8rJU1_BBaC2nSboCtED4ne96n/view?usp=sharing)

OUR **BEST MODEL** can be found at: [Best Model Code](https://drive.google.com/file/d/1HiIyg7Vl3xXvdV6SsQMzfeyxCUanghgG/view?usp=share_link)


Also, we've tested with other algorithms but received lower accuracy:

**KNN** code can be found at: [KNN Code](https://drive.google.com/file/d/1iz_UsknPecgTOGVodqcKuv07nHfwUqJm/view?usp=share_link)

**HMM** code can be found at: [HMM Code](https://drive.google.com/file/d/14fSbUs4xWUS_v8MiYYj7hMKvZ0vrsp0h/view?usp=share_link)

**DECISION TREE** code can be found at: [Decision Tree Code](https://drive.google.com/file/d/13EVhBrG8-FMqMXZps9YmxYXTACod-r60/view?usp=share_link)

**SVM** code can be found at: [SVM Code](https://drive.google.com/file/d/1JYQbJJbcSaHmGLjU__qGeaBzYKtYzmZ9/view?usp=share_link)

**MLP** code can be found at: [MLP Code](https://drive.google.com/file/d/1x-SDei8_IJZ6IihagWwy0vYkGxr8ODhR/view?usp=share_link)

**TRANSFORMER** code can be found at: [Transformer Code](https://drive.google.com/file/d/1r2YFhK9J4cdkMYK5XkTrPbKfyr7Pi0te/view?usp=share_link)

# Evaluation and Results

## Training Set Metrics:

- **Accuracy**: 0.74
- **Precision**: 0.81
- **Recall**: 0.74

### Classification Report:

| Category        | Precision | Recall | F1-Score |
|-----------------|-----------|--------|----------|
| Static          | 0.93      | 0.72   | 0.81     |
| Slightly Move   | 1.00      | 0.60   | 0.75     |
| Move            | 0.58      | 1.00   | 0.73     |
| Intensely Move  | 0.75      | 0.63   | 0.69     |
| **Average**     | 0.81      | 0.74   | 0.75     |


## Validation Set Metrics:

- **Accuracy**: 0.48
- **Precision**: 0.51
- **Recall**: 0.50

### Classification Report:

| Category        | Precision | Recall | F1-Score |
|-----------------|-----------|--------|----------|
| Static          | 0.44      | 0.57   | 0.50     |
| Slightly Move   | 0.75      | 0.30   | 0.43     |
| Move            | 0.45      | 0.71   | 0.56     |
| Intensely Move  | 0.40      | 0.40   | 0.40     |
| **Average**     | 0.51      | 0.50   | 0.47     |

## Overall Metrics:

- **Accuracy**: 0.67
- **Precision**: 0.72
- **Recall**: 0.67

### Classification Report:

| Category        | Precision | Recall | F1-Score |
|-----------------|-----------|--------|----------|
| Static          | 0.74      | 0.68   | 0.71     |
| Slightly Move   | 0.92      | 0.48   | 0.63     |
| Move            | 0.55      | 0.92   | 0.69     |
| Intensely Move  | 0.67      | 0.58   | 0.62     |
| **Average**     | 0.72      | 0.67   | 0.66     |

# Discussion and Conclusions
## Model Disscussion
Our best model is based on an LSTM architecture for the classification task. The input data for the model undergoes feature extraction and preprocessing, providing rich contextual information for the classification task. The feature extraction process consists of two main components: the first is the raw network traffic features, including timestamps, packet lengths, and other information; the second is the dimensionality-reduced features obtained through PCA, which reduces the original high-dimensional features to 256 dimensions, thereby lowering computational complexity while retaining essential information. Afterward, Feature 1 and the PCA-reduced Feature 2 are time-aligned and concatenated horizontally to form the final input features for the model, with a total input dimension of 2834.

In terms of architecture, the LSTM model consists of three layers. The first layer is the LSTM layer, designed to extract temporal features and capture dynamic patterns of motion state changes. The second layer is a fully connected (FC) layer that maps the output of the LSTM to the classification space. Finally, the output layer performs a 4-class classification task, distinguishing between static, slightly moving, moving, and intensely moving states. The hidden layer is set to contain 16 neurons, with a Dropout layer (set to 0.4) included to mitigate overfitting risks.

The hyperparameters of the model have been carefully designed. The learning rate is set to 0.001 and is adaptively adjusted using a scheduler. Additionally, weight decay regularization is applied to prevent excessively large weights from negatively impacting the model’s performance. The Adam optimizer is employed to further enhance the efficiency of the training process.

During the training and evaluation process, the learning rate is dynamically adjusted based on changes in the training loss to improve convergence speed and generalization performance. On the training set, the model demonstrated good classification ability, achieving an accuracy of 78.57%. However, on the validation set, the accuracy was 48.28%, indicating room for improvement in generalization.
## Result Metrics Discussion
### Training Set Analysis
On the training set, the model performs reasonably well, achieving an accuracy of **74%**, indicating that the model correctly classified most samples. And the average recall is **74%**, suggesting that while the model's predictions are generally accurate, it misses some samples in certain categories.

#### Static:
- Precision: **93%**, showing that the model predicts the static category very accurately, with most predictions being correct.
- Recall: **72%**, meaning that **28%** of static samples were misclassified as other categories.

#### Slightly Move:
- Precision: **100%**, indicating that all samples predicted as slightly moving were correct.
- Recall: **60%**, meaning that only **60%** of slightly moving samples were correctly identified, and **40%** were misclassified.

#### Move:
- Precision: **58%**, indicating lower accuracy in predicting the move category, with many misclassifications.
- Recall: **100%**, showing that all samples in the move category were correctly identified with no omissions.

#### Intensely Move:
- Precision: **75%**, Recall: **63%**. The model performs reasonably well in identifying intensely moving samples but still misclassifies some.

Summary: The model performs well on the training set, particularly for static and move categories. However, it struggles with the slightly move and intensely move categories, as shown by their lower recall scores. This highlights the model's difficulty in distinguishing these categories.

---

### Validation Set Analysis

On the validation set, the model's performance is significantly lower than on the training set, with an accuracy of **48%**, indicating insufficient generalization. The average recall (**50%**) is lower than those on the training set, reflecting the model's poor classification performance on the validation set, particularly for certain categories.

#### Static:
- Precision: **44%**, Recall: **57%**. The model performs moderately for the static category, with some static samples misclassified.

#### Slightly Move:
- Precision: **75%**, indicating high precision for the slightly move category.
- Recall: **30%**, showing that most slightly moving samples were not correctly identified, likely due to data imbalance or insufficient features.

#### Move:
- Precision: **45%**, Recall: **71%**. The model achieves decent recall for the move category but has low precision, suggesting many false positives.

#### Intensely Move:
- Precision: **40%**, Recall: **40%**. The model struggles significantly with the intensely move category, showing poor performance in both precision and recall.

Summary: The model performs poorly on the validation set, particularly for the slightly move and intensely move categories. This indicates the model's inability to generalize effectively to unseen data.

---

### Overall Analysis

Combining results from both the training and validation sets, the overall accuracy is **67%** and a average recall of **67%**. While the model performs well for static and move categories, it struggles to differentiate slightly move and intensely move samples.

#### Static and Move:
- These two categories have relatively high precision and recall, indicating that the model successfully learns their features.

#### Slightly Move and Intensely Move:
- The recall scores for these two categories are low, suggesting the model's difficulty in distinguishing them.
- Possible reasons include imbalanced sample distribution, insufficient feature extraction, and limited model capability for handling these more complex categories.
---

## Conclusion
In this project, we combined network traffic data and video motion information to explore various machine learning models and techniques with the goal of achieving high-accuracy classification and analysis of motion states (static, slightly moving, moving, and intensely moving). Through a series of processes involving data preprocessing, feature extraction, and model training, we have made significant progress while also identifying areas in both the data and the models that require improvement. These findings provide a clear direction for future optimizations.

### Project Achievements:
1. **Data Processing and Feature Extraction**:
   - Successfully extracted key features from `.pcap` and `.json` files, including timestamps, packet lengths, and more, which provided a solid foundation for subsequent analysis and classification.
   - Standardized input data through normalization, alignment, and PCA dimensionality reduction, effectively reducing computational complexity while retaining critical information.

2. **Model Development and Comparison**:
   - Implemented and compared various machine learning and deep learning models, including traditional models (e.g., KNN, SVM, Decision Trees, and HMM) as well as deep learning models (e.g., MLP and LSTM).
   - Among the traditional models, performance was generally close to random classification (Base Line: 25%), with most achieving around 25% accuracy, except for HMM, which reached 30%.
   - Deep learning models, particularly LSTM and MLP, outperformed traditional methods, showing strong performance on the training set. However, validation accuracy was relatively lower, especially in distinguishing between slightly moving and intensely moving categories.

3. **Performance Analysis**:
   - The model achieved good recognition performance for static and moving categories, demonstrating its ability to learn key features of these states.
   - Recognition of slightly moving and intensely moving states faced challenges, likely due to insufficient sample sizes and less distinct data features, resulting in lower recall rates.


### Challenges and Future Directions:
1. **Feature Optimization**:
   - The current dataset is limited to 100 samples, restricting the model's learning capabilities. Future efforts should focus on collecting more data, especially for slightly moving and intensely moving categories, to balance the sample distribution.
   - Extracting additional temporal features or combining network traffic data with motion information as multi-modal features could further enhance the model's ability to differentiate between motion states.

2. **Improving Model Generalization**:
   - The significant performance gap between the training and validation sets indicates an overfitting issue. Future improvements could include introducing regularization strategies (e.g., L2 regularization, Dropout) or using data augmentation techniques to improve the model’s generalization.

3. **Multi-Modal Data Integration**:
   - Currently, network traffic and video motion information are processed separately. In the future, combining these two data types into a unified feature space could improve overall model performance.
   - Adding data from other sensors (e.g., motion sensors) could provide additional feature information and further enhance the model's ability to identify motion states accurately.


### Summary:
This project has made significant progress in addressing the multi-modal classification problem involving network traffic and video motion information, offering valuable insights for similar tasks involving temporal data analysis and multi-modal feature integration. Although the model still struggles with some categories, especially in validation accuracy, future improvements in data quality, feature richness, and model architecture are expected to significantly enhance the model’s scalability and practical applicability.

# References

1. Zou, Qingsong, et al. "Iotbeholder: A privacy snooping attack on user habitual behaviors from smart home wi-fi traffic." Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies 7.1 (2023): 1-26.
2. Rahmadi Trimananda, Janus Varmarken, Athina Markopoulou, and Brian Demsky. 2020. Packet-Level Signatures for Smart Home Devices. In Proceedings of 27th Annual Network and Distributed System Security Symposium, NDSS 2020, San Diego, California, USA, February 23-26, 2020. 
3. Ignacio Sanchez, Riccardo Satta, Igor Nai Fovino, Gianmarco Baldini, Gary Steri, David Shaw, and Andrea Ciardulli. 2014. Privacy leakages in Smart Home wireless technologies. In International Carnahan Conference on Security Technology, ICCST 2014, Rome, Italy, October 13-16, 2014. 1–6.
4. “Wireshark · Go Deep.” Wireshark, www.wireshark.org.
5. “Recording a Wi-Fi Packet Trace, Apple Developer Documentation.” Apple Developer Documentation, 2024, developer.apple.com/documentation/network/recording-a-wi-fi-packet-trace.
6. Sharma, Rahul Anand, et al. "Lumos: Identifying and localizing diverse hidden {IoT} devices in an unfamiliar environment." 31st USENIX Security Symposium (USENIX Security 22). 2022.
7. Singh, Akash Deep, et al. "I always feel like somebody's sensing me! A framework to detect, identify, and localize clandestine wireless sensors." 30th USENIX Security Symposium (USENIX Security 21). 2021.
