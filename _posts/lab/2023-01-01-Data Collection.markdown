---
layout: default
modal-id: 103
title: <i class="fas fa-clipboard-check"></i>&nbsp;Data Collection for Personalized Walking Augmentation Parameter Analysis
date: 2023-02-01
img: opt_datacollect.gif
headimg: opt_datacollection.gif
headimg_size: 60
alt: image-alt
project-date: 2022.06 ~ Present
category: lab
thumbnail_text: Data Collection for Personalized Walking Augmentation Parameter Analysis
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Project Background </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; Data collection for what? </p>

I am participating in a [project](http://harco.hanyang.ac.kr/2022/04/28/project-voucher_iitp_gait_project.html) that optimally controls the lower-limb exoskeleton robot for personalization.<br>

In general, human walking differs from person to person, and it shows various and irregular patterns even within an individual.<br>

Therefore, when controlling the Lower-Limb exoskeleton robot, it is necessary to be able to properly cope with these variations in order to apply the most optimal assistance.<br>
<br>
To do this, I am collecting data to develop AI models that robustly judge even with these variances in the project, or to analyze personalization parameter factors.<br>

> <a href="#portfolioModal-101" class="portfolio-link" data-toggle="modal">CNN Model for the robust GAIT Phase Recognition & Terrain Recognition</a>
<br>


<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-database" aria-hidden="true"></i>
&nbsp; Types of Data being Collected </p>

- IMU Raw Data : Linear Acceleration, Angular Velocity, Orientation (Sensor Local Reference Frame)
- EMG Signal : RMS, raw sensor signal
- Force Plate : Force, Moment, Center Of Pressure data
- Marker Tracking Skeleton : Markers expressing the Lower-Limb and it's skeleton information.


<br>
<br>

***
<p style="font-size: 33px; color: rgb(25, 22, 150)"> <i class="fa fa-cloud-upload" aria-hidden="true"></i>&nbsp; Data Collection </p>
<br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-wrench" aria-hidden="true"></i>
&nbsp; Sensor Equipments </p>
When collecting data, the following Six sensor equipment were used.

<div class="wrap_five">
    <a href="https://optitrack.com/">
    <img src="img/posting/posting_datacollection/optitrack_logo.png" style="height: 70%; width: 70%;"></a>
    <a href="https://www.kitronyx.com/">
    <img src="img/posting/posting_datacollection/kitronyx_logo.png" style="height: 70%; width: 70%;"></a>
    <a href="https://www.movella.com/">
    <img src="img/posting/posting_datacollection/Xsens_logo.png" style="height: 70%; width: 70%;"></a>
    <a href="https://delsys.com/trigno/sensors/">
    <img src="img/posting/posting_datacollection/delsys_logo.png" style="height: 70%; width: 70%;"></a>
    <a href="https://www.amti.biz/">
    <img src="img/posting/posting_datacollection/AMTI_logo.png" style="height: 70%; width: 70%;"></a>
    <a href="https://www.anybodytech.com/">
    <img src="img/posting/posting_datacollection/anybody_logo.png" style="height: 70%; width: 70%;"></a>
</div>

<br>    



- Optitrack : Vision Based marker Tracking Equipment
- Kitronyx Insole FSR : FSR-based insole pressure sensor
- Xsens mtw Awinda : Wireless IMU Sensor
- Delsys EMG Trigno: Electromyography
- AMTI Force Plate : Calculation of ground reaction force more accurately
- Anybody Motion Analysis S/W : Human Dynamic Modeling-based motion analysis software


What I had to do here was to synchronize and Integrate all the data of the Equipments above.<br>
<br>

<br><br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-signal" aria-hidden="true"></i>
&nbsp; Sensor Software Communication </p>

When collecting data, if the sensor software was incompatible with each other, it had to be made possible to collect from one software through communication protocols or certain equipment for synchronization.

<img src="img/posting/posting_datacollection/communication.png" style="height: 100%; width: 100%;">

The software I used was Motive, Xsens Analyze, and ROS.<br>
<br>
- In the [Motive software](https://optitrack.com/software/motive/), <br>AMTI Force Plate, Delsys Trigno EMG, and Optitrack Marker data were compatible.<br>
<br>
- In the [Xsens Analyze Software](https://www.movella.com/products/motion-capture/mvn-analyze), <br>IMU data, Optitrack Marker data were compatible.<br>
it's IMU Data is not a sensor raw signal, but <u>calculated information about each joint link.</u> 

<br>
- In [ROS](https://www.ros.org/), <br> Optitrack Marker data, EMG Data, IMU Data, Insole FSR Data were compatible.<br>
it's IMU Data is a sensor <u>raw signal. (not calculated)</u> <br>
In the case of ROS, since it communicates based on TCP IP, it could be made compatible with all software that supports TCP IP.

<br>
<p style="font-size: 20px; color: rgb(25, 22, 150)"> <i class="fa fa-link" aria-hidden="true"></i>
&nbsp; Means of Communication  </p>
I was able to communicate between sensors through two methods:
<br> [Esync](https://optitrack.com/accessories/sync-networking/esync-2/) equipment  ,  TCP IP protocol


<br>
<br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-download" aria-hidden="true"></i>
&nbsp; Data Extraction </p>
The data informations to collect are EMG Sensor signal, Optitrack Marker data, Force Plate data, and IMU Sensor's Raw Sensor data.<br>

<br>
Force Plate, Optitrack Marker, and EMG signals, excluding IMU, were compatible with the Motive software, allowing synchronized signals to be received without any problems.<br>
<br>
One problem here was that getting IMU raw sensor values was hard with the Xsens Analyzer software.<br>
The values that the software sent were not raw values, but values that were calculated in some way. 
(Exporting, not real-time transmission, allows me to see the Sensor Raw value, but even this contains a gravity compensation calculation)

- ref: [https://base.xsens.com/s/article/Output-Parameters-in-MVN-1611927767477?language=en_US](https://base.xsens.com/s/article/Output-Parameters-in-MVN-1611927767477?language=en_US)

<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Synchronizer </p>

So the idea I came up with was to use FSR Insole sensor.
<img src="img/posting/posting_datacollection/synchronizer_picture.png" style="height: 100%; width: 100%;">


