---
layout: page
title: Imbalance Data Handling
subtitle: comparison of three Methods
bigimg: /img/congress.jpg
---




> Has this happened to you?

You are working on your dataset. You create a classification model and get 95% accuracy immediately. “Awesome” you think. You dive a little deeper and discover that 95% of the data belongs to one class. Ooops!This is an example of an **imbalanced dataset** and the frustrating results it can cause.

Imbalanced data typically refers to a problem with classification problems where the classes are not represented equally.
Imbalance Data is common in the world of data. In this project, I met the same problem, let's see how imbalance it is!

{% include 1.html %}

> Why could this happen?

Well, in real world, human labeling for text is expensive, it's time consuming and cost consuming. However, new speeches and bills are generated every day. 

Here we explore **three ways to deal with imbalance data**: 

* Resampling

* Tune hyperparameters for different machine learning models

* Go back to check data

Let's look at them one by one and pick the best method !

### Method 1: Resampling
* balanced ensemble method
* [reference](https://imbalanced-learn.org/en/stable/ensemble.html)
* [original paper](https://statistics.berkeley.edu/sites/default/files/tech-reports/666.pdf)

### Method 2: Change ML Models Class Weight

### Method 3: Relabeling Model

**Let's look at the change from the perspective: quantity**


{% include stance.html %}

**Let's look at the change from a different perspective: proportion**

{% include 1.html %}

{% include 2.html %}
