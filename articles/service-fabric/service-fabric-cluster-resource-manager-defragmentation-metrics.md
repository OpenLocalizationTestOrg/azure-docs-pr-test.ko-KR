---
title: "Azure Service Fabric에서 메트릭의 조각 모음 | Microsoft Docs"
description: "서비스 패브릭에서 메트릭에 대한 전략으로써 조각 모음 또는 압축 사용의 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b253cc07066092aa82d218c9c82c8aac502245a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="de75b-103">서비스 패브릭에서 부하 및 메트릭의 조각 모음</span><span class="sxs-lookup"><span data-stu-id="de75b-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="de75b-104">클러스터의 부하 메트릭을 관리하기 위한 Service Fabric Cluster Resource Manager의 기본 전략은 부하를 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span></span> <span data-ttu-id="de75b-105">노드가 균등하게 사용되도록 하면 핫스폿 및 콜드스폿이 방지되어 경합 및 리소스 낭비를 야기하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span></span> <span data-ttu-id="de75b-106">클러스터에서 워크로드를 분산하는 것은 오류가 지정된 워크로드의 많은 부분을 사용하지 않도록 하기 때문에 오류를 극복하는 측면에서 가장 안전한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="de75b-107">Service Fabric Cluster Resource Manager는 조각 모음이라는 다른 로드 관리 전략을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="de75b-108">조각 모음은 클러스터 전체에 걸쳐 메트릭의 사용률을 분산하려고 하지 않고 통합하려고 하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span></span> <span data-ttu-id="de75b-109">통합은 기본 부하 분산 전략을 뒤집는 것입니다. Cluster Resource Manager는 메트릭 부하의 평균 표준 편차를 최소화하는 대신 늘리려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span></span>

## <a name="when-to-use-defragmentation"></a><span data-ttu-id="de75b-110">조각 모음을 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="de75b-110">When to use defragmentation</span></span>
<span data-ttu-id="de75b-111">클러스터에서 부하를 분산하면 각 노드의 리소스 일부가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-111">Distributing load in the cluster consumes some of the resources on each node.</span></span> <span data-ttu-id="de75b-112">일부 워크로드는 매우 커서 노드의 대부분 또는 전체를 사용하는 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="de75b-113">이러한 경우 대량의 워크로드가 시작될 때 노드에 해당 워크로드를 실행할 충분한 공간이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span></span> <span data-ttu-id="de75b-114">대량의 워크로드는 Service Fabric에서 문제가 되지 않습니다. 이러한 경우 Cluster Resource Manager는 이러한 대량의 워크로드를 위한 공간을 만들기 위해 클러스터를 다시 구성해야 한다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="de75b-115">그러나 동시에 해당 워크로드는 클러스터에서 예약되기를 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="de75b-116">실행될 서비스와 상태가 많은 경우 큰 워크로드는 오랫동안 클러스터에 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="de75b-117">클러스터의 다른 워크로드도 커서 구성하는 데 시간이 더 오래 걸리는 경우 이러한 상황이 발생하기 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span></span> <span data-ttu-id="de75b-118">Service Fabric 팀은 이 시나리오의 시뮬레이션에서 생성 시간을 측정했습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="de75b-119">클러스터 사용률이 30%~50%보다 높아지자마자, 대규모 서비스를 만드는 데 훨씬 더 오래 걸린다는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="de75b-120">이 시나리오를 처리하기 위해 분산 전략으로 조각 모음을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="de75b-121">특히 생성 시간이 중요한 큰 워크로드의 경우 조각 모음이 해당 새 워크로드를 클러스터에서 예약하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="de75b-122">조각 모음 메트릭을 구성하여 Cluster Resource Manage에서 서비스의 부하를 더 적은 노드로 축소하려고 사전에 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="de75b-123">이렇게 하면 클러스터를 다시 구성하지 않고도 대규모 서비스를 위한 공간이 항상 존재하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span></span> <span data-ttu-id="de75b-124">클러스터를 다시 구성할 필요가 없으므로 대량의 워크로드를 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-124">Not having to reorganize the cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="de75b-125">대부분의 경우에는 디스크 조각 모음이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="de75b-126">서비스는 일반적으로 작으므로 클러스터에서 서비스의 공간을 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="de75b-127">다시 구성할 수 있으면 대부분의 서비스가 작으며 동시에 빠르게 이동될 수 있으므로 다시 구성 작업도 빠르게 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="de75b-128">그러나 서비스가 크고 신속하게 만들어야 할 경우 조각 모음 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span></span> <span data-ttu-id="de75b-129">다음에서는 조각 모음을 사용할 때의 장단점을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-129">We'll discuss the tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="de75b-130">조각 모음의 장단점</span><span class="sxs-lookup"><span data-stu-id="de75b-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="de75b-131">실패한 노드에서 실행되는 서비스가 더 많기 때문에 조각 모음에 미치는 오류의 영향이 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="de75b-132">클러스터의 리소스는 예약된 상태로 보유해야 하고 대량의 워크로드가 만들어질 때까지 기다려야 하므로 조각 모음의 비용도 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span></span>

<span data-ttu-id="de75b-133">다음 다이어그램에서는 조각 모음된 클러스터 및 조각 모음되지 않은 클러스터와 같이 두 클러스터의 시각적 표시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="de75b-134"><center>
![분산된 클러스터 및 조각 모음 클러스터 비교][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="de75b-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="de75b-135">분산된 경우에 가장 큰 서비스 개체 중 하나를 배치하는 데 필요한 이동 수를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="de75b-136">조각 모음된 클러스터에서는 다른 서비스가 이동할 때까지 기다릴 필요 없이 대량의 워크로드를 4개 또는 5개의 노드에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="de75b-137">조각 모음 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="de75b-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="de75b-138">그러면 다른 개념적 절충은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="de75b-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="de75b-139">다음은 생각해 볼 사항을 간단한 테이블로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-139">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="de75b-140">조각 모음 장점</span><span class="sxs-lookup"><span data-stu-id="de75b-140">Defragmentation Pros</span></span> | <span data-ttu-id="de75b-141">조각 모음 단점</span><span class="sxs-lookup"><span data-stu-id="de75b-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="de75b-142">큰 서비스를 빠르게 만들 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="de75b-142">Allows faster creation of large services</span></span> |<span data-ttu-id="de75b-143">더 적은 노드에 부하가 집중되어 경합을 늘립니다</span><span class="sxs-lookup"><span data-stu-id="de75b-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="de75b-144">생성하는 동안 데이터 이동을 줄입니다</span><span class="sxs-lookup"><span data-stu-id="de75b-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="de75b-145">실패한 경우 더 많은 서비스에 영향을 주고 더 많은 이탈이 발생할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="de75b-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="de75b-146">풍부한 요구 사항에 대한 설명 및 공간의 확보가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="de75b-147">전체 리소스 관리 구성이 더 복잡합니다</span><span class="sxs-lookup"><span data-stu-id="de75b-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="de75b-148">동일한 클러스터에서 조각 모음된 일반 메트릭을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-148">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="de75b-149">Cluster Resource Manager는 다른 항목을 분산하는 동안 가능한 한 많은 디스크 조각 모음 메트릭을 통합하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="de75b-150">조각 모음 및 분산 전략을 함께 사용할 때의 결과는 다음을 비롯한 여러 가지 요인에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="de75b-151">부하 분산 메트릭의 수 및 조각 모음 메트릭의 수</span><span class="sxs-lookup"><span data-stu-id="de75b-151">the number of balancing metrics vs. the number of defragmentation metrics</span></span>
  - <span data-ttu-id="de75b-152">서비스가 두 가지 유형의 메트릭을 모두 사용하는지 여부</span><span class="sxs-lookup"><span data-stu-id="de75b-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="de75b-153">메트릭 가중치</span><span class="sxs-lookup"><span data-stu-id="de75b-153">the metric weights</span></span>
  - <span data-ttu-id="de75b-154">현재 메트릭 부하</span><span class="sxs-lookup"><span data-stu-id="de75b-154">current metric loads</span></span>
  
<span data-ttu-id="de75b-155">실험은 필요한 정확한 구성을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-155">Experimentation is required to determine the exact configuration necessary.</span></span> <span data-ttu-id="de75b-156">프로덕션에서 조각 모음 메트릭을 사용하도록 설정하기 전에 워크로드를 철저하게 측정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="de75b-157">동일한 서비스 내에서 조각 모음과 분산된 메트릭을 함께 사용하는 경우에 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="de75b-158">조각 모음 메트릭 구성</span><span class="sxs-lookup"><span data-stu-id="de75b-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="de75b-159">조각 모음 메트릭을 구성하는 작업은 클러스터에서 전역적인 의사 결정이며 개별 메트릭은 조각 모음에서 선택될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="de75b-160">다음 구성 조각은 조각 모음에 대한 메트릭을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-160">The following config snippets show how to configure metrics for defragmentation.</span></span> <span data-ttu-id="de75b-161">이 경우 "Metric2"는 정상적으로 계속 부하가 분산되지만 "Metric1"은 조각 모음 메트릭으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span></span> 

<span data-ttu-id="de75b-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="de75b-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="de75b-163">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="de75b-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="de75b-164">Next steps</span></span>
- <span data-ttu-id="de75b-165">Cluster Resource Manager에는 클러스터를 설명하기 위한 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-165">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="de75b-166">이에 대해 자세히 알아보려면 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)에 대한 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="de75b-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="de75b-167">메트릭은 서비스 패브릭 클러스터 리소스 관리자가 클러스터의 소비와 용량을 관리하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de75b-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="de75b-168">메트릭 및 구성 방법에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="de75b-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
