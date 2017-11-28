---
title: "Azure 일괄 처리에 대 한 PowerShell 시작 aaaGet | Microsoft Docs"
description: "간략 한 소개 toohello toomanage 일괄 처리 리소스를 사용 하는 Azure PowerShell cmdlet"
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
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="5ad6c-103">PowerShell cmdlet을 사용한 Batch 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="5ad6c-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="5ad6c-104">Hello Azure 일괄 처리 PowerShell cmdlet, 수행 하 고 사용할 수 다양 한 hello 스크립트 같은 hello Api 일괄 처리로 수행 하면 Azure 포털 hello 작업과 hello Azure 명령줄 인터페이스 (CLI).</span><span class="sxs-lookup"><span data-stu-id="5ad6c-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="5ad6c-105">이 간략 한 소개 toohello cmdlet toomanage 일괄 처리 계정을 사용 하 고로 풀, 작업, 및 작업과 같은 일괄 처리 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="5ad6c-106">일괄 처리 cmdlet과 구문을 자세한 cmdlet의 전체 목록은 참조 hello [Azure 배치 cmdlet 참조](/powershell/module/azurerm.batch/#batch)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="5ad6c-107">이 문서는 Azure PowerShell 버전 3.0.0의 cmdlet를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="5ad6c-108">Azure PowerShell 업데이트 하는 것이 좋습니다 자주 tootake 활용 해도 서비스 업데이트 및 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ad6c-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5ad6c-109">Prerequisites</span></span>
<span data-ttu-id="5ad6c-110">일괄 처리 리소스 hello 작업 toouse Azure PowerShell toomanage 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="5ad6c-111">Azure PowerShell 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="5ad6c-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="5ad6c-112">Hello 실행 **로그인 AzureRmAccount** cmdlet tooconnect tooyour 구독 (hello hello Azure 리소스 관리자 모듈에서 cmdlet 배송 Azure 배치):</span><span class="sxs-lookup"><span data-stu-id="5ad6c-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="5ad6c-113">**Hello 일괄 처리에 대 한 공급자 네임 스페이스를 가진 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="5ad6c-114">이 작업을 수행할 toobe 하기만 **구독 마다 한 번만**합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="5ad6c-115">배치 계정 및 키 관리</span><span class="sxs-lookup"><span data-stu-id="5ad6c-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="5ad6c-116">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="5ad6c-116">Create a Batch account</span></span>
<span data-ttu-id="5ad6c-117">**New-AzureRmBatchAccount**는 지정된 리소스 그룹에서 배치 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="5ad6c-118">리소스 그룹을 아직 없는 경우 hello를 실행 하 여 하나를 만들 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="5ad6c-119">Hello Azure 중 하나를 지정 영역 hello에 **위치** "Central US"와 같은 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="5ad6c-120">예:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="5ad6c-121">그런 다음 hello 계정에 대 한 이름을 지정 하는 hello 리소스 그룹에 일괄 처리 계정을 만듭니다 <*account_name*> hello 위치 및 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="5ad6c-122">Hello 일괄 처리 계정 만들기 시간 toocomplete 일부 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="5ad6c-123">예:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="5ad6c-124">hello 일괄 처리 계정 이름은 고유한 toohello hello 리소스 그룹에 대 한 Azure 지역 해야 합니다. 3 ~ 24 자 사이의 문자를 포함 하 고 소문자와 숫자만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="5ad6c-125">계정 액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ad6c-125">Get account access keys</span></span>
<span data-ttu-id="5ad6c-126">**Get AzureRmBatchAccountKeys** Azure 배치 계정에 연결 된 hello 액세스 키를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="5ad6c-127">예를 들어 hello tooget 만든 hello 계정의 기본 및 보조 키 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="5ad6c-128">새 액세스 키 생성</span><span class="sxs-lookup"><span data-stu-id="5ad6c-128">Generate a new access key</span></span>
<span data-ttu-id="5ad6c-129">**New-AzureRmBatchAccountKey** 는 Azure 배치 계정에 대해 기본 또는 보조 계정 키를 새로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="5ad6c-130">예를 들어, toogenerate 일괄 처리 계정에 새 기본 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="5ad6c-131">hello에 대 한 "보조 데이터베이스"를 지정 하는 새 보조 키를 toogenerate **KeyType** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="5ad6c-132">Tooregenerate hello 기본 및 보조 키를 개별적으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="5ad6c-133">배치 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="5ad6c-133">Delete a Batch account</span></span>
<span data-ttu-id="5ad6c-134">**Remove-AzureRmBatchAccount** 는 배치 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="5ad6c-135">예:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="5ad6c-136">대화 상자가 나타나면 원하는 tooremove hello 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="5ad6c-137">계정 제거 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="5ad6c-138">BatchAccountContext 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="5ad6c-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="5ad6c-139">일괄 처리 PowerShell cmdlet 생성 하 고 일괄 처리 풀, 작업, 작업을 관리 하 고 다른 리소스는 먼저 BatchAccountContext 개체 toostore를 만들면 계정 이름과 키 hello tooauthenticate를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="5ad6c-140">사용 하 여 hello cmdlet에 hello BatchAccountContext 개체를 전달 하면 **BatchContext** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="5ad6c-141">기본적으로 인증을 위해 hello 계정의 기본 키가 사용 되지만 BatchAccountContext 개체의 변경 하 여 hello 키 toouse를 명시적으로 선택할 수 있습니다 **KeyInUse** 속성: `$context.KeyInUse = "Secondary"`합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="5ad6c-142">배치 리소스 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="5ad6c-142">Create and modify Batch resources</span></span>
<span data-ttu-id="5ad6c-143">와 같은 cmdlet을 사용 하 여 **새로 AzureBatchPool**, **새로 AzureBatchJob**, 및 **새로 AzureBatchTask** 일괄 처리 계정 내 toocreate 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="5ad6c-144">해당 **Get-** 및 **Set-** 기존 리소스의 cmdlet tooupdate hello 속성 및 **e-** 일괄 처리 계정 내 cmdlet tooremove 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="5ad6c-145">이러한 cmdlet 중 많은의 사용할 경우 추가 toopassing BatchContext 개체 toocreate 또는 hello 다음 예제와 같이 자세한 리소스 설정을 포함 하는 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="5ad6c-146">참조 hello 추가 예제에 대 한 각 cmdlet에 대 한 도움말을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="5ad6c-147">배치 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="5ad6c-147">Create a Batch pool</span></span>
<span data-ttu-id="5ad6c-148">Hello hello에 운영 체제 계산 노드 수에 대 한 hello 클라우드 서비스 구성 또는 hello 가상 컴퓨터 구성을 선택 하면을 만들거나 배치 풀을 업데이트할 때 (참조 [배치 기능 개요](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="5ad6c-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="5ad6c-149">계산 노드는 hello 중 하나가 지정 된 이미지로 다시 hello 클라우드 서비스 구성을 지정 하면 [Azure 게스트 OS 릴리스와](../cloud-services/cloud-services-guestos-update-matrix.md#releases)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="5ad6c-150">가상 컴퓨터 구성 hello를 지정 하면 지정 하거나 hello 중 하나가 지원 Linux 또는 Windows VM 이미지에 나열 된 hello [Azure 가상 컴퓨터 마켓플레이스][vm_marketplace], 하거나 사용자 지정을 제공 합니다. 이미지 준비 했는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="5ad6c-151">실행 하는 경우 **새로 AzureBatchPool**, hello 운영 체제 설정을 PSCloudServiceConfiguration 또는 PSVirtualMachineConfiguration 개체에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="5ad6c-152">예를 들어 hello 다음 cmdlet 새 풀을 만듭니다 일괄 처리 크기의 소형 컴퓨팅 노드를 제품군 3 (Windows Server 2012)의 최신 운영 체제 버전 hello와 함께 이미지로 hello 클라우드 서비스 구성.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="5ad6c-153">여기에서 hello **CloudServiceConfiguration** 매개 변수 지정 hello *$configuration* hello PSCloudServiceConfiguration 개체로 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="5ad6c-154">hello **BatchContext** 이전에 정의 된 변수를 지정 하는 매개 변수 *$context* hello BatchAccountContext 개체로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="5ad6c-155">hello 대상 hello 새 풀의 계산 노드 수는 자동 크기 조정 수식에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="5ad6c-156">이 경우 hello 수식은 단순히 **$TargetDedicated = 4**, 최대 4는 hello hello 풀의 계산 노드 수를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="5ad6c-157">풀, 작업, 태스크 및 기타 상세 정보 쿼리</span><span class="sxs-lookup"><span data-stu-id="5ad6c-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="5ad6c-158">와 같은 cmdlet을 사용 하 여 **Get AzureBatchPool**, **Get AzureBatchJob**, 및 **Get AzureBatchTask** tooquery 일괄 처리 계정에서 엔터티에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="5ad6c-159">데이터에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="5ad6c-159">Query for data</span></span>
<span data-ttu-id="5ad6c-160">예를 사용 하 여 **Get AzureBatchPools** toofind 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="5ad6c-161">귀하의 계정에서 모든 풀에 대 한 쿼리이 기본적으로 hello BatchAccountContext 개체에 저장 이미 가정 하 고 *$context*:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="5ad6c-162">OData 필터 사용</span><span class="sxs-lookup"><span data-stu-id="5ad6c-162">Use an OData filter</span></span>
<span data-ttu-id="5ad6c-163">Hello를 사용 하 여 OData 필터를 제공할 수 있습니다 **필터** 매개 변수 toofind에만 개체에 관심이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="5ad6c-164">예를 들어, "myPool"로 시작하는 ID를 갖는 모든 풀을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="5ad6c-165">이 방법은 로컬 파이프라인에서 "Where-Object"를 사용하는 것만큼 유연하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="5ad6c-166">그러나 hello 쿼리가 전송 toohello 일괄 처리 서비스 직접 hello 서버 측에서 인터넷 대역폭 절약 모든 필터링이 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="5ad6c-167">Hello Id 매개 변수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5ad6c-167">Use hello Id parameter</span></span>
<span data-ttu-id="5ad6c-168">대체 tooan OData 필터는 toouse hello **Id** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="5ad6c-169">myPool"id"를 사용 하 여 특정 풀에 대 한 tooquery:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="5ad6c-170">hello **Id** 전체 id 검색, 하지 와일드 카드 또는 OData 스타일 필터 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="5ad6c-171">Hello MaxCount 매개 변수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5ad6c-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="5ad6c-172">기본적으로 각 cmdlet은 최대 1000개의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="5ad6c-173">이 한도 도달 하면 필터 toobring 다시 적은 개체를 구체화 하거나 명시적으로 설정 hello를 사용 하 여 최대 **MaxCount** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="5ad6c-174">예:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="5ad6c-175">tooremove hello 상한 설정 **MaxCount** too0 이하의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="5ad6c-176">Hello PowerShell 파이프라인을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5ad6c-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="5ad6c-177">일괄 처리 cmdlet hello PowerShell 파이프라인 toosend cmdlet 간에 데이터를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="5ad6c-178">이 설정은 효과가 같음 보다 쉽게 여러 엔터티 작업 하지만 매개 변수를 지정 하는 hello.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="5ad6c-179">예를 들어, 다음과 같이 사용자 계정 아래의 모든 작업을 찾아서 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="5ad6c-180">풀의 모든 계산 노드 다시 시작(다시 부팅):</span><span class="sxs-lookup"><span data-stu-id="5ad6c-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="5ad6c-181">응용 프로그램 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="5ad6c-181">Application package management</span></span>
<span data-ttu-id="5ad6c-182">응용 프로그램 패키지 toodeploy 응용 프로그램 toohello 계산 노드가 풀에는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="5ad6c-183">Hello 일괄 처리 PowerShell cmdlet로 업로드 하 고 일괄 처리 계정에 응용 프로그램 패키지를 관리 및 패키지 버전 toocompute 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="5ad6c-184">**만듭니다** .</span><span class="sxs-lookup"><span data-stu-id="5ad6c-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="5ad6c-185">**추가합니다** .</span><span class="sxs-lookup"><span data-stu-id="5ad6c-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="5ad6c-186">집합 hello **기본 버전** hello 응용 프로그램에 대 한:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="5ad6c-187">응용 프로그램의 패키지 **열거**</span><span class="sxs-lookup"><span data-stu-id="5ad6c-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="5ad6c-188">응용 프로그램 패키지 **삭제**</span><span class="sxs-lookup"><span data-stu-id="5ad6c-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="5ad6c-189">응용 프로그램 **삭제**</span><span class="sxs-lookup"><span data-stu-id="5ad6c-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="5ad6c-190">Hello 응용 프로그램을 삭제 하기 전에는 모든 응용 프로그램의 응용 프로그램 패키지 버전을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="5ad6c-191">Toodelete 현재 응용 프로그램 패키지에 있는 응용 프로그램을 시도 하면 '충돌' 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="5ad6c-192">응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="5ad6c-192">Deploy an application package</span></span>
<span data-ttu-id="5ad6c-193">새 풀을 만들 때 배포에 하나 이상의 응용 프로그램 패키지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="5ad6c-194">풀을 만들 때 패키지를 지정할 때 hello 노드 조인 그룹으로 배포 된 tooeach 노드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="5ad6c-195">패키지는 노드를 다시 부팅하거나 이미지로 다시 설치하는 경우에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="5ad6c-196">Hello 지정 `-ApplicationPackageReference` hello 풀을 연결 하는 대로 풀 toodeploy 응용 프로그램 패키지 toohello 풀의 노드를 만들 때 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="5ad6c-197">먼저 만듭니다는 **PSApplicationPackageReference** 개체를 hello 응용 프로그램 Id와 패키지 버전을 toodeploy toohello 풀의 계산 노드를 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="5ad6c-198">이제 hello 그룹을 만들고 인수 toohello hello hello 패키지 참조 방식 개체 지정 `ApplicationPackageReferences` 옵션:</span><span class="sxs-lookup"><span data-stu-id="5ad6c-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="5ad6c-199">응용 프로그램 패키지에 더 많은 정보를 찾을 수 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ad6c-200">수행 해야 [Azure 저장소 계정 연결](#linked-storage-account-autostorage) tooyour 일괄 처리 계정 toouse 응용 프로그램 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="5ad6c-201">풀의 응용 프로그램 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="5ad6c-201">Update a pool's application packages</span></span>
<span data-ttu-id="5ad6c-202">첫 번째 tooan 기존 풀을 할당 된 tooupdate hello 응용 프로그램 hello 필요한 속성 (응용 프로그램 Id와 패키지 버전)을 가진 PSApplicationPackageReference 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="5ad6c-203">다음으로 hello 풀 일괄 처리에서 기존 패키지를 모두 지울, 우리의 새 패키지 참조 추가 가져온 hello 새 풀 설정으로 hello 일괄 처리 서비스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="5ad6c-204">이제 hello 일괄 처리 서비스에서 hello 풀의 속성 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="5ad6c-205">tooactually hello 새 응용 프로그램 패키지 toocompute 노드 hello 풀의 배포, 있지만 다시 시작 해야 하거나 해당 노드를 이미지로 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="5ad6c-206">이 명령을 사용하여 풀의 모든 노드를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="5ad6c-207">풀에 여러 응용 프로그램 패키지 toohello 계산 노드를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="5ad6c-208">너무 원하는 경우*추가* hello 현재 배포 된 패키지를 대체 하지 않고 응용 프로그램 패키지 생략 hello `$pool.ApplicationPackageReferences.Clear()` 위의 줄.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5ad6c-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ad6c-209">Next steps</span></span>
* <span data-ttu-id="5ad6c-210">자세한 cmdlet 구문 및 예제는 [Azure 배치 cmdlet 참조](/powershell/module/azurerm.batch/#batch)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="5ad6c-211">응용 프로그램 및 일괄 처리에서 응용 프로그램 패키지에 대 한 자세한 내용은 참조 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ad6c-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/