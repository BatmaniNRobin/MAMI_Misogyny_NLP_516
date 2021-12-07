# Install.md
**NOTE**
This notebook could easily be run in Google Colab with no prior setup required, however due to RAM limitations on the free tier, a local setup will be described in detail below.
## Install Virtual Environment
We chose to install conda, specifically in our case miniconda. from 
- https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html

1. Miniconda installers specifically for Linux, we chose python 3.9:
   - https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html
2. in terminal window, run:
   - `bash Miniconda3-latest-Linux-x86_64.sh`
3. Follow the prompts to install to local machine, if unsure of any settings, just accept the defaults.
4. Ensure conda install is added in your path variable:
   - `echo $PATH` to check
   - if not added, use `export PATH=$PATH:/home/user/Miniconda3/bin` or wherever you installed it

## Using Conda
1. If Conda is not activated immediately, run:
   - `conda activate`
2. Once activated, you should be in the Base conda environment, to install all of the packages and dependencies to properly run this notebook, run:
   - `conda env create -f environment.yaml`
3. The previous command will have created a new environment with the proper packages and dependencies, in order to be within the proper environment you will need to run:
   - `conda activate NLP_516`
4. One of the main packages, transformers, needs to be a certain version in order for this to run properly, however Conda's main channels did not have the version available to be downloaded, so you need to specify the channel for where to download it, in this case a very popular open-source community channel, conda-forge, is used and and installed by running:
   - `conda install -c conda-forge transformers==4.12.5`
5. Ensure you have a kernel installed locally that is able to run Jupyter Notebooks, if not, below will be described how to setup VScode to run the notebook
6. (Optional)
   - Install VSCode `apt install vscode`, install Firefox Theme, enable the theme
   - Install Jupyter Notebook Extension, and Pylance Extension
   - an alert may pop up describing that a kernel needs to be installed and recommends ipykernel, hit yes and install.
      - if it does not pop up or it dies or exits while running and you are unable to continue running code, you may need to run it manually with:
      - `conda install ipykernel --update-deps --force-reinstall`
      - change conda env within VSCode via top right section where it says python
7. Also if VSCode starts messing up, sometimes it may just be best to just close the application and reopen it, or change conda environments and change back, or even re-running the previous command
8. If you receive an error with tensorflow, or tokenizers not building successfully, you may need to run this command and rearrange the order of these two import statements, dont know why, dont ask but: 
   - `sudo vim /Users/user/miniforge3/envs/cloud/lib/python3.9/site-packages/tensorflow/python/__init__.py`
   - and make the imports be in this order:
   - `from tensorflow.python import pywrap_tensorflow as _pywrap_tensorflow`
   - `from tensorflow.python.eager import context`

## Run
1. Just hit `run all` when step 1-6 are complete and everything seems to be functional, if any errors occur steps 7-8 may offer some assistance however, these steps were tested on a macbook, and 2 windows machines and none had to go past step 6. Enjoy :)