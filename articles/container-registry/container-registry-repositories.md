---
title: "컨테이너 레지스트리 리포지토리 aaaAzure | Microsoft Docs"
description: "어떻게 Docker 이미지에 대 한 toouse Azure 컨테이너 레지스트리 리포지토리"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Azure 컨테이너 레지스트리 리포지토리

Azure 컨테이너 레지스트리 toostore 컨테이너 이미지를 저장소에 있습니다. 리포지토리에 이미지를 저장하면 격리된 환경에 이미지 그룹(또는 이미지 버전)을 포함할 수 있습니다. 이미지 tooyour 레지스트리를 푸시할 때 이러한 저장소를 지정할 수 있습니다.


## <a name="prerequisites"></a>필수 조건
* **Azure Container Registry** - Azure 구독 내에서 컨테이너 레지스트리를 만듭니다. 예를 들어 hello를 사용 하 여 [Azure 포털](container-registry-get-started-portal.md) 또는 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)합니다.
* **Docker CLI** -는 Docker 호스트 및 액세스 hello Docker CLI 명령으로 로컬 컴퓨터를 tooset 설치 [Docker 엔진](https://docs.docker.com/engine/installation/)합니다.
* **이미지를 끌어오도록** -Docker 허브 레지스트리를 공개 하는 hello에서 이미지를 끌어오도록, 태그 및 tooyour 레지스트리 밀어 넣습니다. 방법에 대 한 지침은 밀어넣기 및 끌어오기 이미지, 참조 [푸시 Docker 이미지 tooAzure 개인 레지스트리](container-registry-get-started-docker-cli.md)합니다.


## <a name="viewing-repositories-in-hello-portal"></a>Hello 포털에서에서 저장소 보기

이미지 tooyour 컨테이너 레지스트리가 푸시, 되 면 hello 저장소 호스팅 hello Azure 포털의에서 hello 이미지 목록이 보입니다.

Hello의 hello 단계를 따른 경우 [Docker Push 이미지 tooAzure 개인 레지스트리](container-registry-get-started-docker-cli.md) 문서, 이제이 컨테이너 레지스트리에 Nginx 이미지를 있어야 합니다. Hello 지침의 일환으로, hello 이미지에 대 한 네임 스페이스를 지정 해야 합니다. Hello 아래 예제에서는 hello 명령 hello NGinx 이미지 toohello "예제" 리포지토리를 푸시합니다.

```
docker push myregistry.azurecr.io/samples/nginx
```
 Azure Container Registry는 다단계 리포지토리 네임스페이스를 지원합니다. 이 기능을 통해 이미지 관련된 tooa 특정 앱의 있습니다 toogroup 컬렉션 또는 앱 toospecific 개발 또는 운영 팀의 컬렉션입니다. 저장소 컨테이너 레지스트리에 대 한 자세한 정보는 tooread 참조 [Azure에서 개인 Docker 컨테이너 레지스트리에](container-registry-intro.md)합니다.

tooview hello 컨테이너 레지스트리 리포지토리:

1. Azure 포털 toohello에 로그인
2. Hello에 **Azure 컨테이너 레지스트리** 블레이드, tooinspect 원하는 선택 hello 레지스트리
3. Hello 레지스트리 블레이드에서 클릭 **저장소** toosee 모든 hello 저장소와 해당 이미지의 목록
4. (선택 사항) 특정 이미지 toosee 태그를 선택 합니다.

![Hello 포털에서 저장소](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>다음 단계
Hello 기본 사항을 배웠으므로 레지스트리를 사용 하 여 준비 toostart 됩니다! 예를 들어 컨테이너 이미지 tooan 배포를 시작할 [Azure 컨테이너 서비스](https://azure.microsoft.com/documentation/services/container-service/) 클러스터입니다.
