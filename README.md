# Our Data Architecture

## Simple Flowchart

```mermaid
graph TD;
    
    A[Source Systems] -->|S3 API| B(S3 Bulk Load)
    B --> C[Landing Area (S3)]
    C --> D[Cleansed / Enriched Data (S3)]
    D --> E[Analytics / Reporting (S3)]

    E -->|Query| F[AWS Athena]
    E -->|Storage| G[Redshift (Optional)]
    
    F --> H[BI Tools (QuickSight, Power BI, Qlik)]
    G --> H

    E --> I[AWS Lambda & Glue Processing]
    I --> D

    E --> J[AWS CloudWatch (Monitoring)]
