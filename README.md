# Data Architecture Flowchart

```mermaid
graph TD;
    A[Source Systems] -->|S3 API| B[Bulk Data Ingestion]
    B --> C[Landing Area (S3)]
    C --> D[Cleansed / Enriched (S3)]
    D --> E[Analytics / Reporting (S3)]

    %% Data Processing %%
    D -->|Process Data| F[AWS Glue & AWS Lambda]
    F --> E

    %% Analytical Data Access %%
    E -->|Query| G[AWS Athena / Redshift (Optional)]
    
    %% Target Systems %%
    G --> H[BI & Analytics Tools]
    H -->|Reports/Dashboards| H1[QuickSight]
    H -->|Reports/Dashboards| H2[Power BI (Optional)]
    H -->|Reports/Dashboards| H3[Qlik]

    %% Monitoring & Security %%
    G --> I[AWS CloudWatch]
    B --> J[AWS IAM]
