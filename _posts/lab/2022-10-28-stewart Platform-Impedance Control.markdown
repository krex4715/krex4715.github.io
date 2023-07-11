---
layout: default
title: <i class="fa-solid fa-gear"></i>&nbsp;Development of the Stewart-Gough Platform Impedance Control Algorithm
modal-id: 102
date: 2022-10-28
img: stewart.gif
headimg: stewart.gif
alt: image-alt
project-date: 21.06 ~ 22.06
category: lab
thumbnail_text: Stewart-Gough Platform Impedance Control Algorithm
---



<br><br><br>   

<!-- 
<img src="img/posting/stewart_temp.png" style="height: 100%; width: 100%;"> -->







***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; Project Mission </p>

What I had to do in this Project was to do Impedance Control of the Stewart-Gough Platform manipulator by using Robotics.<br><br>




<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; What is the Stewart-Gough Platform? </p>

The Stewart-Gough platform(a.k.a Stewart Platform) is a type of 6-DOF manipulator with six Prismatic Actuators.<br>
Stewar Platform generally has the structure of<br>
<p style="font-size: 20px;">
- Top Plate<br> 
- Spherical Joint (3-DOF)<br>
- Linear Actuator<br>
- Universial Joint (2-DOF)<br>
- Bottom Plate<br>
</p>
<br>
Because the Stewart Platform motor is oriented in a similar to  to the direction in which the force is to be applied (vertical to the upper plate),<br>
It has the advantage of having <u>a very high carrying load (high robustness),</u> and also being able to <u>firmly control the movement of six degrees of freedom</u> even with simple mechanism.<br><br>


<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; What is the Impedance Control? </p>
<img src="img/posting/posting_stewart/impedance_control_eq.png" style="height: 100%; width: 100%;">

Impedance control is a method of robot control that considers the interaction between the robot and the environment.<br>
This method measures the differences in Actual & Desired Values of q'',q',q (q-set) generated during the interaction between the robot and the environment, and adjusts the robot's motion accordingly.
<br>
q-set can be Cartesian Space Variable, and also Joint Space Variable.<br>
<br>

<img src="img/posting/posting_stewart/stewart_virtual.png" style="height: 80%; width: 80%;"><br>
The control method I applied was in Cartesian Space.
Therefore, it was my goal to implement a system that would force the virtual Spring, Damper to power against differences in the Desired Q-set of the End-Effector.<br><br>



<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; Workflow </p>

<p style="font-size: 20px;">
1. Implementing an Overall High-Level Control Structure<br>
2. Implementing the Dynamic Controller<br>
3. Implementing the Forward Kinematics and Force Torque Mapping<br>
</p>

<br><br><br>

<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fa-solid fa-gear"></i>&nbsp; Implementation </p><br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Overall High-level Control Structure </p>
The First Thing I did was to create an overall Control Structure.<br>

Insufficient knowledge of this, I looked for how impedance control is performed on a typical Robot Arm, UR5.<br>
As a result, I Could lots of Hint from the paper below.
><a href="https://www.researchgate.net/publication/347119124_Sensorless_Impedance_Control_for_the_UR5_Robot">Sensorless Impedance Control for the UR5 Robot</a>
>>Abstract—Robot manipulators are designed to interact with
their surroundings. Even if a task does not specifically involve
interaction, the robot may collide with unknown obstacles during
its motion. To overcome these problems, it is necessary to consider
possible interactions inside the control system. This paper aims
to design a controller that allows the manipulator to reach
a final pose, ...


In this paper, it implement impedance control to move the Actual Q-set value, which is obtained from motor encoder& Forward Kinematics, to Desired Q-Set.<br>
<br>
the Entire Control Structure is described as below.<br>
<img src="img/posting/posting_stewart/ur-5_control.png" style="height: 100%; width: 100%;">

A brief summary of the structure above is as follows.

***
<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">

1. Take "Position in Current Cartesian Space" from the controller and calculate "the Force each actuator must Exert to go to Desired Position"<br><br>

2. Change Joint Space Force to Acceleration in Cartesian Space in Forward Dynamics<br><br>

3. Integrate acceleration in Cartesian Space twice to switch to Position in Cartesian Space<br><br>

4. Convert "Position in Catesian Space" to "Position in Joint Space" using Inverse Kinematics (a.k.a I.K Solver)<br>
   (in revolute actuator, position means 'rotation Angle')<br><br>

5. The motor driver applies a position value to the motor and transfers the actual position of the current motor from the motor encoder to the Forward Kinematics (a.k.a F.K Solver) node.<br><br>

6. Use Forward Kinematics to convert the current Actual Joint Position to the Actual Cartesian Position, which is fed back to the Controller node.<br>

</p>

<i class="fas fa-repeat"></i> Repeat entire Process

***

Stewart Platform Manipulator is closed chain, not Open Chain's robotic arm as above,<br>
so the internal structure of the controller is very different.<br><br>

but the Overall Control Structure is the same.
- There's only one thing different. The input value accepted by the motor driver is the position value for the ur robot, 
but my motor driver accepted the Torque value. so it did not need a conversion process using Forward Dynamics and IK Solver.

<br><br>

Using the above picture as a hint, I expressed the control structure picture of the Stewart Platform as below.
<img src="img/posting/posting_stewart/impedance_control_structure.png" style="height: 100%; width: 100%;"><br>

As you can see in the picture above, it is a simpler structure that you can convert from Joint Force to Joint Torque.<br><br>

Dynamic Controller is key to the overall control structure. <br>
the Dynamic Controller's inputs are Desired Position(P) & Velocity(P') & Acceleration(P") in Cartesian Space , <br>
and Actual Position(P) & Velocity(P') & Acceleration(P") in Cartesian Space.<br>
<br>
※P is same as Q
<br>
And the Output value is the Joint Force that each Actuator has to exert.
<br><br>








<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Dynamic Controller </p>

The Dynamic Controller was created by referring to the paper below.

><a href="https://www.researchgate.net/publication/220103568_Kinematic_and_dynamic_analysis_of_Stewart_platform-based_machine_tool_structures">Kinematic and dynamic analysis of Stewart platform-based machine tool structures</a>
>>In this paper, an analytical study of the kinematics and
dynamics of Stewart platform-based machine tool structures
is presented. The kinematic study includes the derivation of
closed form expressions for the inverse Jacobian matrix
of the mechanism and its time derivative. An evaluation
of a numerical iterative scheme for an on-line solution of the
forward kinematic problem is also presented.  ...

<br><br>

In the above paper, I borrowed Inverse Kinematics, Jacobian Mapping, and Inverse Dynamics.<br>
The expression that this controller wants to create is as follows.<br>
<img src="img/posting/posting_stewart/impedance_control_eq2.png" style="height: 100%; width: 100%;">



● Fdy<br>
A node that calculates the Actuator Force required to perform Gravity Compensation for the set gravity when the Cartesian Space's Position, Velocity, and Acceleration values are input.<br>
This node can be created by referring to the above paper, and I made it with MATLAB to verify that it works well.<br>
<br>
Here is my MATLAB git repository
><a href="https://github.com/krex4715/stewart_platform_Dynamics">https://github.com/krex4715/stewart_platform_Dynamics</a>
>><a href="https://github.com/krex4715/stewart_platform_Dynamics"><img src="img/posting/posting_stewart/matlabimg.png" style="height: 80%; width: 80%;"></a>

● Fim<br>
Impedance Force only calculates Cartesian Force from the difference from Desired Position Set in Cartesian Space space, as explained above.<br>
<img src="img/posting/posting_stewart/stewart_virtual.png" style="height: 80%; width: 80%;"><br>
Later, the Joint Force following Desired Position Set can be obtained by multiplying Cartesian Force with Jacobian Mapping.<br>
<img src="img/posting/posting_stewart/impedance_control_eq3.png" style="height: 70%; width: 70%;">






<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Forward Kinematics and Force Torque Mapping </p>

○ Forward Kinematics<br>

Because the Forward Kinematics of Stewart Platform is the closed chain structures, unlike a typical Kinematics Solutions in Open Chain Manipulator,<br>
it is much more difficult to find the solution of Forward Kinematis than Inverse Kinematics.<br>
<br>
Therefore, the Forward Kinematics node is usually implemented through an Newton Raphson method rather than an Analytic method, <br>
and the node is implemented using the open source below.

> <a href="https://github.com/roscore/fk_for_stewart_platform_ros">https://github.com/roscore/fk_for_stewart_platform_ros</a>
<br>

○ Force Torque Mapping<br>
Originally, it is a part that can be accurately done only when calculating how much current should be given through dynamic modeling of the motor.<br>
But here, this process was too complicated and I didn't have time, so I thought Force and Torque were in the first linear mapping relationship, and heuristically just found the slope and put it in.
<br><br>


