---
title: "Machine Learning Systems: A Unique Puzzle - 4" 
layout: home
parent: "Machine Learning Systems: A Unique Puzzle"
nav_order: 4
---
![ Machine Learning Systems: A Unique Puzzle ](ml_unique_puzzle.png "Machine Learning in Blue")
### This is post number 4 of a series of articles discussing the software engineering perspective of Machine Learning Systems

# Data Labeling

When addressing a problem with a supervised learning machine-learning solution we spend most of the time working on data labeling.

Data labeling unexpectedly requires attention from an engineering perspective, we need to look into how we will label our data and the challenges that come with each method. First, we have hand labeling.

1. **Hand labeling**

    The most common labeling method, is the easiest to set up but it has clear drawbacks:

- *Expensive*

    Labeling manually usually requires a subject matter expert, or even a group of them, for example in medicine x-rays labeling requires a board-certified radiologist. In other cases, you will need to carefully design guidelines on how to label the data samples and educate the labeling team on them, and perform a quality check on the team's performance. 

- *Data Privacy Restrictions*

    With manual labeling, we have also to understand the Data Privacy restrictions and in some cases, we may not be able to share data with an external team to label it. 
    
- *Slow*

    Hand labeling is time-consuming. Slow labeling leads to slow development iteration and also means that model update is less frequent than sometimes needed.

2.  **Natural Labels**

    Depending on the data we are working on, it happens that data samples are labeled with ground truth labels are available. For example for stock prices, actual historical prices are known. Therefore we can train our model based on actual labels obtained naturally from the system. In other cases, we can collect feedback from the user either agreeing or disagreeing with the predictions we are making through our model. This happens also on eCommerce websites, where actual customer selections are known and we can use this to train our recommendation systems models.

4. **Semi-Supervision**

    Semi-Supervision is an approach that has proven to be useful to avoid labeling the entire data set. We simply train on a small set of hand-labeled samples and then use the model to predict, add the high-confidence predicted samples to the training data, and then train again, and so on.
    Another semi-supervision method relies on labeling a small set of samples and then using clustering to label similar samples with the same label.

5.  **Transfer Learning**
    Another possible solution is to avoid hand labeling. Here we just use a pre-trained model on a different dataset. We might only need to label a few data samples to fine-tune the pre-trained model. Different tunning techniques are available and usually defined by the pre-trained model.

6. **Active Learning**
    This is not a labeling method as much as it is a technique to enhance the quality of the training data set. Active Learning means selecting the most confusing data samples, those are the ones the model fails to predict correctly, and then labeling more of these samples hoping that this would enhance the quality of predictions. However, too aggressive Active Learning might cause the model to overfit and affect performance negatively.

### Labeling Problems

1. **Multiplicity**

    This happens when the same sample is annotated with two different and conflicting labels by two annotators. This problem is inevitable. Something we can do is define the problem and rules we want annotators to work with, apply quality checks on labels, and define conflict resolution rules.

2. **Data Linage**

    This technique is all about tracking the sources of the data and sources of labels. This is important and helps in tracking changes in model performance due to the introduction of new data samples. It is also important when we add biased data to the training samples and we would like to identify the data source.

3. **Class Imbalance**

    Class Imbalance is a common problem with data labeling. It refers to the case when the number of samples varies drastically among label classes. ML algorithms tend to work well when the distribution of training data label classes is balanced. A couple of things to notice here is that our model must learn from data and not merely reflect the data distribution, second in some cases we prefer that our model perform well in finding less frequent classes than to perform well overall for example in medicine we want to have less number of false negative diagnosis even this would mean more false positives. To overcome the call imbalance problem we can:
    - We should select the evaluation metric carefully. From my experience, two tools that are particularly helpful in a multi-class classification setting are ***Prescioin vs Recall curve*** similar to this![](PR_curve.png) which plots precision against the recall, and shows the trade-off between precision and recall as the classification threshold changes. The curve is used to find the optimal threshold that balances precision and recall, depending on the requirements of the specific problem at hand. For example, in medical diagnosis, it is often more important to have a high recall, to ensure that all positive cases are detected, even if this results in a lower precision. On the other hand, in spam filtering, it is often more important to have high precision, to ensure that only legitimate emails are classified as such, even if this results in a lower recall. The second tool is the confusion matrix![](confusion_matrix.png) which is a table used to evaluate the performance of a classifier. In the context of multi-class classification, it allows us to visualize the performance of the classifier by comparing the predicted class labels with the true class labels. Each row in the confusion matrix represents the actual class, and each column represents the predicted class. 
    - Now that we have better tools to evaluate model performance in a multi-class setting where we have class imbalance problem we experiment with the following methods to enhance the model performance:
    Undersampling: This involves reducing the size of the majority class by randomly removing samples from it to create a balanced dataset.

        -   Oversampling: This involves generating new samples for the minority class until it reaches a balance with the majority class.

        -   Synthetic data generation: This involves using techniques like SMOTE (Synthetic Minority Over-sampling Technique) to generate synthetic data for the minority class.

        -   Class weighting: This involves adjusting the weight of the loss function so that the model pays more attention to the minority class.

        -   Ensemble methods: This involves combining multiple models either by bagging, boosting, or stacking to create an ensemble that can better handle class imbalance.

        -   Modifying the decision threshold: By default, classifiers make predictions based on a threshold of 0.5, but this can be adjusted to balance precision and recall for imbalanced classes.
        
### 

Salam,

----

