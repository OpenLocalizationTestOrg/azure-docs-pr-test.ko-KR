---
title: "Azure HDInsight Spark 클러스터에서 대화형 쿼리 실행 | Microsoft Docs"
description: "HDInsight에서 Apache Spark 클러스터를 만드는 방법에 대한 HDInsight Spark 빠른 시작입니다."
keywords: "spark 빠른 시작, 대화형 spark, 대화형 쿼리, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ada1c3d1482c68834dbbf5eabbd045a7e0c01f9f
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="3c69e-104">HDInsight Spark 클러스터에서 대화형 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="3c69e-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="3c69e-105">이 문서에서는 Jupyter 노트북을 사용하여 Spark 클러스터에 대해 대화형 Spark SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-105">In this article, you use a Jupyter notebook to run interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="3c69e-106">Jupyter 노트북은 콘솔 기반 대화형 환경을 웹으로 확장하는 브라우저 기반 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-106">Jupyter notebook is a browser-based application that extends the console-based interactive experience to the Web.</span></span> <span data-ttu-id="3c69e-107">자세한 내용은 [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html)(Jupyter 노트북)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c69e-107">For more information, see [The Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="3c69e-108">이 자습서에서는 Jupyter 노트북에서 **PySpark** 커널을 사용하여 대화형 Spark SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-108">For this tutorial, you use the **PySpark** kernel in the Jupyter notebook to run an interactive Spark SQL query.</span></span> <span data-ttu-id="3c69e-109">HDInsight 클러스터의 Jupyter 노트북은 **PySpark3** 및 **Spark**의 두 가지 다른 커널도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="3c69e-110">커널 및 **PySpark** 사용의 이점에 대한 자세한 내용은 [HDInsight에서 Apache Spark 클러스터와 함께 Jupyter Notebook 커널 사용](hdinsight-apache-spark-jupyter-notebook-kernels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c69e-110">For more information about the kernels, and the benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c69e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3c69e-111">Prerequisites</span></span>

* <span data-ttu-id="3c69e-112">**Azure HDInsight Spark 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="3c69e-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="3c69e-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c69e-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-to-run-interactive-queries"></a><span data-ttu-id="3c69e-114">대화형 쿼리를 실행할 Jupyter 노트북 만들기</span><span class="sxs-lookup"><span data-stu-id="3c69e-114">Create a Jupyter notebook to run interactive queries</span></span>

<span data-ttu-id="3c69e-115">쿼리를 실행하기 위해 여기서는 클러스터와 연결된 저장소에서 기본적으로 제공되는 예제 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-115">To run queries, we use sample data that is by default available in the storage associated with the cluster.</span></span> <span data-ttu-id="3c69e-116">그러나 먼저 데이터를 Spark에 데이터 프레임으로 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="3c69e-117">데이터 프레임이 있으면 Jupyter 노트북을 사용하여 이 프레임에 대한 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-117">Once you have the dataframe, you can run queries on it using the Jupyter notebook.</span></span> <span data-ttu-id="3c69e-118">이 섹션에서는 다음을 수행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="3c69e-119">예제 데이터 집합을 Spark 데이터 프레임으로 등록</span><span class="sxs-lookup"><span data-stu-id="3c69e-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="3c69e-120">데이터 프레임에 대한 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="3c69e-120">Run queries on the dataframe.</span></span>

1. <span data-ttu-id="3c69e-121">[Azure 포털](https://portal.azure.com/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-121">Open the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3c69e-122">클러스터를 대시보드에 고정하도록 선택한 경우 대시보드에서 클러스터 타일을 클릭하여 클러스터 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-122">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="3c69e-123">클러스터를 대시보드에 고정하지 않은 경우 왼쪽 창에서 **HDInsight 클러스터**를 클릭한 후 만든 클러스터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-123">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="3c69e-124">**빠른 링크**에서 **클러스터 대시보드**를 클릭한 다음 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="3c69e-125">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-125">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="3c69e-126">![Jupyter 노트북을 열어 대화형 Spark SQL 쿼리 실행](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Jupyter 노트북을 열어 대화형 Spark SQL 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="3c69e-126">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c69e-127">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter 노트북에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-127">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="3c69e-128">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-128">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="3c69e-129">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-129">Create a notebook.</span></span> <span data-ttu-id="3c69e-130">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="3c69e-131">![Jupyter 노트북을 만들어 대화형 Spark SQL 쿼리 실행](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter 노트북을 만들어 대화형 Spark SQL 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="3c69e-131">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="3c69e-132">새 노트북이 만들어지고 Untitled(Untitled.pynb) 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-132">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="3c69e-133">맨 위에서 노트북 이름을 클릭하고 원하는 경우 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-133">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="3c69e-134">![Jupter 노트북에 대한 이름을 제공하여 대화형 Spark 쿼리 실행](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Jupter 노트북에 대한 이름을 제공하여 대화형 Spark 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="3c69e-134">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5. <span data-ttu-id="3c69e-135">빈 셀에 다음 코드를 붙여 넣은 다음 **SHIFT + ENTER**를 눌러 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-135">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="3c69e-136">코드는 이 시나리오에 필요한 형식을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-136">The code imports the types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="3c69e-137">PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-137">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="3c69e-138">첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-138">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span>

    <span data-ttu-id="3c69e-139">![대화형 Spark SQL 쿼리 상태](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "대화형 Spark SQL 쿼리 상태")</span><span class="sxs-lookup"><span data-stu-id="3c69e-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="3c69e-140">Jupyter에서 대화형 쿼리를 실행할 때마다, 웹 브라우저 창 제목에 노트북 제목과 함께 **(사용 중)** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="3c69e-141">또한 오른쪽 위 모서리에 있는 **PySpark** 텍스트 옆에 단색 원이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-141">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="3c69e-142">작업이 완료되면 속이 빈 원으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-142">After the job is completed, it changes to a hollow circle.</span></span>

6. <span data-ttu-id="3c69e-143">Spark 클러스터로 데이터를 로드하기 전에 데이터의 스냅숏을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-143">Before you load the data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="3c69e-144">이 자습서에서 사용하는 예제 데이터는 모든 HDInsight Spark 클러스터에서 **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**에 CSV 파일로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-144">The sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="3c69e-145">이 데이터는 건물의 온도 변화를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-145">The data captures the temperature variations of a building.</span></span> <span data-ttu-id="3c69e-146">다음은 데이터의 첫 행입니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-146">Here are the first few rows of the data.</span></span>

    <span data-ttu-id="3c69e-147">![대화형 Spark SQL 쿼리용 데이터의 스냅숏](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "대화형 Spark SQL 쿼리용 데이터의 스냅숏")</span><span class="sxs-lookup"><span data-stu-id="3c69e-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="3c69e-148">다음 코드를 실행하여 데이터 프레임 및 임시 테이블(**hvac**)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-148">Create a dataframe and a temporary table (**hvac**) by running the following code.</span></span> <span data-ttu-id="3c69e-149">이 자습서에서는 원시 CSV 데이터의 열과 비교하여 모든 열을 임시 테이블에 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-149">For this tutorial, we do not create all the columns in the temporary table as compared to the columns in the raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="3c69e-150">테이블을 만들었으면 다음 코드를 사용하여 데이터에 대한 대화형 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-150">Once the table is created, run interactive query on the data, use the following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="3c69e-151">PySpark 커널을 사용하기 때문에 이제 `%%sql` 매직을 사용하여 만든 임시 테이블 **hvac**에서 대화형 SQL 쿼리를 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on the temporary table **hvac** that you created by using the `%%sql` magic.</span></span> <span data-ttu-id="3c69e-152">`%%sql` 매직 및 기타 PySpark 커널에서 사용 가능한 매직에 대한 자세한 내용은 [Spark HDInsight 클러스터와 함께 Jupyter Notebook에서 사용 가능한 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c69e-152">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="3c69e-153">다음과 같은 테이블 형식 출력이 기본적으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-153">The following tabular output is displayed by default.</span></span>

     <span data-ttu-id="3c69e-154">![대화형 Spark 쿼리 결과의 테이블 출력](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "대화형 Spark 쿼리 결과의 테이블 출력")</span><span class="sxs-lookup"><span data-stu-id="3c69e-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="3c69e-155">다른 시각화로 결과를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="3c69e-156">예를 들어 동일한 출력에 대한 영역 그래프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-156">For example, an area graph for the same output would look like the following.</span></span>

    <span data-ttu-id="3c69e-157">![대화형 Spark 쿼리 결과의 영역 그래프](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "대화형 Spark 쿼리 결과의 영역 그래프")</span><span class="sxs-lookup"><span data-stu-id="3c69e-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="3c69e-158">응용 프로그램 실행을 완료한 후 클러스터 리소스를 해제하도록 Notebook을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-158">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="3c69e-159">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="3c69e-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c69e-160">Next step</span></span>

<span data-ttu-id="3c69e-161">이 문서에서는 Jupyter 노트북을 사용하여 Spark에서 대화형 쿼리를 실행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3c69e-161">In this article you learned how to run interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="3c69e-162">다음 문서로 진행하여 Spark에 등록된 데이터를 Power BI 및 Tableau와 같은 BI 분석 도구로 가져오는 방법을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3c69e-162">Advance to the next article to see how the data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="3c69e-163">Azure HDInsight와 함께 데이터 시각화 도구를 사용하는 Spark BI</span><span class="sxs-lookup"><span data-stu-id="3c69e-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




