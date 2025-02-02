```mermaid
graph TD;
    A[Source Systems] -->|Bulk Load| B[S3 API];
    B --> C[Data Lake];
    C -->|Raw Data| D[S3 Landing Area];
    C -->|Cleansed Data| E[S3 Cleansed / Enriched];
    C -->|Analytics Data| F[S3 Analytics / Reporting];

    D -->|Processing| G[AWS Glue];
    E -->|Processing| G;
    F -->|Processing| G;
    G -->|Data Processing| H[AWS Lambda];

    H -->|Cataloging| I[AWS Glue Data Catalog];
    I -->|Data Classification| J[Data Catalogue & Classification];

    J -->|Query & Access| K[AWS Athena];
    K -->|Optional| L[Redshift];

    L -->|Visualization| M[QuickSight];
    L -->|Optional| N[Power BI];
    L -->|Optional| O[Qlik];

    P[AWS Step Functions] -->|Orchestration| G;
    Q[AWS IAM] -->|Access Management| J;
    R[AWS CloudWatch] -->|Monitoring & Alerts| Q;
    
    style A fill:#f9f,stroke:#333,stroke-width:2px;
    style C fill:#bbf,stroke:#333,stroke-width:2px;
    style G fill:#bfb,stroke:#333,stroke-width:2px;
    style J fill:#ffb,stroke:#333,stroke-width:2px;
    style K fill:#fbb,stroke:#333,stroke-width:2px;
