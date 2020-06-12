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

In order to fine-tune the weights of the final model, i.e. the model used in the fine-tuning approach in the thesis, the following directory ([Final Model (run1)](https://console.cloud.google.com/storage/browser/full-model/final-model/)) should be downloaded, and the "fine_tune_checkpoint:" option in the configuration file should be changed to the path to this directory.



### Auto-labeling and Inference demo
A demo for both the auto-labeling functionality and pixel-depth map functionality has been made, which can be downloaded and used. Both require the installation of the tensorflow setup above and can be directly downloaded and tested with the sample data provided. Both demos uses CPU for inference which is slower, but does not require GPU support or setup for the user. For larger data sets, it is recommended to use GPU support and both demos can be reverted back to GPU by removing the following lines of code in both notebooks:
```python     
	for op in ops: 
            op._set_device('/device:CPU:*')  

```

#### Auto-labeling
The [auto-labeling demo](auto_labeling_demo) shows the auto-labeled core plugs on the easy test set, which can be opened and inspected using lableImage. In order to use the demo, the exported inference graph of the fine-tuned model must be downloaded from the following directory, [Fine-Tuned Model (run4)](https://console.cloud.google.com/storage/browser/full-model/inference-graph-auto-labeling/), and placed inside auto_labeling_demo folder. When this is done, [auto-label Notebook](auto_label_demo/the_auto_label_core_plugs.ipynb) can be run to generate the labels.

In order to generate labels for a new data set: fine-tune the model on a data set using a few hand-labeled examples -> export inference graph -> change path to inference graph in the notebook.
```python
MODEL_NAME = 'path/to/folder_of_exported_inference_graph'
```

#### Pixel-Depth mapping demo
The [auto pixel-depth mapping demo](auto_pixel_depth_mapping_demo) contains a .csv file which contains the predicted core plug classes with their location in pixels along the height of the core image, the estimated depth and source image used for the prediction:
| index | Plug Type | Depth       | Pixel Location | Source Image                  |
|-------|-----------|-------------|----------------|-------------------------------|
|     0 |     hplug | 3701.016613 |           41.0 | images/6407_1_3_3701_3702.jpg |
|     1 |     vplug | 3701.025527 |           63.0 | images/6407_1_3_3701_3702.jpg |
|     2 |      scal | 3701.092180 |          227.5 | images/6407_1_3_3701_3702.jpg |
|     3 |     hplug | 3701.322326 |          795.5 | images/6407_1_3_3701_3702.jpg |
|     4 |     vplug | 3701.663898 |         1638.5 | images/6407_1_3_3701_3702.jpg |
|     5 |      scal | 3702.094194 |          232.0 | images/6407_1_3_3702_3703.jpg |

In order to use the demo, the exported inference graph of the fine-tuned model must be downloaded from the following directory, [Fine-Tuned Model (run4)](https://console.cloud.google.com/storage/browser/full-model/inference-graph-auto-labeling/), and placed inside auto_labeling_demo folder. When this is done, [auto-label Notebook](auto_label_demo/the_auto_label_core_plugs.ipynb) can be run to generate the labels.

In order to generate labels for a new data set: fine-tune the model on a data set using a few hand-labeled examples -> export inference graph -> change path to inference graph in the notebook.
```python
MODEL_NAME = 'path/to/folder_of_exported_inference_graph'

####
