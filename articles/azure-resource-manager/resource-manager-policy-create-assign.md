---
title: "Azure 리소스 정책 할당 및 관리 | Microsoft Docs"
description: "Azure 리소스 정책을 구독 및 리소스 그룹에 적용하고 리소스 정책을 확인하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="1043d-103">리소스 정책 할당 및 관리</span><span class="sxs-lookup"><span data-stu-id="1043d-103">Assign and manage resource policies</span></span>

<span data-ttu-id="1043d-104">정책을 구현하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="1043d-105">정책 정의(Azure에서 제공하는 기본 제공 정책 포함)에서 사용자의 요구 사항을 충족하는 정책이 구독에 이미 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="1043d-106">있는 경우 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="1043d-107">없는 경우 JSON으로 정책 규칙을 정의하고 사용자 구독에 정책 정의로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="1043d-108">이 단계를 사용하면 정책을 할당할 수 있지만 구독에 규칙을 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="1043d-109">어느 경우든, 정책을 범위(예: 구독 또는 리소스 그룹)에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="1043d-110">이제 정책의 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="1043d-111">이 문서에서는 REST API, PowerShell 또는 Azure CLI를 통해 정책 정의를 만들고 범위에 해당 정의를 할당하는 단계에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="1043d-112">포털을 사용해서 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1043d-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="1043d-113">이 문서에서 정책 정의를 만드는 구문은 집중적으로 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="1043d-114">정책 구문에 대한 정보는 [리소스 정책 개요](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1043d-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="1043d-115">REST API</span><span class="sxs-lookup"><span data-stu-id="1043d-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="1043d-116">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="1043d-116">Create policy definition</span></span>

<span data-ttu-id="1043d-117">[정책 정의에 대한 REST API](/rest/api/resources/policydefinitions)를 사용하여 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="1043d-118">REST API를 사용하여 정책 정의를 만들고, 삭제하고, 기존 정의에 관한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="1043d-119">정책 정의를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="1043d-120">다음 예제와 비슷한 요청 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="1043d-121">정책 할당</span><span class="sxs-lookup"><span data-stu-id="1043d-121">Assign policy</span></span>

<span data-ttu-id="1043d-122">[정책 할당에 대한 REST API](/rest/api/resources/policyassignments)를 통해 원하는 범위에 정책 정의를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="1043d-123">REST API를 사용하여 정책 할당을 만들고, 삭제하고, 기존 할당에 관한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="1043d-124">정책 할당을 만들려면 다음과 같이 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="1043d-125">{policy-assignment}는 정책 할당의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="1043d-126">다음 예제와 비슷한 요청 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="1043d-127">정책 보기</span><span class="sxs-lookup"><span data-stu-id="1043d-127">View policy</span></span>
<span data-ttu-id="1043d-128">정책을 가져오려면 [정책 정의 가져오기](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="1043d-129">별칭 가져오기</span><span class="sxs-lookup"><span data-stu-id="1043d-129">Get aliases</span></span>
<span data-ttu-id="1043d-130">REST API를 통해 별칭을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="1043d-131">다음 예제는 별칭의 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="1043d-132">여기에서 볼 수 있듯이 별칭은 속성 이름을 변경하는 경우에도 서로 다른 API 버전에 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="1043d-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1043d-133">PowerShell</span></span>

<span data-ttu-id="1043d-134">PowerShell 예제를 진행하기 전에 [최신 버전의 Azure PowerShell을 설치](/powershell/azure/install-azurerm-ps)했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="1043d-135">정책 매개 변수가 버전 3.6.0에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="1043d-136">이전 버전이 있는 경우 예제에서는 매개 변수를 찾을 수 없음을 나타내는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="1043d-137">정책 정의 보기</span><span class="sxs-lookup"><span data-stu-id="1043d-137">View policy definitions</span></span>
<span data-ttu-id="1043d-138">구독에서 모든 정책 정의를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="1043d-139">기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="1043d-140">각 정책은 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="1043d-141">정책 정의 만들기를 진행하기 전에 기본 제공 정책을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="1043d-142">필요한 한도를 적용하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="1043d-143">대신, 기본 제공 정책을 원하는 범위에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="1043d-144">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="1043d-144">Create policy definition</span></span>
<span data-ttu-id="1043d-145">`New-AzureRmPolicyDefinition` cmdlet을 사용하여 정책 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="1043d-146">출력 `$definition` 개체에 저장되어 정책 할당 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="1043d-147">JSON을 매개 변수로 지정하지 않고 정책 규칙을 포함하는 .json 파일의 경로를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="1043d-148">다음 예제에서는 매개 변수를 포함하는 정책 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="1043d-149">정책 할당</span><span class="sxs-lookup"><span data-stu-id="1043d-149">Assign policy</span></span>

<span data-ttu-id="1043d-150">`New-AzureRmPolicyAssignment` cmdlet을 사용하여 원하는 범위에서 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="1043d-151">다음 예제에서는 리소스 그룹에 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="1043d-152">매개 변수를 요구하는 정책을 할당하려면 해당 값으로 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="1043d-153">다음 예제에서는 기본 제공 정책을 검색하고 매개 변수 값에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="1043d-154">정책 할당 보기</span><span class="sxs-lookup"><span data-stu-id="1043d-154">View policy assignment</span></span>

<span data-ttu-id="1043d-155">특정 정책 할당을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="1043d-156">정책 정의에 대한 정책 규칙을 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="1043d-157">정책 할당 제거</span><span class="sxs-lookup"><span data-stu-id="1043d-157">Remove policy assignment</span></span> 

<span data-ttu-id="1043d-158">정책 할당을 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="1043d-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1043d-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="1043d-160">정책 정의 보기</span><span class="sxs-lookup"><span data-stu-id="1043d-160">View policy definitions</span></span>
<span data-ttu-id="1043d-161">구독에서 모든 정책 정의를 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="1043d-162">기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="1043d-163">각 정책은 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="1043d-164">정책 정의 만들기를 진행하기 전에 기본 제공 정책을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="1043d-165">필요한 한도를 적용하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="1043d-166">대신, 기본 제공 정책을 원하는 범위에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="1043d-167">정책 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="1043d-167">Create policy definition</span></span>

<span data-ttu-id="1043d-168">정책 정의 명령과 함께 Azure CLI를 사용하여 정책 정의를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="1043d-169">정책 할당</span><span class="sxs-lookup"><span data-stu-id="1043d-169">Assign policy</span></span>

<span data-ttu-id="1043d-170">정책 할당 명령을 사용하여 정책을 원하는 범위에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="1043d-171">다음 예제에서는 리소스 그룹에 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="1043d-172">정책 할당 보기</span><span class="sxs-lookup"><span data-stu-id="1043d-172">View policy assignment</span></span>

<span data-ttu-id="1043d-173">정책 할당을 보려면 정책 할당 이름 및 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="1043d-174">정책 할당 제거</span><span class="sxs-lookup"><span data-stu-id="1043d-174">Remove policy assignment</span></span> 

<span data-ttu-id="1043d-175">정책 할당을 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1043d-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="1043d-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1043d-176">Next steps</span></span>
* <span data-ttu-id="1043d-177">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1043d-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

