---
title: "Azure CLI aaaExport 리소스 관리자 템플릿을 | Microsoft Docs"
description: "Azure 리소스 관리자 및 Azure CLI tooexport 리소스 그룹에서 서식 파일을 사용 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Azure CLI를 사용하여 Azure Resource Manager 템플릿 내보내기

리소스 관리자 구독에 기존 리소스에서 리소스 관리자 템플릿을 tooexport가 있습니다. 필요에 따라 솔루션의 hello 템플릿 구문 또는 tooautomate hello 재배포에 대 한 해당 생성 된 템플릿 toolearn를 사용할 수 있습니다.

중요 한 toonote 된다고 두 가지 방법으로 tooexport 서식 파일입니다.

* 배포에 사용한 hello 실제 서식 파일을 내보낼 수 있습니다. hello 내보낸된 템플릿에 hello 원본 서식 파일에 표시 된 그대로 hello 매개 변수 및 변수를 모두 포함 됩니다. 이 방법은 tooretrieve 서식 파일을 할 때 유용 합니다.
* Hello hello 리소스 그룹의 현재 상태를 나타내는 서식 파일을 내보낼 수 있습니다. hello에서 내보낸된 템플릿 배포에 사용 된 파일 따르지 않습니다. 대신, 템플릿에 hello 리소스 그룹의 스냅숏을 만듭니다. hello에서 내보낸된 템플릿에 하드 코드 된 값이 많은 및 일반적으로 정의할 때와 하지 못할 수의 매개 변수입니다. 이 방법은 hello 리소스 그룹을 수정한 경우에 유용 합니다. 이제 템플릿으로 toocapture hello 리소스 그룹이 필요 합니다.

이 항목에서는 두 가지 방법을 모두 보여 줍니다.

## <a name="deploy-a-solution"></a>솔루션 배포

템플릿을 내보내는 대 한 두 tooillustrate 가까워지면, 솔루션 tooyour 구독을 배포 하 여 시작 하겠습니다. 원하는 tooexport 구독에 리소스 그룹이 이미 있는 경우 않아도 toodeploy이이 솔루션입니다. 그러나이 문서의 나머지 부분에서는 hello toohello 서식 파일을이 솔루션에 대 한 참조합니다. hello 예제 스크립트는 저장소 계정을 배포합니다.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>배포 기록에서 템플릿 저장

Hello를 사용 하 여 배포 기록에서 서식 파일을 검색할 수 있습니다 [az 그룹 배포 내보내기](/cli/azure/group/deployment#export) 명령입니다. 다음 예에서는 이전에 배포 하는 저장 hello 템플릿을 hello:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Hello 서식 파일을 반환합니다. JSON, hello 복사한 파일로 저장 합니다. Hello 정확한 템플릿 배포에 사용 되는 점에 주목 합니다. hello 매개 변수 및 변수 GitHub에서 hello 템플릿을 일치합니다. 이 템플릿을 다시 배포할 수 있습니다.


## <a name="export-resource-group-as-template"></a>리소스 그룹을 템플릿으로 내보내기

Hello 배포 기록에서 서식 파일을 검색 하지 않고 hello를 사용 하 여 hello 리소스 그룹의 현재 상태를 나타내는 서식 파일을 검색할 수 있습니다 [az 그룹 내보내기](/cli/azure/group#export) 명령입니다. 많은 변경 내용을 tooyour 리소스 그룹을 변경한 있고 기존 템플릿이 hello 변경 내용을 모두를 나타내는 경우에이 명령을 사용 합니다.

```azurecli
az group export --name ExampleGroup
```

Hello 서식 파일을 반환합니다. JSON, hello 복사한 파일로 저장 합니다. GitHub의 hello 템플릿보다 다른 인지를 확인 합니다. 매개 변수는 다르고 변수는 없습니다. hello 저장소 SKU와 위치는 하드 코드 된 toovalues 합니다. hello 다음 예제에서는 hello 내보낸된 템플릿 되었지만 서식 파일에는 약간 다른 매개 변수 이름:

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

이 서식 파일을 다시 배포할 수 있습니다. 그러나 hello 저장소 계정의 고유한 이름을 추측 수행 해야 합니다. 매개 변수의 이름을 hello는 약간 다릅니다.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>내보낸 템플릿 사용자 지정

이 템플릿 toomake 수정할 수 있습니다 것 보다 쉽게 toouse 보다 유연 합니다. 자세한 위치 변경 hello 위치 속성 toouse tooallow hello 같은 hello 리소스 그룹 위치:

```json
"location": "[resourceGroup().location]",
```

tooavoid tooguess hello 저장소 계정 이름에 대 한 remove hello 매개 변수, 저장소 계정에 대 한 unique 이름을 갖게 됩니다. 저장소 이름 접미사에 대한 매개 변수와 저장소 SKU를 추가합니다.

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Hello uniqueString 함수로 hello 저장소 계정 이름을 생성 하는 변수를 추가 합니다.

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Hello 저장소 계정 toohello 변수의 hello 이름을 설정 합니다.

```json
"name": "[variables('storageAccountName')]",
```

Hello SKU toohello 매개 변수를 설정 합니다.

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

템플릿은 이제 다음과 같이 표시됩니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Hello 수정 된 서식 파일을 다시 배포 합니다.

## <a name="next-steps"></a>다음 단계
* Hello 포털 tooexport 서식 파일을 사용 하는 방법에 대 한 정보를 참조 하십시오. [기존 리소스에서 Azure 리소스 관리자 템플릿 내보내기](resource-manager-export-template.md)합니다.
* 서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.
* 일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.