+++
title = "all_assets_vw_prc"
+++

### What does it do?
Inserts rows into the `all_asset_view` table using values from the `networkelement_sum_vw` and `contractcoverage_sum_vw` tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `contractcoverage_sum_vw` grouped by **neId** and **serialNumber** where
   - **customerId**/**wfId** match input and
   - **serialNumber** is not null
2. Delete all rows from the `all_asset_view` table that match the **customerId**/**wfId**.
3. Insert rows into the `all_asset_view` table using values from the `contractcoverage_sum_vw` and `networkelement_sum_vw` tables.
4. Update the **lastScanDate** field for rows in the `all_asset_view` table.
5. Call the following stored procedures in sequence:
   - amp_neid_update_prc
   - xaas_sub_data_process_prc
{{% /expand %}}

### Referenced Tables
- all_asset_view
- contractcoverage_sum_vw
- data_merge_logs
- networkelement_sum_vw
- pfm_diag_request

### Referenced Stored Procedures
- amp_neid_update_prc
- [log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- xaas_sub_data_process_prc
