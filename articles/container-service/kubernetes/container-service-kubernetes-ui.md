---
title: "웹 UI와 aaaManage Azure Kubernetes 클러스터 | Microsoft Docs"
description: "Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스의 UI"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Kubernetes 웹 hello를 사용 하 여 Azure 컨테이너 서비스와 UI

## <a name="prerequisites"></a>필수 조건
이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.


또한 hello Azure CLI 2.0 있다고 가정 하 고 `kubectl` 도구가 설치 되어 있습니다.

Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.

```console
$ az --version
```

Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.

Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.

```console
$ kubectl version
```

`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>개요

### <a name="connect-toohello-web-ui"></a>Toohello 웹 UI를 연결 합니다.
실행 하 여 hello Kubernetes 웹 UI를 시작할 수 있습니다.

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

로컬 컴퓨터 toohello Kubernetes 웹 UI를 연결 합니다. 웹 브라우저 구성 tootalk tooa 보안 프록시를 열립니다.

### <a name="create-and-expose-a-service"></a>서비스 만들기 및 공개
1. Hello Kubernetes 웹 UI에서에서 클릭 **만들기** hello 상단 오른쪽 창에서 단추입니다.

    ![Kubernetes 만들기 UI](./media/container-service-kubernetes-ui/create.png)

    응용 프로그램을 만들기 시작할 수 있는 대화 상자가 열립니다.

2. Hello 이름을 `hello-nginx`합니다. 사용 하 여 hello [ `nginx` 에서 Docker 컨테이너](https://hub.docker.com/_/nginx/) 하 고이 웹 서비스의 세 개의 복제본을 배포 합니다.

    ![Kubernetes 포드 만들기 대화 상자](./media/container-service-kubernetes-ui/nginx.png)

3. **서비스**에서 **외부**를 선택하고 포트 80을 입력합니다.

    이 설정은 트래픽 toohello 세 개의 복제본에 부하를 분산 합니다.

    ![Kubernetes 서비스 만들기 대화 상자](./media/container-service-kubernetes-ui/service.png)

4. 클릭 **배포** toodeploy 이러한 컨테이너 및 서비스입니다.

    ![Kubernetes 배포](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>컨테이너 보기
클릭 한 후 **배포**, hello UI를 배포할 때 서비스의 뷰를 보여 줍니다.

![Kubernetes 상태](./media/container-service-kubernetes-ui/status.png)

Hello 원에는 각 Kubernetes 개체의 hello 상태 hello UI의 왼쪽 아래에서 확인할 수 있습니다 **포드**합니다. 부분적으로 원이 이면 다음 hello 개체 여전히 배포 하려고 합니다. 개체가 완전히 배포되면 녹색 확인 표시가 표시됩니다.

![Kubernetes가 배포됨](./media/container-service-kubernetes-ui/deployed.png)

모든 것이 실행 되 면 웹 서비스를 실행 하는 hello에 대 한 포드 toosee 회원님의 하나를 클릭 합니다.

![Kubernetes 포드](./media/container-service-kubernetes-ui/pods.png)

Hello에 **포드** 보기 이러한 컨테이너에서 사용 하는 hello CPU 및 메모리 리소스를 비롯 하 여 hello pod에 hello 컨테이너에 대 한 정보를 볼 수 있습니다.

![Kubernetes 리소스](./media/container-service-kubernetes-ui/resources.png)

Hello 리소스 보이지 않으면 해야 toowait 몇 분 정도 데이터 toopropagate 모니터링 hello에 대 한 합니다.

클릭 하 여 컨테이너에 대 한 toosee hello 로그 **로그를 볼**합니다.

![kubernetes 로그](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>서비스 보기
또한 toorunning 컨테이너에서 hello Kubernetes UI 만들었습니다 외부 `Service` 클러스터는 부하 분산 장치 toobring 트래픽 toohello 컨테이너를 제공 합니다.

Hello 왼쪽된 탐색 창에서 클릭 **서비스** tooview 모든 서비스 (있어야 하나만).

![Kubernetes 서비스](./media/container-service-kubernetes-ui/service-deployed.png)

해당 보기의 외부 끝점 (IP 주소) tooyour 서비스 할당 된 나타납니다.
해당 IP 주소를 클릭하면 부하 분산 장치 뒤에서 Nginx 컨테이너가 실행되는 것이 표시됩니다.

![nginx 보기](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>서비스 크기 조정
또한 tooviewing에 사용자 개체에 hello UI, 편집 하 고 hello Kubernetes API 개체를 업데이트할 수 있습니다.

먼저, 클릭 **배포** hello 남아 있는 서비스에 대 한 탐색 창 toosee hello 배포에에서 합니다.

해당 보기에 있는 경우 hello 복제 세트에 클릭 한 다음 클릭 **편집** hello 위쪽 탐색 모음에서:

![kubernetes 편집](./media/container-service-kubernetes-ui/edit.png)

Hello 편집 `spec.replicas` 필드 toobe `2`를 클릭 하 고 **업데이트**합니다.

따라서 프로그램 포드 중 하나를 삭제 하 여 복제본 toodrop tootwo hello 수가 됩니다.

 

