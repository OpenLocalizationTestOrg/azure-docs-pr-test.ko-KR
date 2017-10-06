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
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="ba752-104">Docker Swarm을 통한 컨테이너 관리</span><span class="sxs-lookup"><span data-stu-id="ba752-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="ba752-105">Docker Swarm은 풀링된 Docker 호스트 집합에 컨테이너화된 워크로드를 배포하는 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="ba752-106">Docker 웜 hello native Docker API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="ba752-107">docker는 Docker Swarm에서 컨테이너를 관리 하기 위한 hello 워크플로 거의 동일한 toowhat를 단일 컨테이너 호스트에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="ba752-108">이 문서는 Docker Swarm의 Azure 컨테이너 서비스 인스턴스에서 컨테이너화된 워크로드를 배포하는 간단한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="ba752-109">Docker Swarm에 대한 보다 심층적인 설명서는 [Docker.com의 Docker Swarm](https://docs.docker.com/swarm/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba752-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="ba752-110">이 문서에 대 한 필수 구성 요소 toohello 연습:</span><span class="sxs-lookup"><span data-stu-id="ba752-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="ba752-111">Azure 컨테이너 서비스에서 Swarm 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ba752-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="ba752-112">컨테이너 서비스를 Azure의 hello 웜 클러스터를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="ba752-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="ba752-113">새 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="ba752-113">Deploy a new container</span></span>
<span data-ttu-id="ba752-114">toocreate docker는 Docker Swarm hello에 새 컨테이너를 사용 하 여 hello `docker run` 명령 (위의 hello 필수 조건에 따라 SSH 터널 toohello 마스터 열었는지 확인).</span><span class="sxs-lookup"><span data-stu-id="ba752-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="ba752-115">이 예제는 hello에서 컨테이너를 만듦 `yeasy/simple-web` 이미지:</span><span class="sxs-lookup"><span data-stu-id="ba752-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="ba752-116">사용 하 여 hello 컨테이너를 만든 후 `docker ps` hello 컨테이너에 대 한 tooreturn 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="ba752-117">Hello 컨테이너를 호스팅하는 hello 웜 에이전트에 나열 된 여기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="ba752-118">이제 hello 공용 DNS 이름 hello 웜 에이전트 부하 분산 장치를 통해이 컨테이너에서 실행 되는 hello 응용 프로그램을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="ba752-119">Hello Azure 포털에서에서이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-119">You can find this information in hello Azure portal:</span></span>  

![실제 방문 결과](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="ba752-121">기본적으로 hello 부하 분산 장치에 포트 80, 8080 및 443 열기.</span><span class="sxs-lookup"><span data-stu-id="ba752-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="ba752-122">다른 포트에서 tooconnect 원하는 할 경우 tooopen hello Azure 부하 분산 장치에 해당 포트 hello 에이전트 풀에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="ba752-123">여러 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="ba752-123">Deploy multiple containers</span></span>
<span data-ttu-id="ba752-124">Hello 'docker run' 여러 번 실행 하 여 여러 컨테이너를 시작 될 때 사용할 수 있습니다 `docker ps` 명령 toosee를 hello 컨테이너 호스트에서 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="ba752-125">Hello 아래 예제에서는 세 개의 컨테이너가 분산 되어 균등 하 게 웜 에이전트가 세 hello:</span><span class="sxs-lookup"><span data-stu-id="ba752-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="ba752-126">Docker Compose를 사용하여 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="ba752-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="ba752-127">여러 컨테이너의 Docker Compose tooautomate hello 배포 및 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="ba752-128">toodo, 확인 하는 SSH (보안 셸) 터널을 만들었습니다 (위의 hello 필수 조건 참조) 해당 hello DOCKER_HOST 변수 설정.</span><span class="sxs-lookup"><span data-stu-id="ba752-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="ba752-129">로컬 시스템에 docker-compose.yml 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="ba752-130">toodo이를 사용 하 여이 [샘플](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="ba752-131">실행 `docker-compose up -d` toostart hello 컨테이너 배포:</span><span class="sxs-lookup"><span data-stu-id="ba752-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

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

<span data-ttu-id="ba752-132">마지막으로 실행 중인 컨테이너 hello 목록이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="ba752-133">이 목록에는 Docker Compose를 사용 하 여 배포 된 hello 컨테이너 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="ba752-134">사용할 수는 물론 `docker-compose ps` tooexamine에만 컨테이너에 정의 된 hello 프로그램 `compose.yml` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ba752-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba752-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba752-135">Next steps</span></span>
[<span data-ttu-id="ba752-136">Docker Swarm에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ba752-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

