+++
title = "DataFileManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/DataFileManager.py" >}}

The DataFileManager is used for all data loading tasks. Its purpose is to choose one of the following Managers based on a given [File Type](/glue/file-types) argument:

`ATHENA`:  
[HybridSubscriptionDataLoadManager]({{< ILink href="/ingestion/managers/hybrid-subscription-data-load-manager" >}})  

`INVENTORY_DATA_RECEIVED`:  
[InventoryDataLoadManager]({{< ILink href="/ingestion/managers/inventory-data-load-manager" >}})  

`MERAKI_LICENSE`:  
[LicenseDataLoadManager]({{< ILink href="/ingestion/managers/license-data-load-manager" >}})  

`CIBES_INVENTORY_DATA_RECEIVED` and `DNAC_DATA_RECEIVED` and all other file types:   
[ParquetInvDataLoadManager]({{< ILink href="/ingestion/managers/parquet-inv-data-load-manager" >}})
