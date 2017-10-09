---
title: "Azure Kubernetes에 투구를 사용 하 여 aaaDeploy 컨테이너 | Microsoft Docs"
description: "Azure 컨테이너 서비스의 Kubernetes 클러스터에서 hello 투구 패키징 도구 toodeploy 컨테이너를 사용 하 여"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>투구 toodeploy 컨테이너 Kubernetes 클러스터에서 사용 하 여 

[투구](https://github.com/kubernetes/helm/) 설치 하 고 hello Kubernetes 응용 프로그램 수명 주기를 관리할 때 도움이 되는 오픈 소스 패키징 도구입니다. 예: Apt get 및 Yum 비슷한 tooLinux 패키지 관리자 투구 패키지인 미리 구성 된 Kubernetes 리소스의 사용 되는 toomanage Kubernetes 차트입니다. 이 문서 toowork 투구와 Kubernetes 클러스터에서 Azure 컨테이너 서비스에 배포 하는 방법을 보여 줍니다.

Helm에는 두 가지 구성 요소가 있습니다. 
* hello **투구 CLI** hello 클라우드 또는 로컬 컴퓨터에서 실행 되는 클라이언트  

* **Tiller** 는 hello Kubernetes 클러스터에서 실행 되 고 Kubernetes 응용 프로그램의 hello 수명 주기 관리 하는 서버 
 
## <a name="prerequisites"></a>필수 조건

* Azure Container Service에서 [Kubernetes 클러스터 생성](container-service-kubernetes-walkthrough.md)

* 로컬 컴퓨터에서 [설치 및 구성`kubectl`](../container-service-connect.md)

* 로컬 컴퓨터에 [Helm 설치](https://github.com/kubernetes/helm/blob/master/docs/install.md)

## <a name="helm-basics"></a>Helm 기초 

tooview 정보 hello Kubernetes 클러스터에 대 한 Tiller을 설치 하 고 hello 다음 명령을 입력 하 고 응용 프로그램의 배포:

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
투구를 설치한 후 hello 다음 명령을 입력 하 여 Tiller Kubernetes 클러스터에 설치 합니다.

```bash
helm init --upgrade
```
성공적으로 완료 hello 다음과 같은 출력을 볼 수 있습니다.

![Tiller 설치](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
모든 hello 투구 차트 사용할 수 있는 다음 형식 hello hello 리포지토리에 명령 tooview 있습니다.

```bash 
helm search 
```

Hello 다음과 같은 출력이 표시 됩니다.

![Helm 검색](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello 차트 tooget hello 최신 버전을 입력 합니다.

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Nginx 수신 컨트롤러 차트 배포 
 
toodeploy Nginx 수신 컨트롤러 차트는 단일 명령을 입력 합니다.

```bash
helm install stable/nginx-ingress 
```
![수신 컨트롤러 배포](./media/container-service-kubernetes-helm/nginx-ingress.png)

입력 하는 경우 `kubectl get svc` tooview IP 주소 toohello 수신 컨트롤러에 할당 되어 있는지 확인할 hello 클러스터에서 실행 되는 모든 서비스에 있습니다. (참조 hello 할당 진행 중이면 `<pending>`합니다. 걸리는 시간은 몇 분 toocomplete 가지.) 

Hello IP 주소를 할당 한 후 이동 toohello 값 hello 외부 IP 주소 toosee hello Nginx 백 엔드를 실행 합니다. 
 
![수신 IP 주소](./media/container-service-kubernetes-helm/ingress-ip-address.png)


클러스터를 형식에 설치 하는 막대형 차트의 목록 toosee:

```bash
helm list 
```

Hello 명령 너무 축약할 수 있습니다`helm ls`합니다.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>MariaDB 차트 및 클라이언트 배포

이제 MariaDB 차트 및 MariaDB 클라이언트 tooconnect toohello 데이터베이스를 배포 합니다.

toodeploy hello MariaDB 차트에서 다음 명령을 형식 hello:

```bash
helm install --name v1 stable/mariadb
```

여기서 `--name`은 릴리스에 사용되는 태그입니다.

> [!TIP]
> Hello 배포가 실패 하는 경우 실행 `helm repo update` 하 고 다시 시도 하십시오.
>
 
 
tooview 형식 클러스터에 배포 된 모든 hello 차트:

```bash 
helm list
```
 
tooview 클러스터에서 실행 중인 모든 배포를 입력 합니다.

```bash
kubectl get deployments 
``` 
 
 
마지막으로, toorun pod tooaccess hello 클라이언트를 입력 합니다.

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello 클라이언트에서 다음 명령을, 대체 형식 hello `v1-mariadb` 배포의 hello 이름의:

```bash
sudo mysql –h v1-mariadb
```
 
 
이제 표준 SQL 명령 toocreate 데이터베이스, 테이블 등을 사용할 수 있습니다. 예를 들어 `Create DATABASE testdb1;`은 빈 데이터베이스를 만듭니다. 
 
 
 
## <a name="next-steps"></a>다음 단계

* Kubernetes 차트를 관리 하는 방법에 대 한 자세한 내용은 참조 hello [투구 설명서](https://github.com/kubernetes/helm/blob/master/docs/index.md)합니다. 

