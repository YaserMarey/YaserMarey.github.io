---
title: "Machine Learning Systems: A Unique Puzzle - 2" 
layout: home
---
![ Machine Learning Systems: A Unique Puzzle ](ml_unique_puzzle.png "Machine Learning in Blue")
### This is the first post of a series of articles discussing the software engineering perspective of Machine Learning System

[1 - Extra Layer of Complexity](https://yasermarey.github.io/ml_unique_puzzle_1.html)

# What to solve with Machine Learning

The decision to utilize machine learning in solving a problem may be influenced by the prevalent hype surrounding AI rather than a genuine assessment of its potential value. However, it would be unwise to dismiss new technology solely due to this factor, as technology is constantly evolving. Failure to adopt a maturing technology could result in falling behind competitors.

In general, problems that we can use machine learning to solve have one or more of the following symptoms:

### 1 - Plenty of data is available
Data is crucial as it is what the model learns from. The scarcity of data is a major issue that can disqualify a problem from being solved by machine learning.

### 2 - Cheap False positives and/or False negatives
In one of the systems we built, we aggregated output over a large number of data samples, so error resulting from mistakenly positively or negatively classified samples is averaged, and could be tolerated, especially if it is comparable to or less than manual human error. ML might also still be suitable if the cost of false positives is tolerable for the sake of reducing false negatives, for example, in the case of detecting if a tumor is malignant or benign.

### 3 - The problem is of large scale
 The scale here means that either the problem affects a large number of people or the solution to the problem would have a high frequency of use. For example, sorting through millions of check numbers or postal codes.

### 4 - Problem pattern change continuously
Although pattern change means a model retraining is needed, a problem with a changing pattern is a good candidate to be solved using machine learning since machine learning enables us to automate the task of continuously identifying new patterns. Our model is capable of learning from data without the need to know how data is changed.


----

