---
title: "Azure DC/OS 클러스터와 ACR aaaUsing | Microsoft Docs"
description: "Azure Container Service에서 DC/OS 클러스터에 Azure Container Registry 사용"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>ACR DC/OS 클러스터 toodeploy와 응용 프로그램 사용

탐색이 문서에서는 어떻게 DC/OS 클러스터와 Azure 컨테이너 레지스트리 toouse 합니다. ACR을 사용 하 여 컨테이너 이미지를 관리 및 tooprivately 저장소 있습니다. 이 자습서에서는 hello 다음 작업 방법을 배웁니다.

> [!div class="checklist"]
> * Azure Container Registry 배포(필요한 경우)
> * DC/OS 클러스터에서 ACR 인증 구성
> * 이미지 toohello Azure 컨테이너 레지스트리 업로드
> * Azure 컨테이너 레지스트리 hello에서 컨테이너 이미지를 실행 합니다.

ACS DC/OS 클러스터 toocomplete hello이이 자습서의 단계를 해야 합니다. 필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.

이 자습서에서는 Azure CLI 버전 2.0.4 hello 이상. 실행 `az --version` toofind hello 버전입니다. Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Azure Container Registry 배포

필요한 경우 Azure 컨테이너 레지스트리 hello로 만들 [az acr 만들기](/cli/azure/acr#create) 명령입니다. 

hello 다음 예제에서는 사용 하 여 레지스트리를는 이름을 임의로 생성 합니다. hello 레지스트리 hello를 사용 하 여 관리자 계정으로도 구성 된 `--admin-enabled` 인수입니다.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Hello 레지스트리를 만든 후 Azure CLI hello 비슷한 toohello 다음 데이터를 출력 합니다. Hello를 메모해 `name` 및 `loginServer`, 이후 단계에서 사용 됩니다.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Hello 컨테이너 레지스트리 자격 증명 hello를 사용 하 여 가져오기 [az acr 자격 증명 표시](/cli/azure/acr/credential) 명령입니다. 대체 hello `--name` hello 마지막 단계에서 기록한 하나 hello로 합니다. 이후 단계에서 필요하므로 하나의 암호를 기록해 둡니다.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Azure 컨테이너 레지스트리에 대 한 자세한 내용은 참조 하십시오. [소개 tooprivate Docker 컨테이너 레지스트리에](../../container-registry/container-registry-intro.md)합니다. 

## <a name="manage-acr-authentication"></a>ACR 인증 관리

개인 레지스트리에서 toopush 및 끌어오기 이미지는 toofirst hello 편리한 방법 hello 레지스트리를 인증 합니다. toodo hello를 사용 합니다, `docker login` tooaccess hello 개인 등록 해야 하는 모든 클라이언트에 명령 합니다. DC/OS 클러스터 노드가 여러 개인 경우 toobe ACR hello를 사용 하 여 인증을 해야는 모두 포함 될 수 있으므로 유용한 tooautomate이이 프로세스에서에서 각 노드에 있습니다. 

### <a name="create-shared-storage"></a>공유 저장소 만들기

이 프로세스는 hello 클러스터의 각 노드에서 탑재 된 경우 Azure 파일 공유를 사용 합니다. 아직 공유 저장소를 설정하지 않은 경우 [DC/OS 클러스터 내부에서 파일 공유 설정](container-service-dcos-fileshare.md)을 참조하세요.

### <a name="configure-acr-authentication"></a>ACR 인증 구성

먼저, hello를 hello DC/OS 마스터 및 변수에 저장의 FQDN을 가져옵니다.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

DC/OS 기반 클러스터의 hello 마스터 (또는 hello 첫 번째 마스터)에 대 한 SSH 연결을 만듭니다. 기본값이 아닌 값 hello 클러스터를 만들 때 사용 된 경우 hello 사용자 이름을 업데이트 합니다.

```azurecli-interactive
ssh azureuser@$FQDN
```

다음 명령 toologin toohello Azure 컨테이너 레지스트리 hello를 실행 합니다. Hello 대체 `--username` hello 컨테이너 레지스트리 및 hello hello 이름의 `--password` hello 제공 된 암호 중 하나를 사용 합니다. 마지막 인수 hello *mycontainerregistry.azurecr.io* hello 컨테이너 레지스트리 hello loginServer 이름의 hello 예제에서입니다. 

이 명령은 hello 인증 값 hello에서 로컬로 저장 `~/.docker` 경로입니다.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Hello 컨테이너 레지스트리 인증 값이 포함 된 압축된 파일을 만듭니다.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

이 파일 toohello 클러스터 공유 저장소에 복사 합니다. 이 단계를 수행 하면 hello 파일 hello DC/OS 클러스터의 모든 노드에서 사용할 수 있습니다.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>이미지 tooACR 업로드

이제 개발 컴퓨터 또는 설치 하는 Docker가 있는 다른 시스템에서 이미지 만들기와 toohello Azure 컨테이너 레지스트리 업로드 합니다.

Hello Ubuntu 이미지에서 컨테이너를 만듭니다.

```azurecli-interactive
docker run ubunut --name base-image
```

이제 새 이미지로 hello 컨테이너를 캡처하십시오. hello 이미지 이름 필요한 tooinclude hello `loginServer` hello 컨테이너 registrywith의 형식 이름 `loginServer/imageName`합니다.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Azure 컨테이너 레지스트리 hello에 로그인 합니다. Hello 이름을 hello loginServer 이름으로 바꿉니다, 그리고 hello-hello 컨테이너 레지스트리 및 hello-hello 제공 된 암호 중 하나에 포함 된 암호의 hello 이름으로 사용자 이름입니다.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Hello 이미지 toohello ACR 레지스트리를 마지막으로 업로드 합니다. 이 예제에서는 dcos-demo라는 이미지를 업로드합니다.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>ACR에서 이미지 실행

toouse hello ACR 레지스트리에서 이미지 파일 이름을 만들 *acrDemo.json* 복사 hello에 텍스트를 다음 및 합니다. 예를 들어 hello 이미지 이름을 hello 컨테이너 레지스트리 loginServer 이름 및 이미지 이름으로 대체 `loginServer/imageName`합니다. Hello를 메모해 `uris` 속성입니다. Hello hello 컨테이너 레지스트리 인증 파일 위치 hello DC/OS 클러스터의 각 노드에서 탑재 된 hello Azure 파일 공유에이 경우에이 속성을 보유 합니다.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

DC/OC CLI hello로 hello 응용 프로그램을 배포 합니다.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>다음 단계

이 자습서에서 DC/OS toouse hello 다음을 포함 하 여 Azure 컨테이너 레지스트리 작업을 구성할가 있습니다.

> [!div class="checklist"]
> * Azure Container Registry 배포(필요한 경우)
> * DC/OS 클러스터에서 ACR 인증 구성
> * 이미지 toohello Azure 컨테이너 레지스트리 업로드
> * Azure 컨테이너 레지스트리 hello에서 컨테이너 이미지를 실행 합니다.
