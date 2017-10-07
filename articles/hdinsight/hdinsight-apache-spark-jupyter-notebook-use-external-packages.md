---
title: "Azure HDInsight의 Spark에 Jupyter와 사용자 지정 Maven 패키지 aaaUse | Microsoft Docs"
description: "HDInsight Spark와 함께 사용할 수 있는 tooconfigure Jupyter 노트북 toouse 사용자 지정 Maven 패키지를 클러스터 하는 방법에 대해 단계별로 설명 합니다."
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="a1c72-103">HDInsight의 Apache Spark 클러스터에서 Jupyter Notebook과 함께 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1c72-104">셀 매직 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="a1c72-105">스크립트 작업 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="a1c72-106">자세한 방법을 tooconfigure HDInsight toouse 외부에 Apache Spark 클러스터에서 Jupyter 노트북 커뮤니티 제공 **maven** 하지 않은 패키지를 hello 클러스터에 기본적으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="a1c72-107">Hello를 검색할 수 있습니다 [Maven 리포지토리](http://search.maven.org/) 사용할 수 있는 패키지의 전체 목록은 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="a1c72-108">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="a1c72-109">예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="a1c72-110">이 문서에서는 살펴보겠습니다 어떻게 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter 노트북을 사용 하 여 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a1c72-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a1c72-111">Prerequisites</span></span>
<span data-ttu-id="a1c72-112">Hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-112">You must have hello following:</span></span>

* <span data-ttu-id="a1c72-113">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a1c72-114">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c72-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="a1c72-115">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="a1c72-116">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="a1c72-117">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="a1c72-118">Hello Spark 클러스터 블레이드에서 클릭 **빠른 링크**, 한 다음 hello **클러스터 대시보드** 블레이드에서 클릭 **Jupyter 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="a1c72-119">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1c72-120">또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="a1c72-121">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="a1c72-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="a1c72-122">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-122">Create a new notebook.</span></span> <span data-ttu-id="a1c72-123">**새로 만들기**를 클릭한 후 **Spark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="a1c72-124">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="a1c72-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="a1c72-125">새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="a1c72-126">Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="a1c72-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="a1c72-127">![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")</span><span class="sxs-lookup"><span data-stu-id="a1c72-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="a1c72-128">Hello를 사용 하 여 `%%configure` 매직 tooconfigure hello 노트북 toouse 외부 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="a1c72-129">외부 패키지를 사용 하는 노트북에서 hello 호출 되었는지 확인 `%%configure` hello 첫 번째 코드 셀에서 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="a1c72-130">이렇게 하면 해당 hello 커널 hello 세션이 시작 되기 전에 구성 된 toouse hello 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="a1c72-131">Hello hello 첫 번째 셀에 tooconfigure hello 커널 기억나지 않는 경우 사용할 수 있습니다 `%%configure` hello로 `-f` 매개 변수를 있었으나에 hello 세션 다시 시작 되 고 모든 진행률 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="a1c72-132">HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="a1c72-132">HDInsight version</span></span> | <span data-ttu-id="a1c72-133">명령</span><span class="sxs-lookup"><span data-stu-id="a1c72-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="a1c72-134">HDInsight 3.3 및 HDInsight 3.4용</span><span class="sxs-lookup"><span data-stu-id="a1c72-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="a1c72-135">HDInsight 3.5용</span><span class="sxs-lookup"><span data-stu-id="a1c72-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="a1c72-136">위의 코드 조각 hello Maven 중앙 리포지토리에 hello 외부 패키지에 대 한 hello maven 좌표는 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="a1c72-137">이 코드 조각 `com.databricks:spark-csv_2.10:1.4.0` hello maven 좌표에 대 한 **spark csv** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="a1c72-138">패키지에 대 한 hello 좌표를 구성 하는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="a1c72-139">a.</span><span class="sxs-lookup"><span data-stu-id="a1c72-139">a.</span></span> <span data-ttu-id="a1c72-140">Maven 리포지토리 hello hello 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="a1c72-141">이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="a1c72-142">b.</span><span class="sxs-lookup"><span data-stu-id="a1c72-142">b.</span></span> <span data-ttu-id="a1c72-143">에 대 한 hello 값을 수집 hello 리포지토리에서 **GroupId**, **의 ArtifactId**, 및 **버전**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="a1c72-144">Hello 값을 수집 하 여 클러스터와 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="a1c72-145">이 경우 Scala 2.10 및 Spark 1.4.0 패키지를 사용 하는 것 이지만 클러스터의 hello 적절 한 Scala 또는 Spark 버전에 대 한 tooselect 서로 다른 버전을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="a1c72-146">확인할 수 있습니다 hello Scala 버전 클러스터에서 실행 하 여 `scala.util.Properties.versionString` hello Spark Jupyter 커널 또는 Spark 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="a1c72-147">확인할 수 있습니다 hello Spark 버전 클러스터에서 실행 하 여 `sc.version` Jupyter 노트북에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="a1c72-148">![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")</span><span class="sxs-lookup"><span data-stu-id="a1c72-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="a1c72-149">c.</span><span class="sxs-lookup"><span data-stu-id="a1c72-149">c.</span></span> <span data-ttu-id="a1c72-150">콜론으로 구분 하는 hello 3 값 연결 (**:**).</span><span class="sxs-lookup"><span data-stu-id="a1c72-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="a1c72-151">Hello를 사용 하 여 hello 코드 셀 실행 `%%configure` 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="a1c72-152">이렇게 하면 hello 기본 리비 세션 toouse hello 패키지 사용자가 제공한 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="a1c72-153">Hello 전자 필기장의 후속 셀 hello에에서 아래와 같이 hello 패키지를 지금 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="a1c72-154">Hello 조각을 실행할 수 있습니다, tooview, 아래 그림과 같이 hello hello 데이터 프레임에서 데이터 단계에서 만든 hello 이전 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="a1c72-155"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="a1c72-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a1c72-156">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="a1c72-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a1c72-157">시나리오</span><span class="sxs-lookup"><span data-stu-id="a1c72-157">Scenarios</span></span>
* [<span data-ttu-id="a1c72-158">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="a1c72-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a1c72-159">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a1c72-160">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="a1c72-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a1c72-161">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="a1c72-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a1c72-162">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="a1c72-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a1c72-163">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="a1c72-163">Create and run applications</span></span>
* [<span data-ttu-id="a1c72-164">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a1c72-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a1c72-165">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a1c72-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a1c72-166">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="a1c72-166">Tools and extensions</span></span>

* [<span data-ttu-id="a1c72-167">HDInsight Linux의 Apache Spark 클러스터에서 Jupyter 노트북과 함께 외부 python 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="a1c72-168">IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출</span><span class="sxs-lookup"><span data-stu-id="a1c72-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a1c72-169">IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a1c72-170">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="a1c72-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a1c72-171">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="a1c72-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a1c72-172">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a1c72-173">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="a1c72-173">Manage resources</span></span>
* [<span data-ttu-id="a1c72-174">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1c72-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a1c72-175">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="a1c72-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

