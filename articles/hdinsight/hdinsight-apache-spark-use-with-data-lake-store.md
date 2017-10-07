---
title: "Azure 데이터 레이크 저장소의 Apache Spark tooanalyze 데이터 aaaUse | Microsoft Docs"
description: "Azure 데이터 레이크 저장소에 저장 된 tooanalyze 데이터 Spark 작업 실행"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="145cc-103">데이터 레이크 저장소의 HDInsight Spark 클러스터 tooanalyze 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="145cc-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="145cc-104">이 자습서에서는 HDInsight Spark 클러스터 toorun 데이터 레이크 저장소 계정에서 데이터를 읽는 작업으로 사용할 수 있는 Jupyter 노트북을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="145cc-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="145cc-105">Prerequisites</span></span>

* <span data-ttu-id="145cc-106">Azure Data Lake Store 계정</span><span class="sxs-lookup"><span data-stu-id="145cc-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="145cc-107">Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](../data-lake-store/data-lake-store-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="145cc-108">Data Lake Store를 저장소로 사용하는 Azure HDInsight Spark 클러스터 -</span><span class="sxs-lookup"><span data-stu-id="145cc-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="145cc-109">Hello 지침에 따라 [Azure 포털을 사용 하 여 데이터 레이크 저장소는 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="145cc-110">Hello 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="145cc-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="145cc-111">않아도 tooperform이이 단계 기본 저장소로 데이터 레이크 저장소와 hello HDInsight 클러스터를 만든 경우.</span><span class="sxs-lookup"><span data-stu-id="145cc-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="145cc-112">hello 클러스터 만들기 프로세스는 hello 클러스터를 만드는 동안 지정 된 hello Data Lake 저장소 계정에서 몇 가지 샘플 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="145cc-113">Toohello 건너 뛸 [Data Lake 저장소를 사용 하 여 HDInsight Spark 클러스터](#use-an-hdinsight-spark-cluster-with-data-lake-store)합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="145cc-114">데이터 레이크 저장소와 추가 저장소 및 기본 저장소로 Azure 저장소 Blob으로 하는 HDInsight 클러스터를 만든 경우 먼저 몇 가지 샘플 데이터 toohello Data Lake 저장소 계정을 통해 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="145cc-115">Hello hello HDInsight 클러스터와 연결 된 Azure 저장소 Blob의에서 hello 샘플 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="145cc-116">Hello를 사용할 수 있습니다 [ADLCopy 도구](http://aka.ms/downloadadlcopy) toodo 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="145cc-117">다운로드 하 여 hello 링크에서 hello 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="145cc-118">명령 프롬프트를 열고 toohello AdlCopy 설치 된 디렉터리를 일반적으로 이동 `%HOMEPATH%\Documents\adlcopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="145cc-119">Hello 소스 컨테이너 tooa 데이터 레이크 저장소에서에서 다음 명령을 toocopy hello 특정 blob을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="145cc-120">복사 hello **HVAC.csv** 예제 데이터 파일에 **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="145cc-121">hello 코드 조각 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="145cc-122">파일을 hello 및 hello 적절 한 경우에서 경로 이름에는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="145cc-123">됩니다 증명된 tooenter hello 자격 증명에 대 한 hello Azure 구독이 있는 데이터 레이크 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="145cc-124">출력 유사한 toohello 다음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="145cc-125">hello 데이터 파일 (**HVAC.csv**) 폴더에 복사 될 **/hvac** hello Data Lake 저장소 계정에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="145cc-126">Data Lake Store를 포함한 HDInsight Spark 클러스터 사용</span><span class="sxs-lookup"><span data-stu-id="145cc-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="145cc-127">Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="145cc-128">아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="145cc-129">Hello Spark 클러스터 블레이드에서 클릭 **빠른 링크**, 한 다음 hello **클러스터 대시보드** 블레이드에서 클릭 **Jupyter 노트북**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="145cc-130">메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="145cc-131">또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="145cc-132">대체 **CLUSTERNAME** 클러스터의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="145cc-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="145cc-133">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-133">Create a new notebook.</span></span> <span data-ttu-id="145cc-134">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="145cc-135">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="145cc-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="145cc-136">Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="145cc-137">hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다 드립니다 hello 첫 번째 코드 셀을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="145cc-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="145cc-138">이 시나리오에 필요한 hello 종류를 가져와서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="145cc-139">toodo 따라서 hello 코드 조각을 누릅니다 셀에서 다음을 붙여 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="145cc-140">웹 브라우저 창 제목에 표시 됩니다 Jupyter 작업을 실행할 때마다는 **(Busy)** hello 노트북 제목 함께 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="145cc-141">이 찬 원 모양 다음 toohello를 살펴보면 **PySpark** hello 오른쪽 위 모퉁이의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="145cc-142">Hello 작업이 완료 되 면 tooa 흰색 원을 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="145cc-143">![Jupyter 노트북 작업 상태](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter 노트북 작업 상태")</span><span class="sxs-lookup"><span data-stu-id="145cc-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="145cc-144">Hello를 사용 하 여 임시 테이블에 샘플 데이터를 로드 **HVAC.csv** toohello Data Lake 저장소 계정이 복사 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="145cc-145">Hello 데이터 hello URL 패턴을 사용 하 여 hello Data Lake 저장소 계정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="145cc-146">기본 저장소로 데이터 레이크 저장소를 설정한 경우 HVAC.csv hello 경로 비슷한 toohello url에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="145cc-147">또는 hello 다음과 같은 축약된 형식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="145cc-148">데이터 레이크 저장소 추가 저장소를 설정한 경우 복사한, 같은 hello 위치의 HVAC.csv 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="145cc-149">빈 셀을 다음 코드 예제에서는 붙여넣기 hello 바꿉니다 **MYDATALAKESTORE** Data Lake 저장소 계정 이름 및 키를 눌러 **SHIFT + ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="145cc-150">이 코드 예제에서는 라는 임시 테이블로 hello 데이터 등록 **hvac**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="145cc-151">PySpark 커널을 사용 하는 실행할 수 있습니다 이제 직접 SQL 쿼리 hello 임시 테이블에 **hvac** hello를 사용 하 여 방금 만든 있는지 `%%sql` 매직 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="145cc-152">Hello에 대 한 자세한 내용은 `%%sql` 매직, 뿐만 아니라 다른 마법 hello PySpark 커널 사용할 수 있는 참조 [Jupyter 노트북 HDInsight Spark 클러스터에서 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="145cc-153">Hello 작업이 성공적으로 완료 되 면 다음 표 형식으로 출력 하는 hello 기본적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="145cc-154">![쿼리 결과 출력 테이블](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "쿼리 결과 출력 테이블")</span><span class="sxs-lookup"><span data-stu-id="145cc-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="145cc-155">다른 시각화 요소에서 hello 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="145cc-156">예를 들어 영역에 대 한 그래프 hello hello 다음과 같은 동일한 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="145cc-157">![쿼리 결과 영역 그래프](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "쿼리 결과 영역 그래프")</span><span class="sxs-lookup"><span data-stu-id="145cc-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="145cc-158">Hello 응용 프로그램 실행을 완료 한 후 종료 hello 노트북 toorelease hello 리소스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="145cc-159">toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="145cc-160">이 종료 및 닫기 hello 전자 필기장 합니다.</span><span class="sxs-lookup"><span data-stu-id="145cc-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="145cc-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="145cc-161">Next steps</span></span>

* [<span data-ttu-id="145cc-162">Apache Spark 클러스터에 독립 실행형 Scala 응용 프로그램 toorun 만들기</span><span class="sxs-lookup"><span data-stu-id="145cc-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="145cc-163">Azure 도구 키트에서 HDInsight 도구를 사용 하 여 HDInsight Spark Linux 클러스터를 위한 IntelliJ toocreate Spark 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="145cc-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="145cc-164">HDInsight Spark Linux 클러스터에 대 한 toocreate Spark 응용 프로그램 Eclipse 용 Azure 도구 키트에서 사용 하 여 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="145cc-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
