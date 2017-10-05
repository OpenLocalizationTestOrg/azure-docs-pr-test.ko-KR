---
title: "Azure HDInsight에서 데이터 시각화 도구를 사용하는 Spark BI | Microsoft Docs"
description: "HDInsight 클러스터에서 Apache Spark BI를 사용하는 분석에 대해 데이터 시각화 도구 사용"
keywords: "apache spark bi,spark bi, spark 데이터 시각화, spark 비즈니스 인텔리전스"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="2b56e-104">Azure HDInsight와 함께 데이터 시각화 도구를 사용하는 Apache Spark BI</span><span class="sxs-lookup"><span data-stu-id="2b56e-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="2b56e-105">Power BI 및 Tableau와 같은 데이터 시각화 도구를 사용하여 HDInsight 클러스터에서 Apache Spark BI를 사용하여 원시 샘플 데이터 집합을 분석하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="2b56e-106">이 문서에 설명된 BI 도구와의 연결은 Azure HDInsight 3.6 Preview의 Spark 2.1에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="2b56e-107">Spark 버전 1.6 및 2.0(각각 HDInsight 3.4, 3.5)만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="2b56e-108">이 자습서는 HDInsight Spark 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="2b56e-109">Notebook 환경을 통해 Notebook 자체에서 Python 코드 조각을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="2b56e-110">Notebook 내에서 자습서를 수행하려면 Spark 클러스터를 만들고 Jupyter Notebook(`https://CLUSTERNAME.azurehdinsight.net/jupyter`)을 시작한 다음 **Python** 폴더 아래의 **HDInsight.ipynb에서 Apache Spark와 함께 BI 도구 사용** Notebook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b56e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b56e-111">Prerequisites</span></span>

* <span data-ttu-id="2b56e-112">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="2b56e-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b56e-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="2b56e-114"><a name="hivetable"></a>Spark 데이터 시각화를 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="2b56e-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="2b56e-115">이 섹션에서는 HDInsight Spark 클러스터에서 [Jupyter](https://jupyter.org) Notebook을 사용하여 원시 샘플 데이터를 처리하고 테이블로 저장하는 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="2b56e-116">샘플 데이터는 기본적으로 모든 클러스터에서 사용 가능한 .csv 파일(hvac.csv)입니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="2b56e-117">데이터가 테이블로 저장되면 다음 섹션에서 BI 도구를 사용하여 테이블에 연결하고 데이터 시각화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="2b56e-118">[HDInsight Spark 클러스터에서 대화형 쿼리 실행](hdinsight-apache-spark-load-data-run-query.md) 지침을 완료한 후에 이 문서의 단계를 수행하는 경우 아래의 8단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="2b56e-119">[Azure Portal](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터의 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="2b56e-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="2b56e-120">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="2b56e-121">Spark 클러스터 블레이드에서 **클러스터 대시보드**를 클릭하고 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="2b56e-122">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b56e-123">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="2b56e-124">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="2b56e-125">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-125">Create a notebook.</span></span> <span data-ttu-id="2b56e-126">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="2b56e-127">![Apache Spark BI에 대한 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Apache Spark BI에 대한 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="2b56e-128">새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="2b56e-129">맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="2b56e-130">![Apache Spark BI용 노트북에 대한 이름 제공](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Apache Spark BI용 노트북에 대한 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="2b56e-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="2b56e-131">PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="2b56e-132">첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="2b56e-133">이 시나리오에 필요한 형식을 가져와 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="2b56e-134">그렇게 하려면 셀에 커서를 놓고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="2b56e-135">샘플 데이터를 임시 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="2b56e-136">HDInsight에서 Spark 클러스터를 만들면 샘플 데이터 파일인 **hvac.csv**가 **\HdiSamples\HdiSamples\SensorSampleData\hvac** 아래 연결된 저장소 계정에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="2b56e-137">빈 셀에서 다음 코드 조각을 붙여넣고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="2b56e-138">이 코드 조각은 **hvac**라는 테이블에 데이터를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="2b56e-139">테이블이 성공적으로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="2b56e-140">`%%sql` 매직을 사용하여 Hive 쿼리를 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="2b56e-141">`%%sql` 매직 및 기타 PySpark 커널에서 사용 가능한 매직에 대한 자세한 내용은 [Spark HDInsight 클러스터와 함께 Jupyter Notebook에서 사용 가능한 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b56e-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="2b56e-142">아래와 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="2b56e-143">**isTemporary** 열 아래에서 false를 포함하는 테이블만 metastore에 저장되고 BI 도구에서 액세스할 수 있는 하이브 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="2b56e-144">이 자습서에서는 만든 **hvac** 테이블에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="2b56e-145">테이블에 원하는 데이터가 들어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="2b56e-146">Notebook의 빈 셀에서 다음 코드 조각을 복사하고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="2b56e-147">Notebook을 종료하여 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="2b56e-148">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="2b56e-149"><a name="powerbi"></a>Spark 데이터 시각화에 대해 Power BI 사용</span><span class="sxs-lookup"><span data-stu-id="2b56e-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="2b56e-150">이 섹션은 HDInsight 3.4의 Spark 1.6 및 HDInsight 3.5의 Spark 2.0에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="2b56e-151">데이터를 테이블로 저장하면 Power BI를 사용하여 데이터를 연결하고 시각화하여 보고서, 대시보드 등을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="2b56e-152">Power BI에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="2b56e-153">[http://www.powerbi.com/](http://www.powerbi.com/)에서 Power BI의 미리 보기 구독을 무료로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="2b56e-154">[Power BI](http://www.powerbi.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="2b56e-155">왼쪽 창의 아래쪽에서 **데이터 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="2b56e-156">**데이터 가져오기** 페이지의 **데이터 가져오기 또는 연결**에 있는 **데이터베이스**에서 **가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="2b56e-157">![Apache Spark BI용 Power BI로 데이터 가져오기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Apache Spark BI용 Power BI로 데이터 가져오기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="2b56e-158">다음 화면에서 **Azure HDInsight의 Spark**를 클릭한 다음 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="2b56e-159">메시지가 표시되면 클러스터 URL(`mysparkcluster.azurehdinsight.net`) 및 자격 증명을 입력하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="2b56e-160">![Apache Spark BI에 연결](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Apache Spark BI에 연결")</span><span class="sxs-lookup"><span data-stu-id="2b56e-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="2b56e-161">연결이 설정되면 Power BI는 HDInsight의 Spark 클러스터에서 데이터 가져오기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="2b56e-162">Power BI에서 데이터를 가져와서 **데이터 집합** 제목 아래에 **Spark** 데이터 집합을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="2b56e-163">데이터 집합을 클릭하여 새 워크시트를 열고 데이터를 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="2b56e-164">워크시트를 보고서로 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="2b56e-165">워크시트를 저장하려면 **파일** 메뉴에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="2b56e-166">![Power BI 대시보드의 Apache Spark BI 타일](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 대시보드의 Apache Spark BI 타일")</span><span class="sxs-lookup"><span data-stu-id="2b56e-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="2b56e-167">오른쪽의 **필드** 목록에는 이전에 만든 **hvac** 테이블이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="2b56e-168">이전에 노트북에서 정의한 대로 테이블의 필드를 보려면 테이블을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="2b56e-169">![Apache Spark BI 대시보드에 테이블 나열](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI 대시보드에 테이블 나열")</span><span class="sxs-lookup"><span data-stu-id="2b56e-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="2b56e-170">각 건물에 대한 대상 온도와 실제 온도 간의 차이를 보여주는 시각화를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="2b56e-171">데이터를 시각화하려면 **영역형 차트**(빨간색 상자)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="2b56e-172">축을 정의하려면 **BuildingID** 필드를 **축** 아래에, **ActualTemp**/**TargetTemp** 필드를 **값** 아래에 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="2b56e-173">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="2b56e-174">기본적으로 시각화에서는 **ActualTemp** 및 **TargetTemp**의 합계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="2b56e-175">두 필드 모두에 대해 드롭다운 메뉴에서 **평균** 을 선택하여 두 건물에 대한 실제 및 대상 온도의 평균을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="2b56e-176">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="2b56e-177">데이터 시각화는 스크린샷의 데이터 시각화와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="2b56e-178">커서를 시각화 위로 이동하면 관련 데이터와 함께 도구 설명이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="2b56e-179">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="2b56e-180">최상위 메뉴에서 **저장** 을 클릭하고 보고서 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="2b56e-181">시각화를 고정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-181">You can also pin the visual.</span></span> <span data-ttu-id="2b56e-182">시각화를 고정하면 해당 시각화가 대시보드에 저장되어 최신 값을 한 눈에 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="2b56e-183">동일한 데이터 집합에 대해 시각화를 원하는 만큼 추가하고 대시보드에 고정하여 데이터에 대한 스냅숏을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="2b56e-184">또한 직접 연결을 통해 HDInsight의 Spark 클러스터는 Power BI에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="2b56e-185">이렇게 하면 Power BI에서 항상 클러스터의 최신 데이터를 유지할 수 있으므로 데이터 집합에 대한 새로 고침을 예약할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="2b56e-186"><a name="tableau"></a>Spark 데이터 시각화에 대해 Tableau Desktop 사용</span><span class="sxs-lookup"><span data-stu-id="2b56e-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="2b56e-187">이 섹션은 Azure HDInsight에서 만든 Spark 1.5.2 클러스터에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="2b56e-188">이 Apache Spark BI 자습서를 실행 중인 컴퓨터에 [Tableau Desktop](http://www.tableau.com/products/desktop)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="2b56e-189">또한 Microsoft Spark ODBC 드라이버가 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="2b56e-190">[여기](http://go.microsoft.com/fwlink/?LinkId=616229)에서 드라이버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="2b56e-191">Tableau Desktop을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="2b56e-192">왼쪽 창의 연결할 서버 목록에서 **Spark SQL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="2b56e-193">왼쪽 창에 Spark SQL이 기본적으로 표시되지 않으면 **추가 서버**를 클릭하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="2b56e-194">Spark SQL 연결 대화 상자에서 스크린샷과 같은 값을 제공한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="2b56e-195">![Apache Spark BI용 클러스터에 연결](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark BI용 클러스터에 연결")</span><span class="sxs-lookup"><span data-stu-id="2b56e-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="2b56e-196">컴퓨터에 **Microsoft Spark ODBC 드라이버** 를 설치한 경우에만 인증 드롭다운 목록에 [Microsoft Azure HDInsight Service](http://go.microsoft.com/fwlink/?LinkId=616229) 가 옵션으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="2b56e-197">다음 화면의 **스키마** 드롭다운에서 **찾기** 아이콘, **기본값**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="2b56e-198">![Apache Spark BI용 스키마 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI용 스키마 찾기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="2b56e-199">**테이블** 필드에서 **찾기** 아이콘을 다시 클릭하면 클러스터에 사용 가능한 Hive 테이블이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="2b56e-200">이전에 Notebook을 사용하여 만든 **hvac** 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="2b56e-201">![Apache Spark BI용 테이블 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI용 테이블 찾기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="2b56e-202">테이블을 오른쪽 상단에 있는 상자에 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="2b56e-203">Tableau에서 데이터를 가져오고 빨간색 상자로 강조하여 스키마를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="2b56e-204">![Apache Spark BI용 Tableau에 테이블 추가](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Apache Spark BI용 Tableau에 테이블 추가")</span><span class="sxs-lookup"><span data-stu-id="2b56e-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="2b56e-205">왼쪽 아래에서 **Sheet1** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="2b56e-206">날짜별로 모든 건물에 대한 대상 및 실제 온도 평균을 보여 주는 시각화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="2b56e-207">**날짜** 및 **건물 ID**를 **열**로, **실제 온도**/**대상 온도**를 **행**으로 끌어갑니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="2b56e-208">**표시** 아래에서 **영역**을 선택하여 Spark 데이터 시각화에 대한 영역 맵을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="2b56e-209">![Spark 데이터 시각화를 위한 필드 추가](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark 데이터 시각화를 위한 필드 추가")</span><span class="sxs-lookup"><span data-stu-id="2b56e-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="2b56e-210">기본적으로 온도 필드가 집계로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="2b56e-211">대신, 평균 온도를 표시하려면 아래 표시된 것과 같이 드롭다운에서 이 작업을 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="2b56e-212">![Spark 데이터 시각화에 대한 온도 평균 구하기](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Spark 데이터 시각화에 대한 온도 평균 구하기")</span><span class="sxs-lookup"><span data-stu-id="2b56e-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="2b56e-213">또한 한 온도 맵을 다른 온도 맵 위에 겹쳐 놓아 대상 및 실제 온도 간의 차이를 보다 잘 파악할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="2b56e-214">마우스를 하단 영역 맵의 모서리로 이동하면 빨간색 원으로 강조 표시된 핸들 모양이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="2b56e-215">맵을 위쪽의 다른 맵으로 끌어온 후 빨간색 사각형으로 강조 표시된 모양이 표시되면 마우스를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="2b56e-216">![Spark 데이터 시각화를 위한 맵 병합](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Spark 데이터 시각화를 위한 맵 병합")</span><span class="sxs-lookup"><span data-stu-id="2b56e-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="2b56e-217">스크린샷과 같이 데이터 시각화가 변경되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="2b56e-218">![Spark 데이터 시각화에 대한 Tableau 출력](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 데이터 시각화에 대한 Tableau 출력")</span><span class="sxs-lookup"><span data-stu-id="2b56e-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="2b56e-219">**저장** 을 클릭하여 워크시트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="2b56e-220">대시보드를 만들고 시트를 하나 이상 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b56e-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b56e-221">Next steps</span></span>

<span data-ttu-id="2b56e-222">지금까지 클러스터를 만들고 Spark 데이터 프레임을 만들어 데이터를 쿼리한 다음 BI 도구에서 해당 데이터에 액세스하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="2b56e-223">이제 클러스터 리소스를 관리하고 HDInsight Spark 클러스터에서 실행 중인 작업을 디버그하는 방법에 대한 지침을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b56e-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="2b56e-224">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="2b56e-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2b56e-225">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="2b56e-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

