---
title: "aaaManage Azure PowerShell 사용 하 여 솔루션 | Microsoft Docs"
description: "Azure PowerShell 및 리소스 관리자 toomanage 리소스를 사용 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="89304-103">Azure PowerShell 및 Resource Manager를 사용하여 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="89304-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89304-104">포털</span><span class="sxs-lookup"><span data-stu-id="89304-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="89304-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="89304-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="89304-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89304-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="89304-107">REST API</span><span class="sxs-lookup"><span data-stu-id="89304-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="89304-108">이 문서에서는 설명 어떻게 toomanage Azure PowerShell 및 Azure 리소스 관리자를 사용 하 여 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="89304-109">Resource Manager에 익숙하지 않은 경우에는 [Resource Manager 개요](resource-group-overview.md) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="89304-110">이 항목에서는 관리 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="89304-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="89304-111">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-111">You will:</span></span>

1. <span data-ttu-id="89304-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="89304-112">Create a resource group</span></span>
2. <span data-ttu-id="89304-113">리소스 toohello 리소스 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="89304-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="89304-114">태그 toohello 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="89304-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="89304-115">이름 또는 태그 값을 기반으로 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="89304-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="89304-116">적용 및 hello 리소스에 대 한 잠금을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="89304-117">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="89304-117">Delete a resource group</span></span>

<span data-ttu-id="89304-118">이 문서는 표시 되지 않습니다 어떻게 toodeploy 리소스 관리자 템플릿 tooyour 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="89304-119">해당 정보는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="89304-120">Azure PowerShell 시작</span><span class="sxs-lookup"><span data-stu-id="89304-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="89304-121">Azure PowerShell을 설치 하지 않은 경우 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="89304-122">지난 hello에서 Azure PowerShell 설치 해도 최근 업데이트 하지 않은 경우에 hello 최신 버전을 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="89304-123">Hello 통해 hello 버전을 업데이트할 수 있습니다 tooinstall 사용한 동일한 방법을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="89304-124">예를 들어 hello 웹 플랫폼 설치 관리자를 사용 하는 경우 다시 시작 하 고 업데이트에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="89304-125">toocheck 프로그램 버전의 hello Azure 리소스 모듈을 사용 하 여 다음 cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="89304-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="89304-126">이 항목은 버전 3.3.0에 대해 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="89304-127">이전 버전을 설치 환경이이 항목에 설명 된 hello 단계와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="89304-128">이 버전의 hello cmdlet에 대 한 설명서를 참조 하십시오. [AzureRM.Resources 모듈](/powershell/module/azurerm.resources)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="89304-129">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="89304-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="89304-130">솔루션 작업을 하기 전에 tooyour 계정에 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="89304-131">toolog tooyour Azure 계정에서에서 사용 하 여 hello **로그인 AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89304-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="89304-132">hello cmdlet Azure 계정에 대 한 hello 로그인 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="89304-133">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="89304-134">hello cmdlet hello 작업에 대 한 사용자 계정 및 hello 구독 toouse에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="89304-135">둘 이상의 구독을 보유 하는 경우 다른 구독 tooa 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="89304-136">첫째, 모든 hello 구독 계정에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="89304-137">사용되는 구독 및 사용이 해제된 구독을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="89304-138">tooswitch tooa 다른 구독 hello로 hello 구독 이름 제공 **집합 AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89304-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="89304-139">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="89304-139">Create a resource group</span></span>
<span data-ttu-id="89304-140">모든 리소스 tooyour 구독을 배포 하기 전에 hello 리소스 포함 될 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="89304-141">리소스 그룹 toocreate hello를 사용 하 여 **새로 AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89304-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="89304-142">hello 명령은 hello를 사용 하 여 **이름** 매개 변수 toospecify hello 리소스 그룹 및 hello에 대 한 이름 **위치** 매개 변수 toospecify의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="89304-143">hello 출력 형식에 따라 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="89304-144">Tooretrieve hello 리소스 그룹을 나중에 필요한 경우 hello 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="89304-145">tooget 모든 hello 구독에서 리소스 그룹, 이름을 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="89304-146">리소스 tooa 리소스 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="89304-146">Add resources tooa resource group</span></span>
<span data-ttu-id="89304-147">리소스 toohello 리소스 그룹 tooadd hello를 사용할 수 있습니다 **새로 AzureRmResource** 만드는 cmdlet 또는 리소스의 특정 toohello 형식인 cmdlet (같은 **새로 AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="89304-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="89304-148">보다 쉽게 toouse hello 새 리소스에 필요한 hello 속성에 대 한 매개 변수를 포함 하기 때문에 특정 tooa 리소스 종류를 된 cmdlet을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="89304-149">toouse **새로 AzureRmResource**, 해당 입력 하지 않고도 모든 hello 속성 tooset를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="89304-150">그러나 cmdlet 통해 리소스 추가 hello 새 리소스는 리소스 관리자 템플릿을에 없기 때문에 이후 혼란이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="89304-151">리소스 관리자 템플릿을에서 Azure 솔루션에 대 한 hello 인프라를 정의 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="89304-152">템플릿과 tooreliably를 사용 하면 반복적으로 솔루션을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="89304-153">이 항목에서는 PowerShell cmdlet을 사용하여 저장소 계정을 만들지만 나중에 리소스 그룹에서 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="89304-154">cmdlet을 다음 hello 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89304-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="89304-155">Hello 예제에 표시 된 hello 이름을 사용 하는 대신 hello 저장소 계정에 대 한 고유 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="89304-156">hello 이름은 길이가 3 ~ 24 자 사이 여야 하 고 숫자 및 소문자만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="89304-157">Hello 예제에 표시 된 hello 이름을 사용 하는 경우 해당 이름을 이미 사용 중이기 때문에 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="89304-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="89304-158">필요한 경우 tooretrieve이이 리소스 나중, 사용 cmdlet을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="89304-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="89304-159">태그 추가</span><span class="sxs-lookup"><span data-stu-id="89304-159">Add a tag</span></span>

<span data-ttu-id="89304-160">태그 사용 하면 tooorganize toodifferent 속성에 따라 리소스 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="89304-161">예를 들어 여러 리소스 toohello 속하는 다른 리소스 그룹에 있을 수 있습니다 같은 동일 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="89304-162">부서 태그 및 값 toothose 리소스 toomark를 적용할 수 속하는 toohello 것 같은 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="89304-163">또는 리소스가 프로덕션 환경에서 사용되는지 또는 테스트 환경에서 사용되는지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="89304-164">이 항목에서는 태그 tooonly, 리소스가 두 개를 적용 하지만 사용자 환경에서 가장 가능성이 높은 의미가 tooapply 태그 tooall 리소스.</span><span class="sxs-lookup"><span data-stu-id="89304-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="89304-165">hello 다음 cmdlet은 두 태그 tooyour 저장소 계정에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89304-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="89304-166">태그는 단일 개체로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="89304-166">Tags are updated as a single object.</span></span> <span data-ttu-id="89304-167">먼저 tooadd 태그에 이미 포함 되어 있는 태그 tooa 리소스 hello 기존 태그를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="89304-168">Hello 새 태그 toohello 개체가 있는 hello 기존 태그를 추가 하 고 모든 hello 태그 toohello 리소스를 다시 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="89304-169">리소스 검색</span><span class="sxs-lookup"><span data-stu-id="89304-169">Search for resources</span></span>

<span data-ttu-id="89304-170">사용 하 여 hello **찾기 AzureRmResource** 다른 검색 조건에 대 한 cmdlet tooretrieve 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="89304-171">이름으로 리소스 tooget 제공 hello **ResourceNameContains** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="89304-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="89304-172">tooget 리소스 그룹의 모든 hello 리소스 제공 hello **ResourceGroupNameContains** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="89304-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="89304-173">tooget 태그 이름 및 값을 가진 모든 hello 리소스 제공 hello **TagName** 및 **TagValue** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="89304-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="89304-174">특정 리소스 종류를 사용 하 여 tooall hello 리소스 제공 hello **ResourceType** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="89304-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="89304-175">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="89304-175">Lock a resource</span></span>

<span data-ttu-id="89304-176">Toomake 중요 한 리소스를 실수로 삭제 하거나 수정 해야 하는 경우에 잠금 toohello 리소스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="89304-177">**CanNotDelete** 또는 **ReadOnly**를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="89304-178">관리 잠금 toocreate 또는 delete 권한이 너무`Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="89304-179">Hello 기본 제공 역할의 소유자 및 사용자 액세스 관리자에 게 이러한 작업을 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89304-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="89304-180">잠금을 tooapply hello 다음 cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="89304-181">hello hello 예제에서는 이전에 잠긴된 리소스 삭제할 수 없습니다 hello 잠금을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="89304-182">tooremove 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="89304-183">잠금 설정에 대한 자세한 내용은 [Azure Resource Manager를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="89304-184">리소스 또는 리소스 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="89304-184">Remove resources or resource group</span></span>
<span data-ttu-id="89304-185">리소스 또는 리소스 그룹을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="89304-186">리소스 그룹을 제거 하면 해당 리소스 그룹 내의 모든 hello 리소스 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="89304-187">toodelete hello 리소스 그룹을 사용 하 여 hello에서 리소스 **제거 AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89304-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="89304-188">이 cmdlet은 hello 리소스를 삭제 하지만 hello 리소스 그룹을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="89304-189">toodelete 리소스 그룹 및 모든 리소스를 사용 하 여 hello **제거 AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="89304-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="89304-190">두 cmdlet 모두에 대 한 tooconfirm 묻는 tooremove hello 리소스 또는 리소스 그룹 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="89304-191">반환 하는 경우 hello 작업 hello 리소스 또는 리소스 그룹이 성공적으로 삭제, **True**합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="89304-192">Azure Automation을 사용하여 Resource Manager 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="89304-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="89304-193">이 항목에서는 tooperform Azure PowerShell을 사용한 리소스에 대 한 기본 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="89304-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="89304-194">고급 관리 시나리오에 대 한 일반적으로 스크립트를 toocreate을 필요에 따라 또는 일정에 따라 해당 스크립트를 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="89304-195">[Azure 자동화](../automation/automation-intro.md) Azure 솔루션을 관리 하는 tooautomate 자주 사용 되는 스크립트를 한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="89304-196">hello 다음 항목 보여 toouse Azure 자동화, 리소스 관리자 및 PowerShell tooeffectively 관리 작업을 수행 방법:</span><span class="sxs-lookup"><span data-stu-id="89304-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="89304-197">Runbook 만들기에 대한 내용은 [내 첫 번째 PowerShell Runbook](../automation/automation-first-runbook-textual-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="89304-198">스크립트 갤러리 작업에 대한 내용은 [Azure Automation용 Runbook 및 모듈 갤러리](../automation/automation-runbook-gallery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="89304-199">시작 하 고 가상 컴퓨터를 중지 하는 runbook에 대 한 참조 [Azure 자동화 시나리오: 태그를 사용 하 여 JSON 형식 toocreate Azure VM 시작 및 종료에 대 한 일정](../automation/automation-scenario-start-stop-vm-wjson-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="89304-200">가상 컴퓨터 업무 외 시간을 시작하고 중지하는 Runbook에 대한 내용은 [Automation의 업무 시간 외 VM 시작/중지 솔루션](../automation/automation-solution-vm-management.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89304-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89304-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89304-201">Next steps</span></span>
* <span data-ttu-id="89304-202">리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [Azure 리소스 관리자 템플릿 제작](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="89304-203">템플릿 배포에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="89304-204">기존 리소스 tooa 새 리소스 그룹을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89304-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="89304-205">예제를 보려면 [구독 또는 리소스 그룹 리소스 이동 tooNew](resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="89304-206">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="89304-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

