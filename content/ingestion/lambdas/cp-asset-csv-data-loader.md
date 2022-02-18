+++
title = "cp-asset-csv-data-loader"
+++

{{< GithubLink href="https://www-github3.cisco.com/cxe/cp-asset-data-pipeline/blob/505d1b955f2ccf5f2038b8023535327d4b532fda/lambda/cp-asset-csv-data-loader/lambda_function.py" >}}

Loads CSV files for the `CSDF_AMP_TELE` and `CSDF_SUBSCRIPTION` **recordType**s.


### CSDF_AMP_TELE
| **CSV File**                    | **Staging Table**                                  |
| ------------------------------- | -------------------------------------------------- |
| amp_connector_monthly_trend.csv | iso_connector_monthly_trend_stg                    | 
| amp_consumption_trend.csv       | iso_consumption_trend_stg                          | 
| amp_deployment_details.csv      | iso_depolyment_details_stg                         | 
| amp_user_login_details.csv      | iso_user_login_details_stg                         | 
| amp_user_login_trend.csv        | iso_user_login_trend_stg                           | 

### CSDF_SUBSCRIPTION
| **CSV File**                    | **Staging Table**                                  |
| ------------------------------- | -------------------------------------------------- |
| CSDFSubscription.csv            | iso_subscription_stg                               | 
