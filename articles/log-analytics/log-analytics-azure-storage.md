---
title: "aaaCollect Azure 로그 분석에 대 한 로그 및 메트릭 서비스 | Microsoft Docs"
description: "Azure 리소스 toowrite 로그 및 메트릭 tooLog 분석에서 진단 유틸리티를 구성 합니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Log Analytics에서 사용할 Azure 서비스 로그 및 메트릭 수집

Azure 서비스에 대한 로그 및 메트릭을 수집하는 방법에는 다음 네 가지가 있습니다.

1. Azure 진단 직접 tooLog 분석 (*진단* 다음 표는 hello에서)
2. Azure 진단 tooAzure 저장소 tooLog 분석 (*저장소* 다음 표는 hello에서)
3. Azure 서비스에 대 한 커넥터 (*커넥터* 다음 표는 hello에서)
4. 로그 분석 (다음 표는 hello에 나열 되지 않은 서비스에 대 한 공백) toocollect 및 게시 데이터 스크립트


| 부여                 | 리소스 종류                           | 로그        | 메트릭     | 해결 방법 |
| --- | --- | --- | --- | --- |
| 응용 프로그램 게이트웨이    | Microsoft.Network/applicationGateways   | 진단 | 진단 | [Azure Application Gateway 분석](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application insights    |                                         | 커넥터   | 커넥터   | [Application Insights 커넥터](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)(미리 보기) |
| 자동화 계정     | Microsoft.Automation/AutomationAccounts | 진단 |             | [자세한 정보](../automation/automation-manage-send-joblogs-log-analytics.md)|
| 배치 계정          | Microsoft.Batch/batchAccounts           | 진단 | 진단 | |
| 클래식 Cloud Services  |                                         | 저장소     |             | [자세한 정보](log-analytics-azure-storage-iis-table.md) |
| Cognitive Services      | Microsoft.CognitiveServices/accounts    |             | 진단 | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | 진단 |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | 진단 |             | |
| 이벤트 허브 네임스페이스     | Microsoft.EventHub/namespaces           | 진단 | 진단 | |
| IoT Hub                | Microsoft.Devices/IotHubs               |             | 진단 | |
| 키 자격 증명 모음               | Microsoft.KeyVault/vaults               | 진단 |             | [KeyVault 분석](log-analytics-azure-key-vault.md) |
| 부하 분산 장치          | Microsoft.Network/loadBalancers         | 진단 |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | 진단 | 진단 | |
| 네트워크 보안 그룹 | Microsoft.Network/networksecuritygroups | 진단 |             | [Azure 네트워크 보안 그룹 분석](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| 복구 자격 증명         | Microsoft.RecoveryServices/vaults       |             |             | [Azure Recovery Services 분석(미리 보기)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Search 서비스         | Microsoft.Search/searchServices         | 진단 | 진단 | |
| 서비스 버스 네임스페이스   | Microsoft.ServiceBus/namespaces         | 진단 | 진단 | [Service Bus 분석(미리 보기)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | 저장소     |             | [Service Fabric 분석(미리 보기)](log-analytics-service-fabric.md) |
| SQL(v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | 진단 | [Azure SQL Analytics(미리 보기)](log-analytics-azure-sql.md) |
| 저장소                 |                                         |             | 스크립트      | [Azure Storage 분석(미리 보기)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| 가상 컴퓨터        | Microsoft.Compute/virtualMachines       | 내선 번호   | 내선 번호 <br> 진단  | |
| 가상 컴퓨터 확장 집합 | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | 진단 | |
| 웹 서버 팜        | Microsoft.Web/serverfarms               |             | 진단 | |
| 웹 사이트               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | 진단 | [Azure Web Apps 분석(미리 보기)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Hello 설치 좋습니다 (Linux 및 Windows) Azure 가상 컴퓨터를 모니터링, [로그 분석 VM 확장](log-analytics-azure-vm-extension.md)합니다. hello 에이전트가 가상 컴퓨터 내에서 수집 된 정보를 제공 합니다. 가상 컴퓨터 크기 집합에 대 한 hello 확장을 사용할 수도 있습니다.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Azure 진단 직접 tooLog 분석
많은 Azure 리소스가 수 toowrite 진단 로그 및 메트릭 tooLog 분석에는 hello 기본 설정으로 분석을 위해 hello 데이터를 수집할 직접입니다. Azure 진단을 사용 하는 경우 데이터가 즉시 기록 tooLog 분석 되며 필요 toofirst 쓰기 hello 데이터 toostorage 없습니다.

Azure 리소스를 지 원하는 [Azure 모니터](../monitoring-and-diagnostics/monitoring-overview.md) 해당 로그 및 메트릭 보낼 수 직접 tooLog 분석 합니다.

* 너무 hello 사용 가능한 메트릭 hello 세부 정보를 참조[지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)합니다.
* 너무 hello hello 사용 가능한 로그의 세부 정보를 참조[진단 로그에 대 한 서비스 및 스키마 지원](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)합니다.

### <a name="enable-diagnostics-with-powershell"></a>PowerShell에서 진단 사용
2016 년 11 월 (v2.3.0) hello 필요 하거나 나중에 릴리스의 [Azure PowerShell](/powershell/azure/overview)합니다.

PowerShell 예제를 방법을 따르는 hello toouse [집합 AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable 진단 네트워크 보안 그룹에 있습니다. hello 동일한 방법은 모든 지원 되는 리소스에 대 한-집합 `$resourceId` toohello 리소스 id에 대 한 진단 tooenable hello 리소스입니다.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Resource Manager 템플릿을 사용하여 진단 사용

카탈로그 항목이 생성 된 hello 진단 템플릿 비슷한 toohello 하나를 사용 하 여 아래 tooyour 로그 분석 작업 영역을 전송 하는 경우 리소스에 tooenable 진단 합니다. 이 예제는 Automation 계정에 대한 것이지만 지원되는 모든 리소스 형식에 작동합니다.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Azure 진단 toostorage 다음 tooLog 분석

일부 리소스 내에서 로그를 수집 하려는 가능한 toosend hello 로그 tooAzure 저장소 사용 되며 다음 로그 분석 tooread hello 로그 저장소를 구성 합니다.

로그 분석 צ ְ ײ Azure 저장소에서이 접근 방식을 toocollect 진단을 hello에 대 한 리소스 및 로그:

| 리소스 | 로그 |
| --- | --- |
| Service Fabric |ETWEvent <br> 작업 데이터 <br> 신뢰할 수 있는 행위자 이벤트 <br> 신뢰할 수 있는 서비스 이벤트 |
| 가상 컴퓨터 |Linux Syslog <br> Windows 이벤트 <br> IIS 로그 <br> Windows ETWEvent |
| 웹 역할  <br> 작업자 역할 |Linux Syslog <br> Windows 이벤트 <br> IIS 로그 <br> Windows ETWEvent |

> [!NOTE]
> 저장소 계정 tooa 진단을 보낼 경우 저장소 및 트랜잭션에 대 한 로그 분석 저장소 계정에서 hello 데이터를 읽을 때 일반 Azure 데이터 요금이 청구 됩니다.
>
>

참조 [이벤트에 대 한 IIS 및 테이블 저장소에 blob 저장소를 사용 하 여](log-analytics-azure-storage-iis-table.md) toolearn 로그 분석에서 이러한 로그를 수집할 수는 방법에 대 한 자세한 합니다.

## <a name="connectors-for-azure-services"></a>Azure 서비스용 커넥터

Application Insights toobe tooLog 분석을 전송에 의해 수집 된 데이터를 수 있는 Application Insights에 대 한 커넥터가 있습니다.

Hello에 대 한 자세한 [Application Insights 커넥터](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)합니다.

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>스크립트 toocollect 및 post 데이터 tooLog 분석

Toosend 로그 및 메트릭 tooLog 직접적인 방법을 제공 하지 않는 Azure 서비스에 대 한 Azure 자동화 스크립트 toocollect에서는 분석 로그 및 메트릭 hello 합니다. hello 스크립트 수 있습니다 다음 송신 hello tooLog 분석 사용 하 여 데이터 hello [데이터 수집기 API](log-analytics-data-collector-api.md)

hello Azure 템플릿 갤러리에 [Azure 자동화를 사용 하는 예제](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect 데이터 서비스 및 tooLog 분석을 전송 합니다.

## <a name="next-steps"></a>다음 단계

* [이벤트에 대 한 IIS 및 테이블 저장소에 대 한 blob 저장소를 사용 하 여](log-analytics-azure-storage-iis-table.md) tooread hello 로그 저장소 또는 IIS 로그 서 면된 tooblob 저장소 tootable 진단 유틸리티를 작성 하는 Azure 서비스에 대 한 합니다.
* [솔루션 사용](log-analytics-add-solutions.md) hello 데이터에 대 한 tooprovide 한 정보입니다.
* [검색 쿼리를 사용 하 여](log-analytics-log-searches.md) tooanalyze hello 데이터입니다.
