---
title: "Case Studies"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you use the tools you installed on [last sesssion](https://rcac-geo.github.io/workshop-geoAI/tools.html#install-tools) for your geoAI tasks
- How do you use GFMs available on Anvil for your tasks

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- A Case study of a single-task model with TorchGeo
- A Case study of GFMs with TerraTorch: Prithvi-EO-2.0
- A Case study of GFMs: Aurora

::::::::::::::::::::::::::::::::::::::::::::::::

## 1. A Case study of a single-task model with TorchGeo

### 1.1 Interactive Job

#### 1.1.1 Start interactive job and jupyter notebook

#### 1.1.2 Copy the code below and run them cell by cell 

## 2. A Case study of GFMs with TerraTorch: Prithvi-EO-2.0

### 2.1 Load Prithvi-EO-2.0 Model

```
module load gfms
module load Prithvi-EO-2.0/300M-TL-2025-03-24
```

### 2.2 Sbatch Job

(1) Prepare Jobscript

(2) Submit job and check status & output

### 2.3 Interactive Job

(1) Load modules:

```
module load modtree/gpu cuda/12.0.1 conda

module load datasets
module load geoai/multi-temporal-crop-classification

module load gfms
module load Prithvi-EO-2.0/300M-TL-2025-03-24
module load jupyter
```
(2) Get GPU jobs:

```
sinteractive -A tra250034-gpu -N1 -c32 -p gpu --gpus-per-node=1 -t 30:00
```
you will see the information which means the GPU node is ready to use as below:

```
salloc: job allocation 14571723
salloc: job 14571723 queued and waiting for resources
salloc: job 14571723 has been allocated resources
salloc: Granted job allocation 14571723
salloc: Waiting for resource configuration
salloc: Nodes g007 are ready for job
```

(3) Open jupyter notebook and Use the Kernel you built in last session

- start jupyter notebook by running
  
```jupyter notebook``` in the terminal

- Select the kernel you built in last session (`geo_env` for the give example) from the kernel list, after jupyter notebook is up.


(4) run cell by cell in `terratorch_gfms_case.ipynb` 

It will take ~15 mins to train 10 epochs. You could reduce `EPOCHS = 10` in cell 3 to save more time, or increase it after the workshop to achieve better performance when more GPUs are available. 


(5) you could check the GPU usage with running the commands below in a new terminal:

Based on `salloc: Nodes g007 are ready for job`, you will go to check on `g007` as below. Please change it if yours is different.

```
x-xliu26@login06.anvil:[~] $ ssh g007

x-xliu26@g007.anvil:[~] $ nvidia-smi
Mon Dec  8 14:14:56 2025       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 560.35.03              Driver Version: 560.35.03      CUDA Version: 12.6     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA A100-SXM4-40GB          On  |   00000000:C1:00.0 Off |                    0 |
| N/A   42C    P0            367W /  400W |   16989MiB /  40960MiB |     91%      Default |
|                                         |                        |             Disabled |
+-----------------------------------------+------------------------+----------------------+
                                                                                         
+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A   2195239      C   ...pp/conda_env/geo_env/bin/python3.12      16978MiB |
```


## 3. A Case study of GFMs: Aurora

### 3.1 Load Aurora Model

```
module load gfms
module load Aurora
```

### 3.2 Interactive Job

(1) Start interactive job

```
module load jupyter
module load gfms
module load Aurora
```
```
sinteractive -A tra250034 -N1 -c128 -p wholenode -t 30:00
```

(2) Open jupyter notebook and Use the Centralized Aurora Kernel

- start jupyter notebook by running
  
```jupyter notebook``` in the terminal

- Select `gfms_aurora` from the kernel list, after jupyter notebook is up.

::::::::::::::::::::::::::::::::::::: callout

Note the module jupyter must be loaded before Aurora to have the `gfms_aurora` kernel to be found. 

::::::::::::::::::::::::::::::::::::::::::::::::

(3) run cell by cell in `gfm_aurora-cpu.ipynb`




::::::::::::::::::::::::::::::::::::: exercise 

#### Which categories of task/problem mentioned in the first session do these three cases belong to?

:::::::::::::::::::::::: solution 

1 & 2: Classfication Problem-Semantic Segmentation

3: Regression Problem-Time Series Forecasting  

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::
