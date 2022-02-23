+++
title = "contract_data_merge_prc"
+++

### What does it do?
Merge data into the `contractcoverage` table using values from the `contractcoverage_ib_data` table. 
{{% expand "More Details" %}}
1. Get a count of rows in `contractcoverage` that match **customerId**/**wfId**.
2. If the count it > 0, delete the rows.
3. Get a count of rows in the `base_table_partition_info` table where
   - **customerId** matches input and
   - **partitionStatus** is `A` (Active) and
   - **partitionTag** is `BASE` and
   - **mgmtSystemType** is `CSDFIB`
4. If the count is > 0, get the **wfId** from the rows.
5. If the **wfId** is not `NULL`:
   1. Create a temp table `dup_ne_tmp` with distinct **neId**/**serialNumber** values from the `networkelement` table.
   2. If the `dup_ne_tmp` table has any rows, update **neId** values in `contractcoverage_ib_data` rows to match values from `dup_ne_tmp`
6. Insert rows into the `contractcoverage` table using values from `contractcoverage_ib_data`.
{{% /expand %}}

### Referenced Tables
- base_table_partition_info
- contractcoverage
- contractcoverage_ib_data
- data_merge_logs
- networkelement
- networkelement_ib_data

### Referenced Stored Procedures
- [log_msg_prc]({{< ILink href="/database/stored-procedures/log_msg_prc" >}})
