---
layout: post
title: "Object Detection in Computer Vision: One Metro Trip Summary" 
categories: [Computer Vision]
excerpt: My Cairo Metro Trips would take 30 minutes on average. This is a summary that may consume such a time frame for such a commuter.
---

***My Cairo Metro Trips would take 30 minutes on average. This is a summary that may consume such a time frame for such a commuter.***

In Computer Vision, we focus on enabling machines to interpret and understand visual information from the world around us. Researchers in computer vision study the following topics:


**1. Object recognition**: The ability to recognize and classify objects within an image or video.

**2. Object detection**: The ability to locate objects within an image or video and draw bounding boxes around them.

**3. Image segmentation**: The ability to segment an image into different regions based on their visual properties.

**4. Image restoration**: The ability to restore images that are degraded or corrupted, such as those blurry or have missing data.

**5. Image generation**: The ability to generate new images similar to a given set of images.

**6. Image classification**: The ability to classify an image into one of several categories.

**7. Pose estimation**: The ability to estimate the pose of objects within an image or video.

**8. Motion analysis**: The ability to analyze the motion of objects within an image or video.

These topics are the foundation of many computer vision applications, such as object recognition, autonomous vehicles, medical imaging, and surveillance systems.

### Object Detection

From those topics, Object detection has gathered a lot of attention.

Object detection has many practical applications, such as in autonomous vehicles, surveillance systems, and image search engines.

There are several object detection algorithms used in computer vision, but some of the most commonly used ones are:

**1. R-CNN** (Region-based Convolutional Neural Network): This algorithm is based on [selective search](https://www.researchgate.net/publication/262270555_Selective_Search_for_Object_Recognition), which is a segmentation algorithm that proposes regions of interest in an image. R-CNN then uses a convolutional neural network (CNN) to classify the proposed regions.

**2. Fast R-CNN**: This algorithm is an improvement over R-CNN, as it eliminates the need for selective search by using a CNN to directly propose regions of interest. It also shares computation across the entire image, which makes it faster.

**3. Faster R-CNN**: This algorithm is an extension of Fast R-CNN that adds a region proposal network (RPN) to generate object proposals. The RPN shares features with the Fast R-CNN detector, which makes it faster and more accurate.

**4. YOLO (You Only Look Once)**: This algorithm is a single-stage object detector that divides an image into a grid of cells and predicts bounding boxes and class probabilities for each cell. It is fast and accurate, but can struggle with detecting small objects.

**5. SSD (Single Shot MultiBox Detector)**: This algorithm is also a single-stage detector that predicts bounding boxes and class probabilities for multiple object scales and aspect ratios at the same time. It is fast and accurate, and can detect small objects well.

**6. RetinaNet**: This algorithm uses a focal loss function to address the class imbalance problem in object detection. It is fast and accurate, and can detect small objects well.

**7. Mask R-CNN**: This algorithm extends the Faster R-CNN algorithm to include a mask prediction branch, which generates a binary mask for each object in addition to its bounding box and class label. Mask R-CNN is useful for instance segmentation, where the goal is to segment each object instance in the image.

8. CenterNet: This algorithm is a one-stage object detection algorithm that directly regresses the center point and size of objects in an image. CenterNet achieves state-of-the-art accuracy while maintaining a fast inference speed.

These algorithms differ in their approach to object detection, with some using region proposal networks and others using single-shot detection. 
But it is importnat to understand the following concpects in general:

1- Single Stage vs Mutliple Stage
2- Backbone
3- Non Max Supperssion
4- mAP
5- IoU

### Single Stage vs Mutliple Stage
***Single-stage algorithms***, such as You Only Look Once (YOLO), treat object detection as a regression problem. They divide the image into a grid of cells, and for each cell, the algorithm predicts a fixed number of bounding boxes and corresponding class probabilities. These predictions are made directly on the raw image pixels, without any intermediate representation. Single-stage algorithms are usually faster than their multiple-stage counterparts, but they may suffer from lower accuracy due to their simplified approach.

***Multiple-stage algorithms***, such as Region-Based Convolutional Neural Networks (R-CNN), use a more complex, multi-stage approach to object detection. First, the algorithm generates a set of region proposals, which are likely to contain objects. Then, for each region proposal, the algorithm extracts a feature vector and passes it through a classifier to determine the object class and refine the bounding box coordinates. This approach is more accurate than single-stage algorithms but can be slower due to the multiple stages involved.

### Backbone
In computer vision, a "backbone" refers to the main architecture or network that forms the base of a deep neural network used for image recognition, object detection, or other computer vision tasks.

The backbone typically consists of a series of convolutional layers that extract low-level features from the input image. These layers are often pre-trained on a large-scale image classification task, such as ImageNet, and then fine-tuned on the target task.

The backbone network is responsible for transforming the input image into a high-level feature representation that can be used for subsequent tasks such as object detection, semantic segmentation, or image classification. The features extracted by the backbone are often fed into additional layers or modules that perform specific tasks, such as region proposal or object classification.

Examples of popular backbones in computer vision include *ResNet*, *VGG*, *Inception*, and *MobileNet*. The choice of the backbone depends on the specific task and trade-offs between accuracy and computational efficiency.

### Non Max Supperssion
In computer vision object detection, non-maximum suppression (NMS) is a post-processing step that is applied to the output of object detection algorithms to eliminate duplicate detections of the same object and to keep only the most confident one.

Object detection algorithms often generate multiple bounding boxes around each object detected in the image. However, these bounding boxes may overlap and can result in multiple detections of the same object. To remove the duplicates, non-maximum suppression is used.

The non-maximum suppression algorithm works by first sorting the detections according to their confidence scores. Then, it selects the detection with the highest confidence score and removes all other detections that have a significant overlap with it, usually defined by an overlap threshold (IoU). This process is repeated until all detections have been processed.

Non-maximum suppression is an essential step in object detection algorithms, as it helps to eliminate redundant detections and improves the accuracy of the output. The NMS algorithm can be easily integrated into most object detection algorithms and is typically implemented as a post-processing step after the detection stage.

### mAP
Mean Average Precision (mAP) is a widely used metric in computer vision for evaluating the performance of object detection algorithms. It is a single number that summarizes how well an algorithm can detect and localize objects in an image.

The mAP is calculated by first computing the Average Precision (AP) for each class of object that the algorithm is supposed to detect. The AP is a measure of the precision and recall of the algorithm, where precision is the percentage of true positive detections out of all detections, and recall is the percentage of true positive detections out of all ground-truth objects.

The average precision (AP) is calculated by integrating the precision-recall curve for each class of object, and then taking the average over all classes. The resulting value is the mAP, which ranges from 0 to 1, where higher values indicate better performance.

Precision and recall are widely used metrics in many machine learning tasks. In object detection, precision measures the accuracy of the algorithm in localizing objects, while recall measures the ability of the algorithm to detect all objects in the image. The balance between precision and recall is important because an algorithm that is too aggressive in detecting objects may have high recall but low precision, leading to many false positives. Conversely, an algorithm that is too conservative in detecting objects may have high precision but low recall, missing many objects.

mAP is a widely used metric in object detection because it combines both precision and recall into a single measure that accounts for the accuracy of object localization and the number of detected objects. It is also sensitive to the trade-off between precision and recall and provides a more comprehensive measure of algorithm performance than either precision or recall alone. Additionally, mAP can be easily calculated and compared across different object detection algorithms, making it a standard metric in the field.

### IoU
Intersection over Union (IoU) is an important measure used in object detection to calculate precision and recall.

IoU is a measure of the overlap between the ground-truth object and the predicted object. It is defined as the area of the intersection between the two objects divided by the area of their union. In other words, IoU measures the percentage of overlap between the predicted bounding box and the ground-truth bounding box.

When calculating precision and recall, IoU is used as a threshold for deciding whether a predicted bounding box is considered a true positive or a false positive. A predicted bounding box is considered a true positive if it has an IoU greater than a specified threshold with a ground-truth bounding box. Otherwise, it is considered a false positive.

Precision is calculated as the ratio of true positive detections to the total number of predicted detections. Recall is calculated as the ratio of true positive detections to the total number of ground-truth objects. The IoU threshold is used to determine which predicted detections are counted as true positives and which are counted as false positives.

For example, if the IoU threshold is set to 0.5, a predicted detection with an IoU greater than 0.5 with a ground-truth object is counted as a true positive. If the predicted detection has an IoU less than 0.5 with all ground-truth objects, it is counted as a false positive. The precision and recall values are then calculated based on these true positive and false positive detections.

In summary, IoU is used in precision and recall calculation as a threshold to determine whether a predicted bounding box is a true positive or a false positive, based on the degree of overlap between the predicted and ground-truth bounding boxes.


## Implementations
There are several implementations of object detection algorithms that you can use for your projects, depending on your programming language and hardware. Here are some popular options:

*TensorFlow Object Detection API*: This is an open-source framework developed by Google that provides a collection of pre-trained models and tools for training custom object detection models. 

*PyTorch Object Detection*: This is a similar open-source framework for object detection based on PyTorch. 

*OpenCV*: This is a popular computer vision library that includes pre-trained models and functions for object detection. OpenCV supports several algorithms including Haar Cascades, HOG+SVM, and DNN (Deep Neural Network).

*Detectron2*: An open-source framework for object detection developed by Facebook AI Research. It is built on top of PyTorch and provides pre-trained models and tools for training custom object detection models, supporting algorithms like Faster R-CNN, Mask R-CNN, and RetinaNet.

*Darknet*: This is an open-source neural network framework that supports object detection algorithms like YOLO. Darknet can be used to train and test custom object detection models, and can run on both CPU and GPU.

That is it for now, 

Stay safe

----
Salam