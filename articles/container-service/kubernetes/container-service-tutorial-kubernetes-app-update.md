---
title: "aaaAzure 컨테이너 서비스 자습서-업데이트 응용 프로그램 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 업데이트"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Kubernetes에서 응용 프로그램 업데이트

Kubernetes에서 응용 프로그램을 배포한 후 새 컨테이너 이미지 또는 이미지 버전을 지정하여 업데이트할 수 있습니다. 응용 프로그램을 업데이트 하면 hello 배포의 일부분만 동시에 업데이트 되도록 hello 업데이트 배포를 준비 합니다. 준비 된이 업데이트 hello 응용 프로그램 tookeep hello 업데이트 하는 동안 실행을 사용 하도록 설정 하 고 배포 오류가 발생 하는 경우는 롤백 메커니즘을 제공 합니다. 

이 자습서에서는 6, 7 개의 hello 샘플 Azure 투표 응용 프로그램의 일부 업데이트 됩니다. 완료하는 작업은 다음과 같습니다.

> [!div class="checklist"]
> * Hello 프런트 엔드 응용 프로그램 코드 업데이트
> * 업데이트된 컨테이너 이미지 만들기
> * 푸시 hello 컨테이너 이미지 tooAzure 컨테이너 레지스트리
> * Hello 업데이트 된 컨테이너 이미지를 배포합니다.

후속 자습서에서는 Operations Management Suite은 구성 된 toomonitor hello Kubernetes 클러스터 있습니다.

## <a name="before-you-begin"></a>시작하기 전에

이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램, 컨테이너 레지스트리 tooAzure 및 만들어진 Kubernetes 클러스터 hello 이미지를 업로드 합니다. 그런 다음 hello 응용 프로그램 hello Kubernetes 클러스터에서 실행 합니다. 

이 단계를 완료 하지 않은 toofollow와 함께 사용할 경우 너무 반환[자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다. 

## <a name="update-application"></a>응용 프로그램 업데이트

이 자습서를 toocomplete hello 단계 해야 복제 hello Azure 투표 응용 프로그램의 복사본입니다. 필요한 경우 다음 명령을 hello로이 복제 된 복사본을 만듭니다.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

열기 hello `config_file.cfg` 코드 또는 텍스트 편집기로 파일입니다. Hello 복제 hello 리포지토리의 디렉터리를 다음으로이 파일을 찾을 수 있습니다.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Hello 값을 변경 `VOTE1VALUE` 및 `VOTE2VALUE`, hello 파일을 저장 합니다.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

사용 하 여 [docker 작성](https://docs.docker.com/compose/) toore-hello 프런트 엔드 이미지 및 업데이트 실행된 hello 응용 프로그램을 만듭니다.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>로컬에서 응용 프로그램 테스트

너무 찾아보기`http://localhost:8080` toosee hello 응용 프로그램을 업데이트 합니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>이미지 태그 지정 및 밀어넣기

태그 hello *azure 투표 프런트* hello loginServer hello 컨테이너 레지스트리를 사용 하 여 이미지입니다.

Azure 컨테이너 레지스트리를 사용 하 여 hello로 hello 로그인 서버 이름을 가져오는 [az acr 목록](/cli/azure/acr#list) 명령입니다.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

사용 하 여 [docker 태그](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello 이미지입니다. `<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

사용 하 여 [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello 이미지 tooyour 레지스트리 합니다. `<acrLoginServer>`를 해당 Azure Container Registry 로그인 서버 이름 또는 공개 레지스트리 호스트 이름으로 바꿉니다.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>업데이트된 응용 프로그램 배포

tooensure 최대 가동 시간 hello 응용 프로그램 pod의 여러 인스턴스를 실행 합니다. Hello로이 구성을 확인 [kubectl 가져오기 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.

```bash
kubectl get pod
```

출력:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Hello azure 투표 프런트 이미지를 실행 하는 여러 포드를 설정 하지 않은 경우 확장 hello *azure 투표 프런트* 배포 합니다.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

tooupdate hello 응용 프로그램을 사용 하 여 hello [kubectl 집합](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) 명령입니다. 업데이트 `<acrLoginServer>` 컨테이너 레지스트리 hello 로그인 서버 또는 호스트 이름을 사용 합니다.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

toomonitor hello 배포를 사용 하 여 hello [kubectl 가져오기 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다. Hello 업데이트 응용 프로그램을 배포할 때 사용자 포드 종료 되 고 hello 새 컨테이너 이미지를 사용 하 여 다시 만든 됩니다.

```azurecli-interactive
kubectl get pod
```

출력:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>업데이트된 응용 프로그램 테스트

Hello hello의 외부 IP 주소 가져오기 *azure 투표 프런트* 서비스입니다.

```azurecli-interactive
kubectl get service azure-vote-front
```

찾아보기 toohello IP 주소 toosee hello 응용 프로그램을 업데이트 합니다.

![Azure의 Kubernetes 클러스터 이미지](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 응용 프로그램을 업데이트 하 고이 업데이트 tooa Kubernetes 클러스터에 전달 합니다. 작업을 수행 하는 hello 완료 되었습니다.

> [!div class="checklist"]
> * 업데이트 된 hello 프런트 엔드 응용 프로그램 코드
> * 업데이트된 컨테이너 이미지 만들기
> * Hello 컨테이너 이미지 tooAzure 컨테이너 레지스트리 푸시
> * 업데이트는 배포 된 hello 응용 프로그램

이동 하는 방법에 대 한 다음 자습서 toolearn toohello toomonitor Operations Management Suite로 Kubernetes 합니다.

> [!div class="nextstepaction"]
> [OMS로 Kubernetes 모니터링](./container-service-tutorial-kubernetes-monitor.md)