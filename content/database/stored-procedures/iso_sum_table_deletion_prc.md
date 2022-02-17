+++
title = "iso_sum_table_deletion_prc"
+++

### What does it do?
Deletes all rows matching specified **customerId**/**wfId** from ISO summary tables.
{{% expand "More Details" %}}
1. Deletes rows matching **customerId**/**wfId** from the following tables:
   - iso_daily_login_trend
   - iso_daily_consumption_trend
   - iso_weekly_login_trend 
   - iso_weekly_consumption_trend 
   - iso_monthly_login_trend
   - iso_monthly_consumption_trend
   - iso_quarterly_login_trend
   - iso_quarterly_consumption_trend
   - iso_feature_usage
   - iso_feature_insight_trend
   - iso_summary_view
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
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
