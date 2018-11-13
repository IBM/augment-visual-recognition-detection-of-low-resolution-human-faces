## Work In Progress

<!--Put badges at the very top -->
<!--change the repo -->

<!--Add a new Title and fill in the blanks -->
# Augment Visual Recognition Face Detection to further Identify Covered human faces

In this code pattern, we will demonstrate a methodology to extend `Watson Visual Recognition` face detection by providing a strategy that will detect the border cases such as, blur and covered faces, with `Tensorflow Object Detection`, compiled in `Watson Studio`.

When the reader has completed this code pattern, they will know how to:

* Use and understand Tensorflow Object Detection API's models.
* Understand Watson Visual Recognition's face detection.
* Understand the strategy used to overcome border cases of a Face Detection Model.
* Create and run a Jupyter notebook in Watson Studio.
* Use Object Storage to access data files.

<!--add an image in this path-->
![](/doc/source/images/architecture_diagram.png)

## Flow

1. Create an Image Dataset containing faces that required to be detected, upload these images on Cloud Object Storage.
2. Next these image files are fed into the Watson Studio python notebook.
3. The algorithm first detects faces using a model of Tensorflow Object Detection API.
4. The detected faces are augmented to Watson Visual Recognition face detection output.


<!--Optionally, update this section when the video is created-->
# Watch the Video



# Steps

1. [Sign up for IBM Watson Studio](#1-sign-up-for-ibm-watson-studio)
2. [Create Watson Visual Recognition Service](#2-create-watson-visual-recognition-service)
3. [Run using a Jupyter notebook in the IBM Watson Studio](#3-run-using-a-jupyter-notebook-in-the-ibm-watson-studio)
4. [Analyze the Results](#4-analyze-the-results)


## 1. Sign up for IBM Watson Studio

Once you have created an IBM Cloud Account, navigate to [Watson Studio](https://console.bluemix.net/catalog/services/watson-studio) service and click on the `Create` button.

By signing up for IBM Watson Studio, two additional services will be created - ``Spark`` and ``ObjectStore`` in your [IBM Cloud dashboard](https://console.bluemix.net/dashboard/apps).

## 2. Create Watson Visual Recognition Service

Go to the [Watson Visual Recognition Service](https://console.bluemix.net/catalog/services/visual-recognition) and click on the `Create` button.

![](/doc/source/images/Visual_Recognition_Service.png)

The ``Watson Visual Recognition`` service will be added to your [IBM Cloud Dashboard](https://console.bluemix.net/dashboard/apps).

## 3. Run using a Jupyter notebook in the IBM Watson Studio

1. [Data Preparation](#41-data-preparation)
2. [Model Preparation](#42-model-preparation) 
3. [Create Object Storage service instance](#43-create-object-storage-service-instance)
4. [Create a notebook on Watson Studio](#44-create-a-notebook-on-watson-studio)
5. [Add Tensorflow Object Detection API files](#45-add-tensorflow-object-detection-api-files)
6. [Update notebook with service credentials](#46-update-notebook-with-service-credentials)
7. [Run the notebook](#47-run-the-notebook)


### 3.1 Data Preparation

You can use the dataset provided in this code pattern or create your own dataset. To use the dataset provided in this code pattern, directly use the [Data](https://github.com/IBM/augment-visual-recognition-detection-of-low-resolution-human-faces/tree/master/Data) in this repo. Copy this directory into your created `object_detection` folder.

#### To create your own dataset

Create a folder named `Data` in the created `Object_Detection` folder. Ensure the name of the image file follows the format of `label1` where label can be any label assigned to the image and the number increments for each image.
Eg: Covered1.jpg, Covered2.jpg and so on.

Update the `name` field to your desired name in the `object-detection.pbtxt` file within the unzipped `Object_Detection` folder.

![](/doc/source/images/label.png)

Compress the `Object_Detection` folder so it can be uploaded to Object Storage.

If you are using a mac machine then compression creates some additional files which should be deleted. On command prompt, go to the compressed file location and run the following commands:
```
* zip -d Object_Detection.zip \__MACOSX/\\*
* zip -d Object_Detection.zip \\\*/.DS_Store
```

### 3.2 Model Preparation

* Follow this link- https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md and download any of the COCO trained models, as per your requirement. If you are using the same dataset the preferred model would be `ssd_mobilenet_v1_coco`.
* When you clone the repo
* In the created `object_detection` folder and replace the existing model folder with the unzipped downloaded model.

* Add the `object-detection.pbtxt` file in this repo to the `object_detction` folder.

* Once all components are added your `object_detection` folder would contain the following directory structure.

![](/doc/source/images/Directory_Structure.png)

* Zip the Object_Detection folder to upload it on Object Storage later.


### 4.3 Create Object Storage service instance

If you do not have an Cloud Object Storage instance in you dashboard - [Create an Object Storage instance](https://console.bluemix.net/catalog/services/cloud-object-storage) in your IBM Cloud.

### 4.4 Create a notebook on Watson Studio

A [notebook](https://datascience.ibm.com/docs/content/analyze-data/notebooks-parent.html) in Watson Studio is a web-based environment for interactive computing. You can run small pieces of code that process your data, and you can immediately view the results of your computation.

* Login to [IBM Cloud Dashboard](http://console.bluemix.net/). 
* Click on the Watson Studio instance that was created earlier. 
* Click `Get Started` button at the bottom of the page.

![](/doc/source/images/Get_Started_Watson_Studio.png)

* Select the `New Project` option from the Watson Studio landing page and choose the `Standard` option.

![](/doc/source/images/Create_Watson_Studio_Project.png)

* To create a project in Watson Studio, give the project a name and select the Cloud Object Storage service created.

![](/doc/source/images/Project_Name.png)

* Upon a successful project creation, you are taken to a dashboard view of your project. Take note of the `Assets` and `Settings` tabs, we'll be using them to associate our project with any external assets (datasets and notebooks) and any IBM cloud services.

![](https://raw.githubusercontent.com/IBM/pattern-images/master/watson-studio/project_dashboard.png)

* From the project dashboard view, click the `Assets` tab, click the `+ New notebook` button.

![](https://raw.githubusercontent.com/IBM/pattern-images/master/watson-studio/new_notebook.png)


* Now select the `From URL` tab to specify the URL to the notebook- https://github.com/IBM/augment-visual-recognition-detection-of-low-resolution-human-faces/blob/master/notebook/Augment_Visual_Recognition.ipynb

![](/doc/source/images/New_Notebook.png)

* Click the `Create Notebook` button.


### 4.5 Add Tensorflow Object Detection API files

* Add `Object_Detection.zip` file, prepared in [this section](#42-model-preparation), to Object Storage. In Watson Studio, go to your project default page, use `Find and Add Data` (look for the 10/01 icon) and its `Files` tab
* Click browse and upload `Object_Detection.zip` file

![](/doc/source/images/add_file.png)

* If you use your own dataset, you will need to update the variables/folder names that refer to the data files in the Jupyter Notebook.
* To open the notebook, click on the edit icon to start editing the notebook on your project.
* In the notebook, update the global variables in the cell, if you had used your model/dataset.

#### Update the Global Variables section.

* In the notebook, Section 3.1, `Set up Model Parameters` Update the `MODEL_NAME` varaible with the name of the folder downloaded at [this section](#42-model-preparation)
* Update the label to the label given to your test images as per [this section](#41-data-preparation)

![](/doc/source/images/Model_Params.png)

### 4.6 Update notebook with service credentials

#### Add the Object Storage credentials to the notebook

Select the cell below `2.1 Add your service credentials for Object Storage` section in the notebook to update the credentials for Object Store.

* Use `Find and Add Data` (look for the 10/01 icon) and its Files tab. You should see the file names uploaded earlier. Make sure your active cell is the empty one below 2.1 Add...
* Under Files, click the dropdown for `Insert to code` for `Object_Detection.zip`
* Click `Insert StreamingBody object`.

![](/doc/source/images/streaming_body.png)

* Make sure the credentials are saved as streaming_body_1. If not edit and replace the numbers to 1. There should be four such occurrences in the cell as shown in the below image

![](/doc/source/images/streaming_body_1.png)

#### Add the Visual Recognition credentials to the notebook

* Go to your [IBM Cloud Dashboard](http://console.bluemix.net/). Select the previously created Visual Recognition instance.

![](/doc/source/images/Visual_Recognition_Credentials.png)

* On the landing page, under the Credentials section, copy the `API key`.
* Now, in the notebook, navigating to `4.3 Augment Object Detection output to Watson Visual Recognition Output`

![](/doc/source/images/Visual_Recognition_Notebook.png)

* In the declaration of `VisualRecognitionV3` service, paste the copied API key as value to the `iam_apikey` variable.

### 4.7 Run the notebook

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


# Sample output

This code patterns aims to show a strategy to cover the border cases, such as a covered face.

After setting up the notebook on Watson Studio, first we get the results of Object Detection API of Tensorflow... where in we treat `Covered face` as a an object. 

![](/doc/source/images/analyze_results_1.png)

Next the objects detected are further augmented to `Watson Visual Recognition` Face Detection, in order to showcase an enhanced face detection model. The `green` box depicts the Object Detection and the `blue` box depicts Watson Visual Recognition's Face Detection Output.

![](/doc/source/images/analyze_results_2.png)

Thus, this pattern demonstrates a methodology to extend Watson Visual Recognition's face detection by providing a strategy that will detect the border cases such as, blur and covered faces.

# Troubleshooting


<!--keep this-->

# License
[Apache 2.0](LICENSE)
