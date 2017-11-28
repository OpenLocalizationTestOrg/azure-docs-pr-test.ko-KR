---
title: "Azure Container Service 자습서 - Kubernetes 모니터링 | Microsoft Docs"
description: "Azure Container Service 자습서 - Microsoft OMS(Operations Management Suite)를 사용하여 Kubernetes 모니터링"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="90370-104">Operations Management Suite를 사용하여 Kubernetes 클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="90370-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="90370-105">Kubernetes 클러스터 및 컨테이너를 모니터링하는 것은 중요하며, 특히 여러 앱을 사용하여 대규모의 프로덕션 클러스터를 관리하는 경우 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="90370-106">Microsoft 또는 다른 공급자가 제공하는 여러 Kubernetes 모니터링 솔루션을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="90370-107">이 자습서에서는 Microsoft의 클라우드 기반 IT 관리 솔루션인 [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md)의 컨테이너 솔루션을 사용하여 Kubernetes 클러스터를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="90370-108">(OMS 컨테이너 솔루션은 미리 보기 상태입니다.)</span><span class="sxs-lookup"><span data-stu-id="90370-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="90370-109">7개 중 7단계인 이 자습서에서는 다음과 같은 작업을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="90370-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90370-110">OMS 작업 영역 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="90370-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="90370-111">Kubernetes 노드에서 OMS 에이전트 설정</span><span class="sxs-lookup"><span data-stu-id="90370-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="90370-112">OMS 포털 또는 Azure Portal에서 모니터링 정보에 액세스</span><span class="sxs-lookup"><span data-stu-id="90370-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90370-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="90370-113">Before you begin</span></span>

<span data-ttu-id="90370-114">이전 자습서에서는 응용 프로그램을 컨테이너 이미지에 패키지하고, Azure Container Registry에 이러한 이미지를 업로드하고, Kubernetes 클러스터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="90370-115">이러한 단계를 수행하지 않은 경우 수행하려면 [자습서 1 - 컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="90370-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="90370-116">최소한 이 자습서에는 Linux 에이전트 노드가 있는 Kubernetes 클러스터 및 OMS(Operations Management Suite) 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="90370-117">필요한 경우 [OMS 평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="90370-118">작업 영역 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="90370-118">Get Workspace settings</span></span>

<span data-ttu-id="90370-119">[OMS 포털](https://mms.microsoft.com)에 액세스할 수 있는 경우 **설정** > **연결된 원본** > **Linux 서버**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="90370-120">거기서 *작업 영역 ID* 및 기본 또는 보조 *작업 영역 키*를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="90370-121">클러스터에서 OMS 에이전트를 설정하는 데 필요한 이러한 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="90370-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="90370-122">OMS 에이전트 설정</span><span class="sxs-lookup"><span data-stu-id="90370-122">Set up OMS agents</span></span>

<span data-ttu-id="90370-123">다음은 Linux 클러스터 노드에서 OMS 에이전트를 설정하기 위한 YAML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="90370-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="90370-124">이 파일은 Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)를 만들며, 이는 각 클러스터 노드에서 하나의 같은 Pod를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="90370-125">DaemonSet 리소스는 모니터링 에이전트 배포에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="90370-126">다음 텍스트를 `oms-daemonset.yaml`이라는 파일에 저장하고, *myWorkspaceID* 및 *myWorkspaceKey*의 자리 표시자 값을 해당 OMS 작업 영역 ID 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="90370-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="90370-127">(프로덕션에서 이러한 값을 비밀로 인코딩할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="90370-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="90370-128">다음 명령을 사용하여 DaemonSet를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90370-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="90370-129">DaemonSet가 만들어졌는지 확인하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="90370-130">다음과 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="90370-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="90370-131">에이전트가 실행된 후 OMS에서 데이터를 수집하고 처리하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="90370-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="90370-132">모니터링 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="90370-132">Access monitoring data</span></span>

<span data-ttu-id="90370-133">OMS 포털 또는 Azure Portal의 [컨테이너 솔루션](../../log-analytics/log-analytics-containers.md)을 통해 OMS 컨테이너 모니터링 데이터를 보고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="90370-134">[OMS 포털](https://mms.microsoft.com)을 사용하여 컨테이너 솔루션을 설치하려면 **솔루션 갤러리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="90370-135">그런 다음 **컨테이너 솔루션**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-135">Then add **Container Solution**.</span></span> <span data-ttu-id="90370-136">또는 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview)에서 컨테이너 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="90370-137">OMS 포털의 OMS 대시보드에서 **컨테이너** 요약 타일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="90370-138">타일을 클릭하면 컨테이너 이벤트, 오류, 상태, 이미지 인벤토리, CPU 및 메모리 사용량과 같은 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="90370-139">더 세부적인 정보를 보려면 아무 타일에서 행을 클릭하거나 [로그 검색](../../log-analytics/log-analytics-log-searches.md)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![OMS 포털의 컨테이너 대시보드](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="90370-141">마찬가지로 Azure Portal에서 **Log Analytics**로 이동하고 작업 영역 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="90370-142">**컨테이너** 요약 타일을 보려면 **솔루션** > **컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="90370-143">세부 정보를 보려면 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90370-143">To see details, click the tile.</span></span>

<span data-ttu-id="90370-144">모니터링 데이터 쿼리 및 분석에 대한 자세한 지침은 [Azure Log Analytics 설명서](../../log-analytics/index.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90370-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90370-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90370-145">Next steps</span></span>

<span data-ttu-id="90370-146">이 자습서에서는 OMS를 사용하여 Kubernetes 클러스터를 모니터링했습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="90370-147">설명한 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90370-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90370-148">OMS 작업 영역 설정 가져오기</span><span class="sxs-lookup"><span data-stu-id="90370-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="90370-149">Kubernetes 노드에서 OMS 에이전트 설정</span><span class="sxs-lookup"><span data-stu-id="90370-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="90370-150">OMS 포털 또는 Azure Portal에서 모니터링 정보에 액세스</span><span class="sxs-lookup"><span data-stu-id="90370-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="90370-151">Container Service에 대한 미리 빌드된 스크립트 샘플을 보려면 이 링크를 따라가세요.</span><span class="sxs-lookup"><span data-stu-id="90370-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90370-152">Azure Container Service 스크립트 샘플</span><span class="sxs-lookup"><span data-stu-id="90370-152">Azure Container Service script samples</span></span>](cli-samples.md)
