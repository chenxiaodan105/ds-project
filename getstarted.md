---
layout: page
title: Data Preprocessing
subtitle: methods for text preprocessing
bigimg: /img/congress.jpg
---


## Overview 

Data Preprocessing could be the key in a NLP task. Without good data, we are just feed machine learning models garbage and get garbage out. In later chapter, I would introduce the explainary data analysis, text preprocessing method, text vectorizer and key words extractions. Let's go !

<img src="../img/against.gif" style="width:100%;" alt="stance detection" />


### 1. EDA
**check speech length distribution**

* original speech length distribution:

<img src="../img/all_speeches_length_distribution.jpeg" style="width:50%;" alt="stance detection" />

* zoom in and check speech length(5<length<1000) distribution:

<img src="../img/speeches_with_normal_length_distribution (5<length<1000).jpeg" style="width:50%;" alt="stance detection" />


**check stance distribution**

* original stance distribution:

{% include 11.html %}


### 2. Text Preprocessing Methods
* tokenization

* remove special words

* remove words that are not purely alphabetic words

* remove stopwords

* remove all words that have a length <= 1 characters (this number can be changed)

* limit word frequency


### 3. Text Vectorizer

* Tf-Idf 

* Bag of Words
 
 
### 4. Word Embedding
 
A word embedding is a learned representation for text where words that have the same meaning have a similar representation. It is this approach to representing words and documents that may be considered one of the key breakthroughs of deep learning on challenging natural language processing problems.

check the graph below to have a look at part of the word embedding in this project:
 
 <img src="../img/word_embedding.png" style="width:100%;" alt="stance detection" />
 
 
### 5. Key Words Extraction
 
 **key words extraction from logistic regression**
 
  <img src="../img/LR_feature_importance.png" style="width:100%;" alt="stance detection" />
  
 * for words that contribute to the class 'no stance'
 
  <img src="../img/good.png" style="width:40%;" alt="stance detection" />
  
 * for words that contribute to the class 'have stance'
 
  <img src="../img/bad.png" style="width:40%;" alt="stance detection" />
  
  
  **key words extraction from random forest**
  
  <img src="../img/RF_feature_importance.png" style="width:100%;" alt="stance detection" />
  
  
 
 
 
 


 
 









