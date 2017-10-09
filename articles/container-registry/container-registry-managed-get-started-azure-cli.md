---
title: "aaaCreate 개인 Docker 컨테이너 레지스트리-Azure CLI | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure CLI 2.0 hello로 시작."
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 관리 되는 컨테이너 레지스트리 만들기

Azure Container Registry는 개인 Docker 컨테이너 이미지를 저장하는 데 사용되는 관리되는 Docker 컨테이너 레지스트리 서비스입니다. 이 가이드 hello Azure CLI를 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만드는 방법을 자세히 설명 합니다.

관리되는 Azure 컨테이너 레지스트리는 미리 보기 상태이며 일부 지역에서는 사용할 수 없습니다.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westcentralus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>컨테이너 레지스트리 만들기

Hello를 사용 하 여 ACR 인스턴스를 만들고 [az acr 만들기](/cli/azure/acr#create) 명령입니다.

> [!NOTE]
> 레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다.

 hello 예제에서 hello 레지스트리 이름이 *myContainerRegistry1*, 자신만의 고유 이름으로 대체 합니다.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Hello 레지스트리를 만들면 hello 출력은 유사한 toohello 다음.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>TooACR 인스턴스 로그인

밀어넣기 전에 컨테이너 이미지를 끌어오려면 toohello ACR 인스턴스 로그인 해야 합니다. 따라서 사용 하 여 hello toodo [az acr 로그인](/cli/azure/acr#login) 명령입니다.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

hello 명령은 완료 되 면 로그인 성공 메시지를 반환 합니다.

## <a name="use-azure-container-registry"></a>Azure Container Registry 사용

### <a name="list-container-images"></a>컨테이너 이미지 나열

사용 하 여 hello `az acr` CLI 명령을 tooquery hello 이미지와 저장소의 태그입니다.

> [!NOTE]
> 현재 컨테이너 레지스트리 hello 지원 하지 않는 `docker search` 이미지 및 태그에 대 한 명령 tooquery 합니다.

### <a name="list-repositories"></a>리포지토리 나열

hello 다음 예에서는 나열 JSON (JavaScript Object Notation) 형식의 레지스트리에 hello 저장소:

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>태그 나열

hello 다음 예에서는 나열 hello hello 태그 **샘플/nginx** JSON 형식의 저장소:

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>다음 단계

이 빠른 시작 hello Azure CLI를 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만들었습니다.

> [!div class="nextstepaction"]
> [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
