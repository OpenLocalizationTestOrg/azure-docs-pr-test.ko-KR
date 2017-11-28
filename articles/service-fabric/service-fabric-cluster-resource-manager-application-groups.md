---
title: "Service Fabric 클러스터 리소스 관리자 - 응용 프로그램 그룹 | Microsoft Docs"
description: "서비스 패브릭 클러스터 리소스 관리자에서 응용 프로그램 그룹 기능 개요"
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
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="0cfac-103">응용 프로그램 그룹 소개</span><span class="sxs-lookup"><span data-stu-id="0cfac-103">Introduction to Application Groups</span></span>
<span data-ttu-id="0cfac-104">Service Fabric의 Cluster Resource Manager는 일반적으로 부하([메트릭](service-fabric-cluster-resource-manager-metrics.md)을 통해 표시됨)를 클러스터 전체에 균등하게 분산하여 클러스터 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="0cfac-105">Service Fabric은 클러스터에서 노드의 용량과 [용량](service-fabric-cluster-resource-manager-cluster-description.md)을 통해 전체적으로 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="0cfac-106">메트릭과 용량은 다양한 워크로드에 잘 적용되지만 서로 다른 Service Fabric 응용 프로그램 인스턴스를 과도하게 사용하는 패턴은 때때로 추가 요구 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="0cfac-107">예를 들어 다음을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-107">For example you may want to:</span></span>

- <span data-ttu-id="0cfac-108">일부 명명된 응용 프로그램 인스턴스 내에서 클러스터에 있는 노드에 대한 일부 용량을 서비스용으로 예약</span><span class="sxs-lookup"><span data-stu-id="0cfac-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="0cfac-109">명명된 응용 프로그램 인스턴스 내의 서비스가 실행되는 노드의 총 수 제한(전체 클러스터에 분산하지 않음)</span><span class="sxs-lookup"><span data-stu-id="0cfac-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="0cfac-110">내부 서비스의 수 또는 서비스의 전체 리소스 소비량을 제한하기 위해 명명된 응용 프로그램 인스턴스 자체에서 용량 정의</span><span class="sxs-lookup"><span data-stu-id="0cfac-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="0cfac-111">이러한 요구 사항을 충족하기 위해 Service Fabric Cluster Resource Manager는 응용 프로그램 그룹이라는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="0cfac-112">노드의 최대 수 제한</span><span class="sxs-lookup"><span data-stu-id="0cfac-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="0cfac-113">응용 프로그램 용량에 대한 가장 간단한 사용 사례는 응용 프로그램 인스턴스를 특정 최대 노드 수로 제한해야 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="0cfac-114">이를 통해 해당 응용 프로그램 인스턴스 내의 모든 서비스가 설정된 수의 컴퓨터에 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="0cfac-115">명명된 해당 응용 프로그램 인스턴스 내에서 서비스의 실제 리소스 사용을 예측하거나 방지하려는 경우 통합 방식이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="0cfac-116">다음 이미지에서는 최대 노드 수가 정의되거나 정의되지 않은 응용 프로그램 인스턴스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="0cfac-117"><center>
![최대 노드 수를 정의하는 응용 프로그램 인스턴스][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="0cfac-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="0cfac-118">왼쪽 예제에서 응용 프로그램에는 정의된 최대 노드 수가 없으며 세 가지 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="0cfac-119">Cluster Resource Manager는 클러스터에서 최상의 균형을 달성하기 위해 6개의 사용 가능한 노드에 모든 복제본을 분산했습니다(기본 동작).</span><span class="sxs-lookup"><span data-stu-id="0cfac-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="0cfac-120">오른쪽 예제에서는 동일한 응용 프로그램이 3개의 노드로 제한된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="0cfac-121">이 동작을 제어하는 매개 변수를 MaximumNodes라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="0cfac-122">이 매개 변수는 응용 프로그램을 만드는 동안 설정되거나 이미 실행 중인 응용 프로그램 인스턴스에 대해 업데이트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="0cfac-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cfac-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="0cfac-124">C#</span><span class="sxs-lookup"><span data-stu-id="0cfac-124">C#</span></span>

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

<span data-ttu-id="0cfac-125">노드 집합 내에서 Cluster Resource Manager는 함께 배치되는 서비스 개체 또는 사용되는 노드를 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="0cfac-126">응용 프로그램 메트릭, 부하 및 용량</span><span class="sxs-lookup"><span data-stu-id="0cfac-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="0cfac-127">응용 프로그램 그룹을 사용하면 지정된 명명된 응용 프로그램 인스턴스와 연결된 메트릭 및 이러한 메트릭에 대한 해당 응용 프로그램 인스턴스의 용량을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="0cfac-128">응용 프로그램 메트릭을 사용하여 해당 응용 프로그램 인스턴스 내에서 서비스의 리소스 사용을 추적하고 예약하며 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="0cfac-129">각 응용 프로그램 메트릭에서 두 개의 값을 다음과 같이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="0cfac-130">**총 응용 프로그램 용량** - 이 설정은 특정 메트릭에 대한 응용 프로그램의 총 용량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="0cfac-131">Cluster Resource Manager를 사용하면 이 값을 초과하는 총 부하를 발생시키는 이 응용 프로그램 인스턴스 내에서 새 서비스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="0cfac-132">예를 들어, 응용 프로그램 인스턴스에 10이라는 용량이 있었고 이미 5라는 부하가 있다고 가정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="0cfac-133">10이라는 기본 총 부하를 가진 서비스를 만들도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="0cfac-134">**노드 최대 용량** – 이 설정은 단일 노드의 응용 프로그램에 대한 최대 총 부하를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="0cfac-135">부하가 이 용량을 초과하면 Cluster Resource Manager는 부하가 감소되도록 복제본을 다른 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="0cfac-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="0cfac-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="0cfac-137">C#:</span><span class="sxs-lookup"><span data-stu-id="0cfac-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="0cfac-138">용량 예약</span><span class="sxs-lookup"><span data-stu-id="0cfac-138">Reserving Capacity</span></span>
<span data-ttu-id="0cfac-139">응용 프로그램 그룹의 또 다른 일반적인 용도는 클러스터 내의 리소스가 지정된 응용 프로그램 인스턴스에 대해 예약되었는지 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="0cfac-140">응용 프로그램 인스턴스를 만들 때 해당 공간이 항상 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="0cfac-141">클러스터의 응용 프로그램 공간 예약은 다음과 같은 경우에도 즉시 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="0cfac-142">응용 프로그램 인스턴스가 만들어지지만 그 안에 서비스가 아직 없는 경우</span><span class="sxs-lookup"><span data-stu-id="0cfac-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="0cfac-143">응용 프로그램 인스턴스 내의 서비스 수가 매번 변경되는 경우</span><span class="sxs-lookup"><span data-stu-id="0cfac-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="0cfac-144">서비스가 존재하지만 리소스를 사용하지 않고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="0cfac-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="0cfac-145">응용 프로그램 인스턴스에 대해 리소스를 예약하려면 2개의 추가 매개 변수 *MinimumNodes* 및 *NodeReservationCapacity*를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="0cfac-146">**MinimumNodes** - 응용 프로그램 인스턴스를 실행해야 하는 노드의 최소 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="0cfac-147">**NodeReservationCapacity** - 이 설정은 응용 프로그램에 대한 메트릭을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="0cfac-148">해당 값은 해당 응용 프로그램의 서비스가 실행되는 모든 노드에서 응용 프로그램용으로 예약된 메트릭 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="0cfac-149">**MinimumNodes** 및 **NodeReservationCapacity**를 함께 사용하면 클러스터 내에서 응용 프로그램에 대한 최소 부하 예약이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="0cfac-150">필요한 총 예약 크기보다 더 적은 양의 용량이 클러스터에 남아 있는 경우 응용 프로그램을 만들지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="0cfac-151">용량 예약의 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="0cfac-152"><center>
![예약된 용량을 정의하는 응용 프로그램 인스턴스][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="0cfac-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="0cfac-153">왼쪽 예에서 응용 프로그램은 정의된 응용 프로그램 용량이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="0cfac-154">Cluster Resource Manager는 기본 규칙에 따라 모든 항목의 균형을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="0cfac-155">오른쪽의 예제에서는 Application1을 다음 설정으로 만들었다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="0cfac-156">MinimumNodes 2로 설정</span><span class="sxs-lookup"><span data-stu-id="0cfac-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="0cfac-157">다음으로 정의된 응용 프로그램 메트릭</span><span class="sxs-lookup"><span data-stu-id="0cfac-157">An application Metric defined with</span></span>
  - <span data-ttu-id="0cfac-158">20인 NodeReservationCapacity</span><span class="sxs-lookup"><span data-stu-id="0cfac-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="0cfac-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cfac-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="0cfac-160">C#</span><span class="sxs-lookup"><span data-stu-id="0cfac-160">C#</span></span>

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

<span data-ttu-id="0cfac-161">Service Fabric은 2개의 노드에 Application1용으로 용량을 예약하고, 해당 시점에 Application1 내의 서비스에서 소비하는 부하가 없더라도 Application2의 서비스가 해당 용량을 소비하도록 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="0cfac-162">이 예약된 응용 프로그램 용량은 해당 노드 및 클러스터 내에서 남은 용량으로 소비되고 계산될 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="0cfac-163">예약된 용량은 나머지 클러스터 용량에서 즉시 차감되지만, 하나 이상의 서비스 개체가 배치된 경우에만 특정 노드의 용량에서 예약된 소비량이 차감됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="0cfac-164">이후 예약을 사용하면 리소스가 노드에서 필요할 때만 예약되므로 유연성과 리소스 사용률을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="0cfac-165">응용 프로그램 부하 정보 얻기</span><span class="sxs-lookup"><span data-stu-id="0cfac-165">Obtaining the application load information</span></span>
<span data-ttu-id="0cfac-166">하나 이상의 메트릭에 대해 정의된 응용 프로그램 용량이 정의된 각 응용 프로그램의 경우 해당 서비스의 복제본에서 보고된 집계 부하에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="0cfac-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="0cfac-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="0cfac-168">C#</span><span class="sxs-lookup"><span data-stu-id="0cfac-168">C#</span></span>

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

<span data-ttu-id="0cfac-169">ApplicationLoad 쿼리는 응용 프로그램에 대해 지정된 응용 프로그램 성능에 대한 기본 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="0cfac-170">이 정보에는 최소 노드와 최대 노드 정보 및 응용 프로그램이 현재 사용하고 있는 노드 수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="0cfac-171">다음을 비롯한 각 응용 프로그램 부하 메트릭에 대한 정보도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="0cfac-172">메트릭 이름: 메트릭의 이름.</span><span class="sxs-lookup"><span data-stu-id="0cfac-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="0cfac-173">예약 용량: 이 응용 프로그램에 대한 클러스터에 예약된 클러스터 용량.</span><span class="sxs-lookup"><span data-stu-id="0cfac-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="0cfac-174">응용 프로그램 부하: 이 응용 프로그램 자식 복제본의 총 부하.</span><span class="sxs-lookup"><span data-stu-id="0cfac-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="0cfac-175">응용 프로그램 용량: 응용 프로그램 부하의 허용되는 최대값.</span><span class="sxs-lookup"><span data-stu-id="0cfac-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="0cfac-176">응용 프로그램 용량 삭제</span><span class="sxs-lookup"><span data-stu-id="0cfac-176">Removing Application Capacity</span></span>
<span data-ttu-id="0cfac-177">응용 프로그램 용량 매개 변수가 응용 프로그램에 대해 설정되면 업데이트 응용 프로그램 API 또는 PowerShell cmdlet을 사용하여 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="0cfac-178">예:</span><span class="sxs-lookup"><span data-stu-id="0cfac-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="0cfac-179">이 명령은 응용 프로그램 인스턴스에서 모든 응용 프로그램 용량 관리 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="0cfac-180">여기에는 MinimumNodes, MaximumNodes 및 응용 프로그램의 메트릭(있는 경우)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="0cfac-181">명령은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-181">The effect of the command is immediate.</span></span> <span data-ttu-id="0cfac-182">이 명령이 완료되면 Cluster Resource Manager는 응용 프로그램을 관리하는 기본 동작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="0cfac-183">`Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`을 통해 응용 프로그램 용량 매개 변수를 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="0cfac-184">응용 프로그램 용량에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="0cfac-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="0cfac-185">고려해야 할 응용 프로그램 용량 매개 변수에 대한 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="0cfac-186">유효성 검사 오류가 있는 경우 아무 것도 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="0cfac-187">모든 정수 매개 변수는 음수가 아닌 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="0cfac-188">MinimumNodes는 MaximumNodes보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="0cfac-189">부하 메트릭의 용량을 정의한 경우 다음 규칙을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="0cfac-190">노드 예약 용량은 최대 노드 용량보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="0cfac-191">예를 들어, 노드의 메트릭 "CPU"의 용량을 2단위로 제한하고 각 노드에 3단위를 예약하려고 시도할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="0cfac-192">MaximumNodes를 지정하는 경우 MaximumNodes의 제품 및 최대 노드 용량은 총 응용 프로그램 용량보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="0cfac-193">예를 들어, 부하 메트릭 "CPU"의 최대 노드 용량을 8로 설정했다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="0cfac-194">또한 최대 노드를 10으로 설정했다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="0cfac-195">이 경우 이 부하 메트릭에 대해 응용 프로그램 총 용량은 80보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="0cfac-196">응용 프로그램 생성 및 업데이트 동안 이러한 제한이 둘 다 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="0cfac-197">응용 프로그램 용량을 사용하지 않는 방법</span><span class="sxs-lookup"><span data-stu-id="0cfac-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="0cfac-198">응용 프로그램 그룹 기능을 사용하여 응용 프로그램을 노드의 _특정_ 하위 집합으로 제한하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="0cfac-199">즉, 응용 프로그램을 최대 다섯 개의 노드에서 실행하도록 지정할 수 있지만 클러스터에서 어떤 특정 다섯 개의 노드인지 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="0cfac-200">서비스에 대한 배치 제약 조건을 사용하여 응용 프로그램 특정 노드로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="0cfac-201">동일한 응용 프로그램의 두 서비스가 같은 노드에 배치될 수 있도록 응용 프로그램 용량을 사용하려고 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="0cfac-202">대신 [선호도](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) 또는 [배치 제약 조건](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cfac-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cfac-203">Next steps</span></span>
- <span data-ttu-id="0cfac-204">서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="0cfac-205">클러스터 Resource Manager가 클러스터의 부하를 관리하고 분산하는 방법을 알아보려면 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="0cfac-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="0cfac-206">처음부터 시작 및 [서비스 패브릭 클러스터 리소스 관리자 소개](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0cfac-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="0cfac-207">메트릭이 일반적으로 작동하는 방식에 대한 자세한 내용은 [서비스 패브릭 부하 메트릭](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="0cfac-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="0cfac-208">Cluster Resource Manager에는 클러스터를 설명하기 위한 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfac-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="0cfac-209">이에 대해 자세히 알아보려면 [Service Fabric 클러스터 설명](service-fabric-cluster-resource-manager-cluster-description.md)에 대한 문서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfac-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
