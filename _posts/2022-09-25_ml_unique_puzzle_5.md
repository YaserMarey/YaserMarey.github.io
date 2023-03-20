---
layout: post
title: "Piece-5:Engineering Features" 
categories: [MLOps, Article]
excerpt: This is the post number 5 of a series of articles discussing the software engineering perspective of Machine Learning Systems.
---

![ Machine Learning Systems: A Unique Puzzle ](../images/ml_unique_puzzle.png "Machine Learning in Blue")

We are still talking about data from last two posts. This time I want to summarize feature engieering techniques. Selecting the right features is the very important.

1-	Handling missing values: In statistics and data analysis, "Missing at Random" (MAR), "Missing Not at Random" (MNAR), and "Missing Completely at Random" (MCAR) are terms used to describe the mechanism behind missing data in a dataset. These terms are used to help understand the relationship between the missing data and the variables in the dataset.

Missing Completely at Random (MCAR): Missing data is said to be MCAR if the probability of missing data is independent of both the observed and unobserved data. In other words, there is no relationship between the variables in the dataset and the missing data. MCAR is the ideal scenario, as it does not introduce bias into the analysis.

Missing at Random (MAR): Missing data is said to be MAR if the probability of missing data depends only on the observed data, not on the unobserved data. In other words, the variables in the dataset can be used to predict the likelihood of missing data. MAR can also introduce bias into the analysis, but it is considered less problematic than MNAR.

Missing Not at Random (MNAR): Missing data is said to be MNAR if the probability of missing data depends on the unobserved data. In other words, the missing data is related to variables that are not included in the dataset. MNAR can introduce significant bias into the analysis and is considered the most problematic scenario.

Handling missing values is an important step in data pre-processing and analysis, as missing values can have a significant impact on the results of statistical analyses. There are several methods for handling missing data, and the choice of method depends on the amount of missing data, the nature of the missing data (MCAR, MAR, or MNAR), and the goals of the analysis. Here are some common methods for handling missing data:

Deletion (Listwise or Pairwise): This method involves either deleting all observations with missing values (listwise deletion), or deleting only those observations that have missing values for the specific variables being analyzed (pairwise deletion). This method is suitable for small amounts of missing data and when the data is MCAR.

Mean/Median/Mode Imputation: This method involves replacing missing values with the mean, median, or mode of the non-missing values for the same variable. This method is simple to implement and can be used when the data is MCAR or MAR, but it can also introduce bias into the analysis if the missing values are not MCAR.

Predictive Modeling: This method involves using regression, decision trees, or other predictive models to predict missing values based on the values of other variables in the dataset. This method is more complex than mean imputation, but it can handle missing data that is MAR or MNAR.

Multiple Imputation: This method involves generating multiple imputed datasets, and then analyzing each dataset separately. The results of the analyses are then combined to account for the uncertainty introduced by the imputation process. This method is suitable for datasets with large amounts of missing data and when the data is MAR or MNAR.

2-	Scaling: normalization ( x – min / max – min ) this is to map all values in the range [0 to 1 ] we can also use another formula to map form [-1 to 1] (2*x – min/max-min), also standardization which x – avg(x)/std, also log transformation and log transfomration.

Normalization, standardization, and log transformation are all methods used to pre-process and transform data to make it suitable for further analysis. Here's a brief explanation of each method:

Normalization: Normalization is a method of rescaling a variable to have a values between 0 and 1. This is often done by subtracting the minimum value of the variable and dividing by the range (maximum value minus minimum value). Normalization is useful when comparing variables that have different units or scales, as it puts all variables on the same scale.

Standardization: Standardization is a method of transforming a variable to have a mean of 0 and a standard deviation of 1. This is done by subtracting the mean and dividing by the standard deviation of the variable. Standardization is useful when comparing variables that have different means and standard deviations, as it puts all variables on the same scale.

Log Transformation: Log transformation is a method of transforming a variable to have a logarithmic scale. Log transformation is often used to reduce the influence of outliers, and to make the distribution of the variable more normal. Log transformation is particularly useful when the variable has a skewed distribution or when the variable has a large range of values.


3-	Encoding Categorical Features: assigning a numerical identifier to each category, but this is not working in production very well since categorical classes change all the time that is new values come all the time during production which we didn’t train on at the development time. One solution is to hash input categories using hashing function.

Encoding categorical features is an important step in data pre-processing, as many machine learning algorithms require that input variables be numeric. There are several methods for encoding categorical features, including:

One-hot Encoding: This method creates a new binary variable for each category in a categorical feature. Each observation is then represented by a set of binary variables, with a value of 1 in the corresponding column for the category it belongs to, and a value of 0 in all other columns. One-hot encoding is a suitable method for handling categorical features with a small number of categories.

Label Encoding: This method assigns a unique integer value to each category in a categorical feature. Label encoding is a simple and straightforward method, but it can introduce a numerical ordering into the categories, which may not be appropriate if there is no inherent order in the categories.

Ordinal Encoding: This method assigns a numerical value to each category in a categorical feature based on the order of the categories. Ordinal encoding is appropriate when there is an inherent order in the categories, such as with a scale (e.g., low, medium, high).

Binary Encoding: This method encodes the categories of a categorical feature as binary digits, where each binary digit represents a specific combination of categories. Binary encoding is a suitable method for handling categorical features with a large number of categories.

Count Encoding: This method replaces the categories in a categorical feature with the count of each category in the dataset. Count encoding is a suitable method for handling categorical features with a large number of categories, and it can capture information about the frequency of each category.

The choice of encoding method depends on the specific requirements of the analysis and the algorithm being used. It is important to choose an appropriate encoding method to ensure that the categorical features are represented in a way that is meaningful for the analysis.



4-	Feature Crossing: Multiplying Features that has specific list of values to pick from with each other, for example Marital Status (Married/Single) and Age Group (10-20, 20-30, 30-40, 40-50, 50-60, 60-70, 70-80, 80+) so we will have new set of features such as: (Married, 10-20), (Single, 10-20) …etc
Feature crossing is a method of combining two or more features to create a new feature. The new feature is generated by taking the interaction or combination of the values from the original features. Feature crossing is used to capture higher-order relationships between variables and can help to improve the performance of machine learning models.

For example, if you have two features, "age" and "income", you can create a new feature by crossing these two features, such as "age x income". This new feature will capture the interaction between age and income, and can provide additional information that may not be available from the individual features.

Feature crossing can be applied to both continuous and categorical features. For continuous features, the interaction can be a simple multiplication of the values. For categorical features, the interaction can be a combination of the categories, such as one-hot encoding of the combination.

Feature crossing can lead to an increase in the number of features in a dataset, which can make the analysis more complex. It is important to carefully consider the use of feature crossing, as it may not always be necessary or appropriate for a specific analysis. In some cases, feature crossing can also lead to overfitting, so it may be necessary to apply regularization methods to avoid this issue.


5-	Discrete and Continuous Positional Embeddings: Fourier features.

Salam,

----

