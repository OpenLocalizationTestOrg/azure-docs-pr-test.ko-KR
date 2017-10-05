---
title: "Azure Service Fabric 클러스터 분산 | Microsoft Docs"
description: "서비스 패브릭 클러스터 리소스 관리자를 사용한 클러스터 분산에 대한 소개"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="12c72-103">서비스 패브릭 클러스터 분산</span><span class="sxs-lookup"><span data-stu-id="12c72-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="12c72-104">Service Fabric 클러스터 리소스 관리자는 노드나 서비스의 추가 또는 제거에 대응하는 동적 로드 변경을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="12c72-105">또한 제약 조건 위반을 자동으로 수정하고 사전에 로드를 분산하도록 클러스터를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="12c72-106">그러나 이러한 작업은 얼마나 자주 수행될까요? 그리고 이러한 작업을 트리거하는 것은 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="12c72-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="12c72-107">클러스터 리소스 관리자에서 수행하는 세 가지 작업 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="12c72-108">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-108">They are:</span></span>

1. <span data-ttu-id="12c72-109">배치 – 이 단계는 상태 저장 복제본 또는 누락된 상태 비저장 인스턴스 배치를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="12c72-110">배치에는 새로운 서비스와 실패한 상태 저장 복제본 또는 상태 비저장 인스턴스 모두가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="12c72-111">복제본 또는 인스턴스 삭제와 제거도 여기에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="12c72-112">제약 조건 검사 - 이 단계에서는 시스템 내에서 여러 배치 제약 조건(규칙)을 검사하고 위반을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="12c72-113">규칙의 예로는 노드 용량을 초과하지 않고 서비스 배치 제약 조건을 충족하도록 하는 것을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="12c72-114">분산 - 이 단계에서는 다양한 메트릭에 대해 구성된 원하는 수준의 분산에 따라 다시 조정이 필요한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="12c72-115">필요한 경우 더 균형이 맞는 클러스터에서 배치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="12c72-116">클러스터 리소스 관리자 타이머 구성</span><span class="sxs-lookup"><span data-stu-id="12c72-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="12c72-117">균형 조정과 관련된 첫 번째 컨트롤 집합은 타이머 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="12c72-118">이러한 타이머는 클러스터 리소스 관리자에서 클러스터를 검사하고 수정 작업을 수행하는 빈도를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="12c72-119">Cluster Resource Manager에서 수행할 수 있는 이러한 각 형식의 수정 작업은 해당 빈도를 제어하는 다른 타이머에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="12c72-120">각 타이머가 실행되면 작업이 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="12c72-121">기본적으로 Resource Manager는</span><span class="sxs-lookup"><span data-stu-id="12c72-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="12c72-122">1/10초마다 상태를 검색하고 업데이트를 적용합니다(예: 노드가 다운된 기록).</span><span class="sxs-lookup"><span data-stu-id="12c72-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="12c72-123">배치 검사 플래그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-123">sets the placement check flag</span></span> 
* <span data-ttu-id="12c72-124">제약 조건 검사 플래그를 매 초마다 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="12c72-125">분산 플래그를 5초마다 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="12c72-126">이러한 타이머를 관리하는 구성의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="12c72-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="12c72-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="12c72-128">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="12c72-129">현재 클러스터 리소스 관리자에서는 이러한 작업 중 하나를 한 번에 하나씩 순차적으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="12c72-130">이는 이러한 타이머를 "최소 간격"이라고 하며, 타이머가 "설정 플래그"가 되면 수행되도록 하는 동작을 참조하는 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="12c72-131">예를 들어 클러스터 분산에 앞서 서비스를 만들기 위해 Cluster Resource Manager가 보류 중인 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="12c72-132">지정된 기본 시간 간격에서 알 수 있듯이 클러스터 리소스 관리자에서는 자주 수행해야 하는 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="12c72-133">일반적으로 이는 각 단계에서 수행된 변경 집합이 작음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="12c72-134">작은 변경을 자주 수행하면 클러스터에서 상황이 발생할 때 클러스터 리소스 관리자에서 즉각적으로 반응할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="12c72-135">여러 동일한 형식의 이벤트는 동시에 발생하는 경향이 있으므로 기본 타이머가 일부 일괄 처리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="12c72-136">예를 들어 노드가 실패할 경우 전체 장애 도메인 작업을 한 번에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="12c72-137">이러한 모든 실패는 *PLBRefreshGap* 이후의 다음 상태 업데이트에서 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="12c72-138">수정은 다음 배치, 제약 조건 검사 및 분산 실행 중에 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="12c72-139">기본적으로 Cluster Resource Manager는 클러스터에서 변경 시간 내내 검색하는 것이 아니라 모든 변경을 한꺼번에 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="12c72-140">이렇게 하면 갑작스러운 이탈이 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="12c72-141">Cluster Resource Manager는 클러스터의 분산 여부를 판단하기 위해 추가적인 정보도 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="12c72-142">이를 위해 *BalancingThresholds(분산 임계값)*과 *ActivityThresholds(활동 임계값)*의 다른 두 가지 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="12c72-143">분산 임계값</span><span class="sxs-lookup"><span data-stu-id="12c72-143">Balancing thresholds</span></span>
<span data-ttu-id="12c72-144">분산 임계값은 로드 다시 분산을 트리거하기 위한 주요 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="12c72-145">메트릭에 대한 분산 임계값은 _비율_입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="12c72-146">가장 로드가 많은 노드의 메트릭에 대한 로드를 가장 로드가 적은 노드의 로드 양으로 나눈 값이 해당 메트릭의 *BalancingThreshold*를 초과하는 경우 클러스터의 불균형이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="12c72-147">결과적으로 Cluster Resource Manager가 다음 번에 확인할 때 분산이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="12c72-148">*MinLoadBalancingInterval* 타이머는 클러스터 리소스 관리자에서 로드 다시 분산이 필요한지 확인해야 하는 빈도를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="12c72-149">확인은 아무 것도 발생하지 않는다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="12c72-150">분산 임계값은 클러스터 정의의 일부로서 메트릭 단위로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="12c72-151">메트릭에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="12c72-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="12c72-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="12c72-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="12c72-153">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="12c72-154"><center>
![분산 임계값 예][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="12c72-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="12c72-155">이 예제에서는 각 서비스에서 한 단위의 메트릭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="12c72-156">위 예제에서 노드의 최대 부하는 5이고 최소 부하는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="12c72-157">이 메트릭에 대한 분산 임계값이 3이라고 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="12c72-158">클러스터의 비율이 5/2 = 2.5이며 지정된 분산 임계값인 3보다 낮으므로 클러스터는 균형이 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="12c72-159">Cluster Resource Manager가 확인할 때 분산이 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="12c72-160">아래 예에서 노드의 최대 로드는 10이지만 최소 로드는 2이므로 비율은 5입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="12c72-161">5는 해당 메트릭에 지정된 분산 임계값인 3보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="12c72-162">결과적으로 다음번에 분산 타이머가 실행될 때 분산 변경 실행이 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="12c72-163">이와 같은 상황에서 일부 로드는 일반적으로 노드 3에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="12c72-164">Service Fabric 클러스터 리소스 관리자에서 greedy 방식을 사용하지 않으므로 일부 로드가 노드 2에도 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="12c72-165"><center>
![분산 임계값 예제 작업][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="12c72-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="12c72-166">"분산"은 클러스터에서 로드를 관리하기 위한 두 가지 전략을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="12c72-167">클러스터 리소스 관리자에서 사용하는 기본 전략은 클러스터의 노드 간에 로드를 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="12c72-168">다른 전략은 [조각 모음](service-fabric-cluster-resource-manager-defragmentation-metrics.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="12c72-169">조각 모음은 동일한 분산을 실행하는 동안에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="12c72-170">분산 및 조각 모음 전략은 동일한 클러스터 내의 여러 메트릭에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="12c72-171">서비스에서는 분산 및 조각 모음 메트릭을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="12c72-172">조각 모음 메트릭의 경우 분산 임계값보다 _작은_ 경우 클러스터의 로드 비율에서 다시 분산을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="12c72-173">분산 임계값 이하를 달성하는 것이 명시적 목표는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="12c72-174">분산 임계값은 *트리거*입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="12c72-175">분산이 실행될 때 클러스터 리소스 관리자는 자체적으로 수행할 수 있는 향상된 기능(있는 경우)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="12c72-176">분산 검색이 시작되었기 때문에 어떤 항목도 이동하지 않는다는 의미는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="12c72-177">때로는 클러스터에서 분산되지 않지만 너무 제한되어 수정하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="12c72-178">또는 향상된 기능이 이동해야 하지만 [비용이 많이 들 수도](service-fabric-cluster-resource-manager-movement-cost.md) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="12c72-179">활동 임계값</span><span class="sxs-lookup"><span data-stu-id="12c72-179">Activity thresholds</span></span>
<span data-ttu-id="12c72-180">경우에 따라 노드가 상대적으로 불균형하기도 하지만 클러스터의 *총* 부하량은 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="12c72-181">이러한 현상은 일시적인 감소이거나, 새 클러스터가 막 부트스트랩되었기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="12c72-182">어느 경우든 얻을 수 있는 이득이 거의 없기 때문에 클러스터 분산에 시간을 투자하지 않으려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="12c72-183">클러스터가 분산을 거쳤다면 *절대적인* 큰 차이를 만들지 않고 네트워크와 계산 리소스를 사용하여 항목을 이동한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="12c72-184">이처럼 불필요한 이동을 방지하기 위해 활동 임계값이라고 하는 다른 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="12c72-185">활동 임계값을 사용하면 활동에 대해 일부 절대 하한값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="12c72-186">이 임계값을 초과하는 노드가 없으면 분산 임계값에 도달해도 분산이 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="12c72-187">이 메트릭에 대해 세 개의 분산 임계값을 유지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="12c72-188">활동 임계값도 1,536이라고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="12c72-189">첫 번째 경우에서 분산 임계값에 따르면 클러스터는 불균형 상태이지만 활동 임계값을 충족하는 노드가 없으므로 아무 일도 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="12c72-190">아래 예에서 노드 1은 활동 임계값을 초과했습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="12c72-191">메트릭에 대한 분산 임계값과 활동 임계값이 모두 초과되었으므로 분산이 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="12c72-192">예를 들어 다음 다이어그램을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="12c72-193"><center>
![활동 임계값 예][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="12c72-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="12c72-194">분산 임계값과 마찬가지로 활동 임계값은 클러스터 정의를 통한 메트릭을 기준으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="12c72-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="12c72-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="12c72-196">독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="12c72-197">분산 및 활동 임계값은 모두 특정 메트릭에 연결됩니다. 분산은 동일한 메트릭에 대해 분산 임계값과 활동 임계값을 모두 초과한 경우에만 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="12c72-198">분산 서비스 함께 사용</span><span class="sxs-lookup"><span data-stu-id="12c72-198">Balancing services together</span></span>
<span data-ttu-id="12c72-199">클러스터가 분산되지 않는지 여부는 클러스터 전체의 결정입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="12c72-200">그러나 해결하는 방법은 개별 서비스 복제본과 인스턴스를 움직이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="12c72-201">참 합리적이지 않은가요?</span><span class="sxs-lookup"><span data-stu-id="12c72-201">This makes sense, right?</span></span> <span data-ttu-id="12c72-202">메모리가 한 노드에 쌓여 있다면 여러 복제본이나 인스턴스가 여기에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="12c72-203">불균형을 해결하려면 불균형 상태인 메트릭을 사용하는 상태 저장 복제본이나 상태 비저장 인스턴스를 움직여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="12c72-204">그러나 때때로 자체적으로 분산되지 않는 서비스가 이동됩니다(이전의 로컬 및 전역 가중치에 대한 논의를 상기함).</span><span class="sxs-lookup"><span data-stu-id="12c72-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="12c72-205">모든 서비스의 메트릭이 분산되었을 때 서비스가 이동하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="12c72-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="12c72-206">예를 들어 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-206">Let’s see an example:</span></span>

- <span data-ttu-id="12c72-207">4개 서비스, 즉 서비스 1, 서비스 2, 서비스 3 및 서비스 4를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="12c72-208">서비스 1에서 메트릭 1 및 메트릭 2를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="12c72-209">서비스 2에서 메트릭 2 및 메트릭 3을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="12c72-210">서비스 3에서 메트릭 3 및 메트릭 4를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="12c72-211">서비스 4에서 메트릭 99를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="12c72-212">확실히 여기에 있다는 것을 알 수 있습니다. 즉 체인이 있습니다!</span><span class="sxs-lookup"><span data-stu-id="12c72-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="12c72-213">실제로 4개의 독립된 서비스가 있는 것이 아니라, 3개의 서비스가 관련되어 있고 하나는 자체적으로 꺼져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="12c72-214"><center>
![분산 서비스 함께 사용][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="12c72-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="12c72-215">이 체인으로 인해 메트릭 1-4가 분산되지 않으므로 서비스 1-3에 속한 복제본 또는 인스턴스가 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="12c72-216">메트릭 1, 2 또는 3이 분산되지 않으므로 서비스 4에서 이동이 발생하지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="12c72-217">서비스 4에 속한 복제본 또는 인스턴스를 이동해도 메트릭 1-3의 분산에 아무런 영향을 주지 않기 때문에 전혀 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="12c72-218">클러스터 리소스 관리자는 관련된 서비스를 자동으로 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="12c72-219">서비스에 대한 메트릭을 추가, 제거 또는 변경하면 이러한 관계에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="12c72-220">예를 들어 분산이 두 번 실행되는 동안 서비스 2에서 메트릭 2를 제거하도록 업데이트되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="12c72-221">이를 통해 Service1와 Service2 사이의 체인이 끊깁니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="12c72-222">이제는 관련된 두 개의 서비스 그룹 대신 세 개 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="12c72-223"><center>
![분산 서비스 함께 사용][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="12c72-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="12c72-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12c72-224">Next steps</span></span>
* <span data-ttu-id="12c72-225">메트릭은 서비스 패브릭 클러스터 리소스 관리자가 클러스터의 소비와 용량을 관리하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="12c72-226">메트릭 및 구성 방법에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="12c72-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="12c72-227">이동 비용은 특정 서비스가 다른 서비스에 비해 이동하는 데 비용이 더 많이 드는 것을 클러스터 리소스 관리자에게 알리는 한 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="12c72-228">이동 비용에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-movement-cost.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12c72-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="12c72-229">클러스터 리소스 관리자에는 클러스터에서 이탈을 늦추도록 구성할 수 있는 몇 가지 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12c72-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="12c72-230">일반적으로 필요하지는 않지만 필요할 경우 [여기](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="12c72-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
