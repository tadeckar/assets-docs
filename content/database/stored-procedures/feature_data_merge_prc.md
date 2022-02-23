+++
title = "feature_data_merge_prc"
+++

### What does it do?
Insert rows into the `asset_feature` table using values from the `asset_feature_telemetry` table.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
2. Delete all rows for the given **customerId**/**wfId** from the `asset_feature` table.
3. Get a count of rows in `base_table_partition_info` that match **customerId**/**wfId** where
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `DNAC` and
   - **dnacId** and **customerId** is in row of the `active_dnac_ne` table
4. If the count is > 0, open a read loop on the cursor that inserts rows into the `asset_feature` table using values from the `asset_feature_telemetry` table.
{{% /expand %}}

### Referenced Tables
- active_dnac_ne
- asset_feature
- base_table_partition_info
- data_merge_logs
- asset_feature_telemetry
- networkelement

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
