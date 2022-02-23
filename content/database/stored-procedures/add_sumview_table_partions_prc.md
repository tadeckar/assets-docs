+++
title = "add_sumview_table_partions_prc"
+++

### What does it do?
Adds partitions to the summary view tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `partition_tables` table that match the **partitionTag** input parameter.
2. Insert a row into the `customer_partition_info` table using input parameter values.
3. Get the **partitionId** of the newly created partition.
4. Open a read loop on the cursor that:
   1. Gets a count of rows in the `INFORMATION_SCHEMA.PARTITIONS` table where
      - **TABLE_NAME** matches the **tableName** and 
      - **partition_description** matches **partitionValue**
   2. If the count is 1, alter the table (given the **tableName**) by adding a partition.
{{% /expand %}}

### Referenced Tables
- customer_partition_info
- partition_automation_logs
