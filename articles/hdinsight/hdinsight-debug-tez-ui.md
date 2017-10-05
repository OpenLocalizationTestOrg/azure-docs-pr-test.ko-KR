---
title: "Windows 기반 HDInsight에서 Tez UI 사용 - Azure | Microsoft Docs"
description: "Windows 기반 HDInsight 클러스터에서 Tez UI를 사용하여 Tez 작업 디버깅하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="def64-103">Windows 기반 HDInsight 클러스터에서 Tez UI를 사용하여 Tez 작업 디버깅</span><span class="sxs-lookup"><span data-stu-id="def64-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="def64-104">Tez UI는 Windows 기반 HDInsight 클러스터에서 Tez를 실행 엔진으로 사용하는 작업을 이해하고 디버깅하는 데 사용될 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="def64-105">Tez UI를 사용하면 연결된 항목의 그래프로 작업을 시각화하고 각 항목을 자세히 알아보며 통계 및 로깅 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="def64-106">이 문서의 단계에는 Windows를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="def64-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="def64-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="def64-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="def64-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="def64-109">Prerequisites</span></span>
* <span data-ttu-id="def64-110">Windows 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="def64-111">새 클러스터를 만드는 단계는 [Windows 기반 HDInsight 사용 시작](hdinsight-hadoop-tutorial-get-started-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="def64-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="def64-112">Tez UI는 2016년 2월 8일 이후에 작성된 Windows 기반 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="def64-113">Windows 기반 원격 데스크톱 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="def64-114">Tez 이해</span><span class="sxs-lookup"><span data-stu-id="def64-114">Understanding Tez</span></span>
<span data-ttu-id="def64-115">Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="def64-116">Windows 기반 HDInsight 클러스터의 경우 Hive 쿼리의 일부분으로 다음 명령을 사용하여 Hive에 사용할 수 있는 선택적 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="def64-117">작업을 Tez에 제출하는 경우 작업에 필요한 동작의 실행 순서를 설명하는 DAG(방향성 비순환 그래프)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="def64-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="def64-118">개별 동작은 꼭짓점을 호출하고 전체 작업의 일부를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="def64-119">꼭짓점에서 설명하는 작업의 실제 실행을 태스크라고 하며 클러스터의 여러 노드에 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="def64-120">Tez UI 이해</span><span class="sxs-lookup"><span data-stu-id="def64-120">Understanding the Tez UI</span></span>
<span data-ttu-id="def64-121">Tez UI는 실행 중이거나 Tez를 사용하여 이전에 실행된 프로세스에 대한 정보를 제공하는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="def64-122">Tez에 의해 생성된 DAG를 볼 수 있고 태스크 및 꼭짓점에서 사용된 메모리와 오류 정보와 같은 카운터인 클러스터에 배포되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="def64-123">다음과 같은 시나리오에서 유용한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="def64-124">장기 실행 처리를 모니터링하고 맵의 진행 상황을 보며 태스크를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="def64-125">처리를 향상시킬 방법 또는 실패한 이유를 알아보기 위해 성공 또는 실패한 처리에 대한 기록 데이터를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="def64-126">DAG 생성</span><span class="sxs-lookup"><span data-stu-id="def64-126">Generate a DAG</span></span>
<span data-ttu-id="def64-127">Tez UI는 Tez 엔진을 사용하는 작업이 현재 실행되거나 이전에 실행된 경우에만 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="def64-128">간단한 Hive 쿼리는 Tez를 사용하지 않고 해결될 수 있지만 필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는 Tez가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="def64-129">Tez를 사용하여 실행하는 Hive 쿼리를 실행하기 위해 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="def64-130">웹 브라우저에서 https://CLUSTERNAME.azurehdinsight.net으로 이동합니다. 여기서 **CLUSTERNAME**은 HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="def64-131">페이지 위쪽의 메뉴에서 **Hive 편집기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="def64-132">다음 예제 쿼리로 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="def64-133">예제 쿼리를 지우고 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="def64-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="def64-134">**제출** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-134">Select the **Submit** button.</span></span> <span data-ttu-id="def64-135">페이지의 아래쪽에서 **작업 세션** 섹션은 쿼리 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="def64-136">상태가 **완료됨**으로 변경되면 **세부 정보 보기** 링크를 선택하여 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="def64-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="def64-137">**작업 출력**은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="def64-138">Tez UI 사용</span><span class="sxs-lookup"><span data-stu-id="def64-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="def64-139">Tez UI는 클러스터 헤드 노드의 바탕 화면에서만 사용할 수 있으므로 원격 데스크톱을 사용하여 헤드 노드에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="def64-140">[Azure 포털](https://portal.azure.com)에서 HDInsight 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="def64-141">HDInsight 블레이드 위쪽에서 **원격 데스크톱** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="def64-142">원격 데스크톱 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-142">This will display the remote desktop blade</span></span>

    ![원격 데스크톱 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="def64-144">[원격 데스크]톱 블레이드에서 **연결** 을 선택하여 클러스터 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="def64-145">대화 상자가 나타나면 클러스터 원격 데스크톱 사용자 이름 및 암호를 사용하여 연결을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![원격 데스크톱 연결 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="def64-147">원격 데스크톱 연결을 설정하지 않은 경우 사용자 이름, 암호 및 만료 날짜를 제공한 다음 **사용**을 선택하여 원격 데스크톱을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="def64-148">활성화되면 이전 단계를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="def64-149">연결되면 원격 데스크톱에서 Internet Explorer를 열고 브라우저의 오른쪽 위에 있는 기어 아이콘을 선택한 다음 **호환성 보기 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="def64-150">**호환성 보기 설정**의 아래쪽에서**호환성 보기에 인트라넷 사이트 표시** 및 **Microsoft 호환성 목록** 확인란의 선택을 취소한 다음 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="def64-151">Internet Explorer에서 http://headnodehost:8188/tezui/#/를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="def64-152">그러면 Tez UI가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-152">This will display the Tez UI</span></span>

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="def64-154">Tez UI가 로드되면 클러스터에서 현재 실행 중이거나 실행된 DAG의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="def64-155">기본 보기는 DAG 이름, ID, 제출자, 상태, 시작 시간, 종료 시간, 기간, 응용 프로그램 ID 및 큐를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="def64-156">페이지의 오른쪽에 있는 기어 아이콘을 사용하여 많은 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="def64-157">항목이 하나만 있으면 이전 섹션에서 실행한 쿼리에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="def64-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="def64-158">여러 항목이 있는 경우 DAG 위에 있는 필드에 검색 조건을 입력하여 검색한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="def64-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="def64-159">가장 최근의 DAG 항목에 대한 **DAG 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="def64-160">DAG에 대한 정보 뿐만 아니라 DAG에 대한 정보가 포함된 JSON 파일의 zip을 다운로드할 수 있는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG 세부 정보](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="def64-162">위 **DAG 세부 정보**에는 DAG 정보를 표시하는 데 사용될 수 있는 링크가 여러 개 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="def64-163">**DAG 카운터**는 해당 DAG에 대한 카운터 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="def64-164">**그래픽 보기**는 해당 DAG의 그래픽 표시를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="def64-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="def64-165">**모든 꼭짓점**은 해당 DAG의 꼭짓점에 대한 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="def64-166">**모든 태스크**는 해당 DAG의 꼭짓점에 대한 태스크 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="def64-167">**모든 태스크 시도**는 해당 DAG의 태스크를 실행하려는 시도에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="def64-168">꼭짓점, 태스크 및 TaskAttempts에 대한 열 표시를 스크롤하는 경우 각 행에 대한 **카운터** 및 **로그 보기 또는 다운로드** 링크를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="def64-169">작업에 오류가 발생한 경우 DAG 세부 정보는 실패한 태스크에 대한 정보의 링크와 함께 실패 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="def64-170">진단 정보는 DAG 세부 정보 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="def64-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="def64-171">**그래픽 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-171">Select **Graphical View**.</span></span> <span data-ttu-id="def64-172">이 DAG의 그래픽 표시를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="def64-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="def64-173">보기에서 각 꼭짓점 위로 마우스를 두어 그에 대한 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![그래픽 보기](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="def64-175">꼭짓점을 클릭하면 해당 항목에 대한 **꼭짓점 세부 정보** 를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="def64-176">**맵 1** 꼭짓점을 클릭하면 이 항목에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="def64-177">**확인**을 선택하여 탐색을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-177">Select **Confirm** to confirm the navigation.</span></span>

    ![꼭짓점 세부 정보](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="def64-179">이제 꼭짓점 및 태스크에 관련된 페이지의 위쪽에 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="def64-180">또한 **DAG 세부 정보**로 다시 이동하고 **꼭짓점 세부 정보**를 선택한 다음 **맵 1** 꼭짓점을 선택하면 이 페이지로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="def64-181">**꼭짓점 카운터**는 이 꼭짓점에 대한 카운터 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="def64-182">**태스크**는 이 꼭짓점에 대한 태스크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="def64-183">**태스크 시도**는 이 꼭짓점의 태스크를 실행하려는 시도에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="def64-184">**원본 및 싱크**는 이 꼭짓점에 대한 데이터 원본 및 싱크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="def64-185">이전 메뉴 작업으로 태스크, 태스크 시도, 원본 및 싱크__에 대한 열 표시를 스크롤하여 각 항목에 대한 자세한 정보의 링크를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="def64-186">**태스크**를 선택한 다음 **00_000000**이라는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="def64-187">이 태스크에 대한 **태스크 세부 정보**를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="def64-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="def64-188">이 화면에서 **태스크 카운터** 및 **태스크 시도**를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="def64-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![태스크 세부 정보](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="def64-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="def64-190">Next Steps</span></span>
<span data-ttu-id="def64-191">이제 Tez 뷰를 사용하는 방법을 배웠으므로 [HDInsight에서 Hive 사용](hdinsight-use-hive.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="def64-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="def64-192">Tez에서 자세한 기술 정보는 [Hortonworks의 Tez 페이지](http://hortonworks.com/hadoop/tez/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="def64-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
