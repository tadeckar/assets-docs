+++
title = "add_base_table_partions_prc"
+++

### What does it do?
Adds a partition to tables defined in the `partition_tables` table. (Called from Glue ETL Job.)
{{% expand "More Details" %}}
1. Get a cursor on `partition_tables` table where **partitionTag** and **mgmtSystemType** match input params that selects **tableName**.
2. Get a count of **wfId**s for the given **partitionTag**.
3. If the count is 0:
   - Insert all input params into the `base_table_partition_info` table
   - Open a read loop over the cursor that, if partition on table doesn't already exist, adds the partition to the table.
{{% /expand %}}

### Referenced Tables
- base_table_partition_info
- partition_automation_logs
- partition_tables
