---
layout: page
title: Getting started
subtitle: Methods
bigimg: /img/congress.jpg
---

**Stance detection** is the extraction of a people's reaction to a claim made by a primary actor. It is a core part of a set of approaches to capture political trends. Companies are sensitive to political policies. It could bring them a lot of benefits, such as the fund, the support from the government, if they could catch up with political trends beforehand. 

In this project, NLP method is used to do the prediction based on 2 sessions of congressional bills and transcripts.Just explore it and have fun !

## Overview 

### 1. Introduction
Stance detection is the extraction of a people's reaction to a claim made by a primary actor. It is a core part of a set of approaches to capture political trends. Companies are sensitive to political policies. It could bring them a lot of benefits, such as the fund, the support from the government, if they could catch up with political trends beforehand. 

In this project, NLP method is used to do the prediction based on 2 sessions of congressional bills and transcripts.Just explore it and have fun !

### 2. Text Preprocessing
* tokenization
* remove punctuation
* remove words that are not purely alphabetic words
* remove stopwords
* remove all words that have a length <= 1 characters (this number can be changed)
* limit tokens frequency

### 3. Imbalance Data Handling
* balanced ensemble method
* [reference](https://imbalanced-learn.org/en/stable/ensemble.html)
* [original paper](https://statistics.berkeley.edu/sites/default/files/tech-reports/666.pdf)

### 4. Relabeling Model


### 3. Methods and Results
* stance detection

| method |  F1 score(have stance) | F1 score(no stance) |
| ----------- | ----------- | ----------- | 
| tfidf + lr | 0.21 | 0.85 |
| tfidf + random forest |0.16 | 0.96 |
| tfidf + BalancedRandomForest |0.22 | 0.83|
| tfidf + WeightedBalancedRandomForest| 0.19|0.78|
| relabeling model + tfidf + lr  | 0.80| 0.83 |
| relabeling model + tfidf + random forest |0.88|0.91|
| relabeling model + Glove + LSTM |0.86 | 0.96 |
| relabeling model + Glove + CNN + LSTM | 0.86| 0.95 |

<img src="../img/install-steps.gif" style="width:100%;" alt="Installation steps" />


---

See how easy that is? I wasn't lying - it really can be done in two minutes.
