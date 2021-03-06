# nlp_NER_model

This repository aims to implement Name Entity Recognition (NER) work based on google's pretrained BERT model and BiLSTM-CRF network! 

The model strucuture is reproduction of this repository : https://github.com/hertz-pj/BERT-BiLSTM-CRF-NER-pytorch

This mode design is focusing on handling Chinese data from ETNET financial news and lifestyle financial articles. For textual data outside these scopes, e.g. ETNET DIVA and SoIN, etc., pleease retrain the model with relevant corpus.

This project is built on Python3.7 or above

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Input and output of [model deployment](https://github.com/etnetapp-dev/nlp_NER_model/deployment.py)
![](pic/input_output_example.JPG)
 
For deployment, the model take string of sentence with no more than 128 characters as input and return a json of vocabularies (as keys) and corresponding name entities (as values). 

For sentences with more than 128 characters, please split off the sentences by delimiters (e.g. full-stop or comma) or by truncating the characters after the 128th index before imputting procedure.
 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### workflow of model training
![](pic/nlp_ner_training.jpg)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 ### workflow of model deployment
![](pic/nlp_ner_deployments.jpg)
 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Name Entity definition
![](pic/ner_desc.JPG)
 
There are 24 defined name entities to training the models and the name entities are designed to capture full semantic meaning of financial related articles. 

User can  modify the name entity categories if the domain application is non-financial text information.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Key dependencies
    python (>= 3.7.9)
    pytorch (>= 1.8) (cpu version for deployment, gpu version for development) (https://pytorch.org/)
    pytorch-crf == 1.2 (https://github.com/statech/pytorchCRF)
    transformers == 4.5.1  (https://github.com/huggingface/transformers)         
    
    
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Preparation of model training
    Convert training dataset into BIO format (B for beginning, I for intermediate, O for omit) shown below
    Download the google's pretained bert model to local folder path by following the command in [download_transformers_models_iipynb.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/download_transformers_models_iipynb.ipynb)

#### input of training model in BIO format???
    ??? B-ORG
    ??? I-ORG
    ??? O
    ??? O
    ??? B-EVENT
    ??? I-EVENT
    ??? B-ORG
    ??? I-ORG
    ??? B-PRODUCT
    ??? I-PRODUCT
    ??? O
    ??? O
    ??? O
    ??? B-EVENT
    ??? I-EVENT
    ??? O
    ??? O
    ??? O
    ??? O
    ??? B-PRODUCT
    ??? I-PRODUCT
    ??? O
    ??? B-TERM
    ??? I-TERM
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? B-ORG
    ??? I-ORG
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? B-PRODUCT
    ??? I-PRODUCT
    ??? B-J
    ??? I-J
    ??? O
    ??? O
    ??? O
    ??? O
    ??? O
    ??? B-TERM
    ??? I-TERM
    ??? I-TERM
    ??? I-TERM
    ??? O
    ??? B-TERM
    ??? I-TERM
    ??? I-TERM
    ??? O

User can use the follow annotation tools to produce your own dataset:
1. https://prodi.gy/features/named-entity-recognition
2. https://github.com/doccano/doccano

Please provide clear definition your own name entity categories before labelling.

For the whole dataset in [data folder](https://github.com/etnetapp-dev/nlp_NER_model/tree/master/data) , the labelling process was taken about 2.5 months to complete.

After data annotation, please split the whole dataset of BIO format into train.txt and dev.txt. By default, the train/dev split is 80%/20%. The ratio can be adjusted according to your requirements.

After split off dataset, please use the the section 7.4 of [bert_bilstm_crf_ner_training.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/bert_bilstm_crf_ner_training.ipynb) which can produce the [label.txt](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/data/labels.txt) by taking input of [train.zip](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/data/train.zip)


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Pre-trained model downloaded and saved
[download_transformers_models_iipynb.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/download_transformers_models_iipynb.ipynb)

### Pretrained model set and relevant file after downloaded
![](pic/pretrain_bert_modelset.JPG)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Model training
The training of BERT-Bi-LSTM-CRF model requires intensive GPU resources, thus, we strongly suggest to use google colab as training platform and please select the GPU instance of in colab before training and download the APEX package in order to speed up the training processing.

For detail, please refer to [bert_bilstm_crf_ner_training.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/bert_bilstm_crf_ner_training.ipynb)

In each epoch of the training process, there are accuracy table of each entity shown below. Please note the accuracy of English entity will be lower than average level given the limited of sample size in training dataset. User can increase the accuracy by providing your own labeled dataset and increasing the portion of English labeled entity in training dataset.

#### Name Entity accuracy of model training
![](pic/model_accuracy_result.JPG)

#### Trained model set and relevant file 
![](pic/train_bert_modelset.JPG)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 
#### Model conversion from fp32 to fp16
[convert_model_to_fp16.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/convert_model_to_fp16.ipynb)

BERT-base is model contains 110M parameters which is large to deploy in production environment with no-GPU resources. To reduce the resource consumption, we adopt post-training quantization technique by changing model precision (from FP32 (32-bit floating point) to P16 (16-bit floating point)) which can compress and speed-up model inferernce speed.

After the change of precision, the model size is reduced from more than ~700M to ~500M.


#### Deployment
[deployment.py](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/deployment.py)
