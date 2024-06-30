---
layout: default
modal-id: 2
title: <i class="fa-solid fa-magnifying-glass"></i>&nbsp; (ICPBL) Machine Learning based Anomaly Detection in Wafer Manufacturing
date: 2021-12-30
img: anomaly_ensemble.png
headimg: anomaly_detection.png
alt: image-alt
project-date: 2nd semester project for 3rd year of bachelor course
category: bachelor
thumbnail_text: (ICPBL) ML for Anomaly detections in wafer manufacturing
---



<br><br><br>   


***
<p style="font-size: 33px; color: rgb(25, 22, 150)"><i class="fas fa-glasses"></i>&nbsp; Introduction </p>
<br>
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-question-circle" aria-hidden="true"></i>&nbsp; What Problem do we want to Solve?  </p>

At the end of the First Semester of second grade course, I did some challenge on the Kaggle site below.
>[https://www.kaggle.com/datasets/arbazkhan971/anomaly-detection](https://www.kaggle.com/datasets/arbazkhan971/anomaly-detection)

<br>
It was to make an Binary Classifier to judge defective products in the water manufacturing process by using machine learning models.<br>
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
Because the number of data features was too large and the feature information could not be known, proper visualization and analysis of the data was impossible.<br>
<br>
Even if the EDA process is omitted, I wanted to determine which Feature Set is the most influential Feature Set for learning and remove the Feature Set that is not or bad influential on learning.<br>
<br>
While looking for ways to select the Feature Set properly, I was able to find the [Wrapper Method](https://wooono.tistory.com/249).


<img src="img/posting/posting_anomaly/wrapper.png" style="height: 70%; width: 70%;">

The Wrapper method is the method of extracting the best fature subset of model.<br>
In other words, it refers to a method of learning all Feature Set combinations one by one to find which Feature Set combination is the most effective for learning.


There are two Types of the Wrapper Method: Forward Wrapper Method , Backward Wrapper Method.

- Forward Wrapper Method:
It starts with no feature, adding the most important feature every time it is repeated until there is no further improvement in performance.

- Backward Wrapper Method:
Start with all features, remove the least important features one by one, and repeat until there is no further improvement in performance.

Among them, I chose the forward wrapper method.

<br><br>

<p style="font-size: 20px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Ensemble Learning </p>
Ensemble Learning refers to the combination of several weak classifiers to create a strong classifier. The data entering each classifier in the ensemble must be different dataset.<br>
(Here, techniques such as Bagging and Pasting are used to determine how different datasets are determined.)

but, if different datasets were put differently for <u>Record</u>, there was a concern that the performance of Classifier would be greatly degraded due to the insufficient number of datasets.

In order to prevent this problem, I considered putting differently for <u>Feature(not Record)</u> in each model, based on the fact that this dataset is Highly imbalanced.

At this time, the Forward Wrapper method was applied to each learner in order to put most optimal featureset in each Weak Classifier.


The forward wrapper method is a Feature Selection method that returns the most suitable feature combination for the Model among all possible feature combinations.<br>
(This method has the disadvantage of taking a very long time because it is a method of finding the most optimal combination by comparing the number of cases one by one.)

After calculating the wrapper for each classifier, I sellected the most optimal feature for each classifier and learned the model.

<img src="img/posting/posting_anomaly/ensemble.png" style="height: 70%; width: 70%;">


Among the learned ML models selected in this way, I selected the three Weak Classifiers that performed the best performance.<br>


- [Naive Bayesian](https://scikit-learn.org/stable/modules/naive_bayes.html)
- [KNN](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)
- [Light GBM](https://lightgbm.readthedocs.io/en/latest/pythonapi/lightgbm.LGBMModel.html)

(All models are implemented with [scikit-Learn](https://scikit-learn.org/stable/) package)


<br><br>
<p style="font-size: 20px; color: rgb(25, 22, 150)"> <i class="fa-solid fa-play"></i>
&nbsp; Voting Method</p>
<br>
Generally, types of Voting include Hard Voting, Soft Voting, Weighted Voting.
<img src="img/posting/posting_anomaly/model_ensemble.png" style="height: 70%; width: 70%;">

The method I chose here is Weighted Voting.<br>
I multiplied the probability value of the each weak classifier by weight and divided the total value by threshold.<br>
<br>
Here, optimization was carried out for the <u>the weight(w1,w2,w3) and threshold values</u> to have the best performance through grid search for 10 random seed values.<br>
(It took a very long time.....)

<br><br><br>


***
<p style="font-size: 24px; color: rgb(25, 22, 150)"> <i class="fa fa-check"></i>&nbsp; Performance Evaluation </p>

The key criteria for selecting the final model are AUC and Recall values.<br>

Due to the nature of the task, I judged that the most fatal case was the situation in which the model judged that there was no problem even though the product was defective. So even if Accuracy and Precision score fall, I chose the model to reduce False Negative (FN) as much as possible.

<img src="img/posting/posting_anomaly/performance.png" style="height: 70%; width: 70%;">

The figure above shows the performance index of the Enseamble model with the best performance, and it could be seen that the Recall and AUC scores for Threshold were the highest.