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

<img src="../img/all_speeches_length_distribution.jpeg" style="width:100%;" alt="stance detection" />

* zoom in and check speech length(5<length<1000) distribution:

<img src="../img/speeches_with_normal_length_distribution (5<length<1000).jpeg" style="width:100%;" alt="stance detection" />


**check stance distribution**

* original stance distribution:

{% include 1.html %}

### 2. Text Preprocessing Methods
* tokenization
```
def tokenize_text(text):
    tokens = word_tokenize(text)
    tokens = [token.strip() for token in tokens]
    return tokens
```

* remove special words
```
def remove_special_characters(text):
    tokens = tokenize_text(text)
    pattern = re.compile('[{}]'.format(re.escape(string.punctuation)))
    filtered_tokens = filter(None, [pattern.sub('', token) for token in tokens])
    filtered_text = ' '.join(filtered_tokens)
    return filtered_text
```

* remove words that are not purely alphabetic words
```
def remove_non_alphabetic_characters(text):
    '''
    remove non-alphabetic characters and numbers
    '''
    tokens = tokenize_text(text)
    tokens = [w for w in tokens if w.isalpha()]
    return ' '.join(tokens)
```

* remove stopwords
```
def remove_stopwords(text):
    stop = list(set(stopwords.words('english')))
    tokens = tokenize_text(text)
    filtered_tokens = [token for token in tokens if token not in stop]
    filtered_text = ' '.join(filtered_tokens)
    return filtered_text
```
* remove all words that have a length <= 1 characters (this number can be changed)
```
def remove_tokens_with_length(text,length):
    '''
    remove tokens with length less than or equal the input length
    '''
    tokens = tokenize_text(text)
    tokens = [w for w in tokens if len(w)>length]
    return ' '.join(tokens)
```

* limit tokens frequency

```
def clean_corpus(data, text,min_occurence,max_occurence):
    '''
    ensure all speeches in a corpus only keep tokens with a min occurence
    input: corpus, common tokens with a min occurence in the whole corpus
    output: new target corpus
    '''
    common_tokens = get_common_tokens(data, min_occurence,max_occurence)
    tokens = text.split()
    tokens = [w for w in tokens if w in common_tokens]
    new_speech = ' '.join(tokens)
    return new_speech
```

### 3. Text Vectorizer

* Tf-Idf 
```
def tfidf_model(corpus, ngram_range=(1, 1),min_df=0.1,max_df=0.9,max_features=5000):
    vectorizer = TfidfVectorizer(min_df=min_df,
                                 max_df=max_df,
                                 stop_words='english',
                                 ngram_range=ngram_range,
                                 max_features = max_features)
    features = vectorizer.fit_transform(corpus)
    return vectorizer, features
```

* Bag of Words
```
def bow_model(corpus, ngram_range=(1, 1),min_df=0.1,max_df=0.9,max_features=5000):
    vectorizer = CountVectorizer(min_df=min_df,
                                 max_df=max_df,
                                 stop_words='english',
                                 ngram_range=ngram_range,
                                 max_features = max_features)
    features = vectorizer.fit_transform(corpus)
    return vectorizer, features
 ```
 
 ### 4. Word Embedding
 
A word embedding is a learned representation for text where words that have the same meaning have a similar representation. It is this approach to representing words and documents that may be considered one of the key breakthroughs of deep learning on challenging natural language processing problems.

check the graph below to have a look at part of the word embedding in this project:
 
 <img src="../img/word_embedding.png" style="width:100%;" alt="stance detection" />
 
 
 
 ### 5. Key Words Extraction
 
 **key words extraction from logistic regression**
 
  <img src="../img/LR_feature_importance.png" style="width:100%;" alt="stance detection" />
  
 * for words that contribute to the class 'have stance'
 
  <img src="../img/good.png" style="width:100%;" alt="stance detection" />
  
 * for words that contribute to the class 'no stance'
 
  <img src="../img/bad.png" style="width:100%;" alt="stance detection" />
  
  
  **key words extraction from random forest**
  
  <img src="../img/RF_feature_importance.png" style="width:100%;" alt="stance detection" />
  
  
 
 
 
 


 
 









