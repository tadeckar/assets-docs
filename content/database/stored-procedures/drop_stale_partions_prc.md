+++
title = "drop_stale_partions_prc"
+++

{{% notice note %}}
This procedure runs once every day.
{{% /notice %}}

### What does it do?
Drops partitions in which the **partition_description** in the INFORMATION_SCHEMA db PARTITIONS table does not match up to any **partitionValue**s in the `base_table_partition_info` or `customer_partition_info` tables.
{{% expand "More Details" %}}
1. Gets a cursor over INFORMATION_SCHEMA db PARTITIONS table where:
   - **partition_description** is not in any **partitionValue**s from `base_table_partition_info` and
   - **partition_description** is not in any **partitionValue**s from `customer_partition_info`
2. Opens a read loop on the cursor that drops each partition from the table it's part of. (Note: Read loop skips row where **partition_id** is `pp1`.)
{{% /expand %}}

### Referenced Tables
- base_table_partition_info
- customer_partition_info
- partition_automation_logs
