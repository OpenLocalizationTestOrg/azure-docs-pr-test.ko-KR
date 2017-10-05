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
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 리소스 함수

Resource Manager는 리소스 값을 가져오기 위한 다음 함수를 제공합니다.

* [listKeys 및 list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

매개 변수, 변수 또는 현재 배포에서 값을 가져오려면 [배포 값 함수](resource-group-template-functions-deployment.md)를 참조하세요.

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys 및 list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

list 작업을 지원하는 모든 리소스 형식에 대한 값을 반환합니다. 가장 일반적인 사용법은 `listKeys`입니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| resourceName 또는 resourceIdentifier |예 |string |리소스에 대한 고유 식별자. |
| apiVersion |예 |string |리소스 런타임 상태의 API 버전입니다. 일반적으로 **yyyy-mm-dd** 형식입니다. |

### <a name="return-value"></a>반환 값

listKeys에서 반환된 개체는 다음 형식을 가집니다.

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

다른 list 함수는 다른 반환 형식을 갖습니다. 함수의 형식을 보려면 예제 템플릿에 표시된 것처럼 outputs 섹션에 포함합니다. 

### <a name="remarks"></a>설명

**list**로 시작하는 작업은 템플릿에서 함수로 사용됩니다. 사용 가능한 작업에는 listKeys 뿐만 아니라 `list`, `listAdminKeys`, `listStatus`와 같은 작업도 포함됩니다. 그러나 요청 본문에 있는 값을 필요로 하는 **나열** 작업을 사용할 수 없습니다. 예를 들어 [나열 계정 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) 작업은 *signedExpiry* 등의 요청 본문 매개 변수가 필요하므로 템플릿 내에서 사용할 수 없습니다.

list 작업이 있는 리소스 유형을 확인할 수 있게 다음 PowerShell 옵션이 제공됩니다.

* 리소스 공급자에 대한 [REST API 작업](/rest/api/)을 보고 list 작업을 찾습니다. 예를 들어 저장소 계정에는 [listKeys 작업](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)이 있습니다.
* [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet을 사용합니다. 다음 예제에서는 저장소 계정에 대한 모든 list 작업을 가져옵니다.

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* 다음 Azure CLI 명령을 사용하여 목록 작업만 필터링합니다.

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

[resourceId 함수](#resourceid) 또는 형식 `{providerNamespace}/{resourceType}/{resourceName}`을 사용하여 리소스를 지정합니다.


### <a name="example"></a>예

다음 예에서는 출력 섹션의 저장소 계정에서 기본 및 보조 키를 반환하는 방법을 보여 줍니다.

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

## <a name="providers"></a>providers
`providers(providerNamespace, [resourceType])`

리소스 공급자와 지원되는 리소스 유형에 대한 정보를 반환합니다. 리소스 유형을 제공하지 않는 경우 함수는 리소스 공급자에 대한 모든 지원되는 유형을 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| providerNamespace |예 |string |공급자의 네임스페이스입니다. |
| resourceType |아니요 |string |지정된 네임스페이스 내의 리소스 유형입니다. |

### <a name="return-value"></a>반환 값

각 지원되는 형식이 다음 형식으로 반환됩니다. 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

반환된 값의 배열 순서는 보장되지 않습니다.

### <a name="example"></a>예

다음 예에서는 공급자 함수를 사용하는 방법을 보여 줍니다.

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

앞의 예제는 다음과 같은 형식의 개체를 반환합니다.

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

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

리소스의 런타임 상태를 나타내는 개체를 반환합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| resourceName 또는 resourceIdentifier |예 |string |리소스의 이름 또는 고유 식별자입니다. |
| apiVersion |아니요 |string |지정된 리소스의 API 버전입니다. 리소스가 동일한 템플릿 내에서 프로비전되지 않은 경우 이 매개 변수를 포함합니다. 일반적으로 **yyyy-mm-dd** 형식입니다. |

### <a name="return-value"></a>반환 값

모든 리소스 형식은 reference 함수에 대해 다른 속성을 반환합니다. 이 함수는 미리 정의된 단일 형식을 반환하지 않습니다. 리소스 형식에 대한 속성을 보려면 예제와 같이 outputs 섹션의 개체를 반환합니다.

### <a name="remarks"></a>설명

reference 함수는 런타임 상태에서 값을 파생하므로 변수 섹션에서 사용할 수 없습니다. 템플릿의 출력 섹션에서 사용할 수 있습니다. 

참조 함수를 사용하여 참조되는 리소스가 동일한 템플릿 내에서 프로비전되는 경우 한 리소스가 다른 리소스에 종속되도록 암시적으로 선언합니다. 또한 dependsOn 속성도 사용할 필요가 없습니다. 참조 리소스가 배포를 완료할 때까지 함수는 평가되지 않습니다.

리소스 유형에 대한 속성 이름 및 값을 보려면 outputs 섹션에서 개체를 반환하는 템플릿을 만듭니다. 해당 유형의 기존 리소스가 있는 경우 템플릿은 새로운 리소스를 배포하지 않고 개체를 반환합니다. 

일반적으로 **reference** 함수를 사용하여 blob 끝점 URI 또는 정규화된 도메인 이름과 같은 개체의 특정 값을 반환합니다.

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

### <a name="example"></a>예

동일한 템플릿에서 리소스를 배포하고 참조하려면 다음을 수행합니다.

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

앞의 예제는 다음과 같은 형식의 개체를 반환합니다.

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

다음 예제는 이 템플릿에 배포되지 않는 저장소 계정을 참조합니다. 저장소 계정은 동일한 리소스 그룹 내에 있어야 합니다.

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

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

현재 리소스 그룹을 나타내는 개체를 반환합니다. 

### <a name="return-value"></a>반환 값

반환된 개체는 다음 형식으로 되어 있습니다.

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

### <a name="remarks"></a>설명

resourceGroup 함수는 일반적으로 리소스 그룹과 동일한 위치에 리소스를 만드는 데 사용됩니다. 다음 예에서는 리소스 그룹 위치를 사용하여 웹 사이트에 대한 위치를 할당합니다.

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

### <a name="example"></a>예

다음 템플릿은 리소스 그룹의 속성을 반환합니다.

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

앞의 예제는 다음과 같은 형식의 개체를 반환합니다.

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

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

리소스의 고유 식별자를 반환합니다. 리소스 이름이 모호하거나 동일한 템플릿 내에서 프로비전되지 않은 경우 이 함수를 사용합니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| subscriptionId |아니요 |문자열(GUID 형식) |기본값은 현재 구독입니다. 다른 구독에서 리소스를 검색해야 하는 경우 이 값을 지정합니다. |
| resourceGroupName |아니요 |string |기본값은 현재 리소스 그룹입니다. 다른 리소스 그룹에서 리소스를 검색해야 하는 경우 이 값을 지정합니다. |
| resourceType |예 |string |리소스 공급자 네임스페이스를 포함하는 리소스 유형입니다. |
| resourceName1 |예 |string |리소스의 이름입니다. |
| resourceName2 |아니요 |string |리소스가 중첩된 경우 다음 리소스 이름 세그먼트입니다. |

### <a name="return-value"></a>반환 값

식별자는 다음 형식으로 반환됩니다.

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>설명

사용자가 지정한 매개 변수 값은 리소스가 현재 배포와 동일한 구독 및 리소스 그룹에 있는지 여부에 따라 달라집니다.

동일한 구독 및 리소스 그룹의 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

구독은 동일하지만 리소스 그룹은 다른 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

다른 구독 및 리소스 그룹의 저장소 계정에 대한 리소스 ID를 가져오려면 다음을 사용합니다.

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

다른 리소스 그룹의 데이터베이스에 대한 리소스 ID를 가져오려면 다음을 사용합니다.

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

대체 리소스 그룹의 저장소 계정 또는 가상 네트워크를 사용할 경우 이 함수를 사용해야 합니다. 다음 예에서는 외부 리소스 그룹의 리소스를 쉽게 사용할 수 있는 방법을 보여 줍니다.

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

### <a name="example"></a>예

다음 예제에서는 리소스 그룹의 저장소 계정에 대한 리소스 ID를 반환합니다.

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

기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| sameRGOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | 문자열 | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subscription
`subscription()`

현재 배포에 대한 구독 관련 세부 정보를 반환합니다. 

### <a name="return-value"></a>반환 값

이 함수는 다음 형식을 반환합니다.

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>예

다음 예에서는 출력 섹션에서 호출되는 구독 함수를 보여 줍니다. 

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

## <a name="next-steps"></a>다음 단계
* Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.
* 여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.
* 리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.
* 만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.

