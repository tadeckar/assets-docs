+++
title = "InventoryDataLoadManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/InventoryDataLoadManager.py" >}}

{{% notice info %}}
The InventoryDataLoadManager is not currently in use.
{{% /notice %}}

Loads data of the `IBES_INV_UPLOAD` [File Type]({{< ILink href="/ingestion/types/file-types" >}}).

Firstly, the IDLM tries to create a partition using the `add_base_table_partions_prc` stored procedure. If the partition already exists, processing is skipped.

Next, a thread is spun up to load the data, executing the [DataLoadManager]({{< ILink href="/ingestion/managers/data-load-manager" >}}), which in turn executes a Loader of [IBES Data Load Type]({{< ILink href="/ingestion/types/data-load-types/#ibes" >}}).

The [NotificationManager]({{< ILink href="/ingestion/managers/notification-manager" >}}) is also used record the data load processing start/end times.
