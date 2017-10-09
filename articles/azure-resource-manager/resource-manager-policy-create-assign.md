---
title: "aaaAssign Azure 리소스 정책을 관리 하 고 | Microsoft Docs"
description: "설명 방법을 tooapply Azure 리소스 정책 toosubscriptions 및 리소스 그룹을 방법과 tooview 리소스 정책입니다."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="587cf-103">리소스 정책 할당 및 관리</span><span class="sxs-lookup"><span data-stu-id="587cf-103">Assign and manage resource policies</span></span>

<span data-ttu-id="587cf-104">정책을 tooimplement 이러한 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="587cf-105">요구 사항을 충족 하는 구독에 이미 있는 경우 정책 정의 등 Azure에서 제공 하는 기본 제공 정책 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="587cf-106">있는 경우 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="587cf-107">존재 하지 않는 경우 json을 hello 정책 규칙을 정의 하 고 구독에서 정책 정의으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="587cf-108">이 단계는 hello 정책 할당에 사용할 수는 있지만 hello 규칙 tooyour 구독 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="587cf-109">두 경우 모두에 대 한 hello 정책 tooa 범위 (예: 구독 또는 리소스 그룹)를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="587cf-110">hello 정책 hello 규칙이 이제 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="587cf-111">이 문서 hello 단계 toocreate 정책 정의 중점적으로 다루며 REST API, PowerShell 또는 Azure CLI를 통해 해당 정의 tooa 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="587cf-112">Toouse hello 포털 tooassign 정책, 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="587cf-113">이 문서 hello 정책 정의 만들기 위한 hello 구문에 중점을 두지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="587cf-114">정책 구문에 대한 정보는 [리소스 정책 개요](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="587cf-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="587cf-115">REST API</span><span class="sxs-lookup"><span data-stu-id="587cf-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="587cf-116">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="587cf-116">Create policy definition</span></span>

<span data-ttu-id="587cf-117">Hello로 정책을 만들 수 [정책 정의 대 한 REST API](/rest/api/resources/policydefinitions)합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="587cf-118">hello REST API toocreate를 사용 하면 정책 정의 삭제 하 고 기존 정의 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="587cf-119">toocreate 정책 정의 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="587cf-120">다음 예제 요청 본문 비슷한 toohello를 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-120">Include a request body similar toohello following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a><span data-ttu-id="587cf-121">정책 할당</span><span class="sxs-lookup"><span data-stu-id="587cf-121">Assign policy</span></span>

<span data-ttu-id="587cf-122">Hello 통해 원하는 hello 범위에서 hello 정책 정의 적용할 수 있습니다 [정책 할당에 대 한 REST API](/rest/api/resources/policyassignments)합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="587cf-123">hello REST API toocreate를 사용 하면 정책 할당을 삭제 하 고 기존 할당에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="587cf-124">toocreate 정책 할당을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="587cf-125">hello {정책 할당}은 hello 정책 할당의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="587cf-126">다음 예제 요청 본문 비슷한 toohello를 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-126">Include a request body similar toohello following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="587cf-127">정책 보기</span><span class="sxs-lookup"><span data-stu-id="587cf-127">View policy</span></span>
<span data-ttu-id="587cf-128">tooget 정책을 사용 하 여 hello [정책 정의 가져올](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="587cf-129">별칭 가져오기</span><span class="sxs-lookup"><span data-stu-id="587cf-129">Get aliases</span></span>
<span data-ttu-id="587cf-130">별칭 hello REST API를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="587cf-131">다음 예제는 hello 별칭의 정의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="587cf-132">여기에서 볼 수 있듯이 별칭은 속성 이름을 변경하는 경우에도 서로 다른 API 버전에 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="587cf-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="587cf-133">PowerShell</span></span>

<span data-ttu-id="587cf-134">Hello PowerShell 예제를 계속 하기 전에 있는지 확인 [hello 최신 버전을 설치](/powershell/azure/install-azurerm-ps) 의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="587cf-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="587cf-135">정책 매개 변수가 버전 3.6.0에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="587cf-136">이전 버전의 경우 hello 반환 하는 예제 오류 나타내는 hello 매개 변수를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="587cf-137">정책 정의 보기</span><span class="sxs-lookup"><span data-stu-id="587cf-137">View policy definitions</span></span>
<span data-ttu-id="587cf-138">구독을 사용 하 여 hello 뒤의 모든 정책 정의 명령 toosee 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="587cf-139">기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="587cf-140">각 정책 형식에 따라 hello에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-140">Each policy is returned in hello following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="587cf-141">계속 toocreate 정책 정의 하기 전에 hello 기본 제공 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="587cf-142">필요한 hello 제한을 적용 하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="587cf-143">대신, hello 기본 제공 정책 toohello 원하는 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="587cf-144">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="587cf-144">Create policy definition</span></span>
<span data-ttu-id="587cf-145">Hello를 사용 하 여 정책 정의 만들 수 있습니다 `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="587cf-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

<span data-ttu-id="587cf-146">hello 출력에 저장 됩니다는 `$definition` 정책 할당 하는 동안 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="587cf-147">JSON hello를 매개 변수로 지정 하는 대신 hello 정책 규칙이 포함 된 hello 경로 tooa.json 파일을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="587cf-148">hello 다음 예제에서는 만듭니다 매개 변수를 포함 하는 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-148">hello following example creates a policy definition that includes parameters:</span></span>

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="587cf-149">정책 할당</span><span class="sxs-lookup"><span data-stu-id="587cf-149">Assign policy</span></span>

<span data-ttu-id="587cf-150">Hello를 사용 하 여 원하는 hello 범위의 hello 정책을 적용 `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="587cf-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="587cf-151">다음 예제는 hello hello 정책 tooa 리소스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="587cf-152">tooassign 매개 변수를 요구 하는 정책 만들고이 값을 가진 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="587cf-153">hello 다음 예제에서는 기본 제공 정책을 검색 하 고 전달 매개 변수 값:</span><span class="sxs-lookup"><span data-stu-id="587cf-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="587cf-154">정책 할당 보기</span><span class="sxs-lookup"><span data-stu-id="587cf-154">View policy assignment</span></span>

<span data-ttu-id="587cf-155">tooget 특정 정책 할당을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="587cf-156">정책 정의 사용 하 여에 대 한 tooview hello 정책 규칙:</span><span class="sxs-lookup"><span data-stu-id="587cf-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="587cf-157">정책 할당 제거</span><span class="sxs-lookup"><span data-stu-id="587cf-157">Remove policy assignment</span></span> 

<span data-ttu-id="587cf-158">tooremove 정책 할당을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="587cf-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="587cf-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="587cf-160">정책 정의 보기</span><span class="sxs-lookup"><span data-stu-id="587cf-160">View policy definitions</span></span>
<span data-ttu-id="587cf-161">구독을 사용 하 여 hello 뒤의 모든 정책 정의 명령 toosee 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="587cf-162">기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="587cf-163">각 정책 형식에 따라 hello에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-163">Each policy is returned in hello following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

<span data-ttu-id="587cf-164">계속 toocreate 정책 정의 하기 전에 hello 기본 제공 정책을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="587cf-165">필요한 hello 제한을 적용 하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="587cf-166">대신, hello 기본 제공 정책 toohello 원하는 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="587cf-167">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="587cf-167">Create policy definition</span></span>

<span data-ttu-id="587cf-168">Hello 정책 정의 명령을 사용 하 여 Azure CLI를 사용 하 여 정책 정의 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="587cf-169">정책 할당</span><span class="sxs-lookup"><span data-stu-id="587cf-169">Assign policy</span></span>

<span data-ttu-id="587cf-170">Hello 정책 할당 명령을 사용 하 여 hello 정책 toohello 원하는 범위를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="587cf-171">다음 예제는 hello 정책 tooa 리소스 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="587cf-172">정책 할당 보기</span><span class="sxs-lookup"><span data-stu-id="587cf-172">View policy assignment</span></span>

<span data-ttu-id="587cf-173">정책 할당을 tooview hello 정책 할당 이름 및 hello 범위를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="587cf-174">정책 할당 제거</span><span class="sxs-lookup"><span data-stu-id="587cf-174">Remove policy assignment</span></span> 

<span data-ttu-id="587cf-175">tooremove 정책 할당을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="587cf-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="587cf-176">Next steps</span></span>
* <span data-ttu-id="587cf-177">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="587cf-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

