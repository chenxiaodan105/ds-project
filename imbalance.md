---
layout: page
title: Imbalance Data Handling
subtitle: comparison of three Methods
bigimg: /img/congress.jpg
---

> Has this happened to you?

You are working on your dataset. You create a classification model and get 95% accuracy immediately. “Awesome” you think. You dive a little deeper and discover that 95% of the data belongs to one class. Ooops! This is an example of an **imbalanced dataset** and the frustrating results it can cause.

Imbalanced data typically refers to a problem with classification problems where the classes are not represented equally.
Imbalance Data is common in the world of data. In this project, I met the same problem, let's see how imbalance it is!

{% include 1.html %}

> Why could this happen?

Well, in real world, human labeling for text is expensive, it's time consuming and cost consuming. However, new speeches and bills are generated every day. Here are three possible ways to deal with imbalance data for this project, Let's look at them one by one and pick the best method !

### Method 1: Change ML Models Class Weight

`sklearn ` has its own built-in method to recalculate the weights of different classes in the form `{class_label: weight}`. 
 But in default, all classes are supposed to have weight one. if you want it to recalculate, you could set the parameter `class_weight` to `balance`, which uses the values of y to automatically adjust weights inversely proportional to class frequencies in the input data as n_samples / (n_classes * np.bincount(y)).
 
 Here is an example:
 ```
 from sklearn.linear_model import LogisticRegression
 lr = LogisticRegression(class_weight = 'balanced')
 lr.fit(X,y)
 ```
 
 Here is the result for this project using this method:
 
 {% include original_ml.html %}
 
Unfortunately, for this specific project, the F1 score is still pretty low for the minority class. This method gives very little improvement for both the majority class 'no stance' and the minority class 'have stance', so it's not recommended here.

### Method 2: Resampling

This resampling method for this project is inspired by one paper 'Using Random Forest to Learn Imbalanced Data' firstly.
The author try to use ensemble methods to alleviate the harmness caused by imbalance data. 

>'In this paper we propose two ways to deal with the imbalanced data classification problem using random forest. One is based on cost sensitive learning, and the other is based on a sampling technique. Both methods are shown to improve the prediction accuracy of the minority class, and have favorable performance compared to the existing algorithms.'

**The idea for the balanced random forest ensemble method is:**

- draw a bootstrap sample from the minority class and draw a bootstrap sample from the majority class with the same size of the minority sample

- induce a classification tree to maximize size without pruning. the tree is induced with CART algorithm with the modification of only searching through a set of m randomly selected variables instead of searching through all variables to find the optimal split

- repeat 2 steps above, aggregate the predictions of the emsemble above and get the final prediction

**The idea for the Weighted random forest ensemble method is:**

- place a penalty on misclassifying the minority class. we assign a weight to each class, for the minority class we give a larger weight (i.e. higher classification cost)

- The class weights are incorporated into the RF algorithm in two places. In the tree induction procedure, class weights are used to weight the Gini criterion for finding splits. In the terminal nodes of each tree, class weights are again taken into consideration. The class prediction of each terminal node is determined by “weighted majority vote”; i.e., the weighted vote of a class is the weight for that class times the number of cases for that class at the terminal node.

- The final class prediction for RF is then determined by aggregatting the weighted vote from each individual tree, where the weights are average weights in the terminal nodes. Class weights are an essential tuning parameter to achieve desired performance. The out-of-bag estimate of the accuracy from RF can be used to select weights. This method, Weighted Random Forest (WRF), is incorporated in the present version of the software.

Here is the result for this project using this method:
 
 {% include resampling.html %}
 
 The results have very few improvemnet compared with method 1, but F1 scores for the minority class are basically still very bad. Seems like this method doesn't work here. Since this project is essencially NLP project,when calculating TF-Idf, We have more than 200,000 tokens in our corpus, I think if we resample a very small part of them every time for a tree and finally just aggregate the result, the bias would be very large. That might be the reason it doen't work here. 

You can check these two links for further information:

* [reference](https://imbalanced-learn.org/en/stable/ensemble.html)
* [original paper](https://statistics.berkeley.edu/sites/default/files/tech-reports/666.pdf)
 
 
### Method 3: Relabeling Model (the solution!)

Seems like resampling and class weight method doesn't work like a charm here. So it's a good idea to go back and check data manually. The finding is a surprise here! A lot of speeches in bills and transcripts with some strong indications of stances are mislabeled as '0', namely no stance. Uhhhhh....

That's the reason here comes the regular expression relabeling model. By detecting some strong key words,such as 'support','oppose',etc, the relabeling model would relabel all originally unrelabeled data.

Here is the result for this project using this method:
 
 {% include relabeldata.html %}

**Let's look at the change for stance distribution after relabeling from the perspective: quantity**


{% include stance.html %}

**Let's look at the change after relabeling from a different perspective: proportion**

{% include 1.html %}

{% include 2.html %}
