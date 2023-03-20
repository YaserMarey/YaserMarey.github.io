---
layout: post
title: "ML Puzzle Piece-2:What to Solve with ML" 
categories: [MLOps]
excerpt: This is the second post of a series of articles discussing the software engineering perspective of Machine Learning Systems.
---

![ Machine Learning Systems: A Unique Puzzle ](../images/ml_unique_puzzle.png "Machine Learning in Blue")


The decision to utilize machine learning in solving a problem may be influenced by the prevalent hype surrounding AI, rather than a genuine assessment of its potential value. However, it would be unwise to dismiss it completely. Technology is constantly evolving, and we have seen examples of businesses falling behind competitors due to failure to adopt maturing technology. In general, problems solvable with machine learning have one or more symptoms explained in the following.

### There is something to learn
Learning is the new capability science has allowed us to give to machines. But if we want to solve a problem with a machine that can learn, there should be something learnable to start with. This means that:There should be a pattern, observations shouldn't be completely random. This pattern should also span a reasonable window of time, such that the machine can learn and predict outcomes consistently, at least until the next model train.
The pattern changes continuously
Although this sounds contradictory to what I said above, a problem with a changing pattern is a good candidate to be solved using machine learning. Machine learning enables us to automate the task of pattern discovery. Our model is capable of learning from data without the need to know how data is changing. However, if data changes too fast, faster than the time needed to train the model, then we can't learn anything.

### Let there be data
Data is crucial as it is what the model learns from. The scarcity of data is a major issue that can disqualify a problem from being solved by machine learning. We must have enough data or at least be able to collect it in an economically viable method.

### It's okay to make mistakes
Whether False Positive is cheap, False negative or both or error will be averaged over a large number of data samples. In some cases, model mistakes are acceptable because it is comparable to or less than manual human error. ML might also still be suitable if the cost of false positives is tolerable for the sake of reducing false negatives, for example, in the case of detecting if a tumor is malignant or benign in medicine.

### The problem is of a large scale
The scale here means that either the problem affects a large number of people or the solution to the problem would have a high frequency of use. For example, sorting through millions of check numbers or postal codes, such as what [Yann LeCun](https://en.wikipedia.org/wiki/Yann_LeCun) did in 1998 with the OCR for the set of digits from 0 to 9, to be deployed and used in banks and post offices.

----

Stay safe, 

Salam,

