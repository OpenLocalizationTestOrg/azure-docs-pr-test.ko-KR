---
title: "aaaAzure 컨테이너 서비스 자습서-ACR 준비 | Microsoft Docs"
description: "Azure Container Service 자습서 - ACR 준비"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Azure Container Registry 배포 및 사용

ACR(Azure Container Registry)은 Docker 컨테이너 이미지를 위한 Azure 기반의 개인 레지스트리입니다. 이 자습서를 통해 Azure 컨테이너 레지스트리 인스턴스 배포 하 고 컨테이너 이미지 tooit 푸시하여 7, 워크의 파트 2입니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * ACR(Azure Container Registry) 인스턴스 배포
> * ACR에 대한 컨테이너 이미지 태그 지정
> * Hello 이미지 tooACR를 업로드 하는 중

이후 자습서에서는 컨테이너 이미지를 안전하게 실행하기 위해 이 ACR 인스턴스를 Azure Container Service Kubernetes 클러스터와 통합합니다. 

## <a name="before-you-begin"></a>시작하기 전에

Hello에 [이전 자습서](./container-service-tutorial-kubernetes-prepare-app.md), 간단한 Azure 투표 응용 프로그램에 대 한 컨테이너 이미지를 생성 합니다. 이 자습서에서는이 이미지는 Azure 컨테이너 레지스트리 tooan이 푸시됩니다. Hello Azure 투표 앱 이미지를 만들지 않은 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다. 또는 hello 단계 여기에서 자세히 설명 된 컨테이너 이미지를 사용 합니다.

이 자습서에서는 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="deploy-azure-container-registry"></a>Azure Container Registry 배포

Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. 이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에서 만든 *westeurope* 영역입니다.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Azure 컨테이너 레지스트리 hello로 만들기 [az acr 만들기](/cli/azure/acr#create) 명령입니다. 컨테이너 레지스트리의 hello 이름 **고유 해야**합니다.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

이 자습서의 나머지에서는 hello 통해 "acrname" 자리 표시자로를 위해 사용 hello 컨테이너 레지스트리 선택한 이름입니다.

## <a name="container-registry-login"></a>컨테이너 레지스트리 로그인

이미지 tooit 푸시하기 전에 tooyour ACR 인스턴스 로그인 해야 합니다. 사용 하 여 hello [az acr 로그인](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello 작업 명령입니다. Tooprovide hello 고유한 이름을 만들 때 toohello 컨테이너 레지스트리를 제공 해야 합니다.

```azurecli
az acr login --name <acrName>
```

hello 명령은 완료 되 면 로그인 성공 메시지를 반환 합니다.

## <a name="tag-container-images"></a>컨테이너 이미지 태그 지정

각 컨테이너 이미지 필요 toobe hello 레지스트리 hello loginServer 이름의 태그를 지정 합니다. 이 태그는 컨테이너 이미지 tooan 이미지 레지스트리 푸시할 때 다음 라우팅에 사용 됩니다.

현재 이미지를 사용 하 여 hello 목록이 toosee [docker 이미지](https://docs.docker.com/engine/reference/commandline/images/) 명령입니다.

```bash
docker images
```

출력:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

tooget hello loginServer 이름 hello 다음 명령을 실행 합니다.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

이제 태그 hello *azure 투표 프런트* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다. 또한 추가 `:redis-v1` hello 이미지 이름의 toohello 끝입니다. 이 태그는 hello 이미지 버전을 나타냅니다.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

태그가 지정 되 면 [docker 이미지] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello 작업을 실행 합니다.

```bash
docker images
```

출력:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>이미지 tooregistry 푸시

Hello 푸시 *azure 투표 프런트* 이미지 toohello 레지스트리 합니다. 

다음 예제는 hello를 사용 하 여 hello ACR loginServer 이름을 사용자 환경에서 hello loginServer로 바꿉니다.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

이 작업은 몇 분 toocomplete입니다.

## <a name="list-images-in-registry"></a>레지스트리에서 이미지 나열

tooreturn tooyour Azure 컨테이너 레지스트리에 사용자 hello 밀어 넣은 이미지 목록 [az acr 리포지토리 목록](/cli/azure/acr/repository#list) 명령입니다. Hello 명령 hello ACR 인스턴스 이름으로 업데이트 합니다.

```azurecli
az acr repository list --name <acrName> --output table
```

출력:

```azurecli
Result
----------------
azure-vote-front
```

다음 toosee hello 태그 특정 이미지를 사용 하 여 hello [az acr 리포지토리 표시 태그](/cli/azure/acr/repository#show-tags) 명령입니다.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

출력:

```azurecli
Result
--------
redis-v1
```

자습서 완료 시 hello 컨테이너 이미지 전용 Azure 컨테이너 레지스트리 인스턴스에 저장 되었습니다. 이 이미지는 이후 자습서에서 ACR tooa Kubernetes 클러스터에서 배포 됩니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 ACS Kubernetes 클러스터에서 사용하기 위해 Azure Container Registry를 준비했습니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * Azure Container Registry 인스턴스 배포
> * ACR에 대한 컨테이너 이미지 태그 지정
> * 업로드 된 hello 이미지 tooACR

Azure에서 Kubernetes 클러스터를 배포 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [Kubernetes 클러스터 배포](./container-service-tutorial-kubernetes-deploy-cluster.md)