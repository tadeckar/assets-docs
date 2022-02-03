+++
title = "Ingestion"
chapter = false
+++

The repositories associated with AWS Glue are:
- [cp-asset-data-pipeline](https://www-github3.cisco.com/cxe/cp-asset-data-pipeline): Ingest Data to MySQL from Parquet files in S3
- [cp-asset-data-export-pipeline](https://www-github3.cisco.com/cxe/cp-asset-data-export-pipeline): Export data to consumers (Insights)

## Overview
![Overview](/images/ingestion.png)

At a high level, a Lambda function listens for SQS events. Upon receiving, the Glue ETL Job is triggered. The job downloads files from an S3 bucket, parses them, and stores results in staging tables of the RDS MySQL database.

The SQS message's `recordType` property signals the type of data that should be loaded. The graph below depicts the flow of logic through the Glue ETL Job.

{{< mermaid >}}
graph TD;
  RT{SQS recordType} -->|CSDF_AMP_TELE| PINV(ParqeutInvDataLoadManager)
  RT -->|CSDF_SUBSCRIPTION| PINV
  RT -->|CIBES_INVENTORY_DATA_RECEIVED| PINV
  RT -->|DNAC_DATA_RECEIVED| PINV
  RT -->|MERAKI_LICENSE| LIC(LicenseDataLoadManager)
  RT -->|XAAS_INVENTORY_DATA_RECEIVED| PINV
  RT -->|DCC_SUB| PINV
  RT -->|ATHENA| HYB(HybridSubscriptionDataLoadManager)

  PINV --> PINVD{SQS mgmtSystemType}
  PINVD -->|DCC_SUB| DCC_SUBL(DataLoadManager)
  DCC_SUBL --> DCC_SUBL_NEPDL(NEParquetDataLoader)
  DCC_SUBL --> DCC_SUBL_SPDL(SubscriptionParquetDataLoader)
  PINVD -->|DNAC_DL| DNAC_DLL(DataLoadManager)
  DNAC_DLL --> DNAC_DLL_NEPDL(NEParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_EQPDL(EQParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_APDL(AlertsParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_BMPDL(BulletinMasterParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_CPDL(ContractParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_CLIPDL(CLIParquetDataLoader)
  DNAC_DLL --> DNAC_DLL_CONFIGPDL(ConfigParquetDataLoader)
  PINVD -->|else| PINVD_ELSE(DataLoadManager)
  PINVD_ELSE --> ELSE_BMPDL(BulletinMasterParquetDataLoader)
  PINVD_ELSE --> ELSE_NEPDL(NEParquetDataLoader)
  PINVD_ELSE --> ELSE_EQPDL(EQParquetDataLoader)
  PINVD_ELSE --> ELSE_APDL(AlertsParquetDataLoader)
  PINVD_ELSE --> ELSE_CPDL(ContractParquetDataLoader)
  click PINV "/ingestion/managers/parquet-inv-data-load-manager/"
  click DCC_SUBL "/ingestion/managers/data-load-manager/"
  click DNAC_DLL "/ingestion/managers/data-load-manager/"
  click PINVD_ELSE "/ingestion/managers/data-load-manager/"

  LIC --> LIC_DLM(DataLoadManager)
  LIC_DLM --> LPDL(LicenseParquetDataLoader)
  click LIC "/ingestion/managers/license-data-load-manager/"
  click LIC_DLM "/ingestion/managers/data-load-manager/"

  HYB --> HYB_DLM(DataLoadManager)
  HYB_DLM --> HSPDL(HybridSubscriptionParquetDataLoader)
  click HYB "/ingestion/managers/hybrid-subscription-data-load-manager/"
  click HYB_DLM "/ingestion/managers/data-load-manager/"

{{< /mermaid >}}

### Contents
{{% children %}}
