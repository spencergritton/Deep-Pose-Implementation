# Implementation of [Deep Pose](https://openaccess.thecvf.com/content_cvpr_2014/papers/Toshev_DeepPose_Human_Pose_2014_CVPR_paper.pdf)

# Introduction
This repository contains an implementation of stage one of the Deep Pose. This network was proposed by ‪Alexander Toshev et al. in 2014 as one of the first deep learning based approaches to human pose estimation. We (my partner Ashwin Gupta and myself) perform this implementation utilizing the Microsoft Common Objects in Context (COCO) dataset. This work was completed as the final project of a graduate course in computer vision at the University of Michigan in 2021. 

# Human Pose Estimation
Human Pose Estimation identifies and classifies the poses of human body parts and joints in images, videos, or through other computer vision input sources. In general, pose estimation is used to represent and infer human body poses in 2D and/or 3D space. Below is an example image (taken from this project) where a person has had their joints labelled and represented in a way that is easy to visualize.

![Example Pose](docs/example-pose.png)

# Deep Pose Model
As mentioned above, the Deep Pose model was one of the first deep learning based approaches to human pose estimation. This network takes as input a 224x224 RBG image and outputs normalized (x, y) coordinates along with a visibility value for 17 separate joints labelled in the COCO dataset. For further information on the Deep Pose model, please see the [Deep Pose Paper](https://openaccess.thecvf.com/content_cvpr_2014/papers/Toshev_DeepPose_Human_Pose_2014_CVPR_paper.pdf).

# Implementation Details
Our implementation differs from the original Deep Pose implementation in a few key areas:
- Due to limited computing resources (student budgets) we implement only stage-one of the Deep Pose model. Stage-one is the same model as the other Deep Pose stages, it simply lacks the iterative refinement process described in the Deep Pose paper, which is significantly more computationally expensive (the authors state training stage-two and stage-three took 7 days each with 100 GPUs).
- We include a visibility output attached to each keypoint marking it as either in the image or not. The original authors do not describe their handling of keypoints not visible in the images.
- We include batch normalization to improve model performance given our lack of training resources.
- Finally, the original authors utilize the Leeds Sports Dataset, whereas we use COCO.

For further implementation details, see our write-up on this project ![here](Project-Report.pdf).

# This Repository
This repository is primarily a host of our code — which is separated into two separate jupyter notebooks, a [dataset generator](dataset-generator.ipynb) and the [pose estimation network](pose-estimator.ipynb).

The *dataset generator* is used to:
1. Download the COCO dataset
2. Extract relevant keypoint annotated images
3. Normalize, transform, and scale images and their associated keypoints
4. Break the data into training and testing sections
5. Export the data to a compact format utilized by the *pose estimation model*

The *pose estimator*:
1. Creates relevant PyTorch models for the data
2. Unpacks the data from the dataset generator and applies data augmentations
3. Implements the Deep Pose network in PyTorch
4. Trains the Deep Pose model
5. Evaluates the Percentage of Correct Parts (PCP) accuracy of the model

# Run the Code
Our code is broken into two separate jupyter notebooks, a [dataset generator](dataset-generator.ipynb) and the [pose estimation network](pose-estimator.ipynb). To run these notebooks perform the following:

**Install Python 3 and Jupyter Notebook**  
I'll leave you to do this yourself.

**Install Required Dependencies**  
``pip3 install -r requirements.txt``

**Run the Code**  
Each jupyter notebook should be setup to run and with (hopefully) adequate comments to describe the contents of the code.
