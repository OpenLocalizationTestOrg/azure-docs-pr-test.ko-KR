---
title: "Azure Kubernetes aaaMonitor 클러스터 CoScale로 | Microsoft Docs"
description: "CoScale을 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="c3299-103">CoScale을 사용하여 Azure Container Service Kubernetes 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="c3299-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="c3299-104">이 문서에서는 보여줍니다 어떻게 toodeploy hello [CoScale](https://www.coscale.com/) 에이전트 toomonitor Azure 컨테이너 서비스의 클러스터 노드 및 프로그램 Kubernetes의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="c3299-105">이러한 구성을 위해서는 CoScale 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="c3299-106">CoScale 정보</span><span class="sxs-lookup"><span data-stu-id="c3299-106">About CoScale</span></span> 

<span data-ttu-id="c3299-107">CoScale은 여러 오케스트레이션 플랫폼의 모든 컨테이너에서 메트릭 및 이벤트를 수집하는 모니터링 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="c3299-108">CoScale은 Kubernetes 환경에 대한 전체 스택 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="c3299-109">Hello 스택의 모든 계층에 대 한 시각화 및 분석 제공: hello OS, Kubernetes, Docker 및 사용자 컨테이너 내에서 실행 되는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="c3299-110">CoScale 몇 가지 기본 제공 모니터링 대시보드를 제공 하 고 기본 제공 비정상 탐지 tooallow 연산자가 고 빠른 개발자 toofind 인프라 및 응용 프로그램 문제.</span><span class="sxs-lookup"><span data-stu-id="c3299-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="c3299-112">이 문서에 나와 있는 것 처럼 Kubernetes 클러스터 toorun SaaS 솔루션으로 CoScale에 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="c3299-113">원하는 tookeep 데이터 현장 CoScale 온-프레미스 설치에 사용할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c3299-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c3299-114">Prerequisites</span></span>

<span data-ttu-id="c3299-115">먼저 너무[CoScale 계정 만들기](https://www.coscale.com/free-trial)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="c3299-116">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="c3299-117">또한 hello 있다고 가정 `az` Azure CLI 및 `kubectl` 도구가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="c3299-118">Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="c3299-119">Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="c3299-120">Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="c3299-121">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="c3299-122">DaemonSet를 사용 하 여 hello CoScale 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="c3299-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="c3299-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) 는 hello 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스를 Kubernetes toorun에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="c3299-124">Hello CoScale 에이전트 같은 모니터링 에이전트를 실행 하기 위한 완벽 한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="c3299-125">TooCoScale에 로그인 한 후 이동 toohello [에이전트 페이지](https://app.coscale.com/) tooinstall CoScale 에이전트는 DaemonSet를 사용 하 여 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="c3299-126">hello CoScale UI는 에이전트 및 전체 Kubernetes 클러스터 모니터링 시작 안내 구성 단계 toocreate를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale 에이전트 구성](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="c3299-128">제공 된 hello 명령을 실행 하는 hello 클러스터에서 toostart hello 에이전트:</span><span class="sxs-lookup"><span data-stu-id="c3299-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Hello CoScale 에이전트 시작](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="c3299-130">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-130">That's it!</span></span> <span data-ttu-id="c3299-131">Hello 에이전트가 실행 되 면 되 면 hello 콘솔의에서 데이터를 몇 분 안에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="c3299-132">Hello 방문 [에이전트 페이지](https://app.coscale.com/) toosee 클러스터에 대 한 요약 추가 구성 단계를 수행 하 고 hello 같은 대시보드에 참조 **Kubernetes 클러스터 개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Kubernetes 클러스터 개요](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="c3299-134">hello CoScale 에이전트 hello 클러스터에서 새 컴퓨터에 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="c3299-135">hello 새 버전이 출시 될 때 자동으로 에이전트 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c3299-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3299-136">Next steps</span></span>

<span data-ttu-id="c3299-137">Hello 참조 [설명서 CoScale](http://docs.coscale.com/) 및 [블로그](https://www.coscale.com/blog) CoScale 솔루션을 모니터링 하는 방법에 대 한 더 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3299-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

