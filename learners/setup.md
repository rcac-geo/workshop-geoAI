---
title: Setup
---

FIXME: Setup instructions live in this document. Please specify the tools and
the data sets the Learner needs to have installed.

## Data Sets

<!--
FIXME: place any data you want learners to use in `episodes/data` and then use
       a relative link ( [data zip file](data/lesson-data.zip) ) to provide a
       link to it, replacing the example.com link.
-->
Download the [data zip file](https://example.com/FIXME) and unzip it to your Desktop

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details

Setup for different systems can be presented in dropdown menus via a `spoiler`
tag. They will join to this discussion block, so you can give a general overview
of the software used in this lesson here and fill out the individual operating
systems (and potentially add more, e.g. online setup) in the solutions blocks.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

Use PuTTY

::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS

Use Terminal.app

::::::::::::::::::::::::


:::::::::::::::: spoiler

### HPC Cluster Anvil
```cd $PROJECT``` 

```module load modtree/gpu conda cuda/12.0.1```

```conda create -p ./geo_env python=3.12```

```conda activate ./geo_env```

```(/anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env) x-xliu26@login05.anvil:```

```pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121```
Installing torch with cuda before terratorch made sure the torch you installed is the version with GPU enabled.

```pip install terratorch```
```conda list terratorch```

```
# packages in environment at /anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                    pypi_0    pypi
```
`terratorch` automatically include `torchgeo`

```
# packages in environment at /anvil/projects/x-asc170016/x-xliu26/app/conda_env/geo_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

```conda install ipykernel```
```ipython kernel install --user --name=geo_env_kernel```

Installed kernelspec geo_env_kernel in /home/x-xliu26/.local/share/jupyter/kernels/geo_env_kernel

::::::::::::::::::::::::

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

### HPC Cluster Gautschi
```cd $SCRATCH```

```module load conda cuda/12.6.0```

```conda create -p ./geo_env python=3.12```

```conda activate ./geo_env```

```(/scratch/gautschi/liu4201/geo_env) liu4201@login03.gautschi:```

```pip3 install torch torchvision --index-url https://download.pytorch.org/whl/cu126```
Installing torch with cuda before terratorch made sure the torch you installed is the version with GPU enabled.

```pip install terratorch```
```conda list torchgeo```

```# packages in environment at /scratch/gautschi/liu4201/geo_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                     pypi_0    pypi
```
`terratorch` automatically include `torchgeo`

```# packages in environment at /scratch/gautschi/liu4201/geo_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

```conda install ipykernel```
```ipython kernel install --user --name=geo_env_kernel```

```Installed kernelspec geo_env_kernel in /home/liu4201/.local/share/jupyter/kernels/geo_env_kernel```

::::::::::::::::::::::::

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

