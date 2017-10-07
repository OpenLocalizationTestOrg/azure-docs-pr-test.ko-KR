---
title: "DC/OS Azure 클러스터에 대 한 공유 aaaFile | Microsoft Docs"
description: "만들고 Azure 컨테이너 서비스에 있는 파일 공유 tooa DC/OS 클러스터 탑재"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>만들기 및 파일 공유 tooa DC/OS 클러스터 탑재
이 자습서 파일을 Azure에서 공유 하 고 각 에이전트와의 마스터에 탑재 toocreate DC/OS 클러스터 hello 하는 방법을 자세히 설명 합니다. 파일 공유를 설정 하면 보다 쉽게 tooshare 파일 구성, access, 로그, 같이 클러스터에 걸쳐 있습니다. 이 자습서의 작업을 수행 하는 hello 진행 됩니다.

> [!div class="checklist"]
> * Azure 저장소 계정 만들기
> * 파일 공유 만들기
> * Hello 공유 hello DC/OS 클러스터에 탑재

ACS DC/OS 클러스터 toocomplete hello이이 자습서의 단계를 해야 합니다. 필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Microsoft Azure에서 파일 공유 만들기

ACS DC/OS 클러스터와 Azure 파일 공유를 사용 하기 전에 hello 저장소 계정 및 파일 공유를 만들어야 합니다. 다음 스크립트는 hello 저장소 및 파일 공유를 toocreate hello를 실행 합니다. 사용자 환경에서 thoes로 hello 매개 변수를 업데이트 합니다.

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>Hello 공유 클러스터에 탑재

다음으로 hello 파일 공유 클러스터 내 모든 가상 컴퓨터에 탑재 된 toobe 필요 합니다. 이 작업은 hello cifs 도구/프로토콜을 사용 하 여 완료 합니다. hello 탑재 작업이 hello 클러스터의 각 노드에 대해 스크립트를 실행 하 여 또는 hello 클러스터의 각 노드에 수동으로 완료할 수 있습니다.

이 예제에서는 두 개의 스크립트가 실행, 한 toomount hello Azure 파일 공유 및 두 번째 toorun이이 스크립트 hello DC/OS 클러스터의 각 노드에서.

첫째, hello Azure 저장소 계정 이름 및 액세스 키가 필요 합니다. 이 정보 다음 명령을 tooget hello를 실행 합니다. 이러한 값을 이후 단계에서 사용하도록 적어둡니다.

저장소 계정 이름:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

저장소 계정 선택키:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

다음으로 hello를 hello DC/OS 마스터 및 변수에 저장의 FQDN을 가져옵니다.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

개인 키 toohello 마스터 노드를 복사 합니다. 이 키가 필요한 toocreate는 ssh hello 클러스터의 모든 노드를 연결 합니다. 기본값이 아닌 값 hello 클러스터를 만들 때 사용 된 경우 hello 사용자 이름을 업데이트 합니다. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

DC/OS 기반 클러스터의 hello 마스터 (또는 hello 첫 번째 마스터)에 대 한 SSH 연결을 만듭니다. 기본값이 아닌 값 hello 클러스터를 만들 때 사용 된 경우 hello 사용자 이름을 업데이트 합니다.

```azurecli-interactive
ssh azureuser@$FQDN
```

라는 파일을 만들어 **cifsMount.sh**, 복사 hello를 내용에 따라 합니다. 

이 스크립트에 사용 되는 toomount hello Azure 파일 공유입니다. 업데이트 hello `STORAGE_ACCT_NAME` 및 `ACCESS_KEY` hello 정보를 사용 하 여 변수 앞서 수집한 합니다.

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
라는 두 번째 파일을 만들어 **getNodesRunScript.sh** hello 파일에 내용을 복사 hello 및 합니다. 

이 스크립트는 모든 클러스터 노드를 검색 하 고 다음 실행 하는 hello **cifsMount.sh** 각 스크립트 toomount hello 파일 공유 합니다.

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Hello 클러스터의 모든 노드에서 hello 스크립트 toomount hello Azure 파일 공유를 실행 합니다.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

hello 파일 공유는 이제에 액세스할 수 있는 `/mnt/share/dcosshare` hello 클러스터의 각 노드에 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서는 Azure에서 파일 공유는 hello 단계를 사용 하 여 처리 된 사용 가능한 tooa DC/OS 클러스터 했습니다.

> [!div class="checklist"]
> * Azure 저장소 계정 만들기
> * 파일 공유 만들기
> * Hello 공유 hello DC/OS 클러스터에 탑재

Azure 컨테이너 레지스트리 Azure에서 DC/운영 체제와 통합 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.  

> [!div class="nextstepaction"]
> [부하 분산 응용 프로그램](container-service-dcos-acr.md)