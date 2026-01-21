---
title: "Case Studies"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you use the tools you installed on [last sesssion](https://rcac-geo.github.io/workshop-geoAI/tools.html#install-tools) for your geoAI tasks?
- How do you use GFMs available on Anvil for your tasks?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- A Case study of a single-task model with TorchGeo
- A Case study of GFMs with TerraTorch: Prithvi-EO-2.0
- A Case study of GFMs: Aurora
- With the three case studies, you will learn three ways to perform GeoAI tasks on HPC: Batch jobs, Interactive jobs via Open OnDemand, and Interactive jobs via ThinLinc.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

Note if you copied the dataset at the [setup session](https://rcac-geo.github.io/workshop-geoAI/index.html#data-sets) to scratch directory, you need to run `cd $SCRATCH` first to change directory. Otherwise if they are at home directory, you are defaulted here and no need for this step of action.
::::::::::::::::::::::::::::::::::::::::::::::::


## 1. A Case study of a single-task model with TorchGeo

### 1.1 Interactive Job on the remote desktop with Open OnDemand 

- With [Open OnDemand](https://ondemand.anvil.rcac.purdue.edu/), click "Desktop" under "Interactive Apps". Input the allocation, Queue, and Wall Time and Cores as the picture below and hit Launch.
<img width="714" height="401" alt="image" src="https://github.com/user-attachments/assets/2d63d165-e063-466b-bec8-7bbc576d5615" />

- The Desktop Session will be queued, and you could click Launch Desktop once it's ready like the picture below. 
  <img width="940" height="272" alt="image" src="https://github.com/user-attachments/assets/4fb0d99d-df90-4285-8a93-33157015ce9b" />
  
- click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below. 


(1) Load modules:

```
module load jupyter
```

(2) Open jupyter notebook and Use the Centralized Aurora Kernel

- start jupyter notebook by running `jupyter notebook` in the terminal

- Select the kernel you built in last session (`geo_env_kernel` for the give example) from the kernel list, after jupyter notebook is up.


(3) run cell by cell in `torchgeo_case-cpu.ipynb`

::::::::::::::::::::::::::::::::::::: callout

Note if GPU is not available, the code is implemented to have just make 1 pass and limit the size of the datasets. You could see the figures of more training with GPU in `torchgeo_case.ipynb`, which has better performance. 

::::::::::::::::::::::::::::::::::::::::::::::::


### 1.2 Interactive Job on the remote desktop with ThinLinc 

With ThinLinc, click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below. 

(1) Load modules:

```
module load jupyter
```

(2) Start interactive job 

```
sinteractive -A tra250034 -N1 -c128 -p wholenode -t 30:00
```
```
salloc: Pending job allocation 14771023
salloc: job 14771023 queued and waiting for resources
salloc: job 14771023 has been allocated resources
salloc: Granted job allocation 14771023
salloc: Waiting for resource configuration
salloc: Nodes a600 are ready for job
```

(3) Open jupyter notebook and Use the Centralized Aurora Kernel

- start jupyter notebook by running
  
```jupyter notebook``` in the terminal

- Select the kernel you built in last session (`geoai_env_kernel` for the give example) from the kernel list, after jupyter notebook is up.


(4) run cell by cell in `torchgeo_case-cpu.ipynb`

::::::::::::::::::::::::::::::::::::: callout

Note if GPU is not available, the code is implemented to have just make 1 pass and limit the size of the datasets. You could see the figures of more training with GPU in `torchgeo_case.ipynb`, which has better performance. 

::::::::::::::::::::::::::::::::::::::::::::::::

## 2. A Case study of GFMs with TerraTorch: Prithvi-EO-2.0

### 2.1 Load Prithvi-EO-2.0 Model

```
module load gfms
module load Prithvi-EO-2.0/300M-TL-2025-03-24
```

### 2.2 Batch Job

(1) Prepare Jobscript

- Build a jobscript `train.gpujob`, for example, you could run the command `vim  train.gpujob` and copy & paste the code below:

```
#!/bin/sh -l
# FILENAME:  myjobsubmissionfile

#SBATCH -A asc170016-gpu
#SBATCH -p gpu # the default queue is "shared" queue
#SBATCH -N 1
#SBATCH -c 32
#SBATCH --gpus-per-node=1
#SBATCH -t 1:30:00
#SBATCH --job-name mgpujob

module load modtree/gpu cuda/12.0.1 conda

module load datasets
module load geoai/multi-temporal-crop-classification

module load gfms
module load Prithvi-EO-2.0/300M-TL-2025-03-24

conda activate $SCRATCH/conda_env/geoai_env
cd ./geoAI  # check the callout note below

python train.py
```
- You will use the `train.py` provided in the workshop, where I have already set the EPOCHS as 10 for shorter time (~15 mins) need. Feel free to reduce it to save more time for this workshop, or increase it to see better performance later.

::::::::::::::::::::::::::::::::::::: callout

Note if you copied the dataset at the [setup session](https://rcac-geo.github.io/workshop-geoAI/index.html#data-sets) to scratch directory, you need to run `cd $SCRATCH/geoAI` to change directory intead of `cd ~/geoAI`. 

::::::::::::::::::::::::::::::::::::::::::::::::

(2) Submit job and check status & output

- submit the job by running `sbatch train.gpujob` in the terminal
- run `squeue --me` in the terminal to check the job status, but note it will return empty after the job finished.
- you could also check the job status by running `jobinfo YOUR_JOB_ID` in the terminal (replace YOUR_JOB_ID with your job id).

### 2.3 Interactive Job on the remote desktop with Open OnDemand 

- With [Open OnDemand](https://ondemand.anvil.rcac.purdue.edu/), click "Desktop" under "Interactive Apps". Input the allocation, Queue, and Wall Time, Cores, and Number of GPUa as the picture below and hit Launch.
<img width="719" height="425" alt="image" src="https://github.com/user-attachments/assets/2938bc00-af2a-4826-93bc-add579988c45" />

- The Desktop Session will be queued, and you could click Launch Desktop once it's ready like the picture below. 
<img width="949" height="271" alt="image" src="https://github.com/user-attachments/assets/e434656d-78c1-4210-97af-6f93dd0b9b46" />
  
- click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below.
  
(1) Load modules:

```
module load modtree/gpu cuda/12.0.1 conda

module load datasets
module load geoai/multi-temporal-crop-classification

module load gfms
module load Prithvi-EO-2.0/300M-TL-2025-03-24
module load jupyter
```

(2) Open jupyter notebook and Use the Kernel you built in last session

- start jupyter notebook by running
  
```jupyter notebook``` in the terminal

- Select the kernel you built in last session (`geoai_env_kernel` for the give example) from the kernel list, after jupyter notebook is up.


(3) run cell by cell in `terratorch_gfms_case.ipynb` 

It will take ~15 mins to train 10 epochs. You could reduce `EPOCHS = 10` in cell 3 to save more time, or increase it after the workshop to achieve better performance when more GPUs are available. 


(4) you could check the GPU usage with running the commands below in a new terminal:

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

### 2.4 Interactive Job on the remote desktop with ThinLinc 

With ThinLinc, click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below. 

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

- Select the kernel you built in last session (`geoai_env_kernel` for the give example) from the kernel list, after jupyter notebook is up.


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

### 3.2 Interactive Job on the remote desktop with Open OnDemand 

- With [Open OnDemand](https://ondemand.anvil.rcac.purdue.edu/), click "Desktop" under "Interactive Apps". Input the allocation, Queue, and Wall Time and Cores as the picture below and hit Launch.
<img width="714" height="401" alt="image" src="https://github.com/user-attachments/assets/2d63d165-e063-466b-bec8-7bbc576d5615" />

- The Desktop Session will be queued, and you could click Launch Desktop once it's ready like the picture below. 
  <img width="940" height="272" alt="image" src="https://github.com/user-attachments/assets/4fb0d99d-df90-4285-8a93-33157015ce9b" />
  
- click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below.
  
(1) Load modules and Start interactive job as below:

```
module load jupyter
module load gfms
module load Aurora
```

(2) Open jupyter notebook and Use the Centralized Aurora Kernel

- start jupyter notebook by running
  
```jupyter notebook``` in the terminal

- Select `gfms_aurora` from the kernel list, after jupyter notebook is up.

::::::::::::::::::::::::::::::::::::: callout

Note the module jupyter must be loaded before Aurora to have the `gfms_aurora` kernel to be found. 

::::::::::::::::::::::::::::::::::::::::::::::::

(3) run cell by cell in `gfm_aurora-cpu.ipynb`

It will take ~5 min to finishi the inference on a whole cpu node. It will be very fast if you request a interactive job with GPU available and run `gfm_aurora-gpu.ipynb`.


### 3.3 Interactive Job on the remote desktop with ThinLinc 

With ThinLinc, click "Terminal Emulator" under "Applications" to open a Terminal and then follow the steps below. 

(1) Load modules and Start interactive job as below:

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

It will take ~5 min to finishi the inference on a whole cpu node. It will be very fast if you request a interactive job with GPU available and run `gfm_aurora-gpu.ipynb`.




::::::::::::::::::::::::::::::::::::: challenge 

#### Which categories of task/problem mentioned in the first session do these three cases belong to?

:::::::::::::::::::::::: solution 

1 & 2: Classfication Problem-Semantic Segmentation

3: Regression Problem-Time Series Forecasting  

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::
