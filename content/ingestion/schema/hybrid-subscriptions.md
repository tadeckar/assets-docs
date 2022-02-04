+++
title = "Hybrid Subscriptions Schema"
+++

{{< mermaid >}}
classDiagram
  class Subscription{
    +Integer erpSalesOrderNumber
    +Integer licenseTermInMonths
    +Long subscriptionCreateDate
    +Long subscriptionProductQuantity
    +Long termEndDate
    +Long termStartDate
    +String contractEntitlementDescr
    +String contractNumber
    +String coverageStatus
    +String endCustomerGuAddressLine1
    +String endCustomerGuAddressLine2
    +String endCustomerGuAddressLine3
    +String endCustomerGuAddressLine4
    +String endCustomerGuCityName
    +String endCustomerGuCountry
    +String endCustomerGuPostalCd
    +String endCustomerGuState
    +String managedNeId
    +String monetizationTypeCd
    +String neId
    +String partnerBeGeoId
    +String partnerBeGeoName
    +String partnerBeId
    +String partnerBeName
    +String serviceLevel
    +String serviceLevelDescription
    +String serviceProgram
    +String subscriptionBillToSiteUseCustName
    +String subscriptionBillToSiteUseId
    +String subscriptionProductClass
    +String subscriptionReferenceId
    +String subscriptionStatus
    +String subscriptionType
    +String termsAndContentCd
    +String webOrderId
  }
  class HybridSubscription{
    +Long deploymentEndDate
    +Long deploymentStartDate
    +Long subscriptionEndDate
    +Long subscriptionStartDate
    +String assetCategory
    +String cavBuId
    +String cavBuName
    +String cavId
    +String cavName
    +String deploymentId
    +String offerType
    +String portalCustomerId
    +String primaryDataRegion
    +String serialNumber
    +String subscriptionRefId
    +String technology
    +String usageStatus
    +String useCaseOrworkLoad
  }
{{< /mermaid >}}
