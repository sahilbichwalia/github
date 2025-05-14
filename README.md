```mermaid
flowchart TD
    %% External Entities
    extCustomer([Customer])
    extAdmin([Administrator])
    extBureau([Credit Bureau])

    %% Process 1.0: Upload Data
    subgraph P1["1.0 Upload Data"]
        p1a[1.1 Receive Data]
        p1b[1.2 Store Application Data]
        p1c[1.3 Acknowledge Upload]
    end

    %% Process 2.0: Process Data
    subgraph P2["2.0 Process Data"]
        p2a[2.1 Fetch Historical Credit Data]
        p2b[2.2 Validate Input Data]
        p2c[2.3 Feature Engineering]
    end

    %% Process 3.0: Generate Predictions
    subgraph P3["3.0 Generate Predictions"]
        p3a[3.1 Load Model]
        p3b[3.2 Predict Risk Probability]
        p3c[3.3 Store Prediction]
    end

    %% Process 4.0: Classify Priority
    subgraph P4["4.0 Classify Priority"]
        p4a[4.1 Classify Application]
        p4b[4.2 Send Risk Result to Customer]
        p4c[4.3 Send Analytics to Admin]
    end

    %% Data Stores
    d1[[D1\nXGBoost Model Store]]
    d2[[D2\nCredit Data Table]]
    d3[[D3\nApplication Table]]
    d4[[D4\nPrediction Results Table]]
    d5[[D5\nPriority Classification Table]]

    %% Data Flow for P1
    extCustomer -->|CSV / Manual Form| p1a
    p1a --> p1b
    p1b -->|Application Data| d3
    p1c -->|Upload Confirmation| extCustomer
    p1b --> p1c

    %% Data Flow for P2
    p2a -->|Credit History| d2
    d2 --> p2a
    d3 --> p2b
    p2b --> p2c
    p2c -->|Transformed Data| p3a
    p2b -->|Validation Report| extAdmin

    %% Data Flow for P3
    p3a -->|Model| d1
    d1 --> p3a
    p3a --> p3b
    p3b --> p3c
    p3c -->|Prediction Results| d4
    p3b -->|Risk Score| p4a

    %% Data Flow for P4
    p4a -->|Priority Classification| d5
    p4a --> p4b
    p4a --> p4c
    p4b -->|Risk Status| extCustomer
    p4c -->|Analytics Report| extAdmin
    d5 -->|Priority Info| extCustomer
