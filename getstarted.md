---
layout: page
title: Data Preprocessing
subtitle: methods for text preprocessing
bigimg: /img/congress.jpg
---


## Overview 

Data Preprocessing could be the key in a NLP task. Without good data, we are just feed machine learning models garbage and get garbage out. 

<img src="../img/against.gif" style="width:100%;" alt="stance detection" />


### 1. EDA
**check speech length distribution**

* original speech length distribution:

<img src="../img/all_speeches_length_distribution.jpeg" style="width:100%;" alt="stance detection" />

* zoom in and check speech length(5<length<1000) distribution:

<img src="../img/speeches_with_normal_length_distribution (5<length<1000).jpeg" style="width:100%;" alt="stance detection" />


**check stance distribution**

* original stance distribution:

<img src="../img/data distribution before relabelling.jpeg" style="width:100%;" alt="stance detection" />

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
def get_common_tokens(data,min_occurence,max_occurence):
    '''
    get the vocab of the whole corpus
    '''
    vocab = Counter()
    corpus = data['text']
    for speech in corpus:
        tokens = speech.split()
        vocab.update(tokens)
    # keep tokens with a min occurence
    min_occurence = min_occurence
    common_tokens = [k for k,c in vocab.items() if c > min_occurence or c < max_occurence]
    return common_tokens

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
 


 
 









