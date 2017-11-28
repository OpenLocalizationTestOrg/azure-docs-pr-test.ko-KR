---
title: "Azure 자동화에서 runbook 사용 하 여 로그 분석 데이터 aaaCollecting | Microsoft Docs"
description: "로그 분석에서 분석할 hello OMS 리포지토리에 toocollect 데이터 Azure 자동화에서에서 runbook을 만들를 안내 과정을 단계별로 자습서입니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="63727-103">Azure Automation Runbook을 사용하여 Log Analytics에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="63727-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="63727-104">에이전트의 [데이터 원본](../log-analytics/log-analytics-data-sources.md)을 비롯한 다양한 원본에서 Log Analytics으로 대량의 데이터를 수집할 수 있고 [Azure에서 수집된 데이터](../log-analytics/log-analytics-azure-storage.md)도 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="63727-105">Toocollect 데이터 필요한 되지 않는 이러한 표준 원본을 통해 액세스할 수 있는 경우에 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="63727-106">이러한 경우 hello를 사용할 수 있습니다 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md) 모든 REST API 클라이언트에서 toowrite 데이터 tooLog 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="63727-107">일반적인 메서드 tooperform이 데이터 컬렉션에서 Azure 자동화에서 runbook을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="63727-108">이 자습서를 만들고 toowrite 데이터 tooLog 분석 Azure 자동화에서에서 runbook 예약 hello 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="63727-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="63727-109">Prerequisites</span></span>
<span data-ttu-id="63727-110">이 시나리오에는 Azure 구독에서 구성 된 리소스를 다음 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="63727-111">둘 다 무료 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-111">Both can be a free account.</span></span>

- <span data-ttu-id="63727-112">[Log Analytics 작업 영역](../log-analytics/log-analytics-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="63727-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="63727-113">[Azure Automation 계정](../automation/automation-offering-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="63727-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="63727-114">시나리오의 개요</span><span class="sxs-lookup"><span data-stu-id="63727-114">Overview of scenario</span></span>
<span data-ttu-id="63727-115">이 자습서에서는 Automation 작업에 대한 정보를 수집하는 Runbook을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="63727-116">Azure 자동화의 Runbook은 powershell을 구현 때문에 작성 하 고 hello Azure 자동화 편집기에서 스크립트를 테스트 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="63727-117">Hello 필요한 정보를 수집 중인를 확인 한 후에 해당 데이터 tooLog 분석을 작성 하 고 hello 사용자 지정 데이터 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="63727-118">마지막으로, 일정 toostart hello runbook을 정기적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63727-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="63727-119">이 runbook 하지 않고 Azure 자동화 toosend 작업 정보 tooLog 분석을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="63727-120">이 시나리오는 주로 사용 되는 toosupport hello 자습서 있으며 hello 데이터 tooa 테스트 작업 영역을 보내는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="63727-121">1. 데이터 수집기 API 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="63727-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="63727-122">모든 [hello HTTP 데이터 수집기 API에서에서 요청](../log-analytics/log-analytics-data-collector-api.md#create-a-request) 권한 부여 헤더를 포함 하 고 적절 하 게 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="63727-123">Runbook에서이 수행할 수 있지만이 프로세스를 간소화 하는 모듈을 사용 하 여 필요한 코드의 hello 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="63727-124">사용할 수 있는 하나의 모듈은 [OMSIngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI) hello PowerShell 갤러리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="63727-125">toouse는 [모듈](../automation/automation-integration-modules.md) runbook에서는 설치 해야 자동화 계정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="63727-126">동일한 계정을 사용 하 여 수 hello에서 모든 runbook hello hello 모듈의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="63727-127">Automation 계정에서 **자산** > **모듈** > **모듈 추가**를 선택하여 새 모듈을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="63727-128">hello PowerShell 갤러리 하지만 제공 빠른 옵션 toodeploy 모듈 직접 tooyour 자동화 계정이 자습서에 대 한 해당 옵션을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI 모듈](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="63727-130">너무 이동[PowerShell 갤러리](https://www.powershellgallery.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="63727-131">**OMSIngestionAPI**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="63727-132">Hello 클릭 **tooAzure 자동화 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="63727-133">자동화 계정을 선택 하 고 클릭 **확인** tooinstall hello 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="63727-134">2. Automation 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="63727-134">2. Create Automation variables</span></span>
<span data-ttu-id="63727-135">[Automation 변수](..\automation\automation-variables.md)는 Automation 계정의 모든 Runbook에서 사용할 수 있는 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="63727-136">Runbook 자세히 만드는 유연한 toochange를 허용 하 여 이러한 값을 편집 하지 않고도 실제 runbook hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="63727-137">Hello HTTP 데이터 수집기 API의에서 모든 요청 hello ID와 키의 hello OMS 작업 영역을 차지 하며 변수 자산은 이상적인 toostore이이 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="63727-139">Hello Azure 포털에서에서 tooyour 자동화 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="63727-140">**공유 리소스**에서 **변수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="63727-141">클릭 **변수 추가** 다음 표에 hello에 hello 두 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63727-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="63727-142">속성</span><span class="sxs-lookup"><span data-stu-id="63727-142">Property</span></span> | <span data-ttu-id="63727-143">작업 영역 ID 값</span><span class="sxs-lookup"><span data-stu-id="63727-143">Workspace ID Value</span></span> | <span data-ttu-id="63727-144">작업 영역 키 값</span><span class="sxs-lookup"><span data-stu-id="63727-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="63727-145">이름</span><span class="sxs-lookup"><span data-stu-id="63727-145">Name</span></span> | <span data-ttu-id="63727-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="63727-146">WorkspaceId</span></span> | <span data-ttu-id="63727-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="63727-147">WorkspaceKey</span></span> |
| <span data-ttu-id="63727-148">유형</span><span class="sxs-lookup"><span data-stu-id="63727-148">Type</span></span> | <span data-ttu-id="63727-149">문자열</span><span class="sxs-lookup"><span data-stu-id="63727-149">String</span></span> | <span data-ttu-id="63727-150">문자열</span><span class="sxs-lookup"><span data-stu-id="63727-150">String</span></span> |
| <span data-ttu-id="63727-151">값</span><span class="sxs-lookup"><span data-stu-id="63727-151">Value</span></span> | <span data-ttu-id="63727-152">로그 분석 작업의 작업 영역 ID hello에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="63727-153">주 가상 컴퓨터 또는 보조 키의 로그 분석 작업 영역 hello를 사용 하 여 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="63727-154">암호화</span><span class="sxs-lookup"><span data-stu-id="63727-154">Encrypted</span></span> | <span data-ttu-id="63727-155">아니요</span><span class="sxs-lookup"><span data-stu-id="63727-155">No</span></span> | <span data-ttu-id="63727-156">예</span><span class="sxs-lookup"><span data-stu-id="63727-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="63727-157">3. runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="63727-157">3. Create runbook</span></span>

<span data-ttu-id="63727-158">Azure 자동화 편집기를 편집 하 고 runbook을 테스트할 수 있는 hello 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="63727-159">Hello 옵션 toouse hello 스크립트 편집기 toowork와 있는 [PowerShell 직접](../automation/automation-edit-textual-runbook.md) 또는 [그래픽 runbook을 만들](../automation/automation-graphical-authoring-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="63727-160">이 자습서에서는 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook 편집](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="63727-162">Tooyour 자동화 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="63727-163">**Runbook** > **Runbook 추가** > **새 Runbook 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="63727-164">Hello runbook 이름에 대 한 입력 **수집-자동화 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="63727-165">Hello runbook 형식 선택 **PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="63727-166">클릭 **만들기** toocreate hello runbook 및 시작 hello 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="63727-167">복사한 hello hello runbook에 코드를 다음을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="63727-168">Hello 코드 설명 hello 스크립트에서 toohello 메모를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="63727-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="63727-169">4. Runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="63727-169">4. Test runbook</span></span>
<span data-ttu-id="63727-170">Azure 자동화 너무 환경이 포함 되어[runbook을 테스트](../automation/automation-testing-runbook.md) 게시 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="63727-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="63727-171">Hello runbook에서 수집 하는 hello 데이터를 검사할 수 있으며를 쓰는지 tooLog 분석 게시 하기 전에 예상 대로 tooproduction 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Runbook 테스트](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="63727-173">클릭 **저장** toosave hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="63727-174">클릭 **테스트 창** hello 테스트 환경에서 tooopen hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="63727-175">Runbook에 매개 변수가 있으므로 증명된 tooenter 값에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="63727-176">Hello 리소스 그룹의 hello 이름을 입력 하 고 hello 자동화 계정에서 진행 중인 toocollect 작업 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="63727-177">클릭 **시작** toohello hello runbook을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="63727-178">hello runbook의 상태로 시작 됩니다 **큐 대기** 너무 상태가 되기 전에**실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="63727-179">hello runbook에 대 한 json 형식으로 수집 하는 hello 작업 자세한 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="63727-180">작업이 목록에 없으면 다음 되었을 수 있습니다 지난 1 시간 동안 hello에 hello 자동화 계정에서 만든 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="63727-181">Hello 자동화 계정의 모든 runbook을 시작 해 보십시오 하 고 hello 테스트를 다시 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="63727-182">Hello 출력 명령 tooLog 분석을 게시 하는 hello의 모든 오류를 표시 하지 않음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="63727-183">메시지와 비슷한 toohello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-183">You should have a message similar toohello following.</span></span>

    ![POST 출력](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="63727-185">5. Log Analytics의 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="63727-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="63727-186">테스트에서는 hello runbook이 완료 된 hello 출력 성공적으로 받았음을 확인 되 면 hello 레코드를 사용 하 여 만든 있는지 확인할 수 있습니다는 [로그 분석에서 로그 검색](../log-analytics/log-analytics-log-searches.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![로그 출력](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="63727-188">Hello Azure 포털에서에서 로그 분석 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="63727-189">**로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="63727-190">다음 명령을 형식 hello `Type=AutomationJob_CL` hello 검색 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="63727-191">Note hello 레코드 종류에는 hello 스크립트에 지정 되지 않은 _CL 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63727-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="63727-192">해당 접미사는 자동으로 추가 된 toohello 로그 형식 tooindicate는 사용자 지정 로그 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="63727-193">해당 hello runbook이 예상 대로 작동 나타내는 반환 하는 하나 이상의 레코드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63727-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="63727-194">6. Hello runbook을 게시</span><span class="sxs-lookup"><span data-stu-id="63727-194">6. Publish hello runbook</span></span>
<span data-ttu-id="63727-195">Toopublish 해당 hello runbook이 제대로 작동을 확인 한 후 해야 되므로 프로덕션 환경에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="63727-196">Tooedit 계속 하 고 hello 게시 된 버전을 수정 하지 않고 hello runbook을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Runbook 게시](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="63727-198">Tooyour 자동화 계정을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="63727-199">**Runbook**을 클릭하고 **Collect-Automation-jobs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="63727-200">**편집**, **게시**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="63727-201">클릭 **예** 묻는 tooverify toooverwrite hello를 이전에 사용할 버전을 게시 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="63727-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="63727-202">7. 로깅 옵션 설정</span><span class="sxs-lookup"><span data-stu-id="63727-202">7. Set logging options</span></span> 
<span data-ttu-id="63727-203">테스트를 위해 수 tooview 있었습니다 [자세한 정보를 출력](../automation/automation-runbook-output-and-messages.md#message-streams) hello 스크립트에 hello $VerbosePreference 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="63727-204">프로덕션 hello runbook에 대 한 tooset hello 로깅 속성 tooview 자세한 정보를 출력 하려는 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="63727-205">이 자습서에 사용 된 hello runbook에 대 한 hello json 데이터 분석 tooLog 송신할이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63727-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![로깅 및 추적](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="63727-207">Runbook에 대 한 hello 속성에서 선택 **로깅 및 추적** 아래 **Runbook 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="63727-208">에 대 한 hello 설정을 변경 **상세 레코드를 기록** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="63727-209">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="63727-210">8. Runbook 예약</span><span class="sxs-lookup"><span data-stu-id="63727-210">8. Schedule runbook</span></span>
<span data-ttu-id="63727-211">hello 가장 일반적인 방법은 toostart 모니터링 데이터를 수집 하는 runbook은 tooschedule 것 toorun 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="63727-212">만들어서이 작업을 수행는 [Azure 자동화의 일정](../automation/automation-schedules.md) 및 tooyour runbook을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Runbook 예약](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="63727-214">Runbook에 대 한 hello 속성에서 선택 **일정** 아래 **리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="63727-215">클릭 **일정을 추가할** > **일정 tooyour runbook을 연결** > **새 일정을 만들려면**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="63727-216">Hello hello 일정 및 클릭에 대 한 값을 뒤에 형식 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="63727-217">속성</span><span class="sxs-lookup"><span data-stu-id="63727-217">Property</span></span> | <span data-ttu-id="63727-218">값</span><span class="sxs-lookup"><span data-stu-id="63727-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="63727-219">이름</span><span class="sxs-lookup"><span data-stu-id="63727-219">Name</span></span> | <span data-ttu-id="63727-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="63727-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="63727-221">Starts</span><span class="sxs-lookup"><span data-stu-id="63727-221">Starts</span></span> | <span data-ttu-id="63727-222">언제 든 지 5 분 이상 지난 hello 현재 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="63727-223">되풀이</span><span class="sxs-lookup"><span data-stu-id="63727-223">Recurrence</span></span> | <span data-ttu-id="63727-224">Recurring</span><span class="sxs-lookup"><span data-stu-id="63727-224">Recurring</span></span> |
| <span data-ttu-id="63727-225">Recur every</span><span class="sxs-lookup"><span data-stu-id="63727-225">Recur every</span></span> | <span data-ttu-id="63727-226">1시간</span><span class="sxs-lookup"><span data-stu-id="63727-226">1 hour</span></span> |
| <span data-ttu-id="63727-227">Set expiration</span><span class="sxs-lookup"><span data-stu-id="63727-227">Set expiration</span></span> | <span data-ttu-id="63727-228">아니요</span><span class="sxs-lookup"><span data-stu-id="63727-228">No</span></span> |

<span data-ttu-id="63727-229">Hello 일정을 만든 후 tooset hello 매개 변수 값이이 일정 hello runbook 시작 될 때마다 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="63727-230">**매개 변수 및 실행 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="63727-231">**ResourceGroupName** 및 **AutomationAccountName**에 대한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="63727-232">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="63727-233">9. Runbook이 일정에 맞게 시작되는지 확인</span><span class="sxs-lookup"><span data-stu-id="63727-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="63727-234">Runbook이 시작될 때마다 [작업이 만들어지고](../automation/automation-runbook-execution.md) 모든 출력이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="63727-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="63727-235">사실, 이들은 runbook hello 동일한 작업을 수집 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="63727-236">Hello 일정에 대 한 hello 시작 시간 경과 된 후 hello hello runbook 작업을 확인 하 여 예상 대로 해당 hello runbook 시작을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63727-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![작업](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="63727-238">Runbook에 대 한 hello 속성에서 선택 **작업** 아래 **리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="63727-239">시작 된 각 시간 hello runbook에 대 한 작업 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63727-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="63727-240">세부 정보 hello 작업 tooview 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="63727-241">클릭 **모든 로그** tooview hello 로그 및 hello runbook에서 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="63727-242">Toohello 아래쪽 toofind 아래 항목 비슷한 toohello 이미지를 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="63727-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![자세한 정보 표시](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="63727-244">이 항목을 클릭 tooview hello tooLog 분석 보낸 json 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="63727-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63727-245">Next steps</span></span>
- <span data-ttu-id="63727-246">사용 하 여 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md) 표시 뷰 toocreate hello toohello 로그 분석 저장소 수집한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="63727-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="63727-247">runbook을 패키지는 [관리 솔루션](operations-management-suite-solutions-creating.md) toodistribute toocustomers 합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="63727-248">[Log Analytics](https://docs.microsoft.com/azure/log-analytics/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="63727-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="63727-249">[Azure Automation](https://docs.microsoft.com/azure/automation/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="63727-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="63727-250">Hello에 대 한 자세한 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="63727-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
