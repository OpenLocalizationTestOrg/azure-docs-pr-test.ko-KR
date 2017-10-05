---
title: "OMS Log Analytics에 Azure Automation 작업 데이터 전달 | Microsoft Docs"
description: "이 문서에서는 작업 상태 및 runbook 작업 스트림을 Microsoft Operations Management Suite Log Analytics로 보내 통찰력 및 관리를 강화하는 방법을 알아봅니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: 2c0ca7fc332963e5a5db3c20c400ed877ae0cc54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-to-log-analytics-oms"></a><span data-ttu-id="b916f-103">자동화에서 Log Analytics로 작업 상태 및 작업 스트림 전달(OMS)</span><span class="sxs-lookup"><span data-stu-id="b916f-103">Forward job status and job streams from Automation to Log Analytics (OMS)</span></span>
<span data-ttu-id="b916f-104">자동화에서 Microsoft Operations Management Suite(OMS) Log Analytics 작업 영역으로 runbook 작업 상태 및 작업 스트림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-104">Automation can send runbook job status and job streams to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="b916f-105">개별 작업에 대해 Azure Portal에서 또는 PowerShell을 사용하여 작업 로그 및 작업 스트림을 볼 수 있으며 이를 통해 보다 간단한 조사가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-105">Job logs and job streams are visible in the Azure portal, or with PowerShell, for individual jobs and this allows you to perform simple investigations.</span></span> <span data-ttu-id="b916f-106">이제 Log Anaytics를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="b916f-107">자동화 작업에 대한 통찰력 확보</span><span class="sxs-lookup"><span data-stu-id="b916f-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="b916f-108">Runbook 작업 상태(예: 실패 또는 일시 중단)를 기반으로 전자 메일 또는 경고 트리거</span><span class="sxs-lookup"><span data-stu-id="b916f-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="b916f-109">작업 스트림에서 고급 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="b916f-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="b916f-110">자동화 계정 간에 작업 상호 연결</span><span class="sxs-lookup"><span data-stu-id="b916f-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="b916f-111">시간별 작업 기록 시각화</span><span class="sxs-lookup"><span data-stu-id="b916f-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="b916f-112">필수 구성 요소 및 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="b916f-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="b916f-113">Automation 로그를 Log Analytics로 보내려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-113">To start sending your Automation logs to Log Analytics, you need:</span></span>

1. <span data-ttu-id="b916f-114">[Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)의 2016년 11월(v2.3.0) 이후 릴리스</span><span class="sxs-lookup"><span data-stu-id="b916f-114">The November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="b916f-115">Log Analytics 작업 영역.</span><span class="sxs-lookup"><span data-stu-id="b916f-115">A Log Analytics workspace.</span></span> <span data-ttu-id="b916f-116">자세한 내용은 [Log Analytics 시작](../log-analytics/log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b916f-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="b916f-117">Azure Automation 계정에 대한 ResourceId</span><span class="sxs-lookup"><span data-stu-id="b916f-117">The ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="b916f-118">Azure Automation 계정 및 Log Analytics 작업 영역에 대한 ResourceId를 찾으려면 다음 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-118">To find the ResourceId for your Azure Automation account and Log Analytics workspace, run the following PowerShell:</span></span>

```powershell
# Find the ResourceId for the Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find the ResourceId for the Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="b916f-119">여러 Automation 계정 또는 작업 영역이 있는 경우 이전 명령의 출력에서 구성해야 하는 *Name*을 찾고 *ResourceId* 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-119">If you have multiple Automation accounts, or workspaces, in the output of the preceding commands, find the *Name* you need to configure and copy the value for *ResourceId*.</span></span>

<span data-ttu-id="b916f-120">Automation 계정의 *Name*을 찾으려면 Azure Portal의 **Automation 계정** 블레이드에서 Automation 계정을 선택한 다음 **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-120">If you need to find the *Name* of your Automation account, in the Azure portal select your Automation account from the **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="b916f-121">**계정 설정** 아래에 있는 **모든 설정** 블레이드에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-121">From the **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="b916f-122">**속성** 블레이드에서 이들 값을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-122">In the **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="b916f-123">![자동화 계정 속성](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b916f-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="b916f-124">Log Analytics와의 통합 설정</span><span class="sxs-lookup"><span data-stu-id="b916f-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="b916f-125">컴퓨터의 **시작** 화면에서 **Windows PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-125">On your computer, start **Windows PowerShell** from the **Start** screen.</span></span>  
2. <span data-ttu-id="b916f-126">다음 PowerShell을 복사하고, `$workspaceId` 및 `$automationAccountId` 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-126">Copy and paste the following PowerShell, and edit the value for the `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="b916f-127">`-Environment` 매개 변수에 유효한 값은 사용 중인 클라우드 환경에 따라 *AzureCloud* 또는 *AzureUSGovernment*입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-127">For the `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on the cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="b916f-128">이 스크립트를 실행한 후 새 JobLogs 또는 쓰고 있는 JobStreams의 10분 이내에 Log Analytics에 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="b916f-129">로그를 보려면 Log Analytics 로그 검색에서 다음 쿼리를 실행합니다. `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="b916f-129">To see the logs, run the following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="b916f-130">구성 확인</span><span class="sxs-lookup"><span data-stu-id="b916f-130">Verify configuration</span></span>
<span data-ttu-id="b916f-131">Automation 계정이 Log Analytics 작업 영역으로 로그를 보내는지 확인하려면 다음 PowerShell을 사용하여 Automation 계정에 대해 진단이 올바르게 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-131">To confirm that your Automation account is sending logs to your Log Analytics workspace, check that diagnostics are set correctly on the Automation account using the following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="b916f-132">출력에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-132">In the output ensure that:</span></span>
+ <span data-ttu-id="b916f-133">*로그*에서 *Enabled* 값이 *True*인지 여부</span><span class="sxs-lookup"><span data-stu-id="b916f-133">Under *Logs*, the value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="b916f-134">*WorkspaceId* 값이 Log Analytics 작업 공간의 ResourceId로 설정되어 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="b916f-134">The value of *WorkspaceId* is set to the ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="b916f-135">Log Analytics 레코드</span><span class="sxs-lookup"><span data-stu-id="b916f-135">Log Analytics records</span></span>
<span data-ttu-id="b916f-136">Azure Automation의 진단은 Log Analytics에 두 가지 유형의 레코드를 만들고 **Type=AzureDiagnostic**로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="b916f-137">작업 로그</span><span class="sxs-lookup"><span data-stu-id="b916f-137">Job Logs</span></span>
| <span data-ttu-id="b916f-138">속성</span><span class="sxs-lookup"><span data-stu-id="b916f-138">Property</span></span> | <span data-ttu-id="b916f-139">설명</span><span class="sxs-lookup"><span data-stu-id="b916f-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b916f-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="b916f-140">TimeGenerated</span></span> |<span data-ttu-id="b916f-141">runbook 작업이 실행된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-141">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="b916f-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="b916f-142">RunbookName_s</span></span> |<span data-ttu-id="b916f-143">runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-143">The name of the runbook.</span></span> |
| <span data-ttu-id="b916f-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="b916f-144">Caller_s</span></span> |<span data-ttu-id="b916f-145">작업을 시작한 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-145">Who initiated the operation.</span></span>  <span data-ttu-id="b916f-146">가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="b916f-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="b916f-147">Tenant_g</span></span> | <span data-ttu-id="b916f-148">호출자에 대한 테넌트를 식별하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-148">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="b916f-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="b916f-149">JobId_g</span></span> |<span data-ttu-id="b916f-150">runbook 작업의 ID인 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-150">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="b916f-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="b916f-151">ResultType</span></span> |<span data-ttu-id="b916f-152">runbook 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-152">The status of the runbook job.</span></span>  <span data-ttu-id="b916f-153">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-153">Possible values are:</span></span><br><span data-ttu-id="b916f-154">- 시작됨</span><span class="sxs-lookup"><span data-stu-id="b916f-154">- Started</span></span><br><span data-ttu-id="b916f-155">- 중지됨</span><span class="sxs-lookup"><span data-stu-id="b916f-155">- Stopped</span></span><br><span data-ttu-id="b916f-156">- 일시 중단됨</span><span class="sxs-lookup"><span data-stu-id="b916f-156">- Suspended</span></span><br><span data-ttu-id="b916f-157">- 실패</span><span class="sxs-lookup"><span data-stu-id="b916f-157">- Failed</span></span><br><span data-ttu-id="b916f-158">- 완료됨</span><span class="sxs-lookup"><span data-stu-id="b916f-158">- Completed</span></span> |
| <span data-ttu-id="b916f-159">Category</span><span class="sxs-lookup"><span data-stu-id="b916f-159">Category</span></span> | <span data-ttu-id="b916f-160">데이터 유형의 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-160">Classification of the type of data.</span></span>  <span data-ttu-id="b916f-161">Automation의 경우 값은 JobLogs입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-161">For Automation, the value is JobLogs.</span></span> |
| <span data-ttu-id="b916f-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="b916f-162">OperationName</span></span> | <span data-ttu-id="b916f-163">Azure에서 수행되는 작업 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-163">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="b916f-164">Automation의 경우 이 값은 Job입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-164">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="b916f-165">리소스</span><span class="sxs-lookup"><span data-stu-id="b916f-165">Resource</span></span> | <span data-ttu-id="b916f-166">Automation 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-166">Name of the Automation account</span></span> |
| <span data-ttu-id="b916f-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b916f-167">SourceSystem</span></span> | <span data-ttu-id="b916f-168">Log Analytics가 데이터를 수집한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-168">How Log Analytics collected the data.</span></span> <span data-ttu-id="b916f-169">Azure 진단의 경우 항상 *Azure*입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="b916f-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="b916f-170">ResultDescription</span></span> |<span data-ttu-id="b916f-171">runbook 작업 결과 상태를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-171">Describes the runbook job result state.</span></span>  <span data-ttu-id="b916f-172">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-172">Possible values are:</span></span><br><span data-ttu-id="b916f-173">- 작업 시작</span><span class="sxs-lookup"><span data-stu-id="b916f-173">- Job is started</span></span><br><span data-ttu-id="b916f-174">- 작업 실패</span><span class="sxs-lookup"><span data-stu-id="b916f-174">- Job Failed</span></span><br><span data-ttu-id="b916f-175">- Job Completed입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-175">- Job Completed</span></span> |
| <span data-ttu-id="b916f-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="b916f-176">CorrelationId</span></span> |<span data-ttu-id="b916f-177">runbook 작업의 상관 관계 ID인 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-177">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="b916f-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="b916f-178">ResourceId</span></span> |<span data-ttu-id="b916f-179">Runbook의 Azure Automation 계정 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-179">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="b916f-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="b916f-180">SubscriptionId</span></span> | <span data-ttu-id="b916f-181">Automation 계정에 대한 Azure 구독 ID(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-181">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="b916f-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b916f-182">ResourceGroup</span></span> | <span data-ttu-id="b916f-183">Automation 계정에 대한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-183">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="b916f-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="b916f-184">ResourceProvider</span></span> | <span data-ttu-id="b916f-185">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="b916f-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="b916f-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="b916f-186">ResourceType</span></span> | <span data-ttu-id="b916f-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="b916f-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="b916f-188">작업 스트림</span><span class="sxs-lookup"><span data-stu-id="b916f-188">Job Streams</span></span>
| <span data-ttu-id="b916f-189">속성</span><span class="sxs-lookup"><span data-stu-id="b916f-189">Property</span></span> | <span data-ttu-id="b916f-190">설명</span><span class="sxs-lookup"><span data-stu-id="b916f-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b916f-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="b916f-191">TimeGenerated</span></span> |<span data-ttu-id="b916f-192">runbook 작업이 실행된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-192">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="b916f-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="b916f-193">RunbookName_s</span></span> |<span data-ttu-id="b916f-194">runbook의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-194">The name of the runbook.</span></span> |
| <span data-ttu-id="b916f-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="b916f-195">Caller_s</span></span> |<span data-ttu-id="b916f-196">작업을 시작한 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-196">Who initiated the operation.</span></span>  <span data-ttu-id="b916f-197">가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="b916f-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="b916f-198">StreamType_s</span></span> |<span data-ttu-id="b916f-199">작업 스트림의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-199">The type of job stream.</span></span> <span data-ttu-id="b916f-200">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-200">Possible values are:</span></span><br><span data-ttu-id="b916f-201">- 진행</span><span class="sxs-lookup"><span data-stu-id="b916f-201">-Progress</span></span><br><span data-ttu-id="b916f-202">- 출력</span><span class="sxs-lookup"><span data-stu-id="b916f-202">- Output</span></span><br><span data-ttu-id="b916f-203">- 경고</span><span class="sxs-lookup"><span data-stu-id="b916f-203">- Warning</span></span><br><span data-ttu-id="b916f-204">- 오류</span><span class="sxs-lookup"><span data-stu-id="b916f-204">- Error</span></span><br><span data-ttu-id="b916f-205">- 디버그</span><span class="sxs-lookup"><span data-stu-id="b916f-205">- Debug</span></span><br><span data-ttu-id="b916f-206">- Verbose입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-206">- Verbose</span></span> |
| <span data-ttu-id="b916f-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="b916f-207">Tenant_g</span></span> | <span data-ttu-id="b916f-208">호출자에 대한 테넌트를 식별하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-208">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="b916f-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="b916f-209">JobId_g</span></span> |<span data-ttu-id="b916f-210">runbook 작업의 ID인 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-210">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="b916f-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="b916f-211">ResultType</span></span> |<span data-ttu-id="b916f-212">runbook 작업의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-212">The status of the runbook job.</span></span>  <span data-ttu-id="b916f-213">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-213">Possible values are:</span></span><br><span data-ttu-id="b916f-214">- 진행 중</span><span class="sxs-lookup"><span data-stu-id="b916f-214">- In Progress</span></span> |
| <span data-ttu-id="b916f-215">Category</span><span class="sxs-lookup"><span data-stu-id="b916f-215">Category</span></span> | <span data-ttu-id="b916f-216">데이터 유형의 분류입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-216">Classification of the type of data.</span></span>  <span data-ttu-id="b916f-217">Automation의 경우 값은 JobStreams입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-217">For Automation, the value is JobStreams.</span></span> |
| <span data-ttu-id="b916f-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="b916f-218">OperationName</span></span> | <span data-ttu-id="b916f-219">Azure에서 수행되는 작업 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-219">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="b916f-220">Automation의 경우 이 값은 Job입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-220">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="b916f-221">리소스</span><span class="sxs-lookup"><span data-stu-id="b916f-221">Resource</span></span> | <span data-ttu-id="b916f-222">Automation 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-222">Name of the Automation account</span></span> |
| <span data-ttu-id="b916f-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="b916f-223">SourceSystem</span></span> | <span data-ttu-id="b916f-224">Log Analytics가 데이터를 수집한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-224">How Log Analytics collected the data.</span></span> <span data-ttu-id="b916f-225">Azure 진단의 경우 항상 *Azure*입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="b916f-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="b916f-226">ResultDescription</span></span> |<span data-ttu-id="b916f-227">runbook의 출력 스트림을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-227">Includes the output stream from the runbook.</span></span> |
| <span data-ttu-id="b916f-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="b916f-228">CorrelationId</span></span> |<span data-ttu-id="b916f-229">runbook 작업의 상관 관계 ID인 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-229">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="b916f-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="b916f-230">ResourceId</span></span> |<span data-ttu-id="b916f-231">Runbook의 Azure Automation 계정 리소스 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-231">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="b916f-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="b916f-232">SubscriptionId</span></span> | <span data-ttu-id="b916f-233">Automation 계정에 대한 Azure 구독 ID(GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-233">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="b916f-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b916f-234">ResourceGroup</span></span> | <span data-ttu-id="b916f-235">Automation 계정에 대한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-235">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="b916f-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="b916f-236">ResourceProvider</span></span> | <span data-ttu-id="b916f-237">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="b916f-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="b916f-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="b916f-238">ResourceType</span></span> | <span data-ttu-id="b916f-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="b916f-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="b916f-240">Log Analytics에서 자동화 로그 보기</span><span class="sxs-lookup"><span data-stu-id="b916f-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="b916f-241">Automation 작업 로그를 Log Analytics로 보내기 시작했으므로 이제 Log Analytics 내에서 이러한 로그로 수행할 수 있는 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-241">Now that you have started sending your Automation job logs to Log Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="b916f-242">로그를 보려면 다음 쿼리를 실행합니다. `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="b916f-242">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="b916f-243">Runbook 작업이 실패하거나 일시 중단된 경우 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="b916f-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="b916f-244">고객이 자주 묻는 질문 중 하나는 Runbook 작업에 문제가 발생한 경우 전자 메일 또는 텍스트를 보낼 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-244">One of our top customer asks is for the ability to send an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="b916f-245">경고 규칙을 만들려면 경고를 호출해야 하는 runbook 작업 레코드에 대한 로그 검색을 만드는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-245">To create an alert rule, you start by creating a log search for the runbook job records that should invoke the alert.</span></span>  <span data-ttu-id="b916f-246">**경고** 단추를 클릭하여 경고 규칙을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-246">Click the **Alert** button to create and configure the alert rule.</span></span>

1. <span data-ttu-id="b916f-247">Log Analytics 개요 페이지에서 **로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-247">From the Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="b916f-248">쿼리 필드에 다음 검색을 입력하여 경고에 대한 로그 검색 쿼리를 만듭니다. `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  다음을 사용하여 RunbookName별로 그룹화할 수도 있습니다.`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="b916f-248">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by the RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="b916f-249">둘 이상의 Automation 계정 또는 구독에서 작업 영역으로의 로그를 설정한 경우 구독 또는 Automation 계정별로 경고를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-249">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="b916f-250">자동화 계정 이름은 JobLogs 검색의 리소스 필드에서 파생될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-250">Automation account name can be derived from the Resource field in the search of JobLogs.</span></span>  
3. <span data-ttu-id="b916f-251">**경고 규칙 추가** 화면을 열려면 페이지 위쪽의 **경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-251">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span></span> <span data-ttu-id="b916f-252">경고 구성 옵션에 자세한 내용은 [Log Analytics의 경고](../log-analytics/log-analytics-alerts.md#alert-rules)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b916f-252">For further details on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="b916f-253">오류와 함께 완료된 모든 작업 찾기</span><span class="sxs-lookup"><span data-stu-id="b916f-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="b916f-254">오류에 대한 경고 외에도, runbook 작업에 대해 비종료 오류가 발생하는 경우를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-254">In addition to alerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="b916f-255">이러한 경우 PowerShell은 오류 스트림을 생성하지만 비종료 오류가 발생해도 작업이 일시 중단되거나 실패하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-255">In these cases PowerShell produces an error stream, but the non-terminating errors do not cause your job to suspend or fail.</span></span>    

1. <span data-ttu-id="b916f-256">Log Analytics 작업 영역에서 **로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="b916f-257">쿼리 필드에서 `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` 을 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-257">In the query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="b916f-258">작업에 대한 작업 스트림 보기</span><span class="sxs-lookup"><span data-stu-id="b916f-258">View job streams for a job</span></span>
<span data-ttu-id="b916f-259">작업을 디버깅할 때 작업 스트림을 살펴볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-259">When you are debugging a job, you may also want to look into the job streams.</span></span>  <span data-ttu-id="b916f-260">다음 쿼리는 GUID가 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0인 단일 작업의 모든 스트림을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-260">The following query shows all the streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="b916f-261">기록 작업 상태 보기</span><span class="sxs-lookup"><span data-stu-id="b916f-261">View historical job status</span></span>
<span data-ttu-id="b916f-262">마지막으로 시간별 작업 기록을 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-262">Finally, you may want to visualize your job history over time.</span></span>  <span data-ttu-id="b916f-263">이 쿼리를 사용하여 시간이 지남에 따른 작업 상태를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-263">You can use this query to search for the status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="b916f-264">![OMS 기록 작업 상태 차트](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="b916f-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="b916f-265">요약</span><span class="sxs-lookup"><span data-stu-id="b916f-265">Summary</span></span>
<span data-ttu-id="b916f-266">Automation 작업 상태 및 스트림 데이터를 Log Analytics로 전송하면 다음과 같은 작업을 통해 Automation 작업의 상태를 보다 정확히 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-266">By sending your Automation job status and stream data to Log Analytics, you can get better insight into the status of your Automation jobs by:</span></span>
+ <span data-ttu-id="b916f-267">문제가 발생할 때 알리도록 경고 설정</span><span class="sxs-lookup"><span data-stu-id="b916f-267">Setting up alerts to notify you when there is an issue</span></span>
+ <span data-ttu-id="b916f-268">사용자 지정 보기와 검색 쿼리를 사용하여 runbook 결과, runbook 작업 상태 및 기타 관련된 핵심 지표 또는 메트릭 시각화.</span><span class="sxs-lookup"><span data-stu-id="b916f-268">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="b916f-269">Log Analytics는 Automation 작업의 작동을 보다 정확히 이해하도록 하며 인시던트를 더 빠르게 해결하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="b916f-269">Log Analytics provides greater operational visibility to your Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b916f-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b916f-270">Next steps</span></span>
* <span data-ttu-id="b916f-271">Log Analytics를 사용하여 여러 검색 쿼리를 작성하고 자동화 작업 로그를 검토하는 방법에 대한 자세한 내용은 [Log Analytics의 로그 검색](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="b916f-271">To learn more about how to construct different search queries and review the Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="b916f-272">Runbook에서 출력 및 오류 메시지를 만들고 검색하는 방법은 [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="b916f-272">To understand how to create and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="b916f-273">Runbook 실행, Runbook 작업 모니터링 방법 및 기타 기술 세부 정보를 알아보려면 [Runbook 작업 추적](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="b916f-273">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="b916f-274">OMS Log Analytics 및 데이터 수집 소스에 대한 자세한 내용은 [Log Analytics에서 Azure Storage 데이터 수집 개요](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="b916f-274">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
