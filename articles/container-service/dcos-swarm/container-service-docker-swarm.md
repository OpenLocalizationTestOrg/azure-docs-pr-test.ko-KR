---
title: "Docker API와 Azure Swarm aaaManage 클러스터 | Microsoft Docs"
description: "Azure 컨테이너 서비스의 컨테이너 tooa docker는 Docker Swarm 클러스터 배포"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Docker Swarm을 통한 컨테이너 관리
Docker Swarm은 풀링된 Docker 호스트 집합에 컨테이너화된 워크로드를 배포하는 환경을 제공합니다. Docker 웜 hello native Docker API를 사용 합니다. docker는 Docker Swarm에서 컨테이너를 관리 하기 위한 hello 워크플로 거의 동일한 toowhat를 단일 컨테이너 호스트에 있게 됩니다. 이 문서는 Docker Swarm의 Azure 컨테이너 서비스 인스턴스에서 컨테이너화된 워크로드를 배포하는 간단한 예제를 제공합니다. Docker Swarm에 대한 보다 심층적인 설명서는 [Docker.com의 Docker Swarm](https://docs.docker.com/swarm/)을 참조하세요.

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

이 문서에 대 한 필수 구성 요소 toohello 연습:

[Azure 컨테이너 서비스에서 Swarm 클러스터 만들기](container-service-deployment.md)

[컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>새 컨테이너 배포
toocreate docker는 Docker Swarm hello에 새 컨테이너를 사용 하 여 hello `docker run` 명령 (위의 hello 필수 조건에 따라 SSH 터널 toohello 마스터 열었는지 확인). 이 예제는 hello에서 컨테이너를 만듦 `yeasy/simple-web` 이미지:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

사용 하 여 hello 컨테이너를 만든 후 `docker ps` hello 컨테이너에 대 한 tooreturn 정보입니다. Hello 컨테이너를 호스팅하는 hello 웜 에이전트에 나열 된 여기를 확인 합니다.

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

이제 hello 공용 DNS 이름 hello 웜 에이전트 부하 분산 장치를 통해이 컨테이너에서 실행 되는 hello 응용 프로그램을 액세스할 수 있습니다. Hello Azure 포털에서에서이 정보를 찾을 수 있습니다.  

![실제 방문 결과](./media/container-service-docker-swarm/real-visit.jpg)  

기본적으로 hello 부하 분산 장치에 포트 80, 8080 및 443 열기. 다른 포트에서 tooconnect 원하는 할 경우 tooopen hello Azure 부하 분산 장치에 해당 포트 hello 에이전트 풀에 대 한 합니다.

## <a name="deploy-multiple-containers"></a>여러 컨테이너 배포
Hello 'docker run' 여러 번 실행 하 여 여러 컨테이너를 시작 될 때 사용할 수 있습니다 `docker ps` 명령 toosee를 hello 컨테이너 호스트에서 실행 되 고 있습니다. Hello 아래 예제에서는 세 개의 컨테이너가 분산 되어 균등 하 게 웜 에이전트가 세 hello:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Docker Compose를 사용하여 컨테이너 배포
여러 컨테이너의 Docker Compose tooautomate hello 배포 및 구성을 사용할 수 있습니다. toodo, 확인 하는 SSH (보안 셸) 터널을 만들었습니다 (위의 hello 필수 조건 참조) 해당 hello DOCKER_HOST 변수 설정.

로컬 시스템에 docker-compose.yml 파일을 만듭니다. toodo이를 사용 하 여이 [샘플](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml)합니다.

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

실행 `docker-compose up -d` toostart hello 컨테이너 배포:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

마지막으로 실행 중인 컨테이너 hello 목록이 반환 됩니다. 이 목록에는 Docker Compose를 사용 하 여 배포 된 hello 컨테이너 반영 합니다.

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

사용할 수는 물론 `docker-compose ps` tooexamine에만 컨테이너에 정의 된 hello 프로그램 `compose.yml` 파일입니다.

## <a name="next-steps"></a>다음 단계
[Docker Swarm에 대해 자세히 알아보기](https://docs.docker.com/swarm/)

