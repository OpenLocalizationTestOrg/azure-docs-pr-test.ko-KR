---
title: "aaaMonitor Azure Kubernetes 클러스터 Sysdig | Microsoft Docs"
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="dc403-103">Sysdig을 사용하여 Azure Container Service Kubernetes 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="dc403-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc403-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dc403-104">Prerequisites</span></span>
<span data-ttu-id="dc403-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="dc403-106">또한 hello azure cli 및 kubectl 도구가 설치 되어 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="dc403-107">Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="dc403-108">Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="dc403-109">Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="dc403-110">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="dc403-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="dc403-111">Sysdig</span></span>
<span data-ttu-id="dc403-112">Sysdig은 Azure에서 실행 중인 Kubernetes 클러스터에 대한 컨테이너를 모니터링할 수 있는 외부 모니터링 서비스 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="dc403-113">Sysdig을 사용하려면 활성 Sysdig 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="dc403-114">[사이트](https://app.sysdigcloud.com)에서 계정에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="dc403-115">Toohello Sysdig 클라우드 웹 사이트를 로그인 후 사용자 이름을 클릭 하 고 "액세스 키입니다." hello 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API 키](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="dc403-117">Hello Sysdig 에이전트 tooKubernetes 설치</span><span class="sxs-lookup"><span data-stu-id="dc403-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="dc403-118">컨테이너, 각 프로세스가 Sysdig 실행 컴퓨터는 Kubernetes를 사용 하 여 toomonitor `DaemonSet`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="dc403-119">DaemonSets은 컴퓨터당 컨테이너의 단일 인스턴스를 실행하는 Kubernetes API 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="dc403-120">Hello Sysdig의 모니터링 에이전트와 같은 도구를 설치 하기 위한 완벽 한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="dc403-121">tooinstall hello Sysdig daemonset 먼저 다운로드 해야 [hello 템플릿](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) sysdig에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="dc403-122">해당 파일을 `sysdig-daemonset.yaml`로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="dc403-123">Linux 및 OS X에서 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="dc403-124">PowerShell에서:</span><span class="sxs-lookup"><span data-stu-id="dc403-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="dc403-125">그런 다음 해당 파일 tooinsert Sysdig 계정에서 얻은 하 여 액세스 키를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="dc403-126">마지막으로, DaemonSet hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="dc403-127">모니터링 보기</span><span class="sxs-lookup"><span data-stu-id="dc403-127">View your monitoring</span></span>
<span data-ttu-id="dc403-128">설치 하 고 실행 되 면 hello 에이전트 백 tooSysdig 데이터를 펌프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="dc403-129">Toothe 돌아가서 [sysdig 대시보드](https://app.sysdigcloud.com) 사용자 컨테이너에 대 한 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="dc403-130">[새 대시보드 마법사](https://app.sysdigcloud.com/#/dashboards/new)를 통해 Kubernetes 특정 대시보드를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc403-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
