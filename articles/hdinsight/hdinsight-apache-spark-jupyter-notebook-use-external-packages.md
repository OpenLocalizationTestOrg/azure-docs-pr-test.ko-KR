---
title: "Azure HDInsight의 Spark에서 Jupyter와 함께 사용자 지정 Maven 패키지 사용 | Microsoft Docs"
description: "HDInsight Spark 클러스터에서 사용할 수 있는 Jupyter 노트북을 사용자 지정 Maven 패키지를 사용하도록 구성하는 방법에 대한 단계별 지침입니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="398d8-103">HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="398d8-104">셀 매직 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="398d8-105">스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="398d8-106">클러스터에 기본적으로 포함되지 않는 외부의 커뮤니티 제공 **maven** 패키지를 사용하도록 HDInsight의 Apache Spark 클러스터에 있는 Jupyter Notebook을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="398d8-107">사용할 수 있는 패키지의 전체 목록은 [Maven 리포지토리](http://search.maven.org/) 를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="398d8-108">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="398d8-109">예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="398d8-110">이 문서에서는 Jupyter 노트북에서 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 패키지를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="398d8-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="398d8-111">Prerequisites</span></span>
<span data-ttu-id="398d8-112">다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-112">You must have the following:</span></span>

* <span data-ttu-id="398d8-113">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="398d8-114">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="398d8-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="398d8-115">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="398d8-116">[Azure 포털](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터에 대한 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="398d8-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="398d8-117">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="398d8-118">Spark 클러스터 블레이드에서 **빠른 연결**을 클릭한 다음 **클러스터 대시보드** 블레이드에서 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="398d8-119">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="398d8-120">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="398d8-121">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="398d8-122">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-122">Create a new notebook.</span></span> <span data-ttu-id="398d8-123">**새로 만들기**를 클릭한 후 **Spark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="398d8-124">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="398d8-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="398d8-125">새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="398d8-126">맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="398d8-127">![노트북 이름 제공](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "노트북 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="398d8-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="398d8-128">`%%configure` Magic을 사용하여 외부 패키지를 사용하도록 Notebook을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="398d8-129">외부 패키지를 사용하는 Notebook에서 `%%configure` Magic을 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="398d8-130">이렇게 하면 커널은 세션이 시작되기 전에 패키지를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="398d8-131">첫 번째 셀에서 커널을 구성하는 것을 잊은 경우 `%%configure`과 `-f` 매개 변수를 사용할 수 있지만 세션이 다시 시작되고 모든 진행률이 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="398d8-132">HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="398d8-132">HDInsight version</span></span> | <span data-ttu-id="398d8-133">명령</span><span class="sxs-lookup"><span data-stu-id="398d8-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="398d8-134">HDInsight 3.3 및 HDInsight 3.4용</span><span class="sxs-lookup"><span data-stu-id="398d8-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="398d8-135">HDInsight 3.5용</span><span class="sxs-lookup"><span data-stu-id="398d8-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="398d8-136">위의 코드 조각에는 Maven Center Repository의 외부 패키지에 대한 Maven 좌표가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="398d8-137">이 코드 조각에서 `com.databricks:spark-csv_2.10:1.4.0` 는 **spark-csv** 패키지에 대한 Maven 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="398d8-138">패키지의 좌표를 생성하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="398d8-139">a.</span><span class="sxs-lookup"><span data-stu-id="398d8-139">a.</span></span> <span data-ttu-id="398d8-140">Maven Repository에서 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="398d8-141">이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="398d8-142">b.</span><span class="sxs-lookup"><span data-stu-id="398d8-142">b.</span></span> <span data-ttu-id="398d8-143">해당 리포지토리에서 **GroupId**, **ArtifactId** 및 **Version** 값을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="398d8-144">수집하는 값이 클러스터와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="398d8-145">이 경우에는 Scala 2.10 및 Spark 1.4.0 패키지를 사용하고 있지만 클러스터의 해당 Scala 또는 Spark 버전에 대해 다른 버전을 선택해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="398d8-146">Spark Jupyter 커널에서 또는 Spark 제출 시 `scala.util.Properties.versionString`을 실행하여 클러스터에서 Scala 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="398d8-147">Jupyter Notebook에서 `sc.version`을 실행하여 클러스터에서 Spark 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="398d8-148">![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")</span><span class="sxs-lookup"><span data-stu-id="398d8-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="398d8-149">c.</span><span class="sxs-lookup"><span data-stu-id="398d8-149">c.</span></span> <span data-ttu-id="398d8-150">콜론(**:**)으로 구분된 세 개의 값을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="398d8-151">`%%configure` Magic을 사용하여 코드 셀을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="398d8-152">이렇게 하면 제공된 패키지를 사용하도록 기본 Livy 세션이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="398d8-153">이제 아래와 같이 노트북의 다음 셀에서 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="398d8-154">아래와 같이 코드 조각을 실행하여 이전 단계에서 만든 데이터 프레임의 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="398d8-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="398d8-155"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="398d8-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="398d8-156">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="398d8-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="398d8-157">시나리오</span><span class="sxs-lookup"><span data-stu-id="398d8-157">Scenarios</span></span>
* [<span data-ttu-id="398d8-158">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="398d8-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="398d8-159">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="398d8-160">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="398d8-161">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="398d8-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="398d8-162">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="398d8-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="398d8-163">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="398d8-163">Create and run applications</span></span>
* [<span data-ttu-id="398d8-164">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="398d8-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="398d8-165">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="398d8-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="398d8-166">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="398d8-166">Tools and extensions</span></span>

* [<span data-ttu-id="398d8-167">HDInsight Linux의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 python 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="398d8-168">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="398d8-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="398d8-169">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="398d8-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="398d8-170">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="398d8-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="398d8-171">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="398d8-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="398d8-172">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="398d8-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="398d8-173">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="398d8-173">Manage resources</span></span>
* [<span data-ttu-id="398d8-174">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="398d8-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="398d8-175">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="398d8-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

