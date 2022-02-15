+++
title = "retry_failed_uploads_prc"
+++

{{% notice note %}}
This procedure runs every 12 hours.
{{% /notice %}}

### What does it do?
Check for `FAILED`/`SUSPENDED` rows in `asset_inventory_notification` that were started over 12 hours ago and have not been retried. For each row, partitions are dropped if they exist and rows are deleted from the `base_table_partition_info` table. The row status is updated to `RECEIVED`. Also, all rows of the `asset_contract_notification` where the processing was started over 24 hours ago in `FAILED`/`SUSPENDED` state.
{{% expand "More Details" %}}
1. Gets a cursor over `asset_inventory_notification` where
   - **processingStart** is over 12 hours ago, also not null/undefined, and
   - **processingStatus** is either `FAILED` or `SUSPENDED` and
   - **retrycount** is 0
2. Open a read loop on the cursor that:
   1. Checks if the **wfId** is already present in the `customer_partition_info` and if not
      1. Check if any uploads for the same **mgmtSystemId** with **processingStart** in the last 12 hours are in `SUCCESS` state. If none are, then
      2. Call the `drop_partions_prc` on the **customerId**/**wfId**
      3. Delete the rows from the `base_table_partition_info` table
      4. Update the rows in `asset_inventory_notification` that are in `FAILED`/`SUSPENDED` state by:
         - setting the **processingStatus** to `RECEIVED` and
         - setting the **retryCount** to  1
         - setting the **recordType** to either   
           a. `INVENTORY_DATA_RECEIVED` if **mgmtSystemType** is `DNAC` or `CSDFIB`, or   
           b. `CIBES_INVENTORY_DATA_RECEIVED` otherwise
3. Update all rows in `asset_contract_notification` that were started over 24 hours ago and in `FAILED`/`SUSPENDED` state by: 
   - setting **processingStatus** to `RECEIEVED`
   - setting **retryCount** to 1
{{% /expand %}}

### Referenced Tables
- asset_contract_notification
- asset_inventory_notification
- base_table_partition_info
- customer_partition_info
- partition_automation_logs

### Referenced Stored Procedures
- [drop_partions_prc]({{< ILink href="/database/stored-procedures/drop_partions_prc" >}})
