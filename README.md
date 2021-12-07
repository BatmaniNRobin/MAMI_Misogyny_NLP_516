# MAMI_Misogyny_NLP_516
## Authors
Mohammad Malik and Adair Maynard Group Project for CMSC 516: Natural Language Processing at Virginia Commonwealth University.
## Overview
This project is intended as a submission to CodaLab's Task 5: Multimedia Automatic Misogyny Identification (MAMI) (https://competitions.codalab.org/competitions/34175) subtask A a basic task about misogynous meme identification, where a meme should be categorized either as misogynous or not misogynous. This task consists of the identification of misogynous memes, taking advantage of both text and images available as source of information. Our project exclusively looks at processing the text elements for memes. 

## Data
The dataset consists of 10,000 memes and data consolidated on csv file provided on Google Drive. For this natural language processing (NLP) task, the data was split into 85% training, 10% test, and 5% development (validation). 

## Model
### Preprocessing
The following steps were completed for preprocssing the data: remove stop words using NLTK library, get rid of URLs added by free meme generators, get rid of punctuation.
### DistilBERT 
This model was used since in literature it was shown to reduces the size of a BERT model by 40%, while retaining 97% of its language understanding capabilities and being 60% faster. Once this was run on the text, then the inputted text was tokenized and generated contextual word embeddings.
### Postprocessing
Since BERT output is not 0 or 1 passed into a decoder that can map to 0 or 1. The neural network passed through was the default in the DistillBERT model that uses a neural network setup called Masked language modeling (MLM), similar to recurrent neural networks and Generative Pre-trained Transformer. When taking a sentence, the model randomly masks 15% of the words in the input then run the entire masked sentence through the model and has to predict the masked words. Cosine embedding loss is used.
### Evaluation
Evalution was completed by running epoches to determine the accuracy and validation scores, then forming a confusion matrix to look at the AUROC, precision, recall and F1 score.

## Install
**NOTE**
This notebook could easily be run in Google Colab with no prior setup required, however due to RAM limitations on the free tier, a local setup will be described in detail below.
### Install Virtual Environment
We chose to install conda, specifically in our case miniconda. from 
- https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html

1. Miniconda installers specifically for Linux, we chose python 3.9:
   - https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html
2. if installing from source, in terminal window, run:
   - `bash Miniconda3-latest-Linux-x86_64.sh`
   otherwise begin and run the installer and ensure that the `add to path` checkbox is checked, also the method for Windows machines.
3. Follow the prompts to install to local machine, if unsure of any settings, just accept the defaults.
4. Ensure conda install is added in your path variable:
   - `echo $PATH` to check
   - if not added, use `export PATH=$PATH:/home/user/Miniconda3/bin` or wherever you installed it

### Using Conda
1. If Conda is not activated immediately, run:
   - `conda activate`
2. Once activated, you should be in the Base conda environment, to install all of the packages and dependencies to properly run this notebook, run:
   - `conda env create -f environment.yml`
3. The previous command will have created a new environment with the proper packages and dependencies, in order to be within the proper environment you will need to run:
   - `conda activate NLP_516`
4. One of the main packages, transformers, needs to be a certain version in order for this to run properly, however Conda's main channels did not have the version available to be downloaded, so you need to specify the channel for where to download it, in this case a very popular open-source community channel, conda-forge, is used and and installed by running:
   - `conda install -c conda-forge transformers==4.12.5`
5. Ensure you have a kernel installed locally that is able to run Jupyter Notebooks, if not, below will be described how to setup VScode to run the notebook
### Install VSCode
1. (Optional)
   - Install VSCode `apt install vscode`, install Firefox Theme, enable the theme
   - Install Jupyter Notebook Extension, and Pylance Extension
   - an alert may pop up describing that a kernel needs to be installed and recommends ipykernel, hit yes and install.
      - if it does not pop up or it dies or exits while running and you are unable to continue running code, you may need to run it manually with:
      - `conda install ipykernel --update-deps --force-reinstall`
2. Also if VSCode starts messing up, sometimes it may just be best to just close the application and reopen it, or change conda environments and change back, or even re-running the previous command
3. If you receive an error with tensorflow, or tokenizers not building successfully, you may need to run this command and rearrange the order of these two import statements, dont know why, dont ask but: 
   - `sudo vim /Users/user/miniforge3/envs/cloud/lib/python3.9/site-packages/tensorflow/python/__init__.py`
   - and make the imports be in this order:
   - `from tensorflow.python import pywrap_tensorflow as _pywrap_tensorflow`
   - `from tensorflow.python.eager import context`

## Results
| Measure | Value |
| ----------- | ----------- |
| Accuracy | 78.42% |
| Precision | 78.81% |
| Recall | 76.23% |
| F1 | 77.50% |
| Cohen’s kappa | 56.78% |
| AUROC | 86.15% |


### Confusion Matrix
![image](https://user-images.githubusercontent.com/63976253/144958864-5f36c8d2-37df-41cb-a10d-f6ed4186f2b4.PNG)


