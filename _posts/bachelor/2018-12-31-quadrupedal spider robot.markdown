---
layout: default
modal-id: 1
title: <i class="fas fa-spider"></i>&nbsp; Fabrication of a Quadrupedal Spider Robot
date: 2018-12-31
img: fourlegrobot.gif
headimg: spider.gif
alt: image-alt
project-date: 1st semester project for 2nd year of bachelor course
category: bachelor
thumbnail_text: Quadrupedal Spider Robot
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; Quadrupedal Spider Robot </p>
At the end of the First Semester of second grade course, I did a Simple Project to control spider robots using Inverse Kinematics.<br>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Hardward Design </p>

A simple representation of the robot structure is shown below.<br>
Each leg has three motors.<br><br>

<img src="img/posting/posting_spider/hardware_simple.png" style="width:60%;"><br>

To make it into a robot shape, I designed the parts using Solid Works CAD tool & 3d Printer.<br>
<img src="img/posting/posting_spider/solidworks_design.png" style="width:60%;"><br>

<table>
  <tr>
    <td><img src="img/posting/posting_spider/hardware1.jpg" style="width:80%;"></td>
    <td><img src="img/posting/posting_spider/hardware2.jpg" style="width:60%;"></td>
  </tr>
</table>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Analytical Inverse Kinematics Solver </p>
One of the legs of the spider robot to control has 3DOF Robot.

<img src="img/posting/posting_spider/analytic_ik.png" style="width:100%;">

The space to be mapped is a three-dimensional space(x,y,z), so , I could Solve Inverse Kinematics even with a simple cos law as you can see the figure above.<br>

○ Motion Test
<video class="video" autoplay muted controls style="width:50%;">
    <source type="video/mp4" src="img/posting/posting_spider/control.mp4" >
</video>
<br>
<br>
<br>



***

<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fa fa-history" aria-hidden="true"></i>&nbsp; Trial & Error </p>

Since this Quadrupedal Spider Robot consist of cheap motors and simple position control,
There were difficulities in controlling.<br>

○ Failure

<table>
  <tr>
    <td><video class="video" autoplay muted controls style="width:80%;">
        <source type="video/mp4" src="img/posting/posting_spider/failure.mp4" >
    </video></td>
    <td><video class="video" autoplay muted controls style="width:80%;">
        <source type="video/mp4" src="img/posting/posting_spider/failure2.mp4" >
    </video></td>
  </tr>
</table>


<br><br>

After several motion optimizations, I finally succeeded in making this robot walk.

○ Success
<video class="video" autoplay muted controls style="width:50%;">
    <source type="video/mp4" src="img/posting/posting_spider/success.mp4" >
</video>





