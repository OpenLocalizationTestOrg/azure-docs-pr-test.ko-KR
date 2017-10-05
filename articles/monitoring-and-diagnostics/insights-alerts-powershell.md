---
title: "Azure 서비스에 대한 경고 만들기 - PowerShell | Microsoft 문서"
description: "지정한 조건이 충족될 경우 전자 메일, 알림, 웹 사이트 URL 호출(webhook) 또는 자동화를 트리거합니다."
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
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="d285c-103">Azure 서비스의 Azure Monitor에서 메트릭 경고 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d285c-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d285c-104">포털</span><span class="sxs-lookup"><span data-stu-id="d285c-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="d285c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d285c-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="d285c-106">CLI</span><span class="sxs-lookup"><span data-stu-id="d285c-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="d285c-107">개요</span><span class="sxs-lookup"><span data-stu-id="d285c-107">Overview</span></span>
<span data-ttu-id="d285c-108">이 문서에서는 PowerShell을 사용하여 Azure 메트릭 경고를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="d285c-109">Azure 서비스 또는 Azure 서비스의 이벤트에 대한 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="d285c-110">**메트릭 값** - 이 경고는 특정 메트릭의 값이 어느 방향으로든 사용자가 할당한 임계값을 초과했을 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="d285c-111">즉 조건에 처음 부합했을 때와, 조건에 더 이상 부합하지 않게 되었을 때 모두 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="d285c-112">**활동 로그 이벤트** - *모든* 이벤트에 대해 또는 특정 이벤트가 발생했을 때만 경고를 트리거할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="d285c-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="d285c-113">활동 로그 경고에 대해 자세히 알아보려면 [여기를 클릭](monitoring-activity-log-alerts.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="d285c-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="d285c-114">트리거되면 다음을 수행하도록 메트릭 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="d285c-115">서비스 관리자 및 공동 관리자에게 이메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="d285c-116">사용자가 지정한 추가 이메일 주소로 이메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="d285c-117">webhook 호출</span><span class="sxs-lookup"><span data-stu-id="d285c-117">call a webhook</span></span>
* <span data-ttu-id="d285c-118">Azure runbook 실행 시작(현재는 Azure 포털에서만 가능)</span><span class="sxs-lookup"><span data-stu-id="d285c-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="d285c-119">다음을 통해 경고에 대한 정보를 구성하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="d285c-120">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="d285c-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="d285c-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d285c-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="d285c-122">명령줄 인터페이스(CLI)</span><span class="sxs-lookup"><span data-stu-id="d285c-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="d285c-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="d285c-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="d285c-124">```Get-Help``` 입력 후 도움말이 필요한 PowerShell 명령을 입력하면 항상 추가 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="d285c-125">PowerShell에서 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d285c-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="d285c-126">Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="d285c-127">사용 가능한 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="d285c-128">올바른 구독에서 작업 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="d285c-129">그렇지 않은 경우 `Get-AzureRmSubscription`의 출력을 사용하여 올바른 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="d285c-130">리소스 그룹에 대한 기존 규칙을 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="d285c-131">규칙을 만들려면 먼저 몇 가지 중요한 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="d285c-132">경고를 설정할 리소스의 **리소스 ID**</span><span class="sxs-lookup"><span data-stu-id="d285c-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="d285c-133">리소스에 대해 사용 가능한 **메트릭 정의**</span><span class="sxs-lookup"><span data-stu-id="d285c-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="d285c-134">리소스 ID를 가져오는 한 가지 방법은 Azure 포털을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="d285c-135">리소스를 이미 만들었다고 가정하고 포털에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="d285c-136">이 후 다음 블레이드에서 *설정* 섹션의 *속성*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="d285c-137">**리소스 ID**는 다음 블레이드의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="d285c-138">또 다른 방법은 [Azure Resource Explorer](https://resources.azure.com/)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="d285c-139">웹앱에 대한 예제 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="d285c-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="d285c-140">`Get-AzureRmMetricDefinition` 을 사용하여 특정 리소스에 대한 모든 메트릭 정의를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="d285c-141">다음은 해당 메트릭에 대한 메트릭 이름 및 단위를 사용하여 테이블을 생성하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="d285c-142">Get-AzureRmMetricDefinition에 사용 가능한 모든 옵션 목록은 Get-MetricDefinitions를 실행하여 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="d285c-143">다음 예제에서는 웹 사이트 리소스에 대한 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="d285c-144">이 경고는 어느 트래픽이나 5분 동안 계속 수신되면 항상 트리거되며, 트래픽이 5분 동안 수신되지 않으면 다시 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="d285c-145">경고가 트리거되었을 때 Webhook를 만들거나 이메일을 보내려면 먼저 이메일 및/또는 Webhook를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="d285c-146">그런 다음 즉시 다음 예제에서처럼 -Actions 태그를 사용하여 이후의 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="d285c-147">Webhook나 이메일을 PowerShell을 통해 이미 생성된 규칙과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="d285c-148">개별 규칙을 검토하여 경고가 제대로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="d285c-149">경고를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-149">Delete your alerts.</span></span> <span data-ttu-id="d285c-150">이 명령은 이 문서의 앞에서 만든 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="d285c-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d285c-151">Next steps</span></span>
* <span data-ttu-id="d285c-152">[Azure 모니터링 개요](monitoring-overview.md) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="d285c-153">[경고에서의 webhook 구성](insights-webhooks-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="d285c-154">[활동 로그 이벤트에 대한 경고 구성](monitoring-activity-log-alerts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="d285c-155">[Azure Automation Runbook](../automation/automation-starting-a-runbook.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="d285c-156">서비스의 상세 고빈도 메트릭을 수집하기 위한 [진단 로그 수집](monitoring-overview-of-diagnostic-logs.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="d285c-157">서비스를 사용 가능하며 응답할 수 있는 상태로 유지하기 위한 [메트릭 수집](insights-how-to-customize-monitoring.md) 의 개요를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d285c-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
