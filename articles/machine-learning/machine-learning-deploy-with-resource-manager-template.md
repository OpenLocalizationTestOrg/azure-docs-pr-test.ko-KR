---
title: "기계 학습 작업 영역에서 Azure 리소스 관리자와 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy Azure 리소스 관리자 템플릿을 사용 하 여 Azure 기계 학습 작업 영역"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Azure Resource Manager를 사용하여 기계 학습 작업 영역 배포
## <a name="introduction"></a>소개
배포 템플릿을 저장 하는 Azure 리소스 관리자를 사용 하 여 확장 가능한 방식으로 toodeploy 제공 하 여 시간 상호 연결 된 구성 요소에는 유효성 검사 및 다시 시도 메커니즘. Azure 기계 학습 작업 영역을 tooset, 예를 들어 필요한 toofirst는 Azure 저장소 계정을 구성 하 고 다음 작업 영역을 배포 합니다. 수백 개의 작업 영역에 대해 이 작업을 수동으로 수행한다고 가정합니다. 쉽게 대신 toouse Azure 리소스 관리자 템플릿 toodeploy Azure 기계 학습 작업 영역 및 모든 해당 모든 종속 됩니다. 이 문서는 이 과정을 단계별로 안내합니다. Azure Resource Manager에 대한 개요는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.

## <a name="step-by-step-create-a-machine-learning-workspace"></a>단계별: 기계 학습 작업 영역 만들기
Azure 리소스 그룹을 만든 다음 리소스 관리자 템플릿을 사용하여 새 Azure 저장소 계정 및 새 Azure 기계 학습 작업 영역을 배포합니다. Hello 배포 완료 되 면 (hello 기본 키, hello workspaceID 및 hello URL toohello 작업 영역) 생성 된 hello 작업 영역에 대 한 중요 한 정보를 출력 됩니다 했습니다.

### <a name="create-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿 만들기
기계 학습 작업 영역에는 Azure 저장소 계정 toostore hello 연결 된 데이터 집합 tooit이 필요합니다.
hello 다음 템플릿은 사용 hello 이름 hello 리소스 그룹 toogenerate hello 저장소 계정 이름 및 작업 영역 이름을 hello 합니다.  또한 hello 작업 영역을 만들 때 속성으로 hello 저장소 계정 이름을 사용 합니다.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
c:\temp\ 아래에 mlworkspace.json 파일로 이 템플릿을 저장합니다.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Hello 템플릿을 기반으로 hello 리소스 그룹 배포
* PowerShell 열기
* Azure Resource Manager 및 Azure 서비스 관리에 대한 모듈 설치  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   다음이 단계를 다운로드 하 고 hello 모듈 필요한 toocomplete hello 나머지 단계를 설치 합니다. 이 toobe hello PowerShell 명령을 실행 하는 hello 환경에서 한 번만 필요 합니다.   

* TooAzure 인증  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
이 단계는 각 세션에 대해 반복 toobe가 필요 합니다. 인증되면 구독 정보가 표시됩니다.

![Azure 계정][1]

액세스 tooAzure를 만들었으므로 이제 해당 hello 리소스 그룹을 만들 수 있습니다.

* 리소스 그룹 만들기

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

해당 hello 리소스 그룹 서 올바르게 프로 비전을 확인 합니다. **ProvisioningState** 는 "Succeeded"여야 합니다.
hello 리소스 그룹 이름은 hello 템플릿 toogenerate hello 저장소 계정 이름으로 사용 됩니다. hello 저장소 계정 이름은 길이가 3 ~ 24 자 사이 여야 하며 숫자 및 소문자만 사용 합니다.

![리소스 그룹][2]

* Hello 리소스 그룹 배포를 사용 하 여 새 기계 학습 작업 영역을 배포 합니다.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Hello 배포가 완료 되 면 배포 된 hello 영역의 간단 tooaccess 속성입니다. 예를 들어 기본 키 토큰 hello를 액세스할 수 있습니다.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

기존 작업 영역의 또 다른 방법은 tooretrieve 토큰이 toouse hello Invoke AzureRmResourceAction 명령입니다. 예를 들어 hello 기본 및 보조 토큰의 모든 작업 영역을 나열할 수 있습니다.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Hello를 사용 하 여 여러 Azure 기계 학습 스튜디오 작업을 자동화할 수도 있습니다 hello 작업 영역을 프로 비전 되 면 [Azure 기계 학습에 대 한 PowerShell 모듈](http://aka.ms/amlps)합니다.

## <a name="next-steps"></a>다음 단계
* [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)에 대해 자세히 알아봅니다. 
* Hello 살펴보고 [Azure 빠른 시작 템플릿 리포지토리](https://github.com/Azure/azure-quickstart-templates)합니다. 
* [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)에 대한 이 동영상을 시청합니다. 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
