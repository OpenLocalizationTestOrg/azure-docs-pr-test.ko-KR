---
title: "aaaSCP.NET 프로그래밍 가이드 | Microsoft Docs"
description: "자세한 내용은 방법 toouse SCP.NET toocreate 합니다. 에 대 한.NET 기반 스톰 토폴로지 HDInsight의 Storm를 사용 합니다."
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
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="57a68-103">SCP 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="57a68-103">SCP programming guide</span></span>
<span data-ttu-id="57a68-104">SCP은 플랫폼 toobuild 실시간으로, 신뢰할 수 있는 일관 되 고 높은 성능 데이터 처리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="57a68-105">맨 위에 구축 [Apache Storm](http://storm.incubator.apache.org/) -스트림 hello OSS 커뮤니티도 설계 된 시스템을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="57a68-106">Nathan Marz가 디자인한 Storm은 Twitter에서 오픈 소스 방식으로 제공되며,</span><span class="sxs-lookup"><span data-stu-id="57a68-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="57a68-107">활용 [Apache 사육](http://zookeeper.apache.org/), 다른 Apache 프로젝트 tooenable 매우 안정적 분산된 조정 및 상태 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="57a68-108">Hello SCP 프로젝트 포팅 Windows에서 Storm 할 뿐만 아니라 hello 프로젝트 확장명 및 사용자 지정 hello Windows 환경에도 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="57a68-109">.NET 개발자 환경 및 라이브러리를 포함 하는 hello 확장, hello 사용자 지정 Windows 기반 배포를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="57a68-110">toofork hello OSS 프로젝트 필요 하지 않습니다 및 파생된 에코 시스템 Storm 기반으로 활용 하 여 수 hello 확장 및 사용자 지정 방식으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="57a68-111">처리 모델</span><span class="sxs-lookup"><span data-stu-id="57a68-111">Processing model</span></span>
<span data-ttu-id="57a68-112">SCP의 hello 데이터 튜플 스트림을 지속적으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="57a68-113">일반적으로 hello 튜플 대기열으로 이동 일부 먼저 다음을 선택 하 고 스톰 토폴로지 내에서 호스팅되는 비즈니스 논리에 의해 변환, 마지막으로 hello 출력 튜플 tooanother SCP 시스템으로 파이프 될 수 없습니다 이나 커밋된 toostores 수 같은 분산된 파일 시스템 또는 데이터베이스 같은 SQL Server입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![피드는 데이터 저장소는 데이터 tooprocessing을 제공 하는 큐의 다이어그램](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="57a68-115">Storm에서는 응용 프로그램 토폴로지에 따라 계산 그래프가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="57a68-116">토폴로지의 각 노드에는 처리 논리가 포함되며 노드 간의 링크는 데이터 흐름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="57a68-117">hello 노드 tooinject 입력된 데이터를 hello 토폴로지 Spouts 사용된 toosequence hello 데이터 될 수 있는 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="57a68-118">hello 입력된 데이터 수에 있는 로그 파일, 트랜잭션 데이터베이스, 시스템 성능 카운터 두 입력 및 출력 데이터 흐름이 사용 하는 등 hello 노드가 볼트 실제 데이터 필터링 hello 수행 하 고 선택 항목 및 집계 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="57a68-119">SCP는 최상의 노력, 최소한 한 번 및 정확히 한 번 방식의 데이터 처리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="57a68-120">분산된 스트리밍 처리 응용 프로그램에서 네트워크 중단, 컴퓨터 오류 또는 사용자 코드 오류 등과 같은 데이터 처리 중 다양한 오류가 발생할 수 있습니다. 최소-한 번에 처리 되도록 모든 데이터를 처리할지 적어도 한 번 자동으로 다시 재생 하 여 동일한 데이터 오류가 발생 하는 경우 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="57a68-121">최소한 한 번 방식의 처리는 간단하고 안정적이며 대부분의 응용 프로그램에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="57a68-122">그러나 hello 응용 프로그램이 정확한 계산을 요구 하는 경우 예를 들어 최소-한 번에 처리 충분 하지 않습니다 hello 동일한 데이터 수 잠재적으로 재생할 수 hello 응용 프로그램 토폴로지에 있으므로.</span><span class="sxs-lookup"><span data-stu-id="57a68-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="57a68-123">이 경우, 정확 하 게-hello 데이터를 재생 하 고 여러 번 처리 될 수 있습니다 하는 경우에 toomake 있는지 hello 결과 올바른 일단 처리 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="57a68-124">SCP 활용 hello 가상 컴퓨터 JVM (Java) hello 커버에서 Storm 기반 하는 동안.NET 개발자 toodevelop 실시간으로 데이터 프로세스 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="57a68-125">hello.NET 및 JVM 로컬 TCP 소켓을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="57a68-126">기본적으로 각 배출구/볼트 hello 사용자 논리.Net 플러그 인 프로세스에서 실행 되는.Net/Java 프로세스 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="57a68-127">toobuild 처리 SCP 기반으로 응용 프로그램 데이터를 여러 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="57a68-128">디자인 하 고 큐에서 데이터의 hello Spouts toopull를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="57a68-129">디자인 및 볼트 tooprocess hello 입력된 데이터를 구현 하 고 데이터베이스 같은 tooexternal 저장소에 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="57a68-130">Hello 토폴로지를 디자인, 전송 및 hello 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="57a68-131">hello 토폴로지 정의 정점 및 hello 데이터 hello 꼭지점 사이의 흐름.</span><span class="sxs-lookup"><span data-stu-id="57a68-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="57a68-132">SCP은 hello 토폴로지 사양 걸리고 Storm 클러스터를 각 꼭 짓 논리 노드 하나에서 실행 되는 위치에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="57a68-133">hello 장애 조치 및 크기 조정 됩니다 처리 hello 스톰 작업 스케줄러입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="57a68-134">이 문서는 방법을 통해 몇 가지 간단한 예 toowalk ´ ֲ SCP toobuild 데이터 처리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="57a68-135">SCP 플러그 인 인터페이스</span><span class="sxs-lookup"><span data-stu-id="57a68-135">SCP Plugin Interface</span></span>
<span data-ttu-id="57a68-136">SCP 플러그 인 (또는 응용 프로그램)는 독립 실행형 Exe 실행할 수 있는 둘 다 Visual Studio 내 hello 개발 단계에서는 프로덕션 환경에서 배포 후 hello 스톰 파이프라인에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="57a68-137">Hello SCP 플러그 인을 작성 다른 표준 Windows 콘솔 응용 프로그램 작성 동일 방금 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="57a68-138">SCP.NET 플랫폼 배출구/모양에 대 한 몇 가지 인터페이스를 선언 하 고 hello 사용자 플러그 인 코드는 이러한 인터페이스를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="57a68-139">이 디자인의 주요 목적은 hello은 해당 hello 사용자는 자신의 비즈니스 logics 고 SCP.NET 플랫폼에서 처리 하는 다른 작업 toobe에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="57a68-140">hello 사용자 플러그 인 코드 hello 다음 인터페이스 중 하나를 구현 해야, hello 토폴로지 트랜잭션 또는 비트랜잭션 인지와 배출구 인지 볼트 hello 구성 요소 인지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="57a68-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="57a68-141">ISCPSpout</span></span>
* <span data-ttu-id="57a68-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="57a68-142">ISCPBolt</span></span>
* <span data-ttu-id="57a68-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="57a68-143">ISCPTxSpout</span></span>
* <span data-ttu-id="57a68-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="57a68-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="57a68-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="57a68-145">ISCPPlugin</span></span>
<span data-ttu-id="57a68-146">ISCPPlugin는 모든 종류의 플러그 인에 대 한 hello 공용 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="57a68-147">현재는 더미 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="57a68-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="57a68-148">ISCPSpout</span></span>
<span data-ttu-id="57a68-149">ISCPSpout는 hello 인터페이스 비트랜잭션 배출구입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="57a68-150">때 `NextTuple()` 호출 hello C\# 사용자 코드에서 하나 이상의 튜플과 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="57a68-151">내용이 없는 경우 tooemit,이 메서드는 아무 것도 표시 하지 않고 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="57a68-152">`NextTuple()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="57a68-153">없는 튜플 tooemit 인 경우 courteous toohave NextTuple 절전 짧은 시간 (예: 10 밀리초)으로 toowaste 하지 않으므로 CPU를 너무 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="57a68-154">`Ack()` 및 `Fail()`은(는) 사양 파일에서 승인 메커니즘이 사용하도록 설정되어 있어야 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="57a68-155">hello `seqId` 했지만 했는지 아니면 실패 했는지를 사용 하는 tooidentify hello 튜플 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="57a68-156">따라서 ack 비트랜잭션 토폴로지에서 활성화 된 경우 emit 함수 다음 hello 배출구에 사용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="57a68-157">Ack 비트랜잭션 토폴로지에서 지원 되지 않는 경우 hello `Ack()` 및 `Fail()` 빈 함수로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="57a68-158">hello `parms` 이러한 함수에 입력된 매개 변수는 똑같이 비어 있는 사전, 나중에 사용 하도록 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="57a68-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="57a68-159">ISCPBolt</span></span>
<span data-ttu-id="57a68-160">ISCPBolt는 hello 인터페이스 비트랜잭션 볼트입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="57a68-161">새 튜플을 사용할 수 있는 hello `Execute()` 함수를 호출할지 tooprocess 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="57a68-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="57a68-162">ISCPTxSpout</span></span>
<span data-ttu-id="57a68-163">ISCPTxSpout는 hello 인터페이스 트랜잭션 배출구입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="57a68-164">해당하는 비트랜잭션 함수와 마찬가지로 `NextTx()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="57a68-165">없는 데이터 tooemit 인 경우에 courteous toohave `NextTx` 절전 모드는 짧은 시간 (10 밀리초) 동안 따라서 하지 toowaste로 CPU를 너무 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="57a68-166">`NextTx()`위에 호출 되는 새 트랜잭션을 toostart hello 매개 변수 `seqId` 에 사용 되는 사용 되는 tooidentify hello 트랜잭션이 `Ack()` 및 `Fail()`합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="57a68-167">`NextTx()`, 사용자 데이터 tooJava 측면을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="57a68-168">hello 데이터 사육 toosupport 재생에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="57a68-169">Hello 용량의 사육 매우 제한적 이기 때문에 사용자만 메타 데이터를 트랜잭션 배출구에 데이터를 대량 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="57a68-170">Storm에서는 트랜잭션이 실패하면 자동으로 재생하므로 일반적인 경우에는 `Fail()` 을(를) 호출하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="57a68-171">SCP 트랜잭션 배출구에서 내보내는 hello 메타 데이터를 확인할 수를 호출할 수 있습니다 하지만 `Fail()` hello 메타 데이터가 유효 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="57a68-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="57a68-172">hello `parms` 이러한 함수에 입력된 매개 변수는 똑같이 비어 있는 사전, 나중에 사용 하도록 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="57a68-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="57a68-173">ISCPBatchBolt</span></span>
<span data-ttu-id="57a68-174">ISCPBatchBolt는 트랜잭션 모양에 대 한 hello 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="57a68-175">`Execute()`새 튜플 hello 볼트에 도착 하는 경우 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="57a68-176">`FinishBatch()` 이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="57a68-177">hello `parms` 입력된 매개 변수는 사용 하도록 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="57a68-178">트랜잭션 토폴로지에는 `StormTxAttempt`(이)라는 중요한 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="57a68-179">두 필드 `TxId` 및 `AttemptId`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="57a68-180">`TxId`tooidentify 사용 되는 특정 트랜잭션에 이며 지정된 된 트랜잭션이 있을 수 여러 시도 hello 트랜잭션이 실패 하 고는 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="57a68-181">SCP.NET 됩니다는 다른 ISCPBatchBolt 개체 tooprocess 각 새로운 `StormTxAttempt`마찬가지로 Java 쪽에서 어떤 스톰 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="57a68-182">hello이이 디자인의 목적은 toosupport 병렬 트랜잭션을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="57a68-183">사용자에에서 보관 해야 유의 해야 하는 트랜잭션 시도가 완료 된 hello 해당 ISCPBatchBolt 개체가 소멸 됩니다 하 고 가비지 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="57a68-184">개체 모델</span><span class="sxs-lookup"><span data-stu-id="57a68-184">Object Model</span></span>
<span data-ttu-id="57a68-185">또한 SCP.NET와 개발자가 tooprogram 키 개체의 간단한 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="57a68-186">이러한 개체는 **Context**, **StateStore** 및 **SCPRuntime**입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="57a68-187">이 섹션의 hello 나머지 부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="57a68-188">Context</span><span class="sxs-lookup"><span data-stu-id="57a68-188">Context</span></span>
<span data-ttu-id="57a68-189">컨텍스트는 실행 중인 환경 toohello 응용 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="57a68-190">각 ISCPPlugin 인스턴스(ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt)에는 해당하는 Context 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="57a68-191">상황에 맞는에서 제공 하는 hello 기능 두 부분으로 나눌 수 있습니다: (1) hello 정적 부분에서 사용할 수 있는 전체 C hello\# 에서만 hello 특정 컨텍스트 인스턴스에 대해 사용할 수 있는 (2) hello 동적 부분을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="57a68-192">정적 부분</span><span class="sxs-lookup"><span data-stu-id="57a68-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="57a68-193">`Logger` 은(는) 기록용으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="57a68-194">`pluginType`가 사용 되는 C hello 유형의 hello 플러그 인 tooindicate\# 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="57a68-195">경우 hello C\# (Java) 없이 로컬 테스트 모드에서 프로세스를 실행 하는 hello 플러그 인 형식은, `SCP_NET_LOCAL`합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="57a68-196">`Config`Java 쪽에서 tooget 구성 매개 변수를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="57a68-197">hello 매개 변수는 Java 로부터 전달 때 C\# 플러그 인 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="57a68-198">hello `Config` 매개 변수는 두 부분으로 나뉘어: `stormConf` 및 `pluginConf`합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="57a68-199">`stormConf`가 정의 된 매개 변수는 및 `pluginConf` SCP에 정의 된 hello 매개 변수는 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="57a68-200">예:</span><span class="sxs-lookup"><span data-stu-id="57a68-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="57a68-201">`TopologyContext`여러 병렬 처리 수준 구성 요소에 대 한 가장 유용 tooget hello 토폴로지 컨텍스트 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="57a68-202">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="57a68-203">동적 부분</span><span class="sxs-lookup"><span data-stu-id="57a68-203">Dynamic Part</span></span>
<span data-ttu-id="57a68-204">인터페이스 다음 hello 관련 tooa 특정 컨텍스트 인스턴스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="57a68-205">hello 컨텍스트 인스턴스가 SCP.NET 플랫폼에서 만들고 toohello 사용자 코드를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="57a68-206">Ack를 지 원하는 비트랜잭션 배출구에 대 한 메서드를 다음 hello 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="57a68-207">Ack를 지 원하는 비트랜잭션 볼트에 대 한 기본 프린터를 사용할지 명시적으로 `Ack()` 또는 `Fail()` hello 튜플 개 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="57a68-208">및 새 튜플을 내보낼 때 hello 새 튜플의 hello 앵커 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="57a68-209">메서드를 다음 hello 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="57a68-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="57a68-210">StateStore</span></span>
<span data-ttu-id="57a68-211">`StateStore` 은(는) 메타데이터 서비스, 단조 시퀀스 생성 및 비대기 조정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="57a68-212">`StateStore`을(를) 기반으로 하여 분산 잠금, 분산 큐, 장벽 및 트랜잭션 서비스를 비롯한 높은 수준의 분산형 동시성 추상화를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="57a68-213">SCP 응용 프로그램 수 hello를 사용 하 여 `State` toopersist 트랜잭션 토폴로지를 위해 특별히 사육의 일부 정보 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="57a68-214">충돌 하 고 다시 시작 하는 트랜잭션 배출구, 사육에서 hello 필요한 정보를 검색 하 고 hello 파이프라인 다시 시작 수 있도록 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="57a68-215">hello `StateStore` 개체에는 이러한 메서드가 주로:</span><span class="sxs-lookup"><span data-stu-id="57a68-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
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
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="57a68-216">hello `State` 개체에는 이러한 메서드가 주로:</span><span class="sxs-lookup"><span data-stu-id="57a68-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="57a68-217">Hello에 대 한 `Commit()` 메서드 simpleMode tootrue 설정 된 경우, 단순히 삭제 됩니다 hello ZNode 사육에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="57a68-218">그렇지 않으면 삭제 됩니다 커밋됨 hello에 새 노드를 추가 하 고 현재 ZNode hello\_경로입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="57a68-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="57a68-219">SCPRuntime</span></span>
<span data-ttu-id="57a68-220">SCPRuntime hello 다음 두 가지 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="57a68-221">`Initialize()`사용 되는 tooinitialize hello SCP 런타임 환경이입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="57a68-222">이 방법에서는 C hello\# 프로세스 toohello Java 쪽 및 가져옵니다 구성 매개 변수 및 토폴로지 컨텍스트 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="57a68-223">`LaunchPlugin()`사용 되는 tookick hello 메시지 처리 루프 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="57a68-224">이 루프에서 C hello\# hello 메시지 처리, hello 인터페이스 메서드를 호출 하는 아마도 hello 사용자 코드에 의해 제공 되는 다음와 플러그 인에는 메시지 양식 Java 쪽 (튜플 및 제어 신호 포함)를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="57a68-225">메서드에 대 한 입력된 매개 변수 hello `LaunchPlugin()` ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 인터페이스를 구현 하는 개체를 반환할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="57a68-226">얻을 수 ISCPBatchBolt에 대 한 `StormTxAttempt` 에서 `parms`, 재생된 시도 인지 toojudge을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="57a68-227">이 일반적으로 hello 커밋 볼트에서 수행 되 고 hello에 설명 된 `HelloWorldTx` 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="57a68-228">일반적으로 여기에 두 가지 모드 hello SCP 플러그 인 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="57a68-229">로컬 테스트 모드:이 모드에서는 hello SCP 플러그 인 (C hello\# 사용자 코드) hello 개발 단계 중에 Visual Studio 내에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="57a68-230">`LocalContext`메서드 tooserialize 내보내는 hello 튜플 toolocal 파일 및 toomemory 다시 읽기를 제공 하는이 모드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="57a68-231">일반 모드:이 모드에서 SCP 플러그 인 hello 스톰 java 프로세스에 의해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="57a68-232">SCP 플러그 인을 시작하는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="57a68-233">토폴로지 사양 언어</span><span class="sxs-lookup"><span data-stu-id="57a68-233">Topology Specification Language</span></span>
<span data-ttu-id="57a68-234">SCP 토폴로지 사양은 SCP 토폴로지를 설명하고 구성하기 위한 도메인별 언어로,</span><span class="sxs-lookup"><span data-stu-id="57a68-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="57a68-235">Storm의 Clojure DSL(<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)을 기반으로 하며 SCP에 의해 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="57a68-236">토폴로지 사양 toostorm hello를 통해 실행에 대 한 클러스터 직접 전송할 수 ***runspec*** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="57a68-237">SCP.NET 수행 함수 toodefine hello 트랜잭션 토폴로지를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="57a68-238">**새 함수**</span><span class="sxs-lookup"><span data-stu-id="57a68-238">**New Functions**</span></span> | <span data-ttu-id="57a68-239">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="57a68-239">**Parameters**</span></span> | <span data-ttu-id="57a68-240">**설명**</span><span class="sxs-lookup"><span data-stu-id="57a68-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="57a68-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="57a68-241">**tx-topolopy**</span></span> |<span data-ttu-id="57a68-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="57a68-242">topology-name</span></span><br /><span data-ttu-id="57a68-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="57a68-243">spout-map</span></span><br /><span data-ttu-id="57a68-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="57a68-244">bolt-map</span></span> |<span data-ttu-id="57a68-245">Hello 토폴로지 이름의 트랜잭션 토폴로지 정의 &nbsp;정의 맵과 hello 볼트 정의 맵이 spouts</span><span class="sxs-lookup"><span data-stu-id="57a68-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="57a68-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="57a68-246">**scp-tx-spout**</span></span> |<span data-ttu-id="57a68-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="57a68-247">exec-name</span></span><br /><span data-ttu-id="57a68-248">args</span><span class="sxs-lookup"><span data-stu-id="57a68-248">args</span></span><br /><span data-ttu-id="57a68-249">fields</span><span class="sxs-lookup"><span data-stu-id="57a68-249">fields</span></span> |<span data-ttu-id="57a68-250">트랜잭션 Spout를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-250">Define a transactional spout.</span></span> <span data-ttu-id="57a68-251">Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="57a68-252">hello ***필드*** 배출구에 대 한 hello 출력 필드는</span><span class="sxs-lookup"><span data-stu-id="57a68-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="57a68-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="57a68-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="57a68-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="57a68-254">exec-name</span></span><br /><span data-ttu-id="57a68-255">args</span><span class="sxs-lookup"><span data-stu-id="57a68-255">args</span></span><br /><span data-ttu-id="57a68-256">fields</span><span class="sxs-lookup"><span data-stu-id="57a68-256">fields</span></span> |<span data-ttu-id="57a68-257">트랜잭션 Batch Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="57a68-258">Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args입니다.***</span><span class="sxs-lookup"><span data-stu-id="57a68-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="57a68-259">hello 필드는 hello 출력 필드에 대 한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="57a68-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="57a68-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="57a68-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="57a68-261">exec-name</span></span><br /><span data-ttu-id="57a68-262">args</span><span class="sxs-lookup"><span data-stu-id="57a68-262">args</span></span><br /><span data-ttu-id="57a68-263">fields</span><span class="sxs-lookup"><span data-stu-id="57a68-263">fields</span></span> |<span data-ttu-id="57a68-264">트랜잭션 Committer Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="57a68-265">Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="57a68-266">hello ***필드*** 모양에 대 한 hello 출력 필드는</span><span class="sxs-lookup"><span data-stu-id="57a68-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="57a68-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="57a68-267">**nontx-topolopy**</span></span> |<span data-ttu-id="57a68-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="57a68-268">topology-name</span></span><br /><span data-ttu-id="57a68-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="57a68-269">spout-map</span></span><br /><span data-ttu-id="57a68-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="57a68-270">bolt-map</span></span> |<span data-ttu-id="57a68-271">Hello 토폴로지 이름의 비트랜잭션 토폴로지 정의&nbsp; 정의 맵과 hello 볼트 정의 맵이 spouts</span><span class="sxs-lookup"><span data-stu-id="57a68-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="57a68-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="57a68-272">**scp-spout**</span></span> |<span data-ttu-id="57a68-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="57a68-273">exec-name</span></span><br /><span data-ttu-id="57a68-274">args</span><span class="sxs-lookup"><span data-stu-id="57a68-274">args</span></span><br /><span data-ttu-id="57a68-275">fields</span><span class="sxs-lookup"><span data-stu-id="57a68-275">fields</span></span><br /><span data-ttu-id="57a68-276">매개 변수</span><span class="sxs-lookup"><span data-stu-id="57a68-276">parameters</span></span> |<span data-ttu-id="57a68-277">비트랜잭션 Spout를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-277">Define a nontransactional spout.</span></span> <span data-ttu-id="57a68-278">Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="57a68-279">hello ***필드*** 배출구에 대 한 hello 출력 필드는</span><span class="sxs-lookup"><span data-stu-id="57a68-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="57a68-280">hello ***매개 변수*** 선택적 toospecify 사용 하는 "nontransactional.ack.enabled" 등의 일부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="57a68-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="57a68-281">**scp-bolt**</span></span> |<span data-ttu-id="57a68-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="57a68-282">exec-name</span></span><br /><span data-ttu-id="57a68-283">args</span><span class="sxs-lookup"><span data-stu-id="57a68-283">args</span></span><br /><span data-ttu-id="57a68-284">fields</span><span class="sxs-lookup"><span data-stu-id="57a68-284">fields</span></span><br /><span data-ttu-id="57a68-285">매개 변수</span><span class="sxs-lookup"><span data-stu-id="57a68-285">parameters</span></span> |<span data-ttu-id="57a68-286">비트랜잭션 Bolt를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="57a68-287">Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="57a68-288">hello ***필드*** 모양에 대 한 hello 출력 필드는</span><span class="sxs-lookup"><span data-stu-id="57a68-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="57a68-289">hello ***매개 변수*** 선택적 toospecify 사용 하는 "nontransactional.ack.enabled" 등의 일부 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="57a68-290">SCP.NET에서는 다음 키워드가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="57a68-291">**키워드**</span><span class="sxs-lookup"><span data-stu-id="57a68-291">**Key Words**</span></span> | <span data-ttu-id="57a68-292">**설명**</span><span class="sxs-lookup"><span data-stu-id="57a68-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="57a68-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="57a68-293">**:name**</span></span> |<span data-ttu-id="57a68-294">Hello 토폴로지 이름 정의</span><span class="sxs-lookup"><span data-stu-id="57a68-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="57a68-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="57a68-295">**:topology**</span></span> |<span data-ttu-id="57a68-296">정의 함수에 위에 hello를 사용 하 여 토폴로지를 hello 및 스토리에서 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="57a68-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="57a68-297">**:p**</span></span> |<span data-ttu-id="57a68-298">각 배출구 또는 번개 hello 병렬 처리 수준 힌트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="57a68-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="57a68-299">**:config**</span></span> |<span data-ttu-id="57a68-300">정의 업데이트 기존 hello 또는 매개 변수 구성</span><span class="sxs-lookup"><span data-stu-id="57a68-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="57a68-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="57a68-301">**:schema**</span></span> |<span data-ttu-id="57a68-302">Hello 스트림 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="57a68-303">그 외에 자주 사용되는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="57a68-304">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="57a68-304">**Parameter**</span></span> | <span data-ttu-id="57a68-305">**설명**</span><span class="sxs-lookup"><span data-stu-id="57a68-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="57a68-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="57a68-306">**"plugin.name"**</span></span> |<span data-ttu-id="57a68-307">hello C# 플러그 인의 exe 파일 이름</span><span class="sxs-lookup"><span data-stu-id="57a68-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="57a68-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="57a68-308">**"plugin.args"**</span></span> |<span data-ttu-id="57a68-309">플러그 인 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-309">plugin args</span></span> |
| <span data-ttu-id="57a68-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="57a68-310">**"output.schema"**</span></span> |<span data-ttu-id="57a68-311">출력 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-311">Output schema</span></span> |
| <span data-ttu-id="57a68-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="57a68-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="57a68-313">비트랜잭션 토폴로지에 대해 승인이 사용하도록 설정되는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="57a68-314">hello runspec 명령 hello 비트와 함께 배포 될, hello 사용과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="57a68-315">hello ***리소스-dir*** 매개 변수는 선택적, toospecify 필요한 tooplug C를 원하는 경우\# 응용 프로그램, 그리고이 디렉터리는 hello 응용 프로그램, hello 종속성 및 구성을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="57a68-316">hello ***classpath*** 도 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="57a68-317">Java Spout 또는 번개 hello 사양 파일을 포함 하는 경우 사용 되는 toospecify hello Java classpath입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="57a68-318">기타 기능</span><span class="sxs-lookup"><span data-stu-id="57a68-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="57a68-319">입력 및 출력 스키마 선언</span><span class="sxs-lookup"><span data-stu-id="57a68-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="57a68-320">hello 사용자 c에서 튜플을 내보낼 수\# 처리 하 고, hello 플랫폼 요구 사항을 tooserialize hello 튜플 byte, 전송 tooJava 쪽 스톰이 튜플 toohello 대상으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="57a68-321">한편 다운스트림 구성 요소에서 C hello\# 프로세스 java 로부터 튜플을 수신 하 고 플랫폼별 toohello 원래 형식을 변환,이 작업은 모두 hello 플랫폼으로 숨겨져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="57a68-322">toosupport hello serialization 및 deserialization toodeclare hello 스키마 hello 입력 및 출력의 사용자 코드에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="57a68-323">hello 입/출력 스트림 스키마 hello 키가 사전으로 정의 hello StreamId 고 hello 값은 hello 유형의 hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="57a68-324">hello 구성 요소에는 선언 된 다중 스트림이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="57a68-325">컨텍스트 개체에 hello 다음 API를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="57a68-326">사용자 코드는 해당 스트림에 대해 정의 된 hello 스키마를 준수 하는 내보내는 hello 튜플 또는 hello 시스템은 런타임 예외를 throw 하는 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="57a68-327">여러 스트림 지원</span><span class="sxs-lookup"><span data-stu-id="57a68-327">Multi-Stream Support</span></span>
<span data-ttu-id="57a68-328">SCP 지원 사용자 tooemit 코드 또는 hello에 여러 가지 스트림에서 동일 수신 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="57a68-329">선택적 스트림 ID 매개 변수를 사용 하는 hello Emit 메서드 hello 지원 hello 컨텍스트 개체의 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="57a68-330">두 가지 방법 hello SCP.NET 컨텍스트 개체에에서 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="57a68-331">사용 되는 tooemit 튜플 또는 튜플 toospecify StreamId 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="57a68-332">hello StreamId는 문자열이 고 toobe 모두 C에서 일관성이 필요한\# 토폴로지 정의 사양 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="57a68-333">내보내는 tooa 존재 하지 않는 스트림에 hello 런타임 예외를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="57a68-334">필드 그룹화</span><span class="sxs-lookup"><span data-stu-id="57a68-334">Fields Grouping</span></span>
<span data-ttu-id="57a68-335">hello SCP.NET에 기본 제공 필드에에서 그룹화가 Strom 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="57a68-336">Java 프록시 쪽 hello, 모든 hello 필드 데이터 형식이 실제로 byte, 않으며 hello 바이트 개체 해시 코드 tooperform hello 그룹을 사용 하 여 hello 필드를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="57a68-337">hello 바이트 개체 해시 코드는 메모리에서이 개체의 hello 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="57a68-338">Hello 그룹화 2 바이트에 대 한 잘못 된 되도록 해당 공유 hello 콘텐츠 동일 하지만 같은 주소 하지 hello 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="57a68-339">SCP.NET 사용자 지정된 그룹화 메서드를 추가 하 고 hello 바이트 toodo hello 그룹화의 hello 콘텐츠를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="57a68-340">**사양** 파일 처럼은 hello 구문:</span><span class="sxs-lookup"><span data-stu-id="57a68-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="57a68-341">여기서 각 부분의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-341">Here,</span></span>

1. <span data-ttu-id="57a68-342">"scp-field-group"은 "SCP에서 구현하는 사용자 지정된 필드 그룹화"를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="57a68-343">":tx" 또는 ":non-tx"는 트랜잭션 토폴로지인지 여부를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="57a68-344">시작 인덱스 hello tx가 아닌 토폴로지 및 다른 tx 이므로이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="57a68-345">[0,1]은 0부터 시작하는 필드 ID의 해시 집합을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="57a68-346">하이브리드 토폴로지</span><span class="sxs-lookup"><span data-stu-id="57a68-346">Hybrid topology</span></span>
<span data-ttu-id="57a68-347">Java로 작성 된 네이티브 스톰 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="57a68-348">SCP.Net가 향상 것 tooenable 및이 사용자 지정 toowrite C\# toohandle 해당 비즈니스 논리를 코딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="57a68-349">그러나 C\# Spout/Bolt뿐 아니라 Java Spout/Bolt도 포함하는 하이브리드 토폴로지도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="57a68-350">사양 파일에서 Java Spout/Bolt 지정</span><span class="sxs-lookup"><span data-stu-id="57a68-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="57a68-351">사양 파일에 사용 되는 toospecify Java Spouts 및 볼트 "scp 배출구" 및 "scp 볼트" 일 수도 있습니다, 그리고 예를 들면 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="57a68-352">여기 `microsoft.scp.example.HybridTopology.Generator` hello hello Java Spout 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="57a68-353">runSpec 명령에서 Java 클래스 경로 지정</span><span class="sxs-lookup"><span data-stu-id="57a68-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="57a68-354">Java Spouts 또는 볼트 포함 된 toosubmit 토폴로지를 원하는 경우 Java Spouts toofirst 컴파일 hello 또는 볼트 필요 하 고 hello Jar 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="57a68-355">토폴로지를 전송할 때 hello Jar 파일을 포함 하는 hello java 클래스 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="57a68-356">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="57a68-357">여기 **예제\\HybridTopology\\java\\대상\\**  hello Java 배출구/볼트 Jar 파일 있는 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="57a68-358">Java와 C\ 간의 직렬화 및 역직렬화</span><span class="sxs-lookup"><span data-stu-id="57a68-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="57a68-359">SCP 구성 요소는 Java 쪽과 C\# 쪽을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="57a68-360">순서 toointeract 네이티브 Java Spouts/볼트와에서 Serialization/Deserialization를 수행 해야 Java 쪽와 C 간의\# hello 다음 그래프에에서 나타난 것 처럼 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![tooJava 구성 요소를 보내는 tooSCP 구성 요소를 보내는 java 구성 요소 다이어그램](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="57a68-362">**Java 쪽의 직렬화 및 C\# 쪽의 역직렬화**</span><span class="sxs-lookup"><span data-stu-id="57a68-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="57a68-363">먼저 Java 쪽의 직렬화와 C\# 쪽의 역직렬화를 위한 기본 구현이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="57a68-364">Java 쪽의 hello 직렬화 메서드 사양 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="57a68-365">C에서 deserialization 메서드 hello\# C 쪽으로 지정 해야\# 사용자 코드:</span><span class="sxs-lookup"><span data-stu-id="57a68-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="57a68-366">Hello 데이터 형식이 너무 복잡 합니다. 아닌 경우이 기본 구현은 대부분의 경우를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="57a68-367">특정 한 경우에 대 한 하거나 hello 사용자 데이터 형식이 너무 복잡 하기 때문에 또는 hello 성능 기본 구현에 맞지 않으므로 hello 사용자의 요구 사항, 사용자 수 있는 플러그 인 고유한 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="57a68-368">hello 직렬화 인터페이스 java 쪽으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="57a68-369">hello deserialize c에서 인터페이스\# 쪽으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="57a68-370">공용 인터페이스 ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="57a68-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="57a68-371">**C\# 쪽의 직렬화 및 Java 쪽의 역직렬화**</span><span class="sxs-lookup"><span data-stu-id="57a68-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="57a68-372">C의 직렬화 메서드 hello\# C 쪽으로 지정 해야\# 사용자 코드:</span><span class="sxs-lookup"><span data-stu-id="57a68-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="57a68-373">hello Java 쪽에 Deserialization 메서드 사양 파일에 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="57a68-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="57a68-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="57a68-375">여기 "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" 역직렬 변환기의 hello 이름 이므로 "microsoft.scp.example.HybridTopology.Person" hello 대상 클래스 hello 데이터를 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="57a68-376">사용자는 또한 C\# 직렬화 및 Java 역직렬화의 자체 구현을 플러그 인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="57a68-377">이 C에 대 한 hello 인터페이스\# serializer.</span><span class="sxs-lookup"><span data-stu-id="57a68-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="57a68-378">다음은 Java 역직렬 변환기에 대 한 hello 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="57a68-379">SCP 호스트 모드</span><span class="sxs-lookup"><span data-stu-id="57a68-379">SCP Host Mode</span></span>
<span data-ttu-id="57a68-380">이 모드에서는 사용자 자신의 코드 tooDLL 컴파일를 SCPHost.exe SCP toosubmit 토폴로지에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="57a68-381">hello 사양 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="57a68-382">여기에서 `plugin.name`은(는) SCP SDK에서 제공된 `SCPHost.exe`(으)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="57a68-383">SCPHost.exe는 정확히 3개의 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="57a68-384">hello 먼저 하나는 hello DLL 이름이 며, `"HelloWorld.dll"` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="57a68-385">hello 두 번째 메서드는 hello 클래스 이름이 며, `"Scp.App.HelloWorld.Generator"` 이 예에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="57a68-386">hello 셋째 하나 hello의 이름인 호출 된 tooget ISCPPlugin의 인스턴스 수 있는 공용 정적 메서드의 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="57a68-387">호스트 모드에서 사용자 코드는 DLL로 컴파일되며 SCP 플랫폼에 의해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="57a68-388">따라서 SCP 플랫폼 hello 전체 처리 논리의 모든 권한을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="57a68-389">따라서 고객 toosubmit 토폴로지가 권장 SCP 호스트 모드에서 hello 개발 환경을 단순화 하 고 이후 릴리스도에 대 한 더 많은 유연성 및 이전 버전과 호환성을 더 잘 너는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="57a68-390">SCP 프로그래밍 예제</span><span class="sxs-lookup"><span data-stu-id="57a68-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="57a68-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="57a68-391">HelloWorld</span></span>
<span data-ttu-id="57a68-392">**HelloWorld** 아주 간단한 예제 tooshow SCP.Net 맛은 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="57a68-393">여기에는 **generator**라는 Spout와 **splitter** 및 **counter**라는 Bolt 2개가 포함된 비트랜잭션 토폴로지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="57a68-394">hello 배출구 **생성기** 임의로 일부 문장을 생성 하 고 이러한 문장 너무 내보낼 됩니다**분할자**합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="57a68-395">hello 볼트 **분할자** hello 문장 toowords 분할 되며 이러한 단어를 너무 내보낼**카운터** 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="57a68-396">hello 볼트 "counter" 각 단어의 사전 toorecord hello 발생 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="57a68-397">이 예제에는 **HelloWorld.spec** 및 **HelloWorld\_EnableAck.spec**의 두 가지 사양 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="57a68-398">Hello C에서에서\# 코드 것 알아볼 수 hello pluginConf Java 쪽에서 가져와서 ack 활성화 되어 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="57a68-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="57a68-399">사전은 ack를 사용 하는 hello 배출구에 사용 되는 toocache hello 튜플 했지만 되지 않은입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="57a68-400">Fail() 호출 되 면 hello 실패 한 튜플 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="57a68-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="57a68-401">HelloWorldTx</span></span>
<span data-ttu-id="57a68-402">hello **HelloWorldTx** 예제 방법을 tooimplement 트랜잭션 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="57a68-403">이 예제에는 **generator** Spout, **partial-count** Batch Bolt 및 **count-sum** Commit Bolt가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="57a68-404">또한 미리 작성된 txt 파일 **DataSource0.txt**, **DataSource1.txt** 및 **DataSource2.txt**의 세 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="57a68-405">각 트랜잭션에서 배출구 hello **생성기** 임의로 3 개의 파일을 만들어 놓아야 hello에서 두 개의 파일을 선택 하 고 hello 두 파일 이름을 toohello 내보내는 됩니다 **부분 개수** 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="57a68-406">hello 볼트 **부분-c o u** 는 먼저 hello 파일 이름을 받은 hello 튜플 열려 hello 파일 및 count hello 단어 수에서이 파일에서 가져오고 hello 단어 번호 toohello 마지막으로 내보내기 **개수-sum**볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="57a68-407">hello **count sum** 볼트 hello 총 수를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="57a68-408">tooachieve **정확히 한 번만** 의미 체계, hello 커밋 볼트 **count sum** 재생된 트랜잭션 인지 toojudge 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="57a68-409">이 예제에서는 "count-sum"에 정적 멤버 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="57a68-410">Hello ISCPBatchBolt 인스턴스를 만들 때 가져올 `txAttempt` 입력된 매개 변수에서:</span><span class="sxs-lookup"><span data-stu-id="57a68-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
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

<span data-ttu-id="57a68-411">때 `FinishBatch()` 호출 hello `lastCommittedTxId` 재생 된 트랜잭션이 면 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="57a68-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="57a68-412">HybridTopology</span></span>
<span data-ttu-id="57a68-413">이 토폴로지는 Java Spout와 C\# Bolt를 포함하며,</span><span class="sxs-lookup"><span data-stu-id="57a68-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="57a68-414">Hello 기본 serialization 및 deserialization 구현 SCP 플랫폼에서 제공을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="57a68-415">Ref hello 하세요 **HybridTopology.spec** 에 **예제\\HybridTopology** hello 사양 파일 세부 정보에 대 한 폴더 및 **SubmitTopology.bat** 방법에 대 한 toospecify Java classpath 합니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="57a68-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="57a68-416">SCPHostDemo</span></span>
<span data-ttu-id="57a68-417">이 예에서는 기본적으로 HelloWorld 동일 hello.</span><span class="sxs-lookup"><span data-stu-id="57a68-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="57a68-418">hello만 클래스 간의 차이점은 hello 사용자 코드를 DLL로 컴파일될 hello 토폴로지 SCPHost.exe를 사용 하 여 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57a68-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="57a68-419">Ref hello "SCP 호스트 모드" 섹션에 대 한 자세한 설명은 하세요.</span><span class="sxs-lookup"><span data-stu-id="57a68-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57a68-420">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57a68-420">Next Steps</span></span>
<span data-ttu-id="57a68-421">SCP를 사용 하 여 만든 스톰 토폴로지 예 hello 다음 참조.</span><span class="sxs-lookup"><span data-stu-id="57a68-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="57a68-422">Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="57a68-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="57a68-423">HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="57a68-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="57a68-424">C# Storm 토폴로지에서 여러 데이터 스트림 만들기</span><span class="sxs-lookup"><span data-stu-id="57a68-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="57a68-425">Power Bi toovisualize 데이터 스톰 토폴로지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="57a68-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="57a68-426">HDInsight의 Storm을 사용하여 이벤트 허브에서 차량 센서 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="57a68-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="57a68-427">추출, 변환 및 로드 (ETL) tooHBase Azure 이벤트 허브에서</span><span class="sxs-lookup"><span data-stu-id="57a68-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="57a68-428">HDInsight에서 Storm 및 HBase를 사용하여 이벤트의 상관 관계 지정</span><span class="sxs-lookup"><span data-stu-id="57a68-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

