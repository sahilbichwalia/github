```mermaid
flowchart TD
    %% External Entities (Soft rectangles)
    extCustomer(["Customer"]):::entity
    extAdmin(["Administrator"]):::entity
    extBureau(["Credit Bureau"]):::entity

    %% Processes (Rounded rectangles)
    P1(["1.0 Upload Data"]):::process
    P2(["2.0 Process Data"]):::process
    P3(["3.0 Generate Predictions"]):::process
    P4(["4.0 Classify Priority"]):::process

    %% Data Stores (Open-ended rectangles)
    D1[[XGBoost Model Store]]:::store
    D2[[Credit Data Table]]:::store
    D3[[Application Table]]:::store
    D4[[Prediction Results Table]]:::store
    D5[[Priority Class Table]]:::store

    %% Data Flows
    extCustomer -->|CSV/Manual Form| P1
    P1 -->|Raw Data| D3
    P1 -->|Confirmation| extCustomer
    D2 -->|Historical Credit Data| P2
    D3 -->|Application Data| P2
    P2 -->|Preprocessed Data| P3
    P2 -->|Validation Report| extAdmin
    D1 -->|Model| P3
    P3 -->|Predictions| D4
    P3 -->|Risk Probabilities| P4
    P4 -->|Classified Priority| D5
    P4 -->|Risk Assessment| extCustomer
    P4 -->|Analytics Report| extAdmin
    D5 -->|Priority Info| extCustomer

    %% Styles
    classDef process fill:#fdd,stroke:#333,stroke-width:1px
    classDef entity fill:#fdebd0,stroke:#333,stroke-width:1px
    classDef store fill:#fdf2d0,stroke:#333,stroke-width:1px
