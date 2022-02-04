+++
title = "Subscriptions Schema"
+++

{{< mermaid >}}
classDiagram
  class Subscription{
    +String managedNeId
    +String neId
    +String coverageStatus
    +String serviceProgram
    +String contractNumber
    +String serviceLevel
    +String serviceLevelDescription
    +Long termEndDate
    +Long termStartDate
    +String subscriptionType
    +String termsAndContentCd
    +Long subscriptionCreateDate
    +String subscriptionStatus
    +String subscriptionReferenceId
    +String subscriptionBillToSiteUseCustName
    +String subscriptionBillToSiteUseId
    +String subscriptionProductClass
    +Long subscriptionProductQuantity
    +String endCustomerGuAddressLine1
    +String endCustomerGuAddressLine2
    +String endCustomerGuAddressLine3
    +String endCustomerGuAddressLine4
    +String endCustomerGuCityName
    +String endCustomerGuState
    +String endCustomerGuPostalCd
    +String endCustomerGuCountry
    +String partnerBeGeoId
    +String partnerBeGeoName
    +String partnerBeId
    +String partnerBeName
    +String monetizationTypeCd
    +String contractEntitlementDescr
    +Integer licenseTermInMonths
    +String webOrderId
    +Integer erpSalesOrderNumber
  }
{{< /mermaid >}}
