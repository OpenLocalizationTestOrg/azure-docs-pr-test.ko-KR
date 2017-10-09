---
title: "aaaMonitor Azure Kubernetes 클러스터 운영 관리 | Microsoft Docs"
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="0278a-103">Microsoft OMS(Operations Management Suite)를 사용하여 Azure Container Service 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="0278a-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0278a-104">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0278a-104">Prerequisites</span></span>
<span data-ttu-id="0278a-105">이 연습에서는 [Azure Container Service를 사용하여 Kubernetes 클러스터를 만들었다고](container-service-kubernetes-walkthrough.md) 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="0278a-106">또한 hello 있다고 가정 `az` Azure cli 및 `kubectl` 도구가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="0278a-107">Hello 있는 경우 테스트할 수 `az` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="0278a-108">Hello 없는 경우 `az` 도구를 설치 하는 명령 [여기](https://github.com/azure/azure-cli#installation)합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="0278a-109">사용할 수 있습니다 [Azure 클라우드 셸](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), hello가 `az` Azure cli 및 `kubectl` 도구가 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="0278a-110">Hello 있는 경우 테스트할 수 `kubectl` 도구를 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="0278a-111">`kubectl`이 설치되어 있지 않으면 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="0278a-112">tootest kubernetes 키 kubectl 도구에 설치 되어 있는 경우 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="0278a-113">경우 hello 아웃 명령 오류, 위에 kubectl 도구 tooinstall kubernetes 클러스터 키 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="0278a-114">다음 명령을 hello로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="0278a-115">OMS(Operations Management Suite)를 사용하여 컨테이너 모니터링</span><span class="sxs-lookup"><span data-stu-id="0278a-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="0278a-116">OMS(Microsoft Operations Management)는 온-프레미스 및 클라우드 인프라를 관리 및 보호하는 데 유용한 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="0278a-117">컨테이너에서 hello 컨테이너 인벤토리 보기, 성능 및 단일 위치에 있는 로그를 사용 하면 OMS 로그 분석 솔루션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="0278a-118">감사, 중앙된 위치에 hello 로그를 확인 하 여 컨테이너 문제 해결 및 사용 과다 컨테이너 호스트에 잡음이 있는 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="0278a-119">컨테이너 솔루션에 대 한 자세한 내용은 읽어보십시오 toothe [컨테이너, 로그 분석 솔루션](../../log-analytics/log-analytics-containers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="0278a-120">Kubernetes에 OMS 설치</span><span class="sxs-lookup"><span data-stu-id="0278a-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="0278a-121">작업 영역 ID 및 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="0278a-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="0278a-122">OMS 에이전트 tootalk toohello 서비스 hello에 대 한 toobe 작업 영역 id와 작업 영역 키를 사용 하 여 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="0278a-123">계정 tooget hello 작업 영역 id 및 toocreate는 OMS에 필요한 키 <https://mms.microsoft.com>합니다. Hello 단계 toocreate 계정을 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0278a-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="0278a-124">Hello 계정 만들기를 완료 해야 tooobtain id 및 키를 클릭 하 여 **설정**, 다음 **연결 된 원본**, 차례로 **Linux 서버**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="0278a-125">DaemonSet를 사용 하 여 hello OMS 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="0278a-126">Kubernetes toorun에서 DaemonSets 사용 hello 클러스터의 각 호스트에서 컨테이너의 단일 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="0278a-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="0278a-127">모니터링 에이전트를 실행하는 데 완벽합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="0278a-128">여기에 hello [DaemonSet YAML 파일](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="0278a-129">Tooa 파일의 이름이 저장 `oms-daemonset.yaml` 및 바꾸기에 대 한 자리 표시자 값 hello `WSID` 및 `KEY` 작업 영역 id와 hello 파일의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="0278a-130">작업 영역 ID 및 키 toohello DaemonSet 구성을 추가한 후 hello 사용 하 여 클러스터에 hello OMS 에이전트를 설치할 수 있습니다 `kubectl` 명령줄 도구:</span><span class="sxs-lookup"><span data-stu-id="0278a-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="0278a-131">Kubernetes 암호를 사용 하 여 hello OMS 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="0278a-132">tooprotect OMS 작업 영역 ID 및 키 Kubernetes 비밀 DaemonSet YAML 파일의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="0278a-133">Hello 스크립트, 비밀 템플릿 파일 및 hello DaemonSet YAML 파일 복사 (에서 [리포지토리](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) hello에 있는지 확인 하 고 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="0278a-134">비밀 생성 스크립트 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="0278a-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="0278a-135">비밀 템플릿 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="0278a-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="0278a-136">DaemonSet YAML 파일 - omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="0278a-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="0278a-137">Hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-137">Run hello script.</span></span> <span data-ttu-id="0278a-138">OMS 작업 영역 ID와 기본 키 hello 스크립트 hello에 대 한 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="0278a-139">넣은 hello 스크립트에서 실행할 수 있도록 비밀 yaml 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="0278a-140">Hello 비밀 pod를 hello 다음을 실행 하 여 만듭니다.``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="0278a-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="0278a-141">toocheck hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="0278a-141">toocheck, run hello following:</span></span> 

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
 
  - <span data-ttu-id="0278a-142">``` kubectl create -f omsagent-ds-secrets.yaml ```을 실행하여 omsagent daemon-set 만들기</span><span class="sxs-lookup"><span data-stu-id="0278a-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="0278a-143">결론</span><span class="sxs-lookup"><span data-stu-id="0278a-143">Conclusion</span></span>
<span data-ttu-id="0278a-144">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-144">That's it!</span></span> <span data-ttu-id="0278a-145">몇 분 후 수 toosee 데이터 tooyour OMS 대시보드에 흐름 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0278a-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
