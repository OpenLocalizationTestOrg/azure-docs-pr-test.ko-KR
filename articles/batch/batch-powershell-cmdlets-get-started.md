---
title: "Azure Batch용 PowerShell 시작 | Microsoft Docs"
description: "Batch 리소스를 관리하는 데 사용할 수 있는 Azure PowerShell cmdlet에 대한 간략한 소개입니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="e6416-103">PowerShell cmdlet을 사용한 Batch 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="e6416-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="e6416-104">Azure 배치 PowerShell cmdlet을 사용하여 배치 API, Azure 포털, Azure CLI(명령줄 인터페이스)에서 실행한 많은 동일한 작업을 수행하고 스크립트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="e6416-105">배치 계정을 관리하고 풀, 작업, 태스크 등의 배치 리소스 작업에 사용할 수 있는 cmdlet에 대해 간략히 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="e6416-106">배치 cmdlet의 전체 목록과 상세 cmdlet 구문은 [Azure 배치 cmdlet 참조](/powershell/module/azurerm.batch/#batch)에서 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e6416-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="e6416-107">이 문서는 Azure PowerShell 버전 3.0.0의 cmdlet를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="e6416-108">서비스 업데이트 및 향상을 최대한 활용하기 위해서 Azure PowerShell을 자주 업데이트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6416-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e6416-109">Prerequisites</span></span>
<span data-ttu-id="e6416-110">배치 리소스를 관리하도록 Azure PowerShell을 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="e6416-111">Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e6416-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="e6416-112">**Login-AzureRmAccount** cmdlet을 실행하여 구독에 연결(Azure Batch cmdlet은 Azure Resource Manager 모듈에 탑재됨):</span><span class="sxs-lookup"><span data-stu-id="e6416-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="e6416-113">**배치 공급자 네임 스페이스를 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="e6416-114">이 작업은 **구독당 한 번**만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="e6416-115">배치 계정 및 키 관리</span><span class="sxs-lookup"><span data-stu-id="e6416-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="e6416-116">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e6416-116">Create a Batch account</span></span>
<span data-ttu-id="e6416-117">**New-AzureRmBatchAccount**는 지정된 리소스 그룹에서 배치 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="e6416-118">아직 리소스 그룹이 없는 경우 [새 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet을 실행하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="e6416-119">**위치** 매개 변수에서 "미국 중부"와 같이 Azure 지역 중 하나를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="e6416-120">예:</span><span class="sxs-lookup"><span data-stu-id="e6416-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="e6416-121">그런 다음, 리소스 그룹에 배치 계정을 만들어, <*account_name*>의 계정 이름과 리소스 그룹의 위치와 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="e6416-122">배치 계정을 만드는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="e6416-123">예:</span><span class="sxs-lookup"><span data-stu-id="e6416-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="e6416-124">배치 계정 이름은 리소스 그룹에 대해 Azure 지역에 고유해야 하며, 3자에서 24자 사이의 문자를 포함하고, 소문자와 숫자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="e6416-125">계정 액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6416-125">Get account access keys</span></span>
<span data-ttu-id="e6416-126">**Get-AzureRmBatchAccountKey** 는 Azure 배치 계정과 연결된 액세스 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="e6416-127">예를 들어, 사용자가 만든 계정의 기본 및 보조 키를 가져오려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="e6416-128">새 액세스 키 생성</span><span class="sxs-lookup"><span data-stu-id="e6416-128">Generate a new access key</span></span>
<span data-ttu-id="e6416-129">**New-AzureRmBatchAccountKey** 는 Azure 배치 계정에 대해 기본 또는 보조 계정 키를 새로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="e6416-130">예를 들어, 배치 계정의 새 기본 키를 생성하려면 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="e6416-131">새 보조 키를 생성하려면 **KeyType** 매개 변수에 "Secondary"를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="e6416-132">기본 및 보조 키를 개별적으로 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="e6416-133">배치 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="e6416-133">Delete a Batch account</span></span>
<span data-ttu-id="e6416-134">**Remove-AzureRmBatchAccount** 는 배치 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="e6416-135">예:</span><span class="sxs-lookup"><span data-stu-id="e6416-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="e6416-136">메시지가 나타나면 계정을 제거할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="e6416-137">계정을 제거하는 데는 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="e6416-138">BatchAccountContext 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="e6416-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="e6416-139">배치 풀, 작업, 태스크, 기타 리소스를 만들고 관리할 때 배치 PowerShell cmdlet을 사용하여 인증하려면, 우선 계정 이름과 키를 저장할 BatchAccountContext 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="e6416-140">BatchAccountContext 개체를 **BatchContext** 매개 변수를 사용하는 cmdlet에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="e6416-141">기본적으로 계정의 기본 키는 인증에 사용되지만 BatchAccountContext 개체의 **KeyInUse** 속성을 변경하면 사용할 키를 명시적으로 선택할 수 있습니다. `$context.KeyInUse = "Secondary"`</span><span class="sxs-lookup"><span data-stu-id="e6416-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="e6416-142">배치 리소스 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="e6416-142">Create and modify Batch resources</span></span>
<span data-ttu-id="e6416-143">**New-AzureBatchPool**, **New-AzureBatchJob** 및 **New-AzureBatchTask** 등의 cmdlet을 사용하여 배치 계정 아래 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="e6416-144">기존 리소스 속성을 업데이트하는 해당 **Get-** 및 **Set-** cmdlet과, 배치 계정에서 리소스를 제거하는 **Remove-** cmdlet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="e6416-145">이러한 많은 cmdlet을 사용하는 경우 BatchContext 개체를 전달 하는 것 외에도, 다음 예제와 같이 상세한 리소스 설정을 포함하는 개체를 만들거나 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="e6416-146">추가 예제를 보려면 각 cmdlet에 대한 자세한 도움말을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6416-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="e6416-147">배치 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="e6416-147">Create a Batch pool</span></span>
<span data-ttu-id="e6416-148">Batch 풀을 만들거나 업데이트할 때 계산 노드의 운영 체제에 대해 클라우드 서비스 구성 또는 가상 컴퓨터 구성을 선택합니다( [배치 기능 개요](batch-api-basics.md#pool) 참조).</span><span class="sxs-lookup"><span data-stu-id="e6416-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="e6416-149">클라우드 서비스 구성을 지정하면 계산 노드가 [Azure 게스트 OS 릴리스](../cloud-services/cloud-services-guestos-update-matrix.md#releases) 중 하나로 이미지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="e6416-150">가상 컴퓨터 구성을 지정하는 경우 [Azure Virtual Machines Marketplace][vm_marketplace]에 나열된 지원되는 Linux 또는 Windows VM 이미지 중 하나를 지정하거나 미리 준비한 사용자 지정 이미지를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="e6416-151">**New-AzureBatchPool**을 실행하는 경우, PSCloudServiceConfiguration 또는 PSVirtualMachineConfiguration 개체의 운영 체제 설정을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="e6416-152">예를 들어, 다음 cmdlet는 제품군 3(Windows Server 2012)의 최신 운영 체제 버전을 통해 이미지를 만든 클라우드 서비스 구성에서 소규모 계산 노드로 새 배치 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="e6416-153">여기서 **CloudServiceConfiguration** 매개 변수는 *$configuration* 변수를 PSCloudServiceConfiguration 개체로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="e6416-154">**BatchContext** 매개 변수는 이전에 정의한 *$context* 변수를 BatchAccountContext 개체로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="e6416-155">새 풀의 계산 노드 대상 수는 자동 크기 조정 수식에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="e6416-156">이 경우 공식은 단순히 **$TargetDedicated=4**이며 풀의 계산 노드 수는 최대 4개입니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="e6416-157">풀, 작업, 태스크 및 기타 상세 정보 쿼리</span><span class="sxs-lookup"><span data-stu-id="e6416-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="e6416-158">**Get-AzureBatchPool**, **Get-AzureBatchJob** 및 **Get-AzureBatchTask** 등의 cmdlet을 사용하여 배치 계정 아래에 만든 엔터티를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="e6416-159">데이터에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="e6416-159">Query for data</span></span>
<span data-ttu-id="e6416-160">예제와 같이 **Get AzureBatchPools**을 사용하여 풀을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="e6416-161">이 작업은 기본적으로 사용자 계정 아래의 모든 풀을 쿼리합니다. 이때 *$context*에는 이미 BatchAccountContext 개체가 저장되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="e6416-162">OData 필터 사용</span><span class="sxs-lookup"><span data-stu-id="e6416-162">Use an OData filter</span></span>
<span data-ttu-id="e6416-163">**Filter** 매개 변수를 사용하여 OData 필터를 제공하면 사용자와 관계가 있는 개체만 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="e6416-164">예를 들어, "myPool"로 시작하는 ID를 갖는 모든 풀을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="e6416-165">이 방법은 로컬 파이프라인에서 "Where-Object"를 사용하는 것만큼 유연하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="e6416-166">그러나 쿼리가 배치 서비스에 직접 전송되므로 서버에서 모든 필터링이 수행되어 인터넷 대역폭이 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="e6416-167">ID 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="e6416-167">Use the Id parameter</span></span>
<span data-ttu-id="e6416-168">OData 필터의 대안은 **ID** 매개 변수를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="e6416-169">ID가 "myPool"인 특정 풀을 쿼리하려면</span><span class="sxs-lookup"><span data-stu-id="e6416-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="e6416-170">**ID** 매개 변수는 전체 ID 검색만 지원하며 와일드카드 또는 OData 스타일 필터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="e6416-171">MaxCount 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="e6416-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="e6416-172">기본적으로 각 cmdlet은 최대 1000개의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="e6416-173">이 제한에 도달하면 더 적은 수의 개체를 반환하도록 필터를 조정하거나 **MaxCount** 매개 변수를 사용하여 최대값을 명시적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="e6416-174">예:</span><span class="sxs-lookup"><span data-stu-id="e6416-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="e6416-175">상한값을 제거하려면 **MaxCount** 를 0 이하로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="e6416-176">PowerShell 파이프라인 사용</span><span class="sxs-lookup"><span data-stu-id="e6416-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="e6416-177">배치 cmdlet은 PowerShell 파이프라인을 활용하여 cmdlet 간에 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="e6416-178">이 방식은 매개 변수를 지정하는 것과 같은 효과가 있지만 보다 쉽게 여러 엔터티로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="e6416-179">예를 들어, 다음과 같이 사용자 계정 아래의 모든 작업을 찾아서 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="e6416-180">풀의 모든 계산 노드 다시 시작(다시 부팅):</span><span class="sxs-lookup"><span data-stu-id="e6416-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="e6416-181">응용 프로그램 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="e6416-181">Application package management</span></span>
<span data-ttu-id="e6416-182">응용 프로그램 패키지는 풀에서 계산 노드에 응용 프로그램을 배포하는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="e6416-183">배치 PowerShell cmdlet으로 배치 계정에 응용 프로그램 패키지를 업로드하여 관리하고 노드를 계산하는 패키지 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="e6416-184">**만듭니다** .</span><span class="sxs-lookup"><span data-stu-id="e6416-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="e6416-185">**추가합니다** .</span><span class="sxs-lookup"><span data-stu-id="e6416-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="e6416-186">응용 프로그램의 **기본 버전** 설정:</span><span class="sxs-lookup"><span data-stu-id="e6416-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="e6416-187">응용 프로그램의 패키지 **열거**</span><span class="sxs-lookup"><span data-stu-id="e6416-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="e6416-188">응용 프로그램 패키지 **삭제**</span><span class="sxs-lookup"><span data-stu-id="e6416-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="e6416-189">응용 프로그램 **삭제**</span><span class="sxs-lookup"><span data-stu-id="e6416-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="e6416-190">응용 프로그램을 삭제하기 전에 모든 응용 프로그램의 패키지 버전을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="e6416-191">현재 응용 프로그램 패키지를 보유하는 응용 프로그램을 삭제하려고 하면 '충돌' 오류 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="e6416-192">응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="e6416-192">Deploy an application package</span></span>
<span data-ttu-id="e6416-193">새 풀을 만들 때 배포에 하나 이상의 응용 프로그램 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="e6416-194">풀을 만들 때 패키지를 지정하는 경우 노드가 풀에 조인하면 각 노드에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="e6416-195">패키지는 노드를 다시 부팅하거나 이미지로 다시 설치하는 경우에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="e6416-196">풀에 참가하면서 풀의 노드에 응용 프로그램 패키지를 배포하도록 풀을 만들 때 `-ApplicationPackageReference` 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="e6416-197">먼저 **PSApplicationPackageReference** 개체를 만들고 이 개체를 풀의 계산 노드에 배포하려는 응용 프로그램 ID 및 패키지 버전으로 구성:</span><span class="sxs-lookup"><span data-stu-id="e6416-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="e6416-198">이제 풀을 만들고 패키지 참조 개체를 `ApplicationPackageReferences` 옵션에 대한 인수로 지정:</span><span class="sxs-lookup"><span data-stu-id="e6416-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="e6416-199">[Batch 응용 프로그램 패키지를 사용하여 계산 노드에 응용 프로그램 배포](batch-application-packages.md)에서 응용 프로그램 패키지에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6416-200">응용 프로그램 패키지를 사용하려면 [Azure Storage 계정](#linked-storage-account-autostorage) 을 배치 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="e6416-201">풀의 응용 프로그램 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="e6416-201">Update a pool's application packages</span></span>
<span data-ttu-id="e6416-202">기존 풀에 할당된 응용 프로그램을 업데이트하려면 먼저 원하는 속성(응용 프로그램 ID 및 패키지 버전)의 PSApplicationPackageReference 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="e6416-203">다음으로, 배치에서 풀을 가져오고 기존 패키지를 모두 지우고 우리의 새 패키지 참조를 추가하고 새 풀 설정을 사용하여 배치 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="e6416-204">이제 배치 서비스에서 풀의 속성을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="e6416-205">실제로 풀의 계산 노드에 새로운 응용 프로그램 패키지를 배포하려면, 해당 노드를 다시 시작하거나 이미지로 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="e6416-206">이 명령을 사용하여 풀의 모든 노드를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="e6416-207">여러 응용 프로그램 패키지를 풀의 계산 노드에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="e6416-208">현재 배포된 패키지를 교체하는 대신 응용 프로그램 패키지를 *추가*하고자 하는 경우 위의 `$pool.ApplicationPackageReferences.Clear()` 줄을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="e6416-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6416-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6416-209">Next steps</span></span>
* <span data-ttu-id="e6416-210">자세한 cmdlet 구문 및 예제는 [Azure 배치 cmdlet 참조](/powershell/module/azurerm.batch/#batch)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6416-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="e6416-211">Batch의 응용 프로그램과 응용 프로그램 패키지에 대한 자세한 내용은 [Batch 응용 프로그램 패키지를 사용하여 계산 노드에 응용 프로그램 배포](batch-application-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6416-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/