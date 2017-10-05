---
title: "SCP.NET 프로그래밍 가이드 | Microsoft Docs"
description: "HDInsight의 Storm 사용을 위해 SCP.NET을 사용하여 .NET 기반 Storm 토폴로지를 만드는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="e5733-103">SCP 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="e5733-103">SCP programming guide</span></span>
<span data-ttu-id="e5733-104">SCP는 안정적이며 일관성 있는 실시간 고성능 데이터 처리 응용 프로그램을 빌드하기 위한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="e5733-105">이 플랫폼은 OSS 커뮤니티에서 디자인한 스트림 처리 시스템인 [Apache Storm](http://storm.incubator.apache.org/)을 기반으로 구축되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="e5733-106">Nathan Marz가 디자인한 Storm은 Twitter에서 오픈 소스 방식으로 제공되며,</span><span class="sxs-lookup"><span data-stu-id="e5733-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="e5733-107">매우 안정적인 분산 방식 조정과 상태 관리를 수행하는 데 사용할 수 있는 또 다른 Apache 프로젝트인 [Apache ZooKeeper](http://zookeeper.apache.org/)를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="e5733-108">SCP 프로젝트를 통해 Windows에서 Storm을 포팅할 수 있을 뿐 아니라 Windows 에코시스템용 확장 및 사용자 지정도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="e5733-109">이 확장에는 .NET 개발자 환경과 라이브러리가 포함되고 사용자 지정에는 Windows 기반 배포가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="e5733-110">확장과 사용자 지정은 OSS 프로젝트를 분기하지 않아도 되는 방식으로 수행되며, Storm을 기반으로 구축된 파생 에코시스템을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="e5733-111">처리 모델</span><span class="sxs-lookup"><span data-stu-id="e5733-111">Processing model</span></span>
<span data-ttu-id="e5733-112">SCP의 데이터는 튜플의 연속 스트림으로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="e5733-113">일반적으로 튜플은 먼저 큐로 이동한 다음 Storm 토폴로지 내에서 호스트되는 비즈니스 논리에 의해 선택 및 변환됩니다. 그리고 마지막으로 출력을 다른 SCP 시스템에 튜플로 파이프하거나, SQL Server 등의 데이터베이스 또는 분산 파일 시스템에서와 같이 저장소에 커밋할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![데이터 저장소를 피드하는 데이터 피드에서 처리로의 큐 다이어그램](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="e5733-115">Storm에서는 응용 프로그램 토폴로지에 따라 계산 그래프가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="e5733-116">토폴로지의 각 노드에는 처리 논리가 포함되며 노드 간의 링크는 데이터 흐름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="e5733-117">토폴로지에 입력 데이터를 삽입하는 노드인 Spout는 데이터 순서를 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="e5733-118">입력 데이터는 파일 로그, 트랜잭션 데이터베이스, 시스템 성능 카운터 등에 있을 수 있습니다. 입력 및 출력 데이터 흐름을 포함하는 노드는 실제 데이터 필터링과 선택 및 집계를 하는 Bolt라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="e5733-119">SCP는 최상의 노력, 최소한 한 번 및 정확히 한 번 방식의 데이터 처리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="e5733-120">분산된 스트리밍 처리 응용 프로그램에서 네트워크 중단, 컴퓨터 오류 또는 사용자 코드 오류 등과 같은 데이터 처리 중 다양한 오류가 발생할 수 있습니다. 최소한 한 번 방식의 처리는 오류 발생 시 동일한 데이터를 자동으로 재생하여 모든 데이터를 한 번 이상 처리되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="e5733-121">최소한 한 번 방식의 처리는 간단하고 안정적이며 대부분의 응용 프로그램에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="e5733-122">그러나 응용 프로그램에서 정확한 계산을 수행해야 하는 등의 경우에는 응용 프로그램 토폴로지에서 같은 데이터가 재생될 가능성이 있으므로 최소한 한 번 방식의 처리로는 부족합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="e5733-123">이러한 경우에는 데이터가 여러 번 재생 및 처리되어도 올바른 결과를 계산하는 정확히 한 번 방식의 처리 방식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="e5733-124">.NET 개발자는 SCP를 통해 JVM(Java Virtual Machine) 기반 Storm을 백그라운드에서 활용하면서 실시간 데이터 프로세스 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="e5733-125">.NET과 JVM은 TCP 로컬 소켓을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="e5733-126">기본적으로 각 Spout/Bolt는 .NET/Java 프로세스 쌍이며 사용자 논리는 .NET 프로세스에서 플러그 인으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="e5733-127">SCP를 기반으로 데이터 처리 응용 프로그램을 빌드하려면 몇 가지 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="e5733-128">큐에서 데이터를 끌어오도록 Spout를 디자인 및 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="e5733-129">입력 데이터를 처리한 다음 데이터베이스 등의 외부 저장소에 데이터를 저장하도록 Bolt를 디자인 및 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="e5733-130">토폴로지를 디자인한 다음 제출하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="e5733-131">토폴로지는 꼭짓점 및 꼭짓점 간의 데이터 흐름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="e5733-132">SCP는 토폴로지 사양을 가져온 다음 Storm 클러스터에 배포합니다. 이 클러스터의 각 논리 노드에서 개별 꼭짓점이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="e5733-133">Storm 작업 스케줄러가 장애 조치(failover) 및 확장을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="e5733-134">이 문서에서는 몇 가지 간단한 예를 통해 SCP를 사용하여 데이터 처리 응용 프로그램을 빌드하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="e5733-135">SCP 플러그 인 인터페이스</span><span class="sxs-lookup"><span data-stu-id="e5733-135">SCP Plugin Interface</span></span>
<span data-ttu-id="e5733-136">SCP 플러그 인(응용 프로그램)은 개발 단계 중에 Visual Studio 내에서도 독립적으로 실행할 수 있고 프로덕션 환경에 배포한 후에 Storm 파이프라인에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="e5733-137">SCP 플러그 인 작성 방법은 다른 표준 Windows 콘솔 응용 프로그램 작성 방법과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="e5733-138">SCP.NET 플랫폼에서는 Spout/Bolt용 인터페이스를 선언하며, 사용자 플러그 인 코드는 이러한 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="e5733-139">이러한 디자인은 기본적으로 사용자가 자신의 비즈니스 논리를 실행하는 데 주력하고 나머지 작업은 SCP.NET 플랫폼이 처리하도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="e5733-140">토폴로지의 유형(트랜잭션/비트랜잭션) 및 구성 요소의 유형(Spout/Bolt)에 따라 사용자 플러그 인 코드는 다음 인터페이스 중 하나를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="e5733-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="e5733-141">ISCPSpout</span></span>
* <span data-ttu-id="e5733-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="e5733-142">ISCPBolt</span></span>
* <span data-ttu-id="e5733-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="e5733-143">ISCPTxSpout</span></span>
* <span data-ttu-id="e5733-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="e5733-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="e5733-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="e5733-145">ISCPPlugin</span></span>
<span data-ttu-id="e5733-146">ISCPPlugin은 모든 종류의 플러그 인에 공통적으로 적용되는 인터페이스로,</span><span class="sxs-lookup"><span data-stu-id="e5733-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="e5733-147">현재는 더미 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="e5733-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="e5733-148">ISCPSpout</span></span>
<span data-ttu-id="e5733-149">ISCPSpout는 비트랜잭션 Spout용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="e5733-150">`NextTuple()`가 호출되면 C\# 사용자 코드가 하나 이상의 튜플을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="e5733-151">내보낼 튜플이 없으면 아무 항목도 내보내지 않고 이 메서드가 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="e5733-152">`NextTuple()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="e5733-153">내보낼 튜플이 없으면 CPU를 너무 많이 낭비하지 않도록 10밀리초 등의 짧은 시간 동안 NextTuple을 유휴 상태로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="e5733-154">`Ack()` 및 `Fail()`은(는) 사양 파일에서 승인 메커니즘이 사용하도록 설정되어 있어야 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="e5733-155">`seqId` 은(는) 승인되거나 실패한 튜플을 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="e5733-156">따라서 비트랜잭션 토폴로지에서 승인이 사용하도록 설정되어 있으면 Spout에서 다음의 내보내기 함수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="e5733-157">비트랜잭션 토폴로지에서 승인이 지원되지 않으면 `Ack()` 및 `Fail()`은(는) 빈 함수로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="e5733-158">이러한 함수의 `parms` 입력 매개 변수는 빈 사전이며 나중에 사용하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="e5733-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="e5733-159">ISCPBolt</span></span>
<span data-ttu-id="e5733-160">ISCPBolt는 비트랜잭션 Bolt용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="e5733-161">새 튜플을 사용할 수 있으면 `Execute()` 함수가 호출되어 해당 튜플을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="e5733-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="e5733-162">ISCPTxSpout</span></span>
<span data-ttu-id="e5733-163">ISCPTxSpout는 트랜잭션 Spout용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="e5733-164">해당하는 비트랜잭션 함수와 마찬가지로 `NextTx()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="e5733-165">내보낼 데이터가 없으면 CPU를 너무 많이 낭비하지 않도록 10밀리초 등의 짧은 시간 동안 `NextTx` 을(를) 유휴 상태로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="e5733-166">`NextTx()`을(를) 호출하여 새 트랜잭션을 시작하고 출력 매개 변수 `seqId`을(를) 사용하여 트랜잭션을 식별하며 `Ack()` 및 `Fail()`에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="e5733-167">사용자는 `NextTx()`에서 Java 쪽으로 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="e5733-168">재생을 지원하기 위해 데이터는 ZooKeeper에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="e5733-169">ZooKeeper의 용량은 매우 제한되어 있으므로 사용자는 트랜잭션 Spout에서 데이터를 대량으로 내보내서는 안 되며 메타데이터만 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="e5733-170">Storm에서는 트랜잭션이 실패하면 자동으로 재생하므로 일반적인 경우에는 `Fail()` 을(를) 호출하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="e5733-171">그러나 SCP는 트랜잭션 Spout에서 내보낸 메타데이터를 확인할 수 있으면 메타데이터가 잘못된 경우 `Fail()` 을(를) 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="e5733-172">이러한 함수의 `parms` 입력 매개 변수는 빈 사전이며 나중에 사용하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="e5733-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="e5733-173">ISCPBatchBolt</span></span>
<span data-ttu-id="e5733-174">ISCPBatchBolt는 트랜잭션 Bolt용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="e5733-175">`Execute()` 이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="e5733-176">`FinishBatch()` 이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="e5733-177">`parms` 입력 매개 변수는 나중에 사용하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="e5733-178">트랜잭션 토폴로지에는 `StormTxAttempt`(이)라는 중요한 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="e5733-179">두 필드 `TxId` 및 `AttemptId`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="e5733-180">`TxId`는 특정 트랜잭션을 식별하는 데 사용됩니다. 지정된 트랜잭션이 실패하여 재생되는 경우에는 해당 트랜잭션을 여러 번 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="e5733-181">SCP.NET은 Java 쪽에서 Storm이 수행하는 것처럼 다른 ISCPBatchBolt 개체를 새로 생성하여 각 `StormTxAttempt`을(를) 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="e5733-182">이 디자인을 통해 병렬 트랜잭션 처리가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="e5733-183">사용자는 트랜잭션 시도가 완료되면 해당하는 ISCPBatchBolt 개체는 삭제되며 가비지 수집된다는 점을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="e5733-184">개체 모델</span><span class="sxs-lookup"><span data-stu-id="e5733-184">Object Model</span></span>
<span data-ttu-id="e5733-185">SCP.NET에서는 개발자가 프로그래밍에 사용할 수 있는 주요 개체의 간단한 집합도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="e5733-186">이러한 개체는 **Context**, **StateStore** 및 **SCPRuntime**입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="e5733-187">이 섹션의 나머지 부분에서 각 개체에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="e5733-188">Context</span><span class="sxs-lookup"><span data-stu-id="e5733-188">Context</span></span>
<span data-ttu-id="e5733-189">Context는 응용 프로그램에 실행 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="e5733-190">각 ISCPPlugin 인스턴스(ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt)에는 해당하는 Context 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="e5733-191">Context에서 제공하는 기능은 두 부분, 즉 (1) 전체 C\# 프로세스에서 사용할 수 있는 정적 부분과 (2) 특정 Context 인스턴스에서만 사용할 수 있는 동적 부분으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="e5733-192">정적 부분</span><span class="sxs-lookup"><span data-stu-id="e5733-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="e5733-193">`Logger` 은(는) 기록용으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="e5733-194">`pluginType`은 C\# 프로세스의 플러그 인 유형을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="e5733-195">C\# 프로세스를 Java 없이 로컬 테스트 모드에서 실행하는 경우 플러그 인 유형은 `SCP_NET_LOCAL`입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="e5733-196">`Config` 은(는) Java 쪽에서 구성 매개 변수를 가져오기 위한 용도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="e5733-197">C\# 플러그 인을 초기화할 때 Java 쪽에서 매개 변수가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="e5733-198">`Config` 매개 변수는 `stormConf` 및 `pluginConf`의 두 부분으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="e5733-199">`stormConf`은(는) Storm에서 정의하는 매개 변수이고 `pluginConf`은(는) SCP에서 정의하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="e5733-200">예:</span><span class="sxs-lookup"><span data-stu-id="e5733-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="e5733-201">`TopologyContext` 은(는) 토폴로지 컨텍스트를 가져오기 위한 용도로 제공되며 여러 병렬 처리를 수행하는 구성 요소에 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="e5733-202">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="e5733-203">동적 부분</span><span class="sxs-lookup"><span data-stu-id="e5733-203">Dynamic Part</span></span>
<span data-ttu-id="e5733-204">아래에는 특정 Context 인스턴스와 관련된 인터페이스가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="e5733-205">Context 인스턴스는 SCP.NET 플랫폼에서 작성되어 사용자 코드로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="e5733-206">승인을 지원하는 비트랜잭션 Spout의 경우에는 다음 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="e5733-207">승인을 지원하는 비트랜잭션 Bolt는 수신한 튜플에 대해 명시적으로 `Ack()` 또는 `Fail()`을(를) 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="e5733-208">그리고 새 튜플을 내보낼 때는 새 튜플의 앵커도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="e5733-209">다음과 같은 메서드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="e5733-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="e5733-210">StateStore</span></span>
<span data-ttu-id="e5733-211">`StateStore` 은(는) 메타데이터 서비스, 단조 시퀀스 생성 및 비대기 조정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="e5733-212">`StateStore`을(를) 기반으로 하여 분산 잠금, 분산 큐, 장벽 및 트랜잭션 서비스를 비롯한 높은 수준의 분산형 동시성 추상화를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="e5733-213">SCP 응용 프로그램은 `State` 개체를 사용하여 ZooKeeper에 일부 정보를 영구 보존할 수 있습니다(특히 트랜잭션 토폴로지의 경우).</span><span class="sxs-lookup"><span data-stu-id="e5733-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="e5733-214">따라서 트랜잭션 Spout 작동이 중단되어 다시 시작되는 경우 응용 프로그램이 ZooKeeper에서 필요한 정보를 검색하여 파이프라인을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="e5733-215">`StateStore` 개체는 기본적으로 다음 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="e5733-216">`State` 개체는 기본적으로 다음 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="e5733-217">`Commit()` 메서드의 경우 simpleMode를 true로 설정하면 ZooKeeper에서 해당 ZNode만 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="e5733-218">그렇지 않은 경우에는 현재 ZNode를 삭제하고 COMMITTED\_PATH에 새 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="e5733-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="e5733-219">SCPRuntime</span></span>
<span data-ttu-id="e5733-220">SCPRuntime은 다음의 두 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="e5733-221">`Initialize()` 은(는) SCP 런타임 환경을 초기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="e5733-222">이 메서드에서 C\# 프로세스는 Java 쪽에 연결되며 구성 매개 변수와 토폴로지 컨텍스트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="e5733-223">`LaunchPlugin()`은(는) 메시지 처리 루프를 시작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="e5733-224">이 루프에서 C\# 플러그 인은 Java 쪽에서 메시지(튜플과 제어 신호 포함)를 받은 다음 처리합니다. 이때 사용자 코드에서 제공하는 인터페이스 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="e5733-225">`LaunchPlugin()` 메서드의 입력 매개 변수는 ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 인터페이스를 구현하는 개체를 반환할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="e5733-226">ISCPBatchBolt의 경우 `parms`에서 `StormTxAttempt`을(를) 가져와 해당 시도가 재생된 시도인지를 판단하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="e5733-227">이 작업은 일반적으로 커밋 Bolt에서 수행됩니다. `HelloWorldTx` 예제에서 해당 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="e5733-228">일반적으로 여기서 SCP 플러그 인은 두 가지 모드로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="e5733-229">로컬 테스트 모드: 이 모드에서 SCP 플러그 인(C\# 사용자 코드)은 개발 단계 중에 Visual Studio 내에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="e5733-230">`LocalContext` 을(를) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="e5733-231">일반 모드: 이 모드에서는 Storm Java 프로세스를 통해 SCP 플러그 인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="e5733-232">SCP 플러그 인을 시작하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="e5733-233">토폴로지 사양 언어</span><span class="sxs-lookup"><span data-stu-id="e5733-233">Topology Specification Language</span></span>
<span data-ttu-id="e5733-234">SCP 토폴로지 사양은 SCP 토폴로지를 설명하고 구성하기 위한 도메인별 언어로,</span><span class="sxs-lookup"><span data-stu-id="e5733-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="e5733-235">Storm의 Clojure DSL(<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)을 기반으로 하며 SCP에 의해 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="e5733-236">***runspec*** 명령을 통해 토폴로지 사양을 실행용으로 Storm 클러스터에 직접 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="e5733-237">SCP.NET에는 트랜잭션 토폴로지를 정의하는 다음 함수가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="e5733-238">**새 함수**</span><span class="sxs-lookup"><span data-stu-id="e5733-238">**New Functions**</span></span> | <span data-ttu-id="e5733-239">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="e5733-239">**Parameters**</span></span> | <span data-ttu-id="e5733-240">**설명**</span><span class="sxs-lookup"><span data-stu-id="e5733-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5733-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="e5733-241">**tx-topolopy**</span></span> |<span data-ttu-id="e5733-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="e5733-242">topology-name</span></span><br /><span data-ttu-id="e5733-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="e5733-243">spout-map</span></span><br /><span data-ttu-id="e5733-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="e5733-244">bolt-map</span></span> |<span data-ttu-id="e5733-245">토폴로지 이름, &nbsp;Spout 정의 맵 및 Bolt 정의 맵으로 트랜잭션 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="e5733-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="e5733-246">**scp-tx-spout**</span></span> |<span data-ttu-id="e5733-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="e5733-247">exec-name</span></span><br /><span data-ttu-id="e5733-248">args</span><span class="sxs-lookup"><span data-stu-id="e5733-248">args</span></span><br /><span data-ttu-id="e5733-249">fields</span><span class="sxs-lookup"><span data-stu-id="e5733-249">fields</span></span> |<span data-ttu-id="e5733-250">트랜잭션 Spout를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-250">Define a transactional spout.</span></span> <span data-ttu-id="e5733-251">***args***를 사용하여 ***exec-name***이라는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e5733-252">***fields*** 는 Spout의 출력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="e5733-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="e5733-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="e5733-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="e5733-254">exec-name</span></span><br /><span data-ttu-id="e5733-255">args</span><span class="sxs-lookup"><span data-stu-id="e5733-255">args</span></span><br /><span data-ttu-id="e5733-256">fields</span><span class="sxs-lookup"><span data-stu-id="e5733-256">fields</span></span> |<span data-ttu-id="e5733-257">트랜잭션 Batch Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="e5733-258">***args***를 사용하여 ***exec-name***이라는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="e5733-259">Fields는 Bolt의 출력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="e5733-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="e5733-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="e5733-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="e5733-261">exec-name</span></span><br /><span data-ttu-id="e5733-262">args</span><span class="sxs-lookup"><span data-stu-id="e5733-262">args</span></span><br /><span data-ttu-id="e5733-263">fields</span><span class="sxs-lookup"><span data-stu-id="e5733-263">fields</span></span> |<span data-ttu-id="e5733-264">트랜잭션 Committer Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="e5733-265">***args***를 사용하여 ***exec-name***이라는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e5733-266">***fields*** 는 Bolt의 출력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="e5733-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="e5733-267">**nontx-topolopy**</span></span> |<span data-ttu-id="e5733-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="e5733-268">topology-name</span></span><br /><span data-ttu-id="e5733-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="e5733-269">spout-map</span></span><br /><span data-ttu-id="e5733-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="e5733-270">bolt-map</span></span> |<span data-ttu-id="e5733-271">토폴로지 이름, &nbsp; Spout 정의 맵 및 Bolt 정의 맵으로 비트랜잭션 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="e5733-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="e5733-272">**scp-spout**</span></span> |<span data-ttu-id="e5733-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="e5733-273">exec-name</span></span><br /><span data-ttu-id="e5733-274">args</span><span class="sxs-lookup"><span data-stu-id="e5733-274">args</span></span><br /><span data-ttu-id="e5733-275">fields</span><span class="sxs-lookup"><span data-stu-id="e5733-275">fields</span></span><br /><span data-ttu-id="e5733-276">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e5733-276">parameters</span></span> |<span data-ttu-id="e5733-277">비트랜잭션 Spout를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-277">Define a nontransactional spout.</span></span> <span data-ttu-id="e5733-278">***args***를 사용하여 ***exec-name***이라는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e5733-279">***fields*** 는 Spout의 출력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="e5733-280">***parameters*** 는 선택적 항목으로, "nontransactional.ack.enabled"와 같은 일부 매개 변수를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="e5733-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="e5733-281">**scp-bolt**</span></span> |<span data-ttu-id="e5733-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="e5733-282">exec-name</span></span><br /><span data-ttu-id="e5733-283">args</span><span class="sxs-lookup"><span data-stu-id="e5733-283">args</span></span><br /><span data-ttu-id="e5733-284">fields</span><span class="sxs-lookup"><span data-stu-id="e5733-284">fields</span></span><br /><span data-ttu-id="e5733-285">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e5733-285">parameters</span></span> |<span data-ttu-id="e5733-286">비트랜잭션 Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="e5733-287">***args***를 사용하여 ***exec-name***이라는 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="e5733-288">***fields*** 는 Bolt의 출력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="e5733-289">***parameters*** 는 선택적 항목으로, "nontransactional.ack.enabled"와 같은 일부 매개 변수를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="e5733-290">SCP.NET에서는 다음 키워드가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="e5733-291">**키워드**</span><span class="sxs-lookup"><span data-stu-id="e5733-291">**Key Words**</span></span> | <span data-ttu-id="e5733-292">**설명**</span><span class="sxs-lookup"><span data-stu-id="e5733-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e5733-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="e5733-293">**:name**</span></span> |<span data-ttu-id="e5733-294">토폴로지 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-294">Define the Topology Name</span></span> |
| <span data-ttu-id="e5733-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="e5733-295">**:topology**</span></span> |<span data-ttu-id="e5733-296">위의 함수와 기본 제공 함수를 사용하여 토폴로지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="e5733-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="e5733-297">**:p**</span></span> |<span data-ttu-id="e5733-298">각 Spout 또는 Bolt에 대해 병렬 처리 힌트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="e5733-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="e5733-299">**:config**</span></span> |<span data-ttu-id="e5733-300">구성 매개 변수를 정의하거나 기존 매개 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="e5733-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="e5733-301">**:schema**</span></span> |<span data-ttu-id="e5733-302">스트림의 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="e5733-303">그 외에 자주 사용되는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="e5733-304">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="e5733-304">**Parameter**</span></span> | <span data-ttu-id="e5733-305">**설명**</span><span class="sxs-lookup"><span data-stu-id="e5733-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e5733-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="e5733-306">**"plugin.name"**</span></span> |<span data-ttu-id="e5733-307">C# 플러그 인의 exe 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="e5733-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="e5733-308">**"plugin.args"**</span></span> |<span data-ttu-id="e5733-309">플러그 인 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-309">plugin args</span></span> |
| <span data-ttu-id="e5733-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="e5733-310">**"output.schema"**</span></span> |<span data-ttu-id="e5733-311">출력 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-311">Output schema</span></span> |
| <span data-ttu-id="e5733-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="e5733-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="e5733-313">비트랜잭션 토폴로지에 대해 승인이 사용하도록 설정되는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="e5733-314">runspec 명령은 비트와 함께 배포되며 사용 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="e5733-315">***resource-dir*** 매개 변수는 선택 사항입니다. C\# 응용 프로그램을 연결하려는 경우 이 매개 변수를 지정해야 합니다. 이 디렉터리에는 응용 프로그램, 종속성 및 구성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="e5733-316">***classpath*** 매개 변수도 선택 사항으로,</span><span class="sxs-lookup"><span data-stu-id="e5733-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="e5733-317">사양 파일에 Java Spout 또는 Bolt가 포함되는 경우 Java 클래스 경로를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="e5733-318">기타 기능</span><span class="sxs-lookup"><span data-stu-id="e5733-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="e5733-319">입력 및 출력 스키마 선언</span><span class="sxs-lookup"><span data-stu-id="e5733-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="e5733-320">사용자는 C\# 프로세스에서 튜플을 내보낼 수 있습니다. 플랫폼은 해당 튜플을 byte로 직렬화하고 Java 쪽으로 전송해야 하며, 그러면 Storm에서 이 튜플을 대상으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="e5733-321">그와 동시에 C\# 프로세스는 다운스트림 구성 요소에서 Java 쪽으로부터 튜플을 다시 받아 플랫폼별 원래 형식으로 변환합니다. 이러한 모든 작업은 플랫폼에 의해 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="e5733-322">직렬화와 역직렬화를 지원하려면 사용자 코드가 입력과 출력의 스키마를 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="e5733-323">입력/출력 스트림 스키마는 사전으로 정의되며 키는 StreamId이고 값은 열의 Types입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="e5733-324">구성 요소에서 여러 스트림을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-324">The component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="e5733-325">Context 개체에는 다음 API가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="e5733-326">사용자 코드는 내보낸 튜플이 해당 스트림에 대해 정의된 스키마를 따르는지 확인해야 합니다. 그렇지 않으면 시스템에서 런타임 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="e5733-327">여러 스트림 지원</span><span class="sxs-lookup"><span data-stu-id="e5733-327">Multi-Stream Support</span></span>
<span data-ttu-id="e5733-328">SCP는 사용자 코드가 여러 고유 스트림에서 동시에 내보내기 또는 수신을 수행할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="e5733-329">Emit 메서드가 선택적 스트림 ID 매개 변수를 가져올 때 Context 개체에서 이 지원이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="e5733-330">SCP.NET Context 개체에는 두 개의 메서드가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="e5733-331">이러한 메서드는 StreamId를 지정하기 위해 하나 이상의 튜플을 내보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="e5733-332">StreamId는 C\#과 토폴로지 정의 사양에서 일치해야 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="e5733-333">존재하지 않는 스트림으로 내보내기를 수행하는 경우 런타임 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="e5733-334">필드 그룹화</span><span class="sxs-lookup"><span data-stu-id="e5733-334">Fields Grouping</span></span>
<span data-ttu-id="e5733-335">Strom의 기본 제공 필드 그룹화는 SCP.NET에서 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="e5733-336">Java 프록시 쪽에서는 모든 필드 데이터 형식은 실제로 byte[]이고 필드 그룹화는 byte[] 개체 해시 코드를 사용하여 그룹화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="e5733-337">byte[] 개체 해시 코드는 메모리에서 이 개체의 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="e5733-338">따라서 같은 콘텐츠를 공유하지만 주소는 다른 두 byte[] 개체의 경우 그룹화가 올바르게 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="e5733-339">SCP.NET에는 사용자 지정된 그룹화 메서드가 추가되었습니다. 이 메서드는 byte[]의 콘텐츠를 사용하여 그룹화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="e5733-340">**SPEC** 파일의 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="e5733-341">여기서 각 부분의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-341">Here,</span></span>

1. <span data-ttu-id="e5733-342">"scp-field-group"은 "SCP에서 구현하는 사용자 지정된 필드 그룹화"를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="e5733-343">":tx" 또는 ":non-tx"는 트랜잭션 토폴로지인지 여부를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="e5733-344">트랜잭션 토폴로지와 비트랜잭션 토폴로지에서는 시작 인덱스가 서로 다르기 때문에 이 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="e5733-345">[0,1]은 0부터 시작하는 필드 ID의 해시 집합을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="e5733-346">하이브리드 토폴로지</span><span class="sxs-lookup"><span data-stu-id="e5733-346">Hybrid topology</span></span>
<span data-ttu-id="e5733-347">원시 Storm은 Java로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-347">The native Storm is written in Java.</span></span> <span data-ttu-id="e5733-348">SCP.Net은 고객이 비즈니스 논리를 처리하도록 C\# 코드를 작성할 수 있도록 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="e5733-349">그러나 C\# Spout/Bolt뿐 아니라 Java Spout/Bolt도 포함하는 하이브리드 토폴로지도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="e5733-350">사양 파일에서 Java Spout/Bolt 지정</span><span class="sxs-lookup"><span data-stu-id="e5733-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="e5733-351">사양 파일에서 "scp-spout" 및 "scp-bolt"를 사용하여 Java Spout 및 Bolt를 지정할 수도 있습니다. 해당 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="e5733-352">여기에서 `microsoft.scp.example.HybridTopology.Generator`은(는) Java Spout 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="e5733-353">runSpec 명령에서 Java 클래스 경로 지정</span><span class="sxs-lookup"><span data-stu-id="e5733-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="e5733-354">Java Spout 또는 Bolt를 포함하는 토폴로지를 제출하려면 먼저 Java Spout 또는 Bolt를 컴파일한 다음 Jar 파일을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="e5733-355">그런 후에 토폴로지를 제출할 때 Jar 파일을 포함하는 Java 클래스 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="e5733-356">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="e5733-357">여기서 **examples\\HybridTopology\\java\\target\\**은 Java Spout/Bolt Jar 파일을 포함하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="e5733-358">Java와 C\ 간의 직렬화 및 역직렬화</span><span class="sxs-lookup"><span data-stu-id="e5733-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="e5733-359">SCP 구성 요소는 Java 쪽과 C\# 쪽을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="e5733-360">네이티브 Java Spout/Bolt와 상호 작용을 하기 위해 다음 그래프에서 볼 수 있듯이 Java 쪽과 C\# 쪽 사이에서 직렬화/역직렬화를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Java 구성 요소로 전송하는 SCP 구성 요소로 전송하는 java 구성 요소의 다이어그램](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="e5733-362">**Java 쪽의 직렬화 및 C\# 쪽의 역직렬화**</span><span class="sxs-lookup"><span data-stu-id="e5733-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="e5733-363">먼저 Java 쪽의 직렬화와 C\# 쪽의 역직렬화를 위한 기본 구현이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="e5733-364">Java 쪽의 직렬화 메서드는 SPEC 파일에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="e5733-365">C\# 쪽의 역직렬화 메서드는 C\# 사용자 코드에서 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="e5733-366">데이터 형식이 너무 복잡하지 않으면 이 기본 구현에서 대부분의 경우를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="e5733-367">사용자 데이터 형식이 너무 복잡하거나 기본 구현의 성능이 사용자 요구 사항을 충족하지 않는 등의 특정 경우에는 사용자가 고유한 구현을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="e5733-368">Java 쪽의 직렬화 인터페이스는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="e5733-369">C\# 쪽의 역직렬화 인터페이스는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="e5733-370">공용 인터페이스 ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="e5733-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="e5733-371">**C\# 쪽의 직렬화 및 Java 쪽의 역직렬화**</span><span class="sxs-lookup"><span data-stu-id="e5733-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="e5733-372">C\# 쪽의 직렬화 메서드는 C\# 사용자 코드에서 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="e5733-373">Java 쪽의 역직렬화 메서드는 SPEC 파일에서 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="e5733-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="e5733-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="e5733-375">여기에서 "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer"는 역직렬화의 이름이며 "microsoft.scp.example.HybridTopology.Person"는 데이터가 역직렬화되는 대상 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="e5733-376">사용자는 또한 C\# 직렬화 및 Java 역직렬화의 자체 구현을 플러그 인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="e5733-377">다음은 C\# 직렬화에 대한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="e5733-378">다음은 Java 역직렬화에 대한 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="e5733-379">SCP 호스트 모드</span><span class="sxs-lookup"><span data-stu-id="e5733-379">SCP Host Mode</span></span>
<span data-ttu-id="e5733-380">이 모드에서 사용자는 코드를 DLL로 컴파일한 다음 SCP에서 제공하는 SCPHost.exe를 사용하여 토폴로지를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="e5733-381">사양 파일은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="e5733-382">여기에서 `plugin.name`은(는) SCP SDK에서 제공된 `SCPHost.exe`(으)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="e5733-383">SCPHost.exe는 정확히 3개의 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="e5733-384">첫 번째 매개 변수는 DLL 이름으로, 이 예에서는 `"HelloWorld.dll"` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="e5733-385">두 번째 매개 변수는 Class 이름으로, 이 예에서는 `"Scp.App.HelloWorld.Generator"` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="e5733-386">세 번째 매개 변수는 공용 정적 메서드의 이름으로, ISCPPlugin 인스턴스를 가져오기 위해 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="e5733-387">호스트 모드에서 사용자 코드는 DLL로 컴파일되며 SCP 플랫폼에 의해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="e5733-388">따라서 SCP 플랫폼은 전체 처리 논리를 완전하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="e5733-389">따라서 고객은 SCP 호스트 모드에서 토폴로지를 제출하는 것이 좋습니다. 이렇게 하면 개발 환경을 간소화할 수 있으며 Microsoft가 향후 릴리스에서 유동성을 높이고 이전 버전과의 호환성을 보다 효율적으로 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="e5733-390">SCP 프로그래밍 예제</span><span class="sxs-lookup"><span data-stu-id="e5733-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="e5733-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="e5733-391">HelloWorld</span></span>
<span data-ttu-id="e5733-392">**HelloWorld** 는 SCP.Net의 사용법을 확인할 수 있는 매우 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="e5733-393">여기에는 **generator**라는 Spout와 **splitter** 및 **counter**라는 Bolt 2개가 포함된 비트랜잭션 토폴로지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="e5733-394">**generator** Spout는 일부 문장을 임의로 생성하여 **splitter**로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="e5733-395">**splitter** Bolt는 이러한 문장을 단어로 분할한 다음 **counter** Bolt로 단어를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="e5733-396">"counter" Bolt는 사전을 사용하여 각 단어가 나오는 횟수를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="e5733-397">이 예제에는 **HelloWorld.spec** 및 **HelloWorld\_EnableAck.spec**의 두 가지 사양 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="e5733-398">C\# 코드는 Java 쪽에서 pluginConf를 가져와 승인이 사용되는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="e5733-399">승인이 사용되는 경우 Spout에서 사전을 사용하여 승인되지 않은 튜플을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="e5733-400">Fail()을 호출하면 오류가 발생한 튜플이 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="e5733-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="e5733-401">HelloWorldTx</span></span>
<span data-ttu-id="e5733-402">**HelloWorldTx** 예제에서는 트랜잭션 토폴로지 구현 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="e5733-403">이 예제에는 **generator** Spout, **partial-count** Batch Bolt 및 **count-sum** Commit Bolt가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="e5733-404">또한 미리 작성된 txt 파일 **DataSource0.txt**, **DataSource1.txt** 및 **DataSource2.txt**의 세 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="e5733-405">각 트랜잭션에서 **generator** Spout는 미리 작성된 3개 파일 중 2개를 임의로 선택하여 이 두 파일 이름을 **partial-count** Bolt로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="e5733-406">그러면 **partial-count** Batch Bolt는 먼저 수신된 튜플에서 파일 이름을 가져온 다음 파일을 열고 해당 파일의 단어 수를 계산합니다. 그리고 마지막으로 단어 수를 **count-sum** Bolt로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="e5733-407">**count-sum** Bolt는 총 단어 개수의 요약을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="e5733-408">**정확히 한 번** 의미 체계를 적용하려면 Commit Bolt **count-sum**은 해당 트랜잭션이 재생된 트랜잭션인지 여부를 판단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="e5733-409">이 예제에서는 "count-sum"에 정적 멤버 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="e5733-410">ISCPBatchBolt 인스턴스를 만들면 입력 매개 변수에서 `txAttempt`을(를) 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="e5733-411">`FinishBatch()`을(를) 호출하면 `lastCommittedTxId`이(가) 업데이트됩니다(재생된 트랜잭션이 아닌 경우).</span><span class="sxs-lookup"><span data-stu-id="e5733-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="e5733-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="e5733-412">HybridTopology</span></span>
<span data-ttu-id="e5733-413">이 토폴로지는 Java Spout와 C\# Bolt를 포함하며,</span><span class="sxs-lookup"><span data-stu-id="e5733-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="e5733-414">SCP 플랫폼에서 제공하는 기본 직렬화 및 역직렬화 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="e5733-415">사양 파일 세부 정보는 **examples\\HybridTopology** 폴더의 **HybridTopology.spec**을 참조하고 Java 클래스 경로를 지정하는 방법은 **SubmitTopology.bat**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5733-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="e5733-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="e5733-416">SCPHostDemo</span></span>
<span data-ttu-id="e5733-417">이 예제는 기본적으로 HelloWorld와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="e5733-418">차이점은 사용자 코드가 DLL로 컴파일되며 토폴로지가 SCPHost.exe를 사용하여 제출된다는 것뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e5733-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="e5733-419">자세한 설명은 "SCP 호스트 모드" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5733-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5733-420">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5733-420">Next Steps</span></span>
<span data-ttu-id="e5733-421">SCP를 사용하여 만든 Storm 토폴로지 예제는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5733-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="e5733-422">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="e5733-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="e5733-423">HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="e5733-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="e5733-424">C# Storm 토폴로지에서 여러 데이터 스트림 만들기</span><span class="sxs-lookup"><span data-stu-id="e5733-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="e5733-425">Power BI를 사용하여 Storm 토폴로지에서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="e5733-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="e5733-426">HDInsight의 Storm을 사용하여 이벤트 허브에서 차량 센서 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="e5733-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="e5733-427">Azure 이벤트 허브에서 HBase로 ETL(추출, 변환 및 로드)</span><span class="sxs-lookup"><span data-stu-id="e5733-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="e5733-428">HDInsight에서 Storm 및 HBase를 사용하여 이벤트의 상관 관계 지정</span><span class="sxs-lookup"><span data-stu-id="e5733-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

