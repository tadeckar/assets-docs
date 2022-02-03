+++
title = "ParquetInvDataLoadManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/ParquetInvDataLoadManager.py" >}}

Loads data of the `CIBES_INV_UPLOAD` and `DNAC_UPLOAD` [File Types](/pages/tadeckar/assets-docs/ingestion/types/file-types).

Firstly, the PIDLM checks the SQS message for `mgmtSystemType`. If the value of this property is not `DCC_SUB`, PIDLM tries to create a partition using the `add_base_table_partions_prc` stored procedure. Otherwise, processing begins regardless.

When `mgmtSystemType === "DCC_SUB"`, and the partition is created successfully, processing begins. If the partition already exists, the base table partitions are cleared using the `delete_raw_data_wfid_prc` stored procedure, then processing begins.

Next, a thread is spun up to load the data, executing the [DataLoadManager](/pages/tadeckar/assets-docs/ingestion/managers/data-load-manager), which in turn executes a Loader of either [XAAS](/pages/tadeckar/assets-docs/ingestion/types/data-load-types/#xaas), [DNAC](/pages/tadeckar/assets-docs/ingestion/types/data-load-types/#dnac), or [CIBES](/pages/tadeckar/assets-docs/ingestion/types/data-load-types/#cibes) Data Load Types, dependent on the `mgmtSystemType`. See mapping below.

When `mgmtSystemType` is `"DCC_SUB"`, Data Load Type is XAAS.   
When `mgmtSystemType` is `"DNAC_DL"`, Data Load Type is DNAC.   
When `mgmtSystemType` is neither  `"DCC_SUB"` nor `"DNAC_DL"`, Data Load Type is CIBES.  


The [NotificationManager](/pages/tadeckar/assets-docs/ingestion/managers/notification-manager) is also used record the data load processing start/end times.
