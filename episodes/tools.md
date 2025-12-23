---
title: "Install Tools for GeoAI on HPC"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What tools do you need for your geoAI tasks?
- How to do install the tools for HPC?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain tools for GeoAI tasks
- Demonstrate how to install GeoAI tools on your HPC account

::::::::::::::::::::::::::::::::::::::::::::::::
## 1. Tools for GeoAI

### 1.1 TorchGeo

- A PyTorch library specifically designed for geospatial data.
    - For GeoAI tasks
    - Handle satellite imagery, aerial photos, and other geographically referenced data.
- https://torchgeo.readthedocs.io/en/stable/tutorials/torchgeo.html

### 1.2 TerraTorch

- A fine-tuning and benchmarking toolkit for Geospatial Foundation Models. 
- Built on top of PyTorch Lightning and TorchGeo.
    - Uses TorchGeo for dataset management and extends the framework to provide a higher-level abstraction for fine-tuning and benchmarking.
    - Streamlines the process of fine-tuning large pre-trained geospatial models for specific tasks. 
- https://terrastackai.github.io/terratorch/stable/

## 2. Install Tools

### 2.1 Install on HPC Cluster Anvil

(1) Install the tools in your `$PROJECT` directory


```cd $PROJECT```  


(2) Load necessary modules, including `conda` and `cuda`


```module load modtree/gpu conda cuda/12.0.1```


(3) Create and activate the conda environment 

```conda create -p ./app/conda_env/geo_env python=3.12```

```conda activate ./geo_env```

```(/anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env) x-xliu26@login05.anvil:```

(4) Install tools

```pip install terratorch```

```conda list terratorch```

```
# packages in environment at /anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                    pypi_0    pypi
```
`terratorch` automatically include `torchgeo`: ```conda list torchgeo```

```
# packages in environment at /anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

(5) Build a kernel for jupyter notebook

```conda install ipykernel```

```ipython kernel install --user --name=geo_env_kernel```

Installed kernelspec geo_env_kernel in /home/x-xliu26/.local/share/jupyter/kernels/geo_env_kernel


Now Open thinLinc Desktop and open a Terminal
```sinteractive -A nairrtest-ai -p ai -N1 -n7 --gpus-per-node=1 -t 1:00:00```

```
salloc: Pending job allocation 13972179
salloc: job 13972179 queued and waiting for resources
salloc: job 13972179 has been allocated resources
salloc: Granted job allocation 13972179
salloc: Waiting for resource configuration
salloc: Nodes g006 are ready for job

x-xliu26@h001.anvil:[~] $ 
```

```module load jupyter```
```jupyter notebook```
copy and paste the url to webpage

Open a new Terminal
```ssh h000 -L 8888:localhost:8888```

### 2.2 Install on HPC Cluster Gautschi

(1) Install the tools in your `$SCRATCH` directory (Note: storage in `$SCRATCH` will be purged in 30 days without access; they need to backup to your depot space with `sync` command)


```cd $SCRATCH```


(2) Load necessary modules, including `conda` and `cuda`


```module load conda cuda/12.6.0```

(3) Create and activate the conda environment 

```conda create -p ./geo_env python=3.12```


```conda activate ./geo_env```


```(/scratch/gautschi/liu4201/geo_env) liu4201@login03.gautschi:```

(4) Install tools

```pip install terratorch```

```# packages in environment at /scratch/gautschi/liu4201/geo_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                     pypi_0    pypi
```
`terratorch` automatically include `torchgeo`: ```conda list torchgeo```

```# packages in environment at /scratch/gautschi/liu4201/geo_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

(5) Build a kernel for jupyter notebook

```conda install ipykernel```

```ipython kernel install --user --name=geo_env_kernel```

```Installed kernelspec geo_env_kernel in /home/liu4201/.local/share/jupyter/kernels/geo_env_kernel```



Now Open thinLinc Desktop and open a Terminal
```sinteractive -A rcac -p ai -N1 -n14 --gpus-per-node=1 -t 5:00:00```

```
salloc: Granted job allocation 1119021
salloc: Waiting for resource configuration
salloc: Nodes h000 are ready for job

liu4201@h000.gautschi:[~] $
```

```module load jupyter```
```jupyter notebook```
copy and paste the url to webpage

Open a new Terminal
```ssh h000 -L 8888:localhost:8888```


