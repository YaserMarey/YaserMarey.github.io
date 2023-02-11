---
title: "Machine Learning Systems: A Unique Puzzle - 4" 
layout: home
parent: "Machine Learning Systems: A Unique Puzzle"
nav_order: 5
nav_exclude: true
---
![ Machine Learning Systems: A Unique Puzzle ](ml_unique_puzzle.png "Machine Learning in Blue")
### This is the post number 5 of a series of articles discussing the software engineering perspective of Machine Learning Systems

# Features Engineering Common Tasks

1-	Handling missing values: Missing not at random (missing is legitimate since it is not applicable, or the data itself is confidential), missing at random (because it was not provided), missing completely at random(randomly missed because of usually errors in data entry), imputate by filling with the mood, mean or default, another option is  to delete ( column or row )

2-	Scaling: normalization ( x – min / max – min ) this is to map all values in the range [0 to 1 ] we can also use another formula to map form [-1 to 1] (2*x – min/max-min), also standardization which x – avg(x)/std, also log transformation.

3-	Encoding Categorical Features: assigning a numerical identifier to each category, but this is not working in production very well since categorical classes change all the time that is new values come all the time during production which we didn’t train on at the development time. One solution is to hash input categories using hashing function.

4-	Feature Crossing: Multiplying Features that has specific list of values to pick from with each other, for example Marital Status (Married/Single) and Age Group (10-20, 20-30, 30-40, 40-50, 50-60, 60-70, 70-80, 80+) so we will have new set of features such as: (Married, 10-20), (Single, 10-20) …etc

5-	Discrete and Continuous Positional Embeddings: Fourier features.

Salam,

----

