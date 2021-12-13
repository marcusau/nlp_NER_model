# nlp_NER_model


#### 输入数据格式请处理成BIO格式，如下：
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

#### Key dependencies
    python (>= 3.7.9)
    pytorch (>= 1.8) (cpu version for deployment, gpu version for development) (https://pytorch.org/)
    pytorch-crf == 1.2 (https://github.com/statech/pytorchCRF)
    transformers == 4.5.1  (https://github.com/huggingface/transformers)         


#### Model training
    [bert_bilstm_crf_ner_training.ipynb](https://github.com/etnetapp-dev/nlp_NER_model/bert_bilstm_crf_ner_training.ipynb)
