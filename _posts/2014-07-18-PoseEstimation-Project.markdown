---
layout: default
title: <i class="fas fa-walking"></i>&nbsp;Development of Pose Classification Technology <br> for AI Metabus Exercise Platform
modal-id: 1
date: 2014-07-18
img: img_metaverse.png
alt: image-alt
project-date: 22.01 ~ 22.06
thumbnail_text: Development of Pose Classification Technology for AI Metabus Exercise Platform
---


<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What Problem do we want to Solve? </p>
Virtual reality for fitness and health care applications require accurate and real-time pose estimation for interactive features. <br><br> 

Yet, they suffer either a limited angle of view when using handset devices such as smartphones and VR gears for capturing human pose or a limited input interfaces when using distant imaging/computing devices such as Kinect. <br><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; Solution </p>
<img src="img/posting/posting_metaverse/img_tradeoff.png"><br>
Our team's goal was to solve this Trade Off relationship by separating the metaverse and Pose Estimation system.<br>

<img src="img/posting/posting_metaverse/trade_off_solution.png"><br>
The embedded platform NVIDIA Jetson Xavier and camera devices are integrated into one, separating them from other computing platforms to provide a viewing angle for the user's entire body and providing a close input and visualization interface to the user.
<img src="img/posting/posting_metaverse/yoroke_system1.png"><br>


<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Contribution </p>
&nbsp;● This system is a platform to provide the pleasure of exercising with multiple people to those who wanted to exercise with people but were reluctant to reveal themselves to others.<br><br>
&nbsp;● By separating the camera recognition device from the display and input device that the user looks at and inputs, we have established an interface that has a wide camera angle and is comfortable for the user.<br><br>
&nbsp;● In addition, by implementing 3d mapping with a 2D camera, we have built a system that has the potential to reduce equipment costs for Pose Estimation. (Existing 3d cameras and other motion capture equipment are very expensive.)

<br><br><br>





<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-laptop-code" aria-hidden="true"></i> AI Part </p>

I was in charge of the AI part in this project.<br>
My goal was to predict 2D Skeleton information using a 2D camera, <br>and map it to a 3D marker.<br>

The whole process is illustrated as follows.

<img src="img/posting/posting_metaverse/aipart1.png"><br>




<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-person"></i>&nbsp; Pose Estimation </p>





