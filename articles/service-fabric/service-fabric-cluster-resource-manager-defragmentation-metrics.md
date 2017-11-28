---
title: "Azure 서비스 패브릭에서 메트릭 aaaDefragmentation | Microsoft Docs"
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
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="bfcf6-103">서비스 패브릭에서 부하 및 메트릭의 조각 모음</span><span class="sxs-lookup"><span data-stu-id="bfcf6-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="bfcf6-104">hello 클러스터의 부하 메트릭을 관리 하기 위한 hello 서비스 패브릭 클러스터 리소스 관리자의 기본 전략은 toodistribute hello load입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-104">hello Service Fabric Cluster Resource Manager's default strategy for managing load metrics in hello cluster is toodistribute hello load.</span></span> <span data-ttu-id="bfcf6-105">노드는 균등 하 게 사용 되 고 있는 보장 tooboth 경합 및 리소스를 불필요 하 게 이어지는 핫 및 콜드 스폿은 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead tooboth contention and wasted resources.</span></span> <span data-ttu-id="bfcf6-106">오류는 높은 비율의 특정된 작업을 사용 하지 않습니다을 보장 하므로 이후 오류 되지 않고 남아 측면에서 가장 안전한 hello 이기도 hello 클러스터에서 워크 로드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-106">Distributing workloads in hello cluster is also hello safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="bfcf6-107">서비스 패브릭 클러스터 리소스 관리자 hello 부하는 조각 모음을 관리 하기 위한 다른 전략을 지원지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-107">hello Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="bfcf6-108">조각 모음을 메트릭 toodistribute hello 사용률 hello 클러스터 전체 말고 것은 통합을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-108">Defragmentation means that instead of trying toodistribute hello utilization of a metric across hello cluster, it is consolidated.</span></span> <span data-ttu-id="bfcf6-109">통합은 방금의 순서를 변경 hello 기본 균형 조정 전략 – 메트릭 부하의 hello 평균 표준 편차를 최소화 하는 대신, 클러스터 리소스 관리자 hello 시도 tooincrease 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-109">Consolidation is just an inversion of hello default balancing strategy – instead of minimizing hello average standard deviation of metric load, hello Cluster Resource Manager tries tooincrease it.</span></span>

## <a name="when-toouse-defragmentation"></a><span data-ttu-id="bfcf6-110">때 toouse 조각 모음</span><span class="sxs-lookup"><span data-stu-id="bfcf6-110">When toouse defragmentation</span></span>
<span data-ttu-id="bfcf6-111">Hello 클러스터의 부하를 분산 각 노드에 hello 리소스 중 일부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-111">Distributing load in hello cluster consumes some of hello resources on each node.</span></span> <span data-ttu-id="bfcf6-112">일부 워크로드는 매우 커서 노드의 대부분 또는 전체를 사용하는 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="bfcf6-113">이러한 경우에는 없는 큰 경우 충분 하지 않으므로 생성 가져오기 작업 간격을 모든 노드에 toorun에 게 수는.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node toorun them.</span></span> <span data-ttu-id="bfcf6-114">큰 작업 서비스 패브릭;에서 문제가 되지 않습니다. 이러한 경우 hello 클러스터 리소스 관리자 작업이이 대 한 tooreorganize hello 클러스터 toomake 공간이 필요 함을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-114">Large workloads aren't a problem in Service Fabric; in these cases hello Cluster Resource Manager determines that it needs tooreorganize hello cluster toomake room for this large workload.</span></span> <span data-ttu-id="bfcf6-115">그러나 hello 그 동안 워크 로드에 hello 클러스터에 예약 된 toowait toobe 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-115">However, in hello meantime that workload has toowait toobe scheduled in hello cluster.</span></span>

<span data-ttu-id="bfcf6-116">가 없을 경우 많은 서비스와 상태 toomove 주위 hello 작업이 toobe hello 클러스터에 배치에 대 한 오래를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-116">If there are many services and state toomove around, then it could take a long time for hello large workload toobe placed in hello cluster.</span></span> <span data-ttu-id="bfcf6-117">이 hello 클러스터의 다른 워크 로드는 또한 큰 고 긴 tooreorganize 그러니까 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-117">This is more likely if other workloads in hello cluster are also large and so take longer tooreorganize.</span></span> <span data-ttu-id="bfcf6-118">서비스 패브릭 팀 hello 생성 시간에 따라이 시나리오의 시뮬레이션에서 측정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-118">hello Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="bfcf6-119">클러스터 사용률이 30%~50%보다 높아지자마자, 대규모 서비스를 만드는 데 훨씬 더 오래 걸린다는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="bfcf6-120">toohandle이이 시나리오에서는 분산 전략으로 조각 모음을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-120">toohandle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="bfcf6-121">대규모 워크 로드에 대 한 특히 된 작성 시간을 조각 모음에는 실제로 새 워크 로드에서는 중요 한 예약 hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in hello cluster.</span></span>

<span data-ttu-id="bfcf6-122">노드 수가 더 적은를 조각 모음 메트릭 toohave hello hello 서비스의 클러스터 리소스 관리자 tooproactively try toocondense hello 부하를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-122">You can configure defragmentation metrics toohave hello Cluster Resource Manager tooproactively try toocondense hello load of hello services into fewer nodes.</span></span> <span data-ttu-id="bfcf6-123">이렇게 하면 hello 클러스터를 다시 구성 하지 않고 큰 서비스를 위한 공간이 거의 항상 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-123">This helps ensure that there is almost always room for large services without reorganizing hello cluster.</span></span> <span data-ttu-id="bfcf6-124">Tooreorganize hello 클러스터 고 다니지 않아도 큰 작업을 신속 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-124">Not having tooreorganize hello cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="bfcf6-125">대부분의 경우에는 디스크 조각 모음이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="bfcf6-126">서비스는 hello 클러스터의 해당 위한 하드 toofind 공간 되기 때문에 일반적으로 작은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-126">Services are usually be small, so it’s not hard toofind room for them in hello cluster.</span></span> <span data-ttu-id="bfcf6-127">다시 구성할 수 있으면 대부분의 서비스가 작으며 동시에 빠르게 이동될 수 있으므로 다시 구성 작업도 빠르게 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="bfcf6-128">그러나 큰 서비스 하 고 신속 하 게 만들 필요 다음 경우 hello를 조각 모음 전략은입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-128">However, if you have large services and need them created quickly then hello defragmentation strategy is for you.</span></span> <span data-ttu-id="bfcf6-129">다음 조각 모음을 사용 하 여 hello 장단점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-129">We'll discuss hello tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="bfcf6-130">조각 모음의 장단점</span><span class="sxs-lookup"><span data-stu-id="bfcf6-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="bfcf6-131">실패한 노드에서 실행되는 서비스가 더 많기 때문에 조각 모음에 미치는 오류의 영향이 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="bfcf6-132">조각 모음 대량의 작업의 hello 만들기 위해 대기 하는 예약에 hello 클러스터 리소스를 보유 해야 하므로 비용을 높일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-132">Defragmentation can also increase costs, since resources in hello cluster must be held in reserve, waiting for hello creation of large workloads.</span></span>

<span data-ttu-id="bfcf6-133">hello 다음 다이어그램은 두 클러스터의 시각적 표현, 조각화를 방지 하 고 다른 하나는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-133">hello following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="bfcf6-134"><center>
![분산된 클러스터 및 조각 모음 클러스터 비교][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="bfcf6-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="bfcf6-135">Hello 분산 된 경우에서 이동 hello 최대 서비스 개체 중 하나는 필요한 tooplace 될 hello 수를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-135">In hello balanced case, consider hello number of movements that would be necessary tooplace one of hello largest service objects.</span></span> <span data-ttu-id="bfcf6-136">Hello 조각 모음 된 클러스터의 다른 서비스 toomove에 대 한 toowait 필요 없이 hello 작업이 노드 4 개 또는 5에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-136">In hello defragmented cluster, hello large workload could be placed on nodes four or five without having toowait for any other services toomove.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="bfcf6-137">조각 모음 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="bfcf6-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="bfcf6-138">그러면 다른 개념적 절충은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bfcf6-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="bfcf6-139">에 대 한 빠른 목차 항목 toothink 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-139">Here’s a quick table of things toothink about:</span></span>

| <span data-ttu-id="bfcf6-140">조각 모음 장점</span><span class="sxs-lookup"><span data-stu-id="bfcf6-140">Defragmentation Pros</span></span> | <span data-ttu-id="bfcf6-141">조각 모음 단점</span><span class="sxs-lookup"><span data-stu-id="bfcf6-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="bfcf6-142">큰 서비스를 빠르게 만들 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="bfcf6-142">Allows faster creation of large services</span></span> |<span data-ttu-id="bfcf6-143">더 적은 노드에 부하가 집중되어 경합을 늘립니다</span><span class="sxs-lookup"><span data-stu-id="bfcf6-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="bfcf6-144">생성하는 동안 데이터 이동을 줄입니다</span><span class="sxs-lookup"><span data-stu-id="bfcf6-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="bfcf6-145">실패한 경우 더 많은 서비스에 영향을 주고 더 많은 이탈이 발생할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="bfcf6-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="bfcf6-146">풍부한 요구 사항에 대한 설명 및 공간의 확보가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="bfcf6-147">전체 리소스 관리 구성이 더 복잡합니다</span><span class="sxs-lookup"><span data-stu-id="bfcf6-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="bfcf6-148">조각 모음 된 혼합할 수 있습니다 및 일반 메트릭을 hello 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-148">You can mix defragmented and normal metrics in hello same cluster.</span></span> <span data-ttu-id="bfcf6-149">hello 클러스터 리소스 관리자 시도 tooconsolidate hello 조각 모음 메트릭 분산 하는 동안 최대한 많이 다른 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-149">hello Cluster Resource Manager tries tooconsolidate hello defragmentation metrics as much as possible while spreading out hello others.</span></span> <span data-ttu-id="bfcf6-150">조각 모음 능력 분산 전략의 hello 결과 등의 여러 가지 요인에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-150">hello results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="bfcf6-151">균형 조정 hello 수의 조각 모음 메트릭 및 메트릭을 hello 수</span><span class="sxs-lookup"><span data-stu-id="bfcf6-151">hello number of balancing metrics vs. hello number of defragmentation metrics</span></span>
  - <span data-ttu-id="bfcf6-152">서비스가 두 가지 유형의 메트릭을 모두 사용하는지 여부</span><span class="sxs-lookup"><span data-stu-id="bfcf6-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="bfcf6-153">hello 메트릭 가중치</span><span class="sxs-lookup"><span data-stu-id="bfcf6-153">hello metric weights</span></span>
  - <span data-ttu-id="bfcf6-154">현재 메트릭 부하</span><span class="sxs-lookup"><span data-stu-id="bfcf6-154">current metric loads</span></span>
  
<span data-ttu-id="bfcf6-155">실험은 필요한 toodetermine hello 정확 하 게 구성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-155">Experimentation is required toodetermine hello exact configuration necessary.</span></span> <span data-ttu-id="bfcf6-156">프로덕션에서 조각 모음 메트릭을 사용하도록 설정하기 전에 워크로드를 철저하게 측정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="bfcf6-157">조각 모음 및 균형 잡힌된 메트릭은 hello 혼합 하는 경우이 특히 동일한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-157">This is especially true when mixing defragmentation and balanced metrics within hello same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="bfcf6-158">조각 모음 메트릭 구성</span><span class="sxs-lookup"><span data-stu-id="bfcf6-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="bfcf6-159">조각 모음 메트릭 구성 hello 클러스터의 적절 한 글로벌 이며 조각 모음에 대 한 개별 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-159">Configuring defragmentation metrics is a global decision in hello cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="bfcf6-160">다음 구성 조각 hello에 대 한 메트릭을 tooconfigure 조각 모음 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-160">hello following config snippets show how tooconfigure metrics for defragmentation.</span></span> <span data-ttu-id="bfcf6-161">이 경우 "Metric1"는 "Metric2" toobe 균형을 정상적으로 계속 해 서 동안를 조각 모음 기준으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue toobe balanced normally.</span></span> 

<span data-ttu-id="bfcf6-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="bfcf6-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="bfcf6-163">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="bfcf6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfcf6-164">Next steps</span></span>
- <span data-ttu-id="bfcf6-165">클러스터 리소스 관리자 hello에 매뉴얼 hello 클러스터를 설명 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-165">hello Cluster Resource Manager has man options for describing hello cluster.</span></span> <span data-ttu-id="bfcf6-166">toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="bfcf6-166">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="bfcf6-167">메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="bfcf6-167">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="bfcf6-168">메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 및 [이 문서](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="bfcf6-168">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
