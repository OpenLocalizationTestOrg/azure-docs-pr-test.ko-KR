---
title: "서비스 패브릭 성능 모니터링 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터를 모니터링하고 진단하기 위한 성능 카운터에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="10d58-103">성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="10d58-103">Performance metrics</span></span>

<span data-ttu-id="10d58-104">메트릭 수집된 toounderstand hello 성능 클러스터 수 뿐만 아니라 hello 응용 프로그램에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="10d58-105">서비스 패브릭 클러스터에 대 한 hello 다음 성능 카운터를 수집 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="10d58-106">노드</span><span class="sxs-lookup"><span data-stu-id="10d58-106">Nodes</span></span>

<span data-ttu-id="10d58-107">클러스터의 hello 컴퓨터용 hello 다음 toobetter 배율을 결정 하는 적절 한 클러스터를 만들고 각 컴퓨터에 부하를 hello를 이해 하는 성능 카운터를 수집 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="10d58-108">카운터 범주</span><span class="sxs-lookup"><span data-stu-id="10d58-108">Counter Category</span></span> | <span data-ttu-id="10d58-109">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="10d58-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="10d58-110">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-111">평균 디스크 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="10d58-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="10d58-112">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-113">평균 디스크 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="10d58-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="10d58-114">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-115">평균 디스크 초/읽기</span><span class="sxs-lookup"><span data-stu-id="10d58-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="10d58-116">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-117">평균 디스크 초/쓰기</span><span class="sxs-lookup"><span data-stu-id="10d58-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="10d58-118">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-119">디스크 읽기/초 </span><span class="sxs-lookup"><span data-stu-id="10d58-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="10d58-120">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-121">디스크 읽기 바이트/초 </span><span class="sxs-lookup"><span data-stu-id="10d58-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="10d58-122">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-123">디스크 쓰기/초</span><span class="sxs-lookup"><span data-stu-id="10d58-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="10d58-124">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="10d58-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="10d58-125">디스크 쓰기 바이트/초</span><span class="sxs-lookup"><span data-stu-id="10d58-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="10d58-126">메모리</span><span class="sxs-lookup"><span data-stu-id="10d58-126">Memory</span></span> | <span data-ttu-id="10d58-127">Available MBytes</span><span class="sxs-lookup"><span data-stu-id="10d58-127">Available MBytes</span></span> |
| <span data-ttu-id="10d58-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="10d58-128">PagingFile</span></span> | <span data-ttu-id="10d58-129">% 사용량</span><span class="sxs-lookup"><span data-stu-id="10d58-129">% Usage</span></span> |
| <span data-ttu-id="10d58-130">프로세스(합계)</span><span class="sxs-lookup"><span data-stu-id="10d58-130">Process(Total)</span></span> | <span data-ttu-id="10d58-131">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="10d58-131">% Processor Time</span></span> |
| <span data-ttu-id="10d58-132">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-132">Process (per service)</span></span> | <span data-ttu-id="10d58-133">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="10d58-133">% Processor Time</span></span> |
| <span data-ttu-id="10d58-134">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-134">Process (per service)</span></span> | <span data-ttu-id="10d58-135">ID 프로세스</span><span class="sxs-lookup"><span data-stu-id="10d58-135">ID Process</span></span> |
| <span data-ttu-id="10d58-136">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-136">Process (per service)</span></span> | <span data-ttu-id="10d58-137">프로세스 바이트</span><span class="sxs-lookup"><span data-stu-id="10d58-137">Private Bytes</span></span> |
| <span data-ttu-id="10d58-138">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-138">Process (per service)</span></span> | <span data-ttu-id="10d58-139">스레드 개수</span><span class="sxs-lookup"><span data-stu-id="10d58-139">Thread Count</span></span> |
| <span data-ttu-id="10d58-140">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-140">Process (per service)</span></span> | <span data-ttu-id="10d58-141">가상 바이트</span><span class="sxs-lookup"><span data-stu-id="10d58-141">Virtual Bytes</span></span> |
| <span data-ttu-id="10d58-142">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-142">Process (per service)</span></span> | <span data-ttu-id="10d58-143">작업 집합</span><span class="sxs-lookup"><span data-stu-id="10d58-143">Working Set</span></span> |
| <span data-ttu-id="10d58-144">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-144">Process (per service)</span></span> | <span data-ttu-id="10d58-145">작업 집합 - 개인</span><span class="sxs-lookup"><span data-stu-id="10d58-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="10d58-146">.NET 응용 프로그램 및 서비스</span><span class="sxs-lookup"><span data-stu-id="10d58-146">.NET applications and services</span></span>

<span data-ttu-id="10d58-147">.NET 서비스 tooyour 클러스터를 배포 하는 경우 카운터를 따라 hello를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="10d58-148">카운터 범주</span><span class="sxs-lookup"><span data-stu-id="10d58-148">Counter Category</span></span> | <span data-ttu-id="10d58-149">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="10d58-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="10d58-150">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-151">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="10d58-151">Process ID</span></span> |
| <span data-ttu-id="10d58-152">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-153">#커밋된 전체 바이트</span><span class="sxs-lookup"><span data-stu-id="10d58-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="10d58-154">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-155">#예약된 전체 바이트</span><span class="sxs-lookup"><span data-stu-id="10d58-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="10d58-156">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-157">#모든 힙의 바이트</span><span class="sxs-lookup"><span data-stu-id="10d58-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="10d58-158">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-159">#0 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="10d58-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="10d58-160">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-161">#1 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="10d58-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="10d58-162">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-163">#2 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="10d58-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="10d58-164">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="10d58-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="10d58-165">% Time in GC</span><span class="sxs-lookup"><span data-stu-id="10d58-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="10d58-166">Service Fabric 사용자 지정 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="10d58-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="10d58-167">Service Fabric은 상당한 양의 사용자 지정 성능 카운터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="10d58-168">Hello SDK가 설치 되어 있는 경우 목록을 볼 수 있습니다 hello 포괄적인 Windows 컴퓨터에 성능 모니터 응용 프로그램에서 (시작 > 성능 모니터).</span><span class="sxs-lookup"><span data-stu-id="10d58-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="10d58-169">Hello 응용 프로그램에서 배포 하는 tooyour 클러스터, Reliable Actors를 사용 하는 경우 추가에서 countes `Service Fabric Actor` 및 `Service Fabric Actor Method` 범주 (참조 [서비스 패브릭 신뢰할 수 있는 작업 자가 진단](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="10d58-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="10d58-170">마찬가지로 Reliable Services를 사용하는 경우 카운터를 수집해야 하는 `Service Fabric Service` 및 `Service Fabric Service Method` 카운터 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="10d58-171">신뢰할 수 있는 컬렉션을 사용 하는 경우 hello 추가 하는 것이 좋습니다 `Avg. Transaction ms/Commit` hello에서 `Service Fabric Transactional Replicator` 트랜잭션 메트릭에 당 toocollect hello 평균 커밋 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="10d58-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="10d58-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10d58-172">Next steps</span></span>

* <span data-ttu-id="10d58-173">에 대 한 자세한 내용은 [hello 플랫폼 수준에서 이벤트 생성](service-fabric-diagnostics-event-generation-infra.md) 서비스 패브릭에서</span><span class="sxs-lookup"><span data-stu-id="10d58-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="10d58-174">[Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md)을 통해 성능 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="10d58-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
