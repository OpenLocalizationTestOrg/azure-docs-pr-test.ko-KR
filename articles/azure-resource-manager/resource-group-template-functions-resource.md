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
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿용 리소스 함수

리소스 관리자 리소스 값을 가져오고이 대 한 함수를 수행 하는 hello를 제공 합니다.

* [listKeys 및 list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

매개 변수, 변수 또는 hello 현재 배포에서 tooget 값 참조 [배포 값 기능](resource-group-template-functions-deployment.md)합니다.

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys 및 list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

반환 hello hello 목록 작업을 지 원하는 모든 리소스 종류에 대 한 값입니다. 가장 많이 사용 hello `listKeys`합니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| resourceName 또는 resourceIdentifier |예 |string |Hello 리소스에 대 한 고유 식별자입니다. |
| apiVersion |예 |string |리소스 런타임 상태의 API 버전입니다. 일반적으로 hello 형태로 **yyyy-월-일**합니다. |

### <a name="return-value"></a>반환 값

hello는 Listkey에서 개체에 hello 형식에 따라에 반환 합니다.

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

다른 list 함수는 다른 반환 형식을 갖습니다. 함수의 toosee hello 형식 hello 예제 서식 파일에 나와 있는 것 처럼 것 hello 출력 섹션에 포함. 

### <a name="remarks"></a>설명

**list**로 시작하는 작업은 템플릿에서 함수로 사용됩니다. hello 사용할 수 있는 작업에는 뿐만 아니라 Listkey 하지만 같은 작업 `list`, `listAdminKeys`, 및 `listStatus`합니다. 그러나 사용할 수 없습니다 **목록** hello에 대 한 값을 필요로 하는 작업 요청 본문입니다. 예를 들어 hello [목록 계정 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) 작업 등의 요청 본문 매개 변수가 필요 *signedExpiry*이므로 템플릿 내에서 사용할 수 없습니다.

어떤 리소스 유형에 있는 list 작업 toodetermine, hello 다음 옵션을 사용할 수 있습니다.

* 보기 hello [REST API 작업](/rest/api/) 리소스 공급자 및 목록 작업을 찾습니다. 예를 들어 저장소 계정이 있는 hello [Listkey 작업](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)합니다.
* 사용 하 여 hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet. hello 다음 예제에서는 가져옵니다 모든 저장소 계정에 대 한 작업을 나열 합니다.

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* 다음 toofilter 목록 작업을만 hello Azure CLI 명령을 hello를 사용 합니다.

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Hello 중 하나를 사용 하 여 hello 리소스 지정 [resourceId 함수](#resourceid), 또는 hello 형식 `{providerNamespace}/{resourceType}/{resourceName}`합니다.


### <a name="example"></a>예제

hello 다음 예제에서는 hello의 저장소 계정에서 tooreturn hello 기본 및 보조 키 섹션을 출력 하는 방법

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

리소스 공급자와 지원되는 리소스 유형에 대한 정보를 반환합니다. 리소스 종류를 제공 하지 않으면 hello 함수 hello 리소스 공급자에 대 한 모든 지원 되는 hello 형식을 반환 합니다.

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| providerNamespace |예 |string |Hello 공급자의 Namespace |
| resourceType |아니요 |string |네임 스페이스를 지정 하는 hello 형식 hello 내에서 리소스입니다. |

### <a name="return-value"></a>반환 값

형식에 따라 hello에 각 지원 되는 형식 반환 됩니다. 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

배열 정렬 hello 반환 값 보장 되지 않습니다.

### <a name="example"></a>예제

다음 예제는 hello toouse 공급자 함수가 해당 확장을 hello 하는 방법을 보여 줍니다.

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

hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:

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
| apiVersion |아니요 |string |API 버전의 hello 리소스를 지정 합니다. 같은 템플릿 내에서 hello 리소스 프로 비전 되지 않은 경우이 매개 변수를 포함 합니다. 일반적으로 hello 형태로 **yyyy-월-일**합니다. |

### <a name="return-value"></a>반환 값

모든 리소스 종류는 함수를 참조 하는 hello에 대 한 다른 속성을 반환합니다. hello 함수는 단일, 미리 정의 된 형식을 반환 하지 않습니다. 리소스 유형에 대 한 toosee hello 속성 hello에 hello 개체 출력 섹션 hello 예제에 표시 된 대로 반환 합니다.

### <a name="remarks"></a>설명

함수를 참조 하는 hello 런타임 상태에서 해당 값을 파생 하 고 hello 변수 섹션에서 사용할 수 없습니다. 템플릿의 출력 섹션에서 사용할 수 있습니다. 

함수를 참조 하는 hello를 사용 하 여 암시적으로 선언 같은 템플릿 내에서 참조 하는 hello 리소스 프로 비전 된 경우 리소스가 다른 리소스에 종속 되도록 합니다. Tooalso use hello dependsOn 속성이 필요가 없습니다. hello 함수 평가 되지 않습니다 완료할 때까지 hello 참조 리소스 배포.

toosee hello 속성 이름 및 값 리소스 유형에 대 한 hello 출력 섹션의 hello 개체를 반환 하는 템플릿을 만듭니다. 해당 형식의 기존 리소스를 사용 하도록 설정한 경우 서식 파일에 새 리소스를 배포 하지 않고 hello 개체를 반환 합니다. 

Hello를 사용 하는 일반적으로 **참조** tooreturn hello blob 끝점 URI 등의 개체 또는 정규화 된 도메인 이름에서 특정 값을 작동 합니다.

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

### <a name="example"></a>예제

toodeploy 및 참조 hello 리소스 hello에 같은 템플릿을 사용 하 여:

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

hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:

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

hello 다음 예제에서는 참조이 서식 파일에 배포 되지 않은 저장소 계정입니다. hello 저장소 계정이 이미 hello 내에서 동일한 리소스 그룹입니다.

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

Hello 현재 리소스 그룹을 나타내는 개체를 반환 합니다. 

### <a name="return-value"></a>반환 값

개체는 형식에 따라 hello에 반환 하는 hello:

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

Hello resourceGroup 함수의 일반적인 용도 hello의 toocreate 리소스 같은 hello 리소스 그룹 위치입니다. hello 다음 예제에서는 hello 리소스 그룹 위치 tooassign hello 위치 웹 사이트에 대 한 합니다.

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

### <a name="example"></a>예제

hello 다음 템플릿을 반환 hello 리소스 그룹의 hello 속성 합니다.

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

hello 앞의 예제에서에서 개체를 반환 형식에 따라 hello:

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

반환 hello 리소스의 고유 식별자입니다. 이 함수를 사용 하 여 hello 리소스 이름이 모호 하거나 hello 내에서 프로 비전 되지 않습니다 같은 서식 파일입니다. 

### <a name="parameters"></a>매개 변수

| 매개 변수를 포함해야 합니다. | 필수 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| subscriptionId |아니요 |문자열(GUID 형식) |기본값은 현재 구독 hello입니다. Tooretrieve 다른 구독에 리소스를 필요할 때이 값을 지정 합니다. |
| resourceGroupName |아니요 |string |기본값은 현재 리소스 그룹입니다. Tooretrieve 다른 리소스 그룹에 리소스를 필요할 때이 값을 지정 합니다. |
| resourceType |예 |string |리소스 공급자 네임스페이스를 포함하는 리소스 유형입니다. |
| resourceName1 |예 |string |리소스의 이름입니다. |
| resourceName2 |아니요 |string |리소스가 중첩된 경우 다음 리소스 이름 세그먼트입니다. |

### <a name="return-value"></a>반환 값

hello 식별자 형식에 따라 hello에 반환 됩니다.

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>설명

hello 매개 변수 값 지정에 따라 달라 집니다 hello hello 리소스 인지 hello 현재 배포와 동일한 구독 및 리소스 그룹입니다.

tooget hello 리소스 ID가 hello의 저장소 계정에 대 한 같음 구독 및 리소스 그룹을 사용 하 여:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

저장소 계정에 대 한 tooget hello 리소스 ID에 동일한 구독 하지만 다른 리소스 그룹에서 사용 하 여 hello:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

다른 구독 및 리소스 그룹의 저장소 계정에 대 한 tooget hello 리소스 ID를 사용 합니다.

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

다른 리소스 그룹에 데이터베이스에 대 한 tooget hello 리소스 ID를 사용 합니다.

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

종종 해야 toouse이이 함수는 다른 리소스 그룹에 저장소 계정 또는 가상 네트워크를 사용 하는 경우. hello 다음 예제는 리소스는 외부 리소스 그룹에서 사용할 수 있는 방법을 쉽게.

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

### <a name="example"></a>예제

hello 다음 예제에서는 hello 리소스 ID를 반환 저장소 계정에 대 한 hello 리소스 그룹:

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

hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:

| 이름 | 형식 | 값 |
| ---- | ---- | ----- |
| sameRGOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | 문자열 | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | 문자열 | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subscription
`subscription()`

Hello 현재 배포에 대 한 hello 구독에 대 한 세부 정보를 반환 합니다. 

### <a name="return-value"></a>반환 값

hello 함수 형식에 따라 hello를 반환 합니다.

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>예제

hello 다음 예제에서는 hello 출력 섹션에서 호출 하는 hello 구독 함수 

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
* Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.
* 지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.
* toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.

