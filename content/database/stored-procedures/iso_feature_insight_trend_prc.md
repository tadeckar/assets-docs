+++
title = "iso_feature_insight_trend_prc"
+++

### What does it do?
Adds rows to the `iso_feature_insight_trend` table using values from the `iso_connector_monthly_trend_stg` staging table. 
{{% expand "More Details" %}}
1. Get a cursor over rows in the `iso_feature_master` table where **feature_type** is `Connector`.
2. Delete rows from the `iso_connector_monthly_trend_stg` table where
   - the **wfId** field doesn't match the input **wfId**, or is null/undefined and
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
3. Open a read loop on the cursor that inserts new row into `iso_feature_insight_trend ` using values from `iso_connector_monthly_trend_stg`.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- asset_data_load_notification
- iso_connector_monthly_trend_stg
- iso_connector_monthly_trend_stg
- iso_feature_insight_trend
- iso_feature_master

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
