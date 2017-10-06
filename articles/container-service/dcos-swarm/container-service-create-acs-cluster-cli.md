---
title: "Docker 컨테이너 클러스터-Azure CLI aaaDeploy | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 Azure Container Service에 Kubernetes, DC/OS 또는 Docker Swarm 솔루션 배포"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>호스팅 솔루션 hello Azure CLI 2.0을 사용 하 여 Docker 컨테이너 배포

사용 하 여 hello `az acs` hello Azure CLI 2.0 toocreate 명령과 Azure 컨테이너 서비스에서 클러스터를 관리 합니다. Hello를 사용 하 여 Azure 컨테이너 서비스 클러스터를 배포할 수도 [Azure 포털](container-service-deployment.md) 또는 Azure 컨테이너 서비스 Api를 환영 합니다.

에 대 한 도움말 `az acs` 명령을 전달 hello `-h` tooany 명령 매개 변수입니다. 예: `az acs create -h`



## <a name="prerequisites"></a>필수 조건
사용 하 여 Azure 컨테이너 서비스 클러스터 toocreate hello Azure CLI 2.0를 수행 해야 합니다.
* Azure 계정([무료 평가판 받기](https://azure.microsoft.com/pricing/free-trial/))이 있어야 합니다.
* 설치 하 고 hello 설정 [Azure CLI 2.0](/cli/azure/install-az-cli2)

## <a name="get-started"></a>시작 
### <a name="log-in-tooyour-account"></a>Tooyour 계정에 로그인
```azurecli
az login 
```

에 표시 되는 메시지 toolog hello를 대화형으로 수행 합니다. 다른 메서드 toolog를 참조 하십시오. [Azure CLI 2.0 시작](/cli/azure/get-started-with-az-cli2)합니다.

### <a name="set-your-azure-subscription"></a>Azure 구독 설정

Azure 구독이 여러 개 있는 경우 hello 기본 구독을 설정 합니다. 예:

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>리소스 그룹 만들기
모든 클러스터에 대한 리소스 그룹을 만드는 것이 좋습니다. Azure Container Service가 [사용 가능](https://azure.microsoft.com/en-us/regions/services/)한 Azure 지역을 지정합니다. 예:

```azurecli
az group create -n acsrg1 -l "westus"
```
출력은 toohello 다음과 유사 합니다.

![리소스 그룹 만들기](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Azure Container Service 클러스터 만들기

toocreate 클러스터를 사용 하 여 `az acs create`합니다.
Hello 클러스터에 대 한 이름 및 hello 이전 단계에서 만든 hello 리소스 그룹의 hello 이름을 필수 매개 변수. 

다른 입력 집합 toodefault 값 (hello 화면에 다음 참조)은 해당 해당 스위치를 사용 하 여 덮어쓰지 않는 경우. 예를 들어 hello orchestrator tooDC/OS 기본으로 설정 됩니다. 고 하나를 지정 하지 않으면, DNS 이름 접두사 hello 클러스터 이름에 따라 생성 됩니다.

![az acs create 사용](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>기본값을 사용하는 빠른 `acs create`
SSH RSA 공개 키 파일을 설정한 경우 `id_rsa.pub` hello 기본 위치에 (또는 생성에 대 한 [Osx 및 Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../../virtual-machines/linux/ssh-from-windows.md)), hello 다음과 같은 명령을 사용 하 여:

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
SSH 공용 키가 없는 경우 다음 두 번째 명령을 사용합니다. 이 명령은 hello로 `--generate-ssh-keys` 스위치에서 만들어집니다.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

Hello 명령을 입력 하면 hello 클러스터 toobe 생성 될 때까지 10 분 정도 기다립니다. hello 명령 출력의 hello 마스터 및 에이전트 노드 및는 SSH 명령 tooconnect toohello 첫 번째 마스터 정규화 된 도메인 이름 (Fqdn)을 포함합니다. 다음은 축약된 출력입니다.

![이미지 ACS create](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> hello [Kubernetes 연습](../kubernetes/container-service-kubernetes-walkthrough.md) 표시 방법을 toouse `az acs create` 기본 값 toocreate는 Kubernetes 클러스터 합니다.
>

## <a name="manage-acs-clusters"></a>ACS 클러스터 관리

사용 하 여 추가 `az acs` toomanage 클러스터 명령입니다. 다음은 몇 가지 예제입니다.

### <a name="list-clusters-under-a-subscription"></a>구독 아래에 클러스터 나열

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>리소스 그룹의 클러스터 나열

```azurecli
az acs list -g acsrg1 --output table
```

![acs 목록](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>컨테이너 서비스 클러스터 세부 정보 표시

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs 표시](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>배율 hello 클러스터
에이전트 노드의 확장 및 축소가 모두 허용됩니다. 매개 변수를 hello `new-agent-count` hello 새 hello ACS 클러스터의 에이전트 수입니다.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>컨테이너 서비스 클러스터 삭제
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
이 명령은 생성 된 모든 리소스 (네트워크 및 저장소) hello 컨테이너 서비스를 만드는 동안 삭제 되지 않습니다. toodelete 모든 리소스를 쉽게 것이 좋습니다 고유한 리소스 그룹의 각 클러스터를 배포 합니다. 그런 다음 hello 클러스터는 더 이상 필요 하면 hello 리소스 그룹을 삭제 합니다.

## <a name="next-steps"></a>다음 단계
이제 클러스터가 작동하기 시작했으니 연결 및 관리 정보는 다음 문서를 참조하세요.

* [Tooan Azure 컨테이너 서비스 클러스터에 연결](../container-service-connect.md)
* [Azure 컨테이너 서비스 및 DC/OS로 작업](container-service-mesos-marathon-rest.md)
* [Azure 컨테이너 서비스 및 Docker Swarm으로 작업](container-service-docker-swarm.md)
* [Azure Container Service 및 Kubernetes로 작업](../kubernetes/container-service-kubernetes-walkthrough.md)