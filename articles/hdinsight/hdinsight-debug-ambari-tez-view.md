---
title: "aaaUse HDInsight-Azure와 Ambari Tez 보기 | Microsoft Docs"
description: "Toouse hello Ambari Tez HDInsight의 toodebug Tez 작업을 표시 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="54459-103">Ambari 뷰 toodebug Tez 작업을 사용 하 여 HDInsight의</span><span class="sxs-lookup"><span data-stu-id="54459-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="54459-104">HDInsight에 대 한 웹 UI Ambari hello Tez를 사용 하는 사용 되는 toounderstand 및 디버그 작업이 될 수 있는 Tez 보기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="54459-105">hello Tez 보기가 있습니다 toovisualize hello 작업이 연결 된 항목에 대 한 그래프는 각 항목을 더 자세히 분석 하 고 통계 및 로깅 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54459-106">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="54459-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54459-108">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54459-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54459-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54459-109">Prerequisites</span></span>

* <span data-ttu-id="54459-110">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="54459-111">클러스터를 만드는 단계는 [Linux 기반 HDInsight 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54459-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="54459-112">HTML5를 지원하는 최신 웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="54459-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="54459-113">Tez 이해</span><span class="sxs-lookup"><span data-stu-id="54459-113">Understanding Tez</span></span>

<span data-ttu-id="54459-114">Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="54459-115">Linux 기반 HDInsight 클러스터에 대 한 하이브 hello 기본 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="54459-116">Tez 전달 된 비순환 그래프 (DAG) 작업에 필요한 작업의 hello 순서를 설명 하는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54459-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="54459-117">개별 작업 꼭지점 라고 하며 실행 hello에 조각의 전체 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="54459-118">hello 꼭지점에서 설명 하는 hello 작업의 실제 실행 작업을 라고 및 hello 클러스터의 여러 노드에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="54459-119">이해 hello Tez 보기</span><span class="sxs-lookup"><span data-stu-id="54459-119">Understanding hello Tez view</span></span>

<span data-ttu-id="54459-120">hello Tez 보기는 실행 중인 프로세스에 기록 정보 및 정보 둘 다를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="54459-121">이 정보는 작업이 클러스터 사이에서 분산된 방식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="54459-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="54459-122">또한 작업 및 꼭지점에 사용 된 카운터를 표시 하 고 toohello 작업와 관련 된 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="54459-123">Hello 다음 시나리오에에서 유용한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="54459-124">장기 실행 프로세스, 보기 모니터링 hello 지도의 진행률 및 감소 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="54459-125">실패 한 이유 또는 처리 개선할 수 있는 방법을 toolearn 성공 또는 실패 한 프로세스에 대 한 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="54459-126">DAG 생성</span><span class="sxs-lookup"><span data-stu-id="54459-126">Generate a DAG</span></span>

<span data-ttu-id="54459-127">현재 실행 중인 되었거나 이전에 실행 된 하는 hello Tez 보기 데이터를 사용 하는 작업 hello Tez 엔진 경우만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="54459-128">간단한 Hive 쿼리는 Tez를 사용하지 않고도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="54459-129">필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는</span><span class="sxs-lookup"><span data-stu-id="54459-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="54459-130">hello Tez 엔진을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-130">use hello Tez engine.</span></span>

<span data-ttu-id="54459-131">다음 단계 toorun Tez를 사용 하는 하이브 쿼리 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="54459-132">웹 브라우저에서 탐색 toohttps://CLUSTERNAME.azurehdinsight.net, 여기서 **CLUSTERNAME** HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="54459-133">Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **뷰** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="54459-134">이 아이콘은 여러 개의 사각형처럼 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="54459-135">나타나는 hello 드롭다운 목록을 선택 **보기 하이브**합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Hive 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="54459-137">로드 될 때 hello 하이브 뷰 붙여넣기 hello 다음 hello 쿼리 편집기에서 쿼리할을 클릭 한 다음 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="54459-138">Hello에 표시 하는 hello 출력이 표시 hello 작업이 완료 되 면 **쿼리 프로세스 결과** 섹션.</span><span class="sxs-lookup"><span data-stu-id="54459-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="54459-139">hello 결과 텍스트 다음 비슷한 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54459-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="54459-140">선택 hello **로그** 탭 합니다. 정보 비슷한 toohello 텍스트 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54459-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="54459-141">Hello 저장 **앱 id** 값으로이 값은 hello 다음 섹션에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54459-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="54459-142">Hello Tez 보기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="54459-142">Use hello Tez View</span></span>

1. <span data-ttu-id="54459-143">Hello hello 페이지의 hello 위쪽 메뉴에서 선택 hello **뷰** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="54459-144">나타나는 hello 드롭다운 목록을 선택 **Tez 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Tez 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="54459-146">Hello Tez 보기 로드 되 면 hello 클러스터에서 현재 실행 중인 이거나 받아야 하는 하이브 쿼리 목록이 실행 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![모든 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="54459-148">항목이 하나만 있는 경우 hello 이전 섹션에서를 실행 하는 hello 쿼리의입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="54459-149">항목이 여러 개 있는 경우에 hello hello 페이지 위쪽에 hello 필드를 사용 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="54459-150">선택 hello **쿼리 ID** 하이브 쿼리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="54459-151">Hello 쿼리 하는 방법에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54459-151">Information about hello query is displayed.</span></span>

    ![DAG 세부 정보](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="54459-153">이 페이지에 hello 탭을 사용 하면 다음 정보는 tooview hello:</span><span class="sxs-lookup"><span data-stu-id="54459-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="54459-154">**세부 정보를 쿼리**: hello 하이브 쿼리 하는 방법에 대 한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="54459-155">**타임라인**: 각 처리 단계가 진행되는 데 걸린 시간에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="54459-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="54459-156">**구성을**:이 쿼리에 사용 된 hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="54459-157">__쿼리 세부 정보__ hello에 대 한 hello 링크 toofind 정보를 사용할 수 있습니다 __응용 프로그램__ 또는 hello __DAG__ 이 쿼리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="54459-158">hello __응용 프로그램__ 링크 hello이이 쿼리에 대해 YARN 응용 프로그램에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="54459-159">여기에서 hello YARN 응용 프로그램 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="54459-160">hello __DAG__ 링크는이 쿼리에 대 한 지정된 된 비순환 그래프 hello에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="54459-161">여기에서 그래픽으로 나타낸 hello DAG 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="54459-162">Hello 꼭지점 hello DAG에 대 한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54459-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54459-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54459-163">Next Steps</span></span>

<span data-ttu-id="54459-164">이제 toouse hello Tez 보는 방법을 배웠습니다를 보다 자세히 배울에 대 한 [를 사용 하 여 HDInsight의 Hive](hdinsight-use-hive.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="54459-165">Tez 대 한 기술 정보를 자세한 참조 hello [Hortonworks Tez 페이지](http://hortonworks.com/hadoop/tez/)합니다.</span><span class="sxs-lookup"><span data-stu-id="54459-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="54459-166">Ambari HDInsight 사용에 대 한 자세한 내용은 참조 하세요. [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="54459-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
