---
title: "Service Fabric 클러스터 리소스 관리자 - 배치 정책 | Microsoft Docs"
description: "서비스 패브릭 서비스에 대한 추가 배치 정책 및 규칙 개요"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 6c11d49d5fdb3148b0534c9448f815358fa8cab3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="469bf-103">서비스 패브릭 서비스에 대한 배치 정책</span><span class="sxs-lookup"><span data-stu-id="469bf-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="469bf-104">배치 정책은 보다 덜 일반적인 일부 구체적인 시나리오에서 서비스 배치를 제어하는 데 사용할 수 있는 추가적인 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-104">Placement policies are additional rules that can be used to govern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="469bf-105">이러한 시나리오의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="469bf-106">온-프레미스 데이터 센터 또는 Azure 지역 간에 Service Fabric 클러스터의 지리적 거리가 확대되는 경우</span><span class="sxs-lookup"><span data-stu-id="469bf-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="469bf-107">사용자 환경이 지정학적 또는 법적 통제 또는 정책적 경계를 적용해야 하는 여러 영역에 확대되는 경우</span><span class="sxs-lookup"><span data-stu-id="469bf-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need to enforce</span></span>
- <span data-ttu-id="469bf-108">먼 거리 또는 보다 느리거나 덜 안정적인 네트워크 링크의 사용으로 인해 통신 성능 또는 대기 시간을 고려해야 할 경우</span><span class="sxs-lookup"><span data-stu-id="469bf-108">There are communication performance or latency considerations due to large distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="469bf-109">특정 워크로드를 다른 워크로드와 함께 배치하거나 고객과 가까이에 배치해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-109">You need to keep certain workloads collocated as a best effort, either with other workloads or in proximity to customers</span></span>

<span data-ttu-id="469bf-110">이러한 요구 사항 대부분은 클러스터의 장애 도메인으로 표시되는 클러스터의 실제 레이아웃과 맞춰 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-110">Most of these requirements align with the physical layout of the cluster, represented as the fault domains of the cluster.</span></span> 

<span data-ttu-id="469bf-111">이러한 시나리오를 해결하는 데 도움이 되는 고급 배치 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-111">The advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="469bf-112">잘못된 도메인</span><span class="sxs-lookup"><span data-stu-id="469bf-112">Invalid domains</span></span>
2. <span data-ttu-id="469bf-113">필수 도메인</span><span class="sxs-lookup"><span data-stu-id="469bf-113">Required domains</span></span>
3. <span data-ttu-id="469bf-114">기본 설정 도메인</span><span class="sxs-lookup"><span data-stu-id="469bf-114">Preferred domains</span></span>
4. <span data-ttu-id="469bf-115">복제본 압축 불가</span><span class="sxs-lookup"><span data-stu-id="469bf-115">Disallowing replica packing</span></span>

<span data-ttu-id="469bf-116">다음 컨트롤은 대부분 노드 속성 및 배치 제약 조건을 통해 구성할 수 있지만 일부는 더 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="469bf-117">Service Fabric Cluster Resource Manager는 좀 더 간단하게 이러한 추가 배치 정책을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="469bf-118">배치 정책은 명명된 서비스 인스턴스를 기준으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="469bf-119">동적으로 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="469bf-120">잘못된 도메인 지정</span><span class="sxs-lookup"><span data-stu-id="469bf-120">Specifying invalid domains</span></span>
<span data-ttu-id="469bf-121">**InvalidDomain** 배치 정책을 사용하여 특정 장애 도메인이 특정 서비스에 유효하지 않다고 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-121">The **InvalidDomain** placement policy allows you to specify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="469bf-122">이 정책을 사용하면 예를 들어 지정학적 또는 회사 정책상의 이유로 특정 영역에서 특정 서비스가 실행되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="469bf-123">별도 정책을 통해 잘못된 여러 도메인을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="469bf-124"><center>
![잘못된 도메인 예제][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="469bf-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="469bf-125">코드:</span><span class="sxs-lookup"><span data-stu-id="469bf-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="469bf-126">Powershell:</span><span class="sxs-lookup"><span data-stu-id="469bf-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="469bf-127">필수 도메인 지정</span><span class="sxs-lookup"><span data-stu-id="469bf-127">Specifying required domains</span></span>
<span data-ttu-id="469bf-128">필수 도메인 배치 정책 서비스에서는 해당 서비스가 지정된 도메인에만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-128">The required domain placement policy requires that the service is present only in the specified domain.</span></span> <span data-ttu-id="469bf-129">별도 정책을 통해 여러 필수 도메인을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="469bf-130"><center>
![필수 도메인 예제][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="469bf-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="469bf-131">코드:</span><span class="sxs-lookup"><span data-stu-id="469bf-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="469bf-132">Powershell:</span><span class="sxs-lookup"><span data-stu-id="469bf-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-the-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="469bf-133">상태 저장 서비스의 주 복제본에 대한 기본 설정 도메인 지정</span><span class="sxs-lookup"><span data-stu-id="469bf-133">Specifying a preferred domain for the primary replicas of a stateful service</span></span>
<span data-ttu-id="469bf-134">기본 설정 주 도메인은 주 복제본이 될 장애 도메인을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-134">The Preferred Primary Domain specifies the fault domain to place the Primary in.</span></span> <span data-ttu-id="469bf-135">정상 상태인 경우 주 복제본은 이 도메인에 위치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-135">The Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="469bf-136">도메인 또는 주 복제본에 오류가 발생하거나 종료되면 주 복제본은 일부 다른 위치(이상적으로는 동일한 도메인)로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-136">If the domain or the Primary replica fails or shuts down, the Primary moves to some other location, ideally in the same domain.</span></span> <span data-ttu-id="469bf-137">새 위치가 기본 설정 도메인이 아닌 경우 Cluster Resource Manager는 새 위치를 가능한 한 빨리 기본 도메인으로 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-137">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span></span> <span data-ttu-id="469bf-138">이 정책은 Azure 지역 또는 여러 데이터 센터 간에 걸쳐 있는 클러스터에서 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="469bf-139">이 정책은 Azure 지역 또는 여러 데이터 센터에 걸쳐 있으나 특정 위치에 배치되는 것을 선호하는 서비스를 포함하는 클러스터에서 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="469bf-140">주 복제본을 해당 사용자 또는 기타 서비스에 가깝게 배치하면 기본적으로 주 복제본이 처리하는 읽기 작업에서 특히 대기 시간을 낮추는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-140">Keeping Primaries close to their users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="469bf-141"><center>
![기본 설정 주 도메인 및 장애 조치(Failover)][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="469bf-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="469bf-142">Powershell:</span><span class="sxs-lookup"><span data-stu-id="469bf-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="469bf-143">복제본 배포 요구 및 압축 허용 안 함</span><span class="sxs-lookup"><span data-stu-id="469bf-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="469bf-144">복제본은 _일반적으로_ 클러스터가 정상 상태일 때 장애 및 업그레이드 도메인에 걸쳐 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-144">Replicas are _normally_ distributed across fault and upgrade domains when the cluster is healthy.</span></span> <span data-ttu-id="469bf-145">그러나 특정 파티션에 대해 둘 이상의 복제본이 단일 도메인으로 압축될 수 있는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="469bf-146">예를 들어, 클러스터에 3개의 장애 도메인(fd:/0, fd:/1 및 fd:/2)에 있는 9개의 노드가 있고</span><span class="sxs-lookup"><span data-stu-id="469bf-146">For example, let's say that the cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="469bf-147">서비스에 3개의 복제본이 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="469bf-148">fd:/1 및 fd:/2의 해당 복제본에 사용되는 노드가 중단되었다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-148">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="469bf-149">일반적으로 Cluster Resource Manager는 이러한 동일한 장애 도메인에서 다른 노드를 기본으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-149">Normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="469bf-150">이 경우에 용량 문제로 인해 해당 도메인의 다른 노드가 유효하지 않다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-150">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span></span> <span data-ttu-id="469bf-151">Cluster Resource Manager가 해당 복제본에 대한 대체 항목을 빌드하는 경우 fd:/0에서 노드를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-151">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span></span> <span data-ttu-id="469bf-152">그러나 _해당 작업_을 수행하면 장애 도메인 제약을 위반하는 상황이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-152">However, doing _that_ creates a situation where the Fault Domain constraint is violated.</span></span> <span data-ttu-id="469bf-153">복제본을 압축하면 전체 복제본 세트가 가동 중단되거나 손실될 가능성도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-153">Packing replicas increases the chance that the whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="469bf-154">제약 조건 및 제약 조건 우선 순위에 대한 자세한 내용은 [이 항목](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="469bf-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="469bf-155">`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`와 같은 상태 메시지가 표시된 경우 이 조건 또는 비슷한 조건에 도달한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-155">If you've ever seen a health message such as "`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="469bf-156">일반적으로 한 개나 두 개의 복제본만 일시적으로 함께 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="469bf-157">지정된 도메인에 쿼럼 미만의 복제본이 있는 경우 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="469bf-158">압축은 드물지만 발생할 수 있습니다. 그리고 노드가 다시 돌아오기 때문에 일반적으로 이러한 상황은 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-158">Packing is rare, but it can happen, and usually these situations are transient since the nodes come back.</span></span> <span data-ttu-id="469bf-159">노드가 중단되고 Cluster Resource Manager가 대체 노드를 빌드해야 하는 경우 일반적으로 이상적인 장애 도메인에서 사용할 수 있는 다른 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-159">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span></span>

<span data-ttu-id="469bf-160">일부 워크로드는 더 적은 도메인에 압축되는 경우에도 항상 목표 복제본 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-160">Some workloads would prefer always having the target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="469bf-161">이러한 워크로드는 동시에 발생하는 영구적인 도메인 오류 전체에 대해 안정적이며 일반적으로 로컬 상태를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="469bf-162">다른 워크로드는 위험 정확성 또는 데이터의 손실이 발생하기 전에 가동 중지 시간을 감수합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-162">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="469bf-163">대부분의 프로덕션 워크로드가 세 개 이상의 복제본, 세 개 이상의 장애 도메인 및 장애 도메인당 여러 개의 유효한 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="469bf-164">따라서 기본 동작은 기본적으로 도메인 압축을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-164">Because of this, the default behavior allows domain packing by default.</span></span> <span data-ttu-id="469bf-165">기본 동작은 일시적인 도메인 압축을 의미하더라도 정상적인 부하 분산 및 장애 조치(failover)를 통해 이러한 극단적인 경우를 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-165">The default behavior allows normal balancing and failover to handle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="469bf-166">지정된 워크로드에 대해 이러한 압축을 사용하지 않도록 설정하려면 서비스에서 `RequireDomainDistribution` 정책을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-166">If you want to disable such packing for a given workload, you can specify the `RequireDomainDistribution` policy on the service.</span></span> <span data-ttu-id="469bf-167">이 정책을 설정하면 Cluster Resource Manager를 통해 동일한 장애 도메인 또는 업그레이드 도메인에서 동일한 파티션의 두 복제본이 실행되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-167">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition run in the same fault or upgrade domain.</span></span>

<span data-ttu-id="469bf-168">코드:</span><span class="sxs-lookup"><span data-stu-id="469bf-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="469bf-169">Powershell:</span><span class="sxs-lookup"><span data-stu-id="469bf-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="469bf-170">현재 지리적으로 분산되지 않은 클러스터의 서비스에 대해 이러한 구성을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="469bf-170">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="469bf-171">가능하지만 그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="469bf-172">시나리오에서 꼭 필요한 경우가 아니면 유효하지 않은 필수 기본 도메인 구성은 피해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-172">The required, invalid, and preferred domain configurations should be avoided unless the scenarios require them.</span></span> <span data-ttu-id="469bf-173">지정된 워크로드를 단일 랙에서 실행하거나 다른 로컬 클러스터의 일부 세그먼트를 기본으로 사용하려는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-173">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span></span> <span data-ttu-id="469bf-174">여러 하드웨어 구성을 장애 도메인 간에 분산하고 일반 배치 제약 조건 및 노드 속성을 통해 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="469bf-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="469bf-175">Next steps</span></span>
- <span data-ttu-id="469bf-176">서비스 구성에 대한 자세한 내용은 [서비스 구성에 대한 자세한 정보](service-fabric-cluster-resource-manager-configure-services.md)에서 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="469bf-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
