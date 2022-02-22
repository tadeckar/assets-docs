+++
title = "license_sum_view_prc"
+++

### What does it do?
Syncs the `license_sum_view` table with values from `iso_subscription_stg`.
{{% expand "More Details" %}}
1. Get a count of rows in the `license_sum_view` table matching **customerId**/**wfId**.
2. If the count is > 0, delete those rows from `license_sum_view`.
3. Call the `athena_license_assetCategory_update_prc` stored procedure with **customerId**/**wfId**
4. Insert rows into `license_sum_view` using values from `iso_subscription_stg` if the **SUBSCRIPTION_PRODUCT_FAMILY** is not `UCSBFC`.
5. Update **useCaseIds**, **solutionIds**, **solutionInfo**, **licenseLevel**, and **level4CompName** in `license_sum_view` using values from `pid_solution_mapping`.
6. Get a count of rows in `license_sum_view` matching **customerId**/**wfId** where **solutionIds** is `|52517223|` (Meraki).
7. If the count is > 0, delete those rows from `license_sum_view`.
8. Get a count of rows in `customer_wfid_info` where 
   - **customerId** matches input and
   - **module** is `MERAKI_LICENSE` and
   - **wfIdStatus** is `A` (Active)
9. If the count is > 0:
   1. Get the **wfId** from `customer_wfid_info`.
   2. Get a count of rows in `meraki_license_sum_view_stage` matching **customerId**/**wfId**.
   3. If the count is > 0, insert rows into `license_sum_view` with values from `meraki_license_sum_view_stage`.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- customer_wfid_info 
- iso_subscription_stg
- license_sum_view
- meraki_license_sum_view_stage
- pid_solution_mapping

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- athena_license_assetCategory_update_prc
