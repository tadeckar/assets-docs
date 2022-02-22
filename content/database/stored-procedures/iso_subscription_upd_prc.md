+++
title = "iso_subscription_upd_prc"
+++

### What does it do?
Syncs the `iso_summary_view` with values from the `iso_contract_view` table.
{{% expand "More Details" %}}
1. Get a cursor over `iso_contract_view` with distinct values of **cavId** that match **customerId**/**wfId**.
2. Open a read loop on the cursor that:
   1. Get values from various columns of the `iso_contract_view` table.
   2. Update rows in `iso_summary_view` with values from `iso_contract_view`.
3. Update rows in `iso_summary_view` with **businessProcessInfo** value from `service_level_info`.
4. Update rows in `iso_summary_view` with **solutionInfo**, **usecaseIds**, and **solutionIds** values from `pid_solution_mapping`.
5. Create a temporary table with distinct **ampNeId**, **useCaseIds**, and **solutionIds** from `iso_summary_view`.
6. Update rows of the following tables with correct values for **useCaseIds** and **solutionIds**:
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
7. Drop the temporary table.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- iso_contract_view
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
- pid_solution_mapping
- service_level_info

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
