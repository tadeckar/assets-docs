+++
title = "iso_data_process_wrap_prc"
+++

### What does it do?
Call stored procedures to create summary views for iso data.
{{% expand "More Details" %}}
1. Get a count of the rows in the `customer_wfid_info` table that match **customerId**/**wfId** where
   - **module** is `CSDF_AMP_TELE` and
   - **wfIdStatus** is `I`
2. If the count is 0, then insert a row.
3. Call stored procedures
   1. Call the `iso_sum_table_deletion_prc` stored procedure
   2. Call the `iso_daily_trend_prc` stored procedure
   3. Call the `iso_weekly_and_monthly_trend_prc` stored procedure
   4. Call the `iso_feature_usage_prc` stored procedure
   5. Call the `iso_feature_insight_trend_prc` stored procedure
   6. Call the `iso_summary_view_prc` stored procedure
4. Delete any row from the `customer_wfid_info` table matching **customerId**/**wfId** where **wfIdStatus** is `A`.
5. Update **wfIdStatus** to `A` for any row from the `customer_wfid_info` table matching **customerId**/**wfId** where **wfIdStatus** is `I`.
6. Delete any rows from the following tables that match **customerId** but don't match **wfId**:
   - iso_daily_consumption_trend
   - iso_daily_login_trend
   - iso_feature_insight_trend 
   - iso_feature_usage
   - iso_monthly_consumption_trend
   - iso_monthly_login_trend
   - iso_quarterly_consumption_trend
   - iso_quarterly_login_trend
   - iso_summary_view
   - iso_weekly_consumption_trend
   - iso_weekly_login_trend
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- customer_wfid_info
- iso_daily_consumption_trend
- iso_daily_login_trend
- iso_feature_insight_trend 
- iso_feature_usage
- iso_monthly_consumption_trend
- iso_monthly_login_trend
- iso_quarterly_consumption_trend
- iso_quarterly_login_trend
- iso_summary_view
- iso_weekly_consumption_trend
- iso_weekly_login_trend

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- iso_daily_trend_prc
- iso_feature_insight_trend_prc
- iso_feature_usage_prc
- iso_sum_table_deletion_prc
- iso_summary_view_prc
- iso_weekly_and_monthly_trend_prc
