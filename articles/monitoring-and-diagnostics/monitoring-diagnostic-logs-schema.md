---
title: "aaaAzure 진단 로그 지원 서비스 및 스키마 | Microsoft Docs"
description: "Azure 진단 로그에 대 한 hello 지원 되는 서비스 및 이벤트 스키마를 이해 합니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: a3cbf5267e1bd0dc257f4fb4f42c323644046a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-services-schemas-and-categories-for-azure-diagnostic-logs"></a>Azure 진단 로그에 대해 지원되는 서비스, 스키마 및 범주

[Azure 리소스 진단 로그](monitoring-overview-of-diagnostic-logs.md) 는 해당 리소스의 hello 작업을 설명 하는 Azure 리소스에서 내보낸 로그입니다. 이러한 로그는 리소스 종류별로 다릅니다. 이 문서에서는 hello 집합이 내보내는 각 서비스에 의해 이벤트에 대 한 지원 되는 서비스 및 이벤트 스키마에 설명 합니다. 또한 이 문서에는 리소스 종류당 사용 가능한 로그 범주의 전체 목록이 포함되어 있습니다.

## <a name="supported-services-and-schemas-for-resource-diagnostic-logs"></a>리소스 진단 로그에 대해 지원되는 서비스 및 스키마
리소스 진단 로그에 대 한 hello 스키마 hello 리소스 및 로그 범주에 따라 달라 집니다.   

| 부여 | 스키마 및 문서 |
| --- | --- |
| API Management | 스키마를 사용할 수 없음 |
| 응용 프로그램 게이트웨이 |[Application Gateway에 대한 진단 로깅](../application-gateway/application-gateway-diagnostics.md) |
| Azure Automation |[Azure Automation에 대한 Log Analytics](../automation/automation-manage-send-joblogs-log-analytics.md) |
| Azure Batch |[Azure Batch 진단 로깅](../batch/batch-diagnostics.md) |
| Customer Insights | 스키마를 사용할 수 없음 |
| Content Delivery Network | 스키마를 사용할 수 없음 |
| CosmosDB | 스키마를 사용할 수 없음 |
| 데이터 레이크 분석 |[Azure Data Lake Analytics에 대한 진단 로그에 액세스](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| 데이터 레이크 저장소 |[Azure Data Lake Store에 대한 진단 로그에 액세스](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| Event Hubs |[Azure Event Hubs 진단 로그](../event-hubs/event-hubs-diagnostic-logs.md) |
| 키 자격 증명 모음 |[Azure Key Vault 로깅](../key-vault/key-vault-logging.md) |
| 부하 분산 장치 |[Azure Load Balancer에 대한 Log analytics](../load-balancer/load-balancer-monitor-log.md) |
| Logic Apps |[Logic Apps B2B 사용자 지정 추적 스키마](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| 네트워크 보안 그룹 |[NSG(네트워크 보안 그룹)에 대한 로그 분석](../virtual-network/virtual-network-nsg-manage-log.md) |
| Recovery Services | 스키마를 사용할 수 없음|
| 검색 |[검색 트래픽 분석 설정 및 사용](../search/search-traffic-analytics.md) |
| 서버 관리 | 스키마를 사용할 수 없음 |
| Service Bus |[Azure Service Bus 진단 로그](../service-bus-messaging/service-bus-diagnostic-logs.md) |
| Stream Analytics |[작업 진단 로그](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |

## <a name="supported-log-categories-per-resource-type"></a>각 리소스 유형별 지원되는 로그 범주
|리소스 종류|Category|범주 표시 이름|
|---|---|---|
|Microsoft.ApiManagement/service|GatewayLogs|로그 관련된 tooApiManagement 게이트웨이|
|Microsoft.Automation/automationAccounts|JobLogs|작업 로그|
|Microsoft.Automation/automationAccounts|JobStreams|작업 스트림|
|Microsoft.Automation/automationAccounts|DscNodeStatus|디스크 노드 상태|
|Microsoft.Batch/batchAccounts|ServiceLog|서비스 로그|
|Microsoft.Cdn/profiles/endpoints|CoreAnalytics|Hello 끝점의 예: 대역폭, 송신, 등 hello 메트릭을 가져옵니다.|
|Microsoft.CustomerInsights/hubs|AuditEvents|AuditEvents|
|Microsoft.DataLakeAnalytics/accounts|감사|감사 로그|
|Microsoft.DataLakeAnalytics/accounts|요청|요청 로그|
|Microsoft.DataLakeStore/accounts|감사|감사 로그|
|Microsoft.DataLakeStore/accounts|요청|요청 로그|
|Microsoft.DocumentDB/databaseAccounts|DataPlaneRequests|DataPlaneRequests|
|Microsoft.EventHub/namespaces|ArchiveLogs|보관 로그|
|Microsoft.EventHub/namespaces|OperationalLogs|작업 로그|
|Microsoft.EventHub/namespaces|AutoScaleLogs|자동 크기 조정 로그|
|Microsoft.KeyVault/vaults|AuditEvent|감사 로그|
|Microsoft.Logic/workflows|WorkflowRuntime|워크플로 런타임 진단 이벤트|
|Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|통합 계정 이벤트 추적|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|네트워크 보안 그룹 이벤트|
|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|네트워크 보안 그룹 규칙 카운터|
|Microsoft.Network/loadBalancers|LoadBalancerAlertEvent|부하 분산 장치 경고 이벤트|
|Microsoft.Network/loadBalancers|LoadBalancerProbeHealthStatus|부하 분산 장치 프로브 상태|
|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|Application Gateway 액세스 로그|
|Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|Application Gateway 성능 로그|
|Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|Application Gateway 방화벽 로그|
|Microsoft.RecoveryServices/Vaults|AzureBackupReport|Azure Backup 보고 데이터|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryJobs|Azure Site Recovery 작업|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryEvents|Azure Site Recovery 이벤트|
|Microsoft.RecoveryServices/Vaults|AzureSiteRecoveryReplicatedItems|Azure Site Recovery 복제된 항목|
|Microsoft.Search/searchServices|OperationLogs|작업 로그|
|Microsoft.ServiceBus/namespaces|OperationalLogs|작업 로그|
|Microsoft.StreamAnalytics/streamingjobs|실행|실행|
|Microsoft.StreamAnalytics/streamingjobs|작성|작성|

## <a name="next-steps"></a>다음 단계

* [진단 로그에 대해 자세히 알아보기](monitoring-overview-of-diagnostic-logs.md)
* [진단 로그 리소스를 너무 스트림**이벤트 허브**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Hello Azure 모니터 REST API를 사용 하 여 리소스 진단 설정 변경](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Azure Storage에서 Log Analytics를 사용하여 로그 분석](../log-analytics/log-analytics-azure-storage.md)
