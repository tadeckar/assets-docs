+++
title = "drop_pending_wfid_status_sum_tables_prc"
+++

{{% notice note %}}
This procedure runs once every day.
{{% /notice %}}

### What does it do?
Calls the `drop_partions_prc` stored procedure on rows of the `customer_partition_info` table that have been in `P` state for over a day.
{{% expand "More Details" %}}
1. Get a cursor over `customer_partition_info` where
   - **lastUpdateDate** is > 1 day go and 
   - **partitionStatus** is `P`
2. Open a read loop on the cursor that
   1. Calls the `drop_partions_prc` stored procedure with fields from the row
   2. Deletes the row from `customer_partition_info`
{{% /expand %}}

### Referenced Tables
- customer_partition_info
- partition_automation_logs

### Referenced Stored Procedures
- [drop_partions_prc]({{< ILink href="/database/stored-procedures/drop_partions_prc" >}})
