+++
title = "iso_daily_trend_prc"
+++

### What does it do?
Adds rows to ISO daily trend tables using values from ISO trend staging tables. 
{{% expand "More Details" %}}
1. Delete rows from the `iso_user_login_trend_stg` table where
   - the **wfId** field doesn't match the input **wfId**, or is null/undefined and
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
2. Delete rows from the `iso_user_login_trend_stg` table where
   - the **wfId** field doesn't match the input **wfId**, or is null/undefined and
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
3. Delete rows from the `iso_consumption_trend_stg` table where
   - the **wfId** field doesn't match the input **wfId**, or is null/undefined and
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
4. Insert new row into `iso_daily_login_trend ` using values from `iso_user_login_trend_stg`.
5. Insert new row into `iso_daily_consumption_trend` using values from `iso_consumption_trend_stg`.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- asset_data_load_notification 
- iso_consumption_trend_stg 
- iso_daily_consumption_trend
- iso_daily_login_trend
- iso_user_login_trend_stg
- iso_user_login_trend_stg

### Referenced Stored Procedures
- amp_log_msg_prc
