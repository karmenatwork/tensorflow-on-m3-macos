# Tensorflow on a M3 macOS

***Notes***: 
- As of early 2024, TensorFlow has **native support** for Apple Silicon (M1/M2/M3 chips). This means you can run TensorFlow efficiently on your M3 Mac without needing to use Rosetta 2 for translation.

- Installation is simpler now. Apple has worked with the TensorFlow team to create a package called tensorflow-macos, which is optimized for Mac systems with Apple Silicon.

- Metal support. TensorFlow on Mac can use Apple's Metal framework for GPU acceleration, which is optimized for Apple Silicon.

## Before installation

Before anything make sure you have Xcode Command Line tools (Xcode CLT) installed

`xcode-select --install`


Choose based on your [experience.](https://docs.anaconda.com/distro-or-miniconda/)
 
I have followed [conda's tip](https://conda.io/projects/conda/en/latest/user-guide/install/index.html): "If you are just starting out, we recommend installing conda via the Miniconda installer." I just finished an AI/ML bootcamp and since I'm still a bun in the owen, I chose to [download the latest](https://conda.io/projects/conda/en/latest/index.html)
Miniconda installer for macOS with Apple Silicon. Then I followed its instructions.

After the installation is finished, open your ternminal and type the command  `conda`. You will see `(base)` which is the default environment. It's a good idea to have jupyter installed there.  
`(base) ➜  ~ conda install -y jupyter`

## Installation
### Option 1: Install packages one by one on a new environment

#### 1. Create and activate a virtual environment

`conda create -n ENV_NAME`

For example, you can create an environment with a python's version

`conda create -n ENV_NAME python=<version>`

such as: `conda create -n tf python=3.11`

then activate it by doing: 

`conda activate tf`

#### 2. Upgrade pip

`python3 -m pip install --upgrade pip`

#### 3. Install TensorFlow packages
```
python3 -m pip install tensorflow-macos
python3 -m pip install tensorflow-metal
```

### Option 2: Bundling packages on a `yml` file.

Put together a yml file similar to `tensorflow-m3-macos-env.yml`

***Note:***
You do not need to install a specific package called `tensorflow-deps` for running TensorFlow on an M3 Mac as it used to be months ago. In my case, I decided to bundle the packages in a yml file, where I added jupyter notebook and some data science / machine learning packages I use often (pandas numpy matplotlib scikit-learn). Yet, trying to install tensorflow with `python 3.12`didn't work, so I downgraded to `python 3.11`

`conda env create --name tf -f tensorflow-m3-macos-env.yml`

### Create environment

`conda create -n ENV_NAME`

For example, you can create an environment with a python's version

`conda create -n ENV_NAME python=<version>`

such as:  `conda create -n tf python=3.11`, and then to activate run

`conda activate tf`

You will see your current environment in your terminal like `(tf)` .


## Cheat Sheat

**To create an environment, use**

`conda create -n ENV_NAME`

**To activate this environment, use**

`conda activate ENV_NAME`

**To deactivate an active environment, use**

`conda deactivate`

**To remove an environment, deactivate it first and then use**

`conda remove --name ENV_NAME --all`

**To install packages, use**

`conda install <package>`

**To list packages installed in an environment**
`conda list -n ENV_NAME`

Popular packages needed :

`conda install pandas numpy matplotlib scikit-learn`

`conda install -c conda-forge jupyterlab`

`conda install -c conda-forge imbalanced-learn`

## Tips

Everytime you open a new tab in your terminal, it will open with the `(base)` environment by default. If you don't want this to happen.

In the file `.condarc` add

````
channels:
  - defaults
auto_activate_base: false

````