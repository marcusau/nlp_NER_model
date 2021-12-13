# nlp_NER_model


#### Each of data source folders contain four key scripts:
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

#### Each of data source folders contain four key scripts:
    source_api.py  (structure requests function of external APIs in python scope)
    schema.py (contains object-oriented (OOP) data model structure of data incoming from external APIs)
    db_table.py ( contains tables' structure and relationship of mysql db in term of python scope)
    CRUD.py  ( contains data-fetch functions of external APIs and Data I/O functions between modules and SQLDB )
