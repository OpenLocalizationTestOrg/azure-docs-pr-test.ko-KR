---
title: "hello 서비스 패브릭 클러스터 리소스 관리자의 aaaThrottling | Microsoft Docs"
description: "Hello 서비스 패브릭 클러스터 리소스 관리자에서 제공 하는 tooconfigure hello 스로틀에 알아봅니다."
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
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a><span data-ttu-id="72adf-103">Hello 서비스 패브릭 클러스터 리소스 관리자를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-103">Throttling hello Service Fabric Cluster Resource Manager</span></span>
<span data-ttu-id="72adf-104">클러스터 리소스 관리자 hello을 올바르게 구성한 경우에 hello 클러스터 중단 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-104">Even if you’ve configured hello Cluster Resource Manager correctly, hello cluster can get disrupted.</span></span> <span data-ttu-id="72adf-105">예를 들어 동시 노드 및 오류 도메인 오류-업그레이드 하는 동안 발생 한 경우 어떻게 되는지 있을 수 있습니까? 클러스터 리소스 관리자 hello 항상 시도 toofix hello 클러스터 tooreorganize 및 해결 하는 hello 클러스터의 리소스를 사용 하 여 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-105">For example, there could be simultaneous node and fault domain failures - what would happen if that occurred during an upgrade? hello Cluster Resource Manager always tries toofix everything, consuming hello cluster's resources trying tooreorganize and fix hello cluster.</span></span> <span data-ttu-id="72adf-106">스로틀 hello 클러스터 리소스 toostabilize צ ְ ײ-hello 노드 돌아와서 있도록 백업을 제공 하는 데 도움이 되 hello 네트워크 파티션을 치료, 수정 된 bits 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-106">Throttles help provide a backstop so that hello cluster can use resources toostabilize - hello nodes come back, hello network partitions heal, corrected bits get deployed.</span></span>

<span data-ttu-id="72adf-107">가 이러한 유형의 상황 toohelp, hello 서비스 패브릭 클러스터 리소스 관리자에 몇 가지 스로틀 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-107">toohelp with these sorts of situations, hello Service Fabric Cluster Resource Manager includes several throttles.</span></span> <span data-ttu-id="72adf-108">이러한 제한은 꽤 큰 장애물입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-108">These throttles are all fairly large hammers.</span></span> <span data-ttu-id="72adf-109">일반적으로 신중한 계획 및 테스트 없이 변경해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-109">Generally they shouldn’t be changed without careful planning and testing.</span></span>

<span data-ttu-id="72adf-110">Hello 클러스터 리소스 관리자의 스로틀을 변경한 경우 조정 해야 해당 tooyour 예상 되는 실제 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-110">If you change hello Cluster Resource Manager's throttles, you should tune them tooyour expected actual load.</span></span> <span data-ttu-id="72adf-111">상황에 따라 긴 toostabilize를 사용 하는 hello 클러스터 것을 의미 하는 경우에 일부 나와 있는 원위치에서 toohave 필요를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-111">You may determine you need toohave some throttles in place, even if it means hello cluster takes longer toostabilize in some situations.</span></span> <span data-ttu-id="72adf-112">테스트는 필요한 toodetermine hello 스로틀에 대 한 올바른 값입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-112">Testing is required toodetermine hello correct values for throttles.</span></span> <span data-ttu-id="72adf-113">스로틀 toobe 충분히 높은 tooallow hello 클러스터 toorespond toochanges 상당한 시간이 필요 하며 충분 한 tooactually 너무 많은 리소스 소비를 방지 하는 하위.</span><span class="sxs-lookup"><span data-stu-id="72adf-113">Throttles need toobe high enough tooallow hello cluster toorespond toochanges in a reasonable amount of time, and low enough tooactually prevent too much resource consumption.</span></span> 

<span data-ttu-id="72adf-114">대부분의 고객을 살펴본 hello 시간 경과 했는데도 문제가 있다면 리소스 제한 된 환경에서 이미 프로그램이 스로틀을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-114">Most of hello time we’ve seen customers use throttles it has been because they were already in a resource constrained environment.</span></span> <span data-ttu-id="72adf-115">몇 가지 예는 각 노드 또는의 많은 상태 저장 복제본 수 toobuild 아닌 디스크에 대 한 제한 된 네트워크 대역폭 것 병렬 toothroughput 제한 사항 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-115">Some examples would be limited network bandwidth for individual nodes, or disks that aren't able toobuild many stateful replicas in parallel due toothroughput limitations.</span></span> <span data-ttu-id="72adf-116">스로틀, 없이 수 있습니다. 작업 toofail 발생 하는 이러한 리소스를 가득 채울 또는 작업 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-116">Without throttles, operations could overwhelm these resources, causing operations toofail or be slow.</span></span> <span data-ttu-id="72adf-117">이러한 상황에서는 고객 스로틀을 사용 하 고 hello 클러스터 tooreach 안정적인 상태 걸리는 시간의 hello 크기를 확장 하는 것을 알고 있는.</span><span class="sxs-lookup"><span data-stu-id="72adf-117">In these situations customers used throttles and knew they were extending hello amount of time it would take hello cluster tooreach a stable state.</span></span> <span data-ttu-id="72adf-118">고객은 또한 제한된 상태에서는 전반적인 안정성이 낮은 상태로 실행될 수 있다는 사실도 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-118">Customers also understood they could end up running at lower overall reliability while they were throttled.</span></span>


## <a name="configuring-hello-throttles"></a><span data-ttu-id="72adf-119">구성 hello 스로틀</span><span class="sxs-lookup"><span data-stu-id="72adf-119">Configuring hello throttles</span></span>

<span data-ttu-id="72adf-120">서비스 패브릭은 hello 복제본 이동 수 제한에 대 한 두 가지 메커니즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-120">Service Fabric has two mechanisms for throttling hello number of replica movements.</span></span> <span data-ttu-id="72adf-121">서비스 패브릭 5.7 이전부터 있던 hello 기본 메커니즘 이동 수의 절대값 수치로 제한 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-121">hello default mechanism that existed before Service Fabric 5.7 represents throttling as an absolute number of moves allowed.</span></span> <span data-ttu-id="72adf-122">이러한 방식이 모든 규모의 클러스터에 맞지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-122">This does not work for clusters of all sizes.</span></span> <span data-ttu-id="72adf-123">특히, 대규모 클러스터 hello 기본값에 대 한 값 너무 작아서도 필요한 경우, 더 작은 클러스터에 아무런 영향을 주지 않고 분산 속도가 크게 느려지지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-123">In particular, for large clusters hello default value can be too small, significantly slowing down balancing even when it is necessary, while having no effect in smaller clusters.</span></span> <span data-ttu-id="72adf-124">이 이전 메커니즘으로 대체 되었습니다. 백분율 기반 조정을 확장성이 좋아집니다 동적 클러스터 서비스는 hello 수의 노드 정기적으로 변경 하십시오.</span><span class="sxs-lookup"><span data-stu-id="72adf-124">This prior mechanism has been superseded by percentage-based throttling, which scales better with dynamic clusters in which hello number of services and nodes change regularly.</span></span>

<span data-ttu-id="72adf-125">hello 스로틀 hello 클러스터에 있는 복제본의 hello 수의 백분율을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-125">hello throttles are based on a percentage of hello number of replicas in hello clusters.</span></span> <span data-ttu-id="72adf-126">표현 hello 규칙을 사용 하는 기반 Percetage 스로틀: "로 이동 하지 마십시오 복제본의 10% 이상을 10 분 간격 에서" 예.</span><span class="sxs-lookup"><span data-stu-id="72adf-126">Percetage based throttles enable expressing hello rule: "do not move more than 10% of replicas in a 10 minute interval", for example.</span></span>

<span data-ttu-id="72adf-127">백분율 기반 조정에 대 한 hello 구성 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-127">hello configuration settings for percentage-based throttling are:</span></span>

  - <span data-ttu-id="72adf-128">Hello 클러스터에 있는 복제본의 총 수 비율로 표현 되 GlobalMovementThrottleThresholdPercentage-이동 언제 든 지 클러스터에서 허용 되는 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-128">GlobalMovementThrottleThresholdPercentage - Maximum number of movements allowed in cluster at any time, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="72adf-129">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-129">0 indicates no limit.</span></span> <span data-ttu-id="72adf-130">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-130">hello default value is 0.</span></span> <span data-ttu-id="72adf-131">이 설정 및 GlobalMovementThrottleThreshold를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-131">If both this setting and GlobalMovementThrottleThreshold are specified, then hello more conservative limit is used.</span></span>
  - <span data-ttu-id="72adf-132">GlobalMovementThrottleThresholdPercentageForPlacement-이동 hello 배치 단계 중에 허용 된 hello 클러스터에 있는 복제본의 총 수 비율로 표현 되는 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-132">GlobalMovementThrottleThresholdPercentageForPlacement - Maximum number of movements allowed during hello placement phase, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="72adf-133">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-133">0 indicates no limit.</span></span> <span data-ttu-id="72adf-134">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-134">hello default value is 0.</span></span> <span data-ttu-id="72adf-135">이 설정 및 GlobalMovementThrottleThresholdForPlacement를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-135">If both this setting and GlobalMovementThrottleThresholdForPlacement are specified, then hello more conservative limit is used.</span></span>
  - <span data-ttu-id="72adf-136">GlobalMovementThrottleThresholdPercentageForBalancing-이동 hello hello 클러스터에 있는 복제본의 총 수 비율로 표현 되는 단계를 분산 하는 동안 허용 된 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-136">GlobalMovementThrottleThresholdPercentageForBalancing - Maximum number of movements allowed during hello balancing phase, expressed as percentage of total number of replicas in hello cluster.</span></span> <span data-ttu-id="72adf-137">0은 제한하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-137">0 indicates no limit.</span></span> <span data-ttu-id="72adf-138">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-138">hello default value is 0.</span></span> <span data-ttu-id="72adf-139">이 설정 및 GlobalMovementThrottleThresholdForBalancing를 지정 하는 경우 다음 hello 보다 보수적 제한이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-139">If both this setting and GlobalMovementThrottleThresholdForBalancing are specified, then hello more conservative limit is used.</span></span>

<span data-ttu-id="72adf-140">Hello 스로틀 백분율을 지정할 때 5 %0.05로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-140">When specifying hello throttle percentage, you'd specify 5% as 0.05.</span></span> <span data-ttu-id="72adf-141">hello 간격 이러한 스로틀 제어 되는 초에 지정 된 GlobalMovementThrottleCountingInterval hello입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-141">hello interval on which these throttles are governed is hello GlobalMovementThrottleCountingInterval, which is specified in seconds.</span></span>


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

<span data-ttu-id="72adf-142">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-142">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

### <a name="default-count-based-throttles"></a><span data-ttu-id="72adf-143">기본 횟수 기반 제한</span><span class="sxs-lookup"><span data-stu-id="72adf-143">Default count based throttles</span></span>
<span data-ttu-id="72adf-144">이 정보는 이전 클러스터가 있거나 클러스터가 업그레이드된 후에도 이러한 구성을 계속 유지하는 경우에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-144">This information is provided in case you have older clusters or still retain these configurations in clusters that have since been upgraded.</span></span> <span data-ttu-id="72adf-145">일반적으로 이러한 hello 백분율을 기준으로 스로틀 위의으로 바뀌는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-145">In general, it is recommended that these are replaced with hello percentage-based throttles above.</span></span> <span data-ttu-id="72adf-146">백분율 기반 조정 하지 않으면 기본적으로 하므로 이러한 스로틀 비활성화 되 고 hello 백분율을 기준으로 스로틀으로 대체 될 때까지 클러스터에 대 한 기본 스로틀 hello 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-146">Since percentage-based throttling is disabled by default, these throttles remain hello default throttles for a cluster until they are disabled and replaced with hello percentage-based throttles.</span></span> 

  - <span data-ttu-id="72adf-147">GlobalMovementThrottleThreshold –이 설정은 일부 시간별 hello 클러스터에 이동 hello 총 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-147">GlobalMovementThrottleThreshold – this setting controls hello total number of movements in hello cluster over some time.</span></span> <span data-ttu-id="72adf-148">hello 기간 hello GlobalMovementThrottleCountingInterval 초에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-148">hello amount of time is specified in seconds as hello GlobalMovementThrottleCountingInterval.</span></span> <span data-ttu-id="72adf-149">hello GlobalMovementThrottleThreshold hello에 대 한 기본값은 1000 및 hello GlobalMovementThrottleCountingInterval hello에 대 한 기본값은 600입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-149">hello default value for hello GlobalMovementThrottleThreshold is 1000 and hello default value for hello GlobalMovementThrottleCountingInterval is 600.</span></span>
  - <span data-ttu-id="72adf-150">MovementPerPartitionThrottleThreshold –이 설정은 일부 시간에 따라 모든 서비스 파티션에 대 한 이동 hello 총 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-150">MovementPerPartitionThrottleThreshold – this setting controls hello total number of movements for any service partition over some time.</span></span> <span data-ttu-id="72adf-151">hello 기간 hello MovementPerPartitionThrottleCountingInterval 초에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-151">hello amount of time is specified in seconds as hello MovementPerPartitionThrottleCountingInterval.</span></span> <span data-ttu-id="72adf-152">hello MovementPerPartitionThrottleThreshold hello에 대 한 기본값은 50 및 hello MovementPerPartitionThrottleCountingInterval hello에 대 한 기본값은 600입니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-152">hello default value for hello MovementPerPartitionThrottleThreshold is 50 and hello default value for hello MovementPerPartitionThrottleCountingInterval is 600.</span></span>

<span data-ttu-id="72adf-153">이 스로틀에 대 한 hello 구성 hello hello 백분율 기반 조정을으로 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-153">hello configuration for these throttles follows hello same pattern as hello percentage-based throttling.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72adf-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72adf-154">Next steps</span></span>
- <span data-ttu-id="72adf-155">toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="72adf-155">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="72adf-156">클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72adf-156">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="72adf-157">toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="72adf-157">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
