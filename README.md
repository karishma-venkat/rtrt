

# Our Data Architecture

## Data Flow Diagram

```mermaid
graph TD;
    
    %% Source Systems %%
    A[Source Systems] -->|S3 API| B(Bulk Upload to S3)

    %% Data Platform %%
    subgraph "Data Platform"
        subgraph "Data Lake"
            C1[Landing Area (S3)]
            C2[Cleansed / Enriched (S3)]
            C3[Analytics / Reporting (S3)]
        end
        
        subgraph "Data Processing"
            D1[AWS Glue]
            D2[AWS Lambda]
        end
        
        subgraph "Data Catalogue & Classification"
            E1[AWS Glue Data Catalog]
        end
    end

    %% Data Flow Connections %%
    B --> C1
    C1 --> D1
    D1 --> C2
    C2 --> D2
    D2 --> C3
    C3 --> E1

    %% Analytical Data Access %%
    subgraph "Analytical Data Access"
        F1[API]
        F2[AWS Athena]
        F3[Redshift (Optional)]
    end

    C3 -->|Processed Data| F1
    F1 --> F2
    F2 --> F3

    %% Target Systems %%
    subgraph "Target Systems"
        G1[Notebooks (Optional)]
        G2[QuickSight]
        G3[Power BI (Optional)]
        G4[Qlik]
    end
    
    F2 -->|Query| G1
    F2 -->|BI Reports| G2
    F3 -->|Reports| G3
    F3 -->|Dashboards| G4

    %% Monitoring & Security %%
    subgraph "Monitoring & Security"
        H1[AWS CloudWatch]
        H2[AWS IAM]
    end

    F2 --> H1
    B --> H2
```
