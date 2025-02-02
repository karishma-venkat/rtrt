Our Data Architecture

Source Systems
   |
   |--> Bulk (S3 API)
           |
           v
   --------------------------
   |      Data Platform      |
   |  --------------------   |
   |  |      Data Lake   |   |
   |  |-----------------|   |
   |  |  S3 Landing     |   |
   |  |  Area          |   |
   |  |---------------|   |
   |  |  S3 Cleansed  |   |
   |  |  / Enriched   |   |
   |  |---------------|   |
   |  |  S3 Analytics |   |
   |  |  / Reporting  |   |
   |  --------------------   |
   |                        |
   |  --------------------   |
   |  |  Data Processing  |  |
   |  |------------------|  |
   |  |  AWS Glue       |  |
   |  |  AWS Lambda    |  |
   |  --------------------   |
   |                        |
   |  --------------------   |
   |  | Data Catalogue   |  |
   |  | & Classification|  |
   |  |------------------|  |
   |  | AWS Glue Data   |  |
   |  | Catalog        |  |
   |  --------------------   |
   --------------------------

        AWS Step Functions
                |
                v
   -----------------------------
   |        Data Flow          |
   -----------------------------

   API --> Analytical Data Access
             |--> AWS Athena
             |--> Redshift (Optional)

   AWS Identity & Access Management

   AWS CloudWatch (Monitoring / Alert)

   Target Systems (Analytics)
     |--> Notebooks (Optional)
     |--> QuickSight
     |--> Power BI (Optional)
     |--> Qlik


