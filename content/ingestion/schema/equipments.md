+++
title = "Equipments Schema"
+++

{{< mermaid >}}
classDiagram
  class Equipment{
    +Boolean isCollector
    +Long createdAt
    +Long generatedAt
    +Long updatedAt
    +String cavbuid
    +String cavid
    +String collectedPid
    +String collectedSerialNum
    +String collectorId
    +String containingHwId
    +String createdBy
    +String customerId
    +String equipmentType
    +String genPartyId
    +String hostname
    +String hwId
    +String ibAvailabilityFlag
    +String id
    +String installProductType
    +String itemTypeCode
    +String managedNeId
    +String managementAddress
    +String manufacturer
    +String mgmtSystemAddr
    +String mgmtSystemHostname
    +String mgmtSystemId
    +String mgmtSystemType
    +String neId
    +String pceMultiPid
    +String pcePhysicalType
    +String pcePid
    +String pceProductDescription
    +String pceProductFamily
    +String pceProductName
    +String pceProductType
    +String pceRuleId
    +String prdtSetupClassificationCd
    +String productClass
    +String productDescription
    +String productFamily
    +String productId
    +String productName
    +String productType
    +String productsubtype
    +String serialNumber
    +String snasItemType
    +String snasProductFamily
    +String snasSerialNumber
    +String snasValidationCode
    +String snasValidationSource
    +String sourceNeId
    +String tags
    +String telemetryAvailablityFlag
    +String termsAndContentCd
    +String updatedBy
    +String wfId
  }
{{< /mermaid >}}
