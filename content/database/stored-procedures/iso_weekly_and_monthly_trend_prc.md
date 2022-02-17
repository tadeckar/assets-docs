+++
title = "iso_weekly_and_monthly_trend_prc"
+++

### What does it do?
Inserts rows into ISO weekly, monthly, and quarterly aggregation tables for login and consumption trends.
{{% expand "More Details" %}}
1. Insert rows into `iso_weekly_login_trend` using grouped data from `iso_daily_login_trend`.
2. Insert rows into `iso_weekly_consumption_trend` using grouped data from `iso_daily_consumption_trend`.
3. Insert rows into `iso_monthly_login_trend` using grouped data from `iso_daily_login_trend`.
4. Insert rows into `iso_monthly_consumption_trend` using grouped data from `iso_daily_consumption_trend`.
5. Insert rows into `iso_quarterly_login_trend` using grouped data from `iso_daily_login_trend`.
6. Insert rows into `iso_quarterly_consumption_trend` using grouped data from `iso_daily_consumption_trend`.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- iso_weekly_login_trend
- iso_daily_login_trend
- iso_weekly_consumption_trend
- iso_daily_consumption_trend
- iso_monthly_login_trend
- iso_monthly_consumption_trend
- iso_quarterly_login_trend 
- iso_quarterly_consumption_trend

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
