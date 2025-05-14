```mermaid
flowchart TD
    %% External Entities
    customer["Customer"]
    admin["Administrator"]
    bureau["Credit Bureau"]

    %% Processes
    p1(["1.0 Upload Data"])
    p2(["2.0  Process Data"])
    p3(["3.0 Generate Predictions"])
    p4(["4.0 Classify Priority"])

    %% Data Stores
    d1[[D1 XGBoost Model Store]
    d2[[D2  Credit Data Table]]
    d3[[D3 Application Table]]
    d4[[D4 Prediction Results Table]]
    d5[[D5 Priority Classification Table]]

    %% Data Flows
    customer -->|Upload CSV / Manual Data| p1
    p1 -->|Raw Application Data| d3
    p1 -->|Confirmation| customer
    d2 -->|Historical Credit Data| p1
    d3 -->|Application Data| p2

    p2 -->|Preprocessed Data| p3
    p2 -->|Validation Report| admin
    p2 -->|Transformed Features| p3
    d1 -->|ML Model| p3

    p3 -->|Predictions| d4
    p3 -->|Risk Probabilities| p4

    p4 -->|Classified Priority| d5
    p4 -->|Risk Assessment Results| customer
    p4 -->|Analytics Report| admin
    d5 -->|Priority Info| customer
