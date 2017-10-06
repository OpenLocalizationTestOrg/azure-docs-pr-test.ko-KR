---
title: "aaaAzure 컨테이너 서비스 자습서-규모의 응용 프로그램 | Microsoft Docs"
description: "Azure Container Service 자습서 - 응용 프로그램 크기 조정"
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="37bc2-104">Kubernetes Pod 및 Kubernetes 인프라 크기 조정</span><span class="sxs-lookup"><span data-stu-id="37bc2-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="37bc2-105">Hello 자습서 수행 했다면, 하는 경우 작업 Kubernetes 클러스터에 Azure 컨테이너 서비스 있고 hello Azure 투표 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="37bc2-106">이 자습서에서는, 7 5 부분 hello 포드 hello 응용 프로그램에서 확장 고 pod 자동 크기 조정을 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="37bc2-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="37bc2-107">또한 Azure VM 에이전트 노드 toochange tooscale hello 수의 워크 로드를 호스트에 대 한 클러스터의 용량 hello 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="37bc2-108">완료된 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="37bc2-109">수동으로 Kubernetes Pod 크기 조정</span><span class="sxs-lookup"><span data-stu-id="37bc2-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="37bc2-110">Hello 응용 프로그램에 대 한 프런트 엔드를 실행 하는 자동 크기 조정 포드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="37bc2-111">Hello Kubernetes Azure 에이전트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="37bc2-112">후속 자습서에서는 hello Azure 투표 응용 프로그램 업데이트 되 고 Operations Management Suite toomonitor hello Kubernetes 클러스터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="37bc2-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="37bc2-113">Before you begin</span></span>

<span data-ttu-id="37bc2-114">이전 자습서에서 컨테이너 이미지에 패키지 된 응용 프로그램, 컨테이너 레지스트리 tooAzure 및 만들어진 Kubernetes 클러스터가이 이미지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="37bc2-115">그런 다음 hello 응용 프로그램 hello Kubernetes 클러스터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="37bc2-116">다음이 단계를 수행 하지 않은 toofollow을 따라 하려는 경우 반환 toohello [자습서 1-컨테이너 이미지 만들기](./container-service-tutorial-kubernetes-prepare-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="37bc2-117">최소한 이 자습서에는 실행 중인 응용 프로그램이 있는 Kubernetes 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="37bc2-118">수동으로 Pod 크기 조정</span><span class="sxs-lookup"><span data-stu-id="37bc2-118">Manually scale pods</span></span>

<span data-ttu-id="37bc2-119">지금까지 hello Azure 투표 프런트 엔드 및 Redis 인스턴스 배포 됨에 따라 각각 단일 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="37bc2-120">hello 실행 tooverify [kubectl 가져오기](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="37bc2-121">출력:</span><span class="sxs-lookup"><span data-stu-id="37bc2-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="37bc2-122">Hello에 포드 hello 수를 수동으로 변경 `azure-vote-front` hello를 사용 하 여 배포 [kubectl 배율](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="37bc2-123">이 예에서는 숫자 too5 hello 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="37bc2-124">실행 [kubectl 가져오기 포드](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes hello 포드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="37bc2-125">1 분 정도 지난 후 hello 추가 포드 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="37bc2-126">출력:</span><span class="sxs-lookup"><span data-stu-id="37bc2-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="37bc2-127">Pod 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="37bc2-127">Autoscale pods</span></span>

<span data-ttu-id="37bc2-128">Kubernetes 지원 [수평 포드 자동 크기 조정](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello 수가 포드 CPU 사용률 또는 기타에 따라 배포에서 메트릭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="37bc2-129">toouse hello autoscaler CPU 요청 및 제한을 정의 하면 포드 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="37bc2-130">Hello에 `azure-vote-front` 배포에서는 프런트 엔드 컨테이너 요청 0.25 CPU 0.5의 제한으로 hello CPU.</span><span class="sxs-lookup"><span data-stu-id="37bc2-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="37bc2-131">hello 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="37bc2-132">hello 다음 예제에서는 hello [kubectl 자동 크기 조정](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) tooautoscale hello 수가 hello에 포드 명령 `azure-vote-front` 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="37bc2-133">여기에서 50%를 초과 하는 CPU 사용률, hello autoscaler hello 포드 tooa 최대를 10 늘리십시오.</span><span class="sxs-lookup"><span data-stu-id="37bc2-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="37bc2-134">hello 다음 명령을 실행 하는 hello autoscaler toosee hello 상태:</span><span class="sxs-lookup"><span data-stu-id="37bc2-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="37bc2-135">출력:</span><span class="sxs-lookup"><span data-stu-id="37bc2-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="37bc2-136">Hello Azure 투표 응용 프로그램에 대 한 최소한의 부하를 몇 분 후 hello pod 복제본 수가 too3 자동으로 감소합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="37bc2-137">배율 hello 에이전트</span><span class="sxs-lookup"><span data-stu-id="37bc2-137">Scale hello agents</span></span>

<span data-ttu-id="37bc2-138">Hello 이전 자습서에서 기본 명령을 사용 하 여 Kubernetes 클러스터를 만든 경우에 세 개의 에이전트 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="37bc2-139">클러스터에 더 많거나 적은 컨테이너 작업을 계획 하는 경우 에이전트의 hello 수를 수동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="37bc2-140">사용 하 여 hello [az acs 확장](/cli/azure/acs#scale) 명령을 실행 하 고 에이전트의 hello 번호 hello 지정 `--new-agent-count` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="37bc2-141">hello 다음 예제에서는 hello 수가 증가 라는 hello Kubernetes 클러스터의 에이전트 노드 too4 *myK8sCluster*합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="37bc2-142">hello 명령 작업은 몇 분 toocomplete입니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="37bc2-143">hello 명령 출력 에이전트의 hello 번호에서에서 노드 표시의 hello 값 `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="37bc2-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="37bc2-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37bc2-144">Next steps</span></span>

<span data-ttu-id="37bc2-145">이 자습서에서는 Kubernetes 클러스터의 다양한 크기 조정 기능을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="37bc2-146">설명한 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="37bc2-147">수동으로 Kubernetes Pod 크기 조정</span><span class="sxs-lookup"><span data-stu-id="37bc2-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="37bc2-148">Hello 응용 프로그램에 대 한 프런트 엔드를 실행 하는 자동 크기 조정 포드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="37bc2-149">Hello Kubernetes Azure 에이전트 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="37bc2-150">Kubernetes에서 응용 프로그램을 업데이트 하는 방법에 대 한 다음 자습서 toolearn toohello를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37bc2-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37bc2-151">Kubernetes에서 응용 프로그램 업데이트</span><span class="sxs-lookup"><span data-stu-id="37bc2-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

