---
title: "Apache Spark를 사용하여 Azure Data Lake Store의 데이터 분석 | Microsoft Docs"
description: "Spark 작업을 실행하여 Azure Data Lake 저장소에 저장된 데이터 분석"
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="4ec2e-103">HDInsight Spark 클러스터를 사용하여 Data Lake Store의 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="4ec2e-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="4ec2e-104">이 자습서에서는 HDInsight Spark 클러스터와 함께 제공되는 Jupyter Notebook을 사용하여 Data Lake Store 계정에서 데이터를 읽는 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ec2e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4ec2e-105">Prerequisites</span></span>

* <span data-ttu-id="4ec2e-106">Azure Data Lake Store 계정</span><span class="sxs-lookup"><span data-stu-id="4ec2e-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="4ec2e-107">[Azure Portal을 사용하여 Azure Data Lake Store 시작](../data-lake-store/data-lake-store-get-started-portal.md)에 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="4ec2e-108">Data Lake Store를 저장소로 사용하는 Azure HDInsight Spark 클러스터 -</span><span class="sxs-lookup"><span data-stu-id="4ec2e-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="4ec2e-109">[Azure Portal을 사용하여 Data Lake Store로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)에 나오는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="4ec2e-110">데이터 준비</span><span class="sxs-lookup"><span data-stu-id="4ec2e-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="4ec2e-111">기본 저장소로 Data Lake Store를 사용하여 HDInsight 클러스터를 만든 경우 이 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="4ec2e-112">클러스터 만들기 프로세스는 클러스터를 만드는 동안 지정된 Data Lake Store 계정에서 몇 가지 샘플 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="4ec2e-113">[Data Lake Store에서 HDInsight Spark 클러스터 사용](#use-an-hdinsight-spark-cluster-with-data-lake-store) 섹션으로 건너 뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="4ec2e-114">Data Lake Store를 추가 저장소로, Azure Storage Blob을 기본 저장소로 사용하여 HDInsight 클러스터를 만든 경우 먼저 몇 가지 샘플 데이터를 Data Lake Store 계정으로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="4ec2e-115">HDInsight 클러스터와 연결된 Azure Storage Blob의 샘플 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="4ec2e-116">이 작업에는 [ADLCopy 도구](http://aka.ms/downloadadlcopy) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="4ec2e-117">링크에서 도구를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="4ec2e-118">명령 프롬프트를 열고 AdlCopy가 설치된 디렉터리로 이동합니다(일반적으로 `%HOMEPATH%\Documents\adlcopy`).</span><span class="sxs-lookup"><span data-stu-id="4ec2e-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="4ec2e-119">다음 명령을 실행하여 원본 컨테이너에서 데이터 레이크 저장소로 특정 BLOB를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="4ec2e-120">**/HdiSamples/HdiSamples/SensorSampleData/hvac/**의 **HVAC.csv** 샘플 데이터 파일을 Azure Data Lake Store 계정으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="4ec2e-121">코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="4ec2e-122">파일과 경로 이름의 대/소문자가 적절한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="4ec2e-123">Data Lake Store 계정이 있는 Azure 구독에 대한 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="4ec2e-124">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="4ec2e-125">데이터 파일(**HVAC.csv**)은 Data Lake Store 계정의 **/hvac** 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="4ec2e-126">Data Lake Store를 포함한 HDInsight Spark 클러스터 사용</span><span class="sxs-lookup"><span data-stu-id="4ec2e-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="4ec2e-127">[Azure 포털](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터에 대한 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="4ec2e-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="4ec2e-128">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="4ec2e-129">Spark 클러스터 블레이드에서 **빠른 연결**을 클릭한 다음 **클러스터 대시보드** 블레이드에서 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="4ec2e-130">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ec2e-131">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="4ec2e-132">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="4ec2e-133">새 Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-133">Create a new notebook.</span></span> <span data-ttu-id="4ec2e-134">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="4ec2e-135">![새 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "새 Jupyter 노트북 만들기")</span><span class="sxs-lookup"><span data-stu-id="4ec2e-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="4ec2e-136">PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="4ec2e-137">첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="4ec2e-138">이 시나리오에 필요한 형식을 가져와 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="4ec2e-139">이렇게 하려면 셀에 다음 코드 조각을 붙여 넣고 **SHIFT + ENTER**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="4ec2e-140">Jupyter에서 작업을 실행할 때마다, 웹 브라우저 창 제목에 Notebook 제목과 함께 **(사용 중)** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="4ec2e-141">또한 오른쪽 위 모서리에 있는 **PySpark** 텍스트 옆에 단색 원이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="4ec2e-142">작업이 완료되면 속이 빈 원으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="4ec2e-143">![Jupyter 노트북 작업 상태](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter 노트북 작업 상태")</span><span class="sxs-lookup"><span data-stu-id="4ec2e-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="4ec2e-144">Data Lake Store 계정에 복사한 **HVAC.csv** 파일을 사용하여 샘플 데이터를 임시 테이블에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="4ec2e-145">다음 URL 패턴을 사용하여 Data Lake 저장소 계정의 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="4ec2e-146">Data Lake Store를 기본 저장소로 사용하는 경우 HVAC.csv는 다음 URL과 비슷한 경로에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="4ec2e-147">또는 다음과 같이 축약된 형식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="4ec2e-148">Data Lake Store를 추가 저장소로 사용하는 경우 HVAC.csv는 다음과 같이 복사한 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="4ec2e-149">빈 셀에는 다음 코드 예제를 붙여넣습니다. 이때 **MYDATALAKESTORE**를 Data Lake Store 계정 이름으로 바꾸고 **Shift+Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="4ec2e-150">이 코드 예제는 **hvac**라는 임시 테이블에 데이터로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="4ec2e-151">PySpark 커널을 사용하기 때문에 이제 `%%sql` 매직을 사용하여 방금 만든 임시 테이블 **hvac**에서 SQL 쿼리를 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="4ec2e-152">`%%sql` 매직 및 기타 PySpark 커널에서 사용 가능한 매직에 대한 자세한 내용은 [Spark HDInsight 클러스터와 함께 Jupyter Notebook에서 사용 가능한 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="4ec2e-153">작업이 성공적으로 완료되면 기본적으로 다음 테이블 형식의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="4ec2e-154">![쿼리 결과 출력 테이블](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "쿼리 결과 출력 테이블")</span><span class="sxs-lookup"><span data-stu-id="4ec2e-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="4ec2e-155">다른 시각화로 결과를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="4ec2e-156">예를 들어 동일한 출력에 대한 영역 그래프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="4ec2e-157">![쿼리 결과 영역 그래프](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "쿼리 결과 영역 그래프")</span><span class="sxs-lookup"><span data-stu-id="4ec2e-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="4ec2e-158">응용 프로그램 실행을 완료한 후 리소스를 해제하도록 Notebook을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="4ec2e-159">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="4ec2e-160">그러면 Notebook이 종료되고 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="4ec2e-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4ec2e-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4ec2e-161">Next steps</span></span>

* [<span data-ttu-id="4ec2e-162">Apache Spark에서 실행할 독립 실행형 Scala 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4ec2e-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4ec2e-163">IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 HDInsight Spark Linux 클러스터용 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4ec2e-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4ec2e-164">Eclipse용 Azure 도구 키트의 HDInsight 도구를 사용하여 HDInsight Spark Linux 클러스터용 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4ec2e-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
