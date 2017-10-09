---
title: "aaaCreate 개인 Docker 레지스트리-Azure 포털 | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure 포털 hello로 시작."
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 관리 되는 컨테이너 레지스트리 만들기

Azure Container Registry는 개인 Docker 컨테이너 이미지를 저장하는 데 사용되는 관리되는 Docker 컨테이너 레지스트리 서비스입니다. 이 가이드 hello Azure 포털을 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만드는 방법을 자세히 설명 합니다.

관리되는 Azure 컨테이너 레지스트리는 미리 보기 상태이며 일부 지역에서는 사용할 수 없습니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인

Azure 포털에서 http://portal.azure.com toohello에 로그인 합니다.

## <a name="create-a-container-registry"></a>컨테이너 레지스트리 만들기

1. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.

2. 에 대 한 검색 hello 마켓플레이스 **Azure 컨테이너 레지스트리** 선택 합니다.

3. 클릭 **만들기** hello ACR 만들기 블레이드가 열립니다.

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. Hello에 **Azure 컨테이너 레지스트리** 블레이드에서 hello 다음 정보를 입력 합니다. 완료하면 **만들기**를 클릭합니다.

    a. **레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다. 이 예제에서는 hello 레지스트리 이름이 *myAzureContainerRegistry1*, 되지만 대신 사용자 고유의의 고유 이름입니다. hello 이름에는 문자와 숫자만 포함할 수 있습니다.

    b. **리소스 그룹**: 기존 선택 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.

    c. **위치**: 여기서 hello 서비스는 Azure 데이터 센터 위치를 선택 [사용 가능한](https://azure.microsoft.com/regions/services/)와 같은 **미국 중남부**합니다.

    d. **관리: 사용자**:는 관리자 사용자 tooaccess hello 레지스트리를 사용 하도록 설정 합니다. Hello 레지스트리를 만든 후이 설정을 변경할 수 있습니다.

    e. **사용 하 여 관리 되는 레지스트리**: Select 예 toohave ACR 자동으로 hello 레지스트리 저장소 관리, webhook을 사용 하 고 AAD 인증을 사용 합니다.

    f. **가격 책정 계층**: 가격 책정 계층을 선택합니다. 자세한 내용은 ACR 가격 책정을 참조하세요.

## <a name="log-in-tooacr-instance"></a>TooACR 인스턴스 로그인

밀어넣기 전에 컨테이너 이미지를 끌어오려면 toohello ACR 인스턴스 로그인 해야 합니다. 

따라서, toodo hello Azure CLI 2.0을 사용 합니다. 필요한 경우 hello를 사용 하 여 Azure에 로그인 하는 첫째, [az 로그인](/cli/azure/#login) 명령입니다. 

```azurecli
az login
```

를 사용 하 여 hello [az acr 로그인](/cli/azure/acr#login) toohello Azure 컨테이너 레지스트리에서에서 toolog 명령입니다.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

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

이 빠른 시작 hello Azure 포털을 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만들었습니다.

> [!div class="nextstepaction"]
> [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
