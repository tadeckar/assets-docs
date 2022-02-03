+++
title = "NotificationManager"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/master/glue/cp-asset-data-import-job/csco/dp/manager/NotificationManager.py" >}}

The NotificationManager is a utility class that houses a variety of functions for modifying the `asset_inventory_notification` and `asset_data_load_notification` tables.

The NotificationManager also houses the (seemingly unrelated) function to delete all rows matching a given customerId/wfId for a given table.
