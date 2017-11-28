---
title: "실행 Azure HDInsight의 Apache Spark aaaDebug 작업 | Microsoft Docs"
description: "작업 사용 하 여 YARN UI, Spark UI 및 Spark 기록 서버 tootrack 및 디버그 Azure HDInsight의 Spark 클러스터에서 실행 중인"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="f4a45-103">Azure HDInsight에서 실행 중인 Apache Spark 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="f4a45-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="f4a45-104">이 문서에서 tootrack 및 디버그 멤버 hello YARN UI Spark UI를 사용 하 여 HDInsight 클러스터에서 실행 중인 작업 하 고 스파크 기록 서버 hello 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="f4a45-105">이 문서에 대 한 hello Spark 클러스터를 사용할 수 있는 노트북을 사용 하 여 Spark 작업을 시작 하겠습니다 **기계 학습: MLLib를 사용 하 여 음식 검사 데이터에서 예측 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="f4a45-106">Tootrack 제출한 다른 방법을 사용도를 사용 하 여 예를 들어 응용 프로그램 아래 hello 단계를 사용할 수 있습니다 **spark 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4a45-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4a45-107">Prerequisites</span></span>
<span data-ttu-id="f4a45-108">Hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-108">You must have hello following:</span></span>

* <span data-ttu-id="f4a45-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f4a45-109">An Azure subscription.</span></span> <span data-ttu-id="f4a45-110">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4a45-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f4a45-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f4a45-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4a45-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="f4a45-113">Hello 노트북 실행를 시작한 해야  **[기계 학습: MLLib를 사용 하 여 음식 검사 데이터에서 예측 분석](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="f4a45-114">방법에 대 한 지침은 toorun이이 노트북 hello 링크를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="f4a45-115">Hello YARN UI에서에서 응용 프로그램 추적</span><span class="sxs-lookup"><span data-stu-id="f4a45-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="f4a45-116">Hello YARN UI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-116">Launch hello YARN UI.</span></span> <span data-ttu-id="f4a45-117">Hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **YARN**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![YARN UI 시작](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="f4a45-119">또는 hello Ambari UI에서에서 hello YARN UI를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="f4a45-120">hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="f4a45-121">Ambari UI hello에서 클릭 **YARN**, 클릭 **빠른 링크**, hello 활성 리소스 관리자를 클릭 하 고 클릭 **ResourceManager UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="f4a45-122">Hello 응용 프로그램에 hello 이름이 Jupyter 노트북을 사용 하 여 hello Spark 작업을 시작 했으므로 **remotesparkmagics** (이것이 hello 전자 필기장에서 시작 된 모든 응용 프로그램에 대 한 hello 이름).</span><span class="sxs-lookup"><span data-stu-id="f4a45-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="f4a45-123">Hello 작업에 대 한 자세한 내용은 응용 프로그램 이름 tooget hello에 대 한 hello 응용 프로그램 ID를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="f4a45-124">Hello 응용 프로그램 보기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-124">This launches hello application view.</span></span>
   
    ![Spark 응용 프로그램 ID 찾기](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="f4a45-126">Hello Jupyter 노트북에서 시작 하는 이러한 응용 프로그램에 대 한 hello 상태는 항상 **실행** hello 노트북 종료 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="f4a45-127">Hello 응용 프로그램 보기에서 hello 응용 프로그램 및 hello 로그 (stdout/stderr)와 관련 된 hello 컨테이너 아웃 toofind 추가로 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="f4a45-128">Hello 해당 toohello 링크를 클릭 하 여 hello Spark UI를 시작할 수도 있습니다 **추적 URL**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![컨테이너 로그 다운로드](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="f4a45-130">Hello Spark UI에서에서 응용 프로그램 추적</span><span class="sxs-lookup"><span data-stu-id="f4a45-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="f4a45-131">Spark UI hello에서 앞에서 시작 하는 hello 응용 프로그램에서 생성 하는 hello Spark 작업으로 다운 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="f4a45-132">hello에 대 한 hello 링크를 클릭 하는 hello 응용 프로그램 보기에서 toolaunch hello Spark UI **추적 URL**위의 hello 화면 캡처에 나타난 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="f4a45-133">Hello Jupyter 노트북에서 실행 되는 hello 응용 프로그램에 의해 실행 되는 모든 hello Spark 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Spark 작업 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="f4a45-135">Hello 클릭 **Executor** toosee 처리 및 저장 각 실행 기에 대 한 정보를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="f4a45-136">Hello를 클릭 하 여 hello 호출 스택을 검색할 수도 있습니다 **스레드 덤프** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Spark 실행자 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="f4a45-138">Hello 클릭 **단계** hello 응용 프로그램과 관련 된 toosee hello 단계를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="f4a45-140">각 단계에서는 아래와 같이 실행 통계를 볼 수 있는 여러 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="f4a45-142">Hello 단계 세부 정보 페이지에서 DAG 시각화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="f4a45-143">Hello 확장 **DAG 시각화** 아래와 같이 hello hello 페이지 위쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Spark 단계 DAG 시각화 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="f4a45-145">DAG 또는 직접 Aclyic 그래프 hello hello 응용 프로그램에 다른 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="f4a45-146">Hello 그래프의 각 파랑 상자 hello 응용 프로그램에서 호출한 Spark 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="f4a45-147">Hello 단계 세부 정보 페이지에서 hello 응용 프로그램 타임 라인 보기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="f4a45-148">Hello 확장 **이벤트 타임 라인** 아래와 같이 hello hello 페이지 위쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Spark 단계 이벤트 타임라인 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="f4a45-150">Hello Spark 이벤트 hello 시간대 형식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="f4a45-151">hello 시간 표시 막대 뷰는 사용할 수 있는 세 가지 수준에서 작업, 작업, 내에서, 단계 내에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="f4a45-152">위의 hello 이미지는 지정 된 단계에 대 한 hello 시간 표시 막대 뷰를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f4a45-153">Hello를 선택 하는 경우 **확대/축소를 사용 하도록 설정** 확인란을 스크롤할 수 왼쪽과 오른쪽 hello 타임 라인 보기.</span><span class="sxs-lookup"><span data-stu-id="f4a45-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="f4a45-154">Hello Spark UI에서에서 다른 탭도 hello Spark 인스턴스에 대 한 유용한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="f4a45-155">저장소 탭-응용 프로그램 만들기는 RDDs hello 저장소 탭에 대 한 정보를 찾을 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="f4a45-156">환경 탭-이 탭에서는 많은 hello 같은 Spark 인스턴스에 대 한 유용한 정보</span><span class="sxs-lookup"><span data-stu-id="f4a45-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="f4a45-157">Scala 버전</span><span class="sxs-lookup"><span data-stu-id="f4a45-157">Scala version</span></span>
     * <span data-ttu-id="f4a45-158">Hello 클러스터와 연결 된 이벤트 로그 디렉터리</span><span class="sxs-lookup"><span data-stu-id="f4a45-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="f4a45-159">Hello 응용 프로그램에 대 한 실행자 코어 수</span><span class="sxs-lookup"><span data-stu-id="f4a45-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="f4a45-160">등</span><span class="sxs-lookup"><span data-stu-id="f4a45-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="f4a45-161">Spark 기록 서버 hello를 사용 하 여 완료 된 작업에 대 한 정보 찾기</span><span class="sxs-lookup"><span data-stu-id="f4a45-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="f4a45-162">작업이 완료 되 면 hello 작업에 대 한 hello 정보 Spark 기록 서버 hello에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="f4a45-163">toolaunch hello Spark 기록 서버 hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Spark 기록 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="f4a45-165">또는 hello Ambari UI에서에서 hello Spark 기록 서버 UI를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="f4a45-166">hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="f4a45-167">Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **빠른 링크**, 클릭 하 고 **Spark 기록 서버 UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="f4a45-168">나열 된 모든 완료 hello 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="f4a45-169">자세한 내용은 응용 프로그램으로 아래로 응용 프로그램 ID toodrill를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="f4a45-171">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f4a45-171">See also</span></span>
*  [<span data-ttu-id="f4a45-172">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="f4a45-173">데이터 분석가</span><span class="sxs-lookup"><span data-stu-id="f4a45-173">For data analysts</span></span>

* [<span data-ttu-id="f4a45-174">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="f4a45-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f4a45-175">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="f4a45-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f4a45-176">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="f4a45-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="f4a45-177">HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="f4a45-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="f4a45-178">분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용</span><span class="sxs-lookup"><span data-stu-id="f4a45-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="f4a45-179">Spark 개발자</span><span class="sxs-lookup"><span data-stu-id="f4a45-179">For Spark developers</span></span>

* [<span data-ttu-id="f4a45-180">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f4a45-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f4a45-181">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="f4a45-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="f4a45-182">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="f4a45-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="f4a45-183">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="f4a45-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f4a45-184">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="f4a45-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f4a45-185">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="f4a45-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f4a45-186">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="f4a45-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f4a45-187">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="f4a45-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f4a45-188">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a45-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


