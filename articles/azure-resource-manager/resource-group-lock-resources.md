---
title: "Azure 리소스 잠금으로 변경 방지 | Microsoft Docs"
description: "모든 사용자 및 역할에 대해 잠금을 적용하여 사용자가 중요한 Azure 리소스를 업데이트하거나 삭제하지 못하도록 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="22598-103">예기치 않은 변경을 방지하기 위해 리소스 잠그기</span><span class="sxs-lookup"><span data-stu-id="22598-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="22598-104">관리자는 구독, 리소스 그룹 또는 리소스에 잠금을 설정하여 조직의 다른 사용자가 실수로 중요한 리소스를 삭제 또는 수정하지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="22598-105">잠금 수준을 **CanNotDelete** 또는 **ReadOnly**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="22598-106">**CanNotDelete**는 권한이 부여된 사용자가 리소스를 읽고 수정할 수 있지만 삭제할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="22598-107">**ReadOnly**는 권한이 부여된 사용자가 리소스를 읽을 수 있지만 해당 리소스를 삭제하거나 업데이트할 수 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="22598-108">이 잠금을 적용하는 것은 권한 있는 모든 사용자에게 **판독기** 역할에서 부여한 권한을 제한하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="22598-109">잠금을 적용하는 방법</span><span class="sxs-lookup"><span data-stu-id="22598-109">How locks are applied</span></span>

<span data-ttu-id="22598-110">부모 범위에서 잠금을 적용하면 해당 범위 내 모든 리소스가 동일한 잠금을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="22598-111">나중에 추가하는 리소스도 부모의 잠금을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="22598-112">상속의 가장 제한적인 잠금이 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="22598-113">역할 기반 액세스 제어와 달리 관리 잠금을 사용하여 모든 사용자와 역할에 걸쳐 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="22598-114">사용자 및 역할에 대한 권한 설정에 대해 알아보려면 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22598-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="22598-115">리소스 관리자 잠금은 `https://management.azure.com`에 전송된 작업으로 구성되는 관리 수준에서 발생된 작업에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="22598-116">잠금은 리소스 자체 기능을 수행하는 방법을 제한하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="22598-117">리소스 변경은 제한되지만 리소스 작업은 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="22598-118">예를 들어 SQL Database에 대한 읽기 전용 잠금을 사용하면 데이터베이스를 삭제하거나 수정하지 못하지만, 데이터베이스에서 데이터를 만들기, 업데이트 또는 삭제하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="22598-119">이러한 작업이 `https://management.azure.com`로 전송되지 않기 때문에 데이터 전송이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="22598-120">**ReadOnly** 를 적용하면 읽기 작업처럼 보이는 일부 작업에 실제로 추가 작업이 필요하기 때문에 예기치 않은 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="22598-121">예를 들어 저장소 계정에 **ReadOnly** 잠금을 설정하면 모든 사용자가 키를 나열하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="22598-122">반환되는 키를 쓰기 작업에 사용할 수 있기 때문에 목록 키 작업은 POST 요청을 통해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="22598-123">또 다른 예로 앱 서비스 리소스에 **ReadOnly** 잠금을 설정하면 해당 상호 작용이 쓰기 액세스를 필요로 하기 때문에 Visual Studio 서버 탐색기가 리소스에 대한 파일을 표시하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="22598-124">조직에서 잠금을 만들거나 삭제할 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="22598-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="22598-125">관리 잠금을 만들거나 삭제하려면 `Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="22598-126">기본 제공 역할의 경우 **소유자** 및 **사용자 액세스 관리자**에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="22598-127">포털</span><span class="sxs-lookup"><span data-stu-id="22598-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="22598-128">템플릿</span><span class="sxs-lookup"><span data-stu-id="22598-128">Template</span></span>
<span data-ttu-id="22598-129">다음 예제에서는 저장소 계정에 대한 잠금을 만드는 템플릿을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22598-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="22598-130">잠금을 적용할 저장소 계정은 매개 변수로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22598-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="22598-131">잠금 이름은 리소스 이름을 **/Microsoft.Authorization/**과 연결하여 만들어집니다. 이 예제의 경우 잠금 이름은 **myLock**입니다.</span><span class="sxs-lookup"><span data-stu-id="22598-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="22598-132">제공된 형식은 리소스 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="22598-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="22598-133">저장소의 경우 형식을 "Microsoft.Storage/storageaccounts/providers/locks"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="22598-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22598-134">PowerShell</span></span>
<span data-ttu-id="22598-135">[New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) 명령을 사용하여 Azure PowerShell을 통해 배포된 리소스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="22598-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="22598-136">리소스를 잠그려면 리소스 이름, 리소스 종류 및 해당 리소스 그룹 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="22598-137">리소스 그룹을 잠그려면 해당 리소스 그룹의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="22598-138">잠금에 대한 정보를 가져오려면 [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="22598-139">구독의 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="22598-140">리소스에 대한 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="22598-141">리소스 그룹에 대한 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="22598-142">Azure PowerShell은 [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock)을 사용하여 잠금을 업데이트하고, [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock)을 사용하여 잠금을 삭제하는 등 잠금 작업을 위한 다른 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="22598-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="22598-143">Azure CLI</span></span>

<span data-ttu-id="22598-144">[az lock create](/cli/azure/lock#create) 명령을 사용하여 Azure CLI를 통해 배포된 리소스를 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="22598-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="22598-145">리소스를 잠그려면 리소스 이름, 리소스 종류 및 해당 리소스 그룹 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="22598-146">리소스 그룹을 잠그려면 해당 리소스 그룹의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="22598-147">잠금에 대한 정보를 가져오려면 [az lock list](/cli/azure/lock#list)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="22598-148">구독의 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="22598-149">리소스에 대한 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="22598-150">리소스 그룹에 대한 모든 잠금을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="22598-151">Azure CLI는 [az lock update](/cli/azure/lock#update)를 사용하여 잠금을 업데이트하고, [az lock delete](/cli/azure/lock#delete)를 사용하여 잠금을 삭제하는 등 잠금 작업을 위한 다른 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="22598-152">REST API</span><span class="sxs-lookup"><span data-stu-id="22598-152">REST API</span></span>
<span data-ttu-id="22598-153">[관리 잠금을 위한 REST API](https://docs.microsoft.com/rest/api/resources/managementlocks)를 사용하여 배포된 리소스를 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="22598-154">REST API를 사용하여 잠금을 만들고, 삭제하고, 기존 잠금에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="22598-155">잠금을 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="22598-156">범위는 구독, 리소스 그룹 또는 리소스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="22598-157">lock-name은 원하는 잠금 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="22598-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="22598-158">api-version에는 **2015-01-01**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="22598-159">요청에서 잠금에 대한 속성을 지정하는 JSON 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22598-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="22598-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22598-160">Next steps</span></span>
* <span data-ttu-id="22598-161">리소스 잠금 작업에 대한 자세한 내용은 [Azure 리소스 잠금](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="22598-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="22598-162">리소스를 논리적으로 구성하는 방법에 대한 자세한 내용은 [태그를 사용하여 리소스 구성](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="22598-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="22598-163">리소스가 존재하는 리소스 그룹을 변경하려면 [새 리소스 그룹으로 리소스 이동](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="22598-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="22598-164">사용자 지정된 정책을 사용하여 구독을 통해 제한 사항 및 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22598-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="22598-165">자세한 내용은 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22598-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="22598-166">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22598-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

