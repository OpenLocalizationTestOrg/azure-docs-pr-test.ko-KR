---
title: "서식 파일에 리소스 위치 aaaAzure | Microsoft Docs"
description: "표시 방법을 tooset Azure Resource Manager 템플릿의 리소스에 대 한 위치"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿에서 리소스 위치 설정
템플릿을 배포할 때는 각 리소스의 위치를 지정해야 합니다. 이 항목에서는 각 리소스에 대 한 사용 가능한 tooyour 구독 않은 toodetermine hello 위치 입력 하는 방법을 보여 줍니다.

## <a name="determine-supported-locations"></a>지원되는 위치 확인

각 리소스 유형에 대해 지원되는 위치의 전체 목록은 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요. 그러나 구독 액세스 tooall hello 위치 해당 목록에 없을 수 있습니다. 사용자 지정된 위치를 사용할 수 있는 tooyour 구독 목록을 toosee Azure PowerShell 또는 Azure CLI를 사용 합니다. 

hello 다음 예제에서는 PowerShell tooget hello 위치 hello에 대 한 `Microsoft.Web\sites` 리소스 종류:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

hello 다음 예제에서는 Azure CLI 2.0 tooget hello 위치 hello에 대 한 `Microsoft.Web\sites` 리소스 종류:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>템플릿에서 위치 설정

리소스에 대 한 지원 hello 위치를 결정 했으면 tooset 해당 위치에에서 필요한 서식 파일에 있습니다. 이 값은 toocreate hello 리소스 종류를 지 원하는 위치에 리소스를 그룹화 하는 가장 쉬운 방법은 tooset hello와 각 위치를 너무 설정`[resourceGroup().location]`합니다. 서로 다른 위치에 템플릿 tooresource 그룹 hello를 다시 배포할 수 있으며 hello 템플릿 또는 매개 변수 값을 변경 하지 수도 있습니다. 

hello 다음 예제에서는 배포 된 toohello 저장소 계정을 같은 hello 리소스 그룹 위치:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

서식 파일에서 toohardcode hello 위치 해야 할 경우 hello 이름 hello 지원 영역 중 하나를 제공 합니다. 다음 예제는 hello 항상 저장소 계정을 tooNorth 중앙 미국 배포를 보여 줍니다.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a>다음 단계
* 방법에 대 한 권장 사항에 대 한 toocreate 템플릿 참조 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](resource-manager-template-best-practices.md)합니다.

