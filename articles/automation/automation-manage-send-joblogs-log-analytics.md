---
title: "Azure 자동화 작업 데이터 tooOMS 로그 분석 aaaForward | Microsoft Docs"
description: "이 문서에서는 toosend 작업 상태 및 runbook 작업 tooMicrosoft Operations Management Suite 로그 분석 toodeliver 추가 정보 및 관리를 스트림 하는 방법을 보여줍니다."
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
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a><span data-ttu-id="1ebb8-103">자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달</span><span class="sxs-lookup"><span data-stu-id="1ebb8-103">Forward job status and job streams from Automation tooLog Analytics (OMS)</span></span>
<span data-ttu-id="1ebb8-104">자동화는 runbook 작업 상태 및 작업 스트림을 tooyour Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-104">Automation can send runbook job status and job streams tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="1ebb8-105">작업 로그 및 작업 스트림 hello Azure 포털에에서 표시 되 나 powershell을 개별 작업 및이 대 한 사용 하면 tooperform 단순 조사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-105">Job logs and job streams are visible in hello Azure portal, or with PowerShell, for individual jobs and this allows you tooperform simple investigations.</span></span> <span data-ttu-id="1ebb8-106">이제 Log Anaytics를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="1ebb8-107">자동화 작업에 대한 통찰력 확보</span><span class="sxs-lookup"><span data-stu-id="1ebb8-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="1ebb8-108">Runbook 작업 상태(예: 실패 또는 일시 중단)를 기반으로 전자 메일 또는 경고 트리거</span><span class="sxs-lookup"><span data-stu-id="1ebb8-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="1ebb8-109">작업 스트림에서 고급 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="1ebb8-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="1ebb8-110">자동화 계정 간에 작업 상호 연결</span><span class="sxs-lookup"><span data-stu-id="1ebb8-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="1ebb8-111">시간별 작업 기록 시각화</span><span class="sxs-lookup"><span data-stu-id="1ebb8-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="1ebb8-112">필수 구성 요소 및 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="1ebb8-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="1ebb8-113">자동화를 보내는 toostart tooLog 분석 로그 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-113">toostart sending your Automation logs tooLog Analytics, you need:</span></span>

1. <span data-ttu-id="1ebb8-114">2016 년 11 월 hello 또는 나중에 릴리스를 [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span><span class="sxs-lookup"><span data-stu-id="1ebb8-114">hello November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="1ebb8-115">Log Analytics 작업 영역.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-115">A Log Analytics workspace.</span></span> <span data-ttu-id="1ebb8-116">자세한 내용은 [Log Analytics 시작](../log-analytics/log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="1ebb8-117">Azure 자동화 계정에 대 한 hello ResourceId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-117">hello ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="1ebb8-118">Azure 자동화 계정 및 로그 분석 작업 영역에서 다음 PowerShell hello 실행에 대 한 toofind hello ResourceId:</span><span class="sxs-lookup"><span data-stu-id="1ebb8-118">toofind hello ResourceId for your Azure Automation account and Log Analytics workspace, run hello following PowerShell:</span></span>

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="1ebb8-119">작업 영역, hello 명령, 앞의 hello 출력에서 찾을 hello 또는 여러 자동화 계정이 있는 경우 *이름* tooconfigure 필요 하 고 hello 값을 복사 *ResourceId*합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-119">If you have multiple Automation accounts, or workspaces, in hello output of hello preceding commands, find hello *Name* you need tooconfigure and copy hello value for *ResourceId*.</span></span>

<span data-ttu-id="1ebb8-120">Toofind hello 해야 할 경우 *이름* 자동화 계정의 hello Azure 포털 자동화 계정에서에서 선택 hello **자동화 계정** 블레이드에 대 한 선택 **모든설정**.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-120">If you need toofind hello *Name* of your Automation account, in hello Azure portal select your Automation account from hello **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="1ebb8-121">Hello에서 **모든 설정을** 블레이드 아래 **계정 설정** 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-121">From hello **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="1ebb8-122">Hello에 **속성** 블레이드에서 이러한 값을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-122">In hello **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="1ebb8-123">![자동화 계정 속성](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="1ebb8-124">Log Analytics와의 통합 설정</span><span class="sxs-lookup"><span data-stu-id="1ebb8-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="1ebb8-125">사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-125">On your computer, start **Windows PowerShell** from hello **Start** screen.</span></span>  
2. <span data-ttu-id="1ebb8-126">복사 하거나 hello PowerShell에서 다음을 붙여 넣고 hello에 대 한 hello 값 편집 `$workspaceId` 및 `$automationAccountId`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-126">Copy and paste hello following PowerShell, and edit hello value for hello `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="1ebb8-127">Hello에 대 한 `-Environment` 매개 변수에 유효한 값은 *azure 클라우드* 또는 *AzureUSGovernment* 에서 작업 하는 hello 클라우드 환경에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-127">For hello `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on hello cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="1ebb8-128">이 스크립트를 실행한 후 새 JobLogs 또는 쓰고 있는 JobStreams의 10분 이내에 Log Analytics에 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="1ebb8-129">toosee hello 로그, hello 다음 로그 분석 로그 검색에 대 한 쿼리를 실행 합니다.`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="1ebb8-129">toosee hello logs, run hello following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="1ebb8-130">구성 확인</span><span class="sxs-lookup"><span data-stu-id="1ebb8-130">Verify configuration</span></span>
<span data-ttu-id="1ebb8-131">자동화 계정에서 보내는 tooconfirm tooyour 로그 분석 작업 영역을 로그, 진단 hello 다음 PowerShell을 사용 하 여 hello 자동화 계정에서 올바르게 설정 되어 있는지 확인:</span><span class="sxs-lookup"><span data-stu-id="1ebb8-131">tooconfirm that your Automation account is sending logs tooyour Log Analytics workspace, check that diagnostics are set correctly on hello Automation account using hello following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="1ebb8-132">Hello 출력을 확인.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-132">In hello output ensure that:</span></span>
+ <span data-ttu-id="1ebb8-133">아래 *로그*, 값에 대 한 hello *Enabled* 은 *True*</span><span class="sxs-lookup"><span data-stu-id="1ebb8-133">Under *Logs*, hello value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="1ebb8-134">값을 hello *WorkspaceId* toohello ResourceId의 로그 분석 작업 영역 설정</span><span class="sxs-lookup"><span data-stu-id="1ebb8-134">hello value of *WorkspaceId* is set toohello ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="1ebb8-135">Log Analytics 레코드</span><span class="sxs-lookup"><span data-stu-id="1ebb8-135">Log Analytics records</span></span>
<span data-ttu-id="1ebb8-136">Azure Automation의 진단은 Log Analytics에 두 가지 유형의 레코드를 만들고 **Type=AzureDiagnostic**로 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="1ebb8-137">작업 로그</span><span class="sxs-lookup"><span data-stu-id="1ebb8-137">Job Logs</span></span>
| <span data-ttu-id="1ebb8-138">속성</span><span class="sxs-lookup"><span data-stu-id="1ebb8-138">Property</span></span> | <span data-ttu-id="1ebb8-139">설명</span><span class="sxs-lookup"><span data-stu-id="1ebb8-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ebb8-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1ebb8-140">TimeGenerated</span></span> |<span data-ttu-id="1ebb8-141">날짜 및 hello runbook 작업 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-141">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="1ebb8-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="1ebb8-142">RunbookName_s</span></span> |<span data-ttu-id="1ebb8-143">hello runbook의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-143">hello name of hello runbook.</span></span> |
| <span data-ttu-id="1ebb8-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="1ebb8-144">Caller_s</span></span> |<span data-ttu-id="1ebb8-145">Hello 작업을 시작한 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-145">Who initiated hello operation.</span></span>  <span data-ttu-id="1ebb8-146">가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="1ebb8-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="1ebb8-147">Tenant_g</span></span> | <span data-ttu-id="1ebb8-148">호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-148">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="1ebb8-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="1ebb8-149">JobId_g</span></span> |<span data-ttu-id="1ebb8-150">hello hello runbook 작업의 Id는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-150">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="1ebb8-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="1ebb8-151">ResultType</span></span> |<span data-ttu-id="1ebb8-152">hello runbook 작업의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-152">hello status of hello runbook job.</span></span>  <span data-ttu-id="1ebb8-153">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-153">Possible values are:</span></span><br><span data-ttu-id="1ebb8-154">- 시작됨</span><span class="sxs-lookup"><span data-stu-id="1ebb8-154">- Started</span></span><br><span data-ttu-id="1ebb8-155">- 중지됨</span><span class="sxs-lookup"><span data-stu-id="1ebb8-155">- Stopped</span></span><br><span data-ttu-id="1ebb8-156">- 일시 중단됨</span><span class="sxs-lookup"><span data-stu-id="1ebb8-156">- Suspended</span></span><br><span data-ttu-id="1ebb8-157">- 실패</span><span class="sxs-lookup"><span data-stu-id="1ebb8-157">- Failed</span></span><br><span data-ttu-id="1ebb8-158">- 완료됨</span><span class="sxs-lookup"><span data-stu-id="1ebb8-158">- Completed</span></span> |
| <span data-ttu-id="1ebb8-159">Category</span><span class="sxs-lookup"><span data-stu-id="1ebb8-159">Category</span></span> | <span data-ttu-id="1ebb8-160">Hello 종류의 데이터 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-160">Classification of hello type of data.</span></span>  <span data-ttu-id="1ebb8-161">자동화를 위해 hello 값은 JobLogs입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-161">For Automation, hello value is JobLogs.</span></span> |
| <span data-ttu-id="1ebb8-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="1ebb8-162">OperationName</span></span> | <span data-ttu-id="1ebb8-163">Azure에서 수행한 작업의 hello 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-163">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="1ebb8-164">자동화를 위해 hello 값은 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-164">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="1ebb8-165">리소스</span><span class="sxs-lookup"><span data-stu-id="1ebb8-165">Resource</span></span> | <span data-ttu-id="1ebb8-166">hello 자동화 계정 이름</span><span class="sxs-lookup"><span data-stu-id="1ebb8-166">Name of hello Automation account</span></span> |
| <span data-ttu-id="1ebb8-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1ebb8-167">SourceSystem</span></span> | <span data-ttu-id="1ebb8-168">로그 분석 hello 데이터 수집 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-168">How Log Analytics collected hello data.</span></span> <span data-ttu-id="1ebb8-169">Azure 진단의 경우 항상 *Azure*입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="1ebb8-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="1ebb8-170">ResultDescription</span></span> |<span data-ttu-id="1ebb8-171">Hello runbook 작업 결과 상태를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-171">Describes hello runbook job result state.</span></span>  <span data-ttu-id="1ebb8-172">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-172">Possible values are:</span></span><br><span data-ttu-id="1ebb8-173">- 작업 시작</span><span class="sxs-lookup"><span data-stu-id="1ebb8-173">- Job is started</span></span><br><span data-ttu-id="1ebb8-174">- 작업 실패</span><span class="sxs-lookup"><span data-stu-id="1ebb8-174">- Job Failed</span></span><br><span data-ttu-id="1ebb8-175">- Job Completed입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-175">- Job Completed</span></span> |
| <span data-ttu-id="1ebb8-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-176">CorrelationId</span></span> |<span data-ttu-id="1ebb8-177">hello hello runbook 작업의 상관 관계 Id는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-177">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="1ebb8-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-178">ResourceId</span></span> |<span data-ttu-id="1ebb8-179">Hello runbook의 hello Azure 자동화 계정 리소스 id를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-179">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="1ebb8-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-180">SubscriptionId</span></span> | <span data-ttu-id="1ebb8-181">hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-181">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="1ebb8-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1ebb8-182">ResourceGroup</span></span> | <span data-ttu-id="1ebb8-183">Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-183">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="1ebb8-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="1ebb8-184">ResourceProvider</span></span> | <span data-ttu-id="1ebb8-185">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="1ebb8-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="1ebb8-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="1ebb8-186">ResourceType</span></span> | <span data-ttu-id="1ebb8-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="1ebb8-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="1ebb8-188">작업 스트림</span><span class="sxs-lookup"><span data-stu-id="1ebb8-188">Job Streams</span></span>
| <span data-ttu-id="1ebb8-189">속성</span><span class="sxs-lookup"><span data-stu-id="1ebb8-189">Property</span></span> | <span data-ttu-id="1ebb8-190">설명</span><span class="sxs-lookup"><span data-stu-id="1ebb8-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ebb8-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1ebb8-191">TimeGenerated</span></span> |<span data-ttu-id="1ebb8-192">날짜 및 hello runbook 작업 실행 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-192">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="1ebb8-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="1ebb8-193">RunbookName_s</span></span> |<span data-ttu-id="1ebb8-194">hello runbook의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-194">hello name of hello runbook.</span></span> |
| <span data-ttu-id="1ebb8-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="1ebb8-195">Caller_s</span></span> |<span data-ttu-id="1ebb8-196">Hello 작업을 시작한 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-196">Who initiated hello operation.</span></span>  <span data-ttu-id="1ebb8-197">가능한 값은 전자 메일 주소 또는 예약된 작업의 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="1ebb8-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="1ebb8-198">StreamType_s</span></span> |<span data-ttu-id="1ebb8-199">작업 스트림의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-199">hello type of job stream.</span></span> <span data-ttu-id="1ebb8-200">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-200">Possible values are:</span></span><br><span data-ttu-id="1ebb8-201">- 진행</span><span class="sxs-lookup"><span data-stu-id="1ebb8-201">-Progress</span></span><br><span data-ttu-id="1ebb8-202">- 출력</span><span class="sxs-lookup"><span data-stu-id="1ebb8-202">- Output</span></span><br><span data-ttu-id="1ebb8-203">- 경고</span><span class="sxs-lookup"><span data-stu-id="1ebb8-203">- Warning</span></span><br><span data-ttu-id="1ebb8-204">- 오류</span><span class="sxs-lookup"><span data-stu-id="1ebb8-204">- Error</span></span><br><span data-ttu-id="1ebb8-205">- 디버그</span><span class="sxs-lookup"><span data-stu-id="1ebb8-205">- Debug</span></span><br><span data-ttu-id="1ebb8-206">- Verbose입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-206">- Verbose</span></span> |
| <span data-ttu-id="1ebb8-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="1ebb8-207">Tenant_g</span></span> | <span data-ttu-id="1ebb8-208">호출자에 게 hello에 대 한 hello 테 넌 트를 식별 하는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-208">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="1ebb8-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="1ebb8-209">JobId_g</span></span> |<span data-ttu-id="1ebb8-210">hello hello runbook 작업의 Id는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-210">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="1ebb8-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="1ebb8-211">ResultType</span></span> |<span data-ttu-id="1ebb8-212">hello runbook 작업의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-212">hello status of hello runbook job.</span></span>  <span data-ttu-id="1ebb8-213">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-213">Possible values are:</span></span><br><span data-ttu-id="1ebb8-214">- 진행 중</span><span class="sxs-lookup"><span data-stu-id="1ebb8-214">- In Progress</span></span> |
| <span data-ttu-id="1ebb8-215">Category</span><span class="sxs-lookup"><span data-stu-id="1ebb8-215">Category</span></span> | <span data-ttu-id="1ebb8-216">Hello 종류의 데이터 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-216">Classification of hello type of data.</span></span>  <span data-ttu-id="1ebb8-217">자동화를 위해 hello 값은 JobStreams입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-217">For Automation, hello value is JobStreams.</span></span> |
| <span data-ttu-id="1ebb8-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="1ebb8-218">OperationName</span></span> | <span data-ttu-id="1ebb8-219">Azure에서 수행한 작업의 hello 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-219">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="1ebb8-220">자동화를 위해 hello 값은 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-220">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="1ebb8-221">리소스</span><span class="sxs-lookup"><span data-stu-id="1ebb8-221">Resource</span></span> | <span data-ttu-id="1ebb8-222">hello 자동화 계정 이름</span><span class="sxs-lookup"><span data-stu-id="1ebb8-222">Name of hello Automation account</span></span> |
| <span data-ttu-id="1ebb8-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1ebb8-223">SourceSystem</span></span> | <span data-ttu-id="1ebb8-224">로그 분석 hello 데이터 수집 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-224">How Log Analytics collected hello data.</span></span> <span data-ttu-id="1ebb8-225">Azure 진단의 경우 항상 *Azure*입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="1ebb8-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="1ebb8-226">ResultDescription</span></span> |<span data-ttu-id="1ebb8-227">Hello runbook에서 출력 스트림에 hello 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-227">Includes hello output stream from hello runbook.</span></span> |
| <span data-ttu-id="1ebb8-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-228">CorrelationId</span></span> |<span data-ttu-id="1ebb8-229">hello hello runbook 작업의 상관 관계 Id는 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-229">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="1ebb8-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-230">ResourceId</span></span> |<span data-ttu-id="1ebb8-231">Hello runbook의 hello Azure 자동화 계정 리소스 id를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-231">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="1ebb8-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1ebb8-232">SubscriptionId</span></span> | <span data-ttu-id="1ebb8-233">hello hello 자동화 계정에 대 한 Azure 구독 Id (GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-233">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="1ebb8-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1ebb8-234">ResourceGroup</span></span> | <span data-ttu-id="1ebb8-235">Hello 자동화 계정에 대 한 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-235">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="1ebb8-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="1ebb8-236">ResourceProvider</span></span> | <span data-ttu-id="1ebb8-237">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="1ebb8-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="1ebb8-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="1ebb8-238">ResourceType</span></span> | <span data-ttu-id="1ebb8-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="1ebb8-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="1ebb8-240">Log Analytics에서 자동화 로그 보기</span><span class="sxs-lookup"><span data-stu-id="1ebb8-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="1ebb8-241">보내는 자동화 작업 로그 tooLog 분석을 시작 했으므로 이러한 로그 내 로그 분석으로 수행할 수 있는 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-241">Now that you have started sending your Automation job logs tooLog Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="1ebb8-242">다음 쿼리에서 hello 실행 toosee hello 로그:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="1ebb8-242">toosee hello logs, run hello following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="1ebb8-243">Runbook 작업이 실패하거나 일시 중단된 경우 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="1ebb8-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="1ebb8-244">Runbook 작업에 문제가 발생 하는 경우 전자 메일 또는 텍스트 기능 toosend hello에 대 한가 묻습니다 상위 고객 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-244">One of our top customer asks is for hello ability toosend an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="1ebb8-245">toocreate 경고 규칙 hello runbook에 대 한 로그 검색 hello 경고를 호출 해야 하는 작업 레코드를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-245">toocreate an alert rule, you start by creating a log search for hello runbook job records that should invoke hello alert.</span></span>  <span data-ttu-id="1ebb8-246">Hello 클릭 **경고** toocreate 단추 및 hello 경고 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-246">Click hello **Alert** button toocreate and configure hello alert rule.</span></span>

1. <span data-ttu-id="1ebb8-247">Hello 로그 분석 개요 페이지에서 클릭 **로그 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-247">From hello Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="1ebb8-248">Hello 검색 hello 쿼리 필드에 다음을 입력 하 여 경고에 대 한 로그 검색 쿼리를 만들어: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` 를 사용 하 여 hello RunbookName 기준으로 그룹화 수도 있습니다.`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="1ebb8-248">Create a log search query for your alert by typing hello following search into hello query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by hello RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="1ebb8-249">에 둘 이상의 자동화 계정 또는 구독 tooyour 작업 영역에서 로그를 설정 하는 경우 구독 및 자동화 계정에서 경고를 그룹화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-249">If you have set up logs from more than one Automation account or subscription tooyour workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="1ebb8-250">자동화 계정 이름 JobLogs의 hello 검색에서 hello 리소스 필드에서 파생 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-250">Automation account name can be derived from hello Resource field in hello search of JobLogs.</span></span>  
3. <span data-ttu-id="1ebb8-251">tooopen hello **경고 규칙 추가** 화면 **경고** hello hello 페이지 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-251">tooopen hello **Add Alert Rule** screen, click **Alert** at hello top of hello page.</span></span> <span data-ttu-id="1ebb8-252">Hello 옵션 tooconfigure hello 경고에 자세한 내용은 참조 하십시오. [로그 분석에서 경고](../log-analytics/log-analytics-alerts.md#alert-rules)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-252">For further details on hello options tooconfigure hello alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="1ebb8-253">오류와 함께 완료된 모든 작업 찾기</span><span class="sxs-lookup"><span data-stu-id="1ebb8-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="1ebb8-254">또한 오류에 tooalerting, runbook 작업에 종료 되지 않는 오류가 있을 때을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-254">In addition tooalerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="1ebb8-255">이러한 경우 PowerShell 오류 스트림에 생성 합니다. 하지만 hello 종료 되지 않은 오류 작업 toosuspend 발생 하지 않거나 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-255">In these cases PowerShell produces an error stream, but hello non-terminating errors do not cause your job toosuspend or fail.</span></span>    

1. <span data-ttu-id="1ebb8-256">Log Analytics 작업 영역에서 **로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="1ebb8-257">Hello 쿼리 필드에 입력 `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` 클릭 하 고 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-257">In hello query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="1ebb8-258">작업에 대한 작업 스트림 보기</span><span class="sxs-lookup"><span data-stu-id="1ebb8-258">View job streams for a job</span></span>
<span data-ttu-id="1ebb8-259">작업을 디버깅 하는 경우 수도 있습니다 toolook hello 작업 스트림으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-259">When you are debugging a job, you may also want toolook into hello job streams.</span></span>  <span data-ttu-id="1ebb8-260">hello 다음 쿼리 표시 GUID 2ebd22ea e05e-4eb9-9 차원 76 d73cbd4356e0 인 단일 작업에 대 한 모든 hello 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-260">hello following query shows all hello streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="1ebb8-261">기록 작업 상태 보기</span><span class="sxs-lookup"><span data-stu-id="1ebb8-261">View historical job status</span></span>
<span data-ttu-id="1ebb8-262">마지막으로 할 수 있습니다 toovisualize 작업 기록 시간에 따라.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-262">Finally, you may want toovisualize your job history over time.</span></span>  <span data-ttu-id="1ebb8-263">작업의 hello 상태에 대 한 시간에 따라이 쿼리 toosearch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-263">You can use this query toosearch for hello status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="1ebb8-264">![OMS 기록 작업 상태 차트](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="1ebb8-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="1ebb8-265">요약</span><span class="sxs-lookup"><span data-stu-id="1ebb8-265">Summary</span></span>
<span data-ttu-id="1ebb8-266">프로그램 자동화 작업 상태 및 스트림 데이터 tooLog 분석을 전송 하 여 자동화 작업 하 여 hello 상태에 대 한 더 나은 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-266">By sending your Automation job status and stream data tooLog Analytics, you can get better insight into hello status of your Automation jobs by:</span></span>
+ <span data-ttu-id="1ebb8-267">설정 경고 toonotify 있습니다에 문제가 있을 때</span><span class="sxs-lookup"><span data-stu-id="1ebb8-267">Setting up alerts toonotify you when there is an issue</span></span>
+ <span data-ttu-id="1ebb8-268">사용자 지정 보기 및 검색 쿼리 toovisualize를 사용 하 여 프로그램 runbook 결과, runbook 작업 상태 및 기타 관련 주요 표시기 또는 메트릭.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-268">Using custom views and search queries toovisualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="1ebb8-269">로그 분석 operational 띄도록 tooyour 자동화 작업을 제공 및 보다 신속한 주소 인시던트 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebb8-269">Log Analytics provides greater operational visibility tooyour Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1ebb8-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ebb8-270">Next steps</span></span>
* <span data-ttu-id="1ebb8-271">toolearn 어떻게 tooconstruct 다른 검색 쿼리 및 검토 hello 자동화 작업 로그 분석을 사용 하 여 로그에 대 한 자세한 참조 [로그 분석 검색 로그인](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="1ebb8-271">toolearn more about how tooconstruct different search queries and review hello Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="1ebb8-272">runbook에서 toocreate 및 검색 하 고 출력 및 오류 메시지를 확인 하려면 어떻게 toounderstand [Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="1ebb8-272">toounderstand how toocreate and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="1ebb8-273">toolearn toomonitor runbook 작업 및 기타 기술 정보가 참조 하는 방법 runbook 실행에 대 한 자세한 [runbook 작업을 추적 합니다.](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="1ebb8-273">toolearn more about runbook execution, how toomonitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="1ebb8-274">OMS 로그 분석 및 데이터 컬렉션 원본에 대해 자세히 toolearn 참조 [로그 분석 개요에서 수집 하는 Azure 저장소 데이터](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="1ebb8-274">toolearn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
