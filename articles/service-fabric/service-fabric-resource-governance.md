---
title: "컨테이너 및 서비스에 대 한 서비스 패브릭 리소스 관리 aaaAzure | Microsoft Docs"
description: "Azure 서비스 패브릭 서비스 내부 또는 외부 컨테이너 실행에 대 한 리소스 제한을 toospecify 있습니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="bf647-103">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="bf647-103">Resource governance</span></span> 

<span data-ttu-id="bf647-104">여러 서비스에서 실행 되는 동일한 노드 또는 클러스터 hello 때 불가능 한 서비스가 다른 서비스 함으로써 더 많은 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="bf647-105">이 문제는 참조 된 tooas hello 시끄러운 이웃 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="bf647-106">서비스 패브릭 hello 개발자 toospecify 예약 및 제한을 서비스 tooguarantee 리소스 당 있으며 또한 해당 리소스 사용을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="bf647-107">리소스 관리 메트릭</span><span class="sxs-lookup"><span data-stu-id="bf647-107">Resource governance metrics</span></span> 

<span data-ttu-id="bf647-108">리소스 관리는 Service Fabric에서 [서비스 패키지](service-fabric-application-model.md)별로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="bf647-109">hello 리소스 tooService 패키지에 할당 된 코드 패키지 간에 세분화 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="bf647-110">지정 된 hello 리소스 제한이 hello 리소스의 hello 예약을 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="bf647-111">Service Fabric은 두 개의 기본 제공 [메트릭](service-fabric-cluster-resource-manager-metrics.md)을 사용하여 서비스 패키지당 CPU 및 메모리 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="bf647-112">CPU (메트릭 이름을 `ServiceFabric:/_CpuCores`): 코어는 논리 코어 hello 호스트 컴퓨터에 제공 되 고 모든 노드에 걸쳐 모든 코어 가중치를 적용 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="bf647-113">메모리 (메트릭 이름을 `ServiceFabric:/_MemoryInMB`): 메모리는 메가바이트 단위로 및 hello 컴퓨터에서 사용할 수 있는 toophysical 메모리를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="bf647-114">만 제공 hello 런타임 거부 패키지 사용 가능한 리소스를 초과 하는 새 서비스를 열기-소프트 예약 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="bf647-115">그러나 다른 실행 파일 또는 컨테이너는 hello 노드에 배치 되 면 hello 원래 예약이 보장을 위반할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="bf647-116">이러한 두 메트릭에 대 한 hello [클러스터 리소스 관리자](service-fabric-cluster-resource-manager-cluster-description.md) 총 클러스터 용량을 hello 클러스터의 각 노드에 대 한 hello 부하를 추적 하 고 남은 hello 클러스터의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="bf647-117">이러한 두 메트릭을 해당 tooany는 다른 사용자 또는 사용자 지정 메트릭 및 기존의 모든 기능을 함께 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="bf647-118">클러스터 수 [분산](service-fabric-cluster-resource-manager-balancing.md) toothese 두 메트릭 (기본 동작)에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="bf647-119">클러스터 수 [조각 모음](service-fabric-cluster-resource-manager-defragmentation-metrics.md) toothese 두 메트릭에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="bf647-120">[클러스터를 설명](service-fabric-cluster-resource-manager-cluster-description.md)할 때 두 메트릭에 대해 버퍼링된 용량을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="bf647-121">두 메트릭에 대한 [동적 부하 보고](service-fabric-cluster-resource-manager-metrics.md)는 지원되지 않으며 해당 메트릭에 대한 부하는 생성 시 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="bf647-122">리소스 관리를 사용하기 위한 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="bf647-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="bf647-123">용량에에서 정의 되어야 합니다 수동으로 hello 클러스터의 각 노드 유형에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="bf647-124">리소스 관리는 사용자 서비스에서만 허용되고 시스템 서비스에서는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="bf647-125">용량을 지정할 때 일부 코어와 메모리는 시스템 서비스에 할당되지 않은 상태로 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="bf647-126">최적의 성능을 위해서는 hello 설정을 다음도 설정 해야 클러스터 매니페스트에 hello:</span><span class="sxs-lookup"><span data-stu-id="bf647-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="bf647-127">리소스 관리 지정</span><span class="sxs-lookup"><span data-stu-id="bf647-127">Specifying resource governance</span></span> 

<span data-ttu-id="bf647-128">다음 예제는 hello와 같이 리소스 거 버 넌 스 제한 hello 응용 프로그램 매니페스트 (ServiceManifestImport 섹션)에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="bf647-129">이 예제에서는 서비스 패키지 ServicePackageA 위치로 hello 노드에서 코어가 두 개를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="bf647-130">이 서비스 패키지 (CodeA1 및 CodeA2), 두 개의 코드 패키지를 포함 하 고 둘 다 지정 hello `CpuShares` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="bf647-131">hello 비율로 CpuShares 512:256 hello 두 코드 패키지에 대해 hello 코어를 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="bf647-132">따라서이 예제에서는 CodeA1은 코어의 2-3 및 CodeA2 코어의 1/3을 가져옵니다 (가져오고의 보증 소프트 예약 hello 동일).</span><span class="sxs-lookup"><span data-stu-id="bf647-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="bf647-133">경우 CpuShares 코드 패키지에 대 한 지정 하지 않으면 서비스 패브릭 hello 코어 간에 균등 하 게 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="bf647-134">메모리 한도 코드 패키지를 모두 제한 too1024 않으므로 절대 MB의 메모리만 (및 동일 hello의 보증 소프트 예약).</span><span class="sxs-lookup"><span data-stu-id="bf647-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="bf647-135">코드 패키지 (컨테이너 또는 프로세스) toodo 시점과이 제한 보다 더 많은 메모리는 메모리 부족 예외가 발생 하는 수 tooallocate 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="bf647-136">리소스 제한 적용 toowork 서비스 패키지 내의 모든 코드 패키지에 지정 된 메모리 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf647-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf647-137">Next steps</span></span>
* <span data-ttu-id="bf647-138">toolearn 더에 대 한 클러스터 리소스 관리자에서이 내용을 읽고 [문서](service-fabric-cluster-resource-manager-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="bf647-139">응용 프로그램 모델, 서비스 패키지, 코드 패키지 및 복제본 toothem 매핑하 하는 방법에 대해 자세히 toolearn이 내용을 읽고 [문서](service-fabric-application-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf647-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
