---
title: "aaaMonitor Azure DC/OS 클러스터 Datadog | Microsoft Docs"
description: "Datadog를 사용하여 Azure 컨테이너 서비스 클러스터를 모니터링합니다. Hello DC/OS 웹 UI toodeploy hello Datadog 에이전트 tooyour 클러스터를 사용 합니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "컨테이너, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="8ebc4-105">Datadog을 사용하여 Azure Container Service DC/OS 클러스터를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="8ebc4-106">이 문서에서는 Azure 컨테이너 서비스 클러스터의 Datadog 에이전트 tooall hello 에이전트 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="8ebc4-107">이러한 구성을 위해서는 Datadog 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8ebc4-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8ebc4-108">Prerequisites</span></span>
<span data-ttu-id="8ebc4-109">Azure Container Service를 통해 구성된 클러스터를 [배포](container-service-deployment.md) 및 [연결](../container-service-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="8ebc4-110">Hello 탐색 [마라톤 UI](container-service-mesos-marathon-ui.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="8ebc4-111">너무 이동[http://datadoghq.com](http://datadoghq.com) tooset Datadog 계정.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="8ebc4-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="8ebc4-112">Datadog</span></span>
<span data-ttu-id="8ebc4-113">Datadog은 Azure 컨테이너 서비스 클러스터 내의 컨테이너에서 모니터링 데이터를 수집하는 모니터링 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="8ebc4-114">Datadog에는 컨테이너 내에서 특정 메트릭을 볼 수 있는 Docker 통합 대시보드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="8ebc4-115">컨테이너에서 수집된 메트릭은 CPU, 메모리, 네트워크 및 I/O로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="8ebc4-116">Datadog은 메트릭을 컨테이너와 이미지로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="8ebc4-117">어떤 hello의 예로 UI 같습니다. 아래 사용이 CPU에 대 한.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Datadog UI](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="8ebc4-119">Marathon으로 Datadog 배포 구성</span><span class="sxs-lookup"><span data-stu-id="8ebc4-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="8ebc4-120">이러한 단계는 방법을 보여 줍니다 tooconfigure Datadog 마라톤을 사용 하는 응용 프로그램 tooyour 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="8ebc4-121">[http://localhost:80/](http://localhost:80/)을 통해 DC/OS UI에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="8ebc4-122">한 번에서 DC/OS UI를 탐색 하는 hello toohello hello에 있는 "영역" 왼쪽 위에서 아래로 다음을 검색 "Datadog" 하 고 "설치"를 클릭</span><span class="sxs-lookup"><span data-stu-id="8ebc4-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![DC/OS Universe hello 내에서 Datadog 패키지](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="8ebc4-124">이제 toocomplete hello 구성 Datadog 계정 또는 무료 평가판 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="8ebc4-125">로그인 되 면 toohello Datadog 웹 사이트에 toohello 왼쪽 모양과 tooIntegrations 다음-> 이동 [Api](https://app.datadoghq.com/account/settings#api)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API 키](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="8ebc4-127">Hello Datadog 구성 hello DC/OS Universe 내에 다음 API 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![DC/OS Universe hello에 Datadog 구성](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="8ebc4-129">구성 이상 hello toohello 클러스터 Datadog에서 자동으로 에이전트 toothat 노드를 배포에 새 노드를 추가할 때마다 되므로 인스턴스 too10000000을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="8ebc4-130">이는 일시적인 해결책입니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-130">This is an interim solution.</span></span> <span data-ttu-id="8ebc4-131">뒤로 toohello Datadog 웹 사이트를 탐색 하 고 찾는 해야 hello 패키지를 설치 했으면 "[대시보드](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="8ebc4-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="8ebc4-132">여기에 사용자 지정 및 통합 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="8ebc4-133">hello [Docker 대시보드](https://app.datadoghq.com/screen/integration/docker) 클러스터 모니터링에 필요한 모든 hello 컨테이너 메트릭 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="8ebc4-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

