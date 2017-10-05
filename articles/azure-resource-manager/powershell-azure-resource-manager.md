---
title: "PowerShell을 사용한 Azure 솔루션 관리 | Microsoft Docs"
description: "Azure PowerShell 및 Resource Manager를 사용하여 리소스를 관리합니다."
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
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="8dad9-103">Azure PowerShell 및 Resource Manager를 사용하여 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="8dad9-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dad9-104">포털</span><span class="sxs-lookup"><span data-stu-id="8dad9-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="8dad9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8dad9-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="8dad9-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dad9-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="8dad9-107">REST API</span><span class="sxs-lookup"><span data-stu-id="8dad9-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="8dad9-108">이 문서에서는 Azure PowerShell 및 Azure Resource Manager를 사용하여 솔루션을 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="8dad9-109">Resource Manager에 익숙하지 않은 경우에는 [Resource Manager 개요](resource-group-overview.md) 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="8dad9-110">이 항목에서는 관리 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="8dad9-111">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-111">You will:</span></span>

1. <span data-ttu-id="8dad9-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8dad9-112">Create a resource group</span></span>
2. <span data-ttu-id="8dad9-113">리소스 그룹에 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="8dad9-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="8dad9-114">리소스에 태그 추가</span><span class="sxs-lookup"><span data-stu-id="8dad9-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="8dad9-115">이름 또는 태그 값을 기반으로 리소스 쿼리</span><span class="sxs-lookup"><span data-stu-id="8dad9-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="8dad9-116">리소스에 대하 잠금 적용 및 제거</span><span class="sxs-lookup"><span data-stu-id="8dad9-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="8dad9-117">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="8dad9-117">Delete a resource group</span></span>

<span data-ttu-id="8dad9-118">이 문서에서는 Resource Manager 템플릿을 구독에 배포하는 방법을 보여 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="8dad9-119">해당 정보는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="8dad9-120">Azure PowerShell 시작</span><span class="sxs-lookup"><span data-stu-id="8dad9-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="8dad9-121">Azure PowerShell을 설치하지 않은 경우 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8dad9-122">Azure PowerShell을 전에 설치했지만 최근에 업데이트하지 않은 경우에는 최신 버전을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="8dad9-123">설치하는 방법과 동일한 방법을 통해 버전을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="8dad9-124">예를 들어 웹 플랫폼 설치 관리자를 사용한 경우에는 관리자를 다시 시작하고 업데이트를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="8dad9-125">Azure 리소스 모듈의 버전을 확인하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="8dad9-126">이 항목은 버전 3.3.0에 대해 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="8dad9-127">이보다 오래된 버전이 설치되어 있는 경우에는 사용자의 환경이 이 항목에 표시되는 단계와 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="8dad9-128">이 버전의 cmdlet에 대한 설명서는 [AzureRM.Resources Module](/powershell/module/azurerm.resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="8dad9-129">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-129">Log in to your Azure account</span></span>
<span data-ttu-id="8dad9-130">솔루션에서 작업하기 전에 자신의 계정으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="8dad9-131">Azure 계정에 로그인하려면 **Login-AzureRmAccount** Cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8dad9-132">Cmdlet가 Azure 계정에 대한 로그인 자격 증명을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="8dad9-133">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="8dad9-134">이 cmdlet은 작업에 사용할 구독과 계정에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="8dad9-135">구독이 둘 이상인 경우에는 다른 구독으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="8dad9-136">우선 계정에 대한 모든 구독을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="8dad9-137">사용되는 구독 및 사용이 해제된 구독을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="8dad9-138">다른 구독으로 전환하려면 **Set-AzureRmContext** cmdlet에 구독 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8dad9-139">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8dad9-139">Create a resource group</span></span>
<span data-ttu-id="8dad9-140">구독에 리소스를 배포하려면 리소스를 포함하는 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="8dad9-141">리소스 그룹을 만들려면 **New-AzureRmResourceGroup** Cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="8dad9-142">이 명령은 **Name** 매개 변수를 사용하여 리소스 그룹에 대한 이름을 지정하고 **Location** 매개 변수를 사용하여 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="8dad9-143">다음 형식으로 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="8dad9-144">나중에 리소스 그룹을 검색해야 하는 경우 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="8dad9-145">구독에서 리소스 그룹을 모두 가져오려면 이름을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="8dad9-146">리소스 그룹에 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="8dad9-146">Add resources to a resource group</span></span>
<span data-ttu-id="8dad9-147">리소스를 리소스 그룹에 추가하려면 **New-AzureRmResource** cmdlet을 사용하거나 만드는 리소스의 종류에 해당하는 cmdlet(예: **New-AzureRmStorageAccount**)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="8dad9-148">리소스의 종류에 해당하는 cmdlet에는 새 리소스에 필요한 속성의 매개 변수가 포함되기 때문에 이 cmdlet을 사용하는 것이 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="8dad9-149">**New-AzureRmResource**를 사용하는 경우 속성을 설정하라는 메시지를 표시하지 않으려면 설정할 속성을 모두 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="8dad9-150">하지만 cmdlet을 통해 리소스를 추가하면 새 리소스가 Resource Manager 템플릿에 존재하지 않기 때문에 나중에 혼동을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="8dad9-151">Azure 솔루션에 대한 인프라는 Resource Manager 템플릿에서 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="8dad9-152">템플릿을 사용하면 솔루션을 안정적이고 반복적으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="8dad9-153">이 항목에서는 PowerShell cmdlet을 사용하여 저장소 계정을 만들지만 나중에 리소스 그룹에서 템플릿을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="8dad9-154">다음 cmdlet은 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="8dad9-155">예제에 표시된 이름을 사용하는 대신 저장소 계정에 대한 고유 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="8dad9-156">이름은 길이가 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="8dad9-157">예제에 표시된 이름을 사용하면 해당 이름을 이미 사용 중이기 때문에 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="8dad9-158">나중에 이 리소스를 검색해야 하는 경우 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="8dad9-159">태그 추가</span><span class="sxs-lookup"><span data-stu-id="8dad9-159">Add a tag</span></span>

<span data-ttu-id="8dad9-160">태그를 사용하면 다양한 속성에 따라 리소스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="8dad9-161">예를 들어 동일한 부서에 속하는 여러 리소스 그룹에 몇 가지 리소스를 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="8dad9-162">리소스에 부서 태그 및 값을 적용하여 동일한 범주에 속하는 것으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="8dad9-163">또는 리소스가 프로덕션 환경에서 사용되는지 또는 테스트 환경에서 사용되는지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="8dad9-164">이 항목에서는 하나의 리소스에만 태그를 적용하지만 사용자 환경에서는 모든 리소스에 태그를 적용하는 것이 대부분 타당합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="8dad9-165">다음 cmdlet은 저장소 계정에 두 개의 태그를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="8dad9-166">태그는 단일 개체로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-166">Tags are updated as a single object.</span></span> <span data-ttu-id="8dad9-167">이미 태그가 포함된 리소스에 태그를 추가하려면 우선 기존 태그를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="8dad9-168">기존 태그가 포함된 개체에 새 태그를 추가하고 리소스에 모든 태그를 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="8dad9-169">리소스 검색</span><span class="sxs-lookup"><span data-stu-id="8dad9-169">Search for resources</span></span>

<span data-ttu-id="8dad9-170">다른 검색 조건에 대해 리소스를 검색하려면 **Find-AzureRmResource** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="8dad9-171">이름으로 리소스를 가져오려면 **ResourceNameContains** 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="8dad9-172">리소스 그룹의 리소스를 모두 가져오려면 **ResourceGroupNameContains** 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="8dad9-173">태그 이름 및 값을 사용하여 리소스를 모두 가져오려면 **TagName** 및 **TagValue** 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="8dad9-174">특정 리소스 종류에 해당하는 리소스를 모두 가져오려면 **ResourceType** 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="8dad9-175">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="8dad9-175">Lock a resource</span></span>

<span data-ttu-id="8dad9-176">중요한 리소스가 실수로 삭제되거나 수정되지 않도록 해야 하는 경우에는 리소스에 잠금을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="8dad9-177">**CanNotDelete** 또는 **ReadOnly**를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="8dad9-178">관리 잠금을 만들거나 삭제하려면 `Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="8dad9-179">기본 제공 역할의 경우 소유자 및 사용자 액세스 관리자에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="8dad9-180">잠금을 적용하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="8dad9-181">앞의 예제에서 잠긴 리소스는 잠금이 제거될 때까지 삭제될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="8dad9-182">잠금을 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="8dad9-183">잠금 설정에 대한 자세한 내용은 [Azure Resource Manager를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="8dad9-184">리소스 또는 리소스 그룹 제거</span><span class="sxs-lookup"><span data-stu-id="8dad9-184">Remove resources or resource group</span></span>
<span data-ttu-id="8dad9-185">리소스 또는 리소스 그룹을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="8dad9-186">리소스 그룹을 제거하면 리소스 그룹에 포함된 리소스도 모두 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="8dad9-187">리소스 그룹에서 리소스를 삭제하려면 **Remove-AzureRmResource** cmdlet를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="8dad9-188">이 cmdlet은 리소스를 삭제하지만 리소스 그룹은 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="8dad9-189">리소스 그룹과 거기에 포함된 리소스를 모두 삭제하려면 **Remove-AzureRmResourceGroup** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="8dad9-190">두 cmdlet 모두, 리소스 또는 리소스 그룹을 제거할지를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="8dad9-191">작업에서 리소스 또는 리소스 그룹이 성공적으로 삭제되면 **True**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="8dad9-192">Azure Automation을 사용하여 Resource Manager 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="8dad9-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="8dad9-193">이 항목은 Azure PowerShell을 사용하여 리소스에 기본적인 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="8dad9-194">고급 관리 시나리오의 경우 일반적으로 스크립트를 만들고 필요에 따라 또는 일정에 따라 스크립트를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="8dad9-195">[Azure Automation](../automation/automation-intro.md)은 Azure 솔루션을 관리하는 자주 사용되는 스크립트를 자동화하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="8dad9-196">다음 항목은 Azure Automation, Resource Manager 및 PowerShell을 사용하여 관리 작업을 효과적으로 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="8dad9-197">Runbook 만들기에 대한 내용은 [내 첫 번째 PowerShell Runbook](../automation/automation-first-runbook-textual-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="8dad9-198">스크립트 갤러리 작업에 대한 내용은 [Azure Automation용 Runbook 및 모듈 갤러리](../automation/automation-runbook-gallery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="8dad9-199">가상 컴퓨터를 시작하고 중지하는 Runbook에 대한 내용은 [Azure Automation 시나리오: JSON 형식 태그를 사용하여 Azure VM 시작 및 종료 일정 만들기](../automation/automation-scenario-start-stop-vm-wjson-tags.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="8dad9-200">가상 컴퓨터 업무 외 시간을 시작하고 중지하는 Runbook에 대한 내용은 [Automation의 업무 시간 외 VM 시작/중지 솔루션](../automation/automation-solution-vm-management.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dad9-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8dad9-201">Next steps</span></span>
* <span data-ttu-id="8dad9-202">Resource Manager 템플릿을 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8dad9-203">템플릿 배포에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="8dad9-204">기존 리소스를 새 리소스 그룹으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dad9-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="8dad9-205">예제를 보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="8dad9-206">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dad9-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

