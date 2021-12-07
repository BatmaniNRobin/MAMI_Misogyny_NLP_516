# MAMI_Misogyny_NLP_516
## Overview
This project is intended as a submission to CodaLab's Task 5: Multimedia Automatic Misogyny Identification (MAMI) (https://competitions.codalab.org/competitions/34175) subtask A a basic task about misogynous meme identification, where a meme should be categorized either as misogynous or not misogynous. This task consists of the identification of misogynous memes, taking advantage of both text and images available as source of information. Our project exclusively looks at processing the text elements for memes. 

## Data
The dataset consists of 10,000 memes and data consolidated on csv file provided on Google Drive. For this natural language processing (NLP) task, the data was split into 85% training, 10% test, and 5% development (validation). 

## Model
### Preprocessing
The following steps were completed for preprocssing the data: remove stop words using NLTK library, get rid of URLs added by free meme generators, get rid of punctuation
### DistilBERT 
This model was used since in literature it was shown to reduces the size of a BERT model by 40%, while retaining 97% of its language understanding capabilities and being 60% faster. Once this was run on the text, then the inputted text was tokenized and generated contextual word embeddings.
### Postprocessing
Since BERT output is not 0 or 1 passed into a decoder that can map to 0 or 1. The neural network passed through was the default in the DistillBERT model that uses a neural network setup called Masked language modeling (MLM), similar to recurrent neural networks and Generative Pre-trained Transformer. When taking a sentence, the model randomly masks 15% of the words in the input then run the entire masked sentence through the model and has to predict the masked words. Cosine embedding loss is used.
### Evaluation
Evalution was completed by running epoches to determine the accuracy and validation scores, then forming a confusion matrix to look at the AUROC, precision, recall and F1 score

## Install

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
| 413 | 100 |
| 116 | 372 |
