---
title: "aaaAzure 컨테이너 인스턴스 자습서-Azure 컨테이너 레지스트리 준비 | Microsoft Docs"
description: "Azure Container Instances 자습서 - Azure Container Registry 준비"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Azure Container Registry 배포 및 사용

세 부분으로 이루어진 자습서의 두 번째 부분입니다. Hello에 [이전 단계](./container-instances-tutorial-prepare-app.md), 컨테이너 이미지를 작성 하는 간단한 웹 응용 프로그램에 대해 만들어진 [Node.js](http://nodejs.org)합니다. 이 자습서에서는이 이미지는 Azure 컨테이너 레지스트리 tooan이 푸시됩니다. Hello 컨테이너 이미지를 만들지 않은 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-instances-tutorial-prepare-app.md)합니다. 

Azure 컨테이너 레지스트리 hello Docker 컨테이너 이미지에 대 한 Azure 기반, 사설 레지스트리입니다. 이 자습서는 Azure 컨테이너 레지스트리 인스턴스 배포 하 고 컨테이너 이미지 tooit 푸시하여 안내 합니다. 완료되는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * Azure Container Registry 인스턴스 배포
> * Azure Container Registry에 컨테이너 이미지 태그 지정
> * 이미지 tooAzure 컨테이너 레지스트리를 업로드 하는 중

이후 자습서에서 사용자 개인 레지스트리 tooAzure 컨테이너 인스턴스 hello 컨테이너를 배포 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 자습서에서는 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

## <a name="deploy-azure-container-registry"></a>Azure Container Registry 배포

Azure Container Registry를 배포할 때는 먼저 리소스 그룹이 필요합니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컬렉션입니다.

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. 이 예제에서는 리소스 그룹 이름이 *myResourceGroup* hello에서 만든 *eastus* 영역입니다.

```azurecli
az group create --name myResourceGroup --location eastus
```

Azure 컨테이너 레지스트리 hello로 만들기 [az acr 만들기](/cli/azure/acr#create) 명령입니다. 컨테이너 레지스트리의 hello 이름 **고유 해야**합니다. 다음 예제는 hello를 사용 하 여 hello 이름 *mycontainerregistry082*합니다.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

이 자습서의 나머지에서는 hello 전체에서 사용 하 여 `<acrname>` 선택한 hello 컨테이너 레지스트리 이름에 대 한 자리 표시자로 합니다.

## <a name="container-registry-login"></a>컨테이너 레지스트리 로그인

이미지 tooit 푸시하기 전에 tooyour ACR 인스턴스 로그인 해야 합니다. 사용 하 여 hello [az acr 로그인](https://docs.microsoft.com/en-us/cli/azure/acr#login) toocomplete hello 작업 명령입니다. Tooprovide hello 고유한 이름을 만들 때 toohello 컨테이너 레지스트리를 제공 해야 합니다.

```azurecli
az acr login --name <acrName>
```

hello 명령은 완료 되 면 로그인 성공 메시지를 반환 합니다.

## <a name="tag-container-image"></a>컨테이너 이미지 태그 지정

컨테이너 이미지 전용 레지스트리에서 toodeploy hello 이미지 필요 hello로 태그가 지정 된 toobe `loginServer` hello 레지스트리의 이름입니다.

현재 이미지를 사용 하 여 hello 목록이 toosee `docker images` 명령입니다.

```bash
docker images
```

출력:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

tooget hello loginServer 이름 hello 다음 명령을 실행 합니다.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

태그 hello *aci 자습서 앱* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다. 또한 추가 `:v1` hello 이미지 이름의 toohello 끝입니다. 이 태그는 hello 이미지 버전 번호를 나타냅니다.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

태그가 지정 되 면 실행 `docker images` tooverify hello 작업 합니다.

```bash
docker images
```

출력:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>푸시 이미지 tooAzure 컨테이너 레지스트리

Hello 푸시 *aci 자습서 앱* 이미지 toohello 레지스트리 합니다.

다음 예제는 hello를 사용 하 여 hello 컨테이너 레지스트리 loginServer 이름을 사용자 환경에서 hello loginServer로 바꿉니다.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Azure Container Registry에서 이미지 나열

tooreturn tooyour Azure 컨테이너 레지스트리에 사용자 hello 밀어 넣은 이미지 목록 [az acr 리포지토리 목록](/cli/azure/acr/repository#list) 명령입니다. Hello 명령 hello 컨테이너 레지스트리 이름으로 업데이트 합니다.

```azurecli
az acr repository list --name <acrName> --output table
```

출력:

```azurecli
Result
----------------
aci-tutorial-app
```

다음 toosee hello 태그 특정 이미지를 사용 하 여 hello [az acr 리포지토리 표시 태그](/cli/azure/acr/repository#show-tags) 명령입니다.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

출력:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure 컨테이너 레지스트리 Azure 컨테이너 인스턴스를 사용 하도록 준비 된 하 고 hello 컨테이너 이미지에 적용 되었습니다. 단계를 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * Azure Container Registry 인스턴스 배포
> * Azure Container Registry에 컨테이너 이미지 태그 지정
> * 이미지 tooAzure 컨테이너 레지스트리를 업로드 하는 중

Azure 컨테이너 인스턴스를 사용 하 여 hello 컨테이너 tooAzure 배포에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [컨테이너 tooAzure 컨테이너 인스턴스를 배포 합니다.](./container-instances-tutorial-deploy-app.md)
