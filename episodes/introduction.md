---
title: "Get Started with GeoAI"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is GeoAI and its typical tasks?
- What are Foundation Models on Geosciences (GFMs)?
- Why we do GeoAI on HPC clusters?
- What are GeoAI datasets and GFMs available on Anvil, and how to use them?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the foundational concepts of GeoAI and tasks
- Demonstrate how AI are applied to geospatial data 

::::::::::::::::::::::::::::::::::::::::::::::::

## 1 Introduction

### 1.1 GeoAI
- Geospatial Artificial Intelligence
- Give AI a "sense of place" and enabling it to understand and analyze the world through a spatial lens
  
### 1.2 Geospatial Data
- Image VS Imagery
- Compared with Image, it has Coordinates Reference System (CRS)—a mapping to real-world locations.
- Imagery: remotely sensed data captured by satellites, aircraft, drones, or other sensors. 

## 2 GeoAI tasks

### 2.1 Supervised Learning Tasks

#### 2.1.1 Classification Problem
- Image Classification
- Object Detection
- Semantic Segmentation
- Instance Segmentation
- Point Cloud Classification


| Tasks | Image Classification | Object Detection | Semantic Segmentation | Instance Segmentation | Point Cloud Classification |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Goal | Assign a single class label to an entire image | Locate and classify specific objects within an image | Classify every pixel in an image into a defined class | Identify, classify, and delineate each individual instance of an object | Assign a class label to every 3D point in a point cloud (e.g., collected via LiDAR). |
| Output | A single label/category (e.g., "Forest," "Urban Area," "Cloudy Image"). | Bounding boxes (rectangles) around each object, plus a class label for each box. | A pixel-wise mask where all pixels belonging to the same class (e.g., "road") have the same color/label, regardless of individual instance. | Pixel-wise masks for each individual object, distinguishing between separate instances of the same class. | A class label for each point (e.g., "Ground," "Building," "Vegetation," "Power Line"). |
| Applications | image cataloging | Counting features (e.g., number of cars, buildings, trees) | Land cover mapping, road network extraction, defining water bodies, crop type classification | counting individual trees/plants | - |




#### 2.2.2 Regression Problem

- Regression (Spatial Prediction)
    - Predicting continuous values at unobserved locations 
    - Based on known spatial patterns and covariates
    - Applications: predicting air quality at a given location, property values, crop yields.
- Time Series Forecasting  
    - Predicting future values of a variable at specific locations
    - Incorporating both temporal trends and spatial dependencies 
    - Applications: forecasting disease spread, traffic congestion, flood events, urban expansion


### 2.2 Unsupervised Learning Tasks
- Spatial Pattern Recognition (Clustering)
    - Grouping similar data points together based on various attributes 
    - Reveal spatial patterns
    - Applications: crime hotspots, disease clusters…
- Anomaly (Outlier) Detection
    - Identifying unusual /abnormal spatial events 
    - Applications: fraud detection, infrastructure monitoring (e.g., unusual traffic flow), or environmental pollution.


## 3 Foundation Models on Geosciences (GFMs)

- Large-scale neural networks that are pre-trained on vast and diverse datasets in a self-supervised or unsupervised manner.
- Massive Pre-training Data
    - Unlike traditional AI models that are trained for a specific task on a limited, labeled dataset, GFMs are trained on enormous, diverse datasets relevant to Earth systems.
- Generalizable Knowledge
    - Through pre-training, GFMs develop a deep understanding of the underlying relationships and patterns within Earth science data. 
    - Allow them to capture complex features that are relevant across different domains and tasks.
- Adaptability 
    - GFM can be "fine-tuned" or adapted to perform specific geoscience tasks with much less new data than would be required for a traditional model. 
    - In some cases, they can even perform tasks with very few (few-shot) or no (zero-shot) new examples.

## 4 Why GeoAI on HPC clusters

### 4.1 Features of HPC clusters better for GeoAI

- Large Storage on HPC clusters
    - Local (mountable)
        - /home
        - /depot 
        - /scratch
        - /tmp
        - /project
    - Indirect Access
        - Fortress (HPSS tape archive)
        - Ceph (S3 Object Storage)
    - Globus endpoint to easily share data
    - /depot or /project for group storage (only one copy of data is necessary)
      
<img width="612" height="343" alt="image" src="https://github.com/user-attachments/assets/f7d6d5ed-0c71-490b-97c2-ee115bbad4d9" />

- Large computational capacity with GPUs
- Centralized GeoAI datasets and Foundation Models on Geosciences that you can directly use

### 4.2 An Demo on Anvil cluster and Mac book

- A typical example of GFMs: 
    - Prithvi-EO-2.0
    - the second generation Earth Observation(EO) foundation model jointly developed by IBM, NASA, and Jülich Supercomputing Centre.
    - https://huggingface.co/ibm-nasa-geospatial/Prithvi-EO-2.0-300M
    - We will demo a crop classification task with Prithvi-EO-2.0 on Anvil
- Training on Anvil for 50 epochs
    - Jupyter notebook—only one GPU can be used: 4101.991409 seconds: 1.13 hours
    - Sbatch job-when use two GPUs: 2366.664293 seconds: 39.4 mins
- Training on my Mac Max for 1 epoch
    - Jupyter notebook: 38 days 13 hours 44 mins

<img width="738" height="21" alt="image" src="https://github.com/user-attachments/assets/fd5c80c3-15dc-4e4f-8542-6854d15cc15f" />



## 5 GeoAI datasets and GFMs available on Anvil

### 5.1 GeoAI datasets available on Anvil

#### 5.1.1 How to check what GeoAI datasets are avaiable on Anvil

<img width="750" height="393" alt="image" src="https://github.com/user-attachments/assets/a7efa472-d554-408b-b616-e8952116a4b9" />

#### 5.1.2 How to use the GeoAI datasets on Anvil

<img width="750" height="478" alt="image" src="https://github.com/user-attachments/assets/34356f02-5c87-422b-8ebd-eab42b8e483c" />
<img width="750" height="224" alt="image" src="https://github.com/user-attachments/assets/a04aaa3f-658d-4dd9-b9d6-e71083f00a1d" />

### 5.2 GFMs available on Anvil

<img width="1063" height="272" alt="image" src="https://github.com/user-attachments/assets/170671ea-4f88-4d67-a7ef-1821238195ac" />

- Check more information on: https://www.rcac.purdue.edu/knowledge/gfms
- Contact rcac-help@purdue.edu if there is a popular GFMs you want to use and is not currently available on HPC Clusters
- We will cover two case studies of Aurora and Prithvi-EO-2.0 in the 3rd Session today!
