---
layout: default
title: <i class="fas fa-walking"></i>&nbsp;Development of Pose Classification Technology <br> for AI Metabus Exercise Platform
modal-id: 3
date: 2014-07-18
img: Capstone.JPG
headimg: img_metaverse.png
alt: image-alt
project-date: 22.01 ~ 22.06
category: past
thumbnail_text: Development of Pose Estimation for AI Metabus Exercise Platform <br>(Capstone Design Awarded)
---

***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What Problem do we want to Solve? </p>
Virtual reality for fitness and health care applications require accurate and real-time pose estimation for interactive features. <br><br> 

Yet, they suffer either a limited angle of view when using handset devices such as smartphones and VR gears for capturing human pose or a limited input interfaces when using distant imaging/computing devices such as Kinect. <br><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; Solution </p>
<img src="img/posting/posting_metaverse/img_tradeoff.png" style="width:100%;"><br>
Our team's goal was to solve this Trade Off relationship by separating the metaverse and Pose Estimation system.<br>

<img src="img/posting/posting_metaverse/trade_off_solution.png" style="width:100%;"><br>
The embedded platform NVIDIA Jetson Xavier and camera devices are integrated into one, separating them from other computing platforms to provide a viewing angle for the user's entire body and providing a close input and visualization interface to the user.
<img src="img/posting/posting_metaverse/yoroke_system1.png" style="width:100%;"><br>


<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Contribution </p>
&nbsp;● This system is a platform to provide the pleasure of exercising with multiple people to those who wanted to exercise with people but were reluctant to reveal themselves to others.<br><br>
&nbsp;● By separating the camera recognition device from the display and input device that the user looks at and inputs, we have established an interface that has a wide camera angle and is comfortable for the user.<br><br>
&nbsp;● In addition, by implementing 3d mapping with a 2D camera, we have built a system that has the potential to reduce equipment costs for Pose Estimation. (Existing 3d cameras and other motion capture equipment are very expensive.)

<br><br><br>

***








<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-laptop-code" aria-hidden="true"></i> AI Part </p>

I was in charge of the AI part in this project.<br>
My goal was to predict 2D skeleton information using a 2D camera and map it to 3D markers.
In addition, based on the estimated 2D skeleton information, <br>I implemented a simple Machine Learning model that determines the current user's Pose like sitting, standing, and walking.<br><br>
Through this process, the user's movement information was input to the 3D metaverse world.<br><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-person"></i>&nbsp; 3d Pose Estimation </p>

The 3d Pose mapping Prodedure is illustrated as follows.
<img src="img/posting/posting_metaverse/aipart1.png" style="width:100%;"><br>

First, human Skeleton information was extracted in 2D-X,Y coordinates using AI Pose Estimation model. In order to minimize the reference time, we used MobileNet, the lightest model for Poes Estimation.<br><br>
◎ Reference <br> 
- [https://www.tensorflow.org/lite/examples/pose_estimation/overview?hl=ko](https://www.tensorflow.org/lite/examples/pose_estimation/overview?hl=ko)
- [https://junsk1016.github.io/deeplearning/tf-pose-estimation-%EB%B9%8C%EB%93%9C/](https://junsk1016.github.io/deeplearning/tf-pose-estimation-%EB%B9%8C%EB%93%9C/)
- [https://www.augmentedstartups.com/Pose-Estimation](https://www.augmentedstartups.com/Pose-Estimation)

<br>
○ Actual implementation
<video class="video" autoplay muted controls style="width:70%;">
    <source type="video/mp4" src="img/video/posetracking.mp4" >
</video>


<br>
And I used a pose lift model that lifts 2D-X,Y pose datas into 3D-X,Y,Z pose datas so that the extracted 2D data can be mapped in the 3D metaverse world.<br><br>
The metaverse world was implemented by Unity, and the system transmited Marker Data over python TCP IP communication protocol (Socket Programming).<br><br>
◎ Reference <br> 
- [https://github.com/SrikanthVelpuri/tf-pose](https://github.com/SrikanthVelpuri/tf-pose)
- [https://github.com/Jacob12138xieyuan/real-time-3d-pose-estimation-with-Unity3D](https://github.com/Jacob12138xieyuan/real-time-3d-pose-estimation-with-Unity3D)
- [https://github.com/juyongchang/PoseLifter](https://github.com/juyongchang/PoseLifter)
- [J. Chang, G. Moon, K. Lee, Pose Lifter: Absolute 3D human pose lifting network from a single noisy 2D human pose, arXiv preprint arXiv:1910.12029, 2019](https://arxiv.org/abs/1910.12029)
<br>

○ Actual implementation
<video class="video" autoplay muted controls style="width:70%;">
    <source type="video/mp4" src="img/video/3dposetracking.mp4" >
</video>




<br><br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-running"></i>&nbsp; Pose Classification </p>

In addition to mapping poses, it was necessary to distinguish how many times they did and what kind of movements they performed when performing a specific exercise. The model for this is implemented as a simple machine learning model with the previously predicted Pose Estimated 2DX,Y coordinate system as input.

◎ Reference <br> 
- [https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)

<br>
All data for creating the Random Forest model was collected directly by recording the output value of the 2d Pose Estimation model (MobileNet) being actually inference.
- Team members posing as squats for data collection
<img src="img/posting/posting_metaverse/data_collecting.png" style="width:80%;"><br>

***

<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-award"></i>&nbsp; Reward</p>
- 2022 Hanyang Capstone Design Fair . Gold Medal (금상) (학과 1위, 공학대학 전체2위)
<img src="img/posting/posting_metaverse/capstone_award.png" style="width:80%;"><br>
- 2022 Shared AI-Robotics Education 88 Robot Day [SHARE Challenge Bronze Medal](https://gleaming-bar-4ea.notion.site/5eea5ed024054097adf788b62ef08ef2) (동상) <br>
- Publication: [Pose for Metaverse awarded and presented at ICROS'22](http://sigongji22a.icros.org/admin/proceedings/TableOfContents_web.asp)<br>

<img src="img/posting/posting_metaverse/presentation.JPG" style="width:80%;"><br>
<br><br><br><br><br>

***

Project Git Repository : [https://github.com/lpigeon/Pose-Estimation-for-Interactive-Metaverse-Fitness](https://github.com/lpigeon/Pose-Estimation-for-Interactive-Metaverse-Fitness)

