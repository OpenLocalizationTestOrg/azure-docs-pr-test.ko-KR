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
# <a name="assign-and-manage-resource-policies"></a>리소스 정책 할당 및 관리

정책을 tooimplement 이러한 단계를 수행 해야 합니다.

1. 요구 사항을 충족 하는 구독에 이미 있는 경우 정책 정의 등 Azure에서 제공 하는 기본 제공 정책 toosee를 확인 합니다.
2. 있는 경우 이름을 가져옵니다.
3. 존재 하지 않는 경우 json을 hello 정책 규칙을 정의 하 고 구독에서 정책 정의으로 추가 합니다. 이 단계는 hello 정책 할당에 사용할 수는 있지만 hello 규칙 tooyour 구독 적용 되지 않습니다.
4. 두 경우 모두에 대 한 hello 정책 tooa 범위 (예: 구독 또는 리소스 그룹)를 할당 합니다. hello 정책 hello 규칙이 이제 적용 됩니다.

이 문서 hello 단계 toocreate 정책 정의 중점적으로 다루며 REST API, PowerShell 또는 Azure CLI를 통해 해당 정의 tooa 범위를 할당 합니다. Toouse hello 포털 tooassign 정책, 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. 이 문서 hello 정책 정의 만들기 위한 hello 구문에 중점을 두지 않습니다. 정책 구문에 대한 정보는 [리소스 정책 개요](resource-manager-policy.md)를 참조하세요.

## <a name="rest-api"></a>REST API

### <a name="create-policy-definition"></a>정책 정의 만들기

Hello로 정책을 만들 수 [정책 정의 대 한 REST API](/rest/api/resources/policydefinitions)합니다. hello REST API toocreate를 사용 하면 정책 정의 삭제 하 고 기존 정의 대 한 정보입니다.

toocreate 정책 정의 실행 합니다.

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

다음 예제 요청 본문 비슷한 toohello를 다음과 같습니다.

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

### <a name="assign-policy"></a>정책 할당

Hello 통해 원하는 hello 범위에서 hello 정책 정의 적용할 수 있습니다 [정책 할당에 대 한 REST API](/rest/api/resources/policyassignments)합니다. hello REST API toocreate를 사용 하면 정책 할당을 삭제 하 고 기존 할당에 대 한 정보입니다.

toocreate 정책 할당을 실행 합니다.

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

hello {정책 할당}은 hello 정책 할당의 hello 이름입니다.

다음 예제 요청 본문 비슷한 toohello를 다음과 같습니다.

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

### <a name="view-policy"></a>정책 보기
tooget 정책을 사용 하 여 hello [정책 정의 가져올](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) 작업 합니다.

### <a name="get-aliases"></a>별칭 가져오기
별칭 hello REST API를 통해 검색할 수 있습니다.

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

다음 예제는 hello 별칭의 정의 보여 줍니다. 여기에서 볼 수 있듯이 별칭은 속성 이름을 변경하는 경우에도 서로 다른 API 버전에 경로를 정의합니다. 

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

## <a name="powershell"></a>PowerShell

Hello PowerShell 예제를 계속 하기 전에 있는지 확인 [hello 최신 버전을 설치](/powershell/azure/install-azurerm-ps) 의 Azure PowerShell. 정책 매개 변수가 버전 3.6.0에 추가되었습니다. 이전 버전의 경우 hello 반환 하는 예제 오류 나타내는 hello 매개 변수를 찾을 수 없습니다.

### <a name="view-policy-definitions"></a>정책 정의 보기
구독을 사용 하 여 hello 뒤의 모든 정책 정의 명령 toosee 있습니다.

```powershell
Get-AzureRmPolicyDefinition
```

기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다. 각 정책 형식에 따라 hello에 반환 됩니다.

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

계속 toocreate 정책 정의 하기 전에 hello 기본 제공 정책을 확인 합니다. 필요한 hello 제한을 적용 하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다. 대신, hello 기본 제공 정책 toohello 원하는 범위를 할당 합니다.

### <a name="create-policy-definition"></a>정책 정의 만들기
Hello를 사용 하 여 정책 정의 만들 수 있습니다 `New-AzureRmPolicyDefinition` cmdlet.

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

hello 출력에 저장 됩니다는 `$definition` 정책 할당 하는 동안 사용 되는 개체입니다. 

JSON hello를 매개 변수로 지정 하는 대신 hello 정책 규칙이 포함 된 hello 경로 tooa.json 파일을 제공할 수 있습니다.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

hello 다음 예제에서는 만듭니다 매개 변수를 포함 하는 정책을 정의 합니다.

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

### <a name="assign-policy"></a>정책 할당

Hello를 사용 하 여 원하는 hello 범위의 hello 정책을 적용 `New-AzureRmPolicyAssignment` cmdlet. 다음 예제는 hello hello 정책 tooa 리소스 그룹에 할당 합니다.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign 매개 변수를 요구 하는 정책 만들고이 값을 가진 개체입니다. hello 다음 예제에서는 기본 제공 정책을 검색 하 고 전달 매개 변수 값:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>정책 할당 보기

tooget 특정 정책 할당을 사용 합니다.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

정책 정의 사용 하 여에 대 한 tooview hello 정책 규칙:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>정책 할당 제거 

tooremove 정책 할당을 사용 합니다.

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Azure CLI

### <a name="view-policy-definitions"></a>정책 정의 보기
구독을 사용 하 여 hello 뒤의 모든 정책 정의 명령 toosee 있습니다.

```azurecli
az policy definition list
```

기본 제공 정책을 비롯한 사용 가능한 모든 정책 정의를 반환합니다. 각 정책 형식에 따라 hello에 반환 됩니다.

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

계속 toocreate 정책 정의 하기 전에 hello 기본 제공 정책을 확인 합니다. 필요한 hello 제한을 적용 하는 기본 제공 정책을 찾을 경우 정책 정의 만들기를 건너뛸 수 있습니다. 대신, hello 기본 제공 정책 toohello 원하는 범위를 할당 합니다.

### <a name="create-policy-definition"></a>정책 정의 만들기

Hello 정책 정의 명령을 사용 하 여 Azure CLI를 사용 하 여 정책 정의 만들 수 있습니다.

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

### <a name="assign-policy"></a>정책 할당

Hello 정책 할당 명령을 사용 하 여 hello 정책 toohello 원하는 범위를 적용할 수 있습니다. 다음 예제는 hello 정책 tooa 리소스 그룹에 할당 합니다.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>정책 할당 보기

정책 할당을 tooview hello 정책 할당 이름 및 hello 범위를 제공 합니다.

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>정책 할당 제거 

tooremove 정책 할당을 사용 합니다.

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>다음 단계
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

