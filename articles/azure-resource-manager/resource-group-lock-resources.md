---
title: "Azure 리소스 tooprevent 변경 aaaLock | Microsoft Docs"
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="d8fa0-103">잠금 리소스 tooprevent 예기치 않은 변경 내용</span><span class="sxs-lookup"><span data-stu-id="d8fa0-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="d8fa0-104">관리자로 서에서 할 수 있습니다 toolock 구독, 리소스 그룹 또는 리소스 tooprevent 다른 사용자가 조직 실수로 삭제 하거나 중요 한 리소스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="d8fa0-105">너무 hello 잠금 수준을 설정할 수 있습니다**CanNotDelete** 또는 **ReadOnly**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="d8fa0-106">**CanNotDelete** 계속 권한이 있는 사용자가 읽고는 리소스를 수정할 수 있지만 hello 리소스를 삭제할 수는 없습니다 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="d8fa0-107">**읽기 전용** 권한이 있는 사용자는 리소스를 읽을 수는 있지만 hello 리소스를 업데이트 하거나 삭제할 수는 없습니다 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="d8fa0-108">이 잠금은 적용 하는 것은 hello에 의해 부여 된 사용자가 toohello 권한에 모든 권한 있는 비슷한 toorestricting **판독기** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="d8fa0-109">잠금을 적용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d8fa0-109">How locks are applied</span></span>

<span data-ttu-id="d8fa0-110">부모 범위에서 잠금을 적용 하면 해당 범위 내에서 모든 리소스 상속 hello 동일한 잠금.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="d8fa0-111">Hello 잠금 hello 부모에서 상속 하는 리소스도 나중에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="d8fa0-112">hello hello 상속에 가장 제한적인 잠금 우선 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="d8fa0-113">역할 기반 액세스 제어와 달리 모든 사용자 및 역할에서 관리 잠금 tooapply 제한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="d8fa0-114">사용자 및 역할에 대 한 사용 권한을 설정 하는 방법에 대 한 toolearn 참조 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="d8fa0-115">리소스 관리자 잠금을 적용 너무 전송 작업으로 구성 되는 hello 관리 평면에서 발생 하는 toooperations만`https://management.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="d8fa0-116">hello 잠금 리소스에서 자신의 기능을 수행 하는 방법을 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="d8fa0-117">리소스 변경은 제한되지만 리소스 작업은 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="d8fa0-118">예를 들어 SQL 데이터베이스에 대 한 읽기 전용 잠금을 못하도록 삭제 하거나 수정 하지만 hello 데이터베이스 때도 만들기, 업데이트 또는 hello 데이터베이스의에서 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="d8fa0-119">이러한 작업이 너무 보내지지 않기 때문에 데이터 트랜잭션이 허용 됩니다`https://management.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="d8fa0-120">적용 **ReadOnly** 처럼 보일 수도 있지만 일부 작업 읽기 작업에 추가 작업을 실제로 필요 하기 때문에 toounexpected 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="d8fa0-121">예를 들어 배치는 **ReadOnly** 저장소 계정에 대 한 잠금을 나열 hello 키의 모든 사용자가 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="d8fa0-122">키 작업 hello 키에 사용할 수 있는 반환 했기 때문에 POST 요청을 통해 처리 hello 목록 쓰기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="d8fa0-123">또 다른 예로, 배치는 **ReadOnly** 앱 서비스 리소스 수 없습니다 Visual Studio 서버 탐색기에서 상호 작용을 지 쓰기 권한이 필요 하기 때문에 hello 리소스에 대 한 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="d8fa0-124">조직에서 잠금을 만들거나 삭제할 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="d8fa0-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="d8fa0-125">관리 잠금 toocreate 또는 delete 권한이 너무`Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="d8fa0-126">Hello 기본 제공 역할 중만 **소유자** 및 **사용자 액세스 관리자에 게** 이러한 작업을 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="d8fa0-127">포털</span><span class="sxs-lookup"><span data-stu-id="d8fa0-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="d8fa0-128">템플릿</span><span class="sxs-lookup"><span data-stu-id="d8fa0-128">Template</span></span>
<span data-ttu-id="d8fa0-129">hello 다음 예제에서는 저장소 계정에 대 한 잠금을 만드는 템플릿을</span><span class="sxs-lookup"><span data-stu-id="d8fa0-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="d8fa0-130">hello 저장소 계정에는 tooapply hello 잠금은 매개 변수로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="d8fa0-131">hello hello 잠금의 이름을 연결 하 여 만듭니다 hello 리소스 이름의 **/Microsoft.Authorization/** hello 잠금의 이름을 경우 hello 및 **myLock**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="d8fa0-132">제공 된 hello 형식은 특정 toohello 리소스 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="d8fa0-133">저장소에 대 한 hello 유형 too"Microsoft.Storage/storageaccounts/providers/locks set"입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="d8fa0-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8fa0-134">PowerShell</span></span>
<span data-ttu-id="d8fa0-135">사용자 잠금 hello를 사용 하 여 Azure PowerShell을 사용 하 여 리소스를 배포 [새로 AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="d8fa0-136">toolock 리소스에 hello 리소스의 hello 이름, 해당 리소스 종류 및 해당 리소스 그룹 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="d8fa0-137">toolock 리소스 그룹에는 hello 리소스 그룹의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="d8fa0-138">잠금 사용 하는 방법에 대 한 정보 tooget [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="d8fa0-139">tooget 구독에서 모든 hello 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="d8fa0-140">tooget 리소스에 대 한 모든 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="d8fa0-141">tooget 리소스 그룹에 대 한 모든 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="d8fa0-142">Azure PowerShell 작업 잠금에 대 한와 같은 다른 명령에는 [집합 AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate 잠금 및 [제거 AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete 잠금 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="d8fa0-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d8fa0-143">Azure CLI</span></span>

<span data-ttu-id="d8fa0-144">사용자 잠금 hello를 사용 하 여 Azure CLI를 사용 하 여 리소스를 배포 [az 잠금을 만들](/cli/azure/lock#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="d8fa0-145">toolock 리소스에 hello 리소스의 hello 이름, 해당 리소스 종류 및 해당 리소스 그룹 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="d8fa0-146">toolock 리소스 그룹에는 hello 리소스 그룹의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="d8fa0-147">잠금 사용 하는 방법에 대 한 정보 tooget [az 잠금 목록](/cli/azure/lock#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="d8fa0-148">tooget 구독에서 모든 hello 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="d8fa0-149">tooget 리소스에 대 한 모든 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="d8fa0-150">tooget 리소스 그룹에 대 한 모든 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="d8fa0-151">Azure CLI 작업 잠금에 대 한와 같은 다른 명령의 제공 [az 잠금 업데이트](/cli/azure/lock#update) tooupdate 잠금 및 [az 잠금 삭제](/cli/azure/lock#delete) toodelete 잠금 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="d8fa0-152">REST API</span><span class="sxs-lookup"><span data-stu-id="d8fa0-152">REST API</span></span>
<span data-ttu-id="d8fa0-153">Hello 사용 하 여 배포 된 리소스를 잠글 수 [관리 잠금에 대 한 REST API](https://docs.microsoft.com/rest/api/resources/managementlocks)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="d8fa0-154">REST API hello toocreate 및 잠금 삭제 있으며 기존 잠금에 대 한 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="d8fa0-155">toocreate 잠금을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="d8fa0-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="d8fa0-156">구독, 리소스 그룹 또는 리소스 hello 범위 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d8fa0-157">hello 잠금 이름이 원하는 작업이 무엇이 든 toocall hello 잠금.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="d8fa0-158">api-version에는 **2015-01-01**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="d8fa0-159">Hello 요청 hello 잠금에 대 한 hello 속성을 지정 하는 JSON 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="d8fa0-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8fa0-160">Next steps</span></span>
* <span data-ttu-id="d8fa0-161">리소스 잠금 작업에 대한 자세한 내용은 [Azure 리소스 잠금](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="d8fa0-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="d8fa0-162">에서는 리소스를 논리적으로 구성 하는 방법에 대 한 toolearn 참조 [를 사용 하 여 태그 tooorganize 리소스](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="d8fa0-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="d8fa0-163">리소스 그룹 리소스에 있는 toochange 참조 [리소스 toonew 리소스 그룹 이동](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="d8fa0-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="d8fa0-164">사용자 지정된 정책을 사용하여 구독을 통해 제한 사항 및 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="d8fa0-165">자세한 내용은 참조 [toomanage 리소스 사용 정책 및 액세스 제어](resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="d8fa0-166">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8fa0-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

