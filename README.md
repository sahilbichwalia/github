```mermaid
flowchart TD
    entity1["Customer"] -- Upload CSV/Excel file --> process2(("1.0\nUpload\nData"))
    entity1 -- Manual input form data --> process2
    process2 -- Raw application data --> datastore4["D3 Application table"]
    process2 -- Confirmation --> entity1
    datastore3["D2 Credit data table"] -- Historical credit data --> process2
    datastore4 -- Application data --> process3(("2.0\nProcess\nData"))
    process3 -- Preprocessed data --> process4(("3.0\nGenerate\nPredictions"))
    entity3["Credit Bureau"] -- Bureau data --> datastore3
    process3 -- Data validation report --> entity2["Administrator"]
    process3 -- Transformed features --> process4
    datastore1["D1 XGBoost model store"] -- ML model --> process4
    process4 -- Risk probabilities --> process5(("4.0\nClassify\nPriority"))
    process4 -- Prediction details updated --> datastore5["D4 Prediction results table"]
    process4 -- Prediction results --> process5
    process5 -- Priority classification --> datastore6["D5 Priority class table"]
    process5 -- Risk assessment results --> entity1
    process5 -- Analytics report --> entity2
    datastore5 -- Prediction results --> process5
    datastore6 -- Priority class details --> entity1
    n1["This is sample label"]
    n1:::note

    classDef process fill:white,stroke:#000,stroke-width:2px
    classDef datastore fill:white,stroke:#000,stroke-width:2px
    classDef entity fill:white,stroke:#000,stroke-width:2px
    classDef note fill:white,stroke:gray,stroke-width:1px

    class process2,process3,process4,process5 process
    class datastore1,datastore3,datastore4,datastore5,datastore6 datastore
    class entity1,entity2,entity3 entity
