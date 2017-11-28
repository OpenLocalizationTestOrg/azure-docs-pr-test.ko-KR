---
title: "Service Fabric 클러스터 리소스 관리자: 이동 비용 | Microsoft Docs"
description: "Service Fabric 서비스의 이동 비용 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="0766a-103">서비스 이동 비용</span><span class="sxs-lookup"><span data-stu-id="0766a-103">Service movement cost</span></span>
<span data-ttu-id="0766a-104">서비스 패브릭 클러스터 리소스 관리자 hello 하는 요소는 동안 toodetermine 어떤 변경 toomake tooa 클러스터는 해당 변경 내용이 hello 비용을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="0766a-105">hello 클러스터 크기를 향상 시킬 수에 대 한 "cost"의 hello 개념 들여서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="0766a-106">분산, 조각 모음 및 기타 요구 사항을 위해 서비스를 이동할 때 비용이 고려됩니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="0766a-107">hello ´ ֲ toomeet hello 요구 사항 hello에 최소 중단 되었거나 비용이 많이 드는 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="0766a-108">서비스 이동에는 최소한의 CPU 시간과 네트워크 대역폭이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="0766a-109">상태 저장 서비스에 대 한 추가 메모리와 디스크를 사용해 이러한 서비스의 상태 hello 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="0766a-110">Azure 서비스 패브릭 클러스터 리소스 관리자를 생성 하는 hello 솔루션의 hello 저하를 최소화 하면 hello 클러스터의 리소스를 불필요 하 게 소비 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="0766a-111">그러나도 않을 hello hello 클러스터의 리소스 할당을 크게 향상 시켜 주는 tooignore 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="0766a-112">hello 클러스터 리소스 관리자는 컴퓨팅 비용 및 toomanage hello 클러스터 시도 하는 동안 제한의 두 가지 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="0766a-113">hello 첫 번째 메커니즘 하기가 이동할 때마다 계산 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="0766a-114">Hello에 대 한 두 개의 솔루션으로 생성 되는 경우 동일한 균형을 맞출 (점수) hello 클러스터 리소스 관리자 (총 이동 수)를 가장 낮은 비용 hello로 하나 hello를 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="0766a-115">이 전략은 효과가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-115">This strategy works well.</span></span> <span data-ttu-id="0766a-116">하지만 복잡한 시스템에서도 기본 또는 정적 부하와 마찬가지로 모든 이동이 동일할 가능성은 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="0766a-117">일부는 훨씬 더 비용이 많이 드는 가능성이 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="0766a-118">이동 비용 설정</span><span class="sxs-lookup"><span data-stu-id="0766a-118">Setting Move Costs</span></span> 
<span data-ttu-id="0766a-119">만들어질 때 서비스에 대 한 hello 기본 이동 비용을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="0766a-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0766a-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="0766a-121">C#:</span><span class="sxs-lookup"><span data-stu-id="0766a-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="0766a-122">수도 지정 하거나 hello 서비스를 만든 후 서비스에 대 한 MoveCost를 동적으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="0766a-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0766a-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="0766a-124">C#:</span><span class="sxs-lookup"><span data-stu-id="0766a-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="0766a-125">복제본별 이동 비용을 동적으로 지정</span><span class="sxs-lookup"><span data-stu-id="0766a-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="0766a-126">hello 이전 조각은 모든 외부 hello 서비스 자체에서 한 번에 전체 서비스에 대 한 MoveCost를 지정 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="0766a-127">그러나 이동 비용이 가장 유용한 경우 hello 이동 비용 특정 서비스 개체의 수명이 따라 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="0766a-128">Hello 아마도 자체 서비스 얼마나 많은 비용이 toomove 한 번의 hello 최상의 파악할 서비스 tooreport 런타임 동안 자신의 개별 이동 비용에 대 한 API가입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="0766a-129">C#:</span><span class="sxs-lookup"><span data-stu-id="0766a-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="0766a-130">이동 비용의 영향</span><span class="sxs-lookup"><span data-stu-id="0766a-130">Impact of move cost</span></span>
<span data-ttu-id="0766a-131">MoveCost에는 0, 낮음, 중간, 높음의 4개 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="0766a-132">MoveCosts 기타, 0을 제외한 상대 tooeach 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="0766a-133">이동 비용이 0 이동 무료 이며 hello 솔루션의 hello 점수에 계산 되지 해야 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="0766a-134">설정 tooHigh 비용의 이전 않습니다 *하지* 한 곳에 유지 되므로 해당 hello 복제본을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="0766a-135"><center>
![이동할 복제본 선택 시의 요인으로 사용되는 이동 비용][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="0766a-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="0766a-136">MoveCost를 사용 하면 원인 중단을 최소화 전반적인 hello 및 쉬운 tooachieve 여전히 해당 균형에 도착 하는 동안에 hello 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="0766a-137">서비스의 개념이 비용의 상대 toomany 작업이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="0766a-138">hello 가장 일반적인 요소 이동 비용 계산에 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="0766a-139">상태 또는 toomove hello 서비스에 데이터의 hello 양입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="0766a-140">클라이언트의 연결이 끊어지는의 hello 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="0766a-141">주 복제본을 이동 하는 것은 일반적으로 보조 복제본을 이동 하는 hello 비용 보다 더 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="0766a-142">진행 중인 작업을 중단의 hello 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="0766a-143">일부 작업 hello 데이터 저장소 수준 또는 응답 tooa 클라이언트 호출에서 수행 하는 작업은 비용이 많이 드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="0766a-144">특정 시점이 지나면 toostop 원하지 경우 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="0766a-145">따라서 hello 작업이 진행 되는 동안에이 서비스 개체 tooreduce hello 가능성을 이동의 hello 이동 비용이 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="0766a-146">Hello 작업이 완료 되 면 hello 비용 백 toonormal을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="0766a-147">클러스터에서 이동 비용 사용</span><span class="sxs-lookup"><span data-stu-id="0766a-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="0766a-148">에 대 한 순서 대로 고려 하는 보다 세부적인 MoveCosts toobe hello, MoveCost 클러스터에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="0766a-149">이 설정이 없으면 hello 기본 모드로 이동 계산 MoveCost, 계산에 사용 되 고 MoveCost 보고서가 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="0766a-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="0766a-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="0766a-151">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="0766a-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0766a-152">Next steps</span></span>
- <span data-ttu-id="0766a-153">서비스 패브릭 클러스터 리소스 관리자 hello 클러스터의 메트릭 toomanage 소비 및 용량을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="0766a-154">메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 하 고 [관리 리소스 소비와 메트릭 사용 하 여 서비스 패브릭에서 부하](service-fabric-cluster-resource-manager-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="0766a-155">toolearn hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 부하를 분산 시키고 방법,에 체크 아웃 [분산 서비스 패브릭 클러스터](service-fabric-cluster-resource-manager-balancing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0766a-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
