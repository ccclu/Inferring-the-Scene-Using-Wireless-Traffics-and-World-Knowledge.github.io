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

### 6.1 Detect Motion Changes in User Behavior
Our model must first accurately detect sudden motion changes in user behavior. This includes identifying transitions such as moving from static to active states, shifting from a slow pace to a faster one, and changing from small-range movements (e.g., hand gestures) to large-range movements (e.g., walking).

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

### Essays
1. https://www.usenix.org/conference/usenixsecurity21/presentation/singh  · H.264 Image Compression-Using 3 key frame-types
2. https://www.usenix.org/conference/usenixsecurity22/presentation/sharma-rahul
3. https://dl.acm.org/doi/abs/10.1145/3580890


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
A total of 100 samples. Each with 40 seconds

This dataset offers a robust foundation for studying the relationship between human activities, environments, and Wi-Fi signal patterns.

<video src="[b4_p4_0.mp4]" controls width="600">
  Your browser does not support the video tag.
</video>


<video src="assets/b4_p4_0.mp4" controls width="600">
  Your browser does not support the video tag.
</video>



<video src="(https://github.com/user-attachments/assets/96b7f0d0-d7a0-4487-912d-17d34ff1a155)" controls width="600">
  Your browser does not support the video tag.
</video>
<video src="[assets/video.mp4](https://github.com/user-attachments/assets/2c33b233-3d9e-4b7b-8696-084ed1480325)" controls width="600">
  Your browser does not support the video tag.
</video>
<video src="[assets/video.mp4](https://github.com/user-attachments/assets/2c33b233-3d9e-4b7b-8696-084ed1480325)" controls width="600">
  Your browser does not support the video tag.
</video>







https://github.com/user-attachments/assets/03fc8dc3-e5eb-469c-9d34-68d492397d48




https://github.com/user-attachments/assets/a02c011c-79cd-46fc-82ec-442356552fb9

<img width="1289" alt="image" src="https://github.com/user-attachments/assets/ec855e8a-6425-4ac6-a364-d3d452efc4c5">


## 3. Transmission Pattern Verification





# Evaluation and Results

# Discussion and Conclusions

# References

1. Zou, Qingsong, et al. "Iotbeholder: A privacy snooping attack on user habitual behaviors from smart home wi-fi traffic." Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies 7.1 (2023): 1-26.
2. Rahmadi Trimananda, Janus Varmarken, Athina Markopoulou, and Brian Demsky. 2020. Packet-Level Signatures for Smart Home Devices. In Proceedings of 27th Annual Network and Distributed System Security Symposium, NDSS 2020, San Diego, California, USA, February 23-26, 2020. 
3. Ignacio Sanchez, Riccardo Satta, Igor Nai Fovino, Gianmarco Baldini, Gary Steri, David Shaw, and Andrea Ciardulli. 2014. Privacy leakages in Smart Home wireless technologies. In International Carnahan Conference on Security Technology, ICCST 2014, Rome, Italy, October 13-16, 2014. 1–6.
4. “Wireshark · Go Deep.” Wireshark, www.wireshark.org.
5. “Recording a Wi-Fi Packet Trace, Apple Developer Documentation.” Apple Developer Documentation, 2024, developer.apple.com/documentation/network/recording-a-wi-fi-packet-trace.
