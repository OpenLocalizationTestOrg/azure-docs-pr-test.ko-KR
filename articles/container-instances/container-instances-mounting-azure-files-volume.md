---
title: "aaaMounting 컨테이너 인스턴스를 Azure에 있는 Azure 파일 볼륨"
description: "Azure 파일을 toomount 방법에 대해 알아봅니다 Azure 컨테이너 인스턴스와 볼륨 toopersist 상태"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Azure Container Instances를 사용하여 Azure 파일 공유 탑재

Azure Container Instances는 기본적으로 상태 비저장 방식으로 작동합니다. Hello 컨테이너 작동이 중단 되거나 중지 되 면 해당 상태가 모두 손실 됩니다. 외부 저장소에서 볼륨을 탑재 해야 hello 컨테이너의 hello 수명이 toopersist 상태입니다. 이 문서를 어떻게 toomount Azure 파일 공유 Azure 컨테이너 인스턴스를 사용 하기 위해 보여 줍니다.

## <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기

Azure Container Instances에서 Azure 파일 공유를 사용하려면 먼저 파일 공유를 만들어야 합니다. 저장소 계정 toohost hello 파일 공유와 hello를 자체 공유 스크립트 toocreate 다음 hello를 실행 합니다. Note hello 스크립트 임의의 값 toohello 기본 문자열을 추가 하므로 해당 hello 저장소 계정 이름은 전역적으로 고유 해야 합니다.

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>Storage 계정 액세스 세부 정보 가져오기

3 개의 값이 필요 하면 toomount 컨테이너 인스턴스를 Azure에서 볼륨으로 Azure 파일 공유를: hello 저장소 계정 이름, hello 공유 이름 및 hello 저장소 액세스 키입니다. 

위의 hello 스크립트를 사용 하는 경우에 hello 저장소 계정 이름은 hello 끝에 있는 임의의 값으로 만들어졌습니다. tooquery hello 최종 문자열 (포함 하 여 hello 임의 부분)에서 다음 명령을 사용 하 여 hello:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

hello 공유 이름이 이미 알려져 (이기 *acishare* 위의 hello 스크립트에) 다음 명령을 hello 남았습니다 hello 저장소 계정 키를 사용 하 여 찾을 수 있는 모든 있으므로:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Azure Key Vault를 사용하여 Storage 계정 액세스 세부 정보 저장

저장소 계정 키 액세스 tooyour 데이터를 보호 하므로 Azure 키 자격 증명 모음에 저장 하는 것이 좋습니다. 

Hello Azure CLI가 있는 주요 자격 증명 모음을 만듭니다.

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

hello `enabled-for-template-deployment` 스위치 사용 하면 Azure 리소스 관리자 toopull 주요 자격 증명 모음에서 암호 배포 시.

Hello 키 자격 증명 모음에는 새 암호로 hello 저장소 계정 키를 저장 합니다.

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Hello 볼륨을 탑재

Azure 파일 공유를 컨테이너에 볼륨으로 탑재할 때는 두 단계를 수행합니다. 먼저, 다음 원하는 하나 이상의 hello 그룹 hello 컨테이너 내에서 탑재 된 hello 볼륨을 지정 hello 컨테이너 그룹 정의의 일부로 hello 공유의 hello 세부 사항을 제공 합니다.

toodefine hello 볼륨 탑재에 사용할 수 있는 toomake 사용 하려는 추가 `volumes` hello Azure Resource Manager 템플릿에 toohello 컨테이너 그룹 정의 배열 다음 hello 개별 컨테이너의 hello 정의에서 참조 합니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

hello 서식 파일에 별도 매개 변수 파일에 제공 될 수 있는 매개 변수로 hello 저장소 계정 이름 및 키가 포함 되어 있습니다. toopopulate hello 매개 변수 파일을 3 개의 값이 필요 합니다: hello 저장소 계정 이름, 프로그램 Azure 키 자격 증명 모음의 리소스 ID hello 및 hello toostore hello 저장소 키를 사용 하는 주요 자격 증명 모음 보안 이름입니다. 이전 단계를 따른 경우에 다음 스크립트는 hello로 이러한 값을 얻을 수 있습니다.

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Hello 매개 변수 파일에 hello 값을 삽입 합니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>Hello 컨테이너를 배포 및 파일 관리

정의 된 hello 템플릿을 사용 하 여 hello 컨테이너 만들고 hello Azure CLI를 사용 하 여 해당 볼륨을 탑재할 수 있습니다. Hello 템플릿 파일 이름이 *azuredeploy.json* 해당 hello 매개 변수 파일의 이름이 고 *azuredeploy.parameters.json*, hello 명령줄은:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Hello 컨테이너 시작 되 면 면 hello를 통해 배포 된 hello 단순한 웹 앱을 사용할 수 있습니다 **seanmckenna/aci-hellofiles** 이미지 toohello 지정한 hello 탑재 경로 시 hello Azure 파일 공유에서 파일을 관리 합니다. Hello 다음을 통해 hello 웹 앱에 대 한 hello ip 주소를 가져옵니다.

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Hello와 같은 도구를 사용할 수 있습니다 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com) tooretrieve hello 파일 기록 된 toohello 파일 공유를 검사 합니다.

>[!NOTE]
> Azure 리소스 관리자 템플릿, 매개 변수 파일을 사용 하 고 hello Azure CLI를 사용 하 여 배포에 대해 자세히 toolearn 참조 [리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](../azure-resource-manager/resource-group-template-deploy-cli.md)합니다.

## <a name="next-steps"></a>다음 단계

- Hello Azure 컨테이너 인스턴스를 사용 하 여 첫 번째 컨테이너에 대 한 배포 [빠른 시작](container-instances-quickstart.md)
- Hello에 대 한 자세한 내용은 [Azure 컨테이너 인스턴스 및 컨테이너 orchestrators 간의 관계](container-instances-orchestrator-relationship.md)
