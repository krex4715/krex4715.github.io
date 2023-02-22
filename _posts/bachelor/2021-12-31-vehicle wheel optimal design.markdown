---
layout: default
modal-id: 3
title: <i class="fa-solid fa-circle-half-stroke"></i>&nbsp; (ICPBL) vehicle Wheel Optimal Design
date: 2021-12-31
img: optimal_wheel.png
alt: image-alt
project-date: 2nd semester project for 3rd year of bachelor course
category: bachelor
thumbnail_text: (ICPBL) vehicle Wheel Optimal Design
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What Problem do we want to Solve?  </p>
In the second semester of the 3rd year of bachelor course, I did a project to design the hollow shaft of a car optimally.<br>




```bash
Mr. A, who works for an automobile company, needs to perform an analysis to design the rear wheel axis of a special car this time.
The outer diameter of the middle and outer parts of the shaft is different, and the weight of the car is 1000 kg.
```

<img src="img/posting/posting_hollowshaft/prob_img.png" style="width:80%;"><br>
```bash
and the cross section of this is shown below.
```
<img src="img/posting/posting_hollowshaft/prob_img2.png" style="width:80%;"><br>





<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-question-circle" aria-hidden="true"></i>&nbsp; Problems & Conditions </p>


● Problems
- Draw FBD,SFD,BMD of the beam
- calculate deflection, maximum stress of the beam
- Design the beam to satisfy minimum mass and deflection (usally, it is a trade off relationship)



● Conditions
- it need to minimize the deflection of the Beam.
- Beam shall not exceed the maximum allowable vertical stress.
- a material of the beam is <u>Steel Alloys Structural A-36</u>, and the characteristics are as follows.
    - 𝐸=200 𝐺𝑃𝑎
    - 𝜌=7.85 𝑀𝑔/𝑚^3 
    - 𝐺=75 𝐺𝑃𝑎 
    - It is assumed that Failure occurs at Yield Strength
    - 𝜎_𝑌=250 𝑀𝑃𝑎 
    - 𝐿_0=1 𝑚
- judge the conditions wich are not given in the question by yourself


<br><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Problem Solving </p>



<img src="img/posting/posting_hollowshaft/prob_simple.png" style="width:80%;"><br>

The weight of the car is 1000kg, and in the picture above, we set F_L to 250Kg. (Assume beam is connected to front and rear wheels and weight distribution is even)