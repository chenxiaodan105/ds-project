---
layout: page
title: Deep Learning
subtitle: neural network structure and performance
bigimg: /img/politics2.png
---

## 1. Neural Network Structure:

**1.1 Pretrained GloVe Word Embedding + LSTM**

* structure
This structure involves the use of a pretrained word embedding for representing words, a LSTM for learning how to dicriminate stances on classification problems.  Yoav Goldberg, in his primer on deep learning for natural language processing, comments that neural networks in general offer better performance than traditional machine learning methods, for example, classical linear classifiers, especially when used with pre-trained word embeddings. Let's see how it works and the final performance.

![GloVe + LSTM](/img/glove_lstm.png)

* performance

![performance1](/img/glove_lstm_acc_loss.png)

**1.2 Pretrained GloVe Word Embedding + CNN + LSTM**
* structure

This structure involves an additional Convolutional Neural Network (CNN) to extract high level features compared to the structure above. It's more like a ngram method in traditional NLP problems. Let's see how it works and the final performance.

![GloVe + CNN + LSTM](/img/cnn_lstm.png)

* performance

![performance2](/img/glove_cnn_lstm_acc_loss.png)


