+++
title = "athena_ib_stg_data_process_prc"
+++

### What does it do?
Syncs rows between the `athena_subscription_stg` and `networkelement_ib_data` tables.
{{% expand "More Details" %}}
1. Gets a count of rows in `base_table_partition_info` where
   - **customerId** matches input and
   - **mgmtSystemType** is `CSDFIB` and
   - **partitionStatus** is `A` (Active)
2. If the count is 1 (customer has 1 active inv upload)
   1. Get the **wfId** of the active partition
   2. Get a count of rows in the `athena_subscription_stg` table that are not in the `networkelement_ib_data` table.
   3. If the count is > 0, update the rows in `networkelement_ib_data` so that they are tagged with athena fields.
   4. Get a count of rows in the `networkelement_ib_data` table that are not in the `athena_subscription_stg` table.
   5. If the count is > 0, update the rows in `athena_subscription_stg` removing the tagged athena fields.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- athena_subscription_stg
- base_table_partition_info
- networkelement_ib_data

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
