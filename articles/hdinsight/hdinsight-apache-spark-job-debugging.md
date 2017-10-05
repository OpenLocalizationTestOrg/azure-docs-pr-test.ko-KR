---
title: "Azure HDInsight에서 실행 중인 Apache Spark 작업 디버그 | Microsoft Docs"
description: "YARN UI, Spark UI 및 Spark 기록 서버를 사용하여 Azure HDInsight의 Spark 클러스터에서 실행 중인 작업을 추적하고 디버깅합니다."
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
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="e37fa-103">Azure HDInsight에서 실행 중인 Apache Spark 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="e37fa-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="e37fa-104">이 문서에서는 YARN UI, Spark UI 및 Spark 기록 서버를 사용하여 HDInsight 클러스터에서 실행 중인 Spark 작업을 추적하고 디버깅하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="e37fa-105">이 문서의 경우 Spark 클러스터에서 사용할 수 있는 Notebook을 통해 Spark 작업(**기계 학습: MLLib를 사용하여 음식 검사 데이터에 대한 예측 분석**)을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="e37fa-106">**spark-submit**등 다른 방법을 사용하여 제출한 응용 프로그램을 추적하기 위해 이 단계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e37fa-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e37fa-107">Prerequisites</span></span>
<span data-ttu-id="e37fa-108">다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-108">You must have the following:</span></span>

* <span data-ttu-id="e37fa-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="e37fa-109">An Azure subscription.</span></span> <span data-ttu-id="e37fa-110">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e37fa-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e37fa-111">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e37fa-112">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e37fa-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="e37fa-113">Notebook, 즉 **[기계 학습: MLLib를 사용하여 음식 검사 데이터에 대한 예측 분석](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**을 실행하기 시작했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="e37fa-114">이 Notebook을 실행하는 방법은 링크를 따라갑니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="e37fa-115">YARN UI에서 응용 프로그램 추적</span><span class="sxs-lookup"><span data-stu-id="e37fa-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="e37fa-116">YARN UI를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-116">Launch the YARN UI.</span></span> <span data-ttu-id="e37fa-117">클러스터 블레이드에서 **클러스터 대시보드**, **YARN**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![YARN UI 시작](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="e37fa-119">또는 Ambari UI에서 YARN UI를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="e37fa-120">Ambari UI를 시작하려면 클러스터 블레이드에서 **클러스터 대시보드**, **HDInsight 클러스터 대시보드의**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="e37fa-121">Ambari UI에서 **YARN**, **빠른 링크**, 활성 리소스 관리자, **ResourceManager UI**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="e37fa-122">Jupyter Notebook을 사용하여 Spark 작업을 시작했기 때문에 응용 프로그램은 **remotesparkmagics** 이라는 이름을 갖게 됩니다(Notebook에서 시작된 모든 응용 프로그램에 대한 이름임).</span><span class="sxs-lookup"><span data-stu-id="e37fa-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="e37fa-123">응용 프로그램 이름에 대한 응용 프로그램 ID를 클릭하여 작업에 대한 자세한 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="e37fa-124">그러면 응용 프로그램 보기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-124">This launches the application view.</span></span>
   
    ![Spark 응용 프로그램 ID 찾기](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="e37fa-126">Jupyter Notebook에서 시작된 이러한 응용 프로그램의 경우 Notebook을 끝낼 때까지 상태는 항상 **실행 중** 입니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="e37fa-127">응용 프로그램 보기에서 응용 프로그램 및 로그 (stdout/stderr)와 연결된 컨테이너에 대해 알아보기 위해 더 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="e37fa-128">아래와 같이 **추적 URL**에 해당하는 연결을 클릭하여 Spark UI를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![컨테이너 로그 다운로드](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="e37fa-130">Spark UI에서 응용 프로그램 추적</span><span class="sxs-lookup"><span data-stu-id="e37fa-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="e37fa-131">Spark UI에서 이전에 시작한 응용 프로그램에 의해 생성된 Spark 작업을 더 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="e37fa-132">Spark UI를 시작하려면 응용 프로그램 보기에서 위의 화면 캡처에 표시된 것처럼 **추적 URL**에 대한 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="e37fa-133">Jupyter Notebook에서 실행 중인 응용 프로그램에 의해 시작되는 모든 Spark 작업을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Spark 작업 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="e37fa-135">**실행자** 탭을 클릭하여 각 실행자에 대한 처리 및 저장소 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="e37fa-136">**Thread Dump** 링크를 클릭하여 호출 스택을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Spark 실행자 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="e37fa-138">**단계** 탭을 클릭하여 응용 프로그램과 관련된 단계를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="e37fa-140">각 단계에서는 아래와 같이 실행 통계를 볼 수 있는 여러 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Spark 단계 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="e37fa-142">단계 세부 정보 페이지에서 DAG 시각화를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="e37fa-143">아래와 같이 페이지의 위쪽에서 **DAG 시각화** 링크를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Spark 단계 DAG 시각화 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="e37fa-145">DAG 또는 Direct Aclyic Graph는 응용 프로그램에서 다양한 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="e37fa-146">그래프의 파란색 상자는 각각 응용 프로그램에서 호출한 Spark 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="e37fa-147">단계 세부 정보 페이지에서 응용 프로그램 타임라인 보기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="e37fa-148">아래와 같이 페이지의 위쪽에서 **이벤트 타임라인** 링크를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Spark 단계 이벤트 타임라인 보기](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="e37fa-150">Spark 이벤트를 타임라인의 형태로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="e37fa-151">타임라인 보기는 작업, 작업 내, 단계 내 등 세 가지 수준에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="e37fa-152">위의 이미지는 지정된 단계에 대한 타임라인 보기를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e37fa-153">**확대/축소 사용** 확인란을 선택한 경우 타임라인 보기를 좌우로 스크롤할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="e37fa-154">Spark UI에서 다른 탭도 Spark 인스턴스에 대한 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="e37fa-155">저장소 탭 - 응용 프로그램이 RDD를 만드는 경우 저장소 탭에 대한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="e37fa-156">환경 탭 - 이 탭은 다음과 같이 Spark 인스턴스에 대한 유용한 정보를 많이 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="e37fa-157">Scala 버전</span><span class="sxs-lookup"><span data-stu-id="e37fa-157">Scala version</span></span>
     * <span data-ttu-id="e37fa-158">클러스터와 연결된 이벤트 로그 디렉터리</span><span class="sxs-lookup"><span data-stu-id="e37fa-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="e37fa-159">응용 프로그램에 대한 실행자 코어 수</span><span class="sxs-lookup"><span data-stu-id="e37fa-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="e37fa-160">등</span><span class="sxs-lookup"><span data-stu-id="e37fa-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="e37fa-161">Spark 기록 서버를 사용하여 완료된 작업에 대한 정보 찾기</span><span class="sxs-lookup"><span data-stu-id="e37fa-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="e37fa-162">작업이 완료되면 작업에 대한 정보는 Spark 기록 서버에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="e37fa-163">Spark 기록 서버를 시작하려면 클러스터 블레이드에서 **클러스터 대시보드**, **Spark 기록 서버**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="e37fa-165">또는 Ambari UI에서 Spark 기록 서버를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="e37fa-166">Ambari UI를 시작하려면 클러스터 블레이드에서 **클러스터 대시보드**, **HDInsight 클러스터 대시보드의**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="e37fa-167">Ambari UI에서 **Spark**, **빠른 링크**, **Spark 기록 서버 UI**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="e37fa-168">완료된 응용 프로그램을 모두 나열하여 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="e37fa-169">자세한 내용은 응용 프로그램 ID를 클릭하여 응용 프로그램에 대해 더 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e37fa-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Spark 기록 서버 시작](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="e37fa-171">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e37fa-171">See also</span></span>
*  [<span data-ttu-id="e37fa-172">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="e37fa-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="e37fa-173">데이터 분석가</span><span class="sxs-lookup"><span data-stu-id="e37fa-173">For data analysts</span></span>

* [<span data-ttu-id="e37fa-174">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="e37fa-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e37fa-175">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="e37fa-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e37fa-176">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="e37fa-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="e37fa-177">HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="e37fa-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="e37fa-178">분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용</span><span class="sxs-lookup"><span data-stu-id="e37fa-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="e37fa-179">Spark 개발자</span><span class="sxs-lookup"><span data-stu-id="e37fa-179">For Spark developers</span></span>

* [<span data-ttu-id="e37fa-180">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e37fa-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e37fa-181">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e37fa-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="e37fa-182">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="e37fa-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e37fa-183">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="e37fa-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e37fa-184">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="e37fa-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e37fa-185">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="e37fa-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e37fa-186">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="e37fa-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e37fa-187">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="e37fa-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e37fa-188">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="e37fa-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


