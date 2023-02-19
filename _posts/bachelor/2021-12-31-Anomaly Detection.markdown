---
layout: default
modal-id: 2
title: <i class="fa-solid fa-magnifying-glass"></i>&nbsp; (ICPBL) Detecting Anomalies using Machine Learning
date: 2021-12-30
img: anomaly_ensemble.png
headimg: anomaly_detection.png
alt: image-alt
project-date: 2nd semester project for 3rd year of bachelor course
category: bachelor
thumbnail_text: (ICPBL) Producing the ML model that detect Detects Anomalies in Wafer Manufacturing
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What Problem do we want to Solve?  </p>

At the end of the First Semester of second grade course, I did some challenge on the Kaggle site below.
>[https://www.kaggle.com/datasets/arbazkhan971/anomaly-detection](https://www.kaggle.com/datasets/arbazkhan971/anomaly-detection)

<br>
It was to make an ML model to judge defective products in the water manufacturing process.<br>
<br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fas fa-lightbulb" aria-hidden="true"></i>&nbsp; characteristics of the Dataset </p>

<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Curse Of Dimensionality</p>
The number of Feature Sets is too large for the number of data.<br>
the number of dataset is 1763, but the number of feature set is 1559.


<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Highly Imbalanced Dataset</p>
There is much more data on normal products than defective ones.

<p style="font-size: 17px;" style="color: rgb(0, 60, 205);">
● Cannot Using Domain Knowledge</p>
Because the company's process is confidential, it does not disclose what the data features. In other words, Domain Knowledge is not available.


<br>
<br>

<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="far fa-lightbulb" aria-hidden="true"></i>&nbsp; Solution </p>
<br>

<p style="font-size: 20px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Feature Selection </p>
Because the number of data features was too large and the information could not be known, proper visualization and analysis of the data was impossible.<br>
<br>
Even if the EDA process is omitted, I wanted to determine which Feature Set is the most influential Feature Set for learning and remove the Feature Set that is not influential or adversely affecting learning from learning.<br>
<br>
While looking for ways to select the Feature Set properly, I was able to find the [Wrapper Method](https://wooono.tistory.com/249).


<img src="img/posting/posting_anomaly/wrapper.png" style="height: 70%; width: 70%;">

The Wrapper method is the method of extracting the Feature subset that performs best in terms of predictive accuracy.<br>
In other words, it refers to a method of learning all Feature Set combinations one by one to find which Feature Set combination is the most effective for learning.


There are two Types of the Wrapper Method: Forward Wrapper Method , Backward Wrapper Method.

- Forward Wrapper Method:
It starts with no feature, adding the most important feature every time it is repeated until there is no further improvement in performance.

- Backward Wrapper Method:
Start with all features, remove the least important features one by one, and repeat until there is no further improvement in performance.



<br><br>

<p style="font-size: 20px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Ensemble Learning </p>
Ensemble refers to the combination of several weak classifiers to create a strong classifier. The data entering each classifier in the ensemble must be different dataset.

Here, if different datasets were put differently for <u>Record</u>, there was a concern that the performance of Classifier would be greatly degraded due to the insufficient number of datasets.

In order to prevent this problem, we considered putting differently in each model for <u>Feature</u>, (not Record) based on the fact that this dataset is Highly imbalanced.

At this time, the Forward Wrapper method was applied to each learner in order to put most optimal featureset in each Weak Classifier.


The forward wrapper method is a Feature Selection method that returns the most suitable feature combination for the Model among all possible feature combinations.<br>

This method has the disadvantage of taking a very long time because it is a method of finding the most optimal combination by comparing the number of cases one by one.

After calculating the wrapper for each classifier from the outside, I sellected the most optimal feature for each classifier and learned the model.

<img src="img/posting/posting_anomaly/ensemble.png" style="height: 70%; width: 70%;">


Among the learned ML models selected in this way, I selected the three Weak Classifiers that performed the best performance.<br>
<br>
Naive Bayesian and KNN, and Light GBM<br>
(All models are implemented with [scikit-Learn](https://scikit-learn.org/stable/) package)





***
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-check"></i>&nbsp; Performance Evaluation </p>





