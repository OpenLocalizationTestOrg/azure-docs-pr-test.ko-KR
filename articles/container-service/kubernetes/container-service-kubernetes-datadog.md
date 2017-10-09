---
title: "aaaMonitor Azure Kubernetes 클러스터 Datadog으로 | Microsoft Docs"
description: "Datadog을 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="9dbbf-103">Datadog을 사용하여 Azure Container Service 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="9dbbf-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dbbf-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9dbbf-104">Prerequisites</span></span>
<span data-ttu-id="9dbbf-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="9dbbf-106">또한 hello 있다고 가정 `az` Azure cli 및 `kubectl` 도구가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="9dbbf-107">Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="9dbbf-108">Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="9dbbf-109">Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="9dbbf-110">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="9dbbf-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="9dbbf-111">DataDog</span></span>
<span data-ttu-id="9dbbf-112">Datadog은 Azure 컨테이너 서비스 클러스터 내의 컨테이너에서 모니터링 데이터를 수집하는 모니터링 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="9dbbf-113">Datadog에는 컨테이너 내에서 특정 메트릭을 볼 수 있는 Docker 통합 대시보드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="9dbbf-114">컨테이너에서 수집된 메트릭은 CPU, 메모리, 네트워크 및 I/O로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="9dbbf-115">Datadog은 메트릭을 컨테이너와 이미지로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="9dbbf-116">먼저 너무[계정 만들기](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="9dbbf-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="9dbbf-117">DaemonSet를 사용 하 여 hello Datadog 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="9dbbf-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="9dbbf-118">Kubernetes toorun에서 DaemonSets 사용 hello 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="9dbbf-119">모니터링 에이전트를 실행하는 데 완벽합니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="9dbbf-120">Hello를 따를 수를 Datadog에 로그인 한 후 [Datadog 지침](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog 에이전트는 DaemonSet를 사용 하 여 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9dbbf-121">결론</span><span class="sxs-lookup"><span data-stu-id="9dbbf-121">Conclusion</span></span>
<span data-ttu-id="9dbbf-122">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-122">That's it!</span></span> <span data-ttu-id="9dbbf-123">Hello 에이전트 가동 되 고 실행 하면 몇 분 안에 hello 콘솔의에서 데이터를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="9dbbf-124">통합 hello를 방문할 수 있는 [kubernetes 대시보드](https://app.datadoghq.com/screen/integration/kubernetes) toosee 클러스터에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="9dbbf-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
