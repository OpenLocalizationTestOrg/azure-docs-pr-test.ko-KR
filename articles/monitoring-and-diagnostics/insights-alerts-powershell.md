---
title: "Azure 서비스-PowerShell에 대 한 경고 aaaCreate | Microsoft Docs"
description: "트리거 전자 메일 알림, 지정한 hello 조건에 해당할 때 자동화 또는 웹 사이트 Url (webhook)를 호출 합니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="cba9d-103">Azure 서비스의 Azure Monitor에서 메트릭 경고 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cba9d-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cba9d-104">포털</span><span class="sxs-lookup"><span data-stu-id="cba9d-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="cba9d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cba9d-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="cba9d-106">CLI</span><span class="sxs-lookup"><span data-stu-id="cba9d-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="cba9d-107">개요</span><span class="sxs-lookup"><span data-stu-id="cba9d-107">Overview</span></span>
<span data-ttu-id="cba9d-108">이 문서에서는 PowerShell을 사용 하 여 Azure 메트릭을를 tooset을 경고 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="cba9d-109">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="cba9d-110">**메트릭 값** -hello 트리거를 지정 된 메트릭 hello 값 두 방향에서 모두 할당 하는 임계값을 초과할 때 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="cba9d-111">즉, 트리거합니다 둘 다 때 hello 조건이 충족 먼저 되 고 다음 나중에 조건 하는 더 이상 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="cba9d-112">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="cba9d-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="cba9d-113">활동 로그 경고에 대 한 자세한 toolearn [여기를 클릭](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="cba9d-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="cba9d-114">메트릭 경고 toodo hello 다음 표시할 때 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="cba9d-115">보낼 전자 메일 알림 toohello 서비스 관리자 및 공동 관리자</span><span class="sxs-lookup"><span data-stu-id="cba9d-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="cba9d-116">사용자가 지정한 tooadditional 메일 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="cba9d-117">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="cba9d-117">call a webhook</span></span>
* <span data-ttu-id="cba9d-118">(만 hello Azure 포털)에서 Azure runbook의 실행 시작</span><span class="sxs-lookup"><span data-stu-id="cba9d-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="cba9d-119">다음을 통해 경고에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="cba9d-120">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="cba9d-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="cba9d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cba9d-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="cba9d-122">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="cba9d-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="cba9d-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="cba9d-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="cba9d-124">추가 정보를 입력할 수 있습니다 항상 ```Get-Help``` 다음 PowerShell 명령을에서 도움말을 원하는 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="cba9d-125">PowerShell에서 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="cba9d-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="cba9d-126">TooAzure에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="cba9d-127">목록을 사용할 수 있는 hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="cba9d-128">Hello 구독을 사용 하 여 작업할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="cba9d-129">그렇지 않은 경우 설정 toohello 오른쪽으로 한 hello 출력을 사용 하 여 `Get-AzureRmSubscription`합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="cba9d-130">toolist 리소스 그룹에서 다음 명령을 사용 하 여 hello에 대 한 기존 규칙:</span><span class="sxs-lookup"><span data-stu-id="cba9d-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="cba9d-131">규칙을 toocreate toohave 몇 가지 중요 한 정보가 필요 정보의 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="cba9d-132">hello **리소스 ID** hello 리소스에 대 한 원하는 tooset에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="cba9d-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="cba9d-133">hello **메트릭 정의** 해당 리소스에 대해 사용할 수 있는</span><span class="sxs-lookup"><span data-stu-id="cba9d-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="cba9d-134">한 가지 방법은 tooget hello 리소스 ID는 toouse hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="cba9d-135">Hello 리소스를 이미 만든 경우 hello 포털에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="cba9d-136">다음 hello 다음 블레이드를 선택 *속성* hello에서 *설정을* 섹션.</span><span class="sxs-lookup"><span data-stu-id="cba9d-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="cba9d-137">**리소스 ID** hello 다음 블레이드에서 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="cba9d-138">또 다른 방법은 toouse hello [Azure 리소스 탐색기](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="cba9d-139">웹앱에 대한 예제 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="cba9d-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="cba9d-140">사용할 수 있습니다 `Get-AzureRmMetricDefinition` tooview hello 목록이 특정 리소스에 대 한 모든 메트릭 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="cba9d-141">hello 다음 예제에서는 이름 hello 메트릭이 포함 된 테이블 및 해당 메트릭에 대 한 hello 단위.</span><span class="sxs-lookup"><span data-stu-id="cba9d-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="cba9d-142">Get-AzureRmMetricDefinition에 사용 가능한 모든 옵션 목록은 Get-MetricDefinitions를 실행하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="cba9d-143">경고를 설정 하는 예제 웹 사이트 리소스에 따라 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="cba9d-144">hello 경고 트리거 일관 되 게 5 분에서 다시 5 분 동안 트래픽이 받는 경우에 대 한 모든 트래픽은 받을 때마다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="cba9d-145">toocreate webhook 또는 송신 메일 경고를 트리거하는 경우에 먼저 hello 전자 메일 및/또는 webhook 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="cba9d-146">그런 다음 나중에 사용 하는 hello 규칙은 바로 만들 hello-작업 태그 hello 다음 예제와 같이 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="cba9d-147">Webhook나 이메일을 PowerShell을 통해 이미 생성된 규칙과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="cba9d-148">tooverify 경고 hello 개별 규칙 확인 하 여 올바르게 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="cba9d-149">경고를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-149">Delete your alerts.</span></span> <span data-ttu-id="cba9d-150">이러한 명령은이 문서에서 이전에 만든 hello 규칙을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="cba9d-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cba9d-151">Next steps</span></span>
* <span data-ttu-id="cba9d-152">[Azure 모니터링의 개요를 얻게](monitoring-overview.md) hello 형식의 정보를 수집 하 고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="cba9d-153">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="cba9d-154">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="cba9d-155">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="cba9d-156">가져오기는 [진단 로그를 수집 하는 작업을 간략하게](monitoring-overview-of-diagnostic-logs.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="cba9d-157">가져오기는 [메트릭 컬렉션의 개요](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="cba9d-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
