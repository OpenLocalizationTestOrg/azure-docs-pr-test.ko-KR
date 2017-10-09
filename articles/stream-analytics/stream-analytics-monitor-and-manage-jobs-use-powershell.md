---
title: "aaaMonitor powershell 스트림 분석 작업을 관리 하 고 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure PowerShell 및 cmdlet toomonitor 및 스트림 분석 작업을 관리 합니다."
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
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="722a2-104">Azure PowerShell cmdlet을 사용하여 Stream Analytics 작업 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="722a2-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="722a2-105">자세한 내용은 어떻게 toomonitor 및 기본 스트림 분석 작업을 실행 하는 Azure PowerShell cmdlet 및 powershell 스크립트를 사용 하 여 스트림 분석 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="722a2-106">Stream Analytics에 Azure PowerShell cmdlet을 실행하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="722a2-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="722a2-107">구독에서 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="722a2-108">hello 다음은 샘플 Azure PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="722a2-109">Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="722a2-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="722a2-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="722a2-111">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="722a2-112">프로그래밍 방식으로 만든 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="722a2-113">Hello toohello 작업 모니터 페이지를 탐색 하 여 Azure 포털에서에서 모니터링을 수동으로 설정할 수 있습니다 및 있습니다 또는 hello 사용 단추를 클릭 하에 있는 hello 단계에 따라 프로그래밍 방식으로이 수행할 수 있는 [Azure 스트림 분석-모니터 스트림 분석을 프로그래밍 방식으로 작업](stream-analytics-monitor-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="722a2-114">Stream Analytics용 Azure PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="722a2-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="722a2-115">hello 다음 Azure PowerShell cmdlet 사용된 toomonitor 수 하 고 Azure 스트림 분석 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="722a2-116">Azure PowerShell에는 여러 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="722a2-117">**Azure powershell 0.9.8은 나열 된 hello 첫 번째 명령은 hello 예제에서 Azure PowerShell 1.0에 대 한 hello 두 번째 명령이입니다.**</span><span class="sxs-lookup"><span data-stu-id="722a2-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="722a2-118">Azure PowerShell 1.0 hello 명령을 항상 "AzureRM" hello 명령에서입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="722a2-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="722a2-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="722a2-120">Hello Azure 구독 또는 지정 된 리소스 그룹에 정의 된 모든 스트림 분석 작업 나열 하거나 리소스 그룹 내에서 특정 작업에 대 한 작업 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="722a2-121">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-121">**Example 1**</span></span>

<span data-ttu-id="722a2-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="722a2-123">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="722a2-124">이 PowerShell 명령을 hello Azure 구독에서에서 모든 hello 스트림 분석 작업에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="722a2-125">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-125">**Example 2**</span></span>

<span data-ttu-id="722a2-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="722a2-127">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="722a2-128">이 PowerShell 명령은 기본 중앙 미국 StreamAnalytics hello 리소스 그룹에서 모든 hello 스트림 분석 작업에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="722a2-129">**예 3**</span><span class="sxs-lookup"><span data-stu-id="722a2-129">**Example 3**</span></span>

<span data-ttu-id="722a2-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="722a2-131">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="722a2-132">이 PowerShell 명령은 hello 리소스 그룹 StreamAnalytics 기본-중앙 미국 StreamingJob hello 스트림 분석 작업에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="722a2-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="722a2-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="722a2-134">지정된 된 스트림 분석 작업에 정의 된 hello 입력의 모든 나열 하거나 특정 입력에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="722a2-135">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-135">**Example 1**</span></span>

<span data-ttu-id="722a2-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="722a2-137">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="722a2-138">이 PowerShell 명령을 StreamingJob hello 작업에 정의 된 모든 hello 입력에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="722a2-139">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-139">**Example 2**</span></span>

<span data-ttu-id="722a2-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="722a2-141">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="722a2-142">이 PowerShell 명령을 EntryStream StreamingJob hello 작업에 정의 된 명명 된 hello 입력에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="722a2-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="722a2-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="722a2-144">모든 지정된 된 스트림 분석 작업에 정의 된 hello 출력 나열 하거나 특정 출력에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="722a2-145">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-145">**Example 1**</span></span>

<span data-ttu-id="722a2-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="722a2-147">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="722a2-148">이 PowerShell 명령을 StreamingJob hello 작업에 정의 된 hello 출력에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="722a2-149">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-149">**Example 2**</span></span>

<span data-ttu-id="722a2-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="722a2-151">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="722a2-152">이 PowerShell 명령은 출력 StreamingJob hello 작업에 정의 된 명명 된 hello 출력에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="722a2-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="722a2-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="722a2-154">스트리밍 단위는 지정한 지역에서의 hello 할당량에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="722a2-155">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-155">**Example 1**</span></span>

<span data-ttu-id="722a2-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="722a2-157">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="722a2-158">이 PowerShell 명령을 hello 중앙 미국 지역에 hello 할당량 및 스트리밍 단위 사용에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="722a2-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="722a2-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="722a2-160">Stream Analytics 작업에 정의된 특정 변환에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="722a2-161">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-161">**Example 1**</span></span>

<span data-ttu-id="722a2-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="722a2-163">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="722a2-164">이 PowerShell 명령을 StreamingJob StreamingJob hello 작업에서 호출 하는 hello 변환에 대 한 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="722a2-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="722a2-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="722a2-166">Stream Analytics 작업 내에서 새 입력을 만들거나 지정한 기존 입력을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="722a2-167">hello hello 입력의 이름을 지정할 수 있습니다 hello 명령줄 또는 hello.json 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="722a2-168">모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="722a2-169">이미 존재 하는 입력 지정을 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 입력 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="722a2-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="722a2-170">Hello – Force 매개 변수 및 이름을 입력 하십시오. 기존, 확인 하지 않고 hello 입력 바뀝니다 지정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="722a2-171">Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [입력 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-input] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="722a2-172">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-172">**Example 1**</span></span>

<span data-ttu-id="722a2-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="722a2-174">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="722a2-175">이 PowerShell 명령은 Input.json hello 파일에서 새 입력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="722a2-176">경우 hello 입력된 정의 파일에 지정 된 hello 이름 가진 기존 입력 이미 정의 되어 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="722a2-177">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-177">**Example 2**</span></span>

<span data-ttu-id="722a2-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="722a2-179">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="722a2-180">이 PowerShell 명령을 EntryStream hello 작업에는 새 입력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="722a2-181">경우이 이름 가진 기존 입력 이미 정의 되어 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="722a2-182">**예 3**</span><span class="sxs-lookup"><span data-stu-id="722a2-182">**Example 3**</span></span>

<span data-ttu-id="722a2-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="722a2-184">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="722a2-185">이 PowerShell 명령은 hello 기존 입력된 소스 EntryStream hello 파일에서 정의 hello 사용 하 여 호출의 hello 정을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="722a2-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="722a2-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="722a2-187">Microsoft Azure에서 새 스트림 분석 작업을 만들거나 기존 지정 된 작업의 hello 정의 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="722a2-188">hello 작업의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="722a2-189">모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="722a2-190">이미 존재 하는 작업 이름을 지정 하 고 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 작업 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="722a2-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="722a2-191">기존 작업 이름을 지정 하 고 hello – Force 매개 변수를 지정 하는 경우 hello 작업 정의 확인 하지 않고 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="722a2-192">Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [스트림 분석 작업 만들기] [ msdn-rest-api-create-stream-analytics-job] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="722a2-193">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-193">**Example 1**</span></span>

<span data-ttu-id="722a2-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="722a2-195">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="722a2-196">이 PowerShell 명령을 JobDefinition.json에 hello 정의에서 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="722a2-197">Hello 작업 정의 파일에 지정 된 hello 이름 사용 하는 기존 작업은 이미 정의 하는 경우 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="722a2-198">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-198">**Example 2**</span></span>

<span data-ttu-id="722a2-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="722a2-200">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="722a2-201">이 PowerShell 명령은 StreamingJob에 대 한 hello 작업 정을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="722a2-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="722a2-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="722a2-203">Stream Analytics 작업 내에서 새 출력을 만들거나 기존 출력을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="722a2-204">hello 출력의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="722a2-205">모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="722a2-206">이미 존재 하는 출력을 지정 하 고 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace hello 기존 출력 여부.</span><span class="sxs-lookup"><span data-stu-id="722a2-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="722a2-207">기존 출력 이름, 확인 하지 않고 hello 출력 바뀝니다 지정 하 고 hello – Force 매개 변수를 지정 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="722a2-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="722a2-208">Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [출력 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-output] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="722a2-209">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-209">**Example 1**</span></span>

<span data-ttu-id="722a2-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="722a2-211">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="722a2-212">이 PowerShell 명령을 StreamingJob hello 작업에서 "output" 라는 새 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="722a2-213">이 이름 가진 기존 출력은 이미 정의 하는 경우 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="722a2-214">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-214">**Example 2**</span></span>

<span data-ttu-id="722a2-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="722a2-216">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="722a2-217">이 PowerShell 명령은 "출력" StreamingJob hello 작업에 대 한 hello 정을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="722a2-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="722a2-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="722a2-219">스트림 분석 작업 내에서 새 변환을 만들거나 기존 변환 hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="722a2-220">hello 변환의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="722a2-221">모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="722a2-222">이미 존재 하는 변환 지정을 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 변환 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="722a2-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="722a2-223">기존 변환 이름을 지정 하 고 hello – Force 매개 변수를 지정 하는 경우 hello 변환 확인 하지 않고 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="722a2-224">Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [변환 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-transformation] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="722a2-225">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-225">**Example 1**</span></span>

<span data-ttu-id="722a2-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="722a2-227">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="722a2-228">이 PowerShell 명령은 StreamingJobTransform hello 작업 StreamingJob에에서 이라는 새 변환을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="722a2-229">경우 기존 변환이 이미 정의 되어이 이름의 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="722a2-230">**예 2**</span><span class="sxs-lookup"><span data-stu-id="722a2-230">**Example 2**</span></span>

<span data-ttu-id="722a2-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="722a2-232">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="722a2-233">이 PowerShell 명령은 hello 작업 StreamingJob에서에서 StreamingJobTransform의 hello 정을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="722a2-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="722a2-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="722a2-235">Microsoft Azure의 Stream Analytics 작업에서 특정 입력을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="722a2-236">지정 하는 경우 hello – Force 매개 변수를 입력 하는 hello 없이 삭제 됩니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="722a2-237">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-237">**Example 1**</span></span>

<span data-ttu-id="722a2-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="722a2-239">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="722a2-240">제거 hello 입력된 EventStream StreamingJob hello 작업에서이 PowerShell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="722a2-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="722a2-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="722a2-242">Microsoft Azure에서 특정 Stream Analytics 작업을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="722a2-243">지정 하는 경우 hello – Force 매개 변수 hello 작업 됩니다 확인 과정 없이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="722a2-244">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-244">**Example 1**</span></span>

<span data-ttu-id="722a2-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="722a2-246">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="722a2-247">이 PowerShell 명령을 hello 작업 StreamingJob을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="722a2-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="722a2-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="722a2-249">Microsoft Azure의 Stream Analytics 작업에서 특정 출력을 비동기적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="722a2-250">지정 하는 경우 hello – Force 매개 변수 hello 출력 됩니다 확인 과정 없이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="722a2-251">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-251">**Example 1**</span></span>

<span data-ttu-id="722a2-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="722a2-253">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="722a2-254">이 PowerShell 명령 제거 hello StreamingJob hello 작업에서 출력을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="722a2-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="722a2-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="722a2-256">Microsoft Azure에 Stream Analytics 작업을 비동기적으로 배포하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="722a2-257">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-257">**Example 1**</span></span>

<span data-ttu-id="722a2-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="722a2-259">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="722a2-260">이 PowerShell 명령을 시작 작업을 사용자 지정 출력 시작 시간이 StreamingJob 설정 tooDecember 12, 2012, 12시 12분: 12 hello UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="722a2-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="722a2-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="722a2-262">Microsoft Azure에서 실행 중인 Stream Analytics 작업을 비동기적으로 중지하고 사용하던 리소스를 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="722a2-263">hello 작업 정 및 메타 데이터는 계속 사용할 수 hello Azure 포털 및 관리 Api 모두를 통해 구독 내에서 hello 작업 수 편집 하 고 다시 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="722a2-264">Hello 중지 상태에 있는 작업에 대 한 청구 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="722a2-265">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-265">**Example 1**</span></span>

<span data-ttu-id="722a2-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="722a2-267">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="722a2-268">이 PowerShell 명령을 StreamingJob hello 작업을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="722a2-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="722a2-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="722a2-270">스트림 분석 tooconnect tooa의 테스트 hello 기능은 입력을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="722a2-271">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-271">**Example 1**</span></span>

<span data-ttu-id="722a2-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="722a2-273">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="722a2-274">이 PowerShell 명령 테스트 hello 연결 상태는 hello EntryStream StreamingJob에를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="722a2-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="722a2-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="722a2-276">스트림 분석 tooconnect tooa의 테스트 hello 기능은 출력을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="722a2-277">**예 1**</span><span class="sxs-lookup"><span data-stu-id="722a2-277">**Example 1**</span></span>

<span data-ttu-id="722a2-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="722a2-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="722a2-279">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="722a2-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="722a2-280">이 PowerShell 명령 테스트 hello 연결 상태는 hello StreamingJob에서 출력을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="722a2-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="722a2-281">지원 받기</span><span class="sxs-lookup"><span data-stu-id="722a2-281">Get support</span></span>
<span data-ttu-id="722a2-282">추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="722a2-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="722a2-283">다음 단계</span><span class="sxs-lookup"><span data-stu-id="722a2-283">Next steps</span></span>
* [<span data-ttu-id="722a2-284">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="722a2-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="722a2-285">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="722a2-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="722a2-286">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="722a2-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="722a2-287">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="722a2-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="722a2-288">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="722a2-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

