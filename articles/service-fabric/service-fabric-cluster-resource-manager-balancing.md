---
title: "aaaBalance Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "소개 toobalancing hello 서비스 패브릭 클러스터 리소스 관리자를 사용 하 여 클러스터입니다."
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="ecd61-103">서비스 패브릭 클러스터 분산</span><span class="sxs-lookup"><span data-stu-id="ecd61-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="ecd61-104">서비스 패브릭 클러스터 리소스 관리자 hello 동적 로드 변경 내용, 응답할 tooadditions 또는 노드 또는 서비스의 제거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="ecd61-105">제약 조건 위반을 자동으로 수정 하 고 사전 hello 클러스터를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="ecd61-106">그러나 이러한 작업은 얼마나 자주 수행될까요? 그리고 이러한 작업을 트리거하는 것은 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="ecd61-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="ecd61-107">해당 hello 클러스터 리소스 관리자가 수행 하는 작업의 세 가지 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="ecd61-108">아래에 이 계정과 키의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-108">They are:</span></span>

1. <span data-ttu-id="ecd61-109">배치 – 이 단계는 상태 저장 복제본 또는 누락된 상태 비저장 인스턴스 배치를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="ecd61-110">배치에는 새로운 서비스와 실패한 상태 저장 복제본 또는 상태 비저장 인스턴스 모두가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="ecd61-111">복제본 또는 인스턴스 삭제와 제거도 여기에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="ecd61-112">제약 조건 검사-이 단계에 대 한 확인 하 고 hello 다른 배치 제약 조건 (규칙) hello 시스템 내에서 위반을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="ecd61-113">규칙의 예로는 노드 용량을 초과하지 않고 서비스 배치 제약 조건을 충족하도록 하는 것을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="ecd61-114">분산-이 단계 toosee 균형 조정이 필요한 경우 hello 구성에 따라 원하는 수준의 다른 메트릭에 대 한 균형을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="ecd61-115">그렇다면 toofind hello에 정렬을 클러스터 즉 분산 더 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="ecd61-116">클러스터 리소스 관리자 타이머 구성</span><span class="sxs-lookup"><span data-stu-id="ecd61-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="ecd61-117">hello 주위 균형 조정 컨트롤의 첫 번째 집합은 타이머의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="ecd61-118">이러한 타이머 얼마나 자주 hello 클러스터 리소스 관리자 hello 클러스터를 검사 하 고 수정 동작을 수행을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="ecd61-119">이러한 각 유형의 다른의 수정 사항 hello 클러스터 리소스 관리자를 만들 수는 해당 빈도 제어 하는 다른 타이머에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="ecd61-120">각 타이머 발생 하는 경우에 hello 작업이 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="ecd61-121">기본적으로 리소스 관리자를 hello:</span><span class="sxs-lookup"><span data-stu-id="ecd61-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="ecd61-122">1/10초마다 상태를 검색하고 업데이트를 적용합니다(예: 노드가 다운된 기록).</span><span class="sxs-lookup"><span data-stu-id="ecd61-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="ecd61-123">hello 배치 확인 플래그를 설정</span><span class="sxs-lookup"><span data-stu-id="ecd61-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="ecd61-124">1 초 마다 hello 제약 조건 검사 플래그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="ecd61-125">분산 플래그 5 초 마다 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="ecd61-126">이러한 타이머를 관리 하는 hello 구성의는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="ecd61-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ecd61-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="ecd61-128">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="ecd61-129">오늘 hello 클러스터 리소스 관리자만 수행 이러한 작업 중 하나가 한 번에 순차적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="ecd61-130">이 때문에 "최소 간격"으로 toothese 타이머를 참조 하 고 hello 플래그로"설정" hello 타이머 꺼질 때 수행 가져오기 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="ecd61-131">예를 들어 보류 중인 클러스터 리소스 관리자를 담당 하는 hello hello 클러스터 균형 조정 하기 전에 toocreate 서비스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="ecd61-132">Hello 기본 시간 간격을 지정 하 여 볼 수 있듯이 hello 클러스터 리소스 관리자를 검사할 항목에 대해 요구 사항을 toodo 자주 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="ecd61-133">일반적으로이 중 각 단계에 변경한 hello 집합이 작은 임을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="ecd61-134">약간 변경 자주 사용 하면 클러스터 리소스 관리자 toobe hello 응답 hello 클러스터에서 상황이 발생할 때.</span><span class="sxs-lookup"><span data-stu-id="ecd61-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="ecd61-135">hello 기본 타이머 제공 몇 가지 일괄 처리 다양 한 hello 이후 동일한 유형의 이벤트는 동시에 toooccur 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="ecd61-136">예를 들어 노드가 실패할 경우 전체 장애 도메인 작업을 한 번에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="ecd61-137">이러한 오류는 hello 다음 상태로 도중 캡처하는 모든 업데이트 hello 후 *PLBRefreshGap*합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="ecd61-138">hello, 배치 제약 조건 검사 하 고 실행을 분산 하는 동안 hello 수정 사항이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="ecd61-139">기본 hello로 클러스터 리소스 관리자는 hello 클러스터의 변경 사항 시간 알아보기가 및 tooaddress 모든 변경 내용을 한 번에 시도 되지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="ecd61-140">이렇게 하면 toobursts는 변동 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="ecd61-141">hello 클러스터 리소스 관리자도 필요 몇 가지 추가 정보 toodetermine hello 클러스터 경우 균형이 맞지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="ecd61-142">이를 위해 *BalancingThresholds(분산 임계값)*과 *ActivityThresholds(활동 임계값)*의 다른 두 가지 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="ecd61-143">분산 임계값</span><span class="sxs-lookup"><span data-stu-id="ecd61-143">Balancing thresholds</span></span>
<span data-ttu-id="ecd61-144">균형 조정 임계값은 hello를 리 밸런스 트리거하 주 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="ecd61-145">hello 메트릭에 대 한 균형 조정 임계값은 한 _비율_합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="ecd61-146">노드 초과 하는 해당 메트릭이 hello에 메트릭에 대 한 hello 부하 가장 적은 hello에 hello 양의 부하로 나눈 값 노드를 로드 하는 경우 *BalancingThreshold*, hello 클러스터 불균형 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="ecd61-147">결과적으로 균형 조정은 트리거된 hello 다음 시간 hello 클러스터 리소스 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="ecd61-148">hello *MinLoadBalancingInterval* 타이머 얼마나 자주 hello 클러스터 리소스 관리자 확인 해야 균형 조정이 필요한 경우를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="ecd61-149">확인은 아무 것도 발생하지 않는다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="ecd61-150">균형 조정 임계값 메트릭을 당 별로 hello 클러스터 정의의 일부로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="ecd61-151">메트릭에 대한 자세한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ecd61-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="ecd61-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="ecd61-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="ecd61-153">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="ecd61-154"><center>
![분산 임계값 예][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="ecd61-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="ecd61-155">이 예제에서는 각 서비스에서 한 단위의 메트릭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="ecd61-156">Hello 상위 예에서 노드에서 hello 최대 부하는 5 하 고 hello 최소값은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="ecd61-157">이 메트릭에 대 한 임계값을 분산 하는 hello는 3 개입니다 경우를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="ecd61-158">Hello 클러스터에서 hello 비율이 5/2 이므로 = 2.5 및 즉 hello 3 hello 클러스터의 임계값을 분산 균형이 조정 된 지정 된 것 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="ecd61-159">분산 없음은 hello 클러스터 리소스 관리자를 확인 하는 경우에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="ecd61-160">Hello 아래 예제에서는 노드의 최대 부하 hello은 hello 최소값은 2, 5의 비율이 동안 10,입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="ecd61-161">포함 된 5의 경우 해당 메트릭에 대 한 세 hello 지정 된 균형 조정 임계값 보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="ecd61-162">결과적으로, 균형 조정 실행 되는 예약 된 다음 번 hello 타이머 발생 균형 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="ecd61-163">이런 경우 몇 가지 부하가 tooNode3 일반적으로 분산된 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="ecd61-164">서비스 패브릭 클러스터 리소스 관리자 hello greedy 접근 방식을 사용 하지 않습니다, 때문에 일부 부하 분산된 tooNode2 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="ecd61-165"><center>
![분산 임계값 예제 작업][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="ecd61-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="ecd61-166">"분산"은 클러스터에서 로드를 관리하기 위한 두 가지 전략을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="ecd61-167">클러스터 리소스 관리자 사용 하 여 hello hello 기본 전략은 hello 클러스터의 hello 노드에서 toodistribute load입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="ecd61-168">hello 다른 전략은 [조각 모음](service-fabric-cluster-resource-manager-defragmentation-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="ecd61-169">Hello 중 조각 모음을 실행 하는 동일한 분산 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="ecd61-170">hello 분산과 조각 모음 전략에 사용할 수 있습니다 다른 메트릭은 hello 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="ecd61-171">서비스에서는 분산 및 조각 모음 메트릭을 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="ecd61-172">조각 모음 메트릭에 대 한 hello의 hello 비율 로드 되었을 때를 리 밸런스 hello 클러스터 트리거 _아래_ hello 임계값 균형 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="ecd61-173">임계값을 분산 하는 hello 아래 가져오는 것은 명시적 목표 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="ecd61-174">분산 임계값은 *트리거*입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="ecd61-175">실행 부하를 분산 시키는 hello 클러스터 리소스 관리자 있는 경우 수행할 수 있는 향상 된 기능을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="ecd61-176">분산 검색이 시작되었기 때문에 어떤 항목도 이동하지 않는다는 의미는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="ecd61-177">경우에 따라 hello 클러스터는 불균형 하지만 너무 제한 된 toocorrect입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="ecd61-178">Hello 향상도 이동 해야 하는 또는 [비용이 많이 드는](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="ecd61-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="ecd61-179">활동 임계값</span><span class="sxs-lookup"><span data-stu-id="ecd61-179">Activity thresholds</span></span>
<span data-ttu-id="ecd61-180">노드는 비교적 불균형, 경우에 따라 hello *총* hello 클러스터의 부하의 양은 적습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="ecd61-181">자격 증명 부하 hello 부족 일시적인 dip 수 또는 hello 클러스터는 새롭고 바로 가져오기 때문에 부트스트랩 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="ecd61-182">두 경우 모두 할 필요가 거의 toobe 얻은 있기 때문에 분산 hello 클러스터 toospend 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="ecd61-183">Hello 클러스터 분산 했습니다, 하는 경우 네트워크를 소비 하는 모든 큰 하지 않고 리소스 toomove 작업만 계산 *절대* 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="ecd61-184">활동 임계값으로 알려진 다른 제어 방법이 tooavoid 불필요 한 이동입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="ecd61-185">활동 임계값 toospecify를 활동에 대 한 절대 하한값 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="ecd61-186">노드가 없으면이 임계값을 초과 이면 hello 균형 조정 임계값을 충족 하는 경우에 발생 되지 않습니다 균형 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="ecd61-187">이 메트릭에 대해 세 개의 분산 임계값을 유지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="ecd61-188">활동 임계값도 1,536이라고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="ecd61-189">Hello 첫 번째 경우에 hello 클러스터는 hello 당 균형이 맞지 않는 균형 조정 임계값 없는 노드 충족 활동 임계값에를 발생 하므로 아무것도 표시 되지 않음.</span><span class="sxs-lookup"><span data-stu-id="ecd61-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="ecd61-190">Node1은 hello 아래 예제에서는 활동 임계값 hello 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="ecd61-191">균형 조정 임계값 hello 둘 다 이므로 hello 메트릭에 대 한 hello 활동 임계값이 초과 되는 예약 된 균형 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="ecd61-192">예를 들어 살펴보겠습니다 다이어그램을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="ecd61-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="ecd61-193"><center>
![활동 임계값 예][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="ecd61-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="ecd61-194">균형 조정 임계값와 동일 하 게 활동 임계값에는 정의 된 당-메트릭을 통해 hello 클러스터 정의</span><span class="sxs-lookup"><span data-stu-id="ecd61-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="ecd61-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="ecd61-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="ecd61-196">독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="ecd61-197">균형 조정 및 활동 임계값이 모두 동률된 tooa 특정 메트릭을-분산 균형 조정 임계값 hello 모두 hello에 대 한 활동 임계값을 초과 하는 경우에 트리거됩니다 동일한 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="ecd61-198">분산 서비스 함께 사용</span><span class="sxs-lookup"><span data-stu-id="ecd61-198">Balancing services together</span></span>
<span data-ttu-id="ecd61-199">Hello 클러스터 불균형 인지 여부를 클러스터 전체 의사 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="ecd61-200">그러나 개별 서비스 복제본과 인스턴스 문제를 해결 하는 방법에 대 한 있네요 hello 방식으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="ecd61-201">참 합리적이지 않은가요?</span><span class="sxs-lookup"><span data-stu-id="ecd61-201">This makes sense, right?</span></span> <span data-ttu-id="ecd61-202">메모리는 한 노드에서 쌓입니다, 여러 복제본 또는 인스턴스 tooit을 원인이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="ecd61-203">해결 hello 불균형 hello 상태 저장 복제본 또는 hello 균형이 맞지 않는 메트릭을 사용 하는 상태 비저장 인스턴스 이동 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="ecd61-204">그러나을 받았으나 불균형 자체 서비스 옮긴 (hello 설명 참조의 로컬 및 전역 가중치를 이전 버전).</span><span class="sxs-lookup"><span data-stu-id="ecd61-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="ecd61-205">모든 서비스의 메트릭이 분산되었을 때 서비스가 이동하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ecd61-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="ecd61-206">예를 들어 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-206">Let’s see an example:</span></span>

- <span data-ttu-id="ecd61-207">4개 서비스, 즉 서비스 1, 서비스 2, 서비스 3 및 서비스 4를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="ecd61-208">서비스 1에서 메트릭 1 및 메트릭 2를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="ecd61-209">서비스 2에서 메트릭 2 및 메트릭 3을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="ecd61-210">서비스 3에서 메트릭 3 및 메트릭 4를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="ecd61-211">서비스 4에서 메트릭 99를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="ecd61-212">확실히 여기에 있다는 것을 알 수 있습니다. 즉 체인이 있습니다!</span><span class="sxs-lookup"><span data-stu-id="ecd61-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="ecd61-213">실제로 4개의 독립된 서비스가 있는 것이 아니라, 3개의 서비스가 관련되어 있고 하나는 자체적으로 꺼져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="ecd61-214"><center>
![분산 서비스 함께 사용][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="ecd61-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="ecd61-215">이 체인으로 인해 메트릭 1-4 불균형 될 수 있다는 복제본 또는 tooservices 속하는 인스턴스가 주위 1-3 toomove 수는.</span><span class="sxs-lookup"><span data-stu-id="ecd61-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="ecd61-216">메트릭 1, 2 또는 3이 분산되지 않으므로 서비스 4에서 이동이 발생하지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="ecd61-217">Hello 복제본 이동 이후 지점이 없는 것 하거나 수 주위 tooService4 속하는 인스턴스가 절대 tooimpact hello 균형 메트릭 1-3입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="ecd61-218">자동으로 hello 클러스터 리소스 관리자는 서비스와 관련 된 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="ecd61-219">추가, 제거 또는 서비스에 대 한 변경 hello 메트릭 간의 관계를 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="ecd61-220">예를 들어 Service2 분산의 두 실행 간의 되었을 수 있습니다 Metric2 tooremove를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="ecd61-221">Service1와 Service2 사이의 hello 체인을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="ecd61-222">이제는 관련된 두 개의 서비스 그룹 대신 세 개 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="ecd61-223"><center>
![분산 서비스 함께 사용][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="ecd61-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="ecd61-224">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecd61-224">Next steps</span></span>
* <span data-ttu-id="ecd61-225">메트릭은 hello 서비스 패브릭 클러스터 리소스 관리자에서 소비 되 고 hello 클러스터의 용량을 관리 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="ecd61-226">메트릭에 대 한 자세한 toolearn 어떻게 tooconfigure, 체크 아웃 및 [이 문서](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="ecd61-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="ecd61-227">이동 비용은 하나의 방법 특정 서비스는 다른 항목 보다 더 비용이 많이 드는 toomove toohello 클러스터 리소스 관리자 신호입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="ecd61-228">이동 비용에 대 한 자세한 참조 너무[이 문서](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="ecd61-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="ecd61-229">hello 클러스터 리소스 관리자에는 몇 가지 스로틀 hello 클러스터에서 변동 아래로 tooslow를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd61-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="ecd61-230">일반적으로 필요하지는 않지만 필요할 경우 [여기](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="ecd61-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
