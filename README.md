# MiniConda, BioConda, and Conda Virtual Environments

### Background
1 - [MiniConda](https://docs.anaconda.com/distro-or-miniconda/) is a free minimal installer for conda (compared to Anaconda).

2 - [BioConda](https://bioconda.github.io/) is used to install many packaged related to biomedical research using the conda package manager. 

3 - [Conda Virtual Environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) provide an easy way to create, export, list, remove, and update envs that have different versions of Python (or R) and/or packages installed in them. It is often best-practice to utilize virtual envs during data analysis to try and avoid potential package issues that may arise. 

-------------------------------------------------------------------------------------------------------------------------------------------

### Installing MiniConda on Linux
Navigate to the [MiniConda installation page](https://docs.anaconda.com/miniconda/miniconda-install/) and download the `.sh` installer. The Linux installation is a script that needs to be executed in order to install miniconda. 
```
# Activate the downloaded Linux installer script
$ bash /path/to/file/Miniconda3-latest-Linux=x86_64.sh
## Accept license agreement

# Add conda to the bin to make it executable from any location
$ sudo ln -s /path/miniconda3/bin/conda /usr/local/bin/conda

# Check Conda installation
$ conda --version

# Updating conda
$ conda update conda
```

--------------------------------------------------------------------------------------------------------------------------------------------

### BioConda Configuration
<ins>Note:</ins> BioConda only supports Linux (x86_64 and aarch64/arm64) and macOS (x86_64 and arm64). 

After successfully installing MiniConda, the BioConda channels need to be configured/updated (one-time set-up), which will modify the systems corresponding `~./condarc` file. Here, the order of channel configuration is important, from lowest to highest priority (top=lowest, bottom=highest), and should be followed exactly to avoid potential probelms with solving dependencies
```
# Execute in order
$ conda config --add channels defaults
$ conda config --add channels bioconda
$ conda config --add channels conda-forge
$ conda config --set channel_priority strict
```
+ The `defaults` channel is the one set by default in a new installation of `conda` and should be set to the lowest priority.
+ The `bioconda` channel enables installation of packages.
+ The `conda-forge` channel enables installation of general purpose packages.
+ The command `conda config --set channel_priority strict` avoids cryptic errors when trying to install and ensures that the channel priority configured above is respected when solving dependencies.

Now, `conda` should be able to install and use any of the [BioConda packages](https://bioconda.github.io/conda-package_index.html).

---------------------------------------------------------------------------------------------------------------------------------------

### Conda Virtual Envs
#### With Python 

```
# Create an environment with a specific version of Python
$ conda create -n myenv python=3.9

# Activate the environment
$ conda activate myenv
```
When activated the conda env name should now be displayed next to the prompt in the terminal (`(myenv)$`). 
<ins>Note:</ins> If the error `CondaError: Run "conda init" before "conda activate"`, then try restarting the terminal and reactivating the conda env to try and resolve the issue. 

<ins>Basic conda env commands:</ins> 
```
# Install packages with conda
(myenv)$ conda install scipy

# Install packages with pip
(myenv)$ pip install scipy

# Determine current environment
$ conda info --envs
## The current env will be highlighted with an asterisk

# View list of envs
$ conda env list

# View list of packages in an env
$ conda list -n myenv
(myenv)$ conda list

# Removing an environment
$ conda remove --name myenv --all
$ conda remove --name 

# Deactivate the environment when finished
$ conda deactivate 
```












