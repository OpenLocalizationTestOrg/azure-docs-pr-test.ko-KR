---
title: "Azure DC/OS 클러스터에서 Vamp로 aaaCanary 버전 | Microsoft Docs"
description: "Toouse는 toocanary 릴리스 서비스 Vamp 하 고 스마트 트래픽 Azure 컨테이너 서비스 DC/OS 클러스터에서 필터링을 적용 하는 방법"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="03746-103">Azure Container Service DC/OS 클러스터에서 Vamp를 사용하여 마이크로 서비스 카나리아 릴리스</span><span class="sxs-lookup"><span data-stu-id="03746-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="03746-104">이 연습에서는 DC/OS 클러스터를 사용하여 Azure Container Service에 Vamp를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="03746-105">카나리아 म hello Vamp 데모 서비스 "sava" 놓은 다음 스마트 트래픽 필터링을 적용 하 여 hello 서비스 Firefox와의 비 호환성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="03746-106">이 연습에서 Vamp DC/OS 클러스터에서 실행 되지만 hello 조정자로 Kubernetes와 Vamp을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="03746-107">카나리아 릴리스 및 Vamp에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="03746-107">About canary releases and Vamp</span></span>


<span data-ttu-id="03746-108">[카나리아 릴리스](https://martinfowler.com/bliki/CanaryRelease.html)란 Netflix, Facebook, Spotify 등의 혁신적인 조직에서 채택한 영리한 배포 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="03746-109">문제를 줄이고, 안전망을 도입하고, 혁신을 가속화하는 합리적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="03746-110">그렇다면 왜 모든 회사에서 이 방법을 사용하지 않을까요?</span><span class="sxs-lookup"><span data-stu-id="03746-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="03746-111">CI/CD 파이프라인 tooinclude 카나리아 전략 확장 복잡성을 추가 하 고 광범위 한 devops 지식 및 전문 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="03746-112">도 시작 가져오기 전에 충분 한 tooblock 작은 회사 및 기업 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="03746-113">[Vamp](http://vamp.io/) 카나리아 해제 기능 tooyour 기본 컨테이너 스케줄러 전환한은 설계 된 오픈 소스 시스템 tooease이이 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="03746-114">Vamp의 카나리아 기능은 백분율 기반 롤아웃보다 우수합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="03746-115">트래픽 필터링 하 고 다양 한 조건에서 예를 들어 tootarget 특정 사용자, IP 범위 또는 장치에 따라 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="03746-116">Vamp는 성능 메트릭을 추적 및 분석하여 실제 데이터를 기반으로 자동화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="03746-117">오류 발생 시 자동으로 롤백하도록 설정하거나 부하 또는 대기 시간에 따라 개별 서비스 변형의 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="03746-118">DC/OS를 사용하여 Azure Container Service 설정</span><span class="sxs-lookup"><span data-stu-id="03746-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="03746-119">마스터 하나와 기본 크기의 에이전트 두 개가 있는 [DC/OS 클러스터를 배포](container-service-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="03746-120">[SSH 터널을 만들어](../container-service-connect.md) tooconnect toohello DC/OS 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="03746-121">이 문서에서는 로컬 포트 80에서 toohello 클러스터 터널을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="03746-122">Vamp 설치</span><span class="sxs-lookup"><span data-stu-id="03746-122">Set up Vamp</span></span>

<span data-ttu-id="03746-123">실행 중인 DC/OS 클러스터를가지고 Vamp hello DC/OS UI (http://localhost:80)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![DC/OS UI](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="03746-125">설치는 두 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03746-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="03746-126">**Elasticsearch를 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="03746-127">그런 다음 **Vamp 배포** hello Vamp DC/OS universe 패키지를 설치 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="03746-128">Elasticsearch 배포</span><span class="sxs-lookup"><span data-stu-id="03746-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="03746-129">Vamp는 메트릭 수집 및 집계에 사용할 Elasticsearch가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="03746-130">Hello를 사용할 수 있습니다 [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy 호환 Vamp Elasticsearch 스택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="03746-131">DC/OS UI hello에서 이동 너무**서비스** 클릭 **서비스 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="03746-132">선택 **JSON 모드** hello에서 **새 서비스 배포** 팝업 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![JSON 모드 선택](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="03746-134">다음 JSON hello에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-134">Paste in hello following JSON.</span></span> <span data-ttu-id="03746-135">이 구성은 1GB의 RAM 및 hello Elasticsearch 포트에는 기본적인 상태 검사를 hello 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="03746-136">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-136">Click **Deploy**.</span></span>

  <span data-ttu-id="03746-137">DC/OS hello Elasticsearch 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="03746-138">Hello에 진행률을 추적할 수 **서비스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="03746-138">You can track progress on hello **Services** page.</span></span>  

  ![Elasticsearch 배포](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="03746-140">Vamp 배포</span><span class="sxs-lookup"><span data-stu-id="03746-140">Deploy Vamp</span></span>

<span data-ttu-id="03746-141">Elasticsearch로 보고 되 면 **실행**, hello DC/OS Universe Vamp 패키지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="03746-142">너무 이동**Universe** 검색 한 **vamp**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="03746-143">![DC/OS universe의 Vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="03746-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="03746-144">클릭 **설치** 다음 toohello vamp 패키지를 선택 하 고 **고급 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="03746-145">아래로 스크롤하여 hello elasticsearch url 입력: `http://elasticsearch.marathon.mesos:9200`합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Elasticsearch URL 입력](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="03746-147">클릭 **검토 하 고 설치**, 클릭 **설치** toostart hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="03746-148">DC/OS가 모든 필수 Vamp 구성 요소를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="03746-149">Hello에 진행률을 추적할 수 **서비스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="03746-149">You can track progress on hello **Services** page.</span></span>
  
  ![universe 패키지로 Vamp 배포](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="03746-151">배포가 완료 되 면 hello Vamp UI를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![DC/OS의 Vamp 서비스](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp UI](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="03746-154">첫 번째 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="03746-154">Deploy your first service</span></span>

<span data-ttu-id="03746-155">Vamp가 실행 중이니, 청사진의 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="03746-156">가장 간단한 형태의 [Vamp 청사진](http://vamp.io/documentation/using-vamp/blueprints/) hello 끝점 (게이트웨이), 클러스터 및 toodeploy 서비스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="03746-157">사용 하 여 클러스터 toogroup hello 동일 카나리아 해제, A에 대 한 논리적 그룹으로 서비스의 여러 변형이 vamp / B 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="03746-158">이 시나리오에서는 [**sava**](https://github.com/magneticio/sava)라고 하는 샘플 모놀리식 응용 프로그램을 사용하며 버전은 1.0입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="03746-159">hello monolith magneticio/sava:1.0.0 아래 Docker 허브에 있는 Docker 컨테이너에 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03746-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="03746-160">포트 8080에서 hello 응용 프로그램을 정상적으로 실행 되지만 있습니다 tooexpose 아래 포트 9050이 경우.</span><span class="sxs-lookup"><span data-stu-id="03746-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="03746-161">간단한 청사진을 사용 하 여 Vamp 통해 hello 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="03746-162">너무 이동**배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="03746-163">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-163">Click **Add**.</span></span>

3. <span data-ttu-id="03746-164">붙여넣기를 수행 하는 hello에 YAML 세부 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="03746-165">이 청사진에는 서비스 변형이 하나뿐인 클러스터가 하나 포함되어 있으며 이후 단계에서 변경할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="03746-166">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-166">Click **Save**.</span></span> <span data-ttu-id="03746-167">Vamp은 hello 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="03746-168">hello 배포 hello에 나열 되어 **배포** 페이지.</span><span class="sxs-lookup"><span data-stu-id="03746-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="03746-169">Hello 배포 toomonitor의 상태를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-169">Click hello deployment toomonitor its status.</span></span>

![Vamp UI - sava 배포](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Vamp UI의 sava 서비스](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="03746-172">Hello에 나열 되는 두 게이트웨이 생성 됩니다 **게이트웨이** 페이지:</span><span class="sxs-lookup"><span data-stu-id="03746-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="03746-173">(포트 9050) 서비스를 실행 하는 안정적인 끝점 tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="03746-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="03746-174">Vamp가 관리하는 내부 게이트웨이(이 게이트웨이는 나중에 자세히 설명).</span><span class="sxs-lookup"><span data-stu-id="03746-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Vamp UI - sava 게이트웨이](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="03746-176">hello sava 서비스가 이제 배포 있지만 hello Azure 부하 분산 장치는 아직 tooforward 트래픽 tooit를 인식 하지 때문에 외부에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="03746-177">tooaccess hello 서비스 업데이트 hello Azure 네트워킹 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="03746-178">Hello Azure 네트워크 구성을 업데이트합니다</span><span class="sxs-lookup"><span data-stu-id="03746-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="03746-179">Vamp 배포 된 hello sava 서비스 노드에서 hello DC/OS 에이전트 9050 포트에서 안정적인 끝점을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="03746-180">외부 hello DC/OS 클러스터에서 tooaccess hello 서비스 같은 클러스터 배포에서 변경 내용을 toohello Azure 네트워크 구성이 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="03746-181">**Hello Azure 부하 분산 장치 구성** hello 에이전트에 대 한 (라는 리소스 hello **에이전트 lb xxxx dcos**) 상태 검색 및 포트 9050 toohello sava 인스턴스에서 규칙 tooforward 트래픽입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="03746-182">**업데이트 hello 네트워크 보안 그룹** hello 공용 에이전트에 대 한 (라는 리소스 hello **XXXX 에이전트-public이-nsg-XXXX**) 포트 9050 tooallow 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="03746-183">자세한 단계 toocomplete에 대 한 이러한 작업을 사용 하 여 hello Azure 포털에서 참조 [공용 액세스 tooan Azure 컨테이너 서비스 응용 프로그램 활성화](container-service-enable-public-access.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="03746-184">모든 포트 설정에 대해 포트 9050을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="03746-185">모든 항목을 만든 후 이동 toohello **개요** hello DC/OS 에이전트 부하 분산 장치의 블레이드 (라는 리소스 hello **에이전트 lb xxxx dcos**).</span><span class="sxs-lookup"><span data-stu-id="03746-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="03746-186">Hello **공용 IP 주소**, 9050 포트에서 주소 tooaccess sava hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Azure Portal - 공용 IP 주소 가져오기](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="03746-189">카나리아 릴리스 실행</span><span class="sxs-lookup"><span data-stu-id="03746-189">Run a canary release</span></span>

<span data-ttu-id="03746-190">이 응용 프로그램의 새 버전 toocanary 릴리스를 프로덕션 환경 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="03746-191">Magneticio/sava:1.1.0으로 컨테이너 화 된 것 되 toogo 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="03746-192">Vamp 쉽게 배포를 실행 하는 새 서비스 toohello를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="03746-193">이러한 "병합된" 서비스는 hello hello 클러스터의 기존 서비스와 함께 배포 되 고 0%의 가중치를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="03746-194">트래픽이 hello 트래픽 분배로 인해 조정 될 때까지 새로 병합 라우트된 tooa 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="03746-195">hello 가중치 슬라이더 hello Vamp UI에서에서 완전히 제어할 hello 분포를 증분 조정 (카나리아 릴리스) 이나 인스턴트 롤백 범위를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="03746-196">새로운 서비스 변형 병합</span><span class="sxs-lookup"><span data-stu-id="03746-196">Merge a new service variant</span></span>

<span data-ttu-id="03746-197">toomerge hello 새 sava 1.1 서비스 배포를 실행 하는 hello로:</span><span class="sxs-lookup"><span data-stu-id="03746-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="03746-198">Hello Vamp UI, 클릭 **청사진**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="03746-199">클릭 **추가** 및 붙여넣기를 수행 하는 hello에 YAML 세부 계획:이 청사진 hello 기존 클러스터 (sava_cluster) 내에서 새 서비스 (sava: 1.1.0) variant toodeploy에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="03746-200">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-200">Click **Save**.</span></span> <span data-ttu-id="03746-201">hello 청사진 저장 되 고 hello에 나열 된 **청사진** 페이지.</span><span class="sxs-lookup"><span data-stu-id="03746-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="03746-202">열기 hello 동작 메뉴를 클릭 한 hello sava: 1.1 청사진 **병합**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Vamp UI - 청사진](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="03746-204">선택 hello **sava** 배포 및 클릭 **병합**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![UI vamp-청사진 toodeployment 병합](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="03746-206">Vamp hello 새 sava: 1.1.0 서비스 variant sava: 1.0.0 hello에 함께 hello 청사진에 설명 된 배포 **sava_cluster** 의 hello 배포를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Vamp UI - 업데이트된 sava 배포](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="03746-208">hello **sava/sava_cluster/webport** 게이트웨이 (hello 클러스터 끝점)도 업데이트, sava: 1.1.0 배포 경로 toohello 새로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="03746-209">이 시점에서 트래픽이 라우팅됩니다 여기 (hello **가중치** too0% 설정).</span><span class="sxs-lookup"><span data-stu-id="03746-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Vamp UI - 클러스터 게이트웨이](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="03746-211">카나리아 릴리스</span><span class="sxs-lookup"><span data-stu-id="03746-211">Canary release</span></span>

<span data-ttu-id="03746-212">두 버전의 sava에에서 배포 된 hello 동일 클러스터 hello를 이동 하 여 서로 트래픽의 hello 배포를 조정 하세요 **가중치** 슬라이더 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="03746-213">클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) 다음 너무**가중치**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="03746-214">Hello 가중치 배포 too50%/50%를 설정 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Vamp UI - 게이트웨이 가중치 슬라이더](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="03746-216">Tooyour 브라우저와를 몇 번 더 hello sava 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="03746-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="03746-217">hello sava 응용 프로그램을 지금 sava: 1.0 및 1.1 sava: 페이지가 사이 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![sava1.0 및 sava1.1 서비스 교대](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="03746-219">이 교체 hello 페이지의 정적 자산 hello 캐싱 때문에 hello "Incognito" 또는 "Anonymous" 모드 브라우저의 가장 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="03746-220">트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="03746-220">Filter traffic</span></span>

<span data-ttu-id="03746-221">배포 후 sava:1.1.0에서 Firefox 브라우저 표시 문제를 일으키는 호환성 문제를 발견했다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="03746-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="03746-222">Vamp toofilter 들어오는 트래픽을 설정할 수 있으며 모든 Firefox 사용자 다시 안정적인 sava: 1.0.0 알려진 toohello 직접 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="03746-223">이 필터도 다른 모든 사용자의 hello tooenjoy hello 이점을 계속 되는 동안 확인 hello Firefox 사용자를 사용 하지 못하게 하는 바로 sava: 1.1.0 향상.</span><span class="sxs-lookup"><span data-stu-id="03746-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="03746-224">사용 하 여 vamp **조건** toofilter 트래픽 간의 게이트웨이의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="03746-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="03746-225">먼저 필터링 된 트래픽과 toohello 조건이 적용 tooeach 경로 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="03746-226">나머지 모든 트래픽이 toohello 게이트웨이 가중치 설정에 따라 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03746-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="03746-227">조건 toofilter 모든 Firefox 사용자를 만들 수 있고 이전 sava 1.0.0 toohello 가리킬 됩니다.:</span><span class="sxs-lookup"><span data-stu-id="03746-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="03746-228">Hello sava/sava_cluster/webport에 **게이트웨이** 페이지 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd는 **조건** toohello 경로 sava/sava_cluster/sava:1.0.0/webport 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="03746-229">Hello 조건을 입력 **사용자 에이전트 Firefox = =** 클릭 ![Vamp UI-저장](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="03746-230">Vamp 0%의 기본 강도 가진 hello 상태를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="03746-231">toostart 필터링 트래픽 tooadjust hello 조건 강도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="03746-232">클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **강도** toohello 조건을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="03746-233">집합 hello **강도** too100% 클릭 ![Vamp UI-저장](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="03746-234">이제 vamp hello 조건 (모든 Firefox 사용자) toosava:1.0.0 일치 하는 모든 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="03746-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![UI vamp-조건 toogateway 적용](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="03746-236">마지막으로 hello 게이트웨이 가중치 toosend 모든 나머지 트래픽 (모든 Firefox 아닌 사용자) toohello 새 sava: 1.1.0 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="03746-237">클릭 ![Vamp UI-편집](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) 다음 너무**가중치** 100%는 방향이 지정 된 toohello 경로 sava/sava_cluster/sava:1.1.0/webport hello 가중치 배포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="03746-238">Hello 조건에 의해 필터링 되지 않으면 모든 트래픽을 지정 된 toohello 새 sava: 1.1.0 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="03746-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="03746-239">toosee hello 필터 작업에서 두 개의 서로 다른 브라우저 (하나 Firefox 및 다른 브라우저)를 열고 둘 다에서 hello sava 서비스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="03746-240">다른 모든 브라우저는 방향이 지정 된 toosava:1.1.0 Firefox에 대 한 모든 요청에서 toosava:1.0.0, 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03746-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Vamp UI - 트래픽 필터링](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="03746-242">요약</span><span class="sxs-lookup"><span data-stu-id="03746-242">Summing up</span></span>

<span data-ttu-id="03746-243">이 문서에서 DC/OS 클러스터에 간략 한 소개 tooVamp.</span><span class="sxs-lookup"><span data-stu-id="03746-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="03746-244">먼저 Vamp를 까 배포 하 고에서 Azure 컨테이너 서비스 DC/OS를 실행 중인 클러스터 Vamp 청사진을 사용 하 여 서비스 hello 노출 된 끝점 (게이트웨이)에서 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="03746-245">또한 Vamp의 강력한 기능 일부 다루었습니다 우리: 병합을 새 서비스 variant toohello 배포를 실행 하 고 증분 소개 다음 트래픽 tooresolve 알려진된 호환성 문제를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="03746-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03746-246">Next steps</span></span>

* <span data-ttu-id="03746-247">Hello 통해 Vamp 동작을 관리 하는 방법에 대 한 자세한 내용은 [REST API Vamp](http://vamp.io/documentation/api/api-reference/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="03746-248">Node.js에서 Vamp 자동화 스크립트를 빌드하고 [Vamp 워크플로](http://vamp.io/documentation/tutorials/create-a-workflow/)로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03746-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="03746-249">추가 [VAMP 자습서](http://vamp.io/documentation/tutorials/overview/)를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="03746-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

