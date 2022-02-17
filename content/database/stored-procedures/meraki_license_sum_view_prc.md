+++
title = "meraki_license_sum_view_prc"
+++

### What does it do?
Inserts rows into the `license_sum_view` table using values from `meraki_license_sum_view_stage`.
{{% expand "More Details" %}}
1. Get a count of rows in `customer_wfid_info` where
   - **customerId** matches input parameter and
   - **module** is `CSDF_SUBSCRIPTION` and
   - **wfIdStatus** is `A` (Active)
2. If the count is > 0:
   1. Get the **wfId** from a row in `customer_wfid_info`.
   2. Get a count of rows in `license_sum_view` where
      - **customerId** matches input and
      - **wfId** matches result from previous step and
      - **solutionIds** is `|52517223|` (Meraki solutionId?)
   3. If count is > 0, delete related rows from the `license_sum_view` table.
3. If a **wfId** was retrieved from `customer_wfid_info` in previous step, use that as the main **wfId**. Otherwise, use **wfId** from the stored procedure's input.
4. Insert rows into `license_sum_view` using values from `meraki_license_sum_view_stage`.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- customer_wfid_info
- license_sum_view
- meraki_license_sum_view_stage

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
