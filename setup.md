---
title: Setup
---

## Instructor

**Xiao Liu**: Xiao is a Senior Research Software Engineer at Purdue University’s Rosen Center for Advanced Computing. She has two Masters in Geosciences and a Master in Computer Sciences and Engineering. Her knowledge encompassed GIS, machine learning, and hydrologic modeling.

## Schedule

| **Time**  | **Session**  |
|:---|-------------|
| 1:00 PM | Get Started with GeoAI |
| 2:00 PM | Tools and Setup |
| 3:00 PM | Cases Studies |
| 4:30 PM | Wrap-Up & Discussion |

## Data Sets

Total size of the data set is ~500 MB. If you have enough space in your home directory(use `myquota` to check), you could copy them there. Otherwise, just copy it to scratch directory (note files here will be purge after 60 days of inactivity).

Copy data to your scratch directory:

```sh
rsync -avP /anvil/projects/x-tra250034/data/geoAI $SCRATCH
```
Or copy data to your home directory:

```sh
rsync -avP /anvil/projects/x-tra250034/data/geoAI $HOME
```
