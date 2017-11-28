---
title: "Azure 자동화-PowerShell 워크플로로 aaaStarting 및 중지와 가상 컴퓨터 | Microsoft Docs"
description: "Runbook 중지 및 toostart 클래식 가상 컴퓨터를 포함 하 여 Azure 자동화 시나리오의 그래픽 버전입니다."
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="a4dfd-103">Azure 자동화 시나리오 - 가상 컴퓨터 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="a4dfd-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="a4dfd-104">이 Azure 자동화 시나리오 runbook toostart 및 중지 클래식 가상 컴퓨터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="a4dfd-105">Hello 다음 중 하나에 대 한이 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="a4dfd-106">사용자 환경에 수정 하지 않고 runbook을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="a4dfd-107">Hello runbook tooperform 사용자 지정 기능을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="a4dfd-108">전체 솔루션의 일부로 다른 runbook에서 hello runbook을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="a4dfd-109">자습서 toolearn runbook 제작 개념으로 hello runbook을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4dfd-110">그래픽</span><span class="sxs-lookup"><span data-stu-id="a4dfd-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="a4dfd-111">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="a4dfd-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="a4dfd-112">이 hello이이 시나리오의 PowerShell 워크플로 runbook 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="a4dfd-113">[그래픽 Runbook](automation-solution-startstopvm-graphical.md)을 사용하여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="a4dfd-114">Hello 시나리오를 가져오기</span><span class="sxs-lookup"><span data-stu-id="a4dfd-114">Getting hello scenario</span></span>
<span data-ttu-id="a4dfd-115">이 시나리오는 hello 다음 링크에서에서 다운로드할 수 있는 두 개의 PowerShell 워크플로 runbook으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="a4dfd-116">Hello 참조 [그래픽 버전](automation-solution-startstopvm-graphical.md) 링크 toohello 그래픽 runbook에 대 한이 시나리오의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="a4dfd-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="a4dfd-117">Runbook</span></span> | <span data-ttu-id="a4dfd-118">링크</span><span class="sxs-lookup"><span data-stu-id="a4dfd-118">Link</span></span> | <span data-ttu-id="a4dfd-119">형식</span><span class="sxs-lookup"><span data-stu-id="a4dfd-119">Type</span></span> | <span data-ttu-id="a4dfd-120">설명</span><span class="sxs-lookup"><span data-stu-id="a4dfd-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a4dfd-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-121">Start-AzureVMs</span></span> |[<span data-ttu-id="a4dfd-122">Azure 클래식 VM 시작</span><span class="sxs-lookup"><span data-stu-id="a4dfd-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="a4dfd-123">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="a4dfd-123">PowerShell Workflow</span></span> |<span data-ttu-id="a4dfd-124">Azure 구독의 모든 기존 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="a4dfd-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="a4dfd-126">Azure 클래식 VM 중지</span><span class="sxs-lookup"><span data-stu-id="a4dfd-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="a4dfd-127">PowerShell 워크플로</span><span class="sxs-lookup"><span data-stu-id="a4dfd-127">PowerShell Workflow</span></span> |<span data-ttu-id="a4dfd-128">자동화 계정의 모든 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="a4dfd-129">설치 하 고 hello 시나리오를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="a4dfd-130">1. Hello runbook을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-130">1. Install hello runbooks</span></span>
<span data-ttu-id="a4dfd-131">Hello runbook에 다운로드 한 후에 가져올 수의 hello 절차를 사용 하 여 [Runbook 가져오기](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="a4dfd-132">2. 검토 hello 설명 및 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a4dfd-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="a4dfd-133">hello runbook에 대 한 설명과 필요한 자산을 포함 하는 주석 처리 된 도움말 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="a4dfd-134">가져올 수도 있습니다 hello이 문서에서 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="a4dfd-135">3. 자산 구성</span><span class="sxs-lookup"><span data-stu-id="a4dfd-135">3. Configure assets</span></span>
<span data-ttu-id="a4dfd-136">hello runbook 자산을 만들고 적절 한 값으로 채우는 해야 다음 hello를 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="a4dfd-137">자산 형식</span><span class="sxs-lookup"><span data-stu-id="a4dfd-137">Asset Type</span></span> | <span data-ttu-id="a4dfd-138">자산 이름</span><span class="sxs-lookup"><span data-stu-id="a4dfd-138">Asset Name</span></span> | <span data-ttu-id="a4dfd-139">설명</span><span class="sxs-lookup"><span data-stu-id="a4dfd-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a4dfd-140">자격 증명</span><span class="sxs-lookup"><span data-stu-id="a4dfd-140">Credential</span></span> |<span data-ttu-id="a4dfd-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="a4dfd-141">AzureCredential</span></span> |<span data-ttu-id="a4dfd-142">Azure 구독 hello 기관 toostart 및 중지할 가상 컴퓨터에 있는 계정의 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="a4dfd-143">Hello에 다른 자격 증명 자산을 지정할 수 또는 **자격 증명** hello의 매개 변수 **Add-azureaccount** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="a4dfd-144">변수</span><span class="sxs-lookup"><span data-stu-id="a4dfd-144">Variable</span></span> |<span data-ttu-id="a4dfd-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a4dfd-145">AzureSubscriptionId</span></span> |<span data-ttu-id="a4dfd-146">Azure 구독 hello 구독 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="a4dfd-147">Hello 시나리오를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a4dfd-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="a4dfd-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a4dfd-148">Parameters</span></span>
<span data-ttu-id="a4dfd-149">hello runbook 매개 변수 뒤 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="a4dfd-150">모든 필수 매개 변수에 대한 값을 제공해야 하며 요구 사항에 따라 다른 매개 변수에 대한 값을 선택적으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="a4dfd-151">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a4dfd-151">Parameter</span></span> | <span data-ttu-id="a4dfd-152">형식</span><span class="sxs-lookup"><span data-stu-id="a4dfd-152">Type</span></span> | <span data-ttu-id="a4dfd-153">필수</span><span class="sxs-lookup"><span data-stu-id="a4dfd-153">Mandatory</span></span> | <span data-ttu-id="a4dfd-154">설명</span><span class="sxs-lookup"><span data-stu-id="a4dfd-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a4dfd-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="a4dfd-155">ServiceName</span></span> |<span data-ttu-id="a4dfd-156">string</span><span class="sxs-lookup"><span data-stu-id="a4dfd-156">string</span></span> |<span data-ttu-id="a4dfd-157">아니요</span><span class="sxs-lookup"><span data-stu-id="a4dfd-157">No</span></span> |<span data-ttu-id="a4dfd-158">값이 제공되면 해당 서비스 이름의 모든 가상 컴퓨터가 시작되거나 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="a4dfd-159">값이 제공 하는 경우 다음 hello Azure 구독이 있는 모든 클래식 가상 컴퓨터의 시작 또는 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="a4dfd-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="a4dfd-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="a4dfd-161">string</span><span class="sxs-lookup"><span data-stu-id="a4dfd-161">string</span></span> |<span data-ttu-id="a4dfd-162">아니요</span><span class="sxs-lookup"><span data-stu-id="a4dfd-162">No</span></span> |<span data-ttu-id="a4dfd-163">Hello의 hello 이름을 포함 [변수 자산](#installing-and-configuring-the-scenario) Azure 구독 hello 구독 ID가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="a4dfd-164">값을 지정하지 않으면 *AzureSubscriptionId* 가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="a4dfd-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="a4dfd-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="a4dfd-166">string</span><span class="sxs-lookup"><span data-stu-id="a4dfd-166">string</span></span> |<span data-ttu-id="a4dfd-167">아니요</span><span class="sxs-lookup"><span data-stu-id="a4dfd-167">No</span></span> |<span data-ttu-id="a4dfd-168">Hello의 hello 이름을 포함 [자격 증명 자산](#installing-and-configuring-the-scenario) runbook toouse hello에 대 한 hello 자격 증명을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="a4dfd-169">값을 지정하지 않으면 *AzureCredential* 이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="a4dfd-170">Hello runbook 시작</span><span class="sxs-lookup"><span data-stu-id="a4dfd-170">Starting hello runbooks</span></span>
<span data-ttu-id="a4dfd-171">Hello 방법 중 하나를 사용할 수 있습니다 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) toostart이이 시나리오에서는 hello runbook 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="a4dfd-172">Windows PowerShell toorun을 사용 하 여 다음 명령 예제는 hello **StartAzureVMs** toostart hello 서비스 이름으로 모든 가상 컴퓨터 *MyVMService*합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="a4dfd-173">출력</span><span class="sxs-lookup"><span data-stu-id="a4dfd-173">Output</span></span>
<span data-ttu-id="a4dfd-174">hello runbook은 [메시지를 출력](automation-runbook-output-and-messages.md) 시작 hello 여부 각 가상 컴퓨터를 나타내는 또는 stop 명령이 성공적으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="a4dfd-175">각 runbook에 대 한 hello 출력 toodetermine hello 결과에서 특정 문자열을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="a4dfd-176">hello 가능한 출력 문자열은 다음 표에 hello에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="a4dfd-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="a4dfd-177">Runbook</span></span> | <span data-ttu-id="a4dfd-178">조건</span><span class="sxs-lookup"><span data-stu-id="a4dfd-178">Condition</span></span> | <span data-ttu-id="a4dfd-179">Message</span><span class="sxs-lookup"><span data-stu-id="a4dfd-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a4dfd-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-180">Start-AzureVMs</span></span> |<span data-ttu-id="a4dfd-181">가상 컴퓨터 이미 실행 중</span><span class="sxs-lookup"><span data-stu-id="a4dfd-181">Virtual machine is already running</span></span> |<span data-ttu-id="a4dfd-182">MyVM 이미 실행 중</span><span class="sxs-lookup"><span data-stu-id="a4dfd-182">MyVM is already running</span></span> |
| <span data-ttu-id="a4dfd-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-183">Start-AzureVMs</span></span> |<span data-ttu-id="a4dfd-184">가상 컴퓨터에 대한 시작 요청이 성공적으로 제출됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="a4dfd-185">MyVM 시작됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-185">MyVM has been started</span></span> |
| <span data-ttu-id="a4dfd-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-186">Start-AzureVMs</span></span> |<span data-ttu-id="a4dfd-187">가상 컴퓨터에 대한 시작 요청 실패</span><span class="sxs-lookup"><span data-stu-id="a4dfd-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="a4dfd-188">MyVM toostart를 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="a4dfd-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-189">Stop-AzureVMs</span></span> |<span data-ttu-id="a4dfd-190">가상 컴퓨터가 이미 중지됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="a4dfd-191">MyVM 이미 중지됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="a4dfd-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-192">Stop-AzureVMs</span></span> |<span data-ttu-id="a4dfd-193">가상 컴퓨터에 대한 중지 요청이 성공적으로 제출됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="a4dfd-194">MyVM 중지됨</span><span class="sxs-lookup"><span data-stu-id="a4dfd-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="a4dfd-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a4dfd-195">Stop-AzureVMs</span></span> |<span data-ttu-id="a4dfd-196">가상 컴퓨터에 대한 중지 요청 실패</span><span class="sxs-lookup"><span data-stu-id="a4dfd-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="a4dfd-197">MyVM toostop를 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-197">MyVM failed toostop</span></span> |

<span data-ttu-id="a4dfd-198">예를 들어 runbook에서 코드 조각을 다음 hello 시도 toostart hello 서비스 이름으로 모든 가상 컴퓨터 *MyServiceName*합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="a4dfd-199">요청 실패 시작 hello 중에 오류 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="a4dfd-200">자세한 분석</span><span class="sxs-lookup"><span data-stu-id="a4dfd-200">Detailed breakdown</span></span>
<span data-ttu-id="a4dfd-201">다음은이 시나리오에서는 hello runbook의 상세한 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="a4dfd-202">이 정보를 사용 하면 tooeither hello runbook 또는 임원의 정당한 toolearn 작성 직접 자동화 시나리오에 대 한 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="a4dfd-203">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a4dfd-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="a4dfd-204">hello 워크플로가 시작 hello에 대 한 hello 값을 가져오는 [입력 매개 변수](#using-the-scenario)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="a4dfd-205">Hello 자산 이름을 입력 하지 않은 경우 기본 이름이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="a4dfd-206">출력</span><span class="sxs-lookup"><span data-stu-id="a4dfd-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="a4dfd-207">이 줄 hello runbook의 hello 출력 문자열 되도록 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="a4dfd-208">이것은 필요 하지 않지만 hello runbook으로 사용 된 경우에 대 한 가장 좋은 방법은 [자식 runbook](automation-child-runbooks.md) 부모 runbook hello 출력을 파악할 수 있도록 tooexpect를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="a4dfd-209">인증</span><span class="sxs-lookup"><span data-stu-id="a4dfd-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="a4dfd-210">다음 줄 hello 설정 hello [자격 증명](automation-credentials.md) 및 hello 나머지 hello runbook에 사용할 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="a4dfd-211">사용 하 여 먼저 **Get-automationpscredential** hello Azure 구독에에서 액세스할 수 있는 자격 증명 hello toostart 및 중지할 가상 컴퓨터를 포함 하는 tooget hello 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="a4dfd-212">**추가 AzureAccount** 다음이 자산 tooset hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="a4dfd-213">hello 출력 hello runbook 출력에 포함 되지 않도록 tooa 더미 변수가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="a4dfd-214">hello 변수 자산 ID를 검색 한 다음 hello 구독과 **Get-automationvariable** 및 사용 하 여 설정 하는 hello 구독 **Select-azuresubscription**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="a4dfd-215">VM 가져오기</span><span class="sxs-lookup"><span data-stu-id="a4dfd-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="a4dfd-216">**Get-azurevm** 사용 되는 tooretrieve hello runbook은 작동 하는 hello 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="a4dfd-217">Hello에는 값을 제공 하는 경우 **ServiceName** 입력 해당 서비스 이름 가진 변수를 다음 유일한 hello 가상 컴퓨터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="a4dfd-218">**ServiceName** 을 비워두면 모든 가상 컴퓨터가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="a4dfd-219">가상 컴퓨터 시작/중지 및 출력 보내기</span><span class="sxs-lookup"><span data-stu-id="a4dfd-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="a4dfd-220">다음 줄 hello 각 가상 컴퓨터 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="a4dfd-221">먼저 hello **PowerState** hello의 가상 컴퓨터는 선택 된 toosee 이미 있으면 실행 또는 hello runbook에 따른 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="a4dfd-222">Hello 대상 상태에 이미 있으면 hello runbook 끝나고 toooutput, 메시지가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="a4dfd-223">그렇지 않은 경우 다음 **Start-azurevm** 또는 **Stop-azurevm** hello 요청 저장된 tooa 변수의 hello 결과 함께 사용 되는 tooattempt toostart 또는 중지 hello 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="a4dfd-224">메시지가는 성공적으로 전송 hello 요청 toostart 또는 중지 여부를 지정 toooutput 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfd-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4dfd-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4dfd-225">Next steps</span></span>
* <span data-ttu-id="a4dfd-226">자식 runbook 작업에 대해 자세히 toolearn 참조 [Azure 자동화에서 자식 runbook](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="a4dfd-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="a4dfd-227">에 대해 더 알아봅니다 toolearn 문제를 해결 하는 동안 runbook 실행 및 로깅 toohelp 메시지가 출력, 참조 [Runbook 출력 및 Azure 자동화에서 메시지](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="a4dfd-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

