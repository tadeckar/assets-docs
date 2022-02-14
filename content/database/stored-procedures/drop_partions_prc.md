+++
title = "drop_partions_prc"
+++

### What does it do?
Drops a partition from all tables that it is a part of.
{{% expand "More Details" %}}
1. Gets a cursor over `partition_tables` where **partitionTag** matches the given parameter.
2. Create a read loop on the cursor that:
   1. Gets a count of rows in INFORMATION_SCHEMA db PARTITIONS table where:
      - **TABLE_NAME** matches the rows **tableName** and
      - **partition_description** matches the given **partitionValue** parameter.
   2. If the count from the previous step is > 1:
      1. Get the rows from the INFORMATION_SCHEMA db PARTITIONS table that match the row from the cursor
      2. Use the **partition_name** field from the result to drop that partition from each table 
{{% /expand %}}

### Referenced Tables
- partition_automation_logs
- partition_tables
