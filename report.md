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
* *: Shifting from a static state to an active state;
* *:Moving from slow to fast-paced activities;
* *:Transitioning from small-scale motions (e.g., hand gestures) to large-scale movements (e.g., walking).
By analyzing the I/O flow patterns of traffic packages, we can further validate whether motion changes correspond to variations in network traffic characteristics, thereby enhancing the model's understanding and classification capabilities for multi-modal data.

### 6.2 The intensity of the movement: Velocity and Range
After detecting a change in the user's movement behavior, the system further utilizes neural networks and large language models (LLMs) to conduct an in-depth analysis of the updated movement information, including details such as movement speed and range. Through neural networks, the model can more accurately assess variations in the user's speed following a change in movement state, such as a shift from slow to fast motion or from a static to an active state. Additionally, the model can analyze changes in movement range, for example, transitioning from small hand movements to larger-scale actions like walking. This detailed analysis provides a more precise understanding of the user’s behavioral patterns and state changes, enhancing the capabilities of future intelligent applications.


## 7. Metrics of Success

To evaluate the model's performance, we will employ traditional machine learning metrics, focusing on four key aspects: accuracy, precision, recall, and confidence.
* ***Accuracy***: This metric reflects the overall effectiveness of the model by measuring the proportion of correct predictions out of all predictions made. High accuracy indicates that the model consistently makes correct classifications, providing a reliable overview of its general performance across the dataset.
* ***Precision***: Precision assesses the model’s ability to correctly identify positive instances among the instances it has classified as positive. It is especially crucial in scenarios where false positives (incorrectly labeling an instance as positive) have significant consequences. A high precision score demonstrates that the model is effective at minimizing false positives.
* ***Recall***: Also known as sensitivity or true positive rate, recall measures the model’s capacity to identify all relevant instances within the dataset. It evaluates the proportion of actual positives that the model successfully detects. High recall is essential when it is critical to capture all positive cases, as it reduces the risk of missing any relevant instance.
  
By systematically evaluating the model using these metrics, we can gain a comprehensive understanding of its strengths and areas for improvement, ensuring that it meets the necessary performance standards for accurate, dependable predictions.


## 8. Execution Plan

***1.*** Identify the correlation between traffic packet flow and the target’s movement, confirming the differences in packet flow patterns across various movement modes.\
***2.*** Extract IPB-related information from the traffic flow data and analyze the relationship between the target’s movements and the IPB data.\
***3.*** Train a large language model (LLM) to take traffic flow data over a specific time period as input and output the transition times between different movement modes of the target, along with detailed movement information for each mode.

# Related Work

### a. Papers
Some works[2] and [3] use encrypted trafffc to analyze user behavior in smart home scenarios. And the work[1] identify a new end-to-end attack surface using IoTBeholder, a system that performs device localization, classiffcation, and user activity identiffcation, which can predict the user behavior by generating a branch of sensors’ information from traffic package.

### b. Datasets

self collected dataset
### c. Software

Wireshark[4]\
Macbook wifi sniffer[5]\
Pytorch
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

# References

1. Zou, Qingsong, et al. "Iotbeholder: A privacy snooping attack on user habitual behaviors from smart home wi-fi traffic." Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies 7.1 (2023): 1-26.
2. Rahmadi Trimananda, Janus Varmarken, Athina Markopoulou, and Brian Demsky. 2020. Packet-Level Signatures for Smart Home Devices. In Proceedings of 27th Annual Network and Distributed System Security Symposium, NDSS 2020, San Diego, California, USA, February 23-26, 2020. 
3. Ignacio Sanchez, Riccardo Satta, Igor Nai Fovino, Gianmarco Baldini, Gary Steri, David Shaw, and Andrea Ciardulli. 2014. Privacy leakages in Smart Home wireless technologies. In International Carnahan Conference on Security Technology, ICCST 2014, Rome, Italy, October 13-16, 2014. 1–6.
4. “Wireshark · Go Deep.” Wireshark, www.wireshark.org.
5. “Recording a Wi-Fi Packet Trace, Apple Developer Documentation.” Apple Developer Documentation, 2024, developer.apple.com/documentation/network/recording-a-wi-fi-packet-trace.
6. Sharma, Rahul Anand, et al. "Lumos: Identifying and localizing diverse hidden {IoT} devices in an unfamiliar environment." 31st USENIX Security Symposium (USENIX Security 22). 2022.
7. Singh, Akash Deep, et al. "I always feel like somebody's sensing me! A framework to detect, identify, and localize clandestine wireless sensors." 30th USENIX Security Symposium (USENIX Security 21). 2021.
