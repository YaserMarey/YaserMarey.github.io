---
title: "Machine Learning Systems: A Unique Puzzle - 4" 
layout: home
parent: "Machine Learning Systems: A Unique Puzzle"
nav_order: 4
nav_exclude: true
---
![ Machine Learning Systems: A Unique Puzzle ](ml_unique_puzzle.png "Machine Learning in Blue")
### This is the post number 4 of a series of articles discussing the software engineering perspective of Machine Learning Systems

# Data Labeling

When addressing a problem with a machine learning solution we spend most of the time working on data.
One of the tasks that could greatly affect the quality of the model and consumes a lot of time is data labeling.

### Methods of labeling
There a number of methods to label data from those:
1-	Hand labeling: problems with handl or manual lableing is that it is 

#### Expensive
    In many cases for example when subject mater experts for examaple x-rays labeling requires a board certified radiologist. 

#### Data Privacy Restrictions
    With manual labeling we have also to understand the Data Privacy restrictions for example we many not be able to share data with an external team to lable it. 
    
### Slow
Hand labeling is time consuming. Slow labeling leads to slow iteration speed. And also means that model update is less frequent than sometimes needed.

2-	Natural labels: this is another method beside hand labeling. Example stock price. Label prediction in this case we will eventually know the price and therefore can train our model based on actual labels obtained naturally from the system. In other cases we can collect feedback from the user either agreeing or disagreeing to the predictions we are making through our model.

3-	Weak supervision: use heuristic rules to label data.

4-	Semi-Supervision: train on small set of hand labeled samples and then use the model to predict, add the high confident predicted samples to train again and so on.
Another method is to use clustering to label similar samples with the same label.

5-	Transfer learning: using pretrained model on a dataset in a problem of a different tdata set with only few samples to finetune the model.

### Labeling Problems
#### Multiplicity
This happen when the same sample is annotated with two different and conflicting labels by two annotators. This problem is inevitable. Something we can do is to clearly define the problem and rules we want annotators to work with.

#### Data Linage
Tracking the sources of the data and sources of labels for each data sample. This is important and helps in tracking changes in model performance due to the introduction of new data samples and how this affects the performance, sometimes data samples and lables are biased therefore tracking sources is important.

#### Class Imbalance
Over-sampling, under-sampling, working out loss function to be less sensitive, choosing the right metrices.

### Solutions
#### Data Synthesis
Some synthesis is possible, which helps a lot with providing data which we agreed that is expensive to collect.

#### Active labeling
Label those samples that model is least certain about or if we apply more than one model then we label those samples which different models don’t agree on their classification or prediction.

### 

Salam,

----

