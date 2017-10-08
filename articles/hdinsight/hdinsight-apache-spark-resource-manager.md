---
title: "Azure HDInsight의 Apache Spark에 대 한 aaaManage 리소스 클러스터 | Microsoft Docs"
description: "Toouse 성능 향상을 위해 Azure HDInsight의 Spark 클러스터에 대 한 리소스를 관리 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="b5536-103">Azure HDInsight에서 Apache Spark 클러스터용 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="b5536-103">Manage resources for Apache Spark cluster on Azure HDInsight</span></span> 

<span data-ttu-id="b5536-104">이 문서에서 Ambari UI, YARN UI 및 hello Spark 기록 서버와 같은 tooaccess hello 인터페이스 Spark 클러스터와 연결 된 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-104">In this article you will learn how tooaccess hello interfaces like Ambari UI, YARN UI, and hello Spark History Server associated with your Spark cluster.</span></span> <span data-ttu-id="b5536-105">어떻게 tootune hello 최적의 성능을 위해 클러스터 구성에 대 한 배우게 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-105">You will also learn about how tootune hello cluster configuration for optimal performance.</span></span>

<span data-ttu-id="b5536-106">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="b5536-106">**Prerequisites:**</span></span>

<span data-ttu-id="b5536-107">Hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-107">You must have hello following:</span></span>

* <span data-ttu-id="b5536-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b5536-108">An Azure subscription.</span></span> <span data-ttu-id="b5536-109">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5536-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b5536-110">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b5536-111">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5536-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-do-i-launch-hello-ambari-web-ui"></a><span data-ttu-id="b5536-112">Hello Ambari 웹 UI를 시작 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="b5536-112">How do I launch hello Ambari Web UI?</span></span>
1. <span data-ttu-id="b5536-113">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-113">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="b5536-114">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-114">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>
2. <span data-ttu-id="b5536-115">Hello Spark 클러스터 블레이드에서 클릭 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-115">From hello Spark cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="b5536-116">메시지가 표시 되 면 hello Spark 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-116">When prompted, enter hello admin credentials for hello Spark cluster.</span></span>

    <span data-ttu-id="b5536-117">![Ambari 시작](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Resource Manager 시작")</span><span class="sxs-lookup"><span data-stu-id="b5536-117">![Launch Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Start Resource Manager")</span></span>
3. <span data-ttu-id="b5536-118">이 아래와 같이 hello Ambari 웹 UI를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-118">This should launch hello Ambari Web UI, as shown below.</span></span>

    <span data-ttu-id="b5536-119">![Ambari 웹 UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari 웹 UI")</span><span class="sxs-lookup"><span data-stu-id="b5536-119">![Ambari Web UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")</span></span>   

## <a name="how-do-i-launch-hello-spark-history-server"></a><span data-ttu-id="b5536-120">Spark 기록 서버 hello을 시작 하는 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="b5536-120">How do I launch hello Spark History Server?</span></span>
1. <span data-ttu-id="b5536-121">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-121">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span>
2. <span data-ttu-id="b5536-122">Hello에서 블레이드에서 아래에서 클러스터 **빠른 링크**, 클릭 **클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-122">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**.</span></span> <span data-ttu-id="b5536-123">Hello에 **클러스터 대시보드** 블레이드에서 클릭 **Spark 기록 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-123">In hello **Cluster Dashboard** blade, click **Spark History Server**.</span></span>

    <span data-ttu-id="b5536-124">![Spark 기록 서버](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark 기록 서버")</span><span class="sxs-lookup"><span data-stu-id="b5536-124">![Spark History Server](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span></span>

    <span data-ttu-id="b5536-125">메시지가 표시 되 면 hello Spark 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-125">When prompted, enter hello admin credentials for hello Spark cluster.</span></span>

## <a name="how-do-i-launch-hello-yarn-ui"></a><span data-ttu-id="b5536-126">Hello Yarn UI를 시작 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="b5536-126">How do I launch hello Yarn UI?</span></span>
<span data-ttu-id="b5536-127">Hello Spark 클러스터에서 현재 실행 중인 hello YARN UI toomonitor 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-127">You can use hello YARN UI toomonitor applications that are currently running on hello Spark cluster.</span></span>

1. <span data-ttu-id="b5536-128">Hello 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **YARN**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-128">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>

    ![YARN UI 시작](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > <span data-ttu-id="b5536-130">또는 hello Ambari UI에서에서 hello YARN UI를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-130">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="b5536-131">hello 클러스터 블레이드에서 toolaunch hello Ambari UI 클릭 **클러스터 대시보드**, 클릭 하 고 **HDInsight 클러스터 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-131">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="b5536-132">Ambari UI hello에서 클릭 **YARN**, 클릭 **빠른 링크**, hello 활성 리소스 관리자를 클릭 하 고 클릭 **ResourceManager UI**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-132">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a><span data-ttu-id="b5536-133">Hello 최적 클러스터 구성 toorun Spark 응용 프로그램 이란?</span><span class="sxs-lookup"><span data-stu-id="b5536-133">What is hello optimum cluster configuration toorun Spark applications?</span></span>
<span data-ttu-id="b5536-134">응용 프로그램 요구 사항에 따라 Spark 구성에 대해 사용할 수 있는 세 hello 키 매개 변수는 `spark.executor.instances`, `spark.executor.cores`, 및 `spark.executor.memory`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-134">hello three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span></span> <span data-ttu-id="b5536-135">실행자는 Spark 응용 프로그램을 위해 시작된 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-135">An Executor is a process launched for a Spark application.</span></span> <span data-ttu-id="b5536-136">Hello 작업자 노드에서 실행 되며 hello 작업 hello 응용 프로그램에 대 한 책임 toocarry 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-136">It runs on hello worker node and is responsible toocarry out hello tasks for hello application.</span></span> <span data-ttu-id="b5536-137">단일 실행 및 각 클러스터에 대 한 hello 실행자 크기 hello 기본 수는 hello 수 작업자 노드 및 hello 작업자 노드 크기에 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-137">hello default number of executors and hello executor sizes for each cluster is calculated based on hello number of worker nodes and hello worker node size.</span></span> <span data-ttu-id="b5536-138">에 저장 됩니다 `spark-defaults.conf` hello 클러스터 헤드 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-138">These are stored in `spark-defaults.conf` on hello cluster head nodes.</span></span>

<span data-ttu-id="b5536-139">hello 구성 매개 변수 3 개 (hello 클러스터에서 실행 하는 모든 응용 프로그램)에 대 한 hello 클러스터 수준에서 구성할 수 있습니다 또는 에서도 각 개별 응용 프로그램에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-139">hello three configuration parameters can be configured at hello cluster level (for all applications that run on hello cluster) or can be specified for each individual application as well.</span></span>

### <a name="change-hello-parameters-using-ambari-ui"></a><span data-ttu-id="b5536-140">Ambari UI를 사용 하 여 hello 매개 변수 변경</span><span class="sxs-lookup"><span data-stu-id="b5536-140">Change hello parameters using Ambari UI</span></span>
1. <span data-ttu-id="b5536-141">Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **Configs**, 펼친 다음 **사용자 지정 spark 기본값**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-141">From hello Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span></span>

    ![Ambari를 사용하여 매개 변수 설정](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. <span data-ttu-id="b5536-143">hello 기본값은 좋은 toohave 4 Spark 응용 프로그램 hello 클러스터에서 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-143">hello default values are good toohave 4 Spark applications run concurrently on hello cluster.</span></span> <span data-ttu-id="b5536-144">변경할 수 있습니다 이러한 값 hello 사용자 인터페이스에서 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-144">You can changes these values from hello user interface, as shown below.</span></span>

    ![Ambari를 사용하여 매개 변수 설정](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. <span data-ttu-id="b5536-146">클릭 **저장** toosave hello 구성 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-146">Click **Save** toosave hello configuration changes.</span></span> <span data-ttu-id="b5536-147">Hello 페이지의 hello 위쪽 나타납니다 toorestart hello 모든 영향을 받는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-147">At hello top of hello page, you will be prompted toorestart all hello affected services.</span></span> <span data-ttu-id="b5536-148">**다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-148">Click **Restart**.</span></span>

    ![서비스 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a><span data-ttu-id="b5536-150">Jupyter 노트북에서 실행 중인 응용 프로그램에 대 한 hello 매개 변수 변경</span><span class="sxs-lookup"><span data-stu-id="b5536-150">Change hello parameters for an application running in Jupyter notebook</span></span>
<span data-ttu-id="b5536-151">Hello Jupyter 노트북에서 실행 중인 응용 프로그램에서는 hello를 사용할 수 있습니다 `%%configure` 매직 toomake hello 구성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-151">For applications running in hello Jupyter notebook, you can use hello `%%configure` magic toomake hello configuration changes.</span></span> <span data-ttu-id="b5536-152">이상적으로 코드 첫 번째 셀을 실행 하기 전에 hello 응용 프로그램의 hello 시작 부분에서 이러한 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-152">Ideally, you must make such changes at hello beginning of hello application, before you run your first code cell.</span></span> <span data-ttu-id="b5536-153">이렇게 하면 해당 hello 구성이 적용 된 toohello 리비 세션을 만들 때 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-153">This ensures that hello configuration is applied toohello Livy session, when it gets created.</span></span> <span data-ttu-id="b5536-154">Hello를 사용 해야 hello 응용 프로그램의 이후 단계에서 toochange hello 구성 하려는 경우 `-f` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-154">If you want toochange hello configuration at a later stage in hello application, you must use hello `-f` parameter.</span></span> <span data-ttu-id="b5536-155">그러나 hello에 진행 되는 모든 하므로 실행 하 여 응용 프로그램 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-155">However, by doing so all progress in hello application will be lost.</span></span>

<span data-ttu-id="b5536-156">아래 hello 조각 toochange Jupyter 실행 중인 응용 프로그램에 대 한 구성을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-156">hello snippet below shows how toochange hello configuration for an application running in Jupyter.</span></span>

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

<span data-ttu-id="b5536-157">구성 매개 변수를 JSON 문자열로 전달 해야 하며 hello 예에서는 열에 표시 된 것 처럼 hello 매직 후 hello 다음 줄에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-157">Configuration parameters must be passed in as a JSON string and must be on hello next line after hello magic, as shown in hello example column.</span></span>

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a><span data-ttu-id="b5536-158">사용 하 여 전송할 응용 프로그램에 대 한 매개 변수를 변경 hello spark 제출</span><span class="sxs-lookup"><span data-stu-id="b5536-158">Change hello parameters for an application submitted using spark-submit</span></span>
<span data-ttu-id="b5536-159">Toochange 구성 매개 변수를 사용 하 여 전송 된 일괄 처리 응용 프로그램에 대 한 hello 하는 방법의 예는 다음 명령을 `spark-submit`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-159">Following command is an example of how toochange hello configuration parameters for a batch application that is submitted using `spark-submit`.</span></span>

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a><span data-ttu-id="b5536-160">CURL을 사용 하 여 전송할 응용 프로그램에 대 한 hello 매개 변수 변경</span><span class="sxs-lookup"><span data-stu-id="b5536-160">Change hello parameters for an application submitted using cURL</span></span>
<span data-ttu-id="b5536-161">다음 명령을 toochange cURL을 사용 하 여 사용 하 여 전송 된 일괄 처리 응용 프로그램에 대 한 구성 매개 변수를 hello 하는 방법의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-161">Following command is an example of how toochange hello configuration parameters for a batch application that is submitted using using cURL.</span></span>

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a><span data-ttu-id="b5536-162">Spark Thrift 서버에서 이러한 매개 변수를 변경하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b5536-162">How do I change these parameters on a Spark Thrift Server?</span></span>
<span data-ttu-id="b5536-163">Spark Thrift 서버 제공 JDBC/ODBC 액세스 tooa Spark 클러스터 하며 사용 되는 tooservice Spark SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-163">Spark Thrift Server provides JDBC/ODBC access tooa Spark cluster and is used tooservice Spark SQL queries.</span></span> <span data-ttu-id="b5536-164">Power BI, Tableau 등과 같은 도구는</span><span class="sxs-lookup"><span data-stu-id="b5536-164">Tools like Power BI, Tableau etc.</span></span> <span data-ttu-id="b5536-165">Spark Thrift 서버 tooexecute Spark SQL 쿼리로 프로토콜 toocommunicate ODBC를 사용 하 여 Spark 응용 프로그램으로.</span><span class="sxs-lookup"><span data-stu-id="b5536-165">use ODBC protocol toocommunicate with Spark Thrift Server tooexecute Spark SQL queries as a Spark Application.</span></span> <span data-ttu-id="b5536-166">Spark 클러스터를 만들 때 두 인스턴스의 각 헤드 노드에서 하나 hello Spark Thrift 서버가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-166">When a Spark cluster is created, two instances of hello Spark Thrift Server are started, one on each head node.</span></span> <span data-ttu-id="b5536-167">각 Spark Thrift 서버 hello YARN UI에서에서 Spark 응용 프로그램으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-167">Each Spark Thrift Server is visible as a Spark application in hello YARN UI.</span></span>

<span data-ttu-id="b5536-168">Spark Thrift 서버는 동적 실행자 할당 멤버를 사용 하며 따라서 hello `spark.executor.instances` 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-168">Spark Thrift Server uses Spark dynamic executor allocation and hence hello `spark.executor.instances` is not used.</span></span> <span data-ttu-id="b5536-169">Spark Thrift 서버 대신 사용 하 여 `spark.dynamicAllocation.minExecutors` 및 `spark.dynamicAllocation.maxExecutors` toospecify hello 실행 기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` toospecify hello executor count.</span></span> <span data-ttu-id="b5536-170">구성 매개 변수를 hello `spark.executor.cores` 및 `spark.executor.memory` 은 toomodify hello 실행자 크기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-170">hello configuration parameters `spark.executor.cores` and `spark.executor.memory` is used toomodify hello executor size.</span></span> <span data-ttu-id="b5536-171">아래와 같이 이러한 매개 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-171">You can change these parameters as shown below.</span></span>

* <span data-ttu-id="b5536-172">Hello 확장 **spark-thrift-sparkconf 고급** 범주 tooupdate hello 매개 변수 `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, 및 `spark.executor.memory`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-172">Expand hello **Advanced spark-thrift-sparkconf** category tooupdate hello parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span></span>

    ![Spark Thrift 서버 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* <span data-ttu-id="b5536-174">Hello 확장 **사용자 지정 spark thrift sparkconf** 범주 tooupdate hello 매개 변수 `spark.executor.cores`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-174">Expand hello **Custom spark-thrift-sparkconf** category tooupdate hello parameter `spark.executor.cores`.</span></span>

    ![Spark Thrift 서버 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a><span data-ttu-id="b5536-176">Spark Thrift 서버 hello의 hello 드라이버 메모리를 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="b5536-176">How do I change hello driver memory of hello Spark Thrift Server?</span></span>
<span data-ttu-id="b5536-177">Spark Thrift 서버 드라이버 메모리는 제공 된 hello hello 헤드 노드의 총 RAM 크기는 14 GB 보다 큰 구성된 too25 %hello 헤드 노드 RAM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-177">Spark Thrift Server driver memory is configured too25% of hello head node RAM size, provided hello total RAM size of hello head node is greater than 14GB.</span></span> <span data-ttu-id="b5536-178">아래와 같이 hello Ambari UI toochange hello 드라이버 메모리 내 구성에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-178">You can use hello Ambari UI toochange hello driver memory configuration, as shown below.</span></span>

* <span data-ttu-id="b5536-179">Hello Ambari UI에서에서 클릭 **Spark**, 클릭 **Configs**, 확장 **spark env 고급**, 다음에 대 한 hello 값을 제공 하 고 **spark_thrift_cmd_opts**.</span><span class="sxs-lookup"><span data-stu-id="b5536-179">From hello Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide hello value for **spark_thrift_cmd_opts**.</span></span>

    ![Spark Thrift 서버 RAM 구성](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a><span data-ttu-id="b5536-181">Spark 클러스터와 함께 BI를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-181">I do not use BI with Spark cluster.</span></span> <span data-ttu-id="b5536-182">Hello 리소스를 다시 사용지 않습니다는 방법</span><span class="sxs-lookup"><span data-stu-id="b5536-182">How do I take hello resources back?</span></span>
<span data-ttu-id="b5536-183">Spark 동적 할당을 사용 하므로 hello만 thrift 서버에서 사용 하는 리소스가 두 응용 프로그램 마스터 hello에 대 한 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-183">Since we use Spark dynamic allocation, hello only resources that are consumed by thrift server are hello resources for hello two application masters.</span></span> <span data-ttu-id="b5536-184">tooreclaim hello 클러스터에서 실행 중인 Thrift 서버 서비스를 hello 이러한 리소스를 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-184">tooreclaim these resources you must stop hello Thrift Server services running on hello cluster.</span></span>

1. <span data-ttu-id="b5536-185">Hello 왼쪽된 창에서 hello Ambari UI에서에서 클릭 **Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-185">From hello Ambari UI, from hello left pane, click **Spark**.</span></span>
2. <span data-ttu-id="b5536-186">Hello 다음 페이지에서 클릭 **Spark Thrift 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-186">In hello next page, click **Spark Thrift Servers**.</span></span>

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. <span data-ttu-id="b5536-188">Spark Thrift 서버가 실행 중인 어떤 hello hello 두 headnodes를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-188">You should see hello two headnodes on which hello Spark Thrift Server is running.</span></span> <span data-ttu-id="b5536-189">Hello headnodes 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-189">Click one of hello headnodes.</span></span>

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. <span data-ttu-id="b5536-191">다음 페이지 hello 해당 헤드 노드에에서 실행 중인 모든 hello 서비스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-191">hello next page lists all hello services running on that headnode.</span></span> <span data-ttu-id="b5536-192">Hello 목록에서 hello 드롭 다운 단추 다음 tooSpark Thrift 서버를 클릭 한 다음 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-192">From hello list click hello drop-down button next tooSpark Thrift Server, and then click **Stop**.</span></span>

    ![Thrift 서버 다시 시작](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. <span data-ttu-id="b5536-194">다른 헤드 노드에 hello에서 이러한 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-194">Repeat these steps on hello other headnode as well.</span></span>

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a><span data-ttu-id="b5536-195">내 Jupyter Notebook이 예상대로 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-195">My Jupyter notebooks are not running as expected.</span></span> <span data-ttu-id="b5536-196">Hello 서비스를 다시 시작할 수는 방법</span><span class="sxs-lookup"><span data-stu-id="b5536-196">How can I restart hello service?</span></span>
<span data-ttu-id="b5536-197">위와 같이 hello Ambari 웹 UI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-197">Launch hello Ambari Web UI as shown above.</span></span> <span data-ttu-id="b5536-198">Hello 왼쪽된 탐색 창에서 클릭 **Jupyter**, 클릭 **서비스 작업**, 클릭 하 고 **모든 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-198">From hello left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span></span> <span data-ttu-id="b5536-199">모든 hello headnodes에 hello Jupyter service가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-199">This will start hello Jupyter service on all hello headnodes.</span></span>

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a><span data-ttu-id="b5536-200">리소스가 부족한지 어떻게 알 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b5536-200">How do I know if I am running out of resources?</span></span>
<span data-ttu-id="b5536-201">위와 같이 hello Yarn UI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-201">Launch hello Yarn UI as shown above.</span></span> <span data-ttu-id="b5536-202">Hello 화면 위로 클러스터 메트릭 표에 값을 확인 **사용 메모리** 및 **총 메모리** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-202">In Cluster Metrics table on top of hello screen, check values of **Memory Used** and **Memory Total** columns.</span></span> <span data-ttu-id="b5536-203">Hello 2 값이 매우 유사 하지 될 충분 한 리소스 toostart hello 다음 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-203">If hello 2 values are very close, there might not be enough resources toostart hello next application.</span></span> <span data-ttu-id="b5536-204">hello에 마찬가지 toohello **VCores 사용** 및 **VCores 총** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-204">hello same applies toohello **VCores Used** and **VCores Total** columns.</span></span> <span data-ttu-id="b5536-205">또한 hello 주 보기에 없는 경우 응용 프로그램에 그대로 유지 **"승인 됨"** 상태 및으로 전환 되지 **실행** 나 **실패** 상태 이면이 수도 있는 것일 수 에 충분 한 리소스 toostart를 얻을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-205">Also, in hello main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources toostart.</span></span>

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a><span data-ttu-id="b5536-206">실행 중인을 kill 어떻게 리소스를 응용 프로그램 toofree?</span><span class="sxs-lookup"><span data-stu-id="b5536-206">How do I kill a running application toofree up resource?</span></span>
1. <span data-ttu-id="b5536-207">Hello 왼쪽된 패널에서 hello Yarn UI 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-207">In hello Yarn UI, from hello left panel, click **Running**.</span></span> <span data-ttu-id="b5536-208">실행 중인 응용 프로그램의 hello 목록에서 응용 프로그램 toobe hello 종료 하 고 hello에서 클릭 결정 **ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-208">From hello list of running applications, determine hello application toobe killed and click on hello **ID**.</span></span>

    <span data-ttu-id="b5536-209">![App1 종료](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "App1 종료")</span><span class="sxs-lookup"><span data-stu-id="b5536-209">![Kill App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")</span></span>

2. <span data-ttu-id="b5536-210">클릭 **응용 프로그램을 중지** hello 오른쪽 위 모퉁이 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-210">Click **Kill Application** on hello top right corner, then click **OK**.</span></span>

    <span data-ttu-id="b5536-211">![App2 종료](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "App2 종료")</span><span class="sxs-lookup"><span data-stu-id="b5536-211">![Kill App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")</span></span>

## <a name="see-also"></a><span data-ttu-id="b5536-212">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b5536-212">See also</span></span>
* [<span data-ttu-id="b5536-213">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="b5536-213">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a><span data-ttu-id="b5536-214">데이터 분석가</span><span class="sxs-lookup"><span data-stu-id="b5536-214">For data analysts</span></span>

* [<span data-ttu-id="b5536-215">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="b5536-215">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b5536-216">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="b5536-216">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b5536-217">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="b5536-217">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="b5536-218">HDInsight에서 Spark를 사용하는 Application Insight 원격 분석 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="b5536-218">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="b5536-219">분산 심층 학습을 위해 Azure HDInsight Spark에서 Caffe 사용</span><span class="sxs-lookup"><span data-stu-id="b5536-219">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="b5536-220">Spark 개발자</span><span class="sxs-lookup"><span data-stu-id="b5536-220">For Spark developers</span></span>

* [<span data-ttu-id="b5536-221">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b5536-221">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b5536-222">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="b5536-222">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="b5536-223">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="b5536-223">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b5536-224">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="b5536-224">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b5536-225">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="b5536-225">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b5536-226">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="b5536-226">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b5536-227">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="b5536-227">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b5536-228">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="b5536-228">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b5536-229">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5536-229">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
