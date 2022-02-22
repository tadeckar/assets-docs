+++
title = "iso_subscription_prc"
+++

### What does it do?
Inserts rows into `aav_subscriptions` using values from `iso_subscription_stg`.
{{% expand "More Details" %}}
1. Delete rows from `iso_subscription_stg` where
   - **customerId** matches input and
   - **wfId** does not match input and
   - there is no row in `asset_data_load_notification` where **processingStatus** is `SUBMITTED` for the above **wfId**.
2. Delete all rows matching **customerId**/**wfId**  in `aav_subscriptions`.
3. Insert rows into `aav_subscriptions` using values from `iso_subscription_stg`.
{{% /expand %}}

### Referenced Tables
- aav_subscriptions
- amp_data_merge_logs
- iso_subscription_stg

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
