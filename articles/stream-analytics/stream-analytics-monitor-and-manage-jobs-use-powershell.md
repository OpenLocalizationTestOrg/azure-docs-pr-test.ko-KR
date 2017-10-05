---
title: "PowerShell을 사용하여 Stream Analytics 작업 모니터링 및 관리 | Microsoft Docs"
description: "Azure PowerShell 및 cmdlet을 사용하여 Stream Analytics 작업을 모니터링하고 관리하는 방법에 대해 알아봅니다."
keywords: "azure powershell, azure powershell cmdlet, powershell 명령, powershell 스크립팅"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: e3449ee90cc83c5e823e5948a2a2e7e633c454f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="8fbb6-104">Azure PowerShell cmdlet을 사용하여 Stream Analytics 작업 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="8fbb6-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="8fbb6-105">기본 Stream Analytics 작업을 실행하는 Azure PowerShell cmdlet 및 PowerShell 스크립팅을 사용하여 Stream Analytics 리소스를 모니터링 및 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="8fbb6-106">Stream Analytics에 Azure PowerShell cmdlet을 실행하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="8fbb6-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="8fbb6-107">구독에서 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="8fbb6-108">다음은 샘플 Azure PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="8fbb6-109">Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="8fbb6-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="8fbb6-111">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="8fbb6-112">프로그래밍 방식으로 만든 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="8fbb6-113">작업의 모니터 페이지로 이동하고 사용 버튼을 클릭하여 Azure 포털에서 수동으로 모니터링을 설정하거나 [Azure Stream Analytics - 프로그래밍 방식으로 Stream Analytics 작업 모니터링](stream-analytics-monitor-jobs.md)의 단계를 수행하여 이를 프로그래밍 방식으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="8fbb6-114">Stream Analytics용 Azure PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="8fbb6-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="8fbb6-115">다음 Azure PowerShell cmdlet은 Azure Stream Analytics 작업을 모니터링하고 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="8fbb6-116">Azure PowerShell에는 여러 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="8fbb6-117">**나열된 예제에서 첫 번째 명령은 Azure PowerShell 0.9.8에 적용되고, 두 번째 명령은 Azure PowerShell 1.0에 적용됩니다.**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="8fbb6-118">Azure PowerShell 1.0 명령에는 항상 "AzureRM"이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="8fbb6-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="8fbb6-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="8fbb6-120">Azure 구독 또는 지정한 리소스 그룹에 정의된 모든 Stream Analytics 작업을 나열하거나 리소스 그룹 내의 특정 작업에 대한 작업 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="8fbb6-121">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-121">**Example 1**</span></span>

<span data-ttu-id="8fbb6-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="8fbb6-123">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="8fbb6-124">이 PowerShell 명령은 Azure 구독의 모든 Stream Analytics 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="8fbb6-125">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-125">**Example 2**</span></span>

<span data-ttu-id="8fbb6-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="8fbb6-127">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="8fbb6-128">이 PowerShell 명령은 리소스 그룹 StreamAnalytics-Default-Central-US의 모든 Stream Analytics 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="8fbb6-129">**예 3**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-129">**Example 3**</span></span>

<span data-ttu-id="8fbb6-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="8fbb6-131">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="8fbb6-132">이 PowerShell 명령은 리소스 그룹 StreamAnalytics-Default-Central-US의 Stream Analytics 작업 StreamingJob에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="8fbb6-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="8fbb6-134">지정한 Stream Analytics 작업에 정의된 모든 입력을 나열하거나 특정 입력에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="8fbb6-135">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-135">**Example 1**</span></span>

<span data-ttu-id="8fbb6-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="8fbb6-137">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="8fbb6-138">이 PowerShell 명령은 StreamingJob 작업에 정의된 모든 입력에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="8fbb6-139">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-139">**Example 2**</span></span>

<span data-ttu-id="8fbb6-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="8fbb6-141">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="8fbb6-142">이 PowerShell 명령은 StreamingJob 작업에 정의된 EntryStream이라는 입력에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="8fbb6-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="8fbb6-144">지정한 Stream Analytics 작업에 정의된 모든 출력을 나열하거나 특정 출력에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="8fbb6-145">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-145">**Example 1**</span></span>

<span data-ttu-id="8fbb6-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="8fbb6-147">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="8fbb6-148">이 PowerShell 명령은 StreamingJob 작업에 정의된 모든 출력에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="8fbb6-149">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-149">**Example 2**</span></span>

<span data-ttu-id="8fbb6-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-151">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-152">이 PowerShell 명령은 StreamingJob 작업에 정의된 Output이라는 출력에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="8fbb6-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="8fbb6-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="8fbb6-154">지정한 지역의 스트리밍 단위 할당량에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="8fbb6-155">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-155">**Example 1**</span></span>

<span data-ttu-id="8fbb6-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="8fbb6-157">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="8fbb6-158">이 PowerShell 명령은 미국 중부 지역의 스트리밍 단위 할당량 및 사용에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="8fbb6-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="8fbb6-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="8fbb6-160">Stream Analytics 작업에 정의된 특정 변환에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="8fbb6-161">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-161">**Example 1**</span></span>

<span data-ttu-id="8fbb6-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="8fbb6-163">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="8fbb6-164">이 PowerShell 명령은 StreamingJob 작업에 정의된 StreamingJob이라는 변환에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="8fbb6-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="8fbb6-166">Stream Analytics 작업 내에서 새 입력을 만들거나 지정한 기존 입력을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="8fbb6-167">.json 파일 또는 명령줄에서 입력의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="8fbb6-168">둘 다 지정하는 경우 명령줄의 이름이 파일에 있는 이름과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="8fbb6-169">이미 존재하는 입력을 지정하고 -Force 매개 변수를 지정하지 않을 경우 cmdlet에서 기존 입력을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="8fbb6-170">–Force 매개 변수와 기존 입력 이름을 지정하면 확인 없이 입력이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="8fbb6-171">JSON 파일 구조 및 내용에 대한 자세한 내용은 [Stream Analytics 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]의 [입력 만들기(Azure 스트림 분석)][msdn-rest-api-create-stream-analytics-input]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="8fbb6-172">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-172">**Example 1**</span></span>

<span data-ttu-id="8fbb6-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="8fbb6-174">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="8fbb6-175">이 PowerShell 명령은 Input.json 파일에 새 입력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="8fbb6-176">입력 정의 파일에 지정된 이름의 기존 입력이 이미 정의되어 있으면 cmdlet에서 해당 입력을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="8fbb6-177">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-177">**Example 2**</span></span>

<span data-ttu-id="8fbb6-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="8fbb6-179">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="8fbb6-180">이 PowerShell 명령은 EntryStream이라는 작업에 새 입력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="8fbb6-181">이 이름의 기존 입력이 이미 정의되어 있으면 cmdlet에서 해당 입력을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="8fbb6-182">**예 3**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-182">**Example 3**</span></span>

<span data-ttu-id="8fbb6-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="8fbb6-184">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="8fbb6-185">이 PowerShell 명령은 EntryStream이라는 기존 입력 소스의 정의를 파일에 있는 정의로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="8fbb6-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="8fbb6-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="8fbb6-187">Microsoft Azure에 새 Stream Analytics 작업을 만들거나 지정한 기존 작업의 정의를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="8fbb6-188">.json 파일 또는 명령줄에서 작업의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="8fbb6-189">둘 다 지정하는 경우 명령줄의 이름이 파일에 있는 이름과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="8fbb6-190">이미 존재하는 작업 이름을 지정하고 -Force 매개 변수를 지정하지 않을 경우 cmdlet에서 기존 작업을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="8fbb6-191">–Force 매개 변수와 기존 작업 이름을 지정하면 확인 없이 작업 정의가 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="8fbb6-192">JSON 파일 구조 및 내용에 대한 자세한 내용은 [Stream Analytics 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]의 [스트림 분석 작업 만들기][msdn-rest-api-create-stream-analytics-job] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="8fbb6-193">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-193">**Example 1**</span></span>

<span data-ttu-id="8fbb6-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="8fbb6-195">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="8fbb6-196">이 PowerShell 명령은 JobDefinition.json의 정의에서 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="8fbb6-197">작업 정의 파일에 지정된 이름의 기존 작업이 이미 정의되어 있으면 cmdlet에서 해당 작업을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="8fbb6-198">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-198">**Example 2**</span></span>

<span data-ttu-id="8fbb6-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="8fbb6-200">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="8fbb6-201">이 PowerShell 명령은 StreamingJob에 대한 작업 정의를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="8fbb6-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="8fbb6-203">Stream Analytics 작업 내에서 새 출력을 만들거나 기존 출력을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="8fbb6-204">.json 파일 또는 명령줄에서 출력의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="8fbb6-205">둘 다 지정하는 경우 명령줄의 이름이 파일에 있는 이름과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="8fbb6-206">이미 존재하는 출력을 지정하고 -Force 매개 변수를 지정하지 않을 경우 cmdlet에서 기존 출력을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="8fbb6-207">–Force 매개 변수와 기존 출력 이름을 지정하면 확인 없이 출력이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="8fbb6-208">JSON 파일 구조 및 내용에 대한 자세한 내용은 [Stream Analytics 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]의 [출력 만들기(Azure 스트림 분석)][msdn-rest-api-create-stream-analytics-output]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="8fbb6-209">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-209">**Example 1**</span></span>

<span data-ttu-id="8fbb6-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="8fbb6-211">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="8fbb6-212">이 PowerShell 명령은 StreamingJob 작업에 "output"이라는 새 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="8fbb6-213">이 이름의 기존 출력이 이미 정의되어 있으면 cmdlet에서 해당 출력을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="8fbb6-214">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-214">**Example 2**</span></span>

<span data-ttu-id="8fbb6-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="8fbb6-216">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="8fbb6-217">이 PowerShell 명령은 StreamingJob 작업에서 "output"의 정의를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="8fbb6-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="8fbb6-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="8fbb6-219">Stream Analytics 작업 내에서 새 변환을 만들거나 기존 변환을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="8fbb6-220">.json 파일 또는 명령줄에서 변환의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="8fbb6-221">둘 다 지정하는 경우 명령줄의 이름이 파일에 있는 이름과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="8fbb6-222">이미 존재하는 변환을 지정하고 -Force 매개 변수를 지정하지 않을 경우 cmdlet에서 기존 변환을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="8fbb6-223">–Force 매개 변수와 기존 변환 이름을 지정하면 확인 없이 변환이 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="8fbb6-224">JSON 파일 구조 및 내용에 대한 자세한 내용은 [Stream Analytics 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]의 [변환 만들기(Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="8fbb6-225">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-225">**Example 1**</span></span>

<span data-ttu-id="8fbb6-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="8fbb6-227">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="8fbb6-228">이 PowerShell 명령은 StreamingJob 작업에 StreamingJobTransform이라는 새 변환을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="8fbb6-229">이 이름의 기존 변환이 이미 정의되어 있으면 cmdlet에서 해당 변환을 바꿀지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="8fbb6-230">**예 2**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-230">**Example 2**</span></span>

<span data-ttu-id="8fbb6-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="8fbb6-232">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="8fbb6-233">이 PowerShell 명령은 StreamingJob 작업에서 StreamingJobTransform의 정의를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="8fbb6-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="8fbb6-235">Microsoft Azure의 Stream Analytics 작업에서 특정 입력을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="8fbb6-236">–Force 매개 변수를 지정하면 확인 없이 입력이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="8fbb6-237">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-237">**Example 1**</span></span>

<span data-ttu-id="8fbb6-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="8fbb6-239">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="8fbb6-240">이 PowerShell 명령은 StreamingJob 작업에서 EventStream 입력을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="8fbb6-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="8fbb6-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="8fbb6-242">Microsoft Azure에서 특정 Stream Analytics 작업을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="8fbb6-243">–Force 매개 변수를 지정하면 확인 없이 작업이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="8fbb6-244">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-244">**Example 1**</span></span>

<span data-ttu-id="8fbb6-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="8fbb6-246">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="8fbb6-247">이 PowerShell 명령은 StreamingJob 작업을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="8fbb6-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="8fbb6-249">Microsoft Azure의 Stream Analytics 작업에서 특정 출력을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="8fbb6-250">–Force 매개 변수를 지정하면 확인 없이 출력이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="8fbb6-251">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-251">**Example 1**</span></span>

<span data-ttu-id="8fbb6-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-253">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-254">이 PowerShell 명령은 StreamingJob 작업에서 Output 출력을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="8fbb6-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="8fbb6-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="8fbb6-256">Microsoft Azure에 Stream Analytics 작업을 비동기적으로 배포하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="8fbb6-257">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-257">**Example 1**</span></span>

<span data-ttu-id="8fbb6-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="8fbb6-259">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="8fbb6-260">이 PowerShell 명령은 사용자 지정 출력 시작 시간이 2012년 12월 12일 12:12:12 UTC로 설정되어 StreamingJob 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="8fbb6-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="8fbb6-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="8fbb6-262">Microsoft Azure에서 실행 중인 Stream Analytics 작업을 비동기적으로 중지하고 사용하던 리소스를 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="8fbb6-263">작업 정의와 메타데이터는 작업을 편집하고 다시 시작할 수 있도록 Azure 포털과 관리 API를 통해 구독 내에서 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="8fbb6-264">중지됨 상태의 작업에 대해서는 요금이 부과되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="8fbb6-265">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-265">**Example 1**</span></span>

<span data-ttu-id="8fbb6-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="8fbb6-267">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="8fbb6-268">이 PowerShell 명령은 StreamingJob 작업을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="8fbb6-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="8fbb6-270">Stream Analytics이 지정한 입력에 연결할 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="8fbb6-271">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-271">**Example 1**</span></span>

<span data-ttu-id="8fbb6-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="8fbb6-273">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="8fbb6-274">이 PowerShell 명령은 StreamingJob에서 EntryStream 입력의 연결 상태를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="8fbb6-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="8fbb6-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="8fbb6-276">Stream Analytics이 지정한 출력에 연결할 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="8fbb6-277">**예 1**</span><span class="sxs-lookup"><span data-stu-id="8fbb6-277">**Example 1**</span></span>

<span data-ttu-id="8fbb6-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="8fbb6-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-279">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="8fbb6-280">이 PowerShell 명령은 StreamingJob에서 Output 출력의 연결 상태를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="8fbb6-281">지원 받기</span><span class="sxs-lookup"><span data-stu-id="8fbb6-281">Get support</span></span>
<span data-ttu-id="8fbb6-282">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8fbb6-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8fbb6-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8fbb6-283">Next steps</span></span>
* [<span data-ttu-id="8fbb6-284">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="8fbb6-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8fbb6-285">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="8fbb6-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8fbb6-286">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="8fbb6-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8fbb6-287">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="8fbb6-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8fbb6-288">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="8fbb6-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

