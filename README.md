# augment-visual-recognition-detection-of-low-resolution-human-faces

Work In Progress


`Intro`

`Architecture Diagram`
## Flow

## Included components

* [Watson Visual Recognition](https://www.ibm.com/watson/services/visual-recognition/): Visual Recognition understands the contents of images - visual concepts tag the image, find human faces, approximate age and gender, and find similar images in a collection.

## Featured technologies

* [Jupyter Notebooks](http://jupyter.org/): An open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text.
* [Tensorflow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection): The TensorFlow Object Detection API is an open source framework built on top of TensorFlow that makes it easy to construct, train and deploy object detection models.

## Video




## Prerequisite
If the below are not already installed on your system, please follow the links and install according to your system specifications-
* [Git](https://git-scm.com/downloads): To clone the repo, alternatively you could use the `Clone or Download` button.
* [IBM Cloud account](https://console.bluemix.net/registration/?target=%2Fdashboard%2Fapps): To access IBM Cloud and Watson Services.
* [IBM Cloud CLI](https://console.bluemix.net/docs/cli): To push the python application on your IBM Cloud Organization.



# Steps

1. [Sign up for IBM Watson Studio](#1-sign-up-for-ibm-watson-studio)
2. [Run using a Jupyter notebook in the IBM Watson Studio](#2-run-using-a-jupyter-notebook-in-the-ibm-watson-studio)
3. [Analyze the Results](#3-analyze-the-results)


## 1. Sign up for IBM Watson Studio

Once you have created an IBM Cloud Account, navigate to [Watson Studio](https://console.bluemix.net/catalog/services/watson-studio) service and click on the `Create` button.

By signing up for IBM Watson Studio, two additional services will be created - ``Spark`` and ``ObjectStore`` in your IBM Cloud dashboard.


## 2. Run using a Jupyter notebook in the IBM Watson Studio

1. [Data Preparation](#21-data-preparation)
2. [Model Preparation](#22-model-preparation) 
3. [Create Object Storage service instance](#23-create-object-storage-service-instance)
4. [Create a notebook on Watson Studio](#24-create-a-notebook-on-watson-studio)
5. [Add Tensorflow Object Detection API files](#25-add-tensorflow-object-detection-api-files)
6. [Update notebook with service credentials](#26-update-the-notebook-with-service-credentials)
7. [Run the notebook](#27-run-the-notebook)


### 2.1 Data Preparation

You can use the dataset provided in this code pattern or create your own dataset. To use the dataset provided in this code pattern, directly use the [Object_Detection.zip]() file given in the git repo.

#### To create your own dataset

Create a folder named `Data` in the [Object_Detection]() folder. Ensure the name of the image file follows the format of `label1` where label can be any label assigned to the image and the number increments for each image.

Compress the `Object_Detection` folder so it can be uploaded to Object Storage.

If you are using a mac machine then compression creates some additional files which should be deleted. On command prompt, go to the compressed file location and run the following commands:
```
* zip -d Object_Detection.zip \__MACOSX/\\*
* zip -d Object_Detection.zip \\\*/.DS_Store
```

### 2.2 Model Preparation

You can use the same Tensorflow model's frozen inference graph used in this code pattern `ssd_inception_v2_coco_2018_01_28`.

#### To use a different model

* Follow this link- https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md and download any of the COCO trained models, as per your requirement.
* Unzip the [Object_Detection]() folder and replace the existing model folder with the unzipped downloaded model


### 2.3 Create Object Storage service instance

If you do not have an Cloud Object Storage instance in you dashboard - [Create an Object Storage instance](https://console.bluemix.net/catalog/services/cloud-object-storage).

### 2.4 Create a notebook on Watson Studio

A [notebook](https://datascience.ibm.com/docs/content/analyze-data/notebooks-parent.html) in Watson Studio is a web-based environment for interactive computing. You can run small pieces of code that process your data, and you can immediately view the results of your computation.

* Login to [IBM Cloud Dashboard](http://console.bluemix.net/). 
* Click on the Watson Studio instance that was created earlier. 
* Click `Get Started` button at the bottom of the page.

![](/doc/source/images/Get_Started_Watson_Studio.png)

* Select the `New Project` option from the Watson Studio landing page and choose the `Jupyter Notebooks` option.

![](/doc/source/images/Create_Watson_Studio_Project.png)

* To create a project in Watson Studio, give the project a name and select the Cloud Object Storage service created.

![](/doc/source/images/Project_Name.png)

* Upon a successful project creation, you are taken to a dashboard view of your project. Take note of the `Assets` and `Settings` tabs, we'll be using them to associate our project with any external assets (datasets and notebooks) and any IBM cloud services.

![](https://raw.githubusercontent.com/IBM/pattern-images/master/watson-studio/project_dashboard.png)

* From the project dashboard view, click the `Assets` tab, click the `+ New notebook` button.

![](https://raw.githubusercontent.com/IBM/pattern-images/master/watson-studio/new_notebook.png)


* Now select the `From URL` tab to specify the URL to the notebook `Put Url` in this repository.

![](/doc/source/images/New_Notebook)

* Click the `Create Notebook` button.


### 2.5 Add Tensorflow Object Detection API files

* Add `Object_Detection.zip` file, created/downloaded in [this section](#21-data-preparation), to Object Storage. In Watson Studio, go to your project default page, use `Find and Add Data` (look for the 10/01 icon) and its `Files` tab
* Click browse and upload `Object_Detection.zip` file

![](/doc/source/images/add_file.png)

If you use your own dataset, you will need to update the variables/folder names that refer to the data files in the Jupyter Notebook.

To open the notebook, click on the edit icon to start editing the notebook on your project.

In the notebook, update the global variables in the cell, if you had used your model/dataset.

#### Update the Global Variables section.

* In the notebook, Section 3.1, `Set up Model Parameters` Update the `MODEL_NAME` varaible with the name of the folder downloaded at [this section](#21-data-preparation)

* Update the label to the label given to your test images as per [this section](#21-data-preparation)

![](/doc/source/images/Model_Params.png)

### 2.6 Update notebook with service credentials

Add the Object Storage credentials to the notebook

Select the cell below 2.1 Add your service credentials for Object Storage section in the notebook to update the credentials for Object Store.

* Delete the contents of the cell
* Use `Find and Add Data` (look for the 10/01 icon) and its Files tab. You should see the file names uploaded earlier. Make sure your active cell is the empty one below 2.2 Add...
* Under Files, click the dropdown for `Insert to code` for `Data.zip`
* Click `Insert StreamingBody object`.
![](images/add_file_imageclassification.png)
* Make sure the credentials are saved as streaming_body_1. If not edit and replace the numbers to 1. There should be four such occurrences in the cell as shown in the below image
![](images/Data_Streaming_Object.png)

### 2.7 Run the notebook

When a notebook is executed, what is actually happening is that each code cell in
the notebook is executed, in order, from top to bottom.

Each code cell is selectable and is preceded by a tag in the left margin. The tag
format is `In [x]:`. Depending on the state of the notebook, the `x` can be:

* A blank, this indicates that the cell has never been executed.
* A number, this number represents the relative order this code step was executed.
* A `*`, this indicates that the cell is currently executing.

There are several ways to execute the code cells in your notebook:

* One cell at a time.
  * Select the cell, and then press the `Play` button in the toolbar.
* Batch mode, in sequential order.
  * From the `Cell` menu bar, there are several options available. For example, you
    can `Run All` cells in your notebook, or you can `Run All Below`, that will
    start executing from the first cell under the currently selected cell, and then
    continue executing all cells that follow.
* At a scheduled time.
  * Press the `Schedule` button located in the top right section of your notebook
    panel. Here you can schedule your notebook to be executed once at some future
    time, or repeatedly at your specified interval.



## 3. Analyze the results




# Troubleshooting

[See DEBUGGING.md.](DEBUGGING.md)

# License

[Apache 2.0](LICENSE)
