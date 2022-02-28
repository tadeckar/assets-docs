+++
title = "contract_group_device_sum_prc"
+++

### What does it do?
Inserts rows into the `contract_group_device_summary` table using values from other various tables.
{{% expand "More Details" %}}
1. If the **transactionType** is `DELETE`/`UPDATE`, delete rows matching **customerId**/**groupId** from the `contract_group_device_summary` table. Otherwise, if the  **transactionType** is `EDIT`, delete rows matching **customerId**/**neId**.
2. If the **transactionType** is `INSERT`/`UPDATE`:
   1. Create a temporary table `contractgrpdevice_tmp` using values from `contractcoverage_sum_vw`.
   2. Insert rows into the `contract_group_device_summary` table using values from the `contractgrpdevice_tmp` and `networkelement_sum_vw` tables.
   3. Drop the `contractgrpdevice_tmp` table.
   4. Count the rows matching **customerId** in the `iso_summary_view` table.
   5. If the count is > 0, insert rows into the `contract_group_device_summary` table using values from the `iso_summary_view`, `asset_group_device`, and `iso_contract_view` tables.
   6. Count the rows matching **customerId** in the `networkelement_sub_stg` table.
   7. If the count is > 0, insert rows into the `contract_group_device_summary` table using values from the `networkelement_sub_stg`, `asset_group_device`, and `subscription_stg` tables.
3. If the **transactionType** is `EDIT`:
   1. Create a temporary table `contractgrpdevice_tmp` using values from `contractcoverage_sum_vw`.
   2. Insert rows into the `contract_group_device_summary` table using values from the `contractgrpdevice_tmp`, `asset_group_device`, and `networkelement_sum_vw` tables.
   3. Drop the `contractgrpdevice_tmp` table.
   4. Count the rows matching **customerId** in the `iso_summary_view` table.
   5. If the count is > 0, insert rows into the `contract_group_device_summary` table using values from the `iso_summary_view`, `asset_group_device`, and `iso_contract_view` tables.
   6. Count the rows matching **customerId** in the `networkelement_sub_stg` table.
   7. If the count is > 0, insert rows into the `contract_group_device_summary` table using values from the `networkelement_sub_stg`, `asset_group_device`, and `subscription_stg` tables.
{{% /expand %}}

### Referenced Tables
- asset_group_device
- contract_group_device_summary
- contractcoverage_sum_vw
- data_merge_logs
- iso_contract_view
- iso_summary_view
- networkelement_sub_stg
- networkelement_sum_vw
- subscription_stg

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
