---
title: "관리 이벤트 로그 경고가 tooActivity에 Azure Alerts aaaMigrate | Microsoft Docs"
description: "관리 이벤트에 대한 경고는 10월 1일에 제거됩니다. 기존 경고를 마이그레이션하여 대비합니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Azure 경고 관리 이벤트 tooActivity 로그 경고 마이그레이션


> [!WARNING]
> 관리 이벤트에 대한 경고는 10월 1일 이후로 해제됩니다. 이러한 경고 하 고 그럴 경우 마이그레이션할 경우 toounderstand 아래 방향으로 hello를 사용 합니다.
>
> 

## <a name="what-is-changing"></a>변경 사항

Azure 모니터 (이전의 Azure Insights) 기능 toocreate 관리 이벤트 오프 트리거되고 알림 tooa webhook URL 또는 전자 메일 주소를 생성 하는 경고를 제공 합니다. 다음 방법 중 하나로 이러한 경고를 만들었을 수 있습니다.
* Hello 특정 리소스 종류에 대 한 Azure 포털에서에서 모니터링-> 경고 추가 경고를 "에 대 한 경고" 설정 되어 있는 너무-> "이벤트"
* Hello 추가 AzureRmLogAlertRule PowerShell cmdlet를 실행 하 여
* 직접 사용 하 여 [경고 REST API hello](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type "ManagementEventRuleCondition" 및 dataSource.odata.type = = "RuleManagementEventDataSource"
 
hello 다음 PowerShell 스크립트 반환 모든 경고 목록에서 각 경고에 설정 하는 hello 조건 뿐만 아니라 사용자 구독을 사용 하는 관리 이벤트에 합니다.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

경고 관리 이벤트에 있으면 위의 hello PowerShell cmdlet에는 일련의 다음과 같은 경고 메시지를 출력 됩니다.

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

이러한 경고 메시지는 무시할 수 있습니다. 경고 관리 이벤트에서 않아도이 PowerShell cmdlet의 hello 출력은 다음과 같이 표시 됩니다.

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

각 경고는 점선으로 구분 하 고 세부 정보 hello 경고 및 모니터링 되 고 hello 특정 규칙의 hello 리소스 ID를 포함 합니다.

이 기능은 너무 전환 되었음을[Azure 모니터 활동 로그 경고](monitoring-activity-log-alerts.md)합니다. 이러한 새 경고를 사용 하면 tooset 활동 로그 이벤트에 대 한 조건 및 새 이벤트 hello 조건과 일치 하는 경우 알림을 받게 합니다. 또한 관리 이벤트에 대한 경고에서 향상된 몇 가지 기능도 제공합니다.
* 사용 하 여 많은 경고 알림 받는 사람 ("작업")의 그룹을 다시 사용할 수 있습니다 [동작 그룹](monitoring-action-groups.md), 경고를 받을 사용자 변경의 hello 복잡성을 줄입니다.
* 작업 그룹이 있는 SMS를 사용하여 휴대폰에서 알림을 직접 받을 수 있습니다.
* [Resource Manager 템플릿을 사용하여 활동 로그 경고를 만들](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 수 있습니다.
* 조건을 만들 수 있습니다 큰 유연성과 복잡성 toomeet와 특정 요구 합니다.
* 알림이 더 빨리 전달됩니다.
 
## <a name="how-toomigrate"></a>어떻게 toomigrate
 
새 활동 로그 경고 toocreate를 제출할 수 있습니다.
* 에 따라 [어떻게에 알림 toocreate hello Azure 포털에는 가이드](monitoring-activity-log-alerts.md)
* 너무 방법에 대해 알아봅니다[리소스 관리자 템플릿을 사용 하 여 경고 만들기](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
사용자가 이전에 만든 관리 이벤트에 대해 경고를 자동으로 마이그레이션된 tooActivity 로그 경고 수 없습니다. 현재 구성 되어 있는 활동 로그 경고로이 수동으로 다시 하 관리 이벤트에 PowerShell 스크립트 toolist hello 알림을 앞 toouse hello가 필요 합니다. 이 작업은 10월 1일 전에 완료해야 합니다. 그 후에는 더 이상 관리 이벤트에 대한 경고를 Azure 구독에서 볼 수 없습니다. Azure Monitor 메트릭 경고, Application Insights 경고 및 Log Analytics 경고를 포함한 다른 유형의 Azure 경고는 이 변경으로 인해 영향을 받지 않습니다. 의문 사항이 있으면 아래에 hello 의견에 게시 합니다.


## <a name="next-steps"></a>다음 단계

* [활동 로그](monitoring-overview-activity-logs.md)에 대해 자세히 알아보기
* [Azure Portal을 통해 활동 로그 경고](monitoring-activity-log-alerts.md) 구성
* [Resource Manager를 통해 활동 로그 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 구성
* 검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)
* [서비스 알림](monitoring-service-notifications.md)에 대해 자세히 알아보기
* [작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기
