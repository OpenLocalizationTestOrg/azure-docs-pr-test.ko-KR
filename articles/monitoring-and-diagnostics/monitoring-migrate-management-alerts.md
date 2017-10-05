---
title: "관리 이벤트에 대한 Azure 경고를 활동 로그 경고로 마이그레이션 | Microsoft Docs"
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
ms.openlocfilehash: 08a457029d3721f5c38dbcd2d2aab7d09a241d8f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="28fe9-104">관리 이벤트에 대한 Azure 경고를 활동 로그 경고로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="28fe9-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="28fe9-105">관리 이벤트에 대한 경고는 10월 1일 이후로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="28fe9-106">아래의 지침을 사용하여 이러한 경고가 있는지 파악하고 마이그레이션하세요(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="28fe9-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="28fe9-107">변경 사항</span><span class="sxs-lookup"><span data-stu-id="28fe9-107">What is changing</span></span>

<span data-ttu-id="28fe9-108">Azure Monitor(이전의 Azure Insights)에서는 관리 이벤트를 트리거하고 웹후크 URL 또는 이메일 주소에 대한 알림을 생성하는 경고를 만드는 기능을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="28fe9-109">다음 방법 중 하나로 이러한 경고를 만들었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="28fe9-110">특정 리소스 종류에 대한 Azure Portal에서 [모니터링] -> [경고] -> [경고 추가] 선택(여기서 "에 대한 경고"가 "이벤트"로 설정됨)</span><span class="sxs-lookup"><span data-stu-id="28fe9-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="28fe9-111">Add-AzureRmLogAlertRule PowerShell cmdlet 실행</span><span class="sxs-lookup"><span data-stu-id="28fe9-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="28fe9-112">odata.type = "ManagementEventRuleCondition" 및 dataSource.odata.type = "RuleManagementEventDataSource"가 포함된 [경고 REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) 직접 사용</span><span class="sxs-lookup"><span data-stu-id="28fe9-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="28fe9-113">다음 PowerShell 스크립트에서는 구독에 포함된 관리 이벤트에 대한 모든 경고 목록과 각 경고에 설정된 조건 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

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

<span data-ttu-id="28fe9-114">관리 이벤트에 대한 경고가 없는 경우 위의 PowerShell cmdlet에서는 다음과 같은 일련의 경고 메시지를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="28fe9-115">이러한 경고 메시지는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-115">These warning messages can be ignored.</span></span> <span data-ttu-id="28fe9-116">관리 이벤트에 대한 경고가 있는 경우 이 PowerShell cmdlet의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="28fe9-117">각 경고는 점선으로 구분되며, 세부 정보에는 경고의 리소스 ID와 모니터링되는 특정 규칙이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="28fe9-118">이 기능은 [Azure Monitor 활동 로그 경고](monitoring-activity-log-alerts.md)로 전환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="28fe9-119">이러한 새 경고를 사용하면 활동 로그 이벤트에 대한 조건을 설정하고 새 이벤트가 조건과 일치할 때 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="28fe9-120">또한 관리 이벤트에 대한 경고에서 향상된 몇 가지 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="28fe9-121">[작업 그룹](monitoring-action-groups.md)을 사용하여 많은 경고에서 알림 수신자 그룹("작업")을 다시 사용할 수 있으므로 경고 수신자 변경에 대한 복잡성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="28fe9-122">작업 그룹이 있는 SMS를 사용하여 휴대폰에서 알림을 직접 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="28fe9-123">[Resource Manager 템플릿을 사용하여 활동 로그 경고를 만들](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="28fe9-124">특정 요구를 충족하도록 더 효율적인 유연성과 복잡성으로 조건을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="28fe9-125">알림이 더 빨리 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="28fe9-126">마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="28fe9-126">How to migrate</span></span>
 
<span data-ttu-id="28fe9-127">새로운 활동 로그 경고를 만들려면 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="28fe9-128">[Azure Portal에서 경고를 만드는 방법에 대한 지침](monitoring-activity-log-alerts.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="28fe9-129">[Resource Manager 템플릿을 사용하여 경고를 만드는 방법](monitoring-create-activity-log-alerts-with-resource-manager-template.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="28fe9-130">이전에 만든 관리 이벤트에 대한 경고는 자동으로 활동 로그 경고로 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="28fe9-131">위의 PowerShell 스크립트를 사용하여 현재 구성한 관리 이벤트에 대한 경고를 나열하고 이를 활동 로그 경고로 수동으로 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="28fe9-132">이 작업은 10월 1일 전에 완료해야 합니다. 그 후에는 더 이상 관리 이벤트에 대한 경고를 Azure 구독에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="28fe9-133">Azure Monitor 메트릭 경고, Application Insights 경고 및 Log Analytics 경고를 포함한 다른 유형의 Azure 경고는 이 변경으로 인해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28fe9-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="28fe9-134">질문이 있으시면 아래에서 의견을 게시해 주세요.</span><span class="sxs-lookup"><span data-stu-id="28fe9-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="28fe9-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28fe9-135">Next steps</span></span>

* <span data-ttu-id="28fe9-136">[활동 로그](monitoring-overview-activity-logs.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="28fe9-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="28fe9-137">[Azure Portal을 통해 활동 로그 경고](monitoring-activity-log-alerts.md) 구성</span><span class="sxs-lookup"><span data-stu-id="28fe9-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="28fe9-138">[Resource Manager를 통해 활동 로그 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 구성</span><span class="sxs-lookup"><span data-stu-id="28fe9-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="28fe9-139">[활동 로그 경고 웹후크 스키마](monitoring-activity-log-alerts-webhook.md) 검토</span><span class="sxs-lookup"><span data-stu-id="28fe9-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="28fe9-140">[서비스 알림](monitoring-service-notifications.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="28fe9-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="28fe9-141">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="28fe9-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
