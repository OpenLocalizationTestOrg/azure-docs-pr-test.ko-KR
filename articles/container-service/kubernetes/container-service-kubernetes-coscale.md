---
title: "CoScale을 사용하여 Azure Kubernetes 클러스터 모니터링 | Microsoft Docs"
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
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="f7483-103">CoScale을 사용하여 Azure Container Service Kubernetes 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="f7483-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="f7483-104">이 문서에서는 [CoScale](https://www.coscale.com/) 에이전트를 배포하여 Azure Container Service의 Kubernetes 클러스터에 있는 모든 노드 및 컨테이너를 모니터링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="f7483-105">이러한 구성을 위해서는 CoScale 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="f7483-106">CoScale 정보</span><span class="sxs-lookup"><span data-stu-id="f7483-106">About CoScale</span></span> 

<span data-ttu-id="f7483-107">CoScale은 여러 오케스트레이션 플랫폼의 모든 컨테이너에서 메트릭 및 이벤트를 수집하는 모니터링 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="f7483-108">CoScale은 Kubernetes 환경에 대한 전체 스택 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="f7483-109">여기에는 스택의 모든 계층, 즉 OS, Kubernetes, Docker 및 컨테이너 내에서 실행되는 응용 프로그램에 대한 시각화 및 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="f7483-110">CoScale은 몇 가지 기본 제공 모니터링 대시보드를 제공하며 운영자 및 개발자가 인프라 및 응용 프로그램 문제를 빠르게 찾을 수 있도록 하는 기본 제공 비정상 감지 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="f7483-112">이 문서에 나와 있는 것처럼 Kubernetes 클러스터에 에이전트를 설치하여 CoScale을 SaaS 솔루션으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="f7483-113">데이터를 온사이트에 유지하려는 경우 온-프레미스 설치에도 CoScale을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f7483-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7483-114">Prerequisites</span></span>

<span data-ttu-id="f7483-115">먼저 [CoScale 계정을 만들어야 합니다](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="f7483-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="f7483-116">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="f7483-117">또한 `az` Azure CLI 및 `kubectl` 도구가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="f7483-118">다음을 실행하여 `az` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="f7483-119">`az` 도구가 설치되어 있지 않으면 [여기](/cli/azure/install-azure-cli)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="f7483-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="f7483-120">다음을 실행하여 `kubectl` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="f7483-121">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="f7483-122">DaemonSet에 CoScale 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="f7483-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="f7483-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)은 Kubernetes가 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스를 실행하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="f7483-124">CoScale 에이전트와 같은 모니터링 에이전트를 실행하는 데 완벽합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="f7483-125">CoScale에 로그인한 후 [에이전트 페이지](https://app.coscale.com/)로 이동한 다음 DaemonSet을 사용하여 클러스터에 CoScale 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="f7483-126">CoScale UI는 에이전트를 만들고 전체 Kubernetes 클러스터 모니터링을 시작하기 위한 단계별 구성 과정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale 에이전트 구성](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="f7483-128">클러스터에서 에이전트를 시작하려면 제공된 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-128">To start the agent on the cluster, run the supplied command:</span></span>

![CoScale 에이전트 시작](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="f7483-130">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-130">That's it!</span></span> <span data-ttu-id="f7483-131">에이전트가 작동 및 실행되면 몇 분 내에 콘솔에 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="f7483-132">[에이전트 페이지](https://app.coscale.com/)를 방문하여 클러스터에 대한 요약을 확인하고, 추가 구성 단계를 수행하고, **Kubernetes 클러스터 개요**와 같은 대시보드를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Kubernetes 클러스터 개요](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="f7483-134">CoScale 에이전트는 클러스터의 새 컴퓨터에 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="f7483-135">새 버전이 릴리스되면 에이전트가 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7483-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7483-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7483-136">Next steps</span></span>

<span data-ttu-id="f7483-137">CoScale 모니터링 솔루션에 대한 자세한 내용은 [CoScale 설명서](http://docs.coscale.com/) 및 [블로그](https://www.coscale.com/blog)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7483-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

