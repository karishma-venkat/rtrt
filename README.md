graph TD;
    A[Source Systems] -->|Bulk Data| B(S3 API);
    B --> C[Data Platform];

    subgraph C[Data Platform]
        subgraph D[Data Lake]
            D1[S3 Landing Area] --> D2[S3 Cleansed/Enriched] --> D3[S3 Analytics/Reporting]
        end
        subgraph E[Data Processing]
            E1[AWS Glue] --> E2[AWS Lambda]
        end
        subgraph F[Data Catalogue & Classification]
            F1[AWS Glue Data Catalog]
        end
    end

    C -->|API| G[Analytical Data Access]
    G -->|Querying| H[AWS Athena]
    G -->|Optional| I[Redshift]

    subgraph Target_Systems[Target Systems (Analytics)]
        J[Notebooks (Optional)]
        K[QuickSight]
        L[Power BI (Optional)]
        M[Qlik]
    end

    G --> Target_Systems;

    C -->|Step Functions| N[AWS Step Functions]
    N --> C;

    C -->|Monitoring/Alert| O[AWS CloudWatch]

    P[AWS Identity & Access Management] --> C
