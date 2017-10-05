---
title: "Azure Resource Manager 템플릿 함수 - 리소스 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 리소스에 대한 값을 검색하는 데 사용할 수 있는 함수에 대해 설명합니다."
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
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="91a8d-103">Azure Resource Manager 템플릿용 리소스 함수</span><span class="sxs-lookup"><span data-stu-id="91a8d-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="91a8d-104">Resource Manager는 리소스 값을 가져오기 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="91a8d-105">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="91a8d-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="91a8d-106">providers</span><span class="sxs-lookup"><span data-stu-id="91a8d-106">providers</span></span>](#providers)
* [<span data-ttu-id="91a8d-107">reference</span><span class="sxs-lookup"><span data-stu-id="91a8d-107">reference</span></span>](#reference)
* [<span data-ttu-id="91a8d-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="91a8d-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="91a8d-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="91a8d-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="91a8d-110">subscription</span><span class="sxs-lookup"><span data-stu-id="91a8d-110">subscription</span></span>](#subscription)

<span data-ttu-id="91a8d-111">매개 변수, 변수 또는 현재 배포에서 값을 가져오려면 [배포 값 함수](resource-group-template-functions-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a8d-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="91a8d-112">listKeys 및 list{Value}</span><span class="sxs-lookup"><span data-stu-id="91a8d-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="91a8d-113">list 작업을 지원하는 모든 리소스 형식에 대한 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="91a8d-114">가장 일반적인 사용법은 `listKeys`입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="91a8d-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91a8d-115">Parameters</span></span>

| <span data-ttu-id="91a8d-116">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-116">Parameter</span></span> | <span data-ttu-id="91a8d-117">필수</span><span class="sxs-lookup"><span data-stu-id="91a8d-117">Required</span></span> | <span data-ttu-id="91a8d-118">형식</span><span class="sxs-lookup"><span data-stu-id="91a8d-118">Type</span></span> | <span data-ttu-id="91a8d-119">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91a8d-120">resourceName 또는 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="91a8d-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="91a8d-121">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-121">Yes</span></span> |<span data-ttu-id="91a8d-122">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-122">string</span></span> |<span data-ttu-id="91a8d-123">리소스에 대한 고유 식별자.</span><span class="sxs-lookup"><span data-stu-id="91a8d-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="91a8d-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="91a8d-124">apiVersion</span></span> |<span data-ttu-id="91a8d-125">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-125">Yes</span></span> |<span data-ttu-id="91a8d-126">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-126">string</span></span> |<span data-ttu-id="91a8d-127">리소스 런타임 상태의 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-127">API version of resource runtime state.</span></span> <span data-ttu-id="91a8d-128">일반적으로 **yyyy-mm-dd** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="91a8d-129">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-129">Return value</span></span>

<span data-ttu-id="91a8d-130">listKeys에서 반환된 개체는 다음 형식을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-130">The returned object from listKeys has the following format:</span></span>

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

<span data-ttu-id="91a8d-131">다른 list 함수는 다른 반환 형식을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-131">Other list functions have different return formats.</span></span> <span data-ttu-id="91a8d-132">함수의 형식을 보려면 예제 템플릿에 표시된 것처럼 outputs 섹션에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="91a8d-133">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-133">Remarks</span></span>

<span data-ttu-id="91a8d-134">**list**로 시작하는 작업은 템플릿에서 함수로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="91a8d-135">사용 가능한 작업에는 listKeys 뿐만 아니라 `list`, `listAdminKeys`, `listStatus`와 같은 작업도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="91a8d-136">그러나 요청 본문에 있는 값을 필요로 하는 **나열** 작업을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="91a8d-137">예를 들어 [나열 계정 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) 작업은 *signedExpiry* 등의 요청 본문 매개 변수가 필요하므로 템플릿 내에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="91a8d-138">list 작업이 있는 리소스 유형을 확인할 수 있게 다음 PowerShell 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="91a8d-139">리소스 공급자에 대한 [REST API 작업](/rest/api/)을 보고 list 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="91a8d-140">예를 들어 저장소 계정에는 [listKeys 작업](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="91a8d-141">[Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="91a8d-142">다음 예제에서는 저장소 계정에 대한 모든 list 작업을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="91a8d-143">다음 Azure CLI 명령을 사용하여 목록 작업만 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="91a8d-144">[resourceId 함수](#resourceid) 또는 형식 `{providerNamespace}/{resourceType}/{resourceName}`을 사용하여 리소스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="91a8d-145">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-145">Example</span></span>

<span data-ttu-id="91a8d-146">다음 예에서는 출력 섹션의 저장소 계정에서 기본 및 보조 키를 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="91a8d-147">providers</span><span class="sxs-lookup"><span data-stu-id="91a8d-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="91a8d-148">리소스 공급자와 지원되는 리소스 유형에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="91a8d-149">리소스 유형을 제공하지 않는 경우 함수는 리소스 공급자에 대한 모든 지원되는 유형을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="91a8d-150">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91a8d-150">Parameters</span></span>

| <span data-ttu-id="91a8d-151">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-151">Parameter</span></span> | <span data-ttu-id="91a8d-152">필수</span><span class="sxs-lookup"><span data-stu-id="91a8d-152">Required</span></span> | <span data-ttu-id="91a8d-153">형식</span><span class="sxs-lookup"><span data-stu-id="91a8d-153">Type</span></span> | <span data-ttu-id="91a8d-154">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91a8d-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="91a8d-155">providerNamespace</span></span> |<span data-ttu-id="91a8d-156">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-156">Yes</span></span> |<span data-ttu-id="91a8d-157">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-157">string</span></span> |<span data-ttu-id="91a8d-158">공급자의 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-158">Namespace of the provider</span></span> |
| <span data-ttu-id="91a8d-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="91a8d-159">resourceType</span></span> |<span data-ttu-id="91a8d-160">아니요</span><span class="sxs-lookup"><span data-stu-id="91a8d-160">No</span></span> |<span data-ttu-id="91a8d-161">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-161">string</span></span> |<span data-ttu-id="91a8d-162">지정된 네임스페이스 내의 리소스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="91a8d-163">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-163">Return value</span></span>

<span data-ttu-id="91a8d-164">각 지원되는 형식이 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="91a8d-165">반환된 값의 배열 순서는 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="91a8d-166">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-166">Example</span></span>

<span data-ttu-id="91a8d-167">다음 예에서는 공급자 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-167">The following example shows how to use the provider function:</span></span>

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

<span data-ttu-id="91a8d-168">앞의 예제는 다음과 같은 형식의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-168">The preceding example returns an object in the following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="91a8d-169">reference</span><span class="sxs-lookup"><span data-stu-id="91a8d-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="91a8d-170">리소스의 런타임 상태를 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="91a8d-171">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91a8d-171">Parameters</span></span>

| <span data-ttu-id="91a8d-172">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-172">Parameter</span></span> | <span data-ttu-id="91a8d-173">필수</span><span class="sxs-lookup"><span data-stu-id="91a8d-173">Required</span></span> | <span data-ttu-id="91a8d-174">형식</span><span class="sxs-lookup"><span data-stu-id="91a8d-174">Type</span></span> | <span data-ttu-id="91a8d-175">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91a8d-176">resourceName 또는 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="91a8d-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="91a8d-177">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-177">Yes</span></span> |<span data-ttu-id="91a8d-178">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-178">string</span></span> |<span data-ttu-id="91a8d-179">리소스의 이름 또는 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="91a8d-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="91a8d-180">apiVersion</span></span> |<span data-ttu-id="91a8d-181">아니요</span><span class="sxs-lookup"><span data-stu-id="91a8d-181">No</span></span> |<span data-ttu-id="91a8d-182">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-182">string</span></span> |<span data-ttu-id="91a8d-183">지정된 리소스의 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-183">API version of the specified resource.</span></span> <span data-ttu-id="91a8d-184">리소스가 동일한 템플릿 내에서 프로비전되지 않은 경우 이 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="91a8d-185">일반적으로 **yyyy-mm-dd** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="91a8d-186">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-186">Return value</span></span>

<span data-ttu-id="91a8d-187">모든 리소스 형식은 reference 함수에 대해 다른 속성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="91a8d-188">이 함수는 미리 정의된 단일 형식을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="91a8d-189">리소스 형식에 대한 속성을 보려면 예제와 같이 outputs 섹션의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="91a8d-190">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-190">Remarks</span></span>

<span data-ttu-id="91a8d-191">reference 함수는 런타임 상태에서 값을 파생하므로 변수 섹션에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="91a8d-192">템플릿의 출력 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="91a8d-193">참조 함수를 사용하여 참조되는 리소스가 동일한 템플릿 내에서 프로비전되는 경우 한 리소스가 다른 리소스에 종속되도록 암시적으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="91a8d-194">또한 dependsOn 속성도 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="91a8d-195">참조 리소스가 배포를 완료할 때까지 함수는 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="91a8d-196">리소스 유형에 대한 속성 이름 및 값을 보려면 outputs 섹션에서 개체를 반환하는 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="91a8d-197">해당 유형의 기존 리소스가 있는 경우 템플릿은 새로운 리소스를 배포하지 않고 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="91a8d-198">일반적으로 **reference** 함수를 사용하여 blob 끝점 URI 또는 정규화된 도메인 이름과 같은 개체의 특정 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="91a8d-199">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-199">Example</span></span>

<span data-ttu-id="91a8d-200">동일한 템플릿에서 리소스를 배포하고 참조하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-200">To deploy and reference the resource in the same template, use:</span></span>

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

<span data-ttu-id="91a8d-201">앞의 예제는 다음과 같은 형식의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-201">The preceding example returns an object in the following format:</span></span>

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

<span data-ttu-id="91a8d-202">다음 예제는 이 템플릿에 배포되지 않는 저장소 계정을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="91a8d-203">저장소 계정은 동일한 리소스 그룹 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-203">The storage account already exists within the same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="91a8d-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="91a8d-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="91a8d-205">현재 리소스 그룹을 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="91a8d-206">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-206">Return value</span></span>

<span data-ttu-id="91a8d-207">반환된 개체는 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-207">The returned object is in the following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="91a8d-208">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-208">Remarks</span></span>

<span data-ttu-id="91a8d-209">resourceGroup 함수는 일반적으로 리소스 그룹과 동일한 위치에 리소스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="91a8d-210">다음 예에서는 리소스 그룹 위치를 사용하여 웹 사이트에 대한 위치를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-210">The following example uses the resource group location to assign the location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="91a8d-211">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-211">Example</span></span>

<span data-ttu-id="91a8d-212">다음 템플릿은 리소스 그룹의 속성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-212">The following template returns the properties of the resource group.</span></span>

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

<span data-ttu-id="91a8d-213">앞의 예제는 다음과 같은 형식의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-213">The preceding example returns an object in the following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="91a8d-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="91a8d-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="91a8d-215">리소스의 고유 식별자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="91a8d-216">리소스 이름이 모호하거나 동일한 템플릿 내에서 프로비전되지 않은 경우 이 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="91a8d-217">매개 변수</span><span class="sxs-lookup"><span data-stu-id="91a8d-217">Parameters</span></span>

| <span data-ttu-id="91a8d-218">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-218">Parameter</span></span> | <span data-ttu-id="91a8d-219">필수</span><span class="sxs-lookup"><span data-stu-id="91a8d-219">Required</span></span> | <span data-ttu-id="91a8d-220">형식</span><span class="sxs-lookup"><span data-stu-id="91a8d-220">Type</span></span> | <span data-ttu-id="91a8d-221">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="91a8d-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="91a8d-222">subscriptionId</span></span> |<span data-ttu-id="91a8d-223">아니요</span><span class="sxs-lookup"><span data-stu-id="91a8d-223">No</span></span> |<span data-ttu-id="91a8d-224">문자열(GUID 형식)</span><span class="sxs-lookup"><span data-stu-id="91a8d-224">string (In GUID format)</span></span> |<span data-ttu-id="91a8d-225">기본값은 현재 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-225">Default value is the current subscription.</span></span> <span data-ttu-id="91a8d-226">다른 구독에서 리소스를 검색해야 하는 경우 이 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="91a8d-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="91a8d-227">resourceGroupName</span></span> |<span data-ttu-id="91a8d-228">아니요</span><span class="sxs-lookup"><span data-stu-id="91a8d-228">No</span></span> |<span data-ttu-id="91a8d-229">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-229">string</span></span> |<span data-ttu-id="91a8d-230">기본값은 현재 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-230">Default value is current resource group.</span></span> <span data-ttu-id="91a8d-231">다른 리소스 그룹에서 리소스를 검색해야 하는 경우 이 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="91a8d-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="91a8d-232">resourceType</span></span> |<span data-ttu-id="91a8d-233">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-233">Yes</span></span> |<span data-ttu-id="91a8d-234">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-234">string</span></span> |<span data-ttu-id="91a8d-235">리소스 공급자 네임스페이스를 포함하는 리소스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="91a8d-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="91a8d-236">resourceName1</span></span> |<span data-ttu-id="91a8d-237">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-237">Yes</span></span> |<span data-ttu-id="91a8d-238">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-238">string</span></span> |<span data-ttu-id="91a8d-239">리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-239">Name of resource.</span></span> |
| <span data-ttu-id="91a8d-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="91a8d-240">resourceName2</span></span> |<span data-ttu-id="91a8d-241">아니요</span><span class="sxs-lookup"><span data-stu-id="91a8d-241">No</span></span> |<span data-ttu-id="91a8d-242">string</span><span class="sxs-lookup"><span data-stu-id="91a8d-242">string</span></span> |<span data-ttu-id="91a8d-243">리소스가 중첩된 경우 다음 리소스 이름 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="91a8d-244">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-244">Return value</span></span>

<span data-ttu-id="91a8d-245">식별자는 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="91a8d-246">설명</span><span class="sxs-lookup"><span data-stu-id="91a8d-246">Remarks</span></span>

<span data-ttu-id="91a8d-247">사용자가 지정한 매개 변수 값은 리소스가 현재 배포와 동일한 구독 및 리소스 그룹에 있는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="91a8d-248">동일한 구독 및 리소스 그룹의 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="91a8d-249">구독은 동일하지만 리소스 그룹은 다른 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="91a8d-250">다른 구독 및 리소스 그룹의 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="91a8d-251">다른 리소스 그룹의 데이터베이스에 대한 리소스 ID를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="91a8d-252">대체 리소스 그룹의 저장소 계정 또는 가상 네트워크를 사용할 경우 이 함수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="91a8d-253">다음 예에서는 외부 리소스 그룹의 리소스를 쉽게 사용할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="91a8d-254">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-254">Example</span></span>

<span data-ttu-id="91a8d-255">다음 예제에서는 리소스 그룹의 저장소 계정에 대한 리소스 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

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

<span data-ttu-id="91a8d-256">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="91a8d-257">이름</span><span class="sxs-lookup"><span data-stu-id="91a8d-257">Name</span></span> | <span data-ttu-id="91a8d-258">형식</span><span class="sxs-lookup"><span data-stu-id="91a8d-258">Type</span></span> | <span data-ttu-id="91a8d-259">값</span><span class="sxs-lookup"><span data-stu-id="91a8d-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="91a8d-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="91a8d-260">sameRGOutput</span></span> | <span data-ttu-id="91a8d-261">문자열</span><span class="sxs-lookup"><span data-stu-id="91a8d-261">String</span></span> | <span data-ttu-id="91a8d-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="91a8d-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="91a8d-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="91a8d-263">differentRGOutput</span></span> | <span data-ttu-id="91a8d-264">문자열</span><span class="sxs-lookup"><span data-stu-id="91a8d-264">String</span></span> | <span data-ttu-id="91a8d-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="91a8d-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="91a8d-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="91a8d-266">differentSubOutput</span></span> | <span data-ttu-id="91a8d-267">문자열</span><span class="sxs-lookup"><span data-stu-id="91a8d-267">String</span></span> | <span data-ttu-id="91a8d-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="91a8d-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="91a8d-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="91a8d-269">nestedResourceOutput</span></span> | <span data-ttu-id="91a8d-270">문자열</span><span class="sxs-lookup"><span data-stu-id="91a8d-270">String</span></span> | <span data-ttu-id="91a8d-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="91a8d-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="91a8d-272">subscription</span><span class="sxs-lookup"><span data-stu-id="91a8d-272">subscription</span></span>
`subscription()`

<span data-ttu-id="91a8d-273">현재 배포에 대한 구독 관련 세부 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="91a8d-274">반환 값</span><span class="sxs-lookup"><span data-stu-id="91a8d-274">Return value</span></span>

<span data-ttu-id="91a8d-275">이 함수는 다음 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="91a8d-276">예</span><span class="sxs-lookup"><span data-stu-id="91a8d-276">Example</span></span>

<span data-ttu-id="91a8d-277">다음 예에서는 출력 섹션에서 호출되는 구독 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91a8d-277">The following example shows the subscription function called in the outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="91a8d-278">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91a8d-278">Next steps</span></span>
* <span data-ttu-id="91a8d-279">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a8d-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="91a8d-280">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a8d-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="91a8d-281">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a8d-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="91a8d-282">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91a8d-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

