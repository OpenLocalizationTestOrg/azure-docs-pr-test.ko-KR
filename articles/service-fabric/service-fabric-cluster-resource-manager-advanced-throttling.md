---
title: "Service Fabric 클러스터 리소스 관리자의 제한 | Microsoft Docs"
description: "서비스 패브릭 클러스터 리소스 관리자에서 제공하는 제한을 구성하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 1be0beaf2e199a9c384187efd80b33c7dab5e87c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="throttling-the-service-fabric-cluster-resource-manager"></a><span data-ttu-id="63b93-103">Service Fabric Cluster Resource Manager 제한</span><span class="sxs-lookup"><span data-stu-id="63b93-103">Throttling the Service Fabric Cluster Resource Manager</span></span>
<span data-ttu-id="63b93-104">클러스터 Resource Manager를 올바르게 구성한 경우에도 클러스터가 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-104">Even if you’ve configured the Cluster Resource Manager correctly, the cluster can get disrupted.</span></span> <span data-ttu-id="63b93-105">예를 들어 동시 노드 및 장애 도메인 오류가 있을 수 있습니다. 업그레이드 중에 이러한 문제가 발생하면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="63b93-105">For example, there could be simultaneous node and fault domain failures - what would happen if that occurred during an upgrade?</span></span> <span data-ttu-id="63b93-106">Cluster Resource Manager는 항상 모든 항목을 수정하려고 시도하며 클러스터의 리소스를 사용하여 클러스터를 다시 구성하고 문제를 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-106">The Cluster Resource Manager always tries to fix everything, consuming the cluster's resources trying to reorganize and fix the cluster.</span></span> <span data-ttu-id="63b93-107">제한은 클러스터가 리소스를 사용하여 안정화(노드 다시 작동, 네트워크 파티션 정상화, 수정된 비트 배포)할 수 있도록 방어벽을 제공하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-107">Throttles help provide a backstop so that the cluster can use resources to stabilize - the nodes come back, the network partitions heal, corrected bits get deployed.</span></span>

<span data-ttu-id="63b93-108">이러한 상황을 위해 Service Fabric 클러스터 Resource Manager는 여러 가지 제한을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-108">To help with these sorts of situations, the Service Fabric Cluster Resource Manager includes several throttles.</span></span> <span data-ttu-id="63b93-109">이러한 제한은 꽤 큰 장애물입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-109">These throttles are all fairly large hammers.</span></span> <span data-ttu-id="63b93-110">일반적으로 신중한 계획 및 테스트 없이 변경해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-110">Generally they shouldn’t be changed without careful planning and testing.</span></span>

<span data-ttu-id="63b93-111">Cluster Resource Manager의 제한을 변경하는 경우 예상되는 실제 부하에 맞게 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-111">If you change the Cluster Resource Manager's throttles, you should tune them to your expected actual load.</span></span> <span data-ttu-id="63b93-112">일부 상황에서 클러스터 안정화에 시간이 더 오래 걸리더라도 일부 제한을 설정해야 하는지 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-112">You may determine you need to have some throttles in place, even if it means the cluster takes longer to stabilize in some situations.</span></span> <span data-ttu-id="63b93-113">올바른 제한 값을 결정하기 위한 테스트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-113">Testing is required to determine the correct values for throttles.</span></span> <span data-ttu-id="63b93-114">제한은 클러스터가 적절한 시간 내에 변경에 응답할 수 있을 만큼 충분히 크고, 너무 많은 리소스 소비를 실제로 방지할 만큼 충분히 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-114">Throttles need to be high enough to allow the cluster to respond to changes in a reasonable amount of time, and low enough to actually prevent too much resource consumption.</span></span> 

<span data-ttu-id="63b93-115">대부분의 경우 고객은 이미 리소스 제약 환경을 사용하고 있기 때문에 예전부터 제한을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-115">Most of the time we’ve seen customers use throttles it has been because they were already in a resource constrained environment.</span></span> <span data-ttu-id="63b93-116">몇 가지 예로 개별 노드 또는 디스크로 제한된 네트워크 대역폭이 있습니다. 이 경우 처리량 제한으로 인해 많은 상태 저장 복제본을 동시에 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-116">Some examples would be limited network bandwidth for individual nodes, or disks that aren't able to build many stateful replicas in parallel due to throughput limitations.</span></span> <span data-ttu-id="63b93-117">제한을 사용하지 않으면 리소스에 비해 작업이 너무 많아져 실패하거나 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-117">Without throttles, operations could overwhelm these resources, causing operations to fail or be slow.</span></span> <span data-ttu-id="63b93-118">이러한 상황에서 고객은 제한을 사용하면서 클러스터가 안정적인 상태에 도달하는 데 걸리는 시간이 더 길어진다는 것을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-118">In these situations customers used throttles and knew they were extending the amount of time it would take the cluster to reach a stable state.</span></span> <span data-ttu-id="63b93-119">고객은 또한 제한된 상태에서는 전반적인 안정성이 낮은 상태로 실행될 수 있다는 사실도 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-119">Customers also understood they could end up running at lower overall reliability while they were throttled.</span></span>


## <a name="configuring-the-throttles"></a><span data-ttu-id="63b93-120">제한 구성</span><span class="sxs-lookup"><span data-stu-id="63b93-120">Configuring the throttles</span></span>

<span data-ttu-id="63b93-121">Service Fabric에는 복제본 이동 수를 제한하는 두 가지 메커니즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-121">Service Fabric has two mechanisms for throttling the number of replica movements.</span></span> <span data-ttu-id="63b93-122">Service Fabric 5.7 이전에 존재하던 기본 메커니즘은 이러한 제한을 허용되는 절대 이동 횟수로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-122">The default mechanism that existed before Service Fabric 5.7 represents throttling as an absolute number of moves allowed.</span></span> <span data-ttu-id="63b93-123">이러한 방식이 모든 규모의 클러스터에 맞지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-123">This does not work for clusters of all sizes.</span></span> <span data-ttu-id="63b93-124">특히 대규모 클러스터의 경우는 이 기본값이 너무 작을 수 있으며 반드시 필요한 경우에도 더 작은 클러스터에는 영향을 미치지 않으면서 부하 분산 작업을 상당히 느려지게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-124">In particular, for large clusters the default value can be too small, significantly slowing down balancing even when it is necessary, while having no effect in smaller clusters.</span></span> <span data-ttu-id="63b93-125">이러한 이전 메커니즘은 동적 클러스터에서 더 잘 확장되는 비율 기반 제한으로 대체되었습니다. 이 제한에서는 서비스 및 노드 수가 정기적으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-125">This prior mechanism has been superseded by percentage-based throttling, which scales better with dynamic clusters in which the number of services and nodes change regularly.</span></span>

<span data-ttu-id="63b93-126">이러한 제한은 클러스터에 있는 복제본의 수 비율을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-126">The throttles are based on a percentage of the number of replicas in the clusters.</span></span> <span data-ttu-id="63b93-127">비율 기반 제한을 사용하면 예를 들어 "10분 간격으로 복제본의 10% 이상을 이동하지 마세요."와 같은 규칙을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-127">Percetage based throttles enable expressing the rule: "do not move more than 10% of replicas in a 10 minute interval", for example.</span></span>

<span data-ttu-id="63b93-128">비율 기반 제한에 대한 구성 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-128">The configuration settings for percentage-based throttling are:</span></span>

  - <span data-ttu-id="63b93-129">GlobalMovementThrottleThresholdPercentage - 클러스터에 있는 복제본의 총 수에 대한 비율로 표시되는 클러스터에 한 번에 허용되는 최대 이동 횟수.</span><span class="sxs-lookup"><span data-stu-id="63b93-129">GlobalMovementThrottleThresholdPercentage - Maximum number of movements allowed in cluster at any time, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="63b93-130">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-130">0 indicates no limit.</span></span> <span data-ttu-id="63b93-131">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-131">The default value is 0.</span></span> <span data-ttu-id="63b93-132">이 설정 및 GlobalMovementThrottleThreshold를 둘 다 지정하는 경우 좀 더 일반적인 제한이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-132">If both this setting and GlobalMovementThrottleThreshold are specified, then the more conservative limit is used.</span></span>
  - <span data-ttu-id="63b93-133">GlobalMovementThrottleThresholdPercentageForPlacement - 클러스터에 있는 복제본의 총 수에 대한 비율로 표시되는 배치 단계 동안 허용되는 최대 이동 횟수.</span><span class="sxs-lookup"><span data-stu-id="63b93-133">GlobalMovementThrottleThresholdPercentageForPlacement - Maximum number of movements allowed during the placement phase, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="63b93-134">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-134">0 indicates no limit.</span></span> <span data-ttu-id="63b93-135">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-135">The default value is 0.</span></span> <span data-ttu-id="63b93-136">이 설정 및 GlobalMovementThrottleThresholdForPlacement를 둘 다 지정하는 경우 좀 더 일반적인 제한이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-136">If both this setting and GlobalMovementThrottleThresholdForPlacement are specified, then the more conservative limit is used.</span></span>
  - <span data-ttu-id="63b93-137">GlobalMovementThrottleThresholdPercentageForBalancing - 클러스터에 있는 복제본의 총 수에 대한 비율로 표시되는 부하 분산 단계 동안 허용되는 최대 이동 횟수.</span><span class="sxs-lookup"><span data-stu-id="63b93-137">GlobalMovementThrottleThresholdPercentageForBalancing - Maximum number of movements allowed during the balancing phase, expressed as percentage of total number of replicas in the cluster.</span></span> <span data-ttu-id="63b93-138">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-138">0 indicates no limit.</span></span> <span data-ttu-id="63b93-139">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-139">The default value is 0.</span></span> <span data-ttu-id="63b93-140">이 설정 및 GlobalMovementThrottleThresholdForBalancing을 둘 다 지정하는 경우 좀 더 일반적인 제한이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-140">If both this setting and GlobalMovementThrottleThresholdForBalancing are specified, then the more conservative limit is used.</span></span>

<span data-ttu-id="63b93-141">제한 비율을 지정할 때 5%를 0.05로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-141">When specifying the throttle percentage, you'd specify 5% as 0.05.</span></span> <span data-ttu-id="63b93-142">이러한 제한이 관리되는 간격은 GlobalMovementThrottleCountingInterval(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-142">The interval on which these throttles are governed is the GlobalMovementThrottleCountingInterval, which is specified in seconds.</span></span>


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

<span data-ttu-id="63b93-143">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-143">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a><span data-ttu-id="63b93-144">기본 횟수 기반 제한</span><span class="sxs-lookup"><span data-stu-id="63b93-144">Default count based throttles</span></span>
<span data-ttu-id="63b93-145">이 정보는 이전 클러스터가 있거나 클러스터가 업그레이드된 후에도 이러한 구성을 계속 유지하는 경우에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-145">This information is provided in case you have older clusters or still retain these configurations in clusters that have since been upgraded.</span></span> <span data-ttu-id="63b93-146">일반적으로 이러한 제한은 위의 비율 기반 제한으로 바꾸는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-146">In general, it is recommended that these are replaced with the percentage-based throttles above.</span></span> <span data-ttu-id="63b93-147">비율 기반 제한은 기본적으로 사용되지 않도록 설정되므로 이러한 제한은 사용하지 않도록 설정하거나 비율 기반 제한으로 바꿀 때까지 클러스터의 기본 제한으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-147">Since percentage-based throttling is disabled by default, these throttles remain the default throttles for a cluster until they are disabled and replaced with the percentage-based throttles.</span></span> 

  - <span data-ttu-id="63b93-148">GlobalMovementThrottleThreshold – 일정 시간 동안 클러스터 내에서 발생하는 총 이동 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-148">GlobalMovementThrottleThreshold – this setting controls the total number of movements in the cluster over some time.</span></span> <span data-ttu-id="63b93-149">기간은 GlobalMovementThrottleCountingInterval(초)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-149">The amount of time is specified in seconds as the GlobalMovementThrottleCountingInterval.</span></span> <span data-ttu-id="63b93-150">GlobalMovementThrottleThreshold의 기본값은 1000이고 GlobalMovementThrottleCountingInterval의 기본값은 600입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-150">The default value for the GlobalMovementThrottleThreshold is 1000 and the default value for the GlobalMovementThrottleCountingInterval is 600.</span></span>
  - <span data-ttu-id="63b93-151">MovementPerPartitionThrottleThreshold – 일정 시간 동안 서비스 파티션에 대해 발생하는 총 이동 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-151">MovementPerPartitionThrottleThreshold – this setting controls the total number of movements for any service partition over some time.</span></span> <span data-ttu-id="63b93-152">기간은 MovementPerPartitionThrottleCountingInterval(초)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-152">The amount of time is specified in seconds as the MovementPerPartitionThrottleCountingInterval.</span></span> <span data-ttu-id="63b93-153">MovementPerPartitionThrottleThreshold의 기본값은 50이고 MovementPerPartitionThrottleCountingInterval의 기본값은 600입니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-153">The default value for the MovementPerPartitionThrottleThreshold is 50 and the default value for the MovementPerPartitionThrottleCountingInterval is 600.</span></span>

<span data-ttu-id="63b93-154">이러한 제한의 구성은 비율 기반 제한과 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-154">The configuration for these throttles follows the same pattern as the percentage-based throttling.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63b93-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63b93-155">Next steps</span></span>
- <span data-ttu-id="63b93-156">클러스터 Resource Manager가 클러스터의 부하를 관리하고 분산하는 방법을 알아보려면 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="63b93-156">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="63b93-157">클러스터 Resource Manager에는 클러스터를 설명하기 위한 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63b93-157">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="63b93-158">이에 대해 자세히 알아보려면 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)에 대한 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="63b93-158">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
