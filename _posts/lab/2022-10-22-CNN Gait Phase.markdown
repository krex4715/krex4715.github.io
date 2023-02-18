---
layout: default
modal-id: 101
title: <i class="fas fa-laptop-code"></i>&nbsp; Development of the CNN Model for robust GAIT Phase Recognition & Terrain Recognition
date: 2023-02-01
img: gaitphase.gif
headimg: gaitphase.png
alt: image-alt
project-date: 2022-06-01 ~ 2022-10-01
category: lab
thumbnail_text: CNN Model for the robust GAIT Phase Recognition & Terrain Recognition
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What is the GAIT Phase? </p>

<img src="img/posting/posting_cnngait/gaitphase_view.png" style="height: 100%; width: 100%">
GAIT phase is a quantitative value between 0 and 100% of the walking stage.<br>

<br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; Why is it Important? </p>
For optimized gait control of the Exoskeletonr Robot, it is necessary to assist the appropriate magnitutde of the force at the correct timing.<br>

This requires Clarification of the walking stage in the current user's current walk so that the optimization algorithm can be applied appropriately.<br>

<br>
I developed a CNN model that Robustly judges this GAIT Phase regardless of Terrain, Walking Speed / Direction, and  environmental Change in data collection <br>
with <u>a minimum number of IMUs</u>

<br>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Implementation Focus </p>

<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Use as few IMU sensors as possible<br>
● Strong against various speed and geographical changes<br>
● Perform topographic and phase judgments simultaneously by changing the head of one BackBone Network
</p>

<br>
<br>

***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-laptop-code" aria-hidden="true"></i> CNN Model Implementation</p>

Convolutional Neural Network is an artificial neural network model using the characteristics of Convolution Kernel, which filters the characteristic distribution of data.<br>
<br>
Using these characteristics, I thought that the convolutional kernel could filter the characteristic changes over time in walking data.<br>
<br>
<br>


<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Preprocessing </p>
Feature Sets that can be obtained from IMU sensors are Angular Velocity, Linear Acceleration, and Orientation(Quaternion).<br>

Despite this limited information, I tried to proceed with the most optimal preprocessing for the model.<br>

the entire Preprocessing Process is as follows.
<img src="img/posting/posting_cnngait/preprocessing.png" style="height: 100%; width: 100%">
First, IMU data are stacked in order of arrival time, and cut by T seconds to make 2D information.<br>
After that, up/down sampling is performed with 200 fixed records, and then the average filter and Min Max Normalization are performed.<br>



<br>
<br>
The main points of this process are as follows.<br>

<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Orientation-free: the Performance has to be preserved regardless of direction</p>
Linear Acceleration, Angular Velocity is a feature set independent of the user's walking direction because it is defined as the IMU's Local Reference Frame.<br>
But, Orientation Feature is able to has a different value depending on the User's Walking Direction. <br>

So I excluded Orientation information from Input Feature.<br>


<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Stacking up data over time to create inputs that look like 2D photos</p>
Feature information used is Angular Velocity and Linear Acceleration information.<br> 
In order to reinforce the lack of the number of features, data accumulated for T seconds was used as input data.

<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Average Filtering</p>
If the number of records is sampled by the same number(200), when the sampling rate is lower than 200, there is a point where the graph is discretly cut off.<br>
Convolutional Kernel is a kernel that detects characteristic changes in data, and it can be found during experiments that these discrete points have a bad effect on learning.<br>
So to smoothen the data, an average filter was used.
(I mixed Delaying and Pulling filters so that there is no time delay.)
<img src="img/posting/posting_cnngait/filter.png" style="height: 100%; width: 100%">


<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Normalized to be strong against various environmental changes</p>
For Linear Acceleration and Angular Velocity, the scaling of the values may vary slightly if the attachment area is slightly distorted.
Mixmax scaling was performed so that it could respond robustly to this variances.


<br><br><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Model Structure </p>
<img src="img/posting/posting_cnngait/ModelStructure.png" style="height: 80%; width: 80%">








<br>
○ Actual implementation
<video class="video" autoplay muted controls style="width:70%;">
    <source type="video/mp4" src="img/posting/posting_cnngait/terrain_gait_phase_recognition.mp4" >
</video>

