---
title: "Azure 서비스 패브릭 상태 저장 서비스에 대 한 컬렉션 aaaIntroduction tooReliable | Microsoft Docs"
description: "서비스 패브릭 상태 저장 서비스를 사용 하면 신뢰할 수 있는 컬렉션 toowrite 항상 사용 가능한 가능 하 고 대기 시간이 짧은 클라우드 응용 프로그램을 제공 합니다."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a><span data-ttu-id="80a71-103">Azure 서비스 패브릭 상태 저장 서비스의 컬렉션 소개 tooReliable</span><span class="sxs-lookup"><span data-stu-id="80a71-103">Introduction tooReliable Collections in Azure Service Fabric stateful services</span></span>
<span data-ttu-id="80a71-104">신뢰할 수 있는 컬렉션 사용 하면 항상 사용 가능한 가능 하 고 대기 시간이 짧은 클라우드 응용 프로그램 toowrite 단일 컴퓨터 응용 프로그램을 작성 하는 것에 처럼 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-104">Reliable Collections enable you toowrite highly available, scalable, and low-latency cloud applications as though you were writing single computer applications.</span></span> <span data-ttu-id="80a71-105">hello의 클래스 hello **Microsoft.ServiceFabric.Data.Collections** 네임 스페이스는 컬렉션에 자동으로 항상 사용 가능 상태 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-105">hello classes in hello **Microsoft.ServiceFabric.Data.Collections** namespace provide a set of collections that automatically make your state highly available.</span></span> <span data-ttu-id="80a71-106">개발자가 tooprogram만 toohello 신뢰할 수 있는 컬렉션 Api 필요를 복제 하는 hello 및 로컬 상태를 관리 하는 신뢰할 수 있는 컬렉션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-106">Developers need tooprogram only toohello Reliable Collection APIs and let Reliable Collections manage hello replicated and local state.</span></span>

<span data-ttu-id="80a71-107">신뢰할 수 있는 컬렉션 및 다른 고가용성 기술 (예: Redis, Azure 테이블 서비스 및 Azure 큐 서비스) 간의 hello 주요 차이점 hello 상태가 유지 되도록 로컬로 hello 서비스 인스턴스의 항상 사용할 수 있게 되는 동안입니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-107">hello key difference between Reliable Collections and other high-availability technologies (such as Redis, Azure Table service, and Azure Queue service) is that hello state is kept locally in hello service instance while also being made highly available.</span></span> <span data-ttu-id="80a71-108">이는 다음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-108">This means that:</span></span>

* <span data-ttu-id="80a71-109">모든 읽기가 로컬이므로 대기 시간이 짧고 처리량이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-109">All reads are local, which results in low latency and high-throughput reads.</span></span>
* <span data-ttu-id="80a71-110">모든 쓰기 hello 최소 네트워크 Io 수를 낮은 대기 시간에 발생 하 고 처리량이 높은 씁니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-110">All writes incur hello minimum number of network IOs, which results in low latency and high-throughput writes.</span></span>

![컬렉션 진화 이미지](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

<span data-ttu-id="80a71-112">신뢰할 수 있는 컬렉션의 hello 자연 스런 hello로 생각할 수 있습니다 **System.Collections** 클래스:에 대 한 복잡성을 늘리지 않고도 hello 클라우드 및 다중 컴퓨터 응용 프로그램을 위해 디자인 된 컬렉션의 새 집합 hello 개발자입니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-112">Reliable Collections can be thought of as hello natural evolution of hello **System.Collections** classes: a new set of collections that are designed for hello cloud and multi-computer applications without increasing complexity for hello developer.</span></span> <span data-ttu-id="80a71-113">따라서 신뢰할 수 있는 컬렉션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-113">As such, Reliable Collections are:</span></span>

* <span data-ttu-id="80a71-114">복제됨: 고가용성을 위해 상태 변경 내용이 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-114">Replicated: State changes are replicated for high availability.</span></span>
* <span data-ttu-id="80a71-115">Persisted: 데이터는 대규모 작동 중단 (예를 들어 데이터 센터 정전)에 대 한 내구성에 대 한 지속형된 toodisk 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-115">Persisted: Data is persisted toodisk for durability against large-scale outages (for example, a datacenter power outage).</span></span>
* <span data-ttu-id="80a71-116">비동기: Api는 비동기 tooensure IO를 초래 하는 경우 스레드가 차단 되지 않으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-116">Asynchronous: APIs are asynchronous tooensure that threads are not blocked when incurring IO.</span></span>
* <span data-ttu-id="80a71-117">트랜잭션: Api 활용 트랜잭션의 hello 추상화 서비스 내에서 신뢰할 수 있는 여러 컬렉션을 쉽게 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-117">Transactional: APIs utilize hello abstraction of transactions so you can manage multiple Reliable Collections within a service easily.</span></span>

<span data-ttu-id="80a71-118">신뢰할 수 있는 컬렉션에서 보다 쉽게 응용 프로그램 상태에 대 한 추론 hello 상자 toomake 강력한 일관성은 보장은 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-118">Reliable Collections provide strong consistency guarantees out of hello box toomake reasoning about application state easier.</span></span>
<span data-ttu-id="80a71-119">강력한 일관성 트랜잭션 커밋 hello 주를 포함 하 여 복제본의 과반수 쿼럼에 hello 전체 트랜잭션을 기록한 후에 완료 되도록 하 여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-119">Strong consistency is achieved by ensuring transaction commits finish only after hello entire transaction has been logged on a majority quorum of replicas, including hello primary.</span></span>
<span data-ttu-id="80a71-120">tooachieve 약한 일관성 응용 프로그램 백 toohello 클라이언트/요청자를 승인 하 수 hello 비동기 커밋 반환 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-120">tooachieve weaker consistency, applications can acknowledge back toohello client/requester before hello asynchronous commit returns.</span></span>

<span data-ttu-id="80a71-121">hello 신뢰할 수 있는 컬렉션 Api는 동시 컬렉션 Api의 진화 (hello에 **System.Collections.Concurrent** 네임 스페이스):</span><span class="sxs-lookup"><span data-stu-id="80a71-121">hello Reliable Collections APIs are an evolution of concurrent collections APIs (found in hello **System.Collections.Concurrent** namespace):</span></span>

* <span data-ttu-id="80a71-122">비동기: 작업 이후 동시 컬렉션와 달리 hello 작업은 복제 되 고 지속 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-122">Asynchronous: Returns a task since, unlike concurrent collections, hello operations are replicated and persisted.</span></span>
* <span data-ttu-id="80a71-123">Out 매개 변수 더: 사용 하 여 `ConditionalValue<T>` tooreturn bool 점과 out 매개 변수 값 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-123">No out parameters: Uses `ConditionalValue<T>` tooreturn a bool and a value instead of out parameters.</span></span> <span data-ttu-id="80a71-124">`ConditionalValue<T>`비슷합니다 `Nullable<T>` 하지만 T toobe 구조체는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-124">`ConditionalValue<T>` is like `Nullable<T>` but does not require T toobe a struct.</span></span>
* <span data-ttu-id="80a71-125">트랜잭션: 트랜잭션에서 여러 신뢰할 수 있는 컬렉션에 대 한 트랜잭션 개체 tooenable hello 사용자 toogroup 동작을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-125">Transactions: Uses a transaction object tooenable hello user toogroup actions on multiple Reliable Collections in a transaction.</span></span>

<span data-ttu-id="80a71-126">오늘날 **Microsoft.ServiceFabric.Data.Collections** 은 다음과 같은 3가지 컬렉션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-126">Today, **Microsoft.ServiceFabric.Data.Collections** contains three collections:</span></span>

* <span data-ttu-id="80a71-127">[신뢰할 수 있는 사전](https://msdn.microsoft.com/library/azure/dn971511.aspx): 키/값 쌍의 복제, 트랜잭션 및 비동기 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-127">[Reliable Dictionary](https://msdn.microsoft.com/library/azure/dn971511.aspx): Represents a replicated, transactional, and asynchronous collection of key/value pairs.</span></span> <span data-ttu-id="80a71-128">비슷한 너무**ConcurrentDictionary**, 둘 다 hello 키 및 모든 종류의 hello 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-128">Similar too**ConcurrentDictionary**, both hello key and hello value can be of any type.</span></span>
* <span data-ttu-id="80a71-129">[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx): 복제, 트랜잭션 및 비동기의 엄격한 FIFO(선입 선출) 큐를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-129">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx): Represents a replicated, transactional, and asynchronous strict first-in, first-out (FIFO) queue.</span></span> <span data-ttu-id="80a71-130">비슷한 너무**ConcurrentQueue**, hello 값은 모든 유형일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-130">Similar too**ConcurrentQueue**, hello value can be of any type.</span></span>
* <span data-ttu-id="80a71-131">[신뢰할 수 있는 동시 큐](service-fabric-reliable-services-reliable-concurrent-queue.md): 높은 처리량을 위해 최고의 순서로 대기되는 복제, 트랜잭션 및 비동기 큐.</span><span class="sxs-lookup"><span data-stu-id="80a71-131">[Reliable Concurrent Queue](service-fabric-reliable-services-reliable-concurrent-queue.md): Represents a replicated, transactional, and asynchronous best effort ordering queue for high throughput.</span></span> <span data-ttu-id="80a71-132">비슷한 toohello **ConcurrentQueue**, hello 값은 모든 유형일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80a71-132">Similar toohello **ConcurrentQueue**, hello value can be of any type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80a71-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80a71-133">Next steps</span></span>
* [<span data-ttu-id="80a71-134">신뢰할 수 있는 컬렉션 지침 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="80a71-134">Reliable Collection Guidelines & Recommendations</span></span>](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [<span data-ttu-id="80a71-135">신뢰할 수 있는 컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="80a71-135">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="80a71-136">트랜잭션 및 잠금</span><span class="sxs-lookup"><span data-stu-id="80a71-136">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [<span data-ttu-id="80a71-137">신뢰할 수 있는 상태 관리자 및 컬렉션 내부</span><span class="sxs-lookup"><span data-stu-id="80a71-137">Reliable State Manager and Collection Internals</span></span>](service-fabric-reliable-services-reliable-collections-internals.md)
* <span data-ttu-id="80a71-138">데이터 관리</span><span class="sxs-lookup"><span data-stu-id="80a71-138">Managing Data</span></span>
  * [<span data-ttu-id="80a71-139">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="80a71-139">Backup and Restore</span></span>](service-fabric-reliable-services-backup-restore.md)
  * [<span data-ttu-id="80a71-140">Notifications</span><span class="sxs-lookup"><span data-stu-id="80a71-140">Notifications</span></span>](service-fabric-reliable-services-notifications.md)
  * [<span data-ttu-id="80a71-141">신뢰할 수 있는 컬렉션 serialization</span><span class="sxs-lookup"><span data-stu-id="80a71-141">Reliable Collection serialization</span></span>](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [<span data-ttu-id="80a71-142">Serialization 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="80a71-142">Serialization and Upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="80a71-143">신뢰할 수 있는 상태 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="80a71-143">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* <span data-ttu-id="80a71-144">기타</span><span class="sxs-lookup"><span data-stu-id="80a71-144">Others</span></span>
  * [<span data-ttu-id="80a71-145">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="80a71-145">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  * [<span data-ttu-id="80a71-146">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="80a71-146">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
