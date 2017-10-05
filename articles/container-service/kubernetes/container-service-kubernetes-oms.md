---
title: "Azure Kubernetes 클러스터 모니터링 - 운영 관리 | Microsoft Docs"
description: "Microsoft Operations Management Suite를 사용하여 Azure Container Service에서 Kubernetes 클러스터 모니터링"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="481ba-103">Microsoft OMS(Operations Management Suite)를 사용하여 Azure Container Service 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="481ba-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="481ba-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="481ba-104">Prerequisites</span></span>
<span data-ttu-id="481ba-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="481ba-106">또한 `az` Azure CLI 및 `kubectl` 도구가 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="481ba-107">다음을 실행하여 `az` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="481ba-108">`az` 도구가 설치되어 있지 않으면 [여기](https://github.com/azure/azure-cli#installation)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="481ba-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="481ba-109">또는 사용자를 위해 이미 `az` Azure cli 및 `kubectl` 도구를 설치한 [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="481ba-110">다음을 실행하여 `kubectl` 도구가 설치되어 있는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="481ba-111">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="481ba-112">kubectl 도구에 kubernetes 키를 설치했는지를 테스트하려면 다음을 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="481ba-113">위의 명령을 실행한 결과 오류가 출력되면 kubernetes 클러스터 키를 kubectl 도구에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="481ba-114">이 작업은 다음 명령을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="481ba-115">OMS(Operations Management Suite)를 사용하여 컨테이너 모니터링</span><span class="sxs-lookup"><span data-stu-id="481ba-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="481ba-116">OMS(Microsoft Operations Management)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="481ba-117">Container Solution은 컨테이너 인벤토리, 성능 및 로그를 한 곳에서 볼 수 있는 OMS Log Analytics에 포함된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-117">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="481ba-118">중앙 위치에서 로그를 확인하여 컨테이너를 감사하고 문제를 해결하며 호스트에서 매우 과도하게 사용되는 컨테이너를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="481ba-119">Container Solution에 대한 자세한 내용은 [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="481ba-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="481ba-120">Kubernetes에 OMS 설치</span><span class="sxs-lookup"><span data-stu-id="481ba-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="481ba-121">작업 영역 ID 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="481ba-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="481ba-122">OMS 에이전트가 서비스와 통신하려면 작업 영역 ID 및 작업 영역 키로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-122">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="481ba-123">작업 영역 ID 및 키를 모두 가져오려면 <https://mms.microsoft.com>에서 OMS 계정을 만들어야 합니다. 다음 단계에 따라 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-123">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="481ba-124">계정을 만들었으면 아래와 같이 **설정**, **연결된 원본**, **Linux 서버**를 차례로 클릭하여 ID 및 키를 획득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-124">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="481ba-125">DaemonSet을 사용하여 OMS 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="481ba-125">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="481ba-126">DaemonSet은 Kubernetes가 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스를 실행하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-126">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="481ba-127">모니터링 에이전트를 실행하는 데 완벽합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="481ba-128">다음은 [DaemonSet YAML 파일](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)입니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-128">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="481ba-129">`oms-daemonset.yaml`라는 파일로 저장하고 `WSID` 및 `KEY`에 대한 자리 표시자 값을 파일의 작업 영역 ID 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-129">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="481ba-130">작업 영역 ID와 키를 DaemonSet 구성에 추가한 후 `kubectl` 명령줄 도구를 사용하여 클러스터에 OMS 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-130">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="481ba-131">Kubernetes 비밀을 사용하여 OMS 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="481ba-131">Installing the OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="481ba-132">OMS 작업 영역 ID 및 키를 보호하려면 Kubernetes 비밀을 DaemonSet YAML 파일의 일부로 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-132">To protect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="481ba-133">[리포지토리](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)에서 스크립트, 비밀 템플릿 파일 및 DaemonSet YAML 파일을 복사하고 이러한 항목이 같은 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-133">Copy the script, secret template file and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span> 
      - <span data-ttu-id="481ba-134">비밀 생성 스크립트 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="481ba-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="481ba-135">비밀 템플릿 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="481ba-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="481ba-136">DaemonSet YAML 파일 - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="481ba-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="481ba-137">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-137">Run the script.</span></span> <span data-ttu-id="481ba-138">스크립트에서 OMS 작업 영역 ID 및 기본 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-138">The script will ask for the OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="481ba-139">이러한 ID와 키를 삽입하면 스크립트는 사용자가 실행할 수 있도록 비밀 yaml 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-139">Please insert that and the script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="481ba-140">다음을 실행하여 비밀 Pod를 만듭니다. ``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="481ba-140">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="481ba-141">확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-141">To check, run the following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="481ba-142">``` kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기</span><span class="sxs-lookup"><span data-stu-id="481ba-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="481ba-143">결론</span><span class="sxs-lookup"><span data-stu-id="481ba-143">Conclusion</span></span>
<span data-ttu-id="481ba-144">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-144">That's it!</span></span> <span data-ttu-id="481ba-145">몇 분 후 OMS 대시보드로 이동하는 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481ba-145">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>
