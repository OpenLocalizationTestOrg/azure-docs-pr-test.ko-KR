---
title: "HDInsight에서 Ambari Tez 보기 사용 - Azure | Microsoft Docs"
description: "Ambari Tez 뷰를 사용하여 HDInsight에서 Tez 작업을 디버깅하는 방법을 알아봅니다."
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
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="0a938-103">HDInsight에서 Ambari 뷰를 사용하여 Tez 작업 디버깅</span><span class="sxs-lookup"><span data-stu-id="0a938-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="0a938-104">HDInsight의 Ambari Web UI에는 Tez를 사용하는 작업을 이해 및 디버깅하는 데 사용할 수 있는 Tez 보기가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="0a938-105">Tez 뷰를 사용하면 연결된 항목의 그래프로 작업을 시각화하고 각 항목을 자세히 알아보며 통계 및 로깅 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a938-106">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="0a938-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0a938-108">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a938-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a938-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0a938-109">Prerequisites</span></span>

* <span data-ttu-id="0a938-110">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0a938-111">클러스터를 만드는 단계는 [Linux 기반 HDInsight 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a938-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="0a938-112">HTML5를 지원하는 최신 웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="0a938-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="0a938-113">Tez 이해</span><span class="sxs-lookup"><span data-stu-id="0a938-113">Understanding Tez</span></span>

<span data-ttu-id="0a938-114">Tez는 기존의 MapReduce 처리보다 빠른 속도를 제공하는 Hadoop의 데이터 처리에 대해 확장 가능한 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="0a938-115">Linux 기반 HDInsight 클러스터에서는 Hive에 대한 기본 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="0a938-116">Tez는 작업에서 수행해야 하는 작업 순서를 설명하는 DAG(방향성 비순환 그래프)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="0a938-117">개별 동작은 꼭짓점을 호출하고 전체 작업의 일부를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="0a938-118">꼭짓점에서 설명하는 작업의 실제 실행을 태스크라고 하며 클러스터의 여러 노드에 분산될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="0a938-119">Tez 뷰 이해</span><span class="sxs-lookup"><span data-stu-id="0a938-119">Understanding the Tez view</span></span>

<span data-ttu-id="0a938-120">Tez 보기는 기록 정보 및 실행 중인 프로세스에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="0a938-121">이 정보는 작업이 클러스터 사이에서 분산된 방식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="0a938-122">또한 태스크와 꼭짓점에서 사용하는 카운터 및 작업과 관련된 오류 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="0a938-123">다음과 같은 시나리오에서 유용한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="0a938-124">장기 실행 처리를 모니터링하고 맵의 진행 상황을 보며 태스크를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="0a938-125">처리를 향상시킬 방법 또는 실패한 이유를 알아보기 위해 성공 또는 실패한 처리에 대한 기록 데이터를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="0a938-126">DAG 생성</span><span class="sxs-lookup"><span data-stu-id="0a938-126">Generate a DAG</span></span>

<span data-ttu-id="0a938-127">Tez 보기에는 Tez 엔진을 사용하는 작업이 현재 실행 중인 경우 또는 이전에 실행된 경우에만 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="0a938-128">간단한 Hive 쿼리는 Tez를 사용하지 않고도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="0a938-129">필터링, 그룹화, 정렬, 조인 등을 수행하는 복잡한 쿼리는</span><span class="sxs-lookup"><span data-stu-id="0a938-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="0a938-130">Tez 엔진을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-130">use the Tez engine.</span></span>

<span data-ttu-id="0a938-131">Tez를 사용하는 Hive 쿼리를 실행하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="0a938-132">웹 브라우저에서 https://CLUSTERNAME.azurehdinsight.net으로 이동합니다. 여기서 **CLUSTERNAME**은 HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="0a938-133">페이지 위쪽의 메뉴에서 **보기** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="0a938-134">이 아이콘은 여러 개의 사각형처럼 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="0a938-135">표시되는 드롭다운에서 **Hive 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Hive 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="0a938-137">로드된 Hive 보기에서 다음 쿼리를 [쿼리 편집기]에 붙여넣은 후 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="0a938-138">작업이 완료되면 **쿼리 프로세스 결과** 섹션에 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="0a938-139">결과는 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="0a938-140">**로그** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-140">Select the **Log** tab.</span></span> <span data-ttu-id="0a938-141">다음 텍스트와 유사한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="0a938-142">다음 섹션에서 사용하는 **App id** 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="0a938-143">Tez 뷰 사용</span><span class="sxs-lookup"><span data-stu-id="0a938-143">Use the Tez View</span></span>

1. <span data-ttu-id="0a938-144">페이지 위쪽의 메뉴에서 **보기** 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="0a938-145">표시되는 드롭다운에서 **Tez 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Tez 뷰 선택](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="0a938-147">Tez 뷰가 로드되면 클러스터에서 현재 실행 중이거나 실행된 Hive 쿼리 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![모든 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="0a938-149">항목이 하나만 있는 경우 이전 섹션에서 실행한 쿼리에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="0a938-150">항목이 여러 개 있는 경우 페이지 맨 위에 있는 필드를 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="0a938-151">Hive 쿼리에 대한 **쿼리 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="0a938-152">쿼리에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-152">Information about the query is displayed.</span></span>

    ![DAG 세부 정보](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="0a938-154">이 페이지에 있는 탭에서 다음 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="0a938-155">**쿼리 세부 정보**: Hive 쿼리에 대한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="0a938-156">**타임라인**: 각 처리 단계가 진행되는 데 걸린 시간에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="0a938-157">**구성**: 이 쿼리에 사용된 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="0a938-158">__쿼리 세부 정보__에서 링크를 사용하여 이 쿼리에 대한 __응용 프로그램__ 또는 __DAG__ 관련 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="0a938-159">__응용 프로그램__ 링크를 클릭하면 이 쿼리의 YARN 응용 프로그램에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="0a938-160">여기에서 YARN 응용 프로그램 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="0a938-161">__DAG__ 링크를 클릭하면 이 쿼리에 대해 지정된 비순환 그래프 관련 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="0a938-162">여기에서 DAG의 그래픽 표시를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="0a938-163">DAG 내에서 꼭짓점에 대한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a938-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a938-164">Next Steps</span></span>

<span data-ttu-id="0a938-165">이제 Tez 뷰를 사용하는 방법을 배웠으므로 [HDInsight에서 Hive 사용](hdinsight-use-hive.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a938-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="0a938-166">Tez에서 자세한 기술 정보는 [Hortonworks의 Tez 페이지](http://hortonworks.com/hadoop/tez/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a938-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="0a938-167">HDInsight과 함께 Ambari를 사용하는 방법에 대한 자세한 내용은 [Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="0a938-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
