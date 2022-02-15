+++
title = "stale_inprogress_data_cleanup_prc"
+++

{{% notice note %}}
This procedure runs every 30 minutes.
{{% /notice %}}

### What does it do?
Updates the **processingStatus** from `INPROGRESS` to `SUCCESS` for rows in the `asset_inventory_notification` table that started over 1 hour ago when **partitionStatus** in the `customer_partition_info` table is `A` (Active.)

Also updates the **processingStatus** from `INPROGRESS` to `SUCCESS` for rows in the `asset_inventory_notification` table that were started over 6 hours ago and are not found in `customer_partition_info` or `base_table_partition_info`.
{{% expand "More Details" %}}
1. Get a cursor over `asset_inventory_notification` where
   - **processingStart** is over 1 hour ago, also not null/undefined, and
   - **processingStatus** is `INPROGRESS`
   - **partitionStatus** from `customer_partition_info` table is `A` (Active)
2. Open a read loop on the cursor that updates the **processingStatus** to `SUCCESS` and sets **processingEnd** to the current time.
3. Set **processingStatus** to `SUCCESS` for all rows of the `asset_inventory_notification` table where
   - **processingStatus** is `INPROGRESS` and
   - **processingStart** is over 6 hours ago, also not null/undefined, and
   - **wfId** is not found in `customer_partition_info` and
   - **wfId** is not found in `base_table_partition_info` with **partitionStatus** as `I` and
   - **processingEnd** is 0
{{% /expand %}}

### Referenced Tables
- asset_inventory_notification
- base_table_partition_info 
- customer_partition_info
- data_merge_logs

### Referenced Stored Procedures
- log_msg_prc
