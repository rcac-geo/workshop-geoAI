---
title: "Get Started with GeoAI"
teaching: 10
exercises: 2
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

## Introduction

### GeoAI
- Geospatial Artificial Intelligence
- Give AI a "sense of place" and enabling it to understand and analyze the world through a spatial lens
### Geospatial Data
- Image VS Imagery
- Compared with Image, it has Coordinates Reference System (CRS)—a mapping to real-world locations.
- Imagery: remotely sensed data captured by satellites, aircraft, drones, or other sensors. 

## GeoAI tasks

### Supervised Learning Tasks
#### Classification Problem
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




#### Regression Problem

- Regression (Spatial Prediction)
    - Predicting continuous values at unobserved locations 
    - Based on known spatial patterns and covariates
    - Applications: predicting air quality at a given location, property values, crop yields.
- Time Series Forecasting  
    - Predicting future values of a variable at specific locations
    - Incorporating both temporal trends and spatial dependencies 
    - Applications: forecasting disease spread, traffic congestion, flood events, urban expansion


### Unsupervised Learning Tasks
- Spatial Pattern Recognition (Clustering)
    - Grouping similar data points together based on various attributes 
    - Reveal spatial patterns
    - Applications: crime hotspots, disease clusters…
- Anomaly (Outlier) Detection
    - Identifying unusual /abnormal spatial events 
    - Applications: fraud detection, infrastructure monitoring (e.g., unusual traffic flow), or environmental pollution.


## Foundation Models on Geosciences (GFMs)
## Why GeoAI on HPC clusters
## GeoAI datasets and GFMs available on Anvil

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Inline instructor notes can help inform instructors of timing challenges
associated with the lessons. They appear in the "Instructor View"

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Can you do it?

What is the output of this command?

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::: solution 

## Output
 
```output
[1] "This new lesson looks good"
```

:::::::::::::::::::::::::::::::::


## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::::::::::::::


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
