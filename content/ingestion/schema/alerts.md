+++
title = "Alerts Schema"
+++

{{< mermaid >}}
classDiagram
  class AlertsFn{
    +Long createdAt
    +Long fieldNoticeId
    +Long updatedAt
    +String cavbuid
    +String caveat
    +String cavid
    +String createdBy
    +String customerId
    +String distributionCode
    +String equipmentType
    +String fieldNoticeName
    +String hostname
    +String hwId
    +String id
    +String managementAddress
    +String neId
    +String productFamily
    +String productId
    +String serialNumber
    +String softwareType
    +String updatedBy
    +String vulnerabilityReason
    +String vulnerabilityStatus
    +String wfId
  }
  class AlertsHwEox{
    +Long createdAt
    +Long updatedAt
    +String bulletinName
    +String cavbuid
    +String cavid
    +String createdBy
    +String customerId
    +String equipmentType
    +String hardwareEoxId
    +String hostname
    +String hwId
    +String id
    +String managementAddress
    +String neId
    +String productId
    +String updatedBy
    +String wfId
  }
  class AlertsPsirt{
    +Long createdAt
    +Long psirtId
    +Long updatedAt
    +String cavbuid
    +String caveat
    +String cavid
    +String createdBy
    +String customerId
    +String cveId
    +String cvssBaseScore
    +String cxLevel
    +String equipmentType
    +String headlineName
    +String hostname
    +String hwId
    +String id
    +String managementAddress
    +String neId
    +String productFamily
    +String productId
    +String publicReleaseInd
    +String severity
    +String softwareType
    +String softwareVersion
    +String solutionIds
    +String updatedBy
    +String usecaseIds
    +String vulnerabilityReason
    +String vulnerabilityStatus
    +String wfId
  }
  class AlertsSwEox{
    +Long createdAt
    +Long updatedAt
    +String bulletinHeadline
    +String cavbuid
    +String cavid
    +String createdBy
    +String customerId
    +String equipmentType
    +String hostname
    +String id
    +String managementAddress
    +String neId
    +String productId
    +String softwareEoxId
    +String softwareType
    +String softwareVersion
    +String updatedBy
    +String wfId
  }
{{< /mermaid >}}
