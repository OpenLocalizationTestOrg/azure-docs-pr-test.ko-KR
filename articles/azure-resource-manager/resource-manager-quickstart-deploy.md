---
title: "aaaDeploy 리소스 tooAzure | Microsoft Docs"
description: "Azure PowerShell 또는 Azure CLI toodeploy 리소스 tooAzure를 사용 합니다. hello 리소스는 리소스 관리자 서식 파일에 정의 됩니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>리소스 tooAzure 배포

이 항목에서는 방법을 toodeploy 리소스 tooyour Azure 구독. Azure PowerShell 또는 Azure CLI toodeploy 솔루션에 대 한 hello 인프라를 정의 하는 리소스 관리자 템플릿을 사용할 수 있습니다.

소개 tooconcepts 리소스 관리자의를 참조 하십시오. [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.

## <a name="steps-for-deployment"></a>배포 단계

이 항목에서는 hello를 배포 하는 [예제 저장소 템플릿](#example-storage-template) 이 항목의 합니다. 다른 서식 파일을 사용할 수 있지만 hello 매개 변수를 전달 하면이 항목에 표시 된 항목 보다 다릅니다.

서식 파일을 만든 후 서식 파일을 배포 하기 위한 일반 단계 hello 됩니다.

1. Tooyour 계정에 로그인
2. Hello 구독 toouse (여러 구독이 있는 toouse 이름이 아닌 hello 기본 구독 하려는 경우에 필요)를 선택 합니다.
3. 리소스 그룹 만들기
4. Hello 템플릿을 배포합니다
5. 배포 상태 확인

hello 다음 섹션에서는 보여 어떻게 tooperform 된 단계와 [PowerShell](#powershell) 또는 [Azure CLI](#azure-cli)합니다.

## <a name="powershell"></a>PowerShell

1. Azure PowerShell tooinstall 참조 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/overview)합니다.

2. tooquickly 배포 시작 하기, hello 다음 cmdlet을 사용 하 여:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  hello `Set-AzureRmContext` cmdlet은 기본 구독 이외의 toouse 구독 하려는 경우에 필요 합니다. toosee 모든 구독 및 Id를 사용 합니다.

  ```powershell
  Get-AzureRmSubscription
  ```

3. hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다. 배포가 완료되면 다음과 비슷한 메시지가 표시됩니다.

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. 리소스 그룹 및 저장소 계정이 되었던 toosee tooyour 구독을 사용 하 여 배포 합니다.

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. 템플릿을 배포할 때 템플릿 매개 변수를 PowerShell 매개 변수로 지정할 수 있습니다. hello 앞의 예제 포함 되지 않았습니다 템플릿 매개 변수를 hello hello 서식 파일의 기본값을 사용 하므로. toodeploy 다른 저장소 계정을 한 hello 저장소 이름 접두사와 SKU hello 저장소 계정 사용에 대 한 매개 변수 값을 제공 합니다.

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  이제 리소스 그룹에 두 개의 저장소 계정이 있습니다. 

## <a name="azure-cli"></a>Azure CLI

1. Azure CLI tooinstall 참조 [Azure CLI 2.0 설치](/cli/azure/install-az-cli2)합니다.

2. tooquickly 배포 시작 하기, hello 다음 명령을 사용 하 여:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  hello `az account set` 명령을 기본 구독 이외의 toouse 구독 하려는 경우에 필요 합니다. toosee 모든 구독 및 Id를 사용 합니다.

  ```azurecli
  az account list
  ```

3. hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다. 배포가 완료되면 다음과 비슷한 메시지가 표시됩니다.

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. 리소스 그룹 및 저장소 계정이 되었던 toosee tooyour 구독을 사용 하 여 배포 합니다.

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. 템플릿을 배포할 때 템플릿 매개 변수를 PowerShell 매개 변수로 지정할 수 있습니다. hello 앞의 예제 포함 되지 않았습니다 템플릿 매개 변수를 hello hello 서식 파일의 기본값을 사용 하므로. toodeploy 다른 저장소 계정을 한 hello 저장소 이름 접두사와 SKU hello 저장소 계정 사용에 대 한 매개 변수 값을 제공 합니다.

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  이제 리소스 그룹에 두 개의 저장소 계정이 있습니다. 

## <a name="example-storage-template"></a>예제 저장소 템플릿

다음 예제에서는 서식 파일 toodeploy 저장소 계정 tooyour 구독은 hello를 사용 합니다.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
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
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>다음 단계

* PowerShell toodeploy 템플릿을 사용 하는 방법에 대 한 자세한 내용은 참조 [리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](/azure/azure-resource-manager/resource-group-template-deploy)합니다.
* Azure CLI toodeploy 템플릿을 사용 하는 방법에 대 한 자세한 내용은 참조 [리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](/azure/azure-resource-manager/resource-group-template-deploy-cli)합니다.



