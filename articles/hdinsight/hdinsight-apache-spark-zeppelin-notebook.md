---
title: "Azure HDInsight에서 Apache Spark 클러스터와 함께 Zeppelin Notebook 사용 | Microsoft Docs"
description: "Azure HDInsight에서 Apache Spark 클러스터와 함께 Zeppelin Notebook을 사용하는 방법에 대한 단계별 지침입니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="96efd-103">Azure HDInsight에서 Apache Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="96efd-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="96efd-104">HDInsight Spark 클러스터에는 Spark 작업을 실행하는 데 사용할 수 있는 Zeppelin Notebook이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="96efd-105">이 문서에서는 HDInsight 클러스터에서 Zeppelin Notebook을 사용하는 방법에 대해 알아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="96efd-106">Zeppelin Notebook은 HDInsight 3.5의 Spark 1.6.3 및 HDInsight 3.6의 Spark 2.1.0에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="96efd-107">**필수 조건:**</span><span class="sxs-lookup"><span data-stu-id="96efd-107">**Prerequisites:**</span></span>

* <span data-ttu-id="96efd-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="96efd-108">An Azure subscription.</span></span> <span data-ttu-id="96efd-109">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96efd-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="96efd-110">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="96efd-111">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96efd-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="96efd-112">Zeppelin Notebook 시작</span><span class="sxs-lookup"><span data-stu-id="96efd-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="96efd-113">Spark 클러스터 블레이드에서 **클러스터 대시보드**를 클릭하고 **Zeppelin Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="96efd-114">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="96efd-115">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Zeppelin Notebook에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="96efd-116">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="96efd-117">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-117">Create a new notebook.</span></span> <span data-ttu-id="96efd-118">헤더 창에서 **노트북**을 클릭하고 **새 메모 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="96efd-119">![새 Zeppelin Notebook 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "새 Zeppelin Notebook 만들기")</span><span class="sxs-lookup"><span data-stu-id="96efd-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="96efd-120">Notebook 이름을 입력한 다음 **노트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="96efd-121">또한 Notebook 헤더에 연결된 상태가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="96efd-122">오른쪽 위 모서리에 녹색 점으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="96efd-123">![Zeppelin Notebook 상태](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 상태")</span><span class="sxs-lookup"><span data-stu-id="96efd-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="96efd-124">샘플 데이터를 임시 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="96efd-125">HDInsight에서 Spark 클러스터를 만들면 샘플 데이터 파일인 **hvac.csv**가 **\HdiSamples\SensorSampleData\hvac** 아래 연결된 저장소 계정에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="96efd-126">새 노트북에 기본적으로 만들어지는 빈 단락에 다음 코드 조각을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="96efd-127">**Shift + Enter**를 누르거나 단락에 대한 **재생** 단추를 클릭하여 코드 조각을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="96efd-128">단락의 오른쪽 모서리 상태가 준비, 보류 중, 실행 중, 완료 순서로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="96efd-129">출력은 같은 단락 하단에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="96efd-130">스크린샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="96efd-131">![원시 데이터에서 임시 테이블 만들기](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "원시 데이터에서 임시 테이블 만들기")</span><span class="sxs-lookup"><span data-stu-id="96efd-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="96efd-132">또한 각 단락에 제목을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="96efd-133">오른쪽 모서리에서 **설정** 아이콘을 클릭하고 **제목 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="96efd-134">이제 **hvac** 테이블에서 Spark SQL 문을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="96efd-135">새 단락에 다음 쿼리를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="96efd-136">이 쿼리는 지정된 날짜에서 각 건물에 대한 건물 ID와 대상 및 실제 온도 간의 차이를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="96efd-137">**Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="96efd-138">**%sql** 문의 처음 부분은 Notebook에 Livy Scala 인터프리터를 사용하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="96efd-139">다음 스크린샷은 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="96efd-140">![Notebook을 사용하여 Spark SQL 문 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Notebook을 사용하여 Spark SQL 문 실행")</span><span class="sxs-lookup"><span data-stu-id="96efd-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="96efd-141">동일한 출력에 대해 서로 다른 표현 간을 전환하려면 표시 옵션(사각형으로 강조 표시됨)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="96efd-142">**설정** 을 클릭하여 출력에서 키 및 값을 구성하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="96efd-143">위 화면 캡처에서는 **buildingID**를 키로, **temp_diff**의 평균을 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="96efd-144">또한 쿼리에 변수를 사용하여 Spark SQL 문을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="96efd-145">다음 코드 조각에서는 쿼리할 수 있는 값이 포함된 쿼리에 변수 **Temp**를 정의하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="96efd-146">쿼리를 처음 실행하면 드롭다운이 변수에 지정한 값으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="96efd-147">새 단락에 이 코드 조각을 붙여넣고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="96efd-148">다음 스크린샷은 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="96efd-149">![Notebook을 사용하여 Spark SQL 문 실행](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Notebook을 사용하여 Spark SQL 문 실행")</span><span class="sxs-lookup"><span data-stu-id="96efd-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="96efd-150">후속 쿼리에 대해서는 드롭다운에서 새 값을 선택하고 쿼리를 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="96efd-151">**설정** 을 클릭하여 출력에서 키 및 값을 구성하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="96efd-152">위 화면 캡처에서는 **buildingID**를 키로, **temp_diff**의 평균을 값으로, **targettemp**를 그룹으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="96efd-153">Livy 인터프리터를 다시 시작하여 응용 프로그램을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="96efd-154">이렇게 하려면 오른쪽 위 모서리의 로그인한 사용자 이름을 클릭하여 인터프리터 설정을 연 다음 **인터프리터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96efd-155">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="96efd-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="96efd-156">Livy 인터프리터 설정으로 스크롤한 다음 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="96efd-157">![Livy 인터프리터 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Zeppelin 인터프리터 다시 시작")</span><span class="sxs-lookup"><span data-stu-id="96efd-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="96efd-158">Notebook에서 외부 패키지 사용 방법</span><span class="sxs-lookup"><span data-stu-id="96efd-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="96efd-159">HDInsight(Linux)의 Apache Spark 클러스터에서 Zeppelin Notebook을 구성하여 클러스터에 포함되지 않는 외부의 커뮤니티 제공 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="96efd-160">사용할 수 있는 패키지의 전체 목록은 [Maven 리포지토리](http://search.maven.org/) 를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="96efd-161">다른 소스에서 사용 가능한 패키지 목록을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="96efd-162">예를 들어 커뮤니티 제공 패키지의 전체 목록은 [Spark 패키지](http://spark-packages.org/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="96efd-163">이 문서에서는 Jupyter Notebook에서 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 패키지를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="96efd-164">인터프리터 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-164">Open interpreter settings.</span></span> <span data-ttu-id="96efd-165">오른쪽 위 모서리의 로그인한 사용자 이름을 클릭한 다음 **인터프리터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96efd-166">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="96efd-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="96efd-167">Livy 인터프리터 설정으로 스크롤한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="96efd-168">![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "인터프리터 설정 변경")</span><span class="sxs-lookup"><span data-stu-id="96efd-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="96efd-169">**livy.spark.jars.packages**라는 새 키를 추가하고 그 값을 `group:id:version` 형식으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="96efd-170">따라서 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 패키지를 사용하려면 키 값을 `com.databricks:spark-csv_2.10:1.4.0`으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="96efd-171">![인터프리터 설정 변경](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "인터프리터 설정 변경")</span><span class="sxs-lookup"><span data-stu-id="96efd-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="96efd-172">**저장**을 클릭한 다음 Livy 인터프리터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="96efd-173">**팁**: 위에서 입력한 키 값에 도달하는 방법을 이해하려면 여기를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96efd-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="96efd-174">a.</span><span class="sxs-lookup"><span data-stu-id="96efd-174">a.</span></span> <span data-ttu-id="96efd-175">Maven Repository에서 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="96efd-176">이 자습서에서는 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="96efd-177">b.</span><span class="sxs-lookup"><span data-stu-id="96efd-177">b.</span></span> <span data-ttu-id="96efd-178">해당 리포지토리에서 **GroupId**, **ArtifactId** 및 **Version** 값을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="96efd-179">![Jupyter Notebook에서 외부 패키지 사용](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter Notebook에서 외부 패키지 사용")</span><span class="sxs-lookup"><span data-stu-id="96efd-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="96efd-180">c.</span><span class="sxs-lookup"><span data-stu-id="96efd-180">c.</span></span> <span data-ttu-id="96efd-181">콜론(**:**)으로 구분된 세 개의 값을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="96efd-182">Zeppelin Notebook 저장 위치</span><span class="sxs-lookup"><span data-stu-id="96efd-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="96efd-183">Zeppelin Notebook은 클러스터 헤드 노드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="96efd-184">따라서 클러스터를 삭제하면 Notebook도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="96efd-185">나중에 다른 클러스터에서 사용하기 위해 Notebook을 유지하려면 작업 실행을 완료 한 후 Notebook을 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="96efd-186">Notebook을 내보내려면 아래 이미지와 같이 **내보내기** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="96efd-187">![Notebook 다운로드](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Notebook 다운로드")</span><span class="sxs-lookup"><span data-stu-id="96efd-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="96efd-188">이렇게 하면 Notebook이 다운로드 위치에 JSON 파일로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="96efd-189">Livy 세션 관리</span><span class="sxs-lookup"><span data-stu-id="96efd-189">Livy session management</span></span>
<span data-ttu-id="96efd-190">Zeppelin Notebook에서 첫 번째 코드 단락을 실행하면 HDInsight Spark 클러스터에 새로운 Livy 세션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="96efd-191">이 세션은 이후에 만드는 모든 Zeppelin Notebook에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="96efd-192">클러스터 재부팅 등 어떤 이유로 Livy 세션이 종료되면 Zeppelin Notebook에서 작업을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="96efd-193">이 경우 Zeppelin Notebook에서 작업 실행을 시작하기 전에 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="96efd-194">Zeppelin Notebook에서 Livy 인터프리터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="96efd-195">이렇게 하려면 오른쪽 위 모서리의 로그인한 사용자 이름을 클릭하여 인터프리터 설정을 연 다음 **인터프리터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="96efd-196">![인터프리터 시작](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 출력")</span><span class="sxs-lookup"><span data-stu-id="96efd-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="96efd-197">Livy 인터프리터 설정으로 스크롤한 다음 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="96efd-198">![Livy 인터프리터 다시 시작](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Zeppelin 인터프리터 다시 시작")</span><span class="sxs-lookup"><span data-stu-id="96efd-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="96efd-199">기존 Zeppelin Notebook에서 코드 셀을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="96efd-200">이렇게 하면 HDInsight 클러스터에 새로운 Livy 세션이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="96efd-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="96efd-201"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="96efd-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="96efd-202">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="96efd-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="96efd-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="96efd-203">Scenarios</span></span>
* [<span data-ttu-id="96efd-204">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="96efd-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="96efd-205">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="96efd-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="96efd-206">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="96efd-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="96efd-207">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="96efd-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="96efd-208">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="96efd-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="96efd-209">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="96efd-209">Create and run applications</span></span>
* [<span data-ttu-id="96efd-210">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="96efd-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="96efd-211">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="96efd-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="96efd-212">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="96efd-212">Tools and extensions</span></span>
* [<span data-ttu-id="96efd-213">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="96efd-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="96efd-214">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="96efd-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="96efd-215">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="96efd-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="96efd-216">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="96efd-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="96efd-217">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="96efd-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="96efd-218">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="96efd-218">Manage resources</span></span>
* [<span data-ttu-id="96efd-219">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="96efd-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="96efd-220">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="96efd-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







