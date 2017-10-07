---
title: "첫 번째 Azure 리소스 관리자 템플릿 aaaCreate | Microsoft Docs"
description: "단계별 가이드 toocreating 첫 번째 Azure 리소스 관리자 서식 파일에 있습니다. Toouse 저장소 계정 toocreate hello 템플릿에 대 한 템플릿 참조 hello 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>첫 번째 Azure Resource Manager 템플릿을 만들고 배포
이 항목의 첫 번째 여 Azure 리소스 관리자 템플릿을 만드는 hello 단계를 안내 합니다. 리소스 관리자 템플릿은 toodeploy 솔루션에 필요한 hello 리소스 정의 하는 JSON 파일입니다. 배포 하 고 Azure 솔루션 관리와 관련 된 toounderstand hello 개념 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다. 기존 리소스가 있는 해당 리소스에 대해 tooget 서식 파일을 원하는 경우 참조 [기존 리소스에서 Azure 리소스 관리자 템플릿 내보내기](resource-manager-export-template.md)합니다.

toocreate 및 개정 템플릿에서 JSON 편집기가 필요합니다. [Visual Studio Code](https://code.visualstudio.com/)는 간단한 오픈 소스 크로스 플랫폼 코드 편집기입니다. Visual Studio Code를 사용하여 Resource Manager 템플릿을 만드는 것이 좋습니다. 이 항목에서는 VS 코드를 사용한다고 가정하지만 다른 JSON 편집기(예: Visual Studio)가 있는 경우 해당 편집기를 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

* Visual Studio Code. 필요한 경우 [https://code.visualstudio.com/](https://code.visualstudio.com/)에서 설치합니다.
* Azure 구독. Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

## <a name="create-template"></a>템플릿 만들기

저장소 계정 tooyour 구독을 배포 하는 간단한 템플릿을 사용 하 여 시작 하겠습니다.

1. **파일** > **새 파일**을 선택합니다. 

   ![새 파일](./media/resource-manager-create-first-template/new-file.png)

2. 복사한 파일에 JSON 구문 다음 hello를 붙여넣습니다.

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   저장소 계정 이름에 어려운 tooset 게 사용할 수 있는 몇 가지 제한이 있습니다. hello 이름 길이 사용 하 여만 숫자 및 소문자, 3 자에서 24 자 사이 여야 하 고 고유 해야 합니다. hello 이전 템플릿을 사용 하 여 hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate 해시 값을 작동 합니다. hello 접두사를 추가, 즉 자세히 toogive이이 해시 값 *저장소*합니다. 

3. 이 파일을 저장 **azuredeploy.json** tooa 로컬 폴더입니다.

   ![템플릿 저장](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>템플릿 배포

사용자는 준비 toodeploy이 서식이 파일입니다. PowerShell 또는 Azure CLI toocreate 리소스 그룹을 사용 합니다. 그런 다음, 저장소 계정 toothat 리소스 그룹을 배포 합니다.

* PowerShell을 hello 명령을 hello 서식 파일을 포함 하는 hello 폴더에서 다음을 사용 합니다.

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Azure CLI의 로컬 설치의 경우 hello 명령을 hello 서식 파일을 포함 하는 hello 폴더에서 다음을 사용 합니다.

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

배포 완료 되 면 hello 리소스 그룹에 저장소 계정이 있습니다.

## <a name="deploy-template-from-cloud-shell"></a>Cloud Shell에서 템플릿 배포

사용할 수 있습니다 [클라우드 셸](../cloud-shell/overview.md) toorun hello Azure CLI 서식 파일을 배포 하기 위한 명령입니다. 그러나 먼저 로드 해야 서식 파일을 hello 파일 공유에 클라우드 셸에 대 한 합니다. Cloud Shell을 사용해 본 적이 없다면 [Azure Cloud Shell 개요](../cloud-shell/overview.md)에서 Cloud Shell 설정 방법을 참조하세요.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.   

2. Cloud Shell 리소스 그룹을 선택합니다. hello 이름 패턴은 `cloud-shell-storage-<region>`합니다.

   ![리소스 그룹 선택](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. 클라우드 셸에 대 한 hello 저장소 계정을 선택 합니다.

   ![저장소 계정 선택](./media/resource-manager-create-first-template/select-storage.png)

4. **파일**을 선택합니다.

   ![파일 선택](./media/resource-manager-create-first-template/select-files.png)

5. 클라우드 셸용 hello 파일 공유를 선택 합니다. hello 이름 패턴은 `cs-<user>-<domain>-com-<uniqueGuid>`합니다.

   ![파일 공유 선택](./media/resource-manager-create-first-template/select-file-share.png)

6. **디렉터리 추가**를 선택합니다.

   ![디렉터리 추가](./media/resource-manager-create-first-template/select-add-directory.png)

7. 이름을 **templates**로 지정하고 **확인**을 선택합니다.

   ![디렉터리 이름 지정](./media/resource-manager-create-first-template/name-templates.png)

8. 새 디렉터리를 선택합니다.

   ![디렉터리 선택](./media/resource-manager-create-first-template/select-templates.png)

9. **업로드**를 선택합니다.

   ![업로드 선택](./media/resource-manager-create-first-template/select-upload.png)

10. 템플릿을 찾아서 업로드합니다.

   ![파일 업로드](./media/resource-manager-create-first-template/upload-files.png)

11. 열기 hello 프롬프트입니다.

   ![Cloud Shell 열기](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Hello 명령을 hello 클라우드 셸에서에서 다음을 입력 합니다.

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

배포 완료 되 면 hello 리소스 그룹에 저장소 계정이 있습니다.

## <a name="customize-hello-template"></a>Hello 템플릿을 사용자 지정

hello 템플릿 정상적으로 작동 하지만 유연한있지 않습니다. 항상 로컬 중복 저장소 tooSouth 중미 배포합니다. hello 이름은 항상 *저장소* 다음 해시 값입니다. tooenable hello 템플릿을 사용 하 여 다양 한 시나리오에 대 한 매개 변수 toohello 서식 파일을 추가 합니다.

hello 다음 예제에서는 두 개의 매개 변수를 사용 하 여 hello 매개 변수 섹션 첫 번째 매개 변수를 hello `storageSKU` toospecify hello 종류의 중복 항목 수 있도록 합니다. Hello 값 저장소 계정에 대해 사용할 수 있는 toovalues에 전달할 수를 제한 합니다. 또한 기본값을 지정합니다. 두 번째 매개 변수를 hello `storageNamePrefix` 집합 tooallow 11 자 최대입니다. 기본값을 지정합니다.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Hello 변수 섹션에서 명명 된 변수를 추가 `storageName`합니다. Hello 매개 변수에서 hello 접두사 값과 hello에서 해시 값을 결합 하 여 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수입니다. Hello를 사용 하 여 [toLower](resource-group-template-functions-string.md#tolower) tooconvert 모든 문자 toolowercase 작동 합니다.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse hello 리소스 정의 변경 하는 저장소 계정에 이러한 새 값:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

해당 hello 확인 hello 저장소 계정의 이름을 이제 사용자가 추가한 toohello 변수를 설정 합니다. hello SKU 이름 toohello hello 매개 변수 값을 설정 됩니다. hello 위치가 설정 hello 같은 hello 리소스 그룹 위치입니다.

파일을 저장합니다. 

이 문서의 hello 단계를 완료 한 후 해당 템플릿을 같이 나타납니다.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>템플릿 다시 배포

값이 서로 다른 hello 템플릿을 다시 배포 합니다.

PowerShell의 경우 다음을 사용합니다.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Azure CLI의 경우 

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

클라우드 셸 hello에 대 한 변경 된 템플릿을 toohello 파일 공유에 업로드 합니다. Hello 기존 파일을 덮어씁니다. 그런 다음 다음 명령을 hello를 사용 합니다.

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>리소스 정리

더 이상 필요 hello 리소스 그룹을 삭제 하 여 배포 된 hello 리소스를 정리 합니다.

PowerShell의 경우 다음을 사용합니다.

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Azure CLI의 경우 

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>다음 단계
* 참조는 템플릿의 hello 구조에 대해 자세히 toolearn [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* 저장소 계정에 대 한 hello 속성에 대 한 toolearn 참조 [저장소 계정 템플릿 참조](/azure/templates/microsoft.storage/storageaccounts)합니다.
* 다양 한 유형의 솔루션에 대 한 전체 템플릿을 tooview 참조 hello [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.
