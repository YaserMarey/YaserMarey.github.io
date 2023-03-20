---
layout: post
title: "ML Puzzle Piece-3:Marvelous data and where to find it" 
categories: [MLOps]
excerpt: This is the third post of a series of articles discussing the software engineering perspective of Machine Learning Systems.
---

![ Machine Learning Systems: A Unique Puzzle ](../images/ml_unique_puzzle.png "Machine Learning in Blue")


The resurrection of machine learning was only possible because of the internet and the proliferation of data sources.

Thanks to facebook and company 90% of the world's data is [been created in the last two years](https://www.domo.com/learn/infographic/data-never-sleeps-5) and estimates say that IoT devices alone will be pouring [90 Zettabytes](https://www.aparavi.com/resources-blog/data-growth-statistics-blow-your-mind) by 2025. 

But this is only good news for data-hungry deep neural networks! 

As we feed more data into your model, we're giving it the opportunity to learn intricate relationships between the inputs and outputs. This ultimately leads to better performance. However, as the data size increases, so does the time and resources needed for training. But with the development in GPU and cloud computing infrastructure, we are able to build increasingly complex DNN's. 

To discuss data in the context of machine learning we need to look into possible data sources, how to categorize data after collecting them, and how to process this data.

### Data Sources
There are many sources of data that can be used for machine learning, including:

***Public datasets***: There are many publicly available datasets that can be used for machine learning, such as the UCI Machine Learning Repository and the Kaggle Datasets.

***Private datasets***: Organizations may also have their own proprietary datasets that can be used for machine learning.

***Web scraping***: Data can be collected from the internet by web scraping, which involves using a program to extract data from websites.

***APIs***: Many companies and organizations provide APIs (Application Programming Interfaces) that allow developers to access their data.

***Sensor data***: Machine learning can also be applied to sensor data, such as data collected from cameras, microphones, and other types of sensors.

***Social Media***: Social media platforms like Twitter, facebook, LinkedIn, Instagram, etc. provide data for various use cases.

***Surveys***: Surveys can be used to collect data for machine learning.

Ultimately, the choice of the data source will depend on the specific problem we are trying to solve and the type of data that is needed to train your model.

### Data Categories
There are several categories of data that are commonly used in machine learning:

***Labeled data***: This type of data is often used for supervised learning and includes input-output pairs that have been labeled by humans.

***Unlabeled data***: This type of data is often used for unsupervised learning and includes input-only data that has not been labeled by humans.

***Structured data***: This type of data is organized in a specific format, such as a table or spreadsheet. Examples include data stored in a relational database or a CSV file.

***Unstructured data***: This type of data doesn't have a specific format and may include text, images, audio, and video. Examples include data from social media, email, and customer reviews.

***Semi-structured data***: This type of data has some structure, but not as much as structured data. Examples include data stored in XML or JSON format.

***Historical data***: This type of data includes past records and transactions that can be used for predictive modeling.

***Real-time data***: This type of data is generated in real-time, such as sensor data or social media data.

***Synthetic data***: This type of data is artificially created by the machine learning engineer to overcome the lack of data or other issues.

***Time series data***: This type of data includes a sequence of values collected over time. Examples include stock prices, weather data, and sensor data.

***Spatial data***: This type of data includes information about geographical locations, such as coordinates, maps, and satellite images.

***Graph data***: This type of data is represented as a graph, where nodes and edges represent entities and relationships. Examples include social networks and web pages.

***Transactional data***: This type of data is used to record business transactions, such as sales, payments, and customer data.

Each type of data has its own characteristics and may require different pre-processing and feature extraction techniques. The choice of data category will depend on the specific problem we are trying to solve and the type of data that is available.

### Data Models

Data models are used to represent and organize data in a specific format or structure. Some common types of data models include:

***Relational Model***: This model organizes data into a series of tables with rows and columns, where each row represents a unique record and each column represents a specific attribute or field.

***Hierarchical Model***: This model organizes data into a tree-like structure, where each parent node has one or more child nodes. This model is often used to represent data in a parent-child relationship.

***Network Model***: This model organizes data in a graph-like structure, where each node represents a record and each edge represents a relationship between two nodes.

***Object-Oriented Model***: This model organizes data into objects and classes, where each object represents an instance of a class and each class represents a set of properties and methods.

***Document Model***: This model organizes data in a semi-structured format, where each document contains a set of fields with values. JSON and MongoDB are common examples of document data models.

***Key-value Model***: This model organizes data into unique keys and associated values. Each key is unique and it's associated with a value. Redis and Riak are examples of key-value data models. 

### How to process Data 

To process data, we have two commonly used methods: Batch processing and stream processing.

***Batch processing*** refers to the process of collecting, aggregating, and processing large sets of data at a time, typically in non-real-time. The data is collected over a period of time, then processed in a batch in a scheduled time. 

Batch processing is often used for offline analysis, data warehousing, and reporting. Examples of batch-processing systems include Hadoop's MapReduce, Apache Spark, and Apache Storm.

***Stream processing***, on the other hand, refers to the process of analyzing and processing data as it is generated or collected in real time. Stream processing systems are designed to handle high-velocity, high-volume, and continuous data streams. 

The data is processed as soon as it is generated and doesn't wait for a batch of data. Examples of stream processing systems are Apache Kafka, Apache Flink, and Apache Storm.

Both batch and stream processing have their own advantages and use cases. Batch processing is better suited for offline and historical analysis, while stream processing is better suited for real-time monitoring, alerting, and decision-making.

Next, I will discuss Labeling as one of the key processes while working with data and preparing it for training.

----

Stay safe, 

Salam,



