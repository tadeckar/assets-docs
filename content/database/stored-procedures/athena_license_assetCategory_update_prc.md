+++
title = "athena_license_assetCategory_update_prc"
+++

### What does it do?
Updates **assetCategory** to `Cisco Plus` for rows in the `iso_subscription_stg` table where **subscription_product_family** is `UCSBFC`.
{{% expand "More Details" %}}
1. Update **assetCategory** to `Cisco Plus` for rows in `iso_subscription_stg` where
   - **customerId**/**wfId** match input and
   - **subscription_reference_id** is found in the `iso_subscription_stg` table where
     - **customerId**/**wfId** match input and
     - **subscription_product_family** is `UCSBFC`
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- iso_subscription_stg

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
