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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="033fb-104">Azure 경고 관리 이벤트 tooActivity 로그 경고 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="033fb-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="033fb-105">관리 이벤트에 대한 경고는 10월 1일 이후로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="033fb-106">이러한 경고 하 고 그럴 경우 마이그레이션할 경우 toounderstand 아래 방향으로 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="033fb-107">변경 사항</span><span class="sxs-lookup"><span data-stu-id="033fb-107">What is changing</span></span>

<span data-ttu-id="033fb-108">Azure 모니터 (이전의 Azure Insights) 기능 toocreate 관리 이벤트 오프 트리거되고 알림 tooa webhook URL 또는 전자 메일 주소를 생성 하는 경고를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="033fb-109">다음 방법 중 하나로 이러한 경고를 만들었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="033fb-110">Hello 특정 리소스 종류에 대 한 Azure 포털에서에서 모니터링-> 경고 추가 경고를 "에 대 한 경고" 설정 되어 있는 너무-> "이벤트"</span><span class="sxs-lookup"><span data-stu-id="033fb-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="033fb-111">Hello 추가 AzureRmLogAlertRule PowerShell cmdlet를 실행 하 여</span><span class="sxs-lookup"><span data-stu-id="033fb-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="033fb-112">직접 사용 하 여 [경고 REST API hello](http://docs.microsoft.com/rest/api/monitor/alertrules) odata.type "ManagementEventRuleCondition" 및 dataSource.odata.type = = "RuleManagementEventDataSource"</span><span class="sxs-lookup"><span data-stu-id="033fb-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="033fb-113">hello 다음 PowerShell 스크립트 반환 모든 경고 목록에서 각 경고에 설정 하는 hello 조건 뿐만 아니라 사용자 구독을 사용 하는 관리 이벤트에 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="033fb-114">경고 관리 이벤트에 있으면 위의 hello PowerShell cmdlet에는 일련의 다음과 같은 경고 메시지를 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="033fb-115">이러한 경고 메시지는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-115">These warning messages can be ignored.</span></span> <span data-ttu-id="033fb-116">경고 관리 이벤트에서 않아도이 PowerShell cmdlet의 hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="033fb-117">각 경고는 점선으로 구분 하 고 세부 정보 hello 경고 및 모니터링 되 고 hello 특정 규칙의 hello 리소스 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="033fb-118">이 기능은 너무 전환 되었음을[Azure 모니터 활동 로그 경고](monitoring-activity-log-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="033fb-119">이러한 새 경고를 사용 하면 tooset 활동 로그 이벤트에 대 한 조건 및 새 이벤트 hello 조건과 일치 하는 경우 알림을 받게 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="033fb-120">또한 관리 이벤트에 대한 경고에서 향상된 몇 가지 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="033fb-121">사용 하 여 많은 경고 알림 받는 사람 ("작업")의 그룹을 다시 사용할 수 있습니다 [동작 그룹](monitoring-action-groups.md), 경고를 받을 사용자 변경의 hello 복잡성을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="033fb-122">작업 그룹이 있는 SMS를 사용하여 휴대폰에서 알림을 직접 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="033fb-123">[Resource Manager 템플릿을 사용하여 활동 로그 경고를 만들](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="033fb-124">조건을 만들 수 있습니다 큰 유연성과 복잡성 toomeet와 특정 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="033fb-125">알림이 더 빨리 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="033fb-126">어떻게 toomigrate</span><span class="sxs-lookup"><span data-stu-id="033fb-126">How toomigrate</span></span>
 
<span data-ttu-id="033fb-127">새 활동 로그 경고 toocreate를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="033fb-128">에 따라 [어떻게에 알림 toocreate hello Azure 포털에는 가이드](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="033fb-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="033fb-129">너무 방법에 대해 알아봅니다[리소스 관리자 템플릿을 사용 하 여 경고 만들기](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="033fb-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="033fb-130">사용자가 이전에 만든 관리 이벤트에 대해 경고를 자동으로 마이그레이션된 tooActivity 로그 경고 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="033fb-131">현재 구성 되어 있는 활동 로그 경고로이 수동으로 다시 하 관리 이벤트에 PowerShell 스크립트 toolist hello 알림을 앞 toouse hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="033fb-132">이 작업은 10월 1일 전에 완료해야 합니다. 그 후에는 더 이상 관리 이벤트에 대한 경고를 Azure 구독에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="033fb-133">Azure Monitor 메트릭 경고, Application Insights 경고 및 Log Analytics 경고를 포함한 다른 유형의 Azure 경고는 이 변경으로 인해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="033fb-134">의문 사항이 있으면 아래에 hello 의견에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="033fb-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="033fb-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="033fb-135">Next steps</span></span>

* <span data-ttu-id="033fb-136">[활동 로그](monitoring-overview-activity-logs.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="033fb-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="033fb-137">[Azure Portal을 통해 활동 로그 경고](monitoring-activity-log-alerts.md) 구성</span><span class="sxs-lookup"><span data-stu-id="033fb-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="033fb-138">[Resource Manager를 통해 활동 로그 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md) 구성</span><span class="sxs-lookup"><span data-stu-id="033fb-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="033fb-139">검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="033fb-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="033fb-140">[서비스 알림](monitoring-service-notifications.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="033fb-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="033fb-141">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="033fb-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
