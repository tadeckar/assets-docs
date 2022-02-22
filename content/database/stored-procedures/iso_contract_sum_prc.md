+++
title = "iso_contract_sum_prc"
+++

### What does it do?
Syncs data from master tables to the `iso_contract_view`.
{{% expand "More Details" %}}
1. Delete all rows from `iso_contract_view` matching **customerId**/**wfId**.
2. Insert rows from `aav_subscriptions` (and `iso_pid_master` for **licenseType**) into the `iso_contract_view` table.
3. Update rows in `iso_contract_view` using values from `csdf_contracts`.
4. Update rows in `iso_contract_view` using values from `pid_solution_mapping` (set **useCaseIds** and **solutionIds**.)
5. Get a count of rows in `iso_contract_view` that are not in `iso_summary_view` (i.e. get new contracts.)
6. If count is > 0:
   1. Get a count of active partitions in `customer_wfid_info` where **module** is `CSDF_AMP_TELE`.
   2. If count is > 0, call the [iso_subscription_upd_prc]({{< ILink href="/database/stored-procedures/iso_subscription_upd_prc" >}}) and [amp_neid_update_prc]({{< ILink href="/database/stored-procedures/amp_neid_update_prc" >}}) stored procedures.
{{% /expand %}}

### Referenced Tables
- aav_subscriptions
- amp_data_merge_logs
- csdf_contracts
- customer_wfid_info
- iso_contract_view
- iso_pid_master
- iso_summary_view
- pid_solution_mapping

### Referenced Stored Procedures
- [amp_log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
- [amp_neid_update_prc]({{< ILink href="/database/stored-procedures/amp_neid_update_prc" >}})
- [iso_subscription_upd_prc]({{< ILink href="/database/stored-procedures/iso_subscription_upd_prc" >}})
