---
title: "Azure 리소스 toomultiple 리소스 그룹 aaaDeploy | Microsoft Docs"
description: "배포 하는 동안 Azure 리소스가 두 개 이상 tootarget 그룹화 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Azure 리소스 toomore 보다 한 리소스 그룹 배포

일반적으로 모든 hello 리소스 템플릿 tooa 단일 리소스 그룹에 배포 합니다. 그러나 함께 toodeploy 리소스 집합을 원하는 하지만 다른 리소스 그룹에 배치 하는 시나리오가 있습니다. 예를 들어 toodeploy hello 백업 가상 컴퓨터가 Azure Site Recovery tooa 별도 리소스 그룹 및 위치에 대 한 좋습니다. 리소스 관리자 hello 부모 서식 파일에 사용 되는 hello 리소스 그룹 보다 toouse 중첩 템플릿 tootarget 여러 리소스 그룹이 있습니다.

hello 리소스 그룹에는 hello 응용 프로그램에 대 한 hello 수명 주기 컨테이너 및 리소스의 컬렉션입니다. Hello 템플릿 외부에서 hello 리소스 그룹을 만들고 배포 중 리소스 그룹 tootarget hello를 지정 합니다. 소개 tooresource 그룹에 대 한 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.

## <a name="example-template"></a>예제 템플릿

tootarget 다른 리소스를 배포 하는 동안 중첩 또는 연결 된 서식 파일을 사용 해야 합니다. hello `Microsoft.Resources/deployments` 리소스 종류 제공는 `resourceGroup` 매개 변수를 사용 toospecify hello에 대 한 다른 리소스 그룹 배포를 중첩 합니다. Hello 배포를 실행 하기 전에 모든 hello 리소스 그룹이 있어야 합니다. hello 다음 예제에서는 배포 배포 하는 동안 지정 된 hello 리소스 그룹에 각각 하나씩 두 개의 저장소 계정-리소스 그룹에 하나 `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

설정한 경우 `resourceGroup` 존재 하지 않는 리소스 그룹의 이름을 toohello hello 배포에 실패 합니다. 에 대 한 값을 제공 하지 않으면 `resourceGroup`, hello 부모 리소스 그룹 리소스 관리자를 사용 합니다.  

## <a name="deploy-hello-template"></a>Hello 템플릿을 배포합니다

toodeploy hello 예제 서식 파일을 hello 포털, Azure PowerShell 또는 Azure CLI를 사용할 수 있습니다. Azure PowerShell 또는 Azure CLI의 경우 2017년 5월 이후의 릴리스를 사용해야 합니다. hello 예제 이라는 파일로 hello 서식 파일을 로컬로 저장 한 가정 **crossrgdeployment.json**합니다.

PowerShell의 경우:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Azure CLI의 경우:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

배포가 완료되면 두 개의 리소스 그룹이 표시됩니다. 각 리소스 그룹에는 저장소 계정이 포함되어 있습니다.

## <a name="use-resourcegroup-function"></a>resourceGroup() 함수 사용

에 대 한 교차 리소스 그룹 배포 hello [resouceGroup() 함수](resource-group-template-functions-resource.md#resourcegroup) hello 중첩 된 서식 파일을 지정 하는 방법에 따라 다르게을 해결 합니다. 

다른 서식 파일에서 한 템플릿을 포함 한 경우 hello 중첩 된 템플릿에서 resouceGroup() toohello 부모 리소스 그룹을 확인 합니다. 포함 된 템플릿 형식에 따라 hello를 사용 합니다.

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Tooa 별도 서식 파일을 연결 하면 연결 된 템플릿의 hello resouceGroup() toohello 중첩된 리소스 그룹을 해결 합니다. 연결 된 템플릿 형식에 따라 hello를 사용 합니다.

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>다음 단계

* 템플릿에 toodefine 매개 변수를 확인 하려면 어떻게 toounderstand [hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해](resource-group-authoring-templates.md)합니다.
* 일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.
* SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.
