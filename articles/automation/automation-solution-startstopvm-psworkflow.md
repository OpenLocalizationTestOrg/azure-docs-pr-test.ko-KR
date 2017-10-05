---
title: "Azure 자동화로 가상 컴퓨터 시작 및 중지 - PowerShell 워크플로 | Microsoft Docs"
description: "기존 가상 컴퓨터를 시작 또는 중지하기 위해 Runbook을 포함하는 Azure 자동화 시나리오의 그래픽 버전"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="6700b-103">Azure 자동화 시나리오 - 가상 컴퓨터 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="6700b-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="6700b-104">Azure 자동화 시나리오는 기존 가상 컴퓨터를 시작하고 중지하는 Runbook을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="6700b-105">다음과 같은 경우에 이 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="6700b-106">사용자의 환경에서 수정하지 않고 Runbook을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="6700b-107">사용자 지정 기능을 수행하도록 Runbook을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="6700b-108">전체 솔루션의 일부로 다른 Runbook에서 Runbook을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="6700b-109">Runbook을 자습서로 사용하여 Runbook 작성 개념을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6700b-110">그래픽</span><span class="sxs-lookup"><span data-stu-id="6700b-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="6700b-111">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="6700b-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="6700b-112">이 시나리오의 PowerShell 워크플로 Runbook 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="6700b-113">[그래픽 Runbook](automation-solution-startstopvm-graphical.md)을 사용하여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="6700b-114">시나리오 가져오기</span><span class="sxs-lookup"><span data-stu-id="6700b-114">Getting the scenario</span></span>
<span data-ttu-id="6700b-115">이 시나리오는 다음 링크에서 다운로드할 수 있는 PowerShell 워크플로 Runbook으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="6700b-116">그래픽 Runbook에 대한 링크는 이 시나리오의 [그래픽 버전](automation-solution-startstopvm-graphical.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6700b-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="6700b-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="6700b-117">Runbook</span></span> | <span data-ttu-id="6700b-118">링크</span><span class="sxs-lookup"><span data-stu-id="6700b-118">Link</span></span> | <span data-ttu-id="6700b-119">형식</span><span class="sxs-lookup"><span data-stu-id="6700b-119">Type</span></span> | <span data-ttu-id="6700b-120">설명</span><span class="sxs-lookup"><span data-stu-id="6700b-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6700b-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-121">Start-AzureVMs</span></span> |[<span data-ttu-id="6700b-122">Azure 클래식 VM 시작</span><span class="sxs-lookup"><span data-stu-id="6700b-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="6700b-123">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="6700b-123">PowerShell Workflow</span></span> |<span data-ttu-id="6700b-124">Azure 구독의 모든 기존 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="6700b-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="6700b-126">Azure 클래식 VM 중지</span><span class="sxs-lookup"><span data-stu-id="6700b-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="6700b-127">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="6700b-127">PowerShell Workflow</span></span> |<span data-ttu-id="6700b-128">자동화 계정의 모든 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="6700b-129">시나리오 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="6700b-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="6700b-130">1. Runbook 설치</span><span class="sxs-lookup"><span data-stu-id="6700b-130">1. Install the runbooks</span></span>
<span data-ttu-id="6700b-131">Runbook을 다운로드한 후에 [Runbook 가져오기](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)의 절차를 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="6700b-132">2. 설명 및 요구 사항 검토</span><span class="sxs-lookup"><span data-stu-id="6700b-132">2. Review the description and requirements</span></span>
<span data-ttu-id="6700b-133">Runbook은 설명 및 필수 자산을 포함하는 주석 처리된 도움말 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="6700b-134">이 문서에서 동일한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="6700b-135">3. 자산 구성</span><span class="sxs-lookup"><span data-stu-id="6700b-135">3. Configure assets</span></span>
<span data-ttu-id="6700b-136">Runbook은 적절한 값으로 생성하고 채워야 하는 다음 자산을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="6700b-137">자산 형식</span><span class="sxs-lookup"><span data-stu-id="6700b-137">Asset Type</span></span> | <span data-ttu-id="6700b-138">자산 이름</span><span class="sxs-lookup"><span data-stu-id="6700b-138">Asset Name</span></span> | <span data-ttu-id="6700b-139">설명</span><span class="sxs-lookup"><span data-stu-id="6700b-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6700b-140">자격 증명</span><span class="sxs-lookup"><span data-stu-id="6700b-140">Credential</span></span> |<span data-ttu-id="6700b-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="6700b-141">AzureCredential</span></span> |<span data-ttu-id="6700b-142">Azure 구독에서 가상 컴퓨터를 시작 및 중지할 권한이 있는 계정에 대한 자격 증명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="6700b-143">**Add-AzureAccount** 활동의 **Credential** 매개 변수에 다른 자격 증명 자산을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="6700b-144">변수</span><span class="sxs-lookup"><span data-stu-id="6700b-144">Variable</span></span> |<span data-ttu-id="6700b-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="6700b-145">AzureSubscriptionId</span></span> |<span data-ttu-id="6700b-146">Azure 구독의 구독 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="6700b-147">시나리오 사용</span><span class="sxs-lookup"><span data-stu-id="6700b-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="6700b-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6700b-148">Parameters</span></span>
<span data-ttu-id="6700b-149">각 Runbook에는 다음과 같은 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="6700b-150">모든 필수 매개 변수에 대한 값을 제공해야 하며 요구 사항에 따라 다른 매개 변수에 대한 값을 선택적으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="6700b-151">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6700b-151">Parameter</span></span> | <span data-ttu-id="6700b-152">형식</span><span class="sxs-lookup"><span data-stu-id="6700b-152">Type</span></span> | <span data-ttu-id="6700b-153">필수</span><span class="sxs-lookup"><span data-stu-id="6700b-153">Mandatory</span></span> | <span data-ttu-id="6700b-154">설명</span><span class="sxs-lookup"><span data-stu-id="6700b-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6700b-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="6700b-155">ServiceName</span></span> |<span data-ttu-id="6700b-156">string</span><span class="sxs-lookup"><span data-stu-id="6700b-156">string</span></span> |<span data-ttu-id="6700b-157">아니요</span><span class="sxs-lookup"><span data-stu-id="6700b-157">No</span></span> |<span data-ttu-id="6700b-158">값이 제공되면 해당 서비스 이름의 모든 가상 컴퓨터가 시작되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="6700b-159">값이 제공되지 않으면 Azure 구독의 모든 기존 가상 컴퓨터가 시작되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="6700b-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="6700b-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="6700b-161">string</span><span class="sxs-lookup"><span data-stu-id="6700b-161">string</span></span> |<span data-ttu-id="6700b-162">아니요</span><span class="sxs-lookup"><span data-stu-id="6700b-162">No</span></span> |<span data-ttu-id="6700b-163">Azure 구독의 구독 ID를 포함하는 [변수 자산](#installing-and-configuring-the-scenario) 의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="6700b-164">값을 지정하지 않으면 *AzureSubscriptionId* 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="6700b-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="6700b-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="6700b-166">string</span><span class="sxs-lookup"><span data-stu-id="6700b-166">string</span></span> |<span data-ttu-id="6700b-167">아니요</span><span class="sxs-lookup"><span data-stu-id="6700b-167">No</span></span> |<span data-ttu-id="6700b-168">사용할 Runbook에 대한 자격 증명을 포함하는 [자격 증명 자산](#installing-and-configuring-the-scenario) 의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="6700b-169">값을 지정하지 않으면 *AzureCredential* 이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="6700b-170">Runbook 시작</span><span class="sxs-lookup"><span data-stu-id="6700b-170">Starting the runbooks</span></span>
<span data-ttu-id="6700b-171">이 시나리오의 Runbook 중 하나를 시작하도록 [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md) 의 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="6700b-172">다음 샘플 명령은 서비스 이름이 **MyVMService** 인 모든 가상 컴퓨터를 시작하기 위하여 *StartAzureVMs*을 실행하도록 Windows PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="6700b-173">출력</span><span class="sxs-lookup"><span data-stu-id="6700b-173">Output</span></span>
<span data-ttu-id="6700b-174">Runbook은 각각의 가상 컴퓨터에 대해 시작 또는 중지 명령이 성공적으로 제출되었는지 여부를 나타내는 [메시지를 출력](automation-runbook-output-and-messages.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="6700b-175">출력물에서 특정 문자열을 찾아서 각 Runbook에 대한 결과를 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="6700b-176">가능한 출력 문자열이 다음 테이블에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="6700b-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="6700b-177">Runbook</span></span> | <span data-ttu-id="6700b-178">조건</span><span class="sxs-lookup"><span data-stu-id="6700b-178">Condition</span></span> | <span data-ttu-id="6700b-179">Message</span><span class="sxs-lookup"><span data-stu-id="6700b-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="6700b-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-180">Start-AzureVMs</span></span> |<span data-ttu-id="6700b-181">가상 컴퓨터 이미 실행 중</span><span class="sxs-lookup"><span data-stu-id="6700b-181">Virtual machine is already running</span></span> |<span data-ttu-id="6700b-182">MyVM 이미 실행 중</span><span class="sxs-lookup"><span data-stu-id="6700b-182">MyVM is already running</span></span> |
| <span data-ttu-id="6700b-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-183">Start-AzureVMs</span></span> |<span data-ttu-id="6700b-184">가상 컴퓨터에 대한 시작 요청이 성공적으로 제출됨</span><span class="sxs-lookup"><span data-stu-id="6700b-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="6700b-185">MyVM 시작됨</span><span class="sxs-lookup"><span data-stu-id="6700b-185">MyVM has been started</span></span> |
| <span data-ttu-id="6700b-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-186">Start-AzureVMs</span></span> |<span data-ttu-id="6700b-187">가상 컴퓨터에 대한 시작 요청 실패</span><span class="sxs-lookup"><span data-stu-id="6700b-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="6700b-188">MyVM 시작 실패</span><span class="sxs-lookup"><span data-stu-id="6700b-188">MyVM failed to start</span></span> |
| <span data-ttu-id="6700b-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-189">Stop-AzureVMs</span></span> |<span data-ttu-id="6700b-190">가상 컴퓨터가 이미 중지됨</span><span class="sxs-lookup"><span data-stu-id="6700b-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="6700b-191">MyVM 이미 중지됨</span><span class="sxs-lookup"><span data-stu-id="6700b-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="6700b-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-192">Stop-AzureVMs</span></span> |<span data-ttu-id="6700b-193">가상 컴퓨터에 대한 중지 요청이 성공적으로 제출됨</span><span class="sxs-lookup"><span data-stu-id="6700b-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="6700b-194">MyVM 중지됨</span><span class="sxs-lookup"><span data-stu-id="6700b-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="6700b-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="6700b-195">Stop-AzureVMs</span></span> |<span data-ttu-id="6700b-196">가상 컴퓨터에 대한 중지 요청 실패</span><span class="sxs-lookup"><span data-stu-id="6700b-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="6700b-197">MyVM 중지 실패</span><span class="sxs-lookup"><span data-stu-id="6700b-197">MyVM failed to stop</span></span> |

<span data-ttu-id="6700b-198">예를 들어 Runbook의 다음 코드 조각은 서비스 이름이 *MyServiceName*인 모든 가상 컴퓨터를 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="6700b-199">실패하는 시작 요청이 있으면 오류 작업에 착수할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="6700b-200">자세한 분석</span><span class="sxs-lookup"><span data-stu-id="6700b-200">Detailed breakdown</span></span>
<span data-ttu-id="6700b-201">다음은 이 시나리오의 Runbook에 대한 자세한 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="6700b-202">이 정보를 사용하여 Runbook을 사용자 지정하거나 자체 자동화 시나리오를 작성하기 위한 학습에 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="6700b-203">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6700b-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="6700b-204">워크플로는 [입력 매개 변수](#using-the-scenario)의 값을 가져오면서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="6700b-205">자산 이름이 제공되지 않으면 기본 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="6700b-206">출력</span><span class="sxs-lookup"><span data-stu-id="6700b-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="6700b-207">이 줄은 Runbook의 출력이 문자열임을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="6700b-208">꼭 필요하지는 않지만 Runbook이 [자식 Runbook](automation-child-runbooks.md) 으로 사용되는 경우 부모 Runbook이 예상 출력 형식을 알 수 있도록 하기 위한 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="6700b-209">인증</span><span class="sxs-lookup"><span data-stu-id="6700b-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="6700b-210">다음 줄은 Runbook 나머지 부분에서 사용될 Azure 구독 및 [자격 증명](automation-credentials.md) 을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="6700b-211">우선 Azure 구독에서 가상 컴퓨터를 시작 및 중지하기 위해 자격 증명을 포함하는 자산을 가져오도록 **Get-AutomationPSCredential** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="6700b-212">**Credential** 에서 이 자산을 사용하여 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="6700b-213">출력은 Runbook 출력에 포함되지 않도록 더미 변수에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="6700b-214">**Get-AutomationVariable**로 구독 ID를 포함하는 변수 자산이 검색되며 **Select-AzureSubscription**으로 구독 세트가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="6700b-215">VM 가져오기</span><span class="sxs-lookup"><span data-stu-id="6700b-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="6700b-216">**Get-AzureVM** 이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="6700b-217">**ServiceName** 입력 변수에 값이 제공되면 해당 서비스 이름을 갖는 가상 컴퓨터만 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="6700b-218">**ServiceName** 을 비워두면 모든 가상 컴퓨터가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="6700b-219">가상 컴퓨터 시작/중지 및 출력 보내기</span><span class="sxs-lookup"><span data-stu-id="6700b-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="6700b-220">다음 줄은 각각의 가상 컴퓨터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="6700b-221">우선 가상 컴퓨터가 실행 중인지, 중지되었는지(Runbook에 따라서) 파악하기 위해 가상 컴퓨터의 **PowerState**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="6700b-222">이미 대상 상태이면 메시지가 출력을 위해 전송되고 runbook은 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="6700b-223">그렇지 않으면 변수에 저장된 요청의 결과를 사용하여 가상 컴퓨터를 시작 또는 중지하기 위해 **Start-AzureVM** 또는 **Stop-AzureVM**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="6700b-224">그러면 시작 또는 중지 요청이 성공적으로 제출되었는지를 알리는 메시지가 출력을 위해 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6700b-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6700b-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6700b-225">Next steps</span></span>
* <span data-ttu-id="6700b-226">자식 Runbook으로 작업하는 방법에 대해 자세히 알아보려면 [Azure 자동화의 자식 Runbook](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="6700b-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="6700b-227">문제를 해결하기 위해 Runbook을 실행 및 로깅하는 동안 출력 메시지에 대해 알아보려면 [Azure 자동화에서 Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="6700b-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

