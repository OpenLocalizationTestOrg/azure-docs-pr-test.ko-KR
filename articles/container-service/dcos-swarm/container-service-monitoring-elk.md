---
title: "Azure DC/OS 클러스터-ELK 스택 aaaMonitor | Microsoft Docs"
description: "ELK(Elasticsearch, Logstash 및 Kibana)를 사용하여 Azure Container Service 클러스터에서 DC/OS 클러스터를 모니터링합니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, DC/OS, Azure, 모니터링, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="d3807-104">ELK를 사용하여 Azure Container Service 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="d3807-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="d3807-105">이 문서에서는 Azure 컨테이너 서비스에서 DC/OS 클러스터에 toodeploy hello ELK (Elasticsearch Logstash, Kibana) 스택 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d3807-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d3807-106">Prerequisites</span></span>
<span data-ttu-id="d3807-107">Azure Container Service를 통해 구성된 DC/OS 클러스터를 [배포](container-service-deployment.md) 및 [연결](../container-service-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="d3807-108">DC/OS 대시보드 hello 및 마라톤 서비스 탐색 [여기](container-service-mesos-marathon-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="d3807-109">또한 hello 설치 [부하 분산 장치 풀 마라톤](container-service-load-balancing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="d3807-110">ELK(Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="d3807-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="d3807-111">ELK 스택 Elasticsearch Logstash의 조합을 이며 Kibana 최종 tooend 스택을 제공 하는 사용 되는 toomonitor 수 있으며 클러스터의 로그를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="d3807-112">DC/OS 클러스터에 hello ELK 스택 구성</span><span class="sxs-lookup"><span data-stu-id="d3807-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="d3807-113">DC/OS UI를 통해 액세스 [http://localhost:80 /](http://localhost:80/) hello DC/OS UI 너무 탐색에서 한 번**Universe**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="d3807-114">검색 하 고 해당 특정 순서로 및 hello DC/OS Universe에서에서 Elasticsearch, Logstash, 및 Kibana를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="d3807-115">Toohello 전환 되는 경우 구성에 대 한 자세히 알아볼 수 있습니다 **고급 설치** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="d3807-119">ELK 컨테이너와 작동 하 고 실행은 한 번 hello tooenable Kibana toobe 마라톤 LB를 통해 액세스를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="d3807-120">너무 이동 **서비스** > **kibana**를 클릭 하 고 **편집** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="d3807-122">너무 설정/해제**JSON 모드** toohello 레이블 섹션 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="d3807-123">Tooadd 필요는 `"HAPROXY_GROUP": "external"` 항목이 여기에 표시 된 대로 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="d3807-124">**변경 내용 배포**를 클릭하면 컨테이너가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="d3807-126">Tooverify 하려는 경우 해당 Kibana hello haproxy와 대시보드는 서비스로 서 등록 haproxy와 9090 포트에서 실행 될 때 tooopen 포트 9090 hello 에이전트 클러스터에서를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="d3807-127">기본적으로에서는 포트 80, 8080 열고 443에서 DC/OS 에이전트 클러스터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="d3807-128">지침 tooopen 포트 공용 평가 제공 하 고 제공 [여기](container-service-enable-public-access.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="d3807-129">tooaccess hello haproxy와 대시보드를 열고 hello 마라톤 LB 관리 인터페이스에서: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="d3807-130">Toohello URL을 탐색 한 후 아래와 같이 hello haproxy와 대시보드를 참조 해야 및 Kibana에 대 한 서비스 항목을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="d3807-132">포트 5601에 배포 된 tooaccess hello Kibana 대시보드에 tooopen 포트 5601 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="d3807-133">[여기](container-service-enable-public-access.md)에 나와 있는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d3807-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="d3807-134">hello Kibana 대시보드를 엽니다. `http://localhost:5601`합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3807-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3807-135">Next steps</span></span>

* <span data-ttu-id="d3807-136">시스템 및 응용 프로그램 로그 전달 및 설정은 [ELK로 DC/OS에서 로그 관리](https://docs.mesosphere.com/1.8/administration/logging/elk/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3807-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="d3807-137">toofilter 로그 참조 [ELK 사용 하 여 로그 필터링](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3807-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

