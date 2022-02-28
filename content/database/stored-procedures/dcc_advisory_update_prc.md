+++
title = "dcc_advisory_update_prc"
+++

### What does it do?
{{% expand "More Details" %}}
1. Create a temporary table `hweox_tmp` using values from `alert_pas_hw_eox_bulletin` and `alert_hweox_dcc` tables grouped by **neId**.
2. Update **ldos** values for rows in the `networkelement_dcc` table using values from `hweox_tmp`.
3. Drop the `hweox_tmp` table.
4. Create a temporary table `critical_adv_cnt_tmp` using values from the `alert_psirt_dcc` table grouped by **neId**.
5. Update **advisoryLevel**, **advisoryCount**, **hasSecurityAdvisory**, and **allPsirtCount** values for rows in the `networkelement_dcc` table using values from `critical_adv_cnt_tmp`.
6. Drop the `critical_adv_cnt_tmp` table.
7. Call the `dcc_license_status_update_prc` stored procedure.
8. Create a temporary table `sweox_tmp` using values from the `alert_pas_sw_eox_bulletin` and `alert_sweox_dcc` tables grouped by **neId**.
9. Update **endOfSwEoxDate** values for rows in the `networkelement_dcc` table using values from `sweox_tmp`.
10. Drop the `sweox_tmp` table.
11. Create a temporary table `fn_adv_cnt_tmp` using values from the `alert_fn_dcc` table grouped by **neId**.
12. Update **fieldNoticeCount** values for rows in the `networkelement_dcc` table using values from `fn_adv_cnt_tmp`.
13. Drop the `bug_cnt_tmp` table.
14. Create a temporary table `bug_cnt_tmp` using values from the `asset_priority_bugs` table grouped by **neId**.
15. Update **bugCount** values for rows in the `networkelement_dcc` table using values from `bug_cnt_tmp`.
16. Drop the `bug_cnt_tmp` table.
{{% /expand %}}

### Referenced Tables
- alert_fn_dcc
- alert_hweox_dcc
- alert_pas_hw_eox_bulletin
- alert_pas_sw_eox_bulletin
- alert_psirt_dcc
- alert_sweox_dcc
- asset_priority_bugs
- data_merge_logs
- networkelement_dcc

### Referenced Stored Procedures
- dcc_license_status_update_prc
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
