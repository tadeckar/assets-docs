+++
title = "networkelement_sum_vw_prc"
+++

### What does it do?
{{% notice warning %}} 
This procedure will call itself recursively if a deadlock error occurs.
{{% /notice %}}
Inserts rows into the `networkelement_sum_vw` table using values from the `networkelement` table.
{{% expand "More Details" %}}
1. Count the rows in `networkelement_sum_vw` matching **customerId**/**wfId** from input.
2. If the count is > 0, delete those rows.
3. Insert rows into the `networkelement_sum_vw` using values from the `networkelement` table.
4. Update the **solution**, **usecase**, and **solutionInfo** values on rows in the `networkelement_sum_vw` using values from the `pid_solution_mapping` table.
{{% /expand %}}

### Referenced Tables
- data_merge_logs
- networkelement
- networkelement_sum_vw
- pid_solution_mapping

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/amp_log_msg_prc" >}})
