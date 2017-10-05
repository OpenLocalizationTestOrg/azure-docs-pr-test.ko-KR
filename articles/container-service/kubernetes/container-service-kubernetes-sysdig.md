---
title: "Azure Kubernetes 클러스터 모니터링 - Sysdig | Microsoft Docs"
description: "Sysdig을 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="eae6c-103">Sysdig을 사용하여 Azure Container Service Kubernetes 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="eae6c-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eae6c-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eae6c-104">Prerequisites</span></span>
<span data-ttu-id="eae6c-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="eae6c-106">또한 Azure CLI 및 kubectl 도구가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="eae6c-107">다음을 실행하여 `az` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="eae6c-108">`az` 도구가 설치되어 있지 않으면 [여기](https://github.com/azure/azure-cli#installation)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="eae6c-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="eae6c-109">다음을 실행하여 `kubectl` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="eae6c-110">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="eae6c-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="eae6c-111">Sysdig</span></span>
<span data-ttu-id="eae6c-112">Sysdig은 Azure에서 실행 중인 Kubernetes 클러스터에 대한 컨테이너를 모니터링할 수 있는 외부 모니터링 서비스 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="eae6c-113">Sysdig을 사용하려면 활성 Sysdig 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="eae6c-114">[사이트](https://app.sysdigcloud.com)에서 계정에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="eae6c-115">Sysdig 클라우드 웹 사이트에 로그인하여 사용자 이름을 클릭하면 페이지에 "선택키"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API 키](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="eae6c-117">Kubernetes에 Sysdig 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="eae6c-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="eae6c-118">컨테이너를 모니터링하기 위해 Sysdig은 Kubernetes `DaemonSet`을 사용하여 각 컴퓨터에서 프로세스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="eae6c-119">DaemonSets은 컴퓨터당 컨테이너의 단일 인스턴스를 실행하는 Kubernetes API 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="eae6c-120">Sysdig의 모니터링 에이전트와 같은 도구를 설치하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="eae6c-121">Sysdig daemonset을 설치하려면 먼저 sysdig에서 [템플릿](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml)을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="eae6c-122">해당 파일을 `sysdig-daemonset.yaml`로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="eae6c-123">Linux 및 OS X에서 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="eae6c-124">PowerShell에서:</span><span class="sxs-lookup"><span data-stu-id="eae6c-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="eae6c-125">그런 후 해당 파일을 편집하여 다음 Sysdig 계정에서 얻은 액세스 키를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="eae6c-126">마지막으로 DaemonSet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="eae6c-127">모니터링 보기</span><span class="sxs-lookup"><span data-stu-id="eae6c-127">View your monitoring</span></span>
<span data-ttu-id="eae6c-128">일단 설치하여 실행 중이면 에이전트는 Sysdig로 데이터를 다시 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="eae6c-129">[sysdig 대시보드](https://app.sysdigcloud.com)로 돌아가 컨테이너에 대한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="eae6c-130">[새 대시보드 마법사](https://app.sysdigcloud.com/#/dashboards/new)를 통해 Kubernetes 특정 대시보드를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae6c-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
