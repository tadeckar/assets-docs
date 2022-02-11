+++
title = "clean_invalid_status_prc"
+++

{{% notice note %}}
This procedure runs once every day.
{{% /notice %}}

### What does it do?
Checks rows in `base_table_partition_info` table where **lastUpdateDate** is over 4 days ago, drops those partitions, and deletes the rows.
{{% expand "More Details" %}}
1. Get a cursor over `base_table_partition_info` where **lastUpdateDate** is over 4 days ago.
2. Loop over the cursor, performing the following tasks  
   1. Call the `drop_partions_prc` stored procedure  
   2. Delete rows from `base_table_partition_info` where  
      - **lastUpdateDate** is over 2 days ago
      - **partitionStatus** is `I`
{{% /expand %}}

### Related Tables
- base_table_partition_info
- partition_automation_logs

### Stored Procedure Calls
- drop_partions_prc
