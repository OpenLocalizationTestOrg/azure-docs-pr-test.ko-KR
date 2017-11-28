---
title: "Azure 클라우드에서 aaaDocker 컨테이너 호스팅 | Microsoft Docs"
description: "Azure 컨테이너 서비스 방식으로 toosimplify hello 만들기, 구성 및 관리는 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 제공 합니다."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 46a0071a7497a3ff44d75413b49f1d06f844c446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodocker-container-hosting-solutions-with-azure-container-service"></a><span data-ttu-id="30ead-104">Azure 컨테이너 서비스를 사용 하 여 솔루션을 호스팅 소개 tooDocker 컨테이너</span><span class="sxs-lookup"><span data-stu-id="30ead-104">Introduction tooDocker container hosting solutions with Azure Container Service</span></span> 
<span data-ttu-id="30ead-105">Azure 컨테이너 서비스 간단 하 게 드립니다 toocreate 구성 하 고 미리 구성 된 toorun 컨테이너 화 가능한 응용 프로그램이 있는 가상 컴퓨터의 클러스터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-105">Azure Container Service makes it simpler for you toocreate, configure, and manage a cluster of virtual machines that are preconfigured toorun containerized applications.</span></span> <span data-ttu-id="30ead-106">Azure 컨테이너 서비스는 일반적인 오픈 소스 예약 및 오케스트레이션 도구의 최적화된 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-106">It uses an optimized configuration of popular open-source scheduling and orchestration tools.</span></span> <span data-ttu-id="30ead-107">Toouse 있습니다를 통해 기존 기술을 사용 하면이 커뮤니티 전문, toodeploy 크기가 크고 점점 본문에 대해 하 고 Microsoft Azure에서 컨테이너 기반 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-107">This enables you toouse your existing skills, or draw upon a large and growing body of community expertise, toodeploy and manage container-based applications on Microsoft Azure.</span></span>

![Azure 컨테이너 서비스를 통해 toomanage 컨테이너 화 가능한 응용 프로그램 Azure에서 여러 호스트에 있습니다.](./media/acs-intro/acs-cluster-new.png)

<span data-ttu-id="30ead-109">Azure 컨테이너 서비스는 hello Docker 컨테이너 형식 tooensure 응용 프로그램 컨테이너가 완전히 이식 가능를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-109">Azure Container Service leverages hello Docker container format tooensure that your application containers are fully portable.</span></span> <span data-ttu-id="30ead-110">또한 컨테이너의 이러한 응용 프로그램 toothousands 또는 짝수 수만 확장할 수 있도록 선택 하는 풀 마라톤 및 DC/OS, docker는 Docker Swarm 또는 Kubernetes 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-110">It also supports your choice of Marathon and DC/OS, Docker Swarm, or Kubernetes so that you can scale these applications toothousands of containers, or even tens of thousands.</span></span>

<span data-ttu-id="30ead-111">Azure 컨테이너 서비스를 사용 하면 응용 프로그램 이식성-hello 오케스트레이션 계층에서 이식성을 포함 하 여 그대로 유지 하면서 Azure의 엔터프라이즈급 기능을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-111">By using Azure Container Service, you can take advantage of the enterprise-grade features of Azure, while still maintaining application portability--including portability at hello orchestration layers.</span></span>

## <a name="using-azure-container-service"></a><span data-ttu-id="30ead-112">Azure 컨테이너 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="30ead-112">Using Azure Container Service</span></span>
<span data-ttu-id="30ead-113">Azure 컨테이너 서비스와 이러한 목표는 오픈 소스 도구와 기술을 담아 고객 사이에서 인기 오늘을 통해 tooprovide 컨테이너 호스팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-113">Our goal with Azure Container Service is tooprovide a container hosting environment by using open-source tools and technologies that are popular among our customers today.</span></span> <span data-ttu-id="30ead-114">toothis 끝 (DC/OS, docker는 Docker Swarm 또는 Kubernetes) 하 여 선택한 orchestrator에 대 한 hello 표준 API 끝점 공개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-114">toothis end, we expose hello standard API endpoints for your chosen orchestrator (DC/OS, Docker Swarm, or Kubernetes).</span></span> <span data-ttu-id="30ead-115">이러한 끝점을 사용 하 여 toothose 끝점 통신의 대상이 될 수 있는 모든 소프트웨어를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-115">By using these endpoints, you can leverage any software that is capable of talking toothose endpoints.</span></span> <span data-ttu-id="30ead-116">예를 들어 hello docker는 Docker Swarm 끝점의 경우 hello toouse hello Docker CLI (명령줄 인터페이스)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-116">For example, in hello case of hello Docker Swarm endpoint, you might choose toouse hello Docker command-line interface (CLI).</span></span> <span data-ttu-id="30ead-117">DC/OS 용 hello DCOS CLI를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-117">For DC/OS, you might choose hello DCOS CLI.</span></span> <span data-ttu-id="30ead-118">Kubernetes의 경우 `kubectl`을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-118">For Kubernetes, you might choose `kubectl`.</span></span>

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a><span data-ttu-id="30ead-119">Azure 컨테이너 서비스를 사용하여 Docker 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="30ead-119">Creating a Docker cluster by using Azure Container Service</span></span>
<span data-ttu-id="30ead-120">Azure 컨테이너 서비스를 사용 하 여 toobegin hello 포털을 통해 Azure 컨테이너 서비스 클러스터를 배포할 (마켓플레이스 검색 hello에 대 한 **Azure 컨테이너 서비스**), Azure 리소스 관리자 템플릿을 사용 하 여 ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), 또는 [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), 또는 hello로 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-120">toobegin using Azure Container Service, you deploy an Azure Container Service cluster via hello portal (search hello Marketplace for **Azure Container Service**), by using an Azure Resource Manager template ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), or [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)), or with hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span></span> <span data-ttu-id="30ead-121">hello 제공 퀵 스타트 서식 파일 수정된 tooinclude 추가 또는 고급 Azure 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-121">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="30ead-122">자세한 내용은 [Azure Container Service 클러스터 배포](container-service-deployment.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30ead-122">For more information, see [Deploy an Azure Container Service cluster](container-service-deployment.md).</span></span>

## <a name="deploying-an-application"></a><span data-ttu-id="30ead-123">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="30ead-123">Deploying an application</span></span>
<span data-ttu-id="30ead-124">Azure Container Service는 오케스트레이션을 위해 Docker Swarm, DC/OS 또는 Kubernetes 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-124">Azure Container Service provides a choice of Docker Swarm, DC/OS, or Kubernetes for orchestration.</span></span> <span data-ttu-id="30ead-125">응용 프로그램을 배포하는 방법은 선택한 Orchestrator에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-125">How you deploy your application depends on your choice of orchestrator.</span></span>

### <a name="using-dcos"></a><span data-ttu-id="30ead-126">DC/OS 사용</span><span class="sxs-lookup"><span data-stu-id="30ead-126">Using DC/OS</span></span>
<span data-ttu-id="30ead-127">DC/OS는 hello Apache Mesos 분산된 시스템 커널 기반 운영 체제를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-127">DC/OS is a distributed operating system based on hello Apache Mesos distributed systems kernel.</span></span> <span data-ttu-id="30ead-128">Apache Mesos hello Apache 소프트웨어 Foundation에 있는 컴퓨터의 목록과 hello 중 일부 [에서 가장 큰 이름을 IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) 사용자 및 참가자입니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-128">Apache Mesos is housed at hello Apache Software Foundation and lists some of hello [biggest names in IT](http://mesos.apache.org/documentation/latest/powered-by-mesos/) as users and contributors.</span></span>

![에이전트 및 마스터가 표시된 DC/OS에 대해 구성된 Azure Container Service.](media/acs-intro/dcos.png)

<span data-ttu-id="30ead-130">DC/OS 및 Apache Mesos는 다음과 같은 인상적인 기능 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-130">DC/OS and Apache Mesos include an impressive feature set:</span></span>

* <span data-ttu-id="30ead-131">입증된 확장성</span><span class="sxs-lookup"><span data-stu-id="30ead-131">Proven scalability</span></span>
* <span data-ttu-id="30ead-132">Apache ZooKeeper를 사용하는 내결함성 있는 복제된 마스터 및 슬레이브</span><span class="sxs-lookup"><span data-stu-id="30ead-132">Fault-tolerant replicated master and slaves using Apache ZooKeeper</span></span>
* <span data-ttu-id="30ead-133">Docker 형식의 컨테이너에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="30ead-133">Support for Docker-formatted containers</span></span>
* <span data-ttu-id="30ead-134">Linux 컨테이너를 사용하여 작업 간에 네이티브 격리</span><span class="sxs-lookup"><span data-stu-id="30ead-134">Native isolation between tasks with Linux containers</span></span>
* <span data-ttu-id="30ead-135">다중 리소스 예약(메모리, CPU, 디스크 및 포트)</span><span class="sxs-lookup"><span data-stu-id="30ead-135">Multiresource scheduling (memory, CPU, disk, and ports)</span></span>
* <span data-ttu-id="30ead-136">새로운 병렬 응용 프로그램을 개발하기 위한 Java, Python 및 C++ API</span><span class="sxs-lookup"><span data-stu-id="30ead-136">Java, Python, and C++ APIs for developing new parallel applications</span></span>
* <span data-ttu-id="30ead-137">클러스터 상태를 볼 수 있는 웹 UI</span><span class="sxs-lookup"><span data-stu-id="30ead-137">A web UI for viewing cluster state</span></span>

<span data-ttu-id="30ead-138">Azure 컨테이너 서비스에서 실행 중인 DC/OS는 기본적으로 작업을 예약 하기 위한 hello 마라톤 오케스트레이션 플랫폼을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-138">By default, DC/OS running on Azure Container Service includes hello Marathon orchestration platform for scheduling workloads.</span></span> <span data-ttu-id="30ead-139">그러나 hello ACS의 DC/OS 배포에 포함 된 hello Mesosphere Universe tooyour 서비스를 추가할 수 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-139">However, included with hello DC/OS deployment of ACS is hello Mesosphere Universe of services that can be added tooyour service.</span></span> <span data-ttu-id="30ead-140">Hello Universe에서에서 서비스에는 Spark, Hadoop, Cassandra, 및 등 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-140">Services in hello Universe include Spark, Hadoop, Cassandra, and much more.</span></span>

![Azure 컨테이너 서비스의 DC/OS Universe](media/dcos/universe.png)

#### <a name="using-marathon"></a><span data-ttu-id="30ead-142">Marathon 사용</span><span class="sxs-lookup"><span data-stu-id="30ead-142">Using Marathon</span></span>
<span data-ttu-id="30ead-143">풀 마라톤은 클러스터 전체 init 및 cgroups-또는 hello 경우 Docker로 포맷 된 컨테이너 Azure 컨테이너 서비스의 서비스 제어 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-143">Marathon is a cluster-wide init and control system for services in cgroups--or, in hello case of Azure Container Service, Docker-formatted containers.</span></span> <span data-ttu-id="30ead-144">Marathon은 응용 프로그램을 배포할 수 있는 웹 UI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-144">Marathon provides a web UI from which you can deploy your applications.</span></span> <span data-ttu-id="30ead-145">사용자는 배포 시 DNS\_PREFIX 및 REGION이 모두 정의된 `http://DNS_PREFIX.REGION.cloudapp.azure.com`과 유사한 URL에서 웹 UI에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-145">You can access this at a URL that looks something like `http://DNS_PREFIX.REGION.cloudapp.azure.com` where DNS\_PREFIX and REGION are both defined at deployment time.</span></span> <span data-ttu-id="30ead-146">물론, 사용자는 자체 DNS 이름을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-146">Of course, you can also provide your own DNS name.</span></span> <span data-ttu-id="30ead-147">Hello 마라톤 웹 UI를 사용 하 여 컨테이너의 실행에 대 한 자세한 내용은 참조 하십시오. [hello 마라톤 웹 UI 통해 DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-147">For more information on running a container using hello Marathon web UI, see [DC/OS container management through hello Marathon web UI](container-service-mesos-marathon-ui.md).</span></span>

![Marathon 응용 프로그램 목록](media/dcos/marathon-applications-list.png)

<span data-ttu-id="30ead-149">또한 풀 마라톤와 통신 하기 위한 hello REST Api를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-149">You can also use hello REST APIs for communicating with Marathon.</span></span> <span data-ttu-id="30ead-150">각 도구에 사용할 수 있는 여러 클라이언트 라이브러리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-150">There are a number of client libraries that are available for each tool.</span></span> <span data-ttu-id="30ead-151">다양 한 언어-를 포함 하 고 물론, 모든 언어에서 hello HTTP 프로토콜을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-151">They cover a variety of languages--and, of course, you can use hello HTTP protocol in any language.</span></span> <span data-ttu-id="30ead-152">또한 인기 있는 다양한 DevOps 도구는 Marathon에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-152">In addition, many popular DevOps tools provide support for Marathon.</span></span> <span data-ttu-id="30ead-153">Azure 컨테이너 서비스 클러스터를 사용하여 작업하는 경우 운영 팀에 최대의 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-153">This provides maximum flexibility for your operations team when you are working with an Azure Container Service cluster.</span></span> <span data-ttu-id="30ead-154">Hello 마라톤 REST API를 사용 하 여 컨테이너의 실행에 대 한 자세한 내용은 참조 하십시오. [hello 마라톤 REST API를 통해 DC/OS 컨테이너 관리](container-service-mesos-marathon-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-154">For more information on running a container by using hello Marathon REST API, see [DC/OS container management through hello Marathon REST API](container-service-mesos-marathon-rest.md).</span></span>

### <a name="using-docker-swarm"></a><span data-ttu-id="30ead-155">Docker Swarm 사용</span><span class="sxs-lookup"><span data-stu-id="30ead-155">Using Docker Swarm</span></span>
<span data-ttu-id="30ead-156">Docker Swarm은 Docker에 대한 네이티브 클러스터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-156">Docker Swarm provides native clustering for Docker.</span></span> <span data-ttu-id="30ead-157">Docker는 Docker Swarm 사용 되므로 표준 Docker API hello, 이미 Docker 디먼을와 통신 하는 모든 도구 Azure 컨테이너 서비스에서 웜 tootransparently 눈금 toomultiple 호스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-157">Because Docker Swarm serves hello standard Docker API, any tool that already communicates with a Docker daemon can use Swarm tootransparently scale toomultiple hosts on Azure Container Service.</span></span>

![Azure 컨테이너 서비스 toouse 웜을 구성합니다.](media/acs-intro/acs-swarm2.png)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="30ead-159">웜 클러스터에서 컨테이너 관리를 위한 지원 되는 도구를 포함 하지만 hello 다음으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-159">Supported tools for managing containers on a Swarm cluster include, but are not limited to, hello following:</span></span>

* <span data-ttu-id="30ead-160">Dokku</span><span class="sxs-lookup"><span data-stu-id="30ead-160">Dokku</span></span>
* <span data-ttu-id="30ead-161">Docker CLI 및 Docker Compose</span><span class="sxs-lookup"><span data-stu-id="30ead-161">Docker CLI and Docker Compose</span></span>
* <span data-ttu-id="30ead-162">Krane</span><span class="sxs-lookup"><span data-stu-id="30ead-162">Krane</span></span>
* <span data-ttu-id="30ead-163">Jenkins</span><span class="sxs-lookup"><span data-stu-id="30ead-163">Jenkins</span></span>

### <a name="using-kubernetes"></a><span data-ttu-id="30ead-164">Kubernetes 사용</span><span class="sxs-lookup"><span data-stu-id="30ead-164">Using Kubernetes</span></span>
<span data-ttu-id="30ead-165">Kubernetes는 인기 있는 프로덕션급 오픈 소스 컨테이너 오케스트레이터 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-165">Kubernetes is a popular open-source, production-grade container orchestrator tool.</span></span> <span data-ttu-id="30ead-166">Kubernetes는 컨테이너화된 응용 프로그램의 배포, 크기 조정 및 관리를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-166">Kubernetes automates deployment, scaling, and management of containerized applications.</span></span> <span data-ttu-id="30ead-167">있기 때문에 오픈 소스 솔루션 hello 오픈 소스 커뮤니티를 통해 생성, Azure 컨테이너 서비스에 원활 하 게 실행 되며 Azure 컨테이너 서비스에서 크기 조정에 사용 되는 toodeploy 컨테이너 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-167">Because it is an open-source solution and is driven by hello open-source community, it runs seamlessly on Azure Container Service and can be used toodeploy containers at scale on Azure Container Service.</span></span>

![Azure 컨테이너 서비스 toouse Kubernetes를 구성합니다.](media/acs-intro/kubernetes.png)

<span data-ttu-id="30ead-169">여기에는 다음과 같이 풍부한 기능들이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-169">It has a rich set of features including:</span></span>
* <span data-ttu-id="30ead-170">수평적 크기 조정</span><span class="sxs-lookup"><span data-stu-id="30ead-170">Horizontal scaling</span></span>
* <span data-ttu-id="30ead-171">서비스 검색 및 부하 분산</span><span class="sxs-lookup"><span data-stu-id="30ead-171">Service discovery and load balancing</span></span>
* <span data-ttu-id="30ead-172">비밀 및 구성 관리</span><span class="sxs-lookup"><span data-stu-id="30ead-172">Secrets and configuration management</span></span>
* <span data-ttu-id="30ead-173">API 기반 자동화된 롤아웃 및 롤백</span><span class="sxs-lookup"><span data-stu-id="30ead-173">API-based automated rollouts and rollbacks</span></span>
* <span data-ttu-id="30ead-174">자동 복구</span><span class="sxs-lookup"><span data-stu-id="30ead-174">Self-healing</span></span>

## <a name="videos"></a><span data-ttu-id="30ead-175">비디오</span><span class="sxs-lookup"><span data-stu-id="30ead-175">Videos</span></span>
<span data-ttu-id="30ead-176">Azure Container Service 시작(101):</span><span class="sxs-lookup"><span data-stu-id="30ead-176">Getting started with Azure Container Service (101):</span></span>  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

<span data-ttu-id="30ead-177">구성 응용 프로그램에서 사용 하 여 hello Azure 컨테이너 서비스 (빌드 2016)</span><span class="sxs-lookup"><span data-stu-id="30ead-177">Building Applications Using hello Azure Container Service (Build 2016)</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a><span data-ttu-id="30ead-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30ead-178">Next steps</span></span>

<span data-ttu-id="30ead-179">Hello를 사용 하 여 컨테이너 서비스 클러스터 배포 [포털](container-service-deployment.md) 또는 [Azure CLI 2.0](container-service-create-acs-cluster-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30ead-179">Deploy a container service cluster using hello [portal](container-service-deployment.md) or [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).</span></span>
