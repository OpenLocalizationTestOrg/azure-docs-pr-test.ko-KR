---
title: "aaaSpark BI 데이터 시각화 도구를 사용 하 여 Azure HDInsight의 | Microsoft Docs"
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
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="ef55a-104">Azure HDInsight와 함께 데이터 시각화 도구를 사용하는 Apache Spark BI</span><span class="sxs-lookup"><span data-stu-id="ef55a-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="ef55a-105">어떻게 toouse 데이터 시각화 도구 등 Power BI와 Tableau tooanalyze Apache Spark BI를 사용 하 여 HDInsight 클러스터에서 원시 샘플 데이터 집합에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-105">Learn how toouse data visualization tools such as Power BI and Tableau tooanalyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="ef55a-106">이 문서에 설명된 BI 도구와의 연결은 Azure HDInsight 3.6 Preview의 Spark 2.1에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="ef55a-107">Spark 버전 1.6 및 2.0(각각 HDInsight 3.4, 3.5)만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="ef55a-108">이 자습서는 HDInsight Spark 클러스터에서 Jupyter 노트북으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="ef55a-109">hello 노트북 경험 자체 hello 노트북에서 Python 코드 조각을 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-109">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="ef55a-110">노트북, 내에서 tooperform hello 자습서 Spark 클러스터를 만듭니다을 시작 하며, Jupyter 노트북 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), 다음 hello 노트북을 실행 하 고 **HDInsight.ipynb의 Apache Spark와 함께 사용 하 여 BI 도구** hello 아래 **Python**  폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-110">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under hello **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef55a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef55a-111">Prerequisites</span></span>

* <span data-ttu-id="ef55a-112">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ef55a-113">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef55a-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="ef55a-114"><a name="hivetable"></a>Spark 데이터 시각화를 위한 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="ef55a-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="ef55a-115">이 섹션을 사용 하 여 hello [Jupyter](https://jupyter.org) 원시 샘플 데이터를 처리 하 고 표 형식으로 저장 하는 HDInsight Spark 클러스터 toorun 작업에서 노트북 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-115">In this section, we use hello [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster toorun jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="ef55a-116">hello 예제 데이터는.csv 파일 (hvac.csv) 사용할 수 있는 기본적으로 모든 클러스터에서.</span><span class="sxs-lookup"><span data-stu-id="ef55a-116">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="ef55a-117">데이터를 테이블로 저장 hello 다음 섹션에서는 BI 도구 tooconnect toohello 테이블을 사용 하 고 데이터 시각화를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-117">Once your data is saved as a table, in hello next section we use BI tools tooconnect toohello table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="ef55a-118">Hello의 hello 지침을 완료 한 후이 문서의 단계를 수행 하는 경우 [HDInsight Spark 클러스터에서 대화형 쿼리를 실행](hdinsight-apache-spark-load-data-run-query.md), 아래의 8 tooStep를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-118">If you are performing hello steps in this article after completing hello instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip tooStep 8 below.</span></span>
>

1. <span data-ttu-id="ef55a-119">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="ef55a-120">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="ef55a-121">Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="ef55a-122">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef55a-123">또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="ef55a-124">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="ef55a-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="ef55a-125">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-125">Create a notebook.</span></span> <span data-ttu-id="ef55a-126">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="ef55a-127">![Apache Spark BI에 대한 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Apache Spark BI에 대한 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="ef55a-128">새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="ef55a-129">Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="ef55a-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="ef55a-130">![Apache Spark BI에 대 한 hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Apache Spark BI에 대 한 hello 전자 필기장에 대 한 이름을 제공")</span><span class="sxs-lookup"><span data-stu-id="ef55a-130">![Provide a name for hello notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for hello notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="ef55a-131">Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="ef55a-132">hello 첫 번째 코드 셀을 실행할 때 사용자에 대 한 hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-132">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="ef55a-133">이 시나리오에 필요한 hello 종류를 가져와서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-133">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="ef55a-134">toodo 누릅니다 hello 셀에 등 hello 커서를 놓고 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-134">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="ef55a-135">샘플 데이터를 임시 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="ef55a-136">Hello 예제 데이터 파일, HDInsight의 Spark 클러스터를 만들 때 **hvac.csv**, 복사한 toohello 연결 된 저장소 계정에는 **\HdiSamples\HdiSamples\SensorSampleData\hvac**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-136">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="ef55a-137">빈 셀을 붙여넣고 hello 다음 코드 조각 및 키를 눌러 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-137">In an empty cell, paste hello following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="ef55a-138">이 코드 조각 이라고 하는 테이블에 hello 데이터 등록 **hvac**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-138">This snippet registers hello data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="ef55a-139">해당 hello 테이블 올바르게 만들어졌는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-139">Verify that hello table was successfully created.</span></span> <span data-ttu-id="ef55a-140">Hello를 사용할 수 있습니다 `%%sql` toorun 하이브 쿼리를 직접 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-140">You can use hello `%%sql` magic toorun Hive queries directly.</span></span> <span data-ttu-id="ef55a-141">Hello에 대 한 자세한 내용은 `%%sql` 매직, 및 기타 마법 hello PySpark 커널 사용할 수 있는 참조 [Jupyter 노트북 HDInsight Spark 클러스터에서 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-141">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="ef55a-142">아래와 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="ef55a-143">Hello에서 false가 테이블에만 hello **isTemporary** 열은 하이브 테이블 hello metastore에 저장 되 고 hello BI 도구에서 액세스할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-143">Only hello tables that have false under hello **isTemporary** column are hive tables that are stored in hello metastore and can be accessed from hello BI tools.</span></span> <span data-ttu-id="ef55a-144">이 자습서에서는 toohello 연결 **hvac** 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-144">In this tutorial, we connect toohello **hvac** table we created.</span></span>

8. <span data-ttu-id="ef55a-145">Hello 의도 한 데이터를 포함 하는 hello 테이블을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-145">Verify that hello table contains hello intended data.</span></span> <span data-ttu-id="ef55a-146">Hello 전자 필기장의 빈 셀을 복사 hello 다음 코드 조각 및 키를 눌러 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-146">In an empty cell in hello notebook, copy hello following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="ef55a-147">Hello 노트북 toorelease hello 리소스를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-147">Shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="ef55a-148">toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-148">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="ef55a-149"><a name="powerbi"></a>Spark 데이터 시각화에 대해 Power BI 사용</span><span class="sxs-lookup"><span data-stu-id="ef55a-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="ef55a-150">이 섹션은 HDInsight 3.4의 Spark 1.6 및 HDInsight 3.5의 Spark 2.0에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="ef55a-151">Power BI tooconnect toohello 데이터를 사용할 수 있으며 toocreate 보고서 시각화 hello 데이터 테이블을 저장 한 후 대시보드, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-151">Once you have saved hello data as a table, you can use Power BI tooconnect toohello data and visualize it toocreate reports, dashboards, etc.</span></span>

1. <span data-ttu-id="ef55a-152">액세스 tooPower BI 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-152">Make sure you have access tooPower BI.</span></span> <span data-ttu-id="ef55a-153">[http://www.powerbi.com/](http://www.powerbi.com/)에서 Power BI의 미리 보기 구독을 무료로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="ef55a-154">역시 로그인[Power BI](http://www.powerbi.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-154">Sign in too[Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="ef55a-155">Hello hello 왼쪽된 창 아래쪽에서 클릭 **데이터 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-155">From hello bottom of hello left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="ef55a-156">Hello에 **데이터 가져오기** 페이지의 **가져오기 또는 연결 tooData**에 대 한 **데이터베이스**, 클릭 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-156">On hello **Get Data** page, under **Import or Connect tooData**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="ef55a-157">![Apache Spark BI용 Power BI로 데이터 가져오기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Apache Spark BI용 Power BI로 데이터 가져오기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="ef55a-158">Hello 다음 화면에서 클릭 **Azure HDInsight의 Spark** 클릭 하 고 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-158">On hello next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="ef55a-159">메시지가 표시 되 면 hello 클러스터 URL을 입력 합니다. (`mysparkcluster.azurehdinsight.net`) 및 hello 자격 증명 tooconnect toohello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-159">When prompted, enter hello cluster URL (`mysparkcluster.azurehdinsight.net`) and hello credentials tooconnect toohello cluster.</span></span>

    <span data-ttu-id="ef55a-160">![Spark BI tooApache 연결](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI를 연결 합니다.")</span><span class="sxs-lookup"><span data-stu-id="ef55a-160">![Connect tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect tooApache Spark BI")</span></span>

    <span data-ttu-id="ef55a-161">Hello 연결이 설정 된 후 Power BI는 HDInsight의 Spark 클러스터 hello에서에서 데이터 가져오기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-161">After hello connection is established, Power BI starts importing data from hello Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="ef55a-162">Power BI가 hello 데이터를 가져오고 추가 **Spark** hello에 데이터 집합 **데이터 집합** 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-162">Power BI imports hello data and adds a **Spark** dataset under hello **Datasets** heading.</span></span> <span data-ttu-id="ef55a-163">Hello 데이터 집합 tooopen 새 워크시트 toovisualize hello 데이터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-163">Click hello data set tooopen a new worksheet toovisualize hello data.</span></span> <span data-ttu-id="ef55a-164">보고서를 보고서로 hello 워크시트에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-164">You can also save hello worksheet as a report.</span></span> <span data-ttu-id="ef55a-165">toosave hello에서 워크시트 **파일** 메뉴를 클릭 하 여 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-165">toosave a worksheet, from hello **File** menu, click **Save**.</span></span>

    <span data-ttu-id="ef55a-166">![Power BI 대시보드의 Apache Spark BI 타일](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 대시보드의 Apache Spark BI 타일")</span><span class="sxs-lookup"><span data-stu-id="ef55a-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="ef55a-167">해당 hello 확인 **필드** 목록 hello 오른쪽에 나열 hello **hvac** 앞에서 만든 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-167">Notice that hello **Fields** list on hello right lists hello **hvac** table you created earlier.</span></span> <span data-ttu-id="ef55a-168">이전 노트북에 정의 된 hello 테이블의 hello 테이블 toosee hello 필드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-168">Expand hello table toosee hello fields in hello table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="ef55a-169">![Apache Spark BI 대시보드에 테이블 나열](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI 대시보드에 테이블 나열")</span><span class="sxs-lookup"><span data-stu-id="ef55a-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="ef55a-170">대상 온도 각 구성에 대 한 실제 온도 간의 시각화 tooshow hello 차이 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ef55a-170">Build a visualization tooshow hello variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="ef55a-171">toovisualize를 데이터 선택 **영역형 차트** (빨간색 상자에 표시).</span><span class="sxs-lookup"><span data-stu-id="ef55a-171">toovisualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="ef55a-172">끌어서 놓기 hello toodefine hello 축 **BuildingID** 아래 **축**, 및 **ActualTemp**/**TargetTemp** 아래 필드 **값**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-172">toodefine hello axis, drag-and-drop hello **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="ef55a-173">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="ef55a-174">기본적으로 hello 시각화에 대 한 hello 합계를 표시 **ActualTemp** 및 **TargetTemp**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-174">By default hello visualization shows hello sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="ef55a-175">예를 둘 다 hello hello 드롭다운 목록에서에서 필드를 선택 **평균** tooget 실제 평균 및 대상 온도 두 건물에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-175">For both hello fields, from hello drop-down, select **Average** tooget an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="ef55a-176">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="ef55a-177">데이터 시각화 hello 화면에 비슷한 toohello 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-177">Your data visualization should be similar toohello one in hello screenshot.</span></span> <span data-ttu-id="ef55a-178">관련 데이터와 함께 hello 시각화 tooget 도구 설명 위로 커서를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-178">Move your cursor over hello visualization tooget tool tips with relevant data.</span></span>

    <span data-ttu-id="ef55a-179">![Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Apache Spark BI를 사용하여 Spark 데이터 시각화 만들기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="ef55a-180">클릭 **저장** hello에서 최상위 메뉴와 보고서 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-180">Click **Save** from hello top menu and provide a report name.</span></span> <span data-ttu-id="ef55a-181">Hello visual를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-181">You can also pin hello visual.</span></span> <span data-ttu-id="ef55a-182">시각화를 고정 하면 hello 최신 값을 한눈에 추적할 수 있도록 대시보드에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-182">When you pin a visualization, it is stored on your dashboard so you can track hello latest value at a glance.</span></span>

   <span data-ttu-id="ef55a-183">원하는 만큼 많은 시각화 요소를 추가할 수 있습니다 hello 동일한 데이터 집합 및 데이터의 스냅샷에 대 한 toohello 대시보드 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-183">You can add as many visualizations as you want for hello same dataset and pin them toohello dashboard for a snapshot of your data.</span></span> <span data-ttu-id="ef55a-184">또한 HDInsight의 Spark 클러스터에 연결 된 tooPower direct 사용 하 여 BI 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-184">Also, Spark clusters on HDInsight are connected tooPower BI with direct connect.</span></span> <span data-ttu-id="ef55a-185">이렇게 하면는 Power BI는 항상 한 hello 클러스터에서 대부분의 최신 데이터 있으므로 hello 데이터 집합에 대 한 새로 고침 tooschedule 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-185">This ensures that Power BI always has hello most up-to-date data from your cluster so you do not need tooschedule refreshes for hello dataset.</span></span>

## <span data-ttu-id="ef55a-186"><a name="tableau"></a>Spark 데이터 시각화에 대해 Tableau Desktop 사용</span><span class="sxs-lookup"><span data-stu-id="ef55a-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="ef55a-187">이 섹션은 Azure HDInsight에서 만든 Spark 1.5.2 클러스터에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="ef55a-188">설치 [Tableau 데스크톱](http://www.tableau.com/products/desktop) 이 Apache Spark BI 자습서를 실행 중인 hello 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on hello computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="ef55a-189">또한 Microsoft Spark ODBC 드라이버가 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="ef55a-190">Hello 드라이버를 설치할 수 있습니다 [여기](http://go.microsoft.com/fwlink/?LinkId=616229)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-190">You can install hello driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="ef55a-191">Tableau Desktop을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="ef55a-192">Hello, 서버 tooconnect 목록에서 hello 왼쪽된 창에서 클릭 **Spark SQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-192">In hello left pane, from hello list of server tooconnect to, click **Spark SQL**.</span></span> <span data-ttu-id="ef55a-193">Spark SQL hello 왼쪽된 창에서 기본적으로 나열 되지 않으면 경우 클릭 하 여 찾을 수 있습니다 **더 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-193">If Spark SQL is not listed by default in hello left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="ef55a-194">Hello 스크린샷에 표시 된 대로 hello Spark SQL 연결 대화 상자에서 hello 값을 제공 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-194">In hello Spark SQL connection dialog box, provide hello values as shown in hello screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="ef55a-195">![Apache Spark BI에 대 한 연결 tooa 클러스터](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark BI에 대 한 연결 tooa 클러스터")</span><span class="sxs-lookup"><span data-stu-id="ef55a-195">![Connect tooa cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="ef55a-196">인증 드롭 다운 목록을 hello **Microsoft Azure HDInsight 서비스** hello를 설치한 경우에 선택적으로 [Microsoft Spark ODBC 드라이버가](http://go.microsoft.com/fwlink/?LinkId=616229) hello 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-196">hello authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed hello [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on hello computer.</span></span>
3. <span data-ttu-id="ef55a-197">Hello에서 hello 다음 화면에서 **스키마** 드롭다운 목록에서 클릭 hello **찾을** 아이콘을 클릭 한 다음 **기본**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-197">On hello next screen, from hello **Schema** drop-down, click hello **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="ef55a-198">![Apache Spark BI용 스키마 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI용 스키마 찾기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="ef55a-199">Hello에 대 한 **테이블** 필드을 hello 클릭 **찾을** 아이콘 다시 모든 hello toolist 하이브 hello 클러스터에서 사용할 수 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-199">For hello **Table** field, click hello **Find** icon again toolist all hello Hive tables available in hello cluster.</span></span> <span data-ttu-id="ef55a-200">Hello 표시 되어야 **hvac** 이전 hello 노트북을 사용 하 여 만든 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-200">You should see hello **hvac** table you created earlier using hello notebook.</span></span>

    <span data-ttu-id="ef55a-201">![Apache Spark BI용 테이블 찾기](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI용 테이블 찾기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="ef55a-202">끌어서 hello 테이블 toohello 맨 위에 있는 상자 hello 오른쪽에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-202">Drag and drop hello table toohello top box on hello right.</span></span> <span data-ttu-id="ef55a-203">Tableau hello 데이터를 가져오며 hello 빨간색 상자로 강조 표시 된 대로 hello 스키마가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-203">Tableau imports hello data and displays hello schema as highlighted by hello red box.</span></span>

    <span data-ttu-id="ef55a-204">![Apache Spark BI에 대 한 테이블 tooTableau 추가](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "테이블 tooTableau Apache Spark BI에 대 한 추가")</span><span class="sxs-lookup"><span data-stu-id="ef55a-204">![Add tables tooTableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables tooTableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="ef55a-205">Hello 클릭 **Sheet1** hello 왼쪽 아래에는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-205">Click hello **Sheet1** tab at hello bottom left.</span></span> <span data-ttu-id="ef55a-206">각 날짜에 대 한 hello 평균 대상과 모든 건물 실제 온도 표시 하는 시각화를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-206">Make a visualization that shows hello average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="ef55a-207">끌기 **날짜** 및 **건물 ID** 너무**열** 및 **실제 Temp**/**대상 Temp**너무**행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-207">Drag **Date** and **Building ID** too**Columns** and **Actual Temp**/**Target Temp** too**Rows**.</span></span> <span data-ttu-id="ef55a-208">아래 **표시**선택, **영역** toouse Spark 데이터 시각화에 대 한 영역 맵.</span><span class="sxs-lookup"><span data-stu-id="ef55a-208">Under **Marks**, select **Area** toouse an area map for Spark data visualization.</span></span>

     <span data-ttu-id="ef55a-209">![Spark 데이터 시각화를 위한 필드 추가](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark 데이터 시각화를 위한 필드 추가")</span><span class="sxs-lookup"><span data-stu-id="ef55a-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="ef55a-210">기본적으로 hello 온도 필드가 표시 되어 집계로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-210">By default, hello temperature fields are shown as aggregate.</span></span> <span data-ttu-id="ef55a-211">대신 tooshow hello 평균 온도 원하는 경우 후 그렇게 hello 드롭다운 목록에서 아래와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-211">If you want tooshow hello average temperatures instead, you can do so from hello drop-down, as shown below.</span></span>

    <span data-ttu-id="ef55a-212">![Spark 데이터 시각화에 대한 온도 평균 구하기](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Spark 데이터 시각화에 대한 온도 평균 구하기")</span><span class="sxs-lookup"><span data-stu-id="ef55a-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="ef55a-213">적용할 수도 있습니다 슈퍼-온도 매핑이 두 개 이상의 다른 tooget 대상과 실제 온도 사이의 차이 보다 나은 느낌 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-213">You can also super-impose one temperature map over hello other tooget a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="ef55a-214">Hello 핸들 셰이프가 강조 표시는 빨간색 원이 나타날 때까지 hello 낮은 영역 맵의 hello 마우스 toohello 모퉁이 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-214">Move hello mouse toohello corner of hello lower area map till you see hello handle shape highlighted in a red circle.</span></span> <span data-ttu-id="ef55a-215">끌어서 hello 빨간색 사각형으로 강조 표시 하는 hello 셰이프가 나타날 때 toohello hello 위쪽과 릴리스 hello 마우스 단추를 다른 map을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-215">Drag hello map toohello other map on hello top and release hello mouse when you see hello shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="ef55a-216">![Spark 데이터 시각화를 위한 맵 병합](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Spark 데이터 시각화를 위한 맵 병합")</span><span class="sxs-lookup"><span data-stu-id="ef55a-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="ef55a-217">데이터 시각화 hello 스크린샷에 표시 된 대로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-217">Your data visualization should change as shown in hello screenshot:</span></span>

    <span data-ttu-id="ef55a-218">![Spark 데이터 시각화에 대한 Tableau 출력](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 데이터 시각화에 대한 Tableau 출력")</span><span class="sxs-lookup"><span data-stu-id="ef55a-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="ef55a-219">클릭 **저장** toosave hello 워크시트입니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-219">Click **Save** toosave hello worksheet.</span></span> <span data-ttu-id="ef55a-220">대시보드를 만들고 하나 이상의 시트 tooit를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-220">You can create dashboards and add one or more sheets tooit.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef55a-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef55a-221">Next steps</span></span>

<span data-ttu-id="ef55a-222">지금까지 어떻게 toocreate 클러스터 Spark 데이터 프레임 tooquery 데이터를 만들고 다음 BI 도구에서 해당 데이터에 액세스 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-222">So far you learned how toocreate a cluster, create Spark data frames tooquery data, and then access that data from BI tools.</span></span> <span data-ttu-id="ef55a-223">이제 toomanage 클러스터 리소스 hello 하 고 HDInsight Spark 클러스터에서 실행 중인 작업을 디버그 하는 방법에 대 한 지침을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-223">You can now look at instructions on how toomanage hello cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="ef55a-224">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef55a-224">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ef55a-225">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="ef55a-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

