+++
title = "HybridSubscriptionDataLoadManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/HybridSubscriptionDataLoadManager.py" >}}

Loads data of the `HYBRID_CLOUD` [File Type](/pages/tadeckar/assets-docs/ingestion/types/file-types).

Firstly, the HSDLM checks whether or not data for the given wfId has already been loaded. If the data has already been loaded, the data is cleared from the `athena_subscription_stg` staging table for the given customerId/wfId before execution proceeds to the next step.

Next, a thread is spun up to load the data, executing the [DataLoadManager](/pages/tadeckar/assets-docs/ingestion/managers/data-load-manager), which in turn executes a Loader for the [Hybrid Data Load Type](/pages/tadeckar/assets-docs/ingestion/types/data-load-types#hybrid).

The [NotificationManager](/pages/tadeckar/assets-docs/ingestion/managers/notification-manager) is also used record the data load processing start/end times, as well as to delete rows when wfId data has already been loaded.
