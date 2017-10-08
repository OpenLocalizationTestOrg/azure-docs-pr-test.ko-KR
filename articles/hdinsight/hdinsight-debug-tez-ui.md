---
title: "Windows 기반 HDInsight-Azure와 Tez UI aaaUse | Microsoft Docs"
description: "Windows 기반 HDInsight HDInsight에서 toouse hello Tez UI toodebug Tez 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="796d8-103">Windows 기반 HDInsight의 hello Tez I toodebug Tez 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="796d8-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="796d8-104">hello Tez UI는 Windows 기반 HDInsight 클러스터에서 hello 실행 엔진으로 Tez를 사용 하는 사용 되는 toounderstand 및 디버그 작업이 될 수 있는 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="796d8-105">hello Tez UI 있습니다 toovisualize hello 작업이 연결 된 항목에 대 한 그래프는 각 항목을 더 자세히 분석 하 고 통계 및 로깅 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="796d8-106">이 문서의 단계 hello 창을 사용 하 여 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="796d8-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="796d8-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="796d8-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="796d8-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="796d8-109">Prerequisites</span></span>
* <span data-ttu-id="796d8-110">Windows 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="796d8-111">새 클러스터를 만드는 단계는 [Windows 기반 HDInsight 사용 시작](hdinsight-hadoop-tutorial-get-started-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="796d8-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="796d8-112">hello Tez UI은 2016 년 2 월 8 일 이후 만들어진 Windows 기반 HDInsight 클러스터에서 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="796d8-113">Windows 기반 원격 데스크톱 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="796d8-114">Tez 이해</span><span class="sxs-lookup"><span data-stu-id="796d8-114">Understanding Tez</span></span>
<span data-ttu-id="796d8-115">Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="796d8-116">Windows 기반 HDInsight 클러스터에 대 한는 hello 하이브 쿼리의 일환으로 다음 명령을 사용 하 여 하이브에 사용할 수 있는 선택적 엔진:</span><span class="sxs-lookup"><span data-stu-id="796d8-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="796d8-117">작업이 제출 된 tooTez 때 전달 된 비순환 그래프 (DAG) hello hello 작업에서 요구 하는 hello 작업의 실행 순서를 설명 하는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="796d8-118">개별 작업 꼭지점 라고 하며 실행 hello에 조각의 전체 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="796d8-119">hello 꼭지점에서 설명 하는 hello 작업의 실제 실행 작업을 라고 및 hello 클러스터의 여러 노드에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="796d8-120">이해 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="796d8-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="796d8-121">hello Tez UI는 웹 페이지에서 제공 하는 현재 실행 중이거나 있어야 하는 프로세스에 대 한 정보는 Tez를 사용 하 여 이전에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="796d8-122">Tooview hello Tez에 의해 생성 된 DAG 허용 즉, 작업 및 꼭 짓 점, 오류 정보에서 사용 하는 메모리 카운터, 클러스터 간에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="796d8-123">Hello 다음 시나리오에에서 유용한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="796d8-124">장기 실행 프로세스, 보기 모니터링 hello 지도의 진행률 및 감소 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="796d8-125">실패 한 이유 또는 처리 개선할 수 있는 방법을 toolearn 성공 또는 실패 한 프로세스에 대 한 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="796d8-126">DAG 생성</span><span class="sxs-lookup"><span data-stu-id="796d8-126">Generate a DAG</span></span>
<span data-ttu-id="796d8-127">hello Tez UI 사용 하는 작업 hello Tez 엔진이 현재 실행 중이거나 hello 이전에 실행 된 경우에 데이터를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="796d8-128">간단한 Hive 쿼리는 Tez를 사용하지 않고 해결될 수 있지만 필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는 Tez가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="796d8-129">다음 단계 toorun Tez를 사용 하 여를 실행 하는 하이브 쿼리 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="796d8-130">웹 브라우저에서 탐색 toohttps://CLUSTERNAME.azurehdinsight.net, 여기서 **CLUSTERNAME** HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="796d8-131">Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **하이브 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="796d8-132">다음 예제 쿼리에서 hello로는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="796d8-133">Hello 예제 쿼리를 지우고 hello 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="796d8-134">선택 hello **전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-134">Select hello **Submit** button.</span></span> <span data-ttu-id="796d8-135">hello **작업 세션** hello 페이지의 hello 아래쪽 섹션에는 hello 쿼리의 hello 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="796d8-136">한 번만 상태가 변경 될 너무 hello**완료 됨**선택, hello **세부 정보 보기** tooview hello 결과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="796d8-137">hello **작업 출력** toohello 다음과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="796d8-138">Hello Tez UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="796d8-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="796d8-139">hello Tez UI 에서만 사용 가능 hello 클러스터 헤드 노드 hello 바탕 화면에서 원격 데스크톱 tooconnect toohello 헤드 노드를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="796d8-140">Hello에서 [Azure 포털](https://portal.azure.com)를 HDInsight 클러스터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="796d8-141">Hello HDInsight 블레이드의 hello 위에서 hello 선택 **원격 데스크톱** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="796d8-142">원격 데스크톱 블레이드 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-142">This will display hello remote desktop blade</span></span>

    ![원격 데스크톱 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="796d8-144">Hello 원격 데스크톱 블레이드에서 선택 **연결** tooconnect toohello 클러스터 헤드 노드.</span><span class="sxs-lookup"><span data-stu-id="796d8-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="796d8-145">메시지가 표시 되 면 hello 클러스터 원격 데스크톱 사용자 이름 및 암호 tooauthenticate hello 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![원격 데스크톱 연결 아이콘](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="796d8-147">원격 데스크톱 연결을 설정 하지 않은 경우 사용자 이름, 암호 및 만료 날짜를 입력 한 다음 선택 **사용** tooenable 원격 데스크톱입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="796d8-148">이 활성화 된 이전 단계 tooconnect hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="796d8-149">연결 되 면 hello 원격 데스크톱을 hello 오른쪽 상단의 hello 브라우저에서 선택 hello 기어 아이콘에서 Internet Explorer를 열고 선택한 후 **호환성 보기 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="796d8-150">Hello 아래에서 **호환성 보기 설정**일반 hello에 대 한 확인란 **호환성 보기에서 인트라넷 사이트 표시** 및 **호환성 목록을 사용 하 여 Microsoft**, 선택한 후 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="796d8-151">Internet Explorer에서 toohttp://headnodehost:8188 찾아보기/tezui / #/ 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="796d8-152">Hello Tez UI가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-152">This will display hello Tez UI</span></span>

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="796d8-154">Hello Tez UI가 로드 될 때 현재 실행 중인 이거나 받아야 하는 Dag 목록이 hello 클러스터에서 실행 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="796d8-155">hello 기본 보기에는 hello Dag 이름, Id, 제출자, 상태, 시작 시간, 종료 시간, 기간, 응용 프로그램 ID 및 큐 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="796d8-156">Hello hello 페이지의 오른쪽에 hello 기어 아이콘을 사용 하 여 더 많은 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="796d8-157">항목이 하나만 있는 경우 hello 이전 섹션에서를 실행 하는 hello 쿼리의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="796d8-158">항목이 여러 개 있는 경우에 Dag hello 위에 hello 필드에 검색 조건을 입력 하 여 검색 다음 도달할 수 있습니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="796d8-159">선택 hello **Dag 이름** hello 가장 최근의 DAG 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="796d8-160">이 hello 옵션 toodownload DAG hello에 대 한 정보를 포함 하는 JSON 파일의 zip DAG hello에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![DAG 세부 정보](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="796d8-162">Hello 위에 **DAG 세부 정보** DAG hello에 대 한 정보를 사용 하는 toodisplay 수 있는 몇 가지 링크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="796d8-163">**DAG 카운터**는 해당 DAG에 대한 카운터 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="796d8-164">**그래픽 보기**는 해당 DAG의 그래픽 표시를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="796d8-165">**모든 꼭 짓 점에** 이 DAG에 hello 꼭지점 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="796d8-166">**모든 작업** 이 DAG에 모든 꼭 짓 점에 대해 hello 작업 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="796d8-167">**모든 TaskAttempts** hello에 대 한 정보를 표시가이 DAG에 toorun 작업을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="796d8-168">있으며 tooview 링크 꼭지점, 작업 및 TaskAttempts에 대 한 hello 열 표시 스크롤하면 **카운터** 및 **보거나 로그를 다운로드할** 각 행에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="796d8-169">Hello 작업과 오류가 발생 한, hello DAG 세부 정보는 실패 상태를 hello 실패 한 작업에 대 한 링크 tooinformation 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="796d8-170">진단 정보는 hello DAG 세부 정보 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="796d8-171">**그래픽 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-171">Select **Graphical View**.</span></span> <span data-ttu-id="796d8-172">Hello DAG 그래픽으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="796d8-173">Hello에 대 한 toodisplay 정보 보기에서에서 각 꼭 짓 점 위로 마우스 hello를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![그래픽 보기](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="796d8-175">꼭 짓 점 클릭 하면 hello가 로드 **꼭지점 정보** 해당 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="796d8-176">Hello 클릭 **지도 1** 이 항목에 대 한 꼭지점 toodisplay 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="796d8-177">선택 **확인** tooconfirm hello 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![꼭짓점 세부 정보](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="796d8-179">Note 해야 한다는 관련된 toovertices 및 작업 하는 hello hello 페이지 위쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="796d8-180">너무 다시 이동 하 여이 페이지에도 도착할 수 있습니다**DAG 세부 정보**선택한 **꼭지점 정보**, hello를 선택 하 고 **지도 1** 꼭 짓 점입니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="796d8-181">**꼭짓점 카운터**는 이 꼭짓점에 대한 카운터 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="796d8-182">**태스크**는 이 꼭짓점에 대한 태스크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="796d8-183">**작업 시도** 이 꼭 짓이 점에 대해 시도 toorun 작업에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="796d8-184">**원본 및 싱크**는 이 꼭짓점에 대한 데이터 원본 및 싱크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="796d8-185">Hello 이전 메뉴와 작업에 대 한 hello 열 디스플레이 스크롤하면 수, 작업 시도 및 소스 & Sinks__ toodisplay 각 항목에 대 한 toomore 정보를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="796d8-186">선택 **작업**, 선택 hello 항목 명명 된 다음 **00_000000**합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="796d8-187">이 태스크에 대한 **태스크 세부 정보**를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="796d8-188">이 화면에서 **태스크 카운터** 및 **태스크 시도**를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![태스크 세부 정보](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="796d8-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="796d8-190">Next Steps</span></span>
<span data-ttu-id="796d8-191">이제 toouse hello Tez 보는 방법을 배웠습니다를 보다 자세히 배울에 대 한 [를 사용 하 여 HDInsight의 Hive](hdinsight-use-hive.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="796d8-192">Tez 대 한 기술 정보를 자세한 참조 hello [Hortonworks Tez 페이지](http://hortonworks.com/hadoop/tez/)합니다.</span><span class="sxs-lookup"><span data-stu-id="796d8-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
