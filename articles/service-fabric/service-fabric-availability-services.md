---
title: "서비스 패브릭 서비스의 aaaAvailability | Microsoft Docs"
description: "서비스에 대한 오류 검색, 장애 조치(Failover) 및 복구를 설명합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a><span data-ttu-id="895e3-103">서비스 패브릭 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="895e3-103">Availability of Service Fabric services</span></span>
<span data-ttu-id="895e3-104">이 문서에서는 Service Fabric이 서비스의 가용성을 유지하는 방법에 대한 개요를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-104">This article gives an overview of how Service Fabric maintains availability of a service.</span></span>

## <a name="availability-of-service-fabric-stateless-services"></a><span data-ttu-id="895e3-105">서비스 패브릭 상태 비저장 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="895e3-105">Availability of Service Fabric stateless services</span></span>
<span data-ttu-id="895e3-106">Azure 서비스 패브릭 서비스는 상태 저장 또는 상태 비저장이 모두 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-106">Azure Service Fabric services can be either stateful or stateless.</span></span> <span data-ttu-id="895e3-107">상태 비저장 서비스는 포함 하지 않는 응용 프로그램 서비스 [로컬 상태](service-fabric-concepts-state.md) 항상 사용할 수 있으며 신뢰할 수 있는 toobe 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-107">A stateless service is an application service that does not have any [local state](service-fabric-concepts-state.md) that needs toobe highly available or reliable.</span></span>

<span data-ttu-id="895e3-108">상태 비저장 서비스를 만들려면 `InstanceCount`를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-108">Creating a stateless service requires defining an `InstanceCount`.</span></span> <span data-ttu-id="895e3-109">hello 인스턴스 수는 hello hello 클러스터에서 실행 해야 하는 hello 상태 비저장 서비스의 응용 프로그램 논리의 인스턴스 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-109">hello instance count defines hello number of instances of hello stateless service's application logic that should be running in hello cluster.</span></span> <span data-ttu-id="895e3-110">Hello 인스턴스 수를 늘리면 hello 상태 비저장 서비스 확장 방법이 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-110">Increasing hello number of instances is hello recommended way of scaling out a stateless service.</span></span>

<span data-ttu-id="895e3-111">상태 비저장 서비스 명명 된 인스턴스의 실패 한 경우 hello 클러스터의 적격 일부 노드는 새 인스턴스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-111">When an instance of a stateless named service fails, a new instance is created on some eligible node in hello cluster.</span></span> <span data-ttu-id="895e3-112">예를 들어 상태 비저장 서비스 인스턴스는 Node1에서 실패하고 Node5에서 다시 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-112">For example, a stateless service instance might fail on Node1 and be recreated on Node5.</span></span>

## <a name="availability-of-service-fabric-stateful-services"></a><span data-ttu-id="895e3-113">서비스 패브릭 상태 저장 서비스의 가용성</span><span class="sxs-lookup"><span data-stu-id="895e3-113">Availability of Service Fabric stateful services</span></span>
<span data-ttu-id="895e3-114">상태 저장 서비스에는 이와 관련된 일부 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-114">A stateful service has some state associated with it.</span></span> <span data-ttu-id="895e3-115">서비스 패브릭에서 상태 저장 서비스는 복제본 세트로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-115">In Service Fabric, a stateful service is modeled as a set of replicas.</span></span> <span data-ttu-id="895e3-116">각 복제본은 해당 서비스에 대 한 hello 상태의 복사본에도 있는 hello 서비스의 hello 코드의 실행 중인 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-116">Each replica is a running instance of hello code of hello service that also has a copy of hello state for that service.</span></span> <span data-ttu-id="895e3-117">하나의 복제본 (주 hello 라고 함)에서 읽기 및 쓰기 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-117">Read and write operations are performed at one replica (called hello Primary).</span></span> <span data-ttu-id="895e3-118">쓰기 작업에서 변경 내용을 toostate는 *복제* toohello hello 복제 세트 (활성 보조 데이터베이스 라고 함)의 다른 복제본 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-118">Changes toostate from write operations are *replicated* toohello other replicas in hello replica set (called Active Secondaries) and applied.</span></span> 

<span data-ttu-id="895e3-119">주 복제본은 하나만 있을 수 있지만 활성 보조 복제본은 여러 개가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-119">There can be only one Primary replica, but there can be multiple Active Secondary replicas.</span></span> <span data-ttu-id="895e3-120">활성 보조 복제본의 hello 수, 구성 가능 하며 복제본 수가 많을 수록 동시 소프트웨어 및 하드웨어 오류 수를 더를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-120">hello number of Active Secondary replicas is configurable, and a higher number of replicas can tolerate a greater number of concurrent software and hardware failures.</span></span>

<span data-ttu-id="895e3-121">Hello 주 복제본의 작동이 서비스 패브릭 hello 활성 보조 복제본 hello 새로운 주 복제본 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-121">If hello Primary replica goes down, Service Fabric makes one of hello Active Secondary replicas hello new Primary replica.</span></span> <span data-ttu-id="895e3-122">활성 보조 복제본이 이미 업데이트 hello 버전의 hello 상태가 (통해 *복제*), 계속 해 서 추가 읽기를 처리 하 고 쓰기 작업 수 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-122">This Active Secondary replica already has hello updated version of hello state (via *replication*), and it can continue processing further read and write operations.</span></span>

<span data-ttu-id="895e3-123">이 개념을 되는 주 가상 컴퓨터 또는 활성 보조 복제본의 복제 역할 hello 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-123">This concept, of a replica being either a Primary or Active Secondary, is known as hello Replica Role.</span></span>

### <a name="replica-roles"></a><span data-ttu-id="895e3-124">복제본 역할</span><span class="sxs-lookup"><span data-stu-id="895e3-124">Replica roles</span></span>
<span data-ttu-id="895e3-125">복제본의 hello 역할은 해당 복제본에 의해 관리 되는 hello 상태의 사용 되는 toomanage hello 수명 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-125">hello role of a replica is used toomanage hello life cycle of hello state being managed by that replica.</span></span> <span data-ttu-id="895e3-126">주 역할의 복제본은 읽기 요청을 서비스합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-126">A replica whose role is Primary services read requests.</span></span> <span data-ttu-id="895e3-127">또한 hello 주 상태를 업데이트 한 hello 변경 내용을 복제 하 여 모든 쓰기 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-127">hello Primary also handles all write requests by updating its state and replicating hello changes.</span></span> <span data-ttu-id="895e3-128">이러한 변경은 hello 복제 세트에 적용 된 toohello 활성 보조입니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-128">These changes are applied toohello Active Secondaries in hello replica set.</span></span> <span data-ttu-id="895e3-129">hello는 활성 보조는 주 복제본을 hello tooreceive 상태의 변경 내용을 복제 되었는지 및 hello 상태 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-129">hello job of an Active Secondary is tooreceive state changes that hello Primary replica has replicated and update its view of hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="895e3-130">더 높은 수준의 프로그래밍와 같은 모델 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 및 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md) hello 개발자의 복제 역할의 hello 개념을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-130">Higher-level programming models such as [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) hide hello concept of replica role from hello developer.</span></span> <span data-ttu-id="895e3-131">작업자 역할의 hello 개념은 거의 대부분의 시나리오에 대 한 간소화 된 서비스에서 하는 동안 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="895e3-131">In Actors, hello notion of role is unnecessary, while in Services it is largely simplified for most scenarios.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="895e3-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="895e3-132">Next steps</span></span>
<span data-ttu-id="895e3-133">서비스 패브릭 개념에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="895e3-133">For more information on Service Fabric concepts, see hello following articles:</span></span>

- [<span data-ttu-id="895e3-134">Service Fabric 서비스 크기 조정</span><span class="sxs-lookup"><span data-stu-id="895e3-134">Scaling Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
- [<span data-ttu-id="895e3-135">서비스 패브릭 서비스 분할</span><span class="sxs-lookup"><span data-stu-id="895e3-135">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
- [<span data-ttu-id="895e3-136">상태 정의 및 관리</span><span class="sxs-lookup"><span data-stu-id="895e3-136">Defining and managing state</span></span>](service-fabric-concepts-state.md)
- [<span data-ttu-id="895e3-137">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="895e3-137">Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
