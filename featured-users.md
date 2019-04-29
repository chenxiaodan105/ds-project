---
layout: page
title: Results
---

### Methods and Results
* stance detection

{% include compare.html %}


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

<img src="../img/comparison.png" style="width:100%;" alt="method comparison" />



