---
title: "Azure Service Fabric 성능 모니터링 | Microsoft Docs"
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="c6c92-103">성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="c6c92-103">Performance metrics</span></span>

<span data-ttu-id="c6c92-104">클러스터의 성능 및 클러스터에서 실행 중인 응용 프로그램을 이해하기 위해 메트릭을 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="c6c92-105">Service Fabric 클러스터의 경우 다음과 같은 성능 카운터를 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="c6c92-106">노드</span><span class="sxs-lookup"><span data-stu-id="c6c92-106">Nodes</span></span>

<span data-ttu-id="c6c92-107">클러스터의 컴퓨터의 경우 각 컴퓨터의 부하를 이해하고 적절한 클러스터 크기 조정을 결정하려면 다음과 같은 성능 카운터를 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="c6c92-108">카운터 범주</span><span class="sxs-lookup"><span data-stu-id="c6c92-108">Counter Category</span></span> | <span data-ttu-id="c6c92-109">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="c6c92-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c6c92-110">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-111">평균</span><span class="sxs-lookup"><span data-stu-id="c6c92-111">Avg.</span></span> <span data-ttu-id="c6c92-112">디스크 읽기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="c6c92-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="c6c92-113">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-114">평균</span><span class="sxs-lookup"><span data-stu-id="c6c92-114">Avg.</span></span> <span data-ttu-id="c6c92-115">디스크 쓰기 큐 길이</span><span class="sxs-lookup"><span data-stu-id="c6c92-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="c6c92-116">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-117">평균</span><span class="sxs-lookup"><span data-stu-id="c6c92-117">Avg.</span></span> <span data-ttu-id="c6c92-118">디스크 초/읽기</span><span class="sxs-lookup"><span data-stu-id="c6c92-118">Disk sec/Read</span></span> |
| <span data-ttu-id="c6c92-119">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-120">평균</span><span class="sxs-lookup"><span data-stu-id="c6c92-120">Avg.</span></span> <span data-ttu-id="c6c92-121">디스크 초/쓰기</span><span class="sxs-lookup"><span data-stu-id="c6c92-121">Disk sec/Write</span></span> |
| <span data-ttu-id="c6c92-122">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-123">디스크 읽기/초 </span><span class="sxs-lookup"><span data-stu-id="c6c92-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="c6c92-124">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-125">디스크 읽기 바이트/초 </span><span class="sxs-lookup"><span data-stu-id="c6c92-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="c6c92-126">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-127">디스크 쓰기/초</span><span class="sxs-lookup"><span data-stu-id="c6c92-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="c6c92-128">PhysicalDisk(디스크당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c6c92-129">디스크 쓰기 바이트/초</span><span class="sxs-lookup"><span data-stu-id="c6c92-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="c6c92-130">메모리</span><span class="sxs-lookup"><span data-stu-id="c6c92-130">Memory</span></span> | <span data-ttu-id="c6c92-131">Available MBytes</span><span class="sxs-lookup"><span data-stu-id="c6c92-131">Available MBytes</span></span> |
| <span data-ttu-id="c6c92-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="c6c92-132">PagingFile</span></span> | <span data-ttu-id="c6c92-133">% 사용량</span><span class="sxs-lookup"><span data-stu-id="c6c92-133">% Usage</span></span> |
| <span data-ttu-id="c6c92-134">프로세스(합계)</span><span class="sxs-lookup"><span data-stu-id="c6c92-134">Process(Total)</span></span> | <span data-ttu-id="c6c92-135">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="c6c92-135">% Processor Time</span></span> |
| <span data-ttu-id="c6c92-136">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-136">Process (per service)</span></span> | <span data-ttu-id="c6c92-137">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="c6c92-137">% Processor Time</span></span> |
| <span data-ttu-id="c6c92-138">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-138">Process (per service)</span></span> | <span data-ttu-id="c6c92-139">ID 프로세스</span><span class="sxs-lookup"><span data-stu-id="c6c92-139">ID Process</span></span> |
| <span data-ttu-id="c6c92-140">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-140">Process (per service)</span></span> | <span data-ttu-id="c6c92-141">프로세스 바이트</span><span class="sxs-lookup"><span data-stu-id="c6c92-141">Private Bytes</span></span> |
| <span data-ttu-id="c6c92-142">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-142">Process (per service)</span></span> | <span data-ttu-id="c6c92-143">스레드 개수</span><span class="sxs-lookup"><span data-stu-id="c6c92-143">Thread Count</span></span> |
| <span data-ttu-id="c6c92-144">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-144">Process (per service)</span></span> | <span data-ttu-id="c6c92-145">가상 바이트</span><span class="sxs-lookup"><span data-stu-id="c6c92-145">Virtual Bytes</span></span> |
| <span data-ttu-id="c6c92-146">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-146">Process (per service)</span></span> | <span data-ttu-id="c6c92-147">작업 집합</span><span class="sxs-lookup"><span data-stu-id="c6c92-147">Working Set</span></span> |
| <span data-ttu-id="c6c92-148">프로세스(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-148">Process (per service)</span></span> | <span data-ttu-id="c6c92-149">작업 집합 - 개인</span><span class="sxs-lookup"><span data-stu-id="c6c92-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="c6c92-150">.NET 응용 프로그램 및 서비스</span><span class="sxs-lookup"><span data-stu-id="c6c92-150">.NET applications and services</span></span>

<span data-ttu-id="c6c92-151">.NET 서비스를 클러스터에 배포하는 경우 다음과 같은 카운터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="c6c92-152">카운터 범주</span><span class="sxs-lookup"><span data-stu-id="c6c92-152">Counter Category</span></span> | <span data-ttu-id="c6c92-153">카운터 이름</span><span class="sxs-lookup"><span data-stu-id="c6c92-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c6c92-154">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-155">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="c6c92-155">Process ID</span></span> |
| <span data-ttu-id="c6c92-156">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-157">#커밋된 전체 바이트</span><span class="sxs-lookup"><span data-stu-id="c6c92-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="c6c92-158">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-159">#예약된 전체 바이트</span><span class="sxs-lookup"><span data-stu-id="c6c92-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="c6c92-160">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-161">#모든 힙의 바이트</span><span class="sxs-lookup"><span data-stu-id="c6c92-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="c6c92-162">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-163">#0 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="c6c92-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="c6c92-164">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-165">#1 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="c6c92-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="c6c92-166">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-167">#2 컬렉션 생성</span><span class="sxs-lookup"><span data-stu-id="c6c92-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="c6c92-168">.NET CLR 메모리(서비스당)</span><span class="sxs-lookup"><span data-stu-id="c6c92-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c6c92-169">% Time in GC</span><span class="sxs-lookup"><span data-stu-id="c6c92-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="c6c92-170">Service Fabric 사용자 지정 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="c6c92-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="c6c92-171">Service Fabric은 상당한 양의 사용자 지정 성능 카운터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="c6c92-172">SDK가 설치되어 있는 경우 성능 모니터 응용 프로그램에서 Windows 컴퓨터의 포괄적인 목록을 볼 수 있습니다(시작 > 성능 모니터).</span><span class="sxs-lookup"><span data-stu-id="c6c92-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="c6c92-173">클러스터에 배포하는 응용 프로그램에서 Reliable Actors를 사용하는 경우 `Service Fabric Actor` 및 `Service Fabric Actor Method` 범주에서 카운터를 추가합니다([Service Fabric Reliable Actors 진단](service-fabric-reliable-actors-diagnostics.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="c6c92-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="c6c92-174">마찬가지로 Reliable Services를 사용하는 경우 카운터를 수집해야 하는 `Service Fabric Service` 및 `Service Fabric Service Method` 카운터 범주가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="c6c92-175">신뢰할 수 있는 컬렉션을 사용하는 경우 `Service Fabric Transactional Replicator`에서 `Avg. Transaction ms/Commit`을 추가하여 트랜잭션 메트릭당 평균 커밋 대기 시간을 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6c92-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6c92-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6c92-176">Next steps</span></span>

* <span data-ttu-id="c6c92-177">Service Fabric에서 [플랫폼 수준의 이벤트 생성](service-fabric-diagnostics-event-generation-infra.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="c6c92-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="c6c92-178">[Azure 진단](service-fabric-diagnostics-event-aggregation-wad.md)을 통해 성능 메트릭 수집</span><span class="sxs-lookup"><span data-stu-id="c6c92-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
