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

## 2. Logging In to HPC Clusters

Once your account([Access Anvil](https://www.rcac.purdue.edu/knowledge/anvil/access/obtaining_an_account)) is ready on regular RCAC HPC clusters, there are three ways for lgging in: the SSH (Secure Shell), ThinLinc, and Open OnDemand. The SSH and ThinLinc use SSH keys, which takes more steps to set up, thus we will use Open OnDemand for online workshop exercises, feel free to try the SSH and ThinLinc by yourself offline.  

### 2.1 Open OnDemand on Anvil

(1) Go to https://ondemand.anvil.rcac.purdue.edu/ and log in with your ACCESS account.

(2) Click Clusters -> Anvil Shell ACCESS to open a terminal as pictures below show.

<img width="750" height="140" alt="image" src="https://github.com/user-attachments/assets/b3e0e20c-ce62-49a0-b7b4-8d53466754f8" />

<img width="741" height="769" alt="image" src="https://github.com/user-attachments/assets/771c373d-41af-4083-b89c-deef51712f7a" />

:::::::::::::::: spoiler

### Note

you could find your Anvil username here if you don't know it. For the example here, my Anvil username is `x-xliu26`, while my ACCESS username is `xliu26`.

::::::::::::::::::::::::

### 2.2 ThinLinc Desktop on Anvil

(1) You need set up SSH Key first via Open OnDemand, the detailed steps are here: https://www.rcac.purdue.edu/knowledge/anvil/access/login/sshkeys

(2) Download the [ThinLinc Client](https://www.cendio.com/thinlinc/download/) and install it to your Laptop.

(3) Open ThinLinc Client, then go to Options -> Security, and select "Public key" in the "Anthentication method" as here:
  
   <img width="514" alt="Screenshot 2025-02-21 at 2 27 31 PM" src="https://github.com/user-attachments/assets/1e3e6a5b-8882-4546-b1e3-de313743ad61" />
   
(4) Input Server, Anvil Username and Key(correct it with your path of key) like here:
   
  <img width="474" height="289" alt="image" src="https://github.com/user-attachments/assets/19be22fc-b29c-4cb0-8ee9-90d09a611879" />

   
(5) Hit "Connect".

### 2.3 With SSH on Anvil

Anvil accepts standard SSH connections with public keys-based authentication to anvil.rcac.purdue.edu using your Anvil username:

```localhost$ ssh -l my-x-anvil-username anvil.rcac.purdue.edu```

:::::::::::::::: spoiler
### Note

Your Anvil username is not the same as your ACCESS username (although it is derived from it). Anvil usernames look like x-ACCESSusername or similar, starting with an x-.

Password-based authentication is not supported on Anvil (in favor of SSH keys). There is no "Anvil password", and your ACCESS password will not be accepted by Anvil's SSH either. SSH keys can be set up from the [Open OnDemand interface](ondemand.anvil.rcac.purdue.edu) on Anvil. Please follow [the steps in Setting up SSH keys](https://www.rcac.purdue.edu/knowledge/anvil/access/login/sshkeys) to add your SSH key on Anvil.

::::::::::::::::::::::::

## 3. Install Tools

### 3.1 Install on HPC Cluster Anvil

Open a Terminal with either way of SSH, Open Ondemand or ThinLinc, and follow the steps below.

(1) Install the tools in your `$SCRATCH` directory


```cd $SCRATCH```  

:::::::::::::::: spoiler

### Note

On this workshop, you will install the tools in `$SCRATCH` for practicing. But for real case use, you should install it into the app subdirectory of your project directory, since storage in `$SCRATCH` will be purged in 30 days without access.

::::::::::::::::::::::::


(2) Load necessary modules, including `conda` and `cuda`


```module load modtree/gpu conda cuda/12.0.1```


(3) Create and activate the conda environment 

```conda create -p ./conda_env/geoai_env python=3.12```

```conda activate ./conda_env/geoai_env```

```(/anvil/scratch/x-xliu26/conda_env/geoai_env) x-xliu26@login05.anvil:```

(4) Install tools

```pip install terratorch```

```conda list terratorch```

```
# packages in environment at /anvil/scratch/x-xliu26/conda_env/geoai_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                    pypi_0    pypi
```
`terratorch` automatically include `torchgeo`: ```conda list torchgeo```

```
# packages in environment at /anvil/scratch/x-xliu26/conda_env/geoai_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

(5) Build a kernel for jupyter notebook

```conda install ipykernel```

```ipython kernel install --user --name=geoai_env_kernel```

Installed kernelspec geo_env_kernel in /home/x-xliu26/.local/share/jupyter/kernels/geoai_env_kernel


### 3.2 Install on HPC Cluster Gautschi

(1) Install the tools in your `$SCRATCH` directory.

:::::::::::::::: spoiler

### Note

Storage in `$SCRATCH` will be purged in 30 days without access; they need to backup to your depot space with `sync` command. Each faculty at Purdue can get free 100 GB for their group to use with submitting an order [here](https://www.rcac.purdue.edu/orders/products?category=3).

::::::::::::::::::::::::

```cd $SCRATCH```


(2) Load necessary modules, including `conda` and `cuda`


```module load conda cuda/12.6.0```

(3) Create and activate the conda environment 

```conda create -p ./geoai_env python=3.12```


```conda activate ./geoai_env```


```(/scratch/gautschi/liu4201/geoai_env) liu4201@login03.gautschi:```

(4) Install tools

```pip install terratorch```

```# packages in environment at /scratch/gautschi/liu4201/geoai_env:
#
# Name                    Version                   Build  Channel
terratorch                1.1                     pypi_0    pypi
```
`terratorch` automatically include `torchgeo`: ```conda list torchgeo```

```# packages in environment at /scratch/gautschi/liu4201/geoai_env:
#
# Name                    Version                   Build  Channel
torchgeo                  0.7.0                    pypi_0    pypi 
```

(5) Build a kernel for jupyter notebook

```conda install ipykernel```

```ipython kernel install --user --name=geoai_env_kernel```

```Installed kernelspec geo_env_kernel in /home/liu4201/.local/share/jupyter/kernels/geo_env_kernel```

Open a new Terminal
```ssh h000 -L 8888:localhost:8888```


