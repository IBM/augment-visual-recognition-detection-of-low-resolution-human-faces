# Short Title

Increase Accuracy of Face Detection with Object Detection

# Long Title

Augment Visual Recognition Face Detection to further Identify Covered human faces with TensorFlow

# Author

* Smruthi Raj Mohan <smrraj32@in.ibm.com>

# URLs

### Github repo

* https://github.com/IBM/augment-visual-recognition-detection-of-low-resolution-human-faces

### Other URLs

* Video URL

# Summary

Face recognition owns significant consideration and is appreciated as one of the most promising applications in the field of image analysis. However, a robust face recognition requires the ability to recognise identity despite many variations in appearance that the face can have in a scene. To achieve an increased accuracy in face detection, we can take the cases where a face detection algorithm fails and append an ML Object Detection model using Tensorflow, to detect the failed cases, by treating them as an object.
In this pattern, we will demonstrate a methodology to extend Watson Visual Recognition's face detection by providing a strategy that will detect the border cases such as, blur and covered faces, using Watson Studio.

# Technologies

* Artificial Intelligence
* Vision
* Tensorflow

# Description

A robust face recognition requires the ability to recognise identity despite many variations in appearance that the face can have in a scene.

How can we achieve an increased accuracy in face detection?

The border cases, where a face detection algorithm tend to fail can be treated as an 'Object'. Then, a model can identify these objects and append it to a face detection algorithm.

For example, suppose we take an example of an image where in a person's face remains covered - like a cloth or cap over a person's head - these faces are treated to be as a separate object, labelled as 'Covered'. Next, the objects detected are appended to a face detection algorithm. Finally, increasing the number of detections done by a face detection algorithm and thereby the accuracy of the prediction.

This code pattern, demonstrates a methodology, for one such border case where it extends Watson Visual Recognition's face detection by providing a strategy that will detect covered faces using Watson Studio, python notebook.

# Flow

![architecture-diagram](https://github.com/IBM/augment-visual-recognition-detection-of-low-resolution-human-faces/blob/master/doc/source/images/architecture_diagram.png)

1. Create an Image Dataset containing faces that required to be detected, upload these images on Cloud Object Storage.
2. Next these image files are fed into the Watson Studio python notebook.
3. The algorithm first detects faces using a model of Tensorflow Object Detection API.
4. The detected faces are augmented to Watson Visual Recognition face detection output.


# Instructions

1. Get the Object Detection Folder
2. Sign up for IBM Watson Studio
3. Create Watson Visual Recognition Service
4. Run using a Jupyter notebook in the IBM Watson Studio
  1. Data Preparation
  2. Model Preparation
  3. Create Object Storage service instance
  4. Create a notebook on Watson Studio
  5. Add Tensorflow Object Detection API files
  6. Update notebook with service credentials
  7. Run the notebook
5. Analyze the Results

# Components and services

* [Tensorflow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)
* [Watson Studio](https://www.ibm.com/in-en/marketplace/watson-studio)
*  [Watson Visual Recognition](https://www.ibm.com/watson/services/visual-recognition/)

# Runtimes

* Python Notebook, Spark Runtime


# Related links

* [Tensorflow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)

# Announcement

Face Detection is one of the most expanding type of recognition in various industries. Initially, it was associated with the security sector but today there is active expansion into other industries including retail, marketing and health. The effectiveness of face detection algorithms is essential to its application in these industries and also for its expansion to other industries.

However, today's face detection algorithm face the following drawbacks-

* Image quality affects how well facial-recognition algorithms work.
* Image size affects how well the face will be recognized.
* The relative angle of the target’s face influences the recognition score profoundly.

Thus, this pattern provides a strategy by which the accuracy of a face detection algorithm can be improved, by treating images with the above mentioned drawbacks as an object, detected by a model and appended to a Face Detection algorithm.
