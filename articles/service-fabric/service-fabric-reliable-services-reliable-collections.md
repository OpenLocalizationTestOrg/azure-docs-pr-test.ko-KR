---
title: "Azure Service Fabric 상태 저장 서비스의 신뢰할 수 있는 컬렉션 소개 | Microsoft Docs"
description: "서비스 패브릭 상태 저장 서비스는가용성 높고, 확장 가능하며, 대기 시간이 낮은 클라우드 응용 프로그램을 작성할 수 있는 믿을 수 렉션을 제공합니다."
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
ms.openlocfilehash: d0247ba0242af05ca6dcd8049ff9116683538fa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliable-collections-in-azure-service-fabric-stateful-services"></a><span data-ttu-id="b5c83-103">Azure 서비스 패브릭 상태 저장 서비스의 신뢰할 수 있는 컬렉션 소개</span><span class="sxs-lookup"><span data-stu-id="b5c83-103">Introduction to Reliable Collections in Azure Service Fabric stateful services</span></span>
<span data-ttu-id="b5c83-104">신뢰할 수 있는 컬렉션을 사용하면 단일 컴퓨터 응용 프로그램을 작성하는 것처럼 가용성이 높고, 확장 가능하며, 대기 시간이 낮은 클라우드 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-104">Reliable Collections enable you to write highly available, scalable, and low-latency cloud applications as though you were writing single computer applications.</span></span> <span data-ttu-id="b5c83-105">**Microsoft.ServiceFabric.Data.Collections** 네임스페이스의 클래스는 상태를 자동으로 항상 사용할 수 있도록 하는 컬렉션 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-105">The classes in the **Microsoft.ServiceFabric.Data.Collections** namespace provide a set of collections that automatically make your state highly available.</span></span> <span data-ttu-id="b5c83-106">개발자는 신뢰할 수 있는 컬렉션 API로 프로그래밍하고 신뢰할 수 있는 컬렉션이 복제된 로컬 상태를 관리하도록 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-106">Developers need to program only to the Reliable Collection APIs and let Reliable Collections manage the replicated and local state.</span></span>

<span data-ttu-id="b5c83-107">신뢰할 수 있는 컬렉션과 다른 고가용성 기술 (예: Redis, Azure 테이블 서비스 및 Azure 큐 서비스)의 주요 차이점은 상태가 서비스 인스턴스에서 로컬로 유지되지만 가용성도 높다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-107">The key difference between Reliable Collections and other high-availability technologies (such as Redis, Azure Table service, and Azure Queue service) is that the state is kept locally in the service instance while also being made highly available.</span></span> <span data-ttu-id="b5c83-108">이는 다음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-108">This means that:</span></span>

* <span data-ttu-id="b5c83-109">모든 읽기가 로컬이므로 대기 시간이 짧고 처리량이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-109">All reads are local, which results in low latency and high-throughput reads.</span></span>
* <span data-ttu-id="b5c83-110">모든 쓰기가 최소한의 네트워크 IO 수를 유발하므로 대기 시간이 짧고 처리량이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-110">All writes incur the minimum number of network IOs, which results in low latency and high-throughput writes.</span></span>

![컬렉션 진화 이미지](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

<span data-ttu-id="b5c83-112">신뢰할 수 있는 컬렉션은 **System.Collections** 클래스의 자연스러운 진화로 생각할 수 있습니다. 즉, 개발자의 복잡성을 늘리지 않고 클라우드 및 다중 컴퓨터 응용 프로그램을 위해 설계된 컬렉션의 새 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-112">Reliable Collections can be thought of as the natural evolution of the **System.Collections** classes: a new set of collections that are designed for the cloud and multi-computer applications without increasing complexity for the developer.</span></span> <span data-ttu-id="b5c83-113">따라서 신뢰할 수 있는 컬렉션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-113">As such, Reliable Collections are:</span></span>

* <span data-ttu-id="b5c83-114">복제됨: 고가용성을 위해 상태 변경 내용이 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-114">Replicated: State changes are replicated for high availability.</span></span>
* <span data-ttu-id="b5c83-115">유지됨: 대규모 정전에 대한 내구성을 위해 데이터가 디스크에 유지됩니다(예: 데이터 센터 전원 정전).</span><span class="sxs-lookup"><span data-stu-id="b5c83-115">Persisted: Data is persisted to disk for durability against large-scale outages (for example, a datacenter power outage).</span></span>
* <span data-ttu-id="b5c83-116">비동기: API는 IO를 초래할 때 스레드가 차단되지 않도록 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-116">Asynchronous: APIs are asynchronous to ensure that threads are not blocked when incurring IO.</span></span>
* <span data-ttu-id="b5c83-117">트랜잭션: API가 트랜잭션 추상화를 활용하므로 서비스 내에서 여러 신뢰할 수 있는 컬렉션을 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-117">Transactional: APIs utilize the abstraction of transactions so you can manage multiple Reliable Collections within a service easily.</span></span>

<span data-ttu-id="b5c83-118">신뢰할 수 있는 컬렉션은 기본적으로 강력한 일관성을 보장하여 응용 프로그램 상태에 대한 추론을 보다 쉽게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-118">Reliable Collections provide strong consistency guarantees out of the box to make reasoning about application state easier.</span></span>
<span data-ttu-id="b5c83-119">강력한 일관성은 주 복제본을 포함한 복제본의 과반수 쿼럼에 전체 트랜잭션이 기록된 후에만 트랜잭션 커밋을 완료하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-119">Strong consistency is achieved by ensuring transaction commits finish only after the entire transaction has been logged on a majority quorum of replicas, including the primary.</span></span>
<span data-ttu-id="b5c83-120">약한 일관성을 달성하려면 비동기 커밋이 반환되기 전에 응용 프로그램이 클라이언트/요청자에 다시 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-120">To achieve weaker consistency, applications can acknowledge back to the client/requester before the asynchronous commit returns.</span></span>

<span data-ttu-id="b5c83-121">신뢰할 수 있는 컬렉션 API는 동시 컬렉션 API( **System.Collections.Concurrent** 네임스페이스에 있음)의 진화입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-121">The Reliable Collections APIs are an evolution of concurrent collections APIs (found in the **System.Collections.Concurrent** namespace):</span></span>

* <span data-ttu-id="b5c83-122">비동기: 동시 컬렉션과 달리 작업이 복제 및 유지되므로 작업을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-122">Asynchronous: Returns a task since, unlike concurrent collections, the operations are replicated and persisted.</span></span>
* <span data-ttu-id="b5c83-123">출력 매개 변수 없음: `ConditionalValue<T>` 를 사용하여 출력 매개 변수 대신 부울 및 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-123">No out parameters: Uses `ConditionalValue<T>` to return a bool and a value instead of out parameters.</span></span> <span data-ttu-id="b5c83-124">`ConditionalValue<T>`는 `Nullable<T>`과 유사하지만 T가 구조체일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-124">`ConditionalValue<T>` is like `Nullable<T>` but does not require T to be a struct.</span></span>
* <span data-ttu-id="b5c83-125">트랜잭션: 트랜잭션 개체를 사용하여 사용자가 트랜잭션의 여러 신뢰할 수 있는 컬렉션에 대한 작업을 그룹화하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-125">Transactions: Uses a transaction object to enable the user to group actions on multiple Reliable Collections in a transaction.</span></span>

<span data-ttu-id="b5c83-126">오늘날 **Microsoft.ServiceFabric.Data.Collections** 은 다음과 같은 3가지 컬렉션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-126">Today, **Microsoft.ServiceFabric.Data.Collections** contains three collections:</span></span>

* <span data-ttu-id="b5c83-127">[신뢰할 수 있는 사전](https://msdn.microsoft.com/library/azure/dn971511.aspx): 키/값 쌍의 복제, 트랜잭션 및 비동기 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-127">[Reliable Dictionary](https://msdn.microsoft.com/library/azure/dn971511.aspx): Represents a replicated, transactional, and asynchronous collection of key/value pairs.</span></span> <span data-ttu-id="b5c83-128">**ConcurrentDictionary**와 유사하게 키와 값은 모든 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-128">Similar to **ConcurrentDictionary**, both the key and the value can be of any type.</span></span>
* <span data-ttu-id="b5c83-129">[신뢰할 수 있는 큐](https://msdn.microsoft.com/library/azure/dn971527.aspx): 복제, 트랜잭션 및 비동기의 엄격한 FIFO(선입 선출) 큐를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-129">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx): Represents a replicated, transactional, and asynchronous strict first-in, first-out (FIFO) queue.</span></span> <span data-ttu-id="b5c83-130">**ConcurrentQueue**와 유사하게 값은 어떤 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-130">Similar to **ConcurrentQueue**, the value can be of any type.</span></span>
* <span data-ttu-id="b5c83-131">[신뢰할 수 있는 동시 큐](service-fabric-reliable-services-reliable-concurrent-queue.md): 높은 처리량을 위해 최고의 순서로 대기되는 복제, 트랜잭션 및 비동기 큐.</span><span class="sxs-lookup"><span data-stu-id="b5c83-131">[Reliable Concurrent Queue](service-fabric-reliable-services-reliable-concurrent-queue.md): Represents a replicated, transactional, and asynchronous best effort ordering queue for high throughput.</span></span> <span data-ttu-id="b5c83-132">**ConcurrentQueue**와 유사하게 값은 어떤 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c83-132">Similar to the **ConcurrentQueue**, the value can be of any type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5c83-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b5c83-133">Next steps</span></span>
* [<span data-ttu-id="b5c83-134">신뢰할 수 있는 컬렉션 지침 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b5c83-134">Reliable Collection Guidelines & Recommendations</span></span>](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [<span data-ttu-id="b5c83-135">신뢰할 수 있는 컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="b5c83-135">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="b5c83-136">트랜잭션 및 잠금</span><span class="sxs-lookup"><span data-stu-id="b5c83-136">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [<span data-ttu-id="b5c83-137">신뢰할 수 있는 상태 관리자 및 컬렉션 내부</span><span class="sxs-lookup"><span data-stu-id="b5c83-137">Reliable State Manager and Collection Internals</span></span>](service-fabric-reliable-services-reliable-collections-internals.md)
* <span data-ttu-id="b5c83-138">데이터 관리</span><span class="sxs-lookup"><span data-stu-id="b5c83-138">Managing Data</span></span>
  * [<span data-ttu-id="b5c83-139">백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="b5c83-139">Backup and Restore</span></span>](service-fabric-reliable-services-backup-restore.md)
  * [<span data-ttu-id="b5c83-140">Notifications</span><span class="sxs-lookup"><span data-stu-id="b5c83-140">Notifications</span></span>](service-fabric-reliable-services-notifications.md)
  * [<span data-ttu-id="b5c83-141">신뢰할 수 있는 컬렉션 serialization</span><span class="sxs-lookup"><span data-stu-id="b5c83-141">Reliable Collection serialization</span></span>](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [<span data-ttu-id="b5c83-142">Serialization 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b5c83-142">Serialization and Upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="b5c83-143">신뢰할 수 있는 상태 관리자 구성</span><span class="sxs-lookup"><span data-stu-id="b5c83-143">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* <span data-ttu-id="b5c83-144">기타</span><span class="sxs-lookup"><span data-stu-id="b5c83-144">Others</span></span>
  * [<span data-ttu-id="b5c83-145">Reliable Services 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="b5c83-145">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  * [<span data-ttu-id="b5c83-146">신뢰할 수 있는 컬렉션에 대한 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="b5c83-146">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
