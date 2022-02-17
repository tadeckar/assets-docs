+++
title = "iso_summary_view_prc"
+++

### What does it do?
Populates data for the ISO Summary view tables.
{{% expand "More Details" %}}
1. Get a cursor over rows in the `iso_contract_view` table where **customerId** matches stored procedure input parameter.
2. Delete rows from the `iso_user_login_details_stg` table where
   - **customerId** matches input and
   - **wfId** does not match input and 
   - there is no **wfId** row in `asset_data_load_notification` in `SUBMITTED` state
3. Insert rows into `iso_summary_view` using values from `iso_component_master` and `iso_depolyment_details_stg`.
4. Update **connectorDeployedCount** and **connectorPurchasedCount** to values from the correlating row in the `iso_daily_consumption_trend` table for rows in `iso_summary_view` table.
5. Update **lastLoginDate** and **lastLoginGt30Days** to values from the correlating row in the `iso_user_login_details_stg` table for rows in `iso_summary_view` table.
6. Update **totalFeatureCount**, **activeFeatureCount**, and **activeFeaturePercent** to values from the correlating row in the `iso_feature_usage` table for rows in `iso_summary_view` table.
7. Open a read loop on the cursor that:
   1. Selects a row from the `iso_contract_view` table that matches the **customerId** and **customerBuId**.
   2. Updates rows in the `iso_summary_view` table with values from the previously selected row.
8. Update **businessProcessInfo** to a value from the correlating row in the `service_level_info` table for rows in `iso_summary_view` table.
9. Update **solutionInfo**, **usecaseIds**, and **solutionIds** to values from the correlating row in the `pid_solution_mapping` table for rows in `iso_summary_view` table.
10. Create the `amp_ne_sol_map_tmp` temporary table and fill it with rows of distinct columns: **ampNeId**, **usecaseIds**, and **solutionIds**.
11. Update **usecaseIds** and **solutionIds** to values from the correlating row in the `amp_ne_sol_map_tmp` table for rows in the following tables.
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
12. Drop the `amp_ne_sol_map_tmp` temporary table.
13. Call the [amp_neid_update_prc]({{< ILink href="/database/stored-procedures/amp_neid_update_prc" >}}) stored procedure.
{{% /expand %}}

### Referenced Tables
- amp_data_merge_logs
- amp_ne_sol_map_tmp
- asset_data_load_notification
- iso_component_master
- iso_contract_view
- iso_daily_consumption_trend
- iso_daily_login_trend
- iso_depolyment_details_stg
- iso_feature_insight_trend
- iso_feature_master
- iso_feature_usage
- iso_monthly_consumption_trend
- iso_monthly_login_trend
- iso_quarterly_consumption_trend
- iso_quarterly_login_trend
- iso_summary_view 
- iso_user_login_details_stg
- iso_weekly_consumption_trend
- iso_weekly_login_trend
- pid_solution_mapping
- service_level_info

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [amp_neid_update_prc]({{< ILink href="/database/stored-procedures/amp_neid_update_prc" >}})
