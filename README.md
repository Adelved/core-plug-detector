# core-plug-detector
This github repository is created as a supplementary resource to my Master's thesis conducted during the spring of 2020. The focus of the project was to fine-tune a Faster R-CNN object detection model using the Tensorflow API in order to detect CCA and non-CCA core plugs in optical core images. 

The data used to train and evaluate the various models, and the pipeline configuration files can be found in the [data](data) directory
## Link to Models
[Faster_RCNN_Inception_Resnet_V2_atrous_COCO_2018_01_28](https://console.cloud.google.com/storage/browser/full-model/faster_rcnn_inception_resnet_v2_atrous_coco_2018_01_28/)

[Final Model (run1)](https://console.cloud.google.com/storage/browser/full-model/final-model/)

[Fine-Tuned Model (run4)](https://console.cloud.google.com/storage/browser/full-model/inference-graph-auto-labeling/)


## Further Training and auto-Labeling
This section requires the user to install Tensorflow and setup the Tensorflow Object Detection Environment, which can be done by following the [installation documentation](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/index.html). The following bullet points summarizes the installation steps necessary in order setup the enviornment with links to their locations in the documentation:

#### setup
* [Install Tensorflow](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#tensorflow-installation). Both CPU and GPU support is available.
* [Install Tensorflow Models](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#tensorflow-models-installation) and complete the following steps in the documentation:
  * Install prerequisites
  * Download the TensorFlow models
  * Protobuf installation/compilation
  * Adding necessary Environment Variables
  * COCO API installation
  * Test installation
* If creating a new dataset, consult the [labelImg installation](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#labelimg-installation) and follow the data processing steps outlined in the project report. Alternatively, follow the [documentation](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html) according to the following steps:
  * Preparing workspace
  * Annotating images
  * Creating label map
  * Creating TensorFlow records (xml to csv and csv to tfrecord)

