# Core Plug Detector and Auto-Labeler
This github repository is created as a supplementary resource to my Master's thesis conducted during the spring of 2020. The focus of the project was to fine-tune a Faster R-CNN object detection model using the Tensorflow API in order to detect CCA and non-CCA core plugs in optical core images. 

The data used to train and evaluate the various models, and the pipeline configuration files can be found in the [data](data) directory. Further, the notebook used for the data augmentation outlined in the thesis can be found in the [preprocessing](preprocessing) directory. 

## Further Training and Auto-Labeling
This section requires to install Tensorflow and setup the Tensorflow Object Detection Environment, which can be done by following the [installation documentation](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/index.html). The following bullet points summarizes the installation steps necessary in order setup the enviornment with links to their locations in the documentation:

### setup
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
  * Creating TensorFlow records (.xml-->.csv-->.tfrecord)


### Further Training
In order to train the model from the original weights, the following directory ([Faster_RCNN_Inception_Resnet_V2_atrous_COCO_2018_01_28](https://console.cloud.google.com/storage/browser/full-model/faster_rcnn_inception_resnet_v2_atrous_coco_2018_01_28/)) should be downloaded, and the "fine_tune_checkpoint:" option in the configuration file should be changed to the path to this directory.

In order to fine-tune the weights of the final model, i.e. the model used in the fine-tuning approach in the thesis, the following directory ([Final Model (run1)](https://console.cloud.google.com/storage/browser/full-model/final-model/)) should be downloaded, and the "fine_tune_checkpoint:" option in the configuration file hsould be changed to the path to this directory.


### Auto-labeling and Inference demo
A demo for both the auto-labeling tool and for visualizing the model predictions 



[Fine-Tuned Model (run4)](https://console.cloud.google.com/storage/browser/full-model/inference-graph-auto-labeling/)







#### auto-labeling
The inference graph for the M2 model has been frozen and exported so that inference can be done on new core images, as can be seen in the modified object detection tutorial [notebook](inference/object_detection_tutorial_modified.ipynb). The notebook shows inference performed on three optical core images, and the cropped result using the predicted bounding boxes from M2 is saved in the [cropped_output](inference/M2_inference_graph/cropped_output) folder. The notebook and the inference graph can be downloaded and used to perform inference and cropping with the following steps:

  * Download the [inference](inference) folder
  * Move the [notebook](inference/object_detection_tutorial_modified.ipynb) and the [M2_inference_graph](inference/M2_inference_graph) folder into models/research/object_detection
  * Add the optical core images to perform inference on in models/research/object_detection/M2_inference_graph/image
  * Start jupyter notebook from the object_detection directory
  * Perform inference by running the notebook


####
