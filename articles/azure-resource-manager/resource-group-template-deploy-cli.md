---
title: "Azure CLI 및 서식 파일을 사용 하 여 aaaDeploy 리소스 | Microsoft Docs"
description: "Azure 리소스 관리자 및 Azure CLI toodeploy 리소스 tooAzure를 사용 합니다. hello 리소스는 리소스 관리자 서식 파일에 정의 됩니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>리소스 관리자 템플릿과 Azure CLI로 리소스 배포

이 항목에서는 설명 어떻게 리소스 관리자 템플릿 toodeploy와 Azure CLI 2.0 toouse 리소스 tooAzure 합니다. 발생 Azure 솔루션을 관리 하는 배포의 hello 개념에 익숙하지 않은 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.  

hello 리소스 관리자 템플릿 배포를 컴퓨터에 로컬 파일 또는 GitHub와 같은 저장소에 있는 외부 파일 일 수도 있습니다. 이 문서에 배포 하는 hello 템플릿을 hello에 사용할 수는 [예제 서식 파일](#sample-template) 섹션 또는 [GitHub의 저장소 계정 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)합니다.

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

설치 된 Azure CLI가 없는 경우에 hello을 사용할 수 있습니다 [클라우드 셸](#deploy-template-from-cloud-shell)합니다.

## <a name="deploy-local-template"></a>로컬 템플릿 배포

리소스 tooAzure를 배포할 때 있습니다.

1. Azure 계정 tooyour에 로그인
2. 배포 된 hello 리소스에 대 한 hello 컨테이너 역할을 하는 리소스 그룹을 만듭니다. hello 리소스 그룹의 hello 이름은 영숫자, 마침표, 밑줄, 하이픈 및 괄호에만 포함할 수 있습니다. Too90 문자를 수 있습니다. 마침표로 끝날 수 없습니다.
3. Toohello 리소스 그룹 hello 템플릿을 hello 리소스 toocreate를 정의 하는 배포

템플릿을은 toocustomize hello 배포를 사용 하는 매개 변수를 포함할 수 있습니다. 예를 들어 특정 환경(예: 개발, 테스트 및 프로덕션)에 맞게 조정되는 값을 제공할 수 있습니다. hello 샘플 템플릿은 hello 저장소 계정 SKU에 대 한 매개 변수를 정의합니다. 

다음 예제는 hello 리소스 그룹을 만들고 서식 파일은 로컬 컴퓨터에서 배포.

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다. 완료 되 면 hello 결과 포함 하는 메시지가 표시:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>외부 템플릿 배포

로컬 컴퓨터의 리소스 관리자 템플릿을 저장 하는 대신 toostore 경우가 외부 위치에서 해당 합니다. 원본 제어 리포지토리(예: GitHub)에 템플릿을 저장할 수 있습니다. 또는 조직에서 공유 액세스에 대한 Azure Storage 계정에 저장할 수 있습니다.

toodeploy 외부 서식 파일을 사용 하 여 hello **uri 템플릿** 매개 변수입니다. GitHub에서 hello 예제 toodeploy hello 샘플 템플릿에서 URI hello를 사용 합니다.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

hello 앞의 예제에서는 공개적으로 액세스할 수 있는 URI 서식 파일에 중요 한 데이터를 포함 하지 해야 하기 때문에 대부분의 시나리오에 대 한 작동 하는 hello 서식 파일 Toospecify 중요 한 데이터 (예: 관리자 암호) 해야 할 경우 해당 값을 안전한 매개 변수로 전달 합니다. 그러나 하지 않을 경우 서식 파일 toobe 공개적으로 액세스할 수 있는, 개인 저장소 컨테이너에 저장 하 여 보호할 수 있습니다. SAS(공유 액세스 서명) 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-cli-sas-token.md)를 참조하세요.

## <a name="deploy-template-from-cloud-shell"></a>Cloud Shell에서 템플릿 배포

사용할 수 있습니다 [클라우드 셸](../cloud-shell/overview.md) toorun hello Azure CLI 서식 파일을 배포 하기 위한 명령입니다. 그러나 먼저 로드 해야 서식 파일을 hello 파일 공유에 클라우드 셸에 대 한 합니다. Cloud Shell을 사용해 본 적이 없다면 [Azure Cloud Shell 개요](../cloud-shell/overview.md)에서 Cloud Shell 설정 방법을 참조하세요.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.   

2. Cloud Shell 리소스 그룹을 선택합니다. hello 이름 패턴은 `cloud-shell-storage-<region>`합니다.

   ![리소스 그룹 선택](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. 클라우드 셸에 대 한 hello 저장소 계정을 선택 합니다.

   ![저장소 계정 선택](./media/resource-group-template-deploy-cli/select-storage.png)

4. **파일**을 선택합니다.

   ![파일 선택](./media/resource-group-template-deploy-cli/select-files.png)

5. 클라우드 셸용 hello 파일 공유를 선택 합니다. hello 이름 패턴은 `cs-<user>-<domain>-com-<uniqueGuid>`합니다.

   ![파일 공유 선택](./media/resource-group-template-deploy-cli/select-file-share.png)

6. **디렉터리 추가**를 선택합니다.

   ![디렉터리 추가](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. 이름을 **templates**로 지정하고 **확인**을 선택합니다.

   ![디렉터리 이름 지정](./media/resource-group-template-deploy-cli/name-templates.png)

8. 새 디렉터리를 선택합니다.

   ![디렉터리 선택](./media/resource-group-template-deploy-cli/select-templates.png)

9. **업로드**를 선택합니다.

   ![업로드 선택](./media/resource-group-template-deploy-cli/select-upload.png)

10. 템플릿을 찾아서 업로드합니다.

   ![파일 업로드](./media/resource-group-template-deploy-cli/upload-files.png)

11. 열기 hello 프롬프트입니다.

   ![Cloud Shell 열기](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Hello 명령을 hello 클라우드 셸에서에서 다음을 입력 합니다.

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a>매개 변수 파일

인라인 스크립트에는 값으로 매개 변수를 전달 하는 대신 쉽게 toouse를 hello 매개 변수 값을 포함 하는 JSON 파일 좋습니다. hello 매개 변수 파일 형식에 따라 hello 이어야 합니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Hello 매개 변수 섹션 (storageAccountType) 서식 파일에 정의 된 hello 매개 변수에 일치 하는 매개 변수 이름을 포함 되어 있는지 확인 합니다. hello 매개 변수 파일 hello 매개 변수의 값을 포함합니다. 자동으로이 값은 배포 중 toohello 서식 파일을 전달 합니다. 다양 한 배포 시나리오에 대 한 여러 매개 변수 파일을 만들고 hello 적절 한 매개 변수 파일에 전달할 수 있습니다. 

앞 예제는 hello를 복사 하 고 이라는 파일로 저장 `storage.parameters.json`합니다.

toopass 로컬 매개 변수 파일을 사용 하 여 `@` toospecify storage.parameters.json 이라는 로컬 파일로 내보내집니다.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>템플릿 배포 테스트

실제로 모든 리소스를 배포 하지 않고 템플릿 및 매개 변수 값에 사용 하 여 tootest [az 그룹 배포의 유효성을 검사](/cli/azure/group/deployment#validate)합니다. 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

오류가 감지 되 면 hello 명령은 hello 테스트 배포에 대 한 정보를 반환 합니다. 특히, 해당 hello 확인 **오류** 값은 null입니다.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

오류가 검색 되 면 hello 명령은 오류 메시지를 반환 합니다. 예를 들어 toopass hello 저장소 계정 SKU에 대 한 잘못 된 값을 시도 하면 다음 오류가 hello 반환:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

서식 파일에 구문 오류가 있으면 hello 명령은 hello 서식 파일을 분석할 수 없습니다 것을 나타내는 오류를 반환 합니다. hello 메시지 hello 줄 번호 및 구문 분석 오류 hello의 위치를 나타냅니다.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse 전체 모드를 사용 하 여 hello `mode` 매개 변수:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a>샘플 템플릿

hello 다음 서식 파일에 사용 됩니다이 항목의 hello 예제. 복사한 후 storage.json이라는 파일로 저장합니다. toounderstand 어떻게 toocreate이 서식이 파일 참조 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](resource-manager-create-first-template.md)합니다.  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>다음 단계
* hello이이 문서의 예제에서는 기본 구독에서 리소스 tooa 리소스 그룹을 배포합니다. 다른 구독을 toouse 참조 [여러 Azure 구독을 관리](/cli/azure/manage-azure-subscriptions-azure-cli)합니다.
* 템플릿을 배포하는 전체 샘플 스크립트는 [Resource Manager 템플릿 배포 스크립트](resource-manager-samples-cli-deploy.md)를 참조하세요.
* 템플릿에 toodefine 매개 변수를 확인 하려면 어떻게 toounderstand [hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해](resource-group-authoring-templates.md)합니다.
* 일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.
* SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-cli-sas-token.md)를 참조하세요.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.
