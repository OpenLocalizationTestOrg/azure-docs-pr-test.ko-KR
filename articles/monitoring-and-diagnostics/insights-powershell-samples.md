---
title: "aaaAzure 모니터 PowerShell 빠른 시작 샘플입니다. | Microsoft Docs"
description: "PowerShell tooaccess 자동 크기 조정, 경고, webhook 및 활동 로그를 검색 하는 등의 Azure 모니터 기능을 사용 합니다."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="15cca-104">Azure Monitor PowerShell 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="15cca-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="15cca-105">Azure 모니터 기능에 액세스 하는 PowerShell 명령 toohelp 샘플이 문서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="15cca-106">Azure 모니터를 사용 하면 구성 된 원격 분석 데이터의 값을 기반으로 하는 호출 웹 Url 또는 tooAutoScale 클라우드 서비스, 가상 컴퓨터 및 웹 앱 및 toosend 경고 알림.</span><span class="sxs-lookup"><span data-stu-id="15cca-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="15cca-107">Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="15cca-108">그러나 hello 네임 스페이스 및 명령을 여전히 다음 hello insights"hello"를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="15cca-109">PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="15cca-109">Set up PowerShell</span></span>
<span data-ttu-id="15cca-110">아직 하지 않는 경우 컴퓨터에 PowerShell toorun를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="15cca-111">자세한 내용은 참조 [어떻게 tooInstall 및 구성 PowerShell](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="15cca-112">이 문서의 예</span><span class="sxs-lookup"><span data-stu-id="15cca-112">Examples in this article</span></span>
<span data-ttu-id="15cca-113">hello 문서의 hello 예제 Azure 모니터 cmdlet을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="15cca-114">Hello에 Azure 모니터 PowerShell cmdlet의 전체 목록을 검토할 수도 있습니다 [Azure 모니터 (Insights) Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="15cca-115">로그인 후 구독 사용</span><span class="sxs-lookup"><span data-stu-id="15cca-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="15cca-116">첫째, tooyour Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="15cca-117">여기에서 toosign이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-117">This requires you toosign in.</span></span> <span data-ttu-id="15cca-118">로그인하면 계정, TenantID 및 기본 구독 ID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="15cca-119">모든 안녕 기본 구독의 hello 컨텍스트에서 Azure cmdlet 작업.</span><span class="sxs-lookup"><span data-stu-id="15cca-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="15cca-120">구독 tooview hello 목록을에 대 한 액세스, hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="15cca-121">toochange 작업 컨텍스트 tooa 다른 구독을 다음 명령을 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="15cca-122">구독에 대한 활동 로그 검색</span><span class="sxs-lookup"><span data-stu-id="15cca-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="15cca-123">사용 하 여 hello `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="15cca-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="15cca-124">hello 다음은 몇 가지 일반적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-124">hello following are some common examples.</span></span>

<span data-ttu-id="15cca-125">이 날짜/시간 toopresent에서 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="15cca-126">이 날짜/시간 범위의 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="15cca-127">특정 리소스 그룹에서 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="15cca-128">특정 리소스 공급자에서 이 날짜/시간 범위의 로그 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="15cca-129">특정 호출자의 모든 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="15cca-130">다음 명령을 검색 hello hello 활동 로그에서 지난 1000 개의 이벤트 hello:</span><span class="sxs-lookup"><span data-stu-id="15cca-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="15cca-131">`Get-AzureRmLog` 명령은 여러 다른 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="15cca-132">Hello 참조 `Get-AzureRmLog` 자세한 정보에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="15cca-133">`Get-AzureRmLog` 명령은 15일 간의 기록만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="15cca-134">Hello를 사용 하 여 **-MaxEvents** tooquery hello 마지막 N, 범위를 벗어나는 이벤트 15 일 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="15cca-135">15 일 보다 오래 된 tooaccess 이벤트 hello (C# 샘플 hello SDK를 사용 하 여) SDK 또는 REST API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="15cca-136">포함 되지 않은 경우 **StartTime**, hello 기본값은 **EndTime** 1 시간을 뺀 값입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="15cca-137">포함 되지 않은 경우 **EndTime**, hello 기본값은 현재 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="15cca-138">모든 시간은 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="15cca-139">경고 기록 검색</span><span class="sxs-lookup"><span data-stu-id="15cca-139">Retrieve alerts history</span></span>
<span data-ttu-id="15cca-140">쿼리할 수 이벤트, 모든 경고 tooview hello 예제 따르는 hello를 사용 하 여 Azure 리소스 관리자 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="15cca-141">특정 경고에 대 한 tooview hello 기록을 규칙 hello를 사용할 수 있습니다 `Get-AzureRmAlertHistory` cmdlet을 hello 경고 규칙의 hello 리소스 ID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="15cca-142">hello `Get-AzureRmAlertHistory` cmdlet은 다양 한 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="15cca-143">자세한 내용은 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15cca-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="15cca-144">경고 규칙에 대한 정보 검색</span><span class="sxs-lookup"><span data-stu-id="15cca-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="15cca-145">모든 명령을 수행 하는 hello 라는 "montest" 리소스 그룹에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="15cca-146">Hello 경고 규칙의 모든 hello 속성을 보기:</span><span class="sxs-lookup"><span data-stu-id="15cca-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="15cca-147">리소스 그룹에 대한 모든 경고를 검색하려면:</span><span class="sxs-lookup"><span data-stu-id="15cca-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="15cca-148">대상 리소스에 대해 설정된 모든 경고 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="15cca-149">예를 들어 VM에 설정된 모든 경고 규칙을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="15cca-150">`Get-AzureRmAlertRule` 명령은 다른 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="15cca-151">자세한 내용은 [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15cca-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="15cca-152">메트릭 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="15cca-152">Create metric alerts</span></span>
<span data-ttu-id="15cca-153">Hello를 사용할 수 있습니다 `Add-AlertRule` cmdlet toocreate 업데이트 하거나 경고 규칙을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="15cca-154">각각 `New-AzureRmAlertRuleEmail` 및 `New-AzureRmAlertRuleWebhook`를 사용하여 전자 메일 및 webhook 속성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="15cca-155">이 방법으로 작업 toohello hello 경고 규칙 cmdlet 할당 **동작** hello 경고 규칙의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="15cca-156">다음 표에서 hello hello 매개 변수를 설명 및 사용 되는 toocreate 메트릭을 사용 하는 경고 값입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="15cca-157">매개 변수</span><span class="sxs-lookup"><span data-stu-id="15cca-157">parameter</span></span> | <span data-ttu-id="15cca-158">value</span><span class="sxs-lookup"><span data-stu-id="15cca-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="15cca-159">이름</span><span class="sxs-lookup"><span data-stu-id="15cca-159">Name</span></span> |<span data-ttu-id="15cca-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="15cca-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="15cca-161">이 경고 규칙의 위치</span><span class="sxs-lookup"><span data-stu-id="15cca-161">Location of this alert rule</span></span> |<span data-ttu-id="15cca-162">미국 동부</span><span class="sxs-lookup"><span data-stu-id="15cca-162">East US</span></span> |
| <span data-ttu-id="15cca-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="15cca-163">ResourceGroup</span></span> |<span data-ttu-id="15cca-164">montest</span><span class="sxs-lookup"><span data-stu-id="15cca-164">montest</span></span> |
| <span data-ttu-id="15cca-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="15cca-165">TargetResourceId</span></span> |<span data-ttu-id="15cca-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="15cca-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="15cca-167">만들어진 hello 경고의 MetricName</span><span class="sxs-lookup"><span data-stu-id="15cca-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="15cca-168">\PhysicalDisk (_Total) \Disk writes/sec입니다. Hello 참조 `Get-MetricDefinitions` tooretrieve 메트릭 이름은 정확 하 게 hello 하는 방법에 대 한 cmdlet</span><span class="sxs-lookup"><span data-stu-id="15cca-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="15cca-169">operator</span><span class="sxs-lookup"><span data-stu-id="15cca-169">operator</span></span> |<span data-ttu-id="15cca-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="15cca-170">GreaterThan</span></span> |
| <span data-ttu-id="15cca-171">임계값(이 메트릭의 경우 수/초)</span><span class="sxs-lookup"><span data-stu-id="15cca-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="15cca-172">1</span><span class="sxs-lookup"><span data-stu-id="15cca-172">1</span></span> |
| <span data-ttu-id="15cca-173">WindowSize(h:mm:ss 형식)</span><span class="sxs-lookup"><span data-stu-id="15cca-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="15cca-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="15cca-174">00:05:00</span></span> |
| <span data-ttu-id="15cca-175">집계 (이 경우의 평균 수를 사용 하 여 hello 메트릭의 통계)</span><span class="sxs-lookup"><span data-stu-id="15cca-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="15cca-176">평균</span><span class="sxs-lookup"><span data-stu-id="15cca-176">Average</span></span> |
| <span data-ttu-id="15cca-177">사용자 지정 전자 메일(문자열 배열)</span><span class="sxs-lookup"><span data-stu-id="15cca-177">custom emails (string array)</span></span> |<span data-ttu-id="15cca-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="15cca-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="15cca-179">전자 메일 tooowners, 참가자 및 독자 보내기</span><span class="sxs-lookup"><span data-stu-id="15cca-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="15cca-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="15cca-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="15cca-181">전자 메일 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="15cca-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="15cca-182">webhook 동작 만들기</span><span class="sxs-lookup"><span data-stu-id="15cca-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="15cca-183">클래식 VM의 hello CPU % 메트릭을 hello 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="15cca-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="15cca-184">Hello 경고 규칙 검색</span><span class="sxs-lookup"><span data-stu-id="15cca-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="15cca-185">또한 hello 추가 경고 cmdlet 속성을 제공 하는 hello에 대 한 경고 규칙이 이미 있는 경우 hello 규칙을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="15cca-186">hello 매개 변수를 포함 하는 경고 규칙을 toodisable **-DisableRule**합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="15cca-187">경고에 사용 가능한 메트릭 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="15cca-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="15cca-188">Hello를 사용할 수 있습니다 `Get-AzureRmMetricDefinition` cmdlet은 특정 리소스에 대 한 모든 메트릭 tooview hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="15cca-189">hello 다음 예제에서는 이름 hello 메트릭이 포함 된 테이블 및에 대 한 hello 단위.</span><span class="sxs-lookup"><span data-stu-id="15cca-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="15cca-190">`Get-AzureRmMetricDefinition` 에 사용 가능한 옵션 전체 목록은 [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="15cca-191">자동 크기 조정 설정 및 관리</span><span class="sxs-lookup"><span data-stu-id="15cca-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="15cca-192">웹앱, VM, 클라우드 서비스 또는 가상 컴퓨터 확장 집합 같은 리소스는 자동 크기 조정 설정을 하나만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="15cca-193">그러나 각 자동 크기 조정 설정이 여러 개의 프로필을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="15cca-194">예를 들어 하나는 성능 기반 규모 프로필이고, 다른 하나는 일정 기반 프로필일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="15cca-195">각 프로필에 여러 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="15cca-196">자동 크기 조정에 대 한 자세한 내용은 참조 [방법을 응용 프로그램 tooAutoscale](../cloud-services/cloud-services-how-to-scale.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="15cca-197">사용 하 여 hello 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="15cca-198">규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-198">Create rule(s).</span></span>
2. <span data-ttu-id="15cca-199">프로필을 만들기는 이전에 만든 toohello 프로필 매핑 hello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="15cca-200">선택 사항: webhook 및 전자 메일 속성을 구성하여 자동 크기 조정에 대한 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="15cca-201">Hello 프로필 및 hello 이전 단계에서 만든 알림 매핑하여 hello 대상 리소스에 대 한 이름으로 자동 크기 조정 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="15cca-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="15cca-202">hello 다음 예제에서는 보여 hello CPU 사용률 메트릭을 사용 하 여 Windows 운영 체제에 대 한 가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 설정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="15cca-203">인스턴스 수가 증가할 것으로 규칙 tooscale 아웃을 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="15cca-204">다음으로 인스턴스 수 감소와 tooscale에서 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="15cca-205">그런 다음 hello 규칙에 대 한 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="15cca-206">webhook 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="15cca-207">전자 메일을 포함 하 여 hello 자동 크기 조정 설정에 대 한 hello 알림 속성을 만들고 이전에 만든 webhook hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="15cca-208">마지막으로 hello 자동 크기 조정 설정을 tooadd hello 프로필을 위에서 만든를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="15cca-209">자동 크기 조정 설정을 관리하는 방법에 대한 자세한 내용은 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15cca-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="15cca-210">자동 크기 조정 기록</span><span class="sxs-lookup"><span data-stu-id="15cca-210">Autoscale history</span></span>
<span data-ttu-id="15cca-211">hello 다음 예제에 나와 방법을 최근 자동 크기 조정 및 경고 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="15cca-212">Hello 활동 로그 검색 tooview hello 자동 크기 조정 기록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="15cca-213">Hello를 사용할 수 있습니다 `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve 자동 크기 조정 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="15cca-214">자세한 내용은 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15cca-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="15cca-215">자동 크기 조정 설정에 대한 세부 사항 보기</span><span class="sxs-lookup"><span data-stu-id="15cca-215">View details for an autoscale setting</span></span>
<span data-ttu-id="15cca-216">Hello를 사용할 수 있습니다 `Get-Autoscalesetting` cmdlet tooretrieve hello 자동 크기 조정 설정에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="15cca-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="15cca-217">hello 다음 예제에서는 모든 자동 크기 조정 설정에 대 한 세부 정보 myrg1' hello 리소스 그룹'.</span><span class="sxs-lookup"><span data-stu-id="15cca-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="15cca-218">hello 다음 예제 myrg1' hello 리소스 그룹'에서 모든 자동 크기 조정 설정에 대 한 세부 정보를 표시 하 고 특히 자동 크기 조정 설정 이름이 'MyScaleVMSSSetting' hello</span><span class="sxs-lookup"><span data-stu-id="15cca-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="15cca-219">자동 크기 조정 설정 제거</span><span class="sxs-lookup"><span data-stu-id="15cca-219">Remove an autoscale setting</span></span>
<span data-ttu-id="15cca-220">Hello를 사용할 수 있습니다 `Remove-Autoscalesetting` cmdlet toodelete 자동 크기 조정 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="15cca-221">활동 로그에 대한 로그 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="15cca-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="15cca-222">만들 수는 *프로필 로그* 및 활동 로그 tooa 저장소 계정에서 데이터 내보내기에 대 한 데이터 보존 기간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="15cca-223">필요에 따라 hello 데이터 tooyour 이벤트 허브를 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="15cca-224">이 기능은 현재 미리 보기 버전이며 구독당 로그 프로필을 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="15cca-225">Hello 뒤에 현재 구독 toocreate로 cmdlet을 사용 하 고 로그 프로필을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="15cca-226">또한 특정 구독을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="15cca-227">PowerShell 기본값 toohello 현재 구독을 변경할 수 있습니다 항상 사용 하 여 해당 `Set-AzureRmContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="15cca-228">해당 구독 내에서 활동 로그 tooroute 데이터 tooany 저장소 계정 또는 이벤트 허브를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="15cca-229">데이터는 JSON 형식의 blob 파일로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="15cca-230">로그 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="15cca-230">Get a log profile</span></span>
<span data-ttu-id="15cca-231">toofetch hello를 사용 하 여 기존 로그 프로필에 `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="15cca-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="15cca-232">데이터를 보존하지 않는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="15cca-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="15cca-233">로그 프로필 제거</span><span class="sxs-lookup"><span data-stu-id="15cca-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="15cca-234">데이터를 보존하는 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="15cca-234">Add a log profile with data retention</span></span>
<span data-ttu-id="15cca-235">Hello를 지정할 수 있습니다 **-RetentionInDays** hello 기간 (일)로 hello 데이터가 보존 되는 양의 정수를 사용 하 여 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="15cca-236">보존 및 이벤트 허브를 사용하여 로그 프로필 추가</span><span class="sxs-lookup"><span data-stu-id="15cca-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="15cca-237">또한 toorouting에서 사용자 데이터의 toostorage 계정 스트리밍할 수도 있습니다 것 tooan 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="15cca-238">Note는이 미리 보기 릴리스 및 hello 저장소 계정 구성이 필수 이지만 이벤트 허브 구성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="15cca-239">진단 로그 구성</span><span class="sxs-lookup"><span data-stu-id="15cca-239">Configure diagnostics logs</span></span>
<span data-ttu-id="15cca-240">여러 Azure 서비스 제공에 추가 로그 및 Azure 저장소 계정에 구성 된 toosave 데이터 일 수 있는 원격 분석 보내기 tooEvent 허브 및/또는 tooan OMS 로그 분석 작업 영역을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="15cca-241">해당 작업을 리소스 수준에서 수행할 수만 및 hello 저장소 계정 또는 이벤트 허브는 hello에 존재 해야 합니다. 동일한 지역 hello 대상 리소스로 hello 진단 설정이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15cca-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="15cca-242">진단 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="15cca-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="15cca-243">진단 설정 비활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="15cca-244">데이터를 보존하지 않도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="15cca-245">데이터를 보존하도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="15cca-246">특정 로그 범주에 대한 데이터를 보존하도록 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="15cca-247">이벤트 허브에 대한 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="15cca-248">OMS에 대한 진단 설정 활성화</span><span class="sxs-lookup"><span data-stu-id="15cca-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
