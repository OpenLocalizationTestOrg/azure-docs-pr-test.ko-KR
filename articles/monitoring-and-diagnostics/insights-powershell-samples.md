---
title: "Azure Monitor PowerShell 빠른 시작 샘플. | Microsoft Docs"
description: "PowerShell을 사용하여 자동 크기 조정, 경고, webhook 및 활동 로그 검색 등의 Azure Monitor 기능에 액세스합니다."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="0a95b-104">Azure Monitor PowerShell 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="0a95b-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="0a95b-105">이 문서에서는 Azure Monitor 기능에 액세스할 수 있는 샘플 PowerShell 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="0a95b-106">Azure Monitor를 통해 Cloud Services, Virtual Machines 및 Web Apps의 크기를 자동으로 조정하고, 구성된 원격 분석 데이터의 값을 기반으로 경고 알림을 보내거나 웹 URL을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="0a95b-107">Azure Monitor는 2016년 9월 25일까지는 "Azure Insights"로 지칭했던 제품의 새로운 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="0a95b-108">하지만 네임스페이스와 다음 명령에서는 "insights"를 계속 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="0a95b-109">PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="0a95b-109">Set up PowerShell</span></span>
<span data-ttu-id="0a95b-110">아직 PowerShell이 컴퓨터에서 실행되도록 설정하지 않았으면 지금 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="0a95b-111">자세한 내용은 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="0a95b-112">이 문서의 예</span><span class="sxs-lookup"><span data-stu-id="0a95b-112">Examples in this article</span></span>
<span data-ttu-id="0a95b-113">문서의 예에서는 Azure Monitor cmdlet을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="0a95b-114">[Azure Monitor(Insights) Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx)에서 Azure Monitor PowerShell cmdlet의 전체 목록을 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="0a95b-115">로그인 후 구독 사용</span><span class="sxs-lookup"><span data-stu-id="0a95b-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="0a95b-116">먼저 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="0a95b-117">그러려면 로그인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-117">This requires you to sign in.</span></span> <span data-ttu-id="0a95b-118">로그인하면 계정, TenantID 및 기본 구독 ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="0a95b-119">모든 Azure cmdlet은 기본 구독의 컨텍스트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="0a95b-120">액세스할 수 있는 구독 목록을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="0a95b-121">작업 컨텍스트를 다른 구독으로 변경하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="0a95b-122">구독에 대한 활동 로그 검색</span><span class="sxs-lookup"><span data-stu-id="0a95b-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="0a95b-123">`Get-AzureRmLog` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="0a95b-124">다음은 몇 가지 일반적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-124">The following are some common examples.</span></span>

<span data-ttu-id="0a95b-125">이 날짜/시간부터 현재까지의 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="0a95b-126">이 날짜/시간 범위의 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="0a95b-127">특정 리소스 그룹에서 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="0a95b-128">특정 리소스 공급자에서 이 날짜/시간 범위의 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="0a95b-129">특정 호출자의 모든 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="0a95b-130">다음 명령은 활동 로그에서 마지막 1,000개 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="0a95b-131">`Get-AzureRmLog` 명령은 여러 다른 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="0a95b-132">자세한 내용은 `Get-AzureRmLog` 참조를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="0a95b-133">`Get-AzureRmLog` 명령은 15일 간의 기록만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="0a95b-134">**-MaxEvents** 매개 변수를 사용하면 15일 이후의 N개 이벤트를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="0a95b-135">15일이 지난 이벤트에 액세스하려면 REST API 또는 SDK(SDK를 사용하는 C# 샘플)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="0a95b-136">**StartTime**을 포함하지 않으면 **EndTime**에서 1시간을 뺀 값이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="0a95b-137">**EndTime**을 포함하지 않으면 현재 시간이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="0a95b-138">모든 시간은 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="0a95b-139">경고 기록 검색</span><span class="sxs-lookup"><span data-stu-id="0a95b-139">Retrieve alerts history</span></span>
<span data-ttu-id="0a95b-140">모든 경고 이벤트를 보려면 다음 예제를 사용하여 Azure Resource Manager 로그를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="0a95b-141">특정 경고 규칙에 대한 기록을 보려면 `Get-AzureRmAlertHistory` cmdlet을 사용하여 경고 규칙의 리소스 ID를 전달하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="0a95b-142">`Get-AzureRmAlertHistory` cmdlet은 다양한 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="0a95b-143">자세한 내용은 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="0a95b-144">경고 규칙에 대한 정보 검색</span><span class="sxs-lookup"><span data-stu-id="0a95b-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="0a95b-145">다음 명령은 모두 "montest"라는 리소스 그룹에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="0a95b-146">경고 규칙의 모든 속성을 보려면:</span><span class="sxs-lookup"><span data-stu-id="0a95b-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="0a95b-147">리소스 그룹에 대한 모든 경고를 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="0a95b-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="0a95b-148">대상 리소스에 대해 설정된 모든 경고 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="0a95b-149">예를 들어 VM에 설정된 모든 경고 규칙을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="0a95b-150">`Get-AzureRmAlertRule` 명령은 다른 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="0a95b-151">자세한 내용은 [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="0a95b-152">메트릭 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="0a95b-152">Create metric alerts</span></span>
<span data-ttu-id="0a95b-153">`Add-AlertRule` cmdlet을 사용하여 경고 규칙을 만들고, 업데이트하고, 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="0a95b-154">각각 `New-AzureRmAlertRuleEmail` 및 `New-AzureRmAlertRuleWebhook`를 사용하여 전자 메일 및 webhook 속성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="0a95b-155">경고 규칙 cmdlet에서, 이러한 것들을 경고 규칙의 **동작** 속성에 동작으로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="0a95b-156">다음은 메트릭을 사용하여 경고를 만드는 데 사용되는 매개 변수 및 값을 설명하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="0a95b-157">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0a95b-157">parameter</span></span> | <span data-ttu-id="0a95b-158">value</span><span class="sxs-lookup"><span data-stu-id="0a95b-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="0a95b-159">이름</span><span class="sxs-lookup"><span data-stu-id="0a95b-159">Name</span></span> |<span data-ttu-id="0a95b-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="0a95b-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="0a95b-161">이 경고 규칙의 위치</span><span class="sxs-lookup"><span data-stu-id="0a95b-161">Location of this alert rule</span></span> |<span data-ttu-id="0a95b-162">미국 동부</span><span class="sxs-lookup"><span data-stu-id="0a95b-162">East US</span></span> |
| <span data-ttu-id="0a95b-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0a95b-163">ResourceGroup</span></span> |<span data-ttu-id="0a95b-164">montest</span><span class="sxs-lookup"><span data-stu-id="0a95b-164">montest</span></span> |
| <span data-ttu-id="0a95b-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="0a95b-165">TargetResourceId</span></span> |<span data-ttu-id="0a95b-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="0a95b-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="0a95b-167">생성된 경고의 MetricName</span><span class="sxs-lookup"><span data-stu-id="0a95b-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="0a95b-168">\PhysicalDisk (_Total) \Disk writes/sec입니다. 참조는 `Get-MetricDefinitions` 메트릭 이름은 정확 하 게 검색 하는 방법에 대 한 cmdlet</span><span class="sxs-lookup"><span data-stu-id="0a95b-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="0a95b-169">operator</span><span class="sxs-lookup"><span data-stu-id="0a95b-169">operator</span></span> |<span data-ttu-id="0a95b-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="0a95b-170">GreaterThan</span></span> |
| <span data-ttu-id="0a95b-171">임계값(이 메트릭의 경우 수/초)</span><span class="sxs-lookup"><span data-stu-id="0a95b-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="0a95b-172">1</span><span class="sxs-lookup"><span data-stu-id="0a95b-172">1</span></span> |
| <span data-ttu-id="0a95b-173">WindowSize(h:mm:ss 형식)</span><span class="sxs-lookup"><span data-stu-id="0a95b-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="0a95b-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="0a95b-174">00:05:00</span></span> |
| <span data-ttu-id="0a95b-175">집계(이 경우, 평균 횟수를 사용하는 메트릭 통계)</span><span class="sxs-lookup"><span data-stu-id="0a95b-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="0a95b-176">평균</span><span class="sxs-lookup"><span data-stu-id="0a95b-176">Average</span></span> |
| <span data-ttu-id="0a95b-177">사용자 지정 전자 메일(문자열 배열)</span><span class="sxs-lookup"><span data-stu-id="0a95b-177">custom emails (string array)</span></span> |<span data-ttu-id="0a95b-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="0a95b-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="0a95b-179">소유자, 참가자 및 일기 권한자에게 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="0a95b-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="0a95b-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="0a95b-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="0a95b-181">전자 메일 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="0a95b-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="0a95b-182">webhook 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="0a95b-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="0a95b-183">클래식 VM에 CPU% 메트릭에 대한 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="0a95b-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="0a95b-184">경고 규칙 검색</span><span class="sxs-lookup"><span data-stu-id="0a95b-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="0a95b-185">지정된 속성에 대한 경고 규칙이 이미 있으면 경고 추가 cmdlet도 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="0a95b-186">경고 규칙을 비활성화하려면 **-DisableRule**매개 변수를 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="0a95b-187">경고에 사용 가능한 메트릭 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a95b-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="0a95b-188">`Get-AzureRmMetricDefinition` cmdlet을 사용하여 특정 리소스에 대한 모든 메트릭 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="0a95b-189">다음은 메트릭 이름 및 단위를 사용하여 테이블을 생성하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="0a95b-190">`Get-AzureRmMetricDefinition` 에 사용 가능한 옵션 전체 목록은 [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="0a95b-191">자동 크기 조정 설정 및 관리</span><span class="sxs-lookup"><span data-stu-id="0a95b-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="0a95b-192">웹앱, VM, 클라우드 서비스 또는 가상 컴퓨터 확장 집합 같은 리소스는 자동 크기 조정 설정을 하나만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="0a95b-193">그러나 각 자동 크기 조정 설정이 여러 개의 프로필을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="0a95b-194">예를 들어 하나는 성능 기반 규모 프로필이고, 다른 하나는 일정 기반 프로필일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="0a95b-195">각 프로필에 여러 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="0a95b-196">자동 크기 조정에 대한 자세한 내용은 [응용 프로그램의 크기 자동 조정 방법](../cloud-services/cloud-services-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="0a95b-197">수행할 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="0a95b-198">규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-198">Create rule(s).</span></span>
2. <span data-ttu-id="0a95b-199">이전에 만든 규칙을 프로필에 매핑하는 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="0a95b-200">선택 사항: webhook 및 전자 메일 속성을 구성하여 자동 크기 조정에 대한 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="0a95b-201">이전 단계에서 만든 프로필과 알림을 매핑하여 대상 리소스에 대한 자동 크기 조정 설정과 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="0a95b-202">다음은 CPU 사용률 메트릭을 사용하여 Windows 운영 체제 기반 가상 컴퓨터 확장 집합에 대한 자동 크기 조정 설정을 만드는 방법을 보여 주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="0a95b-203">먼저, 인스턴스 수가 증가하는 규모 확장 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="0a95b-204">다음으로, 인스턴스 수가 감소하는 규모 감축 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="0a95b-205">그런 다음, 규칙에 대한 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="0a95b-206">webhook 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="0a95b-207">앞에서 만든 전자 메일 및 webhook을 포함하여 자동 크기 조정 설정에 대한 알림 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="0a95b-208">마지막으로, 위에서 만든 프로필을 추가하는 자동 크기 조정 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="0a95b-209">자동 크기 조정 설정을 관리하는 방법에 대한 자세한 내용은 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="0a95b-210">자동 크기 조정 기록</span><span class="sxs-lookup"><span data-stu-id="0a95b-210">Autoscale history</span></span>
<span data-ttu-id="0a95b-211">다음은 최근에 있었던 자동 크기 조정 및 경고 이벤트를 보는 방법을 알려주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="0a95b-212">활동 로그 검색을 사용하여 자동 크기 조정 기록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="0a95b-213">`Get-AzureRmAutoScaleHistory` cmdlet을 사용하여 자동 크기 조정 기록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="0a95b-214">자세한 내용은 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a95b-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="0a95b-215">자동 크기 조정 설정에 대한 세부 사항 보기</span><span class="sxs-lookup"><span data-stu-id="0a95b-215">View details for an autoscale setting</span></span>
<span data-ttu-id="0a95b-216">`Get-Autoscalesetting` cmdlet을 사용하여 자동 크기 조정 설정에 대한 자세한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="0a95b-217">다음은 리소스 그룹 'myrg1'의 모든 자동 크기 조정 설정에 대한 세부 정보를 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="0a95b-218">다음은 리소스 그룹 'myrg1'의 모든 자동 크기 조정 설정과 특히 'MyScaleVMSSSetting'라는 자동 크기 조정 설정에 대한 세부 정보를 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="0a95b-219">자동 크기 조정 설정 제거</span><span class="sxs-lookup"><span data-stu-id="0a95b-219">Remove an autoscale setting</span></span>
<span data-ttu-id="0a95b-220">`Remove-Autoscalesetting` cmdlet을 사용하여 자동 크기 조정 설정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="0a95b-221">활동 로그에 대한 로그 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="0a95b-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="0a95b-222">*로그 프로필*을 만들어 활동 로그에서 저장소 계정으로 데이터를 내보내고 해당 데이터의 보존 기간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="0a95b-223">필요에 따라 이벤트 허브로 데이터를 스트리밍할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="0a95b-224">이 기능은 현재 미리 보기 버전이며 구독당 로그 프로필을 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="0a95b-225">현재 구독과 함께 다음 cmdlet을 사용하여 로그 프로필을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="0a95b-226">또한 특정 구독을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="0a95b-227">PowerShell이 현재 구독의 기본값이지만 언제든지 `Set-AzureRmContext`명령을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="0a95b-228">해당 구독 내의 저장소 계정 또는 이벤트 허브로 데이터를 라우팅하도록 활동 로그를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="0a95b-229">데이터는 JSON 형식의 blob 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="0a95b-230">로그 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a95b-230">Get a log profile</span></span>
<span data-ttu-id="0a95b-231">기존 로그 프로필을 가져오려면 `Get-AzureRmLogProfile` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="0a95b-232">데이터를 보존하지 않는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="0a95b-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="0a95b-233">로그 프로필 제거</span><span class="sxs-lookup"><span data-stu-id="0a95b-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="0a95b-234">데이터를 보존하는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="0a95b-234">Add a log profile with data retention</span></span>
<span data-ttu-id="0a95b-235">**-RetentionInDays** 속성을 양의 정수로 지정하여 데이터가 보존되는 일 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="0a95b-236">보존 및 이벤트 허브를 사용하여 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="0a95b-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="0a95b-237">데이터를 저장소 계정으로 라우팅하는 방법 외에도 데이터를 이벤트 허브에 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="0a95b-238">이 미리 보기 릴리스에서 저장소 계정 구성은 필수지만 이벤트 허브 구성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="0a95b-239">진단 로그 구성</span><span class="sxs-lookup"><span data-stu-id="0a95b-239">Configure diagnostics logs</span></span>
<span data-ttu-id="0a95b-240">여러 Azure 서비스는 Azure Storage 계정에 데이터를 저장하고, 이벤트 허브에 보내거나 OMS 로그 분석 작업 영역에 보낼 수 있도록 구성된 추가 로그와 원격 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="0a95b-241">이 작업은 리소스 수준에서만 수행할 수 있으며 저장소 계정 또는 이벤트 허브가 진단 설정이 구성되는 대상 리소스와 같은 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a95b-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="0a95b-242">진단 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a95b-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="0a95b-243">진단 설정 비활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="0a95b-244">데이터를 보존하지 않도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="0a95b-245">데이터를 보존하도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="0a95b-246">특정 로그 범주에 대한 데이터를 보존하도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="0a95b-247">이벤트 허브에 대한 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="0a95b-248">OMS에 대한 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="0a95b-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
