+++
title = "sub_data_process_wrap_prc"
+++

### What does it do?
Call stored procedures to create summary views for subscriptions, licenses, and contracts.
{{% expand "More Details" %}}
1. Get a count of the rows in the `customer_wfId_info` table that match **customerId**/**wfId** where
   - **module** is `CSDF_SUBSCRIPTION` and
   - **wfIdStatus** is `I`
2. If the count is 0, then insert a row.
3. Call stored procedures
   1. Call the `iso_subscription_prc` stored procedure
   2. Call the `iso_contract_sum_prc` stored procedure
   3. Call the `license_sum_view_prc` stored procedure
4. Delete any row from the `customer_wfId_info` table matching **customerId**/**wfId** where **wfIdStatus** is `A`.
5. Update **wfIdStatus** to `A` for any row from the `customer_wfId_info` table matching **customerId**/**wfId** where **wfIdStatus** is `I`.
6. Delete any rows from the following tables that match **customerId** but don't match **wfId**:
   - `aav_subscriptions`
   - `iso_contract_view`
   - `license_sum_view`
{{% /expand %}}

### Referenced Tables
- aav_subscriptions
- amp_data_merge_logs
- customer_wfid_info
- iso_contract_view 
- license_sum_view 

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- iso_contract_sum_prc
- iso_subscription_prc
- license_sum_view_prc
