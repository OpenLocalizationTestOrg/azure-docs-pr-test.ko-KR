---
title: "Azure Automation에서 Runbook을 사용하여 Log Analytics 데이터 수집 | Microsoft Docs"
description: "Azure Automation에서 Runbook을 만들어 Log Analytics에서 분석할 수 있게 OMS 리포지토리에 데이터를 수집하는 과정을 안내하는 단계별 자습서입니다."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="5b3c9-103">Azure Automation Runbook을 사용하여 Log Analytics에서 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="5b3c9-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="5b3c9-104">에이전트의 [데이터 원본](../log-analytics/log-analytics-data-sources.md)을 비롯한 다양한 원본에서 Log Analytics으로 대량의 데이터를 수집할 수 있고 [Azure에서 수집된 데이터](../log-analytics/log-analytics-azure-storage.md)도 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="5b3c9-105">이러한 표준 원본을 통해 액세스할 수 없는 데이터를 수집해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="5b3c9-106">이러한 경우 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md)를 사용하여 REST API 클라이언트에서 Log Analytics로 데이터를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="5b3c9-107">이 데이터 수집을 수행하는 일반적인 방법은 Azure Automation에서 Runbook을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="5b3c9-108">이 자습서는 Azure Automation에서 Runbook을 만들고 Log Analytics에 데이터를 쓰도록 예약하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5b3c9-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5b3c9-109">Prerequisites</span></span>
<span data-ttu-id="5b3c9-110">이 시나리오를 수행하려면 다음 리소스가 Azure 구독에 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="5b3c9-111">둘 다 무료 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-111">Both can be a free account.</span></span>

- <span data-ttu-id="5b3c9-112">[Log Analytics 작업 영역](../log-analytics/log-analytics-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5b3c9-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="5b3c9-113">[Azure Automation 계정](../automation/automation-offering-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5b3c9-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="5b3c9-114">시나리오의 개요</span><span class="sxs-lookup"><span data-stu-id="5b3c9-114">Overview of scenario</span></span>
<span data-ttu-id="5b3c9-115">이 자습서에서는 Automation 작업에 대한 정보를 수집하는 Runbook을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="5b3c9-116">Azure Automation의 Runbook은 PowerShell을 통해 구현되므로 먼저 Azure Automation 편집기에서 스크립트를 작성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="5b3c9-117">필요한 정보를 제대로 수집하고 있는지 확인한 후에는 해당 데이터를 Log Analytics에 쓰고 사용자 지정 데이터 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="5b3c9-118">마지막으로 정기적으로 Runbokk을 시작하는 일정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="5b3c9-119">이 Runbook 없이도 작업 정보를 Log Analytics로 전송하도록 Azure Automation을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="5b3c9-120">이 시나리오는 기본적으로 이 자습서를 지원하는 데 사용되며, 데이터를 테스트 작업 영역으로 전송하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="5b3c9-121">1. 데이터 수집기 API 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5b3c9-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="5b3c9-122">모든 [HTTP 데이터 수집기 API의 요청](../log-analytics/log-analytics-data-collector-api.md#create-a-request)은 서식을 적절히 지정해야 하며 권한 부여 헤더를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="5b3c9-123">Runbook에서 이 작업을 수행할 수 있지만 이 프로세스를 간소화하는 모듈을 사용하여 필요한 코드의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="5b3c9-124">사용할 수 있는 모듈 하나는 PowerShell 갤러리에 있는 [OMSIngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI)입니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="5b3c9-125">Runbook에서 [모듈](../automation/automation-integration-modules.md)을 사용하려면 Automation 계정에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="5b3c9-126">그러면 같은 계정에 있는 모든 Runbook이 해당 모듈의 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="5b3c9-127">Automation 계정에서 **자산** > **모듈** > **모듈 추가**를 선택하여 새 모듈을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="5b3c9-128">그러나 PowerShell 갤러리는 Automation 계정으로 직접 모듈을 배포할 수 있는 빠른 옵션을 제공하므로, 이 자습서를 위해 해당 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI 모듈](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="5b3c9-130">[PowerShell 갤러리](https://www.powershellgallery.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="5b3c9-131">**OMSIngestionAPI**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="5b3c9-132">**Azure Automation에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="5b3c9-133">Automation 계정을 선택하고 **확인**을 클릭하여 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="5b3c9-134">2. Automation 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="5b3c9-134">2. Create Automation variables</span></span>
<span data-ttu-id="5b3c9-135">[Automation 변수](..\automation\automation-variables.md)는 Automation 계정의 모든 Runbook에서 사용할 수 있는 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="5b3c9-136">이러한 변수를 사용하면 실제 Runbook을 편집하지 않고도 이러한 값을 변경할 수 있으므로 훨씬 유연하게 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="5b3c9-137">HTTP 데이터 수집기 API의 모든 요청에는 OMS 작업 영역의 ID 및 키가 필요하며 변수 자산은 이 정보를 저장하는 데 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![변수](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="5b3c9-139">Azure Portal에서 Automation 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="5b3c9-140">**공유 리소스**에서 **변수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="5b3c9-141">**변수 추가**를 클릭하고 다음 표에 나오는 두 가지 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="5b3c9-142">속성</span><span class="sxs-lookup"><span data-stu-id="5b3c9-142">Property</span></span> | <span data-ttu-id="5b3c9-143">작업 영역 ID 값</span><span class="sxs-lookup"><span data-stu-id="5b3c9-143">Workspace ID Value</span></span> | <span data-ttu-id="5b3c9-144">작업 영역 키 값</span><span class="sxs-lookup"><span data-stu-id="5b3c9-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="5b3c9-145">이름</span><span class="sxs-lookup"><span data-stu-id="5b3c9-145">Name</span></span> | <span data-ttu-id="5b3c9-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="5b3c9-146">WorkspaceId</span></span> | <span data-ttu-id="5b3c9-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="5b3c9-147">WorkspaceKey</span></span> |
| <span data-ttu-id="5b3c9-148">유형</span><span class="sxs-lookup"><span data-stu-id="5b3c9-148">Type</span></span> | <span data-ttu-id="5b3c9-149">문자열</span><span class="sxs-lookup"><span data-stu-id="5b3c9-149">String</span></span> | <span data-ttu-id="5b3c9-150">문자열</span><span class="sxs-lookup"><span data-stu-id="5b3c9-150">String</span></span> |
| <span data-ttu-id="5b3c9-151">값</span><span class="sxs-lookup"><span data-stu-id="5b3c9-151">Value</span></span> | <span data-ttu-id="5b3c9-152">Log Analytics 작업 영역의 작업 영역 ID를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="5b3c9-153">Log Analytics 작업 영역의 기본 또는 보조 키와 함께 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="5b3c9-154">암호화</span><span class="sxs-lookup"><span data-stu-id="5b3c9-154">Encrypted</span></span> | <span data-ttu-id="5b3c9-155">아니요</span><span class="sxs-lookup"><span data-stu-id="5b3c9-155">No</span></span> | <span data-ttu-id="5b3c9-156">예</span><span class="sxs-lookup"><span data-stu-id="5b3c9-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="5b3c9-157">3. runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="5b3c9-157">3. Create runbook</span></span>

<span data-ttu-id="5b3c9-158">Azure Automation은 포털에 Runbook을 편집하고 테스트할 수 있는 편집기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="5b3c9-159">스크립트 편집기를 사용하여 [PowerShell을 직접](../automation/automation-edit-textual-runbook.md) 사용하거나 [그래픽 Runbook을 만들](../automation/automation-graphical-authoring-intro.md) 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="5b3c9-160">이 자습서에서는 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook 편집](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="5b3c9-162">Automation 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="5b3c9-163">**Runbook** > **Runbook 추가** > **새 Runbook 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="5b3c9-164">Runbook 이름으로 **Collect-Automation-jobs**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="5b3c9-165">Runbook 형식으로 **PowerShell**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="5b3c9-166">**만들기**를 클릭하여 Runbook을 만들고 편집기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="5b3c9-167">다음 코드를 복사하여 Runbook에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="5b3c9-168">코드 설명을 보려면 스크립트에 있는 주석을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="5b3c9-169">4. Runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="5b3c9-169">4. Test runbook</span></span>
<span data-ttu-id="5b3c9-170">Azure Automation에는 Runbook을 게시하기 전에 [runbook을 테스트](../automation/automation-testing-runbook.md)하는 환경이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="5b3c9-171">Runbook에서 수집한 데이터를 검사하고, Runbook이 데이터를 프로덕션에 게시하기 전에 예상대로 Log Analytics에 쓰는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Runbook 테스트](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="5b3c9-173">**저장**을 클릭하여 Runbook을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="5b3c9-174">**테스트 창**을 클릭하여 Runbook을 테스트 환경에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="5b3c9-175">Runbook에 매개 변수가 있으므로 해당 값을 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="5b3c9-176">작업 정보를 수집하려는 리소스 그룹 및 Automation 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="5b3c9-177">**시작**을 클릭하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="5b3c9-178">Runbook은 **대기** 상태로 시작한 후 **실행 중** 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="5b3c9-179">Runbook은 수집된 작업을 포함하는 자세한 출력을 JSON 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="5b3c9-180">작업이 목록에 없으면 마지막 시간에 Automation 계정에서 만들어진 작업이 없는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="5b3c9-181">Automation 계정에서 Runbook을 시작한 다음 테스트를 다시 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="5b3c9-182">Log Analytics에 대한 POST 명령 출력에 오류가 표시되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="5b3c9-183">다음과 유사한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-183">You should have a message similar to the following.</span></span>

    ![POST 출력](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="5b3c9-185">5. Log Analytics의 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="5b3c9-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="5b3c9-186">Runbook 테스트가 완료되고 출력이 성공적으로 수신되었음을 확인한 후에는 [Log Analytics의 로그 검색](../log-analytics/log-analytics-log-searches.md)을 사용하여 레코드를 생성되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![로그 출력](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="5b3c9-188">Azure Portal에서 Log Analytics 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="5b3c9-189">**로그 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="5b3c9-190">다음 명령 `Type=AutomationJob_CL`을 입력하고 검색 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="5b3c9-191">레코드 형식에 스크립트에 지정되지 않은 _CL이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="5b3c9-192">이 접미사는 사용자 지정 로그 형식임을 나타내기 위해 로그 형식에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="5b3c9-193">Runbook이 예상대로 작동하고 있음을 나타내는 반환된 하나 이상의 레코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="5b3c9-194">6. Runbook 게시</span><span class="sxs-lookup"><span data-stu-id="5b3c9-194">6. Publish the runbook</span></span>
<span data-ttu-id="5b3c9-195">Runbook이 올바르게 작동하는지 확인한 후에는 프로덕션 환경에서 실행할 수 있도록 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="5b3c9-196">게시된 버전을 수정하지 않고 Runbook을 계속해서 편집하고 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Runbook 게시](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="5b3c9-198">Automation 계정으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-198">Return to your automation account.</span></span>
2. <span data-ttu-id="5b3c9-199">**Runbook**을 클릭하고 **Collect-Automation-jobs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="5b3c9-200">**편집**, **게시**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="5b3c9-201">이전에 게시된 버전을 덮어쓸 것인지 확인하도록 요청되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="5b3c9-202">7. 로깅 옵션 설정</span><span class="sxs-lookup"><span data-stu-id="5b3c9-202">7. Set logging options</span></span> 
<span data-ttu-id="5b3c9-203">테스트의 경우 스크립트에 $VerbosePreference 변수를 설정했으므로 [자세한 정보 출력](../automation/automation-runbook-output-and-messages.md#message-streams)을 볼 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="5b3c9-204">프로덕션의 경우에는 자세한 정보 출력을 보려면 Runbook의 로깅 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="5b3c9-205">이 자습서에 사용된 Runbook의 경우 Log Analytics으로 전송되는 JSON 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![로깅 및 추적](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="5b3c9-207">Runbook에 대한 속성의 **Runbook 설정**에서 **로깅 및 추적**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="5b3c9-208">**상세 레코드 기록**에 대한 설정을 **설정**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="5b3c9-209">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="5b3c9-210">8. Runbook 예약</span><span class="sxs-lookup"><span data-stu-id="5b3c9-210">8. Schedule runbook</span></span>
<span data-ttu-id="5b3c9-211">모니터링 데이터를 수집하는 Runbook을 시작하는 가장 일반적인 방법은 자동으로 실행되도록 예약하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="5b3c9-212">이를 위해 [Azure Automation에서 일정](../automation/automation-schedules.md)을 만들고 Runbook에 첨부하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Runbook 예약](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="5b3c9-214">Runbook에 대한 속성의 **리소스**에서 **일정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="5b3c9-215">**일정 추가** > **Runbook에 일정 연결** > **새 일정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="5b3c9-216">일정에 대해 다음 값을 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="5b3c9-217">속성</span><span class="sxs-lookup"><span data-stu-id="5b3c9-217">Property</span></span> | <span data-ttu-id="5b3c9-218">값</span><span class="sxs-lookup"><span data-stu-id="5b3c9-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="5b3c9-219">이름</span><span class="sxs-lookup"><span data-stu-id="5b3c9-219">Name</span></span> | <span data-ttu-id="5b3c9-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="5b3c9-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="5b3c9-221">Starts</span><span class="sxs-lookup"><span data-stu-id="5b3c9-221">Starts</span></span> | <span data-ttu-id="5b3c9-222">현재 시간보다 적어도 5분 이후의 아무 시간이나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="5b3c9-223">되풀이</span><span class="sxs-lookup"><span data-stu-id="5b3c9-223">Recurrence</span></span> | <span data-ttu-id="5b3c9-224">Recurring</span><span class="sxs-lookup"><span data-stu-id="5b3c9-224">Recurring</span></span> |
| <span data-ttu-id="5b3c9-225">Recur every</span><span class="sxs-lookup"><span data-stu-id="5b3c9-225">Recur every</span></span> | <span data-ttu-id="5b3c9-226">1시간</span><span class="sxs-lookup"><span data-stu-id="5b3c9-226">1 hour</span></span> |
| <span data-ttu-id="5b3c9-227">Set expiration</span><span class="sxs-lookup"><span data-stu-id="5b3c9-227">Set expiration</span></span> | <span data-ttu-id="5b3c9-228">아니요</span><span class="sxs-lookup"><span data-stu-id="5b3c9-228">No</span></span> |

<span data-ttu-id="5b3c9-229">일정을 만든 후에는 이 일정에 따라 Runbook이 시작될 때마다 사용되는 매개 변수 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="5b3c9-230">**매개 변수 및 실행 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="5b3c9-231">**ResourceGroupName** 및 **AutomationAccountName**에 대한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="5b3c9-232">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="5b3c9-233">9. Runbook이 일정에 맞게 시작되는지 확인</span><span class="sxs-lookup"><span data-stu-id="5b3c9-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="5b3c9-234">Runbook이 시작될 때마다 [작업이 만들어지고](../automation/automation-runbook-execution.md) 모든 출력이 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="5b3c9-235">실제로는 Runbook이 수집하는 작업과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="5b3c9-236">일정 시작 시간이 경과된 후 Runbook에 대한 작업을 확인하여 Runbook이 예상대로 시작되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![작업](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="5b3c9-238">Runbook에 대한 속성의 **리소스**에서 **작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="5b3c9-239">Runbook이 시작될 때마다 작업 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="5b3c9-240">해당 정보를 보려면 작업 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="5b3c9-241">Runbook의 로그 및 출력을 보려면 **모든 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="5b3c9-242">아래 이미지와 유사한 항목을 찾을 때까지 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![자세한 정보 표시](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="5b3c9-244">Log Analytics으로 전송된 자세한 JSON 데이터를 보려면 이 항목을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="5b3c9-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b3c9-245">Next steps</span></span>
- <span data-ttu-id="5b3c9-246">[뷰 디자이너](../log-analytics/log-analytics-view-designer.md)를 사용하여 Log Analytics 리포지토리로 수집한 데이터를 표시하는 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="5b3c9-247">Runbook을 [관리 솔루션](operations-management-suite-solutions-creating.md)으로 패키지하여 고객에게 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5b3c9-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="5b3c9-248">[Log Analytics](https://docs.microsoft.com/azure/log-analytics/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5b3c9-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="5b3c9-249">[Azure Automation](https://docs.microsoft.com/azure/automation/)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5b3c9-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="5b3c9-250">[HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5b3c9-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>