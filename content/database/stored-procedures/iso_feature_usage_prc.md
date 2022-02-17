+++
title = "iso_feature_usage_prc"
+++

### What does it do?
Adds rows to the `iso_feature_usage` table using values from the `iso_depolyment_details_stg` staging table. 
{{% expand "More Details" %}}
1. Get a cursor over all rows in the `iso_feature_master` table.
2. Delete rows from the `iso_depolyment_details_stg` table where
   - the **wfId** field doesn't match the input **wfId**, or is null/undefined and
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
3. Open a read loop on the cursor that inserts new row into `iso_feature_usage` using values from `iso_depolyment_details_stg`.
4. Update **enabled** to `true` for rows in `iso_feature_usage` table if the **featureUsedCount** is > 0.
5. Update **connectorDeployedCount** to a value from the correlating row in the `iso_daily_consumption_trend` table for rows in `iso_feature_usage` table.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- asset_data_load_notification
- iso_daily_consumption_trend
- iso_depolyment_details_stg
- iso_feature_master
- iso_feature_usage

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
