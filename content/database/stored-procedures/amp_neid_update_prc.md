+++
title = "amp_neid_update_prc"
+++

### What does it do?
Inserts rows into the `all_asset_view` table using data from other various tables.
{{% expand "More Details" %}}
1. If input parameter **wf** is `AMP`:
   1. Get a count of rows in `customer_partition_info` where
      - **customerId** matches input parameter and
      - **partitionStatus** is `A` (Active)
   2. If the count is 1:
      1. Get the **wfId** from the `customer_partition_info` table
      2. Delete rows from `all_asset_view` where
         - **customerId** matches input and
         - **wfId** matches the resulting **wfId** of previous step and
         - there are rows of the `iso_summary_view` table where **ampNeId** match **neId** of `all_asset_view`
      3. Insert rows into `all_asset_view` using values from `iso_summary_view`
      4. Get a count of rows using values from `iso_summary_view` and `asset_group_master` that do not have correlating rows in `asset_group_device`.
      5. If the count is > 0:
         1. Delete all rows from `asset_group_master` where
            - **customerId** matches input and
            - there are rows in `iso_summary_view` with matching **neId** 
         2. Insert rows into `asset_group_device` using values from `iso_summary_view` and `asset_group_master`.
      6. Delete rows from `contract_group_device_summary` where
         - **customerId** matches input and
         - there are rows of the `iso_summary_view` table where **ampNeId** match **neId** of `contract_group_device_summary`
      7. Insert rows into `contract_group_device_summary` using values from `iso_summary_view`, `asset_group_device`, and `contract_view`
2. If input parameter **wf** is not `AMP`, insert rows into `all_asset_view` using values from `iso_summary_view`.
{{% /expand %}}

### Referenced Tables
- all_asset_view
- asset_group_device
- asset_group_master
- contract_group_device_summary
- customer_partition_info
- data_merge_logs
- iso_contract_view
- iso_summary_view

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
