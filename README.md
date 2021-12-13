# nlp_NER_model

This repository aims to implement Name Entity Recognition (NER) work based on google's pretrained BERT model and BiLSTM-CRF network! 

This mode design is focusing on handling Chinese data from ETNET financial news and lifestyle financial articles. For textual data outside these scopes, e.g. ETNET DIVA and SoIN, etc., pleease retrain the model with relevant corpus.

This project is built on Python3.7 or above

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Input and output of [model deployment](https://github.com/etnetapp-dev/nlp_NER_model/deployment.py)
![](pic/input_output_example.JPG)
 
For deployment, the model take string of sentence with no more than 128 characters as input and return a json of vocabularies (as keys) and corresponding name entities (as values). 

For sentences with more than 128 characters, please split off the sentences by delimiters (e.g. full-stop or comma) or by truncating the characters after the 128th index before imputting procedure.
 
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

#### input of training model in BIO format：
    集 B-ORG
    團 I-ORG
    透 O
    過 O
    收 B-EVENT
    購 I-EVENT
    喜 B-ORG
    力 I-ORG
    啤 B-PRODUCT
    酒 I-PRODUCT
    ， O
    進 O
    行 O
    升 B-EVENT
    級 I-EVENT
    和 O
    多 O
    樣 O
    化 O
    產 B-PRODUCT
    品 I-PRODUCT
    的 O
    需 B-TERM
    求 I-TERM
    將 O
    推 O
    動 O
    平 O
    均 O
    售 O
    價 O
    ， O
    集 B-ORG
    團 I-ORG
    定 O
    位 O
    中 O
    高 O
    檔 O
    啤 B-PRODUCT
    酒 I-PRODUCT
    市 B-J
    場 I-J
    亦 O
    有 O
    助 O
    推 O
    動 O
    盈 B-TERM
    利 I-TERM
    前 I-TERM
    景 I-TERM
    及 O
    毛 B-TERM
    利 I-TERM
    率 I-TERM
    。 O





--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Pre-trained model downloaded and saved
[download_transformers_models_iipynb.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/download_transformers_models_iipynb.ipynb)

### Pretrained model set and relevant file after downloaded
![](pic/pretrain_bert_modelset.JPG)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Model training
The training of BERT-Bi-LSTM-CRF model requires intensive GPU resources, thus, we strongly suggest to use google colab as training platform and please select the GPU instance of in colab before training and download the APEX package in order to speed up the training processing.

For detail, please refer to [bert_bilstm_crf_ner_training.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/blob/master/bert_bilstm_crf_ner_training.ipynb)

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
