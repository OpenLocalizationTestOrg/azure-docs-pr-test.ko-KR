---
title: "HDInsight에서 Storm 및 HBase를 사용하여 시간 별로 이벤트의 상관 관계 지정"
description: "HDInsight에서 Storm 및 HBase를 사용함으로써 다른 시간에 도착하는 이벤트의 상관관계를 지정하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="cb32e-103">Storm 및 HBase를 사용하여 다른 시간에 도착하는 이벤트의 상관 관계 지정</span><span class="sxs-lookup"><span data-stu-id="cb32e-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="cb32e-104">Apache Storm으로 영구적인 데이터 저장소를 사용하여 다른 시간에 도착하는 데이터 항목의 상관 관계를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="cb32e-105">예를 들어, 사용자 세션에 대한 로그인 및 로그아웃 이벤트를 연결하여 세션이 얼마나 지속되었는지 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="cb32e-106">이 문서에서는 사용자 세션에 대한 로그인 및 로그아웃 이벤트를 추적하는 기본 C# Storm 토폴로지를 만드는 방법을 배우고 세션의 지속 시간을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="cb32e-107">토폴로지는 영구 데이터 저장소로 HBase를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="cb32e-108">HBase는 또한 기록 데이터에 대해 배치 쿼리를 실행하여 추가적인 정보를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="cb32e-109">예를 들면 특정 기간에 얼마나 많은 사용자 세션이 시작 또는 종료했는지와 같은 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb32e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cb32e-110">Prerequisites</span></span>

* <span data-ttu-id="cb32e-111">Visual Studio 및 Visual Studio용 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="cb32e-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="cb32e-112">자세한 내용은 [Visual Studio용 HDInsight 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb32e-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="cb32e-113">HDInsight 클러스터의 Apache Storm(Windows 기반).</span><span class="sxs-lookup"><span data-stu-id="cb32e-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="cb32e-114">2016년 10월 28일 이후 생성된 Linux 기반 Storm 클러스터에서는 SCP.NET 토폴로지가 지원되지만 2016년 10월 28일 기준으로 사용 가능한 HBase SDK for .NET 패키지는 Linux 기반 HDInsight에서 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="cb32e-115">HDInsight 클러스터에서 Apache HBase(Linux 또는 Windows 기반)</span><span class="sxs-lookup"><span data-stu-id="cb32e-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cb32e-116">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cb32e-117">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb32e-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="cb32e-118">개발 환경에서 [Java](https://java.com) 1,7 이상 -</span><span class="sxs-lookup"><span data-stu-id="cb32e-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="cb32e-119">Java는 HDInsight 클러스터에 제출될 때 토폴로지를 패키징하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="cb32e-120">**JAVA_HOME** 환경 변수가 Java를 포함하고 있는 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="cb32e-121">**%JAVA_HOME%/bin** 디렉터리가 경로에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="cb32e-122">아키텍처</span><span class="sxs-lookup"><span data-stu-id="cb32e-122">Architecture</span></span>

![토폴로지를 통한 데이터 흐름 다이어그램](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="cb32e-124">이벤트의 상관 관계를 지정하려면 이벤트 원본에 대한 공통 식별자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="cb32e-125">예를 들어 사용자 ID, 세션 ID 또는 a) 고유하고 b) 스톰으로 전송된 모든 데이터에 포함된 데이터의 다른 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="cb32e-126">이 예제는 GUID 값을 사용하여 세션 ID를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="cb32e-127">이 예제는 다음 두 개의 HDInsight 클러스터로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="cb32e-128">HBase: 기록 데이터에 대한 영구 데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="cb32e-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="cb32e-129">Storm: 들어오는 데이터를 수집하는 데 사용</span><span class="sxs-lookup"><span data-stu-id="cb32e-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="cb32e-130">데이터는 Storm 토폴로지에 의해 임의로 생성되고 다음 항목으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="cb32e-131">세션 ID: 각 세션을 고유하게 식별하는 GUID</span><span class="sxs-lookup"><span data-stu-id="cb32e-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="cb32e-132">이벤트: 이벤트 시작(START) 또는 종료(END)</span><span class="sxs-lookup"><span data-stu-id="cb32e-132">Event: a START or END event.</span></span> <span data-ttu-id="cb32e-133">이 예에서는 START가 항상 END 전에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="cb32e-134">시간: 이벤트의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-134">Time: the time of the event.</span></span>

<span data-ttu-id="cb32e-135">이 데이터는 HBase에서 처리 및 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="cb32e-136">Storm 토폴로지</span><span class="sxs-lookup"><span data-stu-id="cb32e-136">Storm topology</span></span>

<span data-ttu-id="cb32e-137">세션이 시작되면 **START** 이벤트가 토폴로지에서 수신되고 HBase에 로그됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="cb32e-138">**END** 이벤트가 수신되면 토폴로지가 **START** 이벤트를 검색하며 두 이벤트 사이에서 시간을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="cb32e-139">그 다음 이 **기간** 값이 **END** 이벤트 정보와 함께 HBase에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb32e-140">이 토폴로지는 기본 패턴을 보여주며 프로덕션 솔루션은 다음과 같은 시나리오에 대한 디자인을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="cb32e-141">이벤트가 잘못된 순서로 도착</span><span class="sxs-lookup"><span data-stu-id="cb32e-141">Events arriving out of order</span></span>
> * <span data-ttu-id="cb32e-142">중복된 이벤트</span><span class="sxs-lookup"><span data-stu-id="cb32e-142">Duplicate events</span></span>
> * <span data-ttu-id="cb32e-143">삭제된 이벤트</span><span class="sxs-lookup"><span data-stu-id="cb32e-143">Dropped events</span></span>

<span data-ttu-id="cb32e-144">샘플 토폴로지는 다음 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="cb32e-145">Session.cs: 임의 세션 ID, 시작 시간 및 세션 지속 시간을 만들어 사용자 세션을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="cb32e-146">Spout.cs: 100개의 세션을 만들고 START 이벤트를 내보내고 각 세션에 대한 임의 시간 제한을 대기하고 END 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="cb32e-147">그런 다음 종료한 세션을 재순환하여 새로운 세션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="cb32e-148">HBaseLookupBolt.cs: 세션 ID를 사용하여 HBase에서 세션 정보를 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="cb32e-149">END 이벤트가 처리되면 해당되는 START 이벤트를 찾아서 세션의 소요 시간을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="cb32e-150">HBaseBolt.cs: HBase에 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="cb32e-151">TypeHelper.cs: HBase에서 읽기/쓰기할 때 형식 변환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="cb32e-152">HBase 스키마</span><span class="sxs-lookup"><span data-stu-id="cb32e-152">HBase schema</span></span>

<span data-ttu-id="cb32e-153">HBase에서 데이터가 다음 스키마/설정을 사용 하여 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="cb32e-154">행 키: 세션 ID가 이 테이블의 행에 대한 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="cb32e-155">열 제품군: 제품군 이름은 'cf'입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="cb32e-156">이 제품군에 저장되는 열은:</span><span class="sxs-lookup"><span data-stu-id="cb32e-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="cb32e-157">이벤트: START 또는 END</span><span class="sxs-lookup"><span data-stu-id="cb32e-157">event: START or END.</span></span>

  * <span data-ttu-id="cb32e-158">시간: 이벤트가 발생한 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="cb32e-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="cb32e-159">지속 시간: 이벤트 START와 END 사이의 길이</span><span class="sxs-lookup"><span data-stu-id="cb32e-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="cb32e-160">버전: 'cf' 패밀리는 각 행의 5가지 버전을 유지하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cb32e-161">버전은 특정 행의 키에 대해 저장된 이전 값의 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="cb32e-162">기본적으로 HBase는 행의 가장 최근 버전에 대한 값만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="cb32e-163">이 경우 같은 행은 모든 이벤트(START, END)에 대해 사용됩니다. 행의 각 버전은 타임 스탬프 값에 의해 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="cb32e-164">버전은 특정 ID에 대해 기록된 이벤트의 기록 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="cb32e-165">프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-165">Download the project</span></span>

<span data-ttu-id="cb32e-166">샘플 프로젝트는 [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="cb32e-167">이 다운로드에는 다음 C# 프로젝트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="cb32e-168">CorrelationTopology: 사용자 세션에 대해 시작 및 종료 이벤트를 임의로 내보내는 C# Storm 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="cb32e-169">각 세션은 1분에서 5분 사이까지 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="cb32e-170">SessionInfo: HBase 테이블을 생성하고 저장된 세션 데이터에 대한 정보를 반환하는 예제 쿼리를 제공하는 C# 콘솔 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="cb32e-171">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="cb32e-171">Create the table</span></span>

1. <span data-ttu-id="cb32e-172">Visual Studio에서 **SessionInfo** 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="cb32e-173">**솔루션 탐색기**에서 **SessionInfo** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![선택한 속성을 가진 메뉴의 스크린샷](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="cb32e-175">**설정**을 선택하고 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="cb32e-176">HBaseClusterURL: HBase 클러스터에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="cb32e-177">예를 들어 https://myhbasecluster.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="cb32e-178">HBaseClusterUserName: 클러스터에 대한 관리/HTTP 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="cb32e-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="cb32e-179">HBaseClusterPassword: 관리/HTTP 사용자 계정에 대한 암호</span><span class="sxs-lookup"><span data-stu-id="cb32e-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="cb32e-180">HBaseTableName: 이 예제와 함께 사용하기 위한 테이블 이름</span><span class="sxs-lookup"><span data-stu-id="cb32e-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="cb32e-181">HBaseTableColumnFamily: 열 패밀리 이름</span><span class="sxs-lookup"><span data-stu-id="cb32e-181">HBaseTableColumnFamily: The column family name</span></span>

     ![설정 대화 상자 이미지](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="cb32e-183">솔루션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-183">Run the solution.</span></span> <span data-ttu-id="cb32e-184">메시지가 표시되면 'c' 키를 선택하여 HBase 클러스터에 테이블을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="cb32e-185">Storm 토폴로지 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="cb32e-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="cb32e-186">Visual Studio에서 **CorrelationTopology** 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="cb32e-187">**솔루션 탐색기**에서 **CorrelationTopology** 프로젝트를 마우스 오른쪽 단추로 클릭하고 [속성]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="cb32e-188">[속성] 창에서 **설정**을 선택하고 이 프로젝트에 대한 구성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="cb32e-189">처음 5개는 **SessionInfo** 프로젝트에서 사용되는 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="cb32e-190">HBaseClusterURL: HBase 클러스터에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="cb32e-191">예를 들어 https://myhbasecluster.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="cb32e-192">HBaseClusterUserName: 클러스터의 관리자/HTTP 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="cb32e-193">HBaseClusterPassword: 관리자/HTTP 사용자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="cb32e-194">HBaseTableName: 이 예제와 함께 사용하기 위한 테이블 이름.</span><span class="sxs-lookup"><span data-stu-id="cb32e-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="cb32e-195">이 값은 SessionInfo 프로젝트에서 사용되는 동일한 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="cb32e-196">HBaseTableColumnFamily: 열 제품군 이름.</span><span class="sxs-lookup"><span data-stu-id="cb32e-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="cb32e-197">이 값은 SessionInfo 프로젝트에서 사용되는 동일한 열 패밀리 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="cb32e-198">기본값이 **SessionInfo** 에서 데이터 검색에 사용되는 이름이므로 HBaseTableColumnNames를 변경하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="cb32e-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="cb32e-199">속성을 저장한 다음 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="cb32e-200">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **HDInsight에서 Storm에 제출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="cb32e-201">메시지가 표시되면 Azure 구독에 대한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Storm 메뉴 항목에 제출 이미지](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="cb32e-203">**토폴로지 제출** 대화 상자에서 이 토폴로지를 배포하려는 Storm 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb32e-204">처음으로 토폴로지를 제출하면 HDInsight 클러스터의 이름을 검색하는 데 몇 초가 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="cb32e-205">토폴로지가 업로드되고 클러스터에 제출되면 **Storm 토폴로지 보기**가 열리고 실행 중인 토폴로지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="cb32e-206">데이터를 새로 고치려면 **CorrelationTopology**를 선택하고 페이지의 오른쪽 위에 있는 [새로 고침] 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![토폴로지 보기 이미지](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="cb32e-208">토폴로지가 데이터를 생성하기 시작하면 **내보낸** 열의 값이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb32e-209">**Storm 토폴로지 보기** 가 자동으로 열리지 않으면 다음 단계를 이용하여 여십시오.</span><span class="sxs-lookup"><span data-stu-id="cb32e-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="cb32e-210">**솔루션 탐색기**에서 **Azure**를 확장하고 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="cb32e-211">토폴로지가 실행되는 Storm 클러스터를 마우스 오른쪽 단추로 클릭한 다음 **Storm 토폴로지 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="cb32e-212">데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="cb32e-212">Query the data</span></span>

<span data-ttu-id="cb32e-213">데이터를 내보낸 후 다음 단계를 사용하여 데이터를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="cb32e-214">**SessionInfo** 프로젝트로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="cb32e-215">실행되고 있지 않다면 새로운 인스턴스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="cb32e-216">메시지가 표시되면 **s**를 선택하여 START 이벤트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="cb32e-217">시간 범위를 정의하기 위해 시작 및 종료 시간을 입력하라는 메시지가 표시됩니다. 이 두 시간 사이의 이벤트만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="cb32e-218">시작 및 종료 시간 입력 시 다음 형식을 사용합니다. HH:MM 및 'am' 또는 'pm'.</span><span class="sxs-lookup"><span data-stu-id="cb32e-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="cb32e-219">예: 11:20pm.</span><span class="sxs-lookup"><span data-stu-id="cb32e-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="cb32e-220">기록된 이벤트를 반환하려면 Storm 토폴로지가 배포되기 전의 시작 시간과 현재의 종료 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="cb32e-221">반환 데이터에는 다음 텍스트와 유사한 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="cb32e-222">END 이벤트의 검색은 START 이벤트의 검색과 동일하게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="cb32e-223">하지만, END 이벤트는 START 이벤트 후 1분과 5분 사이에 임의로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="cb32e-224">END 이벤트를 찾으려면 시간 범위를 몇 차례 시도해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="cb32e-225">또한 END 이벤트에는 START 이벤트 시간과 END 이벤트 시간 사이의 차이인 세션의 소요 시간도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="cb32e-226">다음은 END 이벤트에 대한 데이터 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="cb32e-227">입력한 시간 값은 로컬 시간 단위이지만 쿼리로부터 반환된 시간은 UTC 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="cb32e-228">토폴로지 중지</span><span class="sxs-lookup"><span data-stu-id="cb32e-228">Stop the topology</span></span>

<span data-ttu-id="cb32e-229">토폴로지의 중지가 준비되면 Visual Studio에서 **CorrelationTopology** 프로젝트로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="cb32e-230">**Storm 토폴로지 보기**에서 토폴로지를 선택하고 토폴로지의 상단에 있는 **Kill** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb32e-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="cb32e-231">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="cb32e-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="cb32e-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb32e-232">Next steps</span></span>

<span data-ttu-id="cb32e-233">더 많은 Storm 예제는 [HDInsight의 Storm에 대한 예제 토폴로지](hdinsight-storm-example-topology.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cb32e-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
