---
title: "Azure Container Instances에서 Azure Files 볼륨 탑재"
description: "Azure Container Instances를 사용하여 상태가 유지되도록 Azure Files 볼륨을 탑재하는 방법에 대해 알아봅니다."
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: article
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: be502e6aef39ee4ed8cfc1f8926cb556dc1defb1
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="mount-an-azure-file-share-with-azure-container-instances"></a>Azure Container Instances를 사용하여 Azure 파일 공유 탑재

Azure Container Instances는 기본적으로 상태 비저장 방식으로 작동합니다. 컨테이너의 작동이 중단되거나 중지되면 모든 상태가 손실됩니다. 컨테이너 수명이 지난 후에도 상태를 유지하려면 외부 저장소에서 볼륨을 탑재해야 합니다. 이 문서에서는 Azure Container Instances에서 사용할 수 있도록 Azure 파일 공유를 탑재하는 방법을 설명합니다.

> [!NOTE]
> 현재 Azure 파일 공유를 탑재하는 작업은 Linux 컨테이너에 대해 제한되어 있습니다. 모든 기능을 Windows 컨테이너에서 제공하려고 합니다. 그 동안 [Azure Container Instances에 대한 할당량 및 지역 가용성](container-instances-quotas.md)에서 현재 플랫폼의 차이점을 찾을 수 있습니다.

## <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기

Azure Container Instances에서 Azure 파일 공유를 사용하려면 먼저 파일 공유를 만들어야 합니다. 다음 스크립트를 실행하여 파일 공유를 호스팅할 저장소 계정과 파일 공유 자체를 만듭니다. Storage 계정 이름은 전역적으로 고유해야 하므로 이 스크립트는 기준 문자열에 임의 값을 추가합니다.

```azurecli-interactive
# Change these four parameters as needed
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create \
    --resource-group $ACI_PERS_RESOURCE_GROUP \
    --name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --location $ACI_PERS_LOCATION \
    --sku Standard_LRS

# Export the connection string as an environment variable. The following 'az storage share create' command
# references this environment variable when creating the Azure file share.
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string --resource-group $ACI_PERS_RESOURCE_GROUP --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv`

# Create the file share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="get-storage-credentials"></a>저장소 자격 증명 가져오기

Azure Container Instances의 볼륨으로 Azure 파일 공유를 탑재하려면 Storage 계정 이름, 공유 이름, Storage 액세스 키의 세 가지 값이 필요합니다.

위의 스크립트를 사용한 경우 끝에 임의 값이 붙은 Storage 계정 이름이 생성되었을 것입니다. 임의 값 부분을 포함한 최종 문자열을 쿼리하려면 다음 명령을 사용합니다.

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group $ACI_PERS_RESOURCE_GROUP --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

공유 이름은 이미 알려져 있으므로(위 스크립트에서 *acishare*로 정의됨) 저장소 계정 키만 확인하면 됩니다. 이 키는 다음 명령을 사용하여 확인할 수 있습니다.

```azurecli-interactive
STORAGE_KEY=$(az storage account keys list --resource-group $ACI_PERS_RESOURCE_GROUP --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a>컨테이너 및 탑재 볼륨 배포

Azure 파일 공유를 컨테이너의 볼륨으로 탑재하려면 [az container create][az-container-create]를 사용하여 컨테이너를 만들 때 공유 및 볼륨 탑재 지점을 지정합니다. 이전 단계를 수행한 경우 다음 명령으로 이전에 만든 공유를 탑재하여 컨테이너를 만들 수 있습니다.

```azurecli-interactive
az container create \
    --resource-group $ACI_PERS_RESOURCE_GROUP \
    --name hellofiles \
    --image seanmckenna/aci-hellofiles \
    --ip-address Public \
    --ports 80 \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name $ACI_PERS_SHARE_NAME \
    --azure-file-volume-mount-path /aci/logs/
```

## <a name="manage-files-in-mounted-volume"></a>탑재된 볼륨의 파일 관리

컨테이너가 시작되면 [seanmckenna/aci-hellofiles][aci-hellofiles] 이미지를 통해 사용자가 지정한 탑재 경로에서 Azure 파일 공유의 관리 파일로 배포된 간단한 웹앱을 사용할 수 있습니다. [az container show][az-container-show] 명령을 사용하여 웹앱의 IP 주소를 가져옵니다.

```azurecli-interactive
az container show --resource-group $ACI_PERS_RESOURCE_GROUP --name hellofiles --output table
```

[Azure Portal][portal] 또는 [Microsoft Azure Storage 탐색기][storage-explorer]와 같은 도구를 사용하여 파일 공유에 작성된 파일을 검색하고 검사할 수 있습니다.

## <a name="mount-multiple-volumes"></a>여러 볼륨 탑재

컨테이너 인스턴스에서 여러 볼륨을 탑재하려면 [Azure Resource Manager 템플릿](/azure/templates/microsoft.containerinstance/containergroups)을 사용하여 배포해야 합니다.

먼저 공유 세부 정보를 제공하고 템플릿의 `properties` 섹션에서 `volumes` 배열을 채워서 볼륨을 정의합니다. 예를 들어, 저장소 계정 *myStorageAccount*에 *share1* 및 *share2*라는 두 개의 Azure 파일 공유를 만든 경우 `volumes` 배열이 다음과 비슷하게 표시됩니다.

```json
"volumes": [{
  "name": "myvolume1",
  "azureFile": {
    "shareName": "share1",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
},
{
  "name": "myvolume2",
  "azureFile": {
    "shareName": "share2",
    "storageAccountName": "myStorageAccount",
    "storageAccountKey": "<storage-account-key>"
  }
}]
```

다음으로 볼륨을 탑재하려는 컨테이너 그룹에 있는 각 컨테이너의 경우 컨테이너 정의의 `properties` 섹션에서 `volumeMounts` 배열을 채웁니다. 예를 들어 다음은 이전에 정의한 *myvolume1* 및 *myvolume2*라는 두 개의 볼륨을 탑재합니다.

```json
"volumeMounts": [{
  "name": "myvolume1",
  "mountPath": "/mnt/share1/"
},
{
  "name": "myvolume2",
  "mountPath": "/mnt/share2/"
}]
```

Azure Resource Manager 템플릿을 사용하는 컨테이너 인스턴스 배포의 예제를 보려면 [Azure Container Instances에서 다중 컨테이너 그룹 배포](container-instances-multi-container-group.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

[Azure Container Instances와 컨테이너 오케스트레이터 간의 관계](container-instances-orchestrator-relationship.md)에 대해 자세히 알아봅니다.

<!-- LINKS - External -->
[aci-hellofiles]: https://hub.docker.com/r/seanmckenna/aci-hellofiles/
[portal]: https://portal.azure.com
[storage-explorer]: https://storageexplorer.com

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container#az_container_create
[az-container-show]: /cli/azure/container#az_container_show