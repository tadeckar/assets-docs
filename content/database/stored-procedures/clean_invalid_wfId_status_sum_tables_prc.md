+++
title = "clean_invalid_wfId_status_sum_tables_prc"
+++

{{% notice note %}}
This procedure runs once every day.
{{% /notice %}}

### What does it do?
Drops partitions for rows in `customer_partition_info` where **partitionStatus** is `I` and **lastUpdateDate** is greater than 4 days ago. Then, deletes the rows from `customer_partition_info`.
{{% expand "More Details" %}}
1. Get a cursor over `customer_partition_info` where:
   - **partitionStatus** is `I` and
   - **lastUpdateDate** is greater than 4 days ago.
2. Open a read loop over the cursor that:
   1. Calls the `drop_partions_prc` stored procedure with data from row as params.
   2. Deletes the row from `customer_partition_info` where **lastUpdateDate** is greater than 2 days ago.
{{% /expand %}}

### Referenced Tables
- customer_partition_info
- partition_automation_logs

### Referenced Stored Procedures
- [drop_partions_prc]({{< ILink href="/database/stored-procedures/drop_partions_prc" >}})
