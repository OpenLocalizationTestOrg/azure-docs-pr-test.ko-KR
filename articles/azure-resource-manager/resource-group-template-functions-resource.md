---
title: "aaaAzure 리소스 관리자 템플릿 함수-리소스 | Microsoft Docs"
description: "리소스에 대 한 hello 함수 toouse Azure 리소스 관리자 템플릿 tooretrieve 값에 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="eab51-103">Azure Resource Manager 템플릿용 리소스 함수</span><span class="sxs-lookup"><span data-stu-id="eab51-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="eab51-104">리소스 관리자 리소스 값을 가져오고이 대 한 함수를 수행 하는 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="eab51-105">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="eab51-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="eab51-106">providers</span><span class="sxs-lookup"><span data-stu-id="eab51-106">providers</span></span>](#providers)
* [<span data-ttu-id="eab51-107">reference</span><span class="sxs-lookup"><span data-stu-id="eab51-107">reference</span></span>](#reference)
* [<span data-ttu-id="eab51-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="eab51-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="eab51-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="eab51-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="eab51-110">subscription</span><span class="sxs-lookup"><span data-stu-id="eab51-110">subscription</span></span>](#subscription)

<span data-ttu-id="eab51-111">매개 변수, 변수 또는 hello 현재 배포에서 tooget 값 참조 [배포 값 기능](resource-group-template-functions-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="eab51-112">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="eab51-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="eab51-113">반환 hello hello 목록 작업을 지 원하는 모든 리소스 종류에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="eab51-114">가장 많이 사용 hello `listKeys`합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="eab51-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="eab51-115">Parameters</span></span>

| <span data-ttu-id="eab51-116">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-116">Parameter</span></span> | <span data-ttu-id="eab51-117">필수</span><span class="sxs-lookup"><span data-stu-id="eab51-117">Required</span></span> | <span data-ttu-id="eab51-118">형식</span><span class="sxs-lookup"><span data-stu-id="eab51-118">Type</span></span> | <span data-ttu-id="eab51-119">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eab51-120">resourceName 또는 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="eab51-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="eab51-121">예</span><span class="sxs-lookup"><span data-stu-id="eab51-121">Yes</span></span> |<span data-ttu-id="eab51-122">string</span><span class="sxs-lookup"><span data-stu-id="eab51-122">string</span></span> |<span data-ttu-id="eab51-123">Hello 리소스에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="eab51-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="eab51-124">apiVersion</span></span> |<span data-ttu-id="eab51-125">예</span><span class="sxs-lookup"><span data-stu-id="eab51-125">Yes</span></span> |<span data-ttu-id="eab51-126">string</span><span class="sxs-lookup"><span data-stu-id="eab51-126">string</span></span> |<span data-ttu-id="eab51-127">리소스 런타임 상태의 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-127">API version of resource runtime state.</span></span> <span data-ttu-id="eab51-128">일반적으로 hello 형태로 **yyyy-월-일**합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eab51-129">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-129">Return value</span></span>

<span data-ttu-id="eab51-130">hello는 Listkey에서 개체에 hello 형식에 따라에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="eab51-131">다른 list 함수는 다른 반환 형식을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-131">Other list functions have different return formats.</span></span> <span data-ttu-id="eab51-132">함수의 toosee hello 형식 hello 예제 서식 파일에 나와 있는 것 처럼 것 hello 출력 섹션에 포함.</span><span class="sxs-lookup"><span data-stu-id="eab51-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="eab51-133">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-133">Remarks</span></span>

<span data-ttu-id="eab51-134">**list**로 시작하는 작업은 템플릿에서 함수로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="eab51-135">hello 사용할 수 있는 작업에는 뿐만 아니라 Listkey 하지만 같은 작업 `list`, `listAdminKeys`, 및 `listStatus`합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="eab51-136">그러나 사용할 수 없습니다 **목록** hello에 대 한 값을 필요로 하는 작업 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="eab51-137">예를 들어 hello [목록 계정 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) 작업 등의 요청 본문 매개 변수가 필요 *signedExpiry*이므로 템플릿 내에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="eab51-138">어떤 리소스 유형에 있는 list 작업 toodetermine, hello 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="eab51-139">보기 hello [REST API 작업](/rest/api/) 리소스 공급자 및 목록 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="eab51-140">예를 들어 저장소 계정이 있는 hello [Listkey 작업](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="eab51-141">사용 하 여 hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eab51-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="eab51-142">hello 다음 예제에서는 가져옵니다 모든 저장소 계정에 대 한 작업을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="eab51-143">다음 toofilter 목록 작업을만 hello Azure CLI 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="eab51-144">Hello 중 하나를 사용 하 여 hello 리소스 지정 [resourceId 함수](#resourceid), 또는 hello 형식 `{providerNamespace}/{resourceType}/{resourceName}`합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="eab51-145">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-145">Example</span></span>

<span data-ttu-id="eab51-146">hello 다음 예제에서는 hello의 저장소 계정에서 tooreturn hello 기본 및 보조 키 섹션을 출력 하는 방법</span><span class="sxs-lookup"><span data-stu-id="eab51-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="eab51-147">providers</span><span class="sxs-lookup"><span data-stu-id="eab51-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="eab51-148">리소스 공급자와 지원되는 리소스 유형에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="eab51-149">리소스 종류를 제공 하지 않으면 hello 함수 hello 리소스 공급자에 대 한 모든 지원 되는 hello 형식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="eab51-150">매개 변수</span><span class="sxs-lookup"><span data-stu-id="eab51-150">Parameters</span></span>

| <span data-ttu-id="eab51-151">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-151">Parameter</span></span> | <span data-ttu-id="eab51-152">필수</span><span class="sxs-lookup"><span data-stu-id="eab51-152">Required</span></span> | <span data-ttu-id="eab51-153">형식</span><span class="sxs-lookup"><span data-stu-id="eab51-153">Type</span></span> | <span data-ttu-id="eab51-154">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eab51-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="eab51-155">providerNamespace</span></span> |<span data-ttu-id="eab51-156">예</span><span class="sxs-lookup"><span data-stu-id="eab51-156">Yes</span></span> |<span data-ttu-id="eab51-157">string</span><span class="sxs-lookup"><span data-stu-id="eab51-157">string</span></span> |<span data-ttu-id="eab51-158">Hello 공급자의 Namespace</span><span class="sxs-lookup"><span data-stu-id="eab51-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="eab51-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="eab51-159">resourceType</span></span> |<span data-ttu-id="eab51-160">아니요</span><span class="sxs-lookup"><span data-stu-id="eab51-160">No</span></span> |<span data-ttu-id="eab51-161">string</span><span class="sxs-lookup"><span data-stu-id="eab51-161">string</span></span> |<span data-ttu-id="eab51-162">네임 스페이스를 지정 하는 hello 형식 hello 내에서 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eab51-163">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-163">Return value</span></span>

<span data-ttu-id="eab51-164">형식에 따라 hello에 각 지원 되는 형식 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="eab51-165">배열 정렬 hello 반환 값 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="eab51-166">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-166">Example</span></span>

<span data-ttu-id="eab51-167">다음 예제는 hello toouse 공급자 함수가 해당 확장을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="eab51-168">hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="eab51-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="eab51-169">reference</span><span class="sxs-lookup"><span data-stu-id="eab51-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="eab51-170">리소스의 런타임 상태를 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="eab51-171">매개 변수</span><span class="sxs-lookup"><span data-stu-id="eab51-171">Parameters</span></span>

| <span data-ttu-id="eab51-172">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-172">Parameter</span></span> | <span data-ttu-id="eab51-173">필수</span><span class="sxs-lookup"><span data-stu-id="eab51-173">Required</span></span> | <span data-ttu-id="eab51-174">형식</span><span class="sxs-lookup"><span data-stu-id="eab51-174">Type</span></span> | <span data-ttu-id="eab51-175">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eab51-176">resourceName 또는 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="eab51-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="eab51-177">예</span><span class="sxs-lookup"><span data-stu-id="eab51-177">Yes</span></span> |<span data-ttu-id="eab51-178">string</span><span class="sxs-lookup"><span data-stu-id="eab51-178">string</span></span> |<span data-ttu-id="eab51-179">리소스의 이름 또는 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="eab51-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="eab51-180">apiVersion</span></span> |<span data-ttu-id="eab51-181">아니요</span><span class="sxs-lookup"><span data-stu-id="eab51-181">No</span></span> |<span data-ttu-id="eab51-182">string</span><span class="sxs-lookup"><span data-stu-id="eab51-182">string</span></span> |<span data-ttu-id="eab51-183">API 버전의 hello 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-183">API version of hello specified resource.</span></span> <span data-ttu-id="eab51-184">같은 템플릿 내에서 hello 리소스 프로 비전 되지 않은 경우이 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="eab51-185">일반적으로 hello 형태로 **yyyy-월-일**합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eab51-186">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-186">Return value</span></span>

<span data-ttu-id="eab51-187">모든 리소스 종류는 함수를 참조 하는 hello에 대 한 다른 속성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="eab51-188">hello 함수는 단일, 미리 정의 된 형식을 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="eab51-189">리소스 유형에 대 한 toosee hello 속성 hello에 hello 개체 출력 섹션 hello 예제에 표시 된 대로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="eab51-190">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-190">Remarks</span></span>

<span data-ttu-id="eab51-191">함수를 참조 하는 hello 런타임 상태에서 해당 값을 파생 하 고 hello 변수 섹션에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="eab51-192">템플릿의 출력 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="eab51-193">함수를 참조 하는 hello를 사용 하 여 암시적으로 선언 같은 템플릿 내에서 참조 하는 hello 리소스 프로 비전 된 경우 리소스가 다른 리소스에 종속 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="eab51-194">Tooalso use hello dependsOn 속성이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="eab51-195">hello 함수 평가 되지 않습니다 완료할 때까지 hello 참조 리소스 배포.</span><span class="sxs-lookup"><span data-stu-id="eab51-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="eab51-196">toosee hello 속성 이름 및 값 리소스 유형에 대 한 hello 출력 섹션의 hello 개체를 반환 하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="eab51-197">해당 형식의 기존 리소스를 사용 하도록 설정한 경우 서식 파일에 새 리소스를 배포 하지 않고 hello 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="eab51-198">Hello를 사용 하는 일반적으로 **참조** tooreturn hello blob 끝점 URI 등의 개체 또는 정규화 된 도메인 이름에서 특정 값을 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="eab51-199">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-199">Example</span></span>

<span data-ttu-id="eab51-200">toodeploy 및 참조 hello 리소스 hello에 같은 템플릿을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="eab51-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="eab51-201">hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="eab51-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="eab51-202">hello 다음 예제에서는 참조이 서식 파일에 배포 되지 않은 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="eab51-203">hello 저장소 계정이 이미 hello 내에서 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="eab51-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="eab51-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="eab51-205">Hello 현재 리소스 그룹을 나타내는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="eab51-206">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-206">Return value</span></span>

<span data-ttu-id="eab51-207">개체는 형식에 따라 hello에 반환 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="eab51-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="eab51-208">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-208">Remarks</span></span>

<span data-ttu-id="eab51-209">Hello resourceGroup 함수의 일반적인 용도 hello의 toocreate 리소스 같은 hello 리소스 그룹 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="eab51-210">hello 다음 예제에서는 hello 리소스 그룹 위치 tooassign hello 위치 웹 사이트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="eab51-211">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-211">Example</span></span>

<span data-ttu-id="eab51-212">hello 다음 템플릿을 반환 hello 리소스 그룹의 hello 속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="eab51-213">hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="eab51-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="eab51-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="eab51-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="eab51-215">반환 hello 리소스의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="eab51-216">이 함수를 사용 하 여 hello 리소스 이름이 모호 하거나 hello 내에서 프로 비전 되지 않습니다 같은 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="eab51-217">매개 변수</span><span class="sxs-lookup"><span data-stu-id="eab51-217">Parameters</span></span>

| <span data-ttu-id="eab51-218">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-218">Parameter</span></span> | <span data-ttu-id="eab51-219">필수</span><span class="sxs-lookup"><span data-stu-id="eab51-219">Required</span></span> | <span data-ttu-id="eab51-220">형식</span><span class="sxs-lookup"><span data-stu-id="eab51-220">Type</span></span> | <span data-ttu-id="eab51-221">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="eab51-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="eab51-222">subscriptionId</span></span> |<span data-ttu-id="eab51-223">아니요</span><span class="sxs-lookup"><span data-stu-id="eab51-223">No</span></span> |<span data-ttu-id="eab51-224">문자열(GUID 형식)</span><span class="sxs-lookup"><span data-stu-id="eab51-224">string (In GUID format)</span></span> |<span data-ttu-id="eab51-225">기본값은 현재 구독 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-225">Default value is hello current subscription.</span></span> <span data-ttu-id="eab51-226">Tooretrieve 다른 구독에 리소스를 필요할 때이 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="eab51-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="eab51-227">resourceGroupName</span></span> |<span data-ttu-id="eab51-228">아니요</span><span class="sxs-lookup"><span data-stu-id="eab51-228">No</span></span> |<span data-ttu-id="eab51-229">string</span><span class="sxs-lookup"><span data-stu-id="eab51-229">string</span></span> |<span data-ttu-id="eab51-230">기본값은 현재 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-230">Default value is current resource group.</span></span> <span data-ttu-id="eab51-231">Tooretrieve 다른 리소스 그룹에 리소스를 필요할 때이 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="eab51-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="eab51-232">resourceType</span></span> |<span data-ttu-id="eab51-233">예</span><span class="sxs-lookup"><span data-stu-id="eab51-233">Yes</span></span> |<span data-ttu-id="eab51-234">string</span><span class="sxs-lookup"><span data-stu-id="eab51-234">string</span></span> |<span data-ttu-id="eab51-235">리소스 공급자 네임스페이스를 포함하는 리소스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="eab51-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="eab51-236">resourceName1</span></span> |<span data-ttu-id="eab51-237">예</span><span class="sxs-lookup"><span data-stu-id="eab51-237">Yes</span></span> |<span data-ttu-id="eab51-238">string</span><span class="sxs-lookup"><span data-stu-id="eab51-238">string</span></span> |<span data-ttu-id="eab51-239">리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-239">Name of resource.</span></span> |
| <span data-ttu-id="eab51-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="eab51-240">resourceName2</span></span> |<span data-ttu-id="eab51-241">아니요</span><span class="sxs-lookup"><span data-stu-id="eab51-241">No</span></span> |<span data-ttu-id="eab51-242">string</span><span class="sxs-lookup"><span data-stu-id="eab51-242">string</span></span> |<span data-ttu-id="eab51-243">리소스가 중첩된 경우 다음 리소스 이름 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="eab51-244">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-244">Return value</span></span>

<span data-ttu-id="eab51-245">hello 식별자 형식에 따라 hello에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="eab51-246">설명</span><span class="sxs-lookup"><span data-stu-id="eab51-246">Remarks</span></span>

<span data-ttu-id="eab51-247">hello 매개 변수 값 지정에 따라 달라 집니다 hello hello 리소스 인지 hello 현재 배포와 동일한 구독 및 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="eab51-248">tooget hello 리소스 ID가 hello의 저장소 계정에 대 한 같음 구독 및 리소스 그룹을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="eab51-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="eab51-249">저장소 계정에 대 한 tooget hello 리소스 ID에 동일한 구독 하지만 다른 리소스 그룹에서 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="eab51-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="eab51-250">다른 구독 및 리소스 그룹의 저장소 계정에 대 한 tooget hello 리소스 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="eab51-251">다른 리소스 그룹에 데이터베이스에 대 한 tooget hello 리소스 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="eab51-252">종종 해야 toouse이이 함수는 다른 리소스 그룹에 저장소 계정 또는 가상 네트워크를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="eab51-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="eab51-253">hello 다음 예제는 리소스는 외부 리소스 그룹에서 사용할 수 있는 방법을 쉽게.</span><span class="sxs-lookup"><span data-stu-id="eab51-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="eab51-254">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-254">Example</span></span>

<span data-ttu-id="eab51-255">hello 다음 예제에서는 hello 리소스 ID를 반환 저장소 계정에 대 한 hello 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="eab51-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="eab51-256">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="eab51-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="eab51-257">이름</span><span class="sxs-lookup"><span data-stu-id="eab51-257">Name</span></span> | <span data-ttu-id="eab51-258">형식</span><span class="sxs-lookup"><span data-stu-id="eab51-258">Type</span></span> | <span data-ttu-id="eab51-259">값</span><span class="sxs-lookup"><span data-stu-id="eab51-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="eab51-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="eab51-260">sameRGOutput</span></span> | <span data-ttu-id="eab51-261">문자열</span><span class="sxs-lookup"><span data-stu-id="eab51-261">String</span></span> | <span data-ttu-id="eab51-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="eab51-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="eab51-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="eab51-263">differentRGOutput</span></span> | <span data-ttu-id="eab51-264">문자열</span><span class="sxs-lookup"><span data-stu-id="eab51-264">String</span></span> | <span data-ttu-id="eab51-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="eab51-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="eab51-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="eab51-266">differentSubOutput</span></span> | <span data-ttu-id="eab51-267">문자열</span><span class="sxs-lookup"><span data-stu-id="eab51-267">String</span></span> | <span data-ttu-id="eab51-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="eab51-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="eab51-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="eab51-269">nestedResourceOutput</span></span> | <span data-ttu-id="eab51-270">문자열</span><span class="sxs-lookup"><span data-stu-id="eab51-270">String</span></span> | <span data-ttu-id="eab51-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="eab51-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="eab51-272">subscription</span><span class="sxs-lookup"><span data-stu-id="eab51-272">subscription</span></span>
`subscription()`

<span data-ttu-id="eab51-273">Hello 현재 배포에 대 한 hello 구독에 대 한 세부 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="eab51-274">반환 값</span><span class="sxs-lookup"><span data-stu-id="eab51-274">Return value</span></span>

<span data-ttu-id="eab51-275">hello 함수 형식에 따라 hello를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="eab51-276">예제</span><span class="sxs-lookup"><span data-stu-id="eab51-276">Example</span></span>

<span data-ttu-id="eab51-277">hello 다음 예제에서는 hello 출력 섹션에서 호출 하는 hello 구독 함수</span><span class="sxs-lookup"><span data-stu-id="eab51-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="eab51-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eab51-278">Next steps</span></span>
* <span data-ttu-id="eab51-279">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="eab51-280">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="eab51-281">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="eab51-282">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eab51-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

