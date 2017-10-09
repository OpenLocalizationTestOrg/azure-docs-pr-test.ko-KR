---
title: "aaaService 패브릭 클러스터 리소스 관리자-응용 프로그램 그룹 | Microsoft Docs"
description: "Hello hello 서비스 패브릭 클러스터 리소스 관리자에서에서 응용 프로그램 그룹 기능 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="6f1e3-103">소개 tooApplication 그룹</span><span class="sxs-lookup"><span data-stu-id="6f1e3-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="6f1e3-104">서비스 패브릭 클러스터 리소스 관리자 hello 부하를 분산 함으로써 클러스터 리소스는 일반적으로 관리 (을 통해 나타낼 [메트릭](service-fabric-cluster-resource-manager-metrics.md)) hello 클러스터 전체에서 균등 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="6f1e3-105">서비스 패브릭 관리를 통해 전체 hello 클러스터와 hello 클러스터의 hello 노드 hello 용량 [용량](service-fabric-cluster-resource-manager-cluster-description.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="6f1e3-106">메트릭과 용량은 다양한 워크로드에 잘 적용되지만 서로 다른 Service Fabric 응용 프로그램 인스턴스를 과도하게 사용하는 패턴은 때때로 추가 요구 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="6f1e3-107">예를 들어 다음을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-107">For example you may want to:</span></span>

- <span data-ttu-id="6f1e3-108">예약 일부 응용 프로그램 명명 된 인스턴스 내에서 hello 서비스에 대 한 hello 클러스터의 hello 노드에서 일부 용량</span><span class="sxs-lookup"><span data-stu-id="6f1e3-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="6f1e3-109">Hello 총 (hello 전체 클러스터를 통해 확산) 대신 명명 된 응용 프로그램 인스턴스 내에서 hello 서비스가 실행 되는 노드 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="6f1e3-110">정의 용량 hello 명명 된 응용 프로그램 인스턴스 자체에 toolimit hello 수가 내부 hello 서비스의 서비스 또는 전체 리소스 소비량</span><span class="sxs-lookup"><span data-stu-id="6f1e3-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="6f1e3-111">toomeet 이러한 요구 사항을 hello 서비스 패브릭 클러스터 리소스 관리자는 응용 프로그램 그룹 이라는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="6f1e3-112">Hello 최대 노드 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="6f1e3-113">응용 프로그램 용량에 대 한 가장 간단한 사용 사례 hello 때 응용 프로그램 인스턴스에 필요한 toobe tooa 특정 최대 노드 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="6f1e3-114">이를 통해 해당 응용 프로그램 인스턴스 내의 모든 서비스가 설정된 수의 컴퓨터에 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="6f1e3-115">통합은 toopredict 하려는 또는 hello 서비스 해당 응용 프로그램 명명 된 인스턴스 내에서 물리적 리소스 사용을 방지 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="6f1e3-116">hello 다음 이미지 표시와 정의 노드의 최대 수 없는 응용 프로그램 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="6f1e3-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="6f1e3-117"><center>
![최대 노드 수를 정의하는 응용 프로그램 인스턴스][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="6f1e3-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="6f1e3-118">Hello 왼쪽 예에서 hello 응용 프로그램 정의 노드의 최대 수 없는 경우 인데 % 세 가지 서비스.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="6f1e3-119">hello 클러스터 리소스 관리자가 분산 되어 모든 복제본 6 개의 사용 가능한 노드 tooachieve hello 적절 한 hello 클러스터 (hello 기본 동작).</span><span class="sxs-lookup"><span data-stu-id="6f1e3-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="6f1e3-120">Hello hello 오른쪽 예제에 표시 제한 된 toothree 노드가 동일한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="6f1e3-121">이 동작을 제어 하는 hello 매개 변수 MaximumNodes 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="6f1e3-122">이 매개 변수는 응용 프로그램을 만드는 동안 설정되거나 이미 실행 중인 응용 프로그램 인스턴스에 대해 업데이트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="6f1e3-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f1e3-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="6f1e3-124">C#</span><span class="sxs-lookup"><span data-stu-id="6f1e3-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="6f1e3-125">노드의 hello 집합 내에서 서비스 개체를 함께 배치 하거나 노드를 사용 하는 클러스터 리소스 관리자 hello 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="6f1e3-126">응용 프로그램 메트릭, 부하 및 용량</span><span class="sxs-lookup"><span data-stu-id="6f1e3-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="6f1e3-127">응용 프로그램 그룹을 특정된 명명 된 응용 프로그램 인스턴스 및 이러한 메트릭에 대 한 해당 응용 프로그램 인스턴스의 용량와 관련 된 toodefine 메트릭을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="6f1e3-128">응용 프로그램 메트릭 tootrack, 예약 및 해당 응용 프로그램 인스턴스 내 hello 서비스의 제한 hello 리소스 사용을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="6f1e3-129">각 응용 프로그램 메트릭에서 두 개의 값을 다음과 같이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="6f1e3-130">**전체 응용 프로그램 용량** –이 설정은 특정 메트릭에 대 한 hello 응용 프로그램의 총 용량 hello를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="6f1e3-131">클러스터 리소스 관리자 hello hello 생성을 해야 하는 총 부하 tooexceed이이 값이 응용 프로그램 인스턴스 내에서 새로운 서비스의 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="6f1e3-132">예를 들어 hello 응용 프로그램 인스턴스가 10의 용량 치인 이미 5 개의 부하 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="6f1e3-133">10의 총 기본 부하로 서비스의 hello 만들기가 허용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="6f1e3-134">**최대 노드 용량** –이 설정은 단일 노드에서 hello hello 응용 프로그램에 대 한 최대 총 부하를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="6f1e3-135">이 용량을 통해 로드 되 면 클러스터 리소스 관리자 hello hello 부하가 감소 있도록 복제본 tooother 노드를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="6f1e3-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="6f1e3-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="6f1e3-137">C#:</span><span class="sxs-lookup"><span data-stu-id="6f1e3-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="6f1e3-138">용량 예약</span><span class="sxs-lookup"><span data-stu-id="6f1e3-138">Reserving Capacity</span></span>
<span data-ttu-id="6f1e3-139">응용 프로그램 그룹에 대 한 또 다른 일반적인 용도 tooensure 내의 리소스 클러스터 hello는 특정된 응용 프로그램 인스턴스에 대해 예약 된입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="6f1e3-140">hello 공간 hello 응용 프로그램 인스턴스를 만들 때 항상 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="6f1e3-141">경우에 hello 응용 프로그램을 즉시 전파에 대 한 hello 클러스터에는 공간을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="6f1e3-142">hello 응용 프로그램 인스턴스는 만들어지지만 그 안에 서비스가 아직 없습니다</span><span class="sxs-lookup"><span data-stu-id="6f1e3-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="6f1e3-143">hello 응용 프로그램 인스턴스 내에서 서비스의 hello 번호가 변경 될 때마다</span><span class="sxs-lookup"><span data-stu-id="6f1e3-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="6f1e3-144">hello 서비스 존재 하지만 hello 리소스 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="6f1e3-145">응용 프로그램 인스턴스에 대해 리소스를 예약하려면 2개의 추가 매개 변수 *MinimumNodes* 및 *NodeReservationCapacity*를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="6f1e3-146">**MinimumNodes** -hello 최소 수를 정의 hello 응용 프로그램 노드의 인스턴스에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="6f1e3-147">**NodeReservationCapacity** -이 설정은 hello 응용 프로그램에 대 한 메트릭을 별로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="6f1e3-148">hello 값이 있는 hello 실행 해당 응용 프로그램의 서비스는 모든 노드에 hello 응용 프로그램에 대 한 예약 된 해당 메트릭이 hello 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="6f1e3-149">결합 **MinimumNodes** 및 **NodeReservationCapacity** hello 클러스터 내에서 hello 응용 프로그램에 대 한 최소 부하 예약을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="6f1e3-150">Hello에 대 한 용량 보다 필요한 hello 총 예약 클러스터을 적게 남은 선택한 경우 hello 응용 프로그램을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="6f1e3-151">용량 예약의 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="6f1e3-152"><center>
![예약된 용량을 정의하는 응용 프로그램 인스턴스][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="6f1e3-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="6f1e3-153">Hello 왼쪽 예제에서 응용 프로그램 정의 하는 응용 프로그램 기능이 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="6f1e3-154">클러스터 리소스 관리자 hello toonormal 규칙에 따라 모든 균형을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="6f1e3-155">Hello 오른쪽에 hello 예에서 응용 프로그램 1 설정을 다음 hello로 만들어 졌 음 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="6f1e3-156">MinimumNodes tootwo 설정</span><span class="sxs-lookup"><span data-stu-id="6f1e3-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="6f1e3-157">다음으로 정의된 응용 프로그램 메트릭</span><span class="sxs-lookup"><span data-stu-id="6f1e3-157">An application Metric defined with</span></span>
  - <span data-ttu-id="6f1e3-158">20인 NodeReservationCapacity</span><span class="sxs-lookup"><span data-stu-id="6f1e3-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="6f1e3-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f1e3-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="6f1e3-160">C#</span><span class="sxs-lookup"><span data-stu-id="6f1e3-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="6f1e3-161">서비스 패브릭 응용 프로그램 1에 대 한 두 개의 노드가에서 용량을 예약 하 고 서비스 응용 프로그램 2 tooconsume에서 부하가 hello 시 응용 프로그램 1 내 hello 서비스에서 사용 되는 경우에 이러한 능력을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="6f1e3-162">이 예약 된 응용 프로그램 용량 사용 하 고 용량 및 hello 클러스터 내에서 해당 노드에 남아 있는 hello에 반해 서 집계 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="6f1e3-163">즉시 클러스터 용량 남은 hello에서 하 게 차감 된 hello 예약, hello 예약 되어 있지만 소비 하 게 차감 된 특정 노드의 hello 용량에서 하나 이상의 서비스에 개체 갖추어야 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="6f1e3-164">이후 예약을 사용하면 리소스가 노드에서 필요할 때만 예약되므로 유연성과 리소스 사용률을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="6f1e3-165">Hello 응용 프로그램 부하 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="6f1e3-165">Obtaining hello application load information</span></span>
<span data-ttu-id="6f1e3-166">메트릭을 하나 이상에 대해 정의 된 응용 프로그램 용량이 있는 각 응용 프로그램에 대 한 서비스 복제본에서 보고 하는 hello 집계 부하에 대 한 hello 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="6f1e3-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="6f1e3-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="6f1e3-168">C#</span><span class="sxs-lookup"><span data-stu-id="6f1e3-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="6f1e3-169">hello ApplicationLoad 쿼리 hello hello 응용 프로그램에 대해 지정 된 응용 프로그램 성능에 대 한 기본 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="6f1e3-170">이 정보는 hello 노드 최소 및 최대 노드 정보 및 hello 응용 프로그램 현재 차지 하는 hello 번호 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="6f1e3-171">다음을 비롯한 각 응용 프로그램 부하 메트릭에 대한 정보도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="6f1e3-172">Hello 메트릭의 메트릭 이름: 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="6f1e3-173">예약 용량:이 응용 프로그램에 대 한 hello 클러스터에서 예약 된 용량을 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="6f1e3-174">응용 프로그램 부하: 이 응용 프로그램 자식 복제본의 총 부하.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="6f1e3-175">응용 프로그램 용량: 응용 프로그램 부하의 허용되는 최대값.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="6f1e3-176">응용 프로그램 용량 삭제</span><span class="sxs-lookup"><span data-stu-id="6f1e3-176">Removing Application Capacity</span></span>
<span data-ttu-id="6f1e3-177">응용 프로그램에 대 한 hello 응용 프로그램 용량 매개 변수 설정 되 면 제거할 수도 업데이트 응용 프로그램 Api 또는 PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="6f1e3-178">예:</span><span class="sxs-lookup"><span data-stu-id="6f1e3-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="6f1e3-179">이 명령은 hello 응용 프로그램 인스턴스에서 모든 응용 프로그램 용량 관리 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="6f1e3-180">있는 경우 MinimumNodes, MaximumNodes, 및 hello 응용 프로그램의 메트릭을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="6f1e3-181">즉시 hello hello 명령의 영향을 주지가 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="6f1e3-182">이 명령이 완료 되 면 후 hello 클러스터 리소스 관리자 hello 기본 동작을 사용 하 여 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="6f1e3-183">`Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`을 통해 응용 프로그램 용량 매개 변수를 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="6f1e3-184">응용 프로그램 용량에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="6f1e3-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="6f1e3-185">고려해야 할 응용 프로그램 용량 매개 변수에 대한 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="6f1e3-186">유효성 검사 오류가 있는 경우 아무 것도 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="6f1e3-187">모든 정수 매개 변수는 음수가 아닌 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="6f1e3-188">MinimumNodes는 MaximumNodes보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="6f1e3-189">부하 메트릭의 용량을 정의한 경우 다음 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="6f1e3-190">노드 예약 용량은 최대 노드 용량보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="6f1e3-191">예를 들어 hello 메트릭에 "CPU" hello 노드 tootwo 단위에 대 한 hello 용량 제한 수 없으며 각 노드에서 tooreserve 세 단위를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="6f1e3-192">MaximumNodes를 지정 하는 경우 다음 MaximumNodes 및 최대 노드 용량 hello 제품 하지 보다 커야 합니다 응용 프로그램의 총 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="6f1e3-193">예를 들어 hello 부하 메트릭 "CPU" tooeight 설정에 대 한 최대 노드 용량 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="6f1e3-194">또한 경우를 가정해 최대 노드 too10 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="6f1e3-195">이 경우 이 부하 메트릭에 대해 응용 프로그램 총 용량은 80보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="6f1e3-196">응용 프로그램을 만들고 업데이트 하는 동안 둘 다 hello 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="6f1e3-197">방법 toouse 응용 프로그램 용량 하지</span><span class="sxs-lookup"><span data-stu-id="6f1e3-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="6f1e3-198">Toouse hello 응용 프로그램 그룹 기능 tooconstrain hello 응용 프로그램 tooa 마십시오 _특정_ 노드의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="6f1e3-199">즉, 지정할 수 있습니다에서 최대 5 개의 노드가 hello 응용 프로그램을 실행 하지만 hello 클러스터의 특정 5 노드 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="6f1e3-200">응용 프로그램 toospecific 제한 노드 가능 배치 제약 조건을 사용 하 여 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="6f1e3-201">두 서비스에서 동일한 응용 프로그램에 대 한 사항은 hello hello 같은 노드는 toouse hello 응용 프로그램 용량 tooensure를 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="6f1e3-202">대신 [선호도](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) 또는 [배치 제약 조건](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f1e3-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f1e3-203">Next steps</span></span>
- <span data-ttu-id="6f1e3-204">서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="6f1e3-205">toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="6f1e3-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="6f1e3-206">Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6f1e3-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="6f1e3-207">메트릭이 일반적으로 작동하는 방식에 대한 자세한 내용은 [서비스 패브릭 부하 메트릭](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="6f1e3-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="6f1e3-208">클러스터 리소스 관리자 hello에 hello 클러스터를 설명 하는 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f1e3-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="6f1e3-209">toofind에 대 한 자세한 내용을 확인해이 문서에 [서비스 패브릭 클러스터를 설명 하는](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="6f1e3-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
