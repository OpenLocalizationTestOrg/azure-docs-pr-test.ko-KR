---
title: "aaaOperationalize Spark 작성 기계 학습 모델 | Microsoft Docs"
description: "어떻게 tooload와 모델을 학습 하는 점수에 Azure Blob 저장소 (WASB) python을 저장 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="abe84-103">Spark에서 만든 Machine Learning 모델 운영</span><span class="sxs-lookup"><span data-stu-id="abe84-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="abe84-104">이 항목에서는 방법을 toooperationalize HDInsight Spark에 Python을 사용 하는 저장 된 기계 학습 모델 (ML) 클러스터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="abe84-105">Tooload 기계 학습 모델 Spark MLlib를 사용 하 여 구축 되어 Azure Blob 저장소 (WASB)를 저장 하는 방법 등에 대해 설명 tooscore WASB에도 저장 하는 데이터 집합을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="abe84-106">변환 기능을 사용 하 여 hello MLlib 도구 키트 및 toocreate 레이블이 지정 된 지점 데이터 개체를 사용할 수 있는 입력 방식 hello ML 모델 점수 매기기에 대 한 인덱싱 및 인코딩 함수 hello, 것 방법을 toopre 프로세스 hello에 대 한 입력된 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="abe84-107">hello 모델 평가에 사용 되는 선형 회귀, 로지스틱 회귀, 임의 포리스트 모델 및 그라데이션 승격 트리 모델에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="abe84-108">Spark 클러스터 및 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="abe84-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="abe84-109">설정 단계 및 hello 코드 toooperationalize ML 모델 HDInsight Spark 1.6 클러스터 뿐만 아니라 2.0 Spark 클러스터를 사용 하 여이 연습에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="abe84-110">이 절차에 대 한 hello 코드 Jupyter 노트북에도 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="abe84-111">Spark 1.6용 Notebook</span><span class="sxs-lookup"><span data-stu-id="abe84-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="abe84-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter 노트북 방법을 toooperationalize HDInsight에서 Python을 사용 하 여 저장 된 모델 클러스터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="abe84-113">Spark 2.0용 Notebook</span><span class="sxs-lookup"><span data-stu-id="abe84-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="abe84-114">Spark 1.6 toouse HDInsight Spark 2.0 클러스터에 대 한 toomodify hello Jupyter 노트북 hello Python 코드 파일을 대체 [이 파일](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py)합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="abe84-115">이 코드에서는 Spark 2.0에서 tooconsume hello 모델을 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="abe84-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="abe84-116">Prerequisites</span></span>

1. <span data-ttu-id="abe84-117">Azure 계정 및는 Spark 1.6 (또는)가 필요한 Spark 2.0 HDInsight 클러스터 toocomplete이이 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="abe84-118">Hello 참조 [개요의 데이터 과학 Azure HDInsight의 Spark를 사용 하 여](machine-learning-data-science-spark-overview.md) 방법에 대 한 지침은 toosatisfy 이러한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="abe84-119">해당 항목에는 여기에 NYC 2013 택시 데이터 hello 및 tooexecute hello Spark 클러스터에서 Jupyter 노트북에서 코드가 하는 방식에 대 한 지침에 대 한 설명을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="abe84-120">또한 만들어야 hello 기계 학습 모델 toobe hello 통해 작업 하 여 여기 점수가 매겨진 [데이터 탐색 및 모델링 spark](machine-learning-data-science-spark-data-exploration-modeling.md) hello 1.6 Spark 클러스터 또는 hello Spark 2.0 전자 필기장에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="abe84-121">Spark 2.0 hello 전자 필기장 hello 잘 알려진 Airline 정시 출발에서 데이터 집합 2011 및 2012 hello 분류 작업에 대 한 추가 데이터 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="abe84-122">Hello에 전자 필기장 및 링크 toothem hello에 대 한 설명을 제공 됩니다 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 이 포함 하는 hello GitHub 리포지토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="abe84-123">또한 hello 코드와 연결 된 hello 전자 필기장에서 제네릭 인데 어떤 Spark 클러스터에서 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="abe84-124">HDInsight Spark를 사용 하지 않는 경우 hello 클러스터 설치 및 관리 단계는 여기 표시 된에서 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="abe84-125">설정: 저장소 위치, 라이브러리 및 hello Spark 컨텍스트 사전 설정</span><span class="sxs-lookup"><span data-stu-id="abe84-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="abe84-126">Spark 수 tooread 및 쓰기 tooan Azure 저장소 Blob (WASB)입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="abe84-127">따라서 여기에 저장 된 기존 데이터의 Spark를 사용 하 여 처리할 수 하 고 hello에 다시 저장된 WASB 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="abe84-128">toosave 모델 또는 WASB의 파일을 제대로 지정 toobe hello 경로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="abe84-129">hello 기본 연결 된 컨테이너 toohello Spark 클러스터를 참조할 수 있습니다로 시작 하는 경로 사용 하 여: *"wasb / /"*합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="abe84-130">hello 다음 코드 샘플 hello의 위치를 지정 hello 데이터 toobe 읽기 및 hello 모델 저장소 디렉터리 toowhich hello 모델 출력에 대 한 hello 경로가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="abe84-131">WASB의 저장소 위치에 대한 디렉터리 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="abe84-132">모델 저장 위치: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="abe84-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="abe84-133">이 경로를 올바르게 설정하지 않으면 점수 매기기를 위한 모델이 로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="abe84-134">hello 점수가 매겨진된 결과에 저장 되었습니다: "wasb: / / / 사용자/remoteuser/NYCTaxi/ScoredResults"입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="abe84-135">Hello 경로 toofolder 올바르지 않으면 결과 해당 폴더에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="abe84-136">hello 파일 경로 위치를 복사 하 고 hello hello의 마지막 셀의 hello 출력에서이 코드의 hello 자리 표시자에 붙여넣을 수 **machine-learning-data-science-spark-data-exploration-modeling.ipynb** 전자 필기장 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="abe84-137">Hello 코드 tooset 디렉터리 경로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="abe84-138">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-138">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="abe84-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="abe84-140">라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="abe84-140">Import libraries</span></span>
<span data-ttu-id="abe84-141">Spark 컨텍스트를 설정 하 고 코드 다음 hello를 사용 하 여 필요한 라이브러리 가져오기</span><span class="sxs-lookup"><span data-stu-id="abe84-141">Set spark context and import necessary libraries with hello following code</span></span>

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="abe84-142">미리 설정된 Spark 컨텍스트 및 PySpark 매직</span><span class="sxs-lookup"><span data-stu-id="abe84-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="abe84-143">Jupyter 노트북에 제공 되는 hello PySpark 커널에는 미리 설정 된 컨텍스트가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="abe84-144">따라서 불필요 tooset hello Spark 또는 Hive 컨텍스트 명시적으로 개발 하는 hello 응용 프로그램 사용을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="abe84-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="abe84-145">이러한 컨텍스트는 기본적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-145">These are available for you by default.</span></span> <span data-ttu-id="abe84-146">이러한 컨텍스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-146">These contexts are:</span></span>

* <span data-ttu-id="abe84-147">sc - Spark용</span><span class="sxs-lookup"><span data-stu-id="abe84-147">sc - for Spark</span></span> 
* <span data-ttu-id="abe84-148">sqlContext - Hive용</span><span class="sxs-lookup"><span data-stu-id="abe84-148">sqlContext - for Hive</span></span>

<span data-ttu-id="abe84-149">hello PySpark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 % %입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="abe84-150">이러한 코드 샘플에 사용되는 다음과 같은 두 가지 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="abe84-151">**% % 로컬** hello 코드 줄에서 로컬로 실행 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="abe84-152">코드는 유효한 Python 코드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="abe84-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="abe84-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="abe84-154">SqlContext hello에 대 한 하이브 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="abe84-155">Hello 쿼리의 hello 결과 hello에서 유지 되 hello-o 매개 변수에 전달 되 면 % % 팬더 데이터 프레임으로 로컬 Python 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="abe84-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="abe84-156">Hello 커널에서 Jupyter 노트북 및 미리 정의 된 hello에 대 한 자세한 내용은 "magics"는에 대 한 제공, 참조 [HDInsight Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 HDInsight 클러스터로](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="abe84-157">데이터 수집 및 정리된 데이터 프레임 만들기</span><span class="sxs-lookup"><span data-stu-id="abe84-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="abe84-158">이 섹션에는 일련의 작업 필요한 tooingest hello 데이터 toobe 점수가 매겨진 hello 코드가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="abe84-159">Hello 택시 여행 및 요금 파일의 (.tsv 파일으로 저장 됨), 조인 된 0.1% 샘플에서 형식 hello 데이터를 읽고 다음 무결 한 데이터 프레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="abe84-160">hello 택시 여행 및 요금 파일에 제공 된 hello 절차에 따라 조인 된는: [팀 데이터 과학 프로세스 작업에 hello: HDInsight Hadoop 클러스터를 사용 하 여](machine-learning-data-science-process-hive-walkthrough.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="abe84-161">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-161">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-162">셀 위에서 tooexecute에 걸린 시간: 46.37 초</span><span class="sxs-lookup"><span data-stu-id="abe84-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="abe84-163">Spark에서 점수를 매기도록 데이터 준비</span><span class="sxs-lookup"><span data-stu-id="abe84-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="abe84-164">이 섹션에서는 tooindex, 인코딩 및 분류와 회귀에 대 한 감독 MLlib 학습 알고리즘에서 사용 하는 동안 범주 기능 tooprepare 확장 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="abe84-165">기능 변환: 범주 기능을 점수 매기기 모델에 입력하기 위해 인덱싱 및 인코딩</span><span class="sxs-lookup"><span data-stu-id="abe84-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="abe84-166">이 섹션에서는 어떻게 tooindex 범주 데이터를 사용 하 여는 `StringIndexer` 기능과 인코딩합니다 `OneHotEncoder` hello 모델에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="abe84-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 레이블 인덱스의 레이블 tooa 열의 문자열 열을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="abe84-168">hello 인덱스 레이블 주파수로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="abe84-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 으로 최대 단일 한 값을 이진 벡터의 인덱스 tooa 열을 레이블 열을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="abe84-170">로지스틱 회귀와 같은 연속 중요 기능을 예상 하는 알고리즘을 사용 하면이 인코딩 적용 toobe toocategorical 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="abe84-171">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-171">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-172">셀 위에서 tooexecute에 걸린 시간: 5.37 초</span><span class="sxs-lookup"><span data-stu-id="abe84-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="abe84-173">모델에 입력하기 위해 기능 배열을 사용하여 RDD 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="abe84-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="abe84-174">이 섹션에는 RDD로 tooindex 범주 텍스트 데이터 개체 하 고 한 핫 인코딩 권한 사용된 tootrain 및 테스트 MLlib 로지스틱 회귀 및 트리 기반 모델을 사용할 수 있도록 하는 방법을 보여 주는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="abe84-175">hello 인덱싱된 데이터에 저장 됩니다 [복원 력 있는 분산 데이터 집합 (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="abe84-176">이들은 spark에서 hello 기본 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="abe84-177">RDD 개체는 Spark와 함께 병렬로 작업을 수행할 수 있으며 변경할 수 없고 분할된 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="abe84-178">또한 사용 하 여 tooscale 데이터 hello 하는 방법을 보여 주는 코드가 포함 되어 `StandardScalar` MLlib에서 선형 회귀와 추측 기울기 하강 SGD (), 다양 한 기계 학습 모델을 학습에 널리 사용 되는 알고리즘에서에서 사용 하기 위해 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="abe84-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) 는 사용 되는 tooscale hello 기능 toounit 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="abe84-180">데이터 정규화 라고도 기능 크기 조정 시나리오는 광범위 하 게 분산된 값이 포함 된 기능은 과도 하 게 지정 된 하지 입니까 hello 목표 함수.</span><span class="sxs-lookup"><span data-stu-id="abe84-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="abe84-181">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-181">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-182">셀 위에서 tooexecute에 걸린 시간: 11.72 초</span><span class="sxs-lookup"><span data-stu-id="abe84-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="abe84-183">로지스틱 회귀 모델 hello로 점수와 출력 tooblob 저장</span><span class="sxs-lookup"><span data-stu-id="abe84-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="abe84-184">이 섹션의 hello 코드는 방법을 보여 줍니다 tooload는 로지스틱 회귀 모델을 Azure에 저장 된 blob 저장소 및 팁을 지불 여부 toopredict 택시 여행 사용, 표준 분류 메트릭을 사용 하 여 점수 다음 저장 및 hello 결과 tooblob 그림 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="abe84-185">점수가 매겨진 결과 hello RDD 개체에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="abe84-186">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-186">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-187">셀 위에서 tooexecute에 걸린 시간: 19.22 초</span><span class="sxs-lookup"><span data-stu-id="abe84-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="abe84-188">선형 회귀 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="abe84-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="abe84-189">사용한 [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain 팁 양을 toopredict hello 최적화에 대 한 추측 기울기 하강 SGD ()를 사용 하 여 선형 회귀 모델은 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="abe84-190">이 섹션의 hello 코드 tooload Azure blob 저장소의 선형 회귀 모델이 크기 조정 된 변수를 사용 하 여 점수 하 한 다음 hello 결과 백 toohello blob을 저장 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="abe84-191">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-191">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-192">셀 위에서 tooexecute에 걸린 시간: 16.63 초</span><span class="sxs-lookup"><span data-stu-id="abe84-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="abe84-193">분류 및 회귀 임의 포리스트 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="abe84-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="abe84-194">이 섹션의 hello 코드 tooload hello 분류를 저장 하는 방법을 보여 줍니다. 및 회귀 임의 포리스트 모델과 Azure blob 저장소에 저장 된 표준 분류자 및 회귀 측정값을 성능을 점수를 매깁니다. hello 결과 백 tooblob 저장소를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="abe84-195">[임의 포리스트](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="abe84-196">과잉 맞춤의 많은 의사 결정 트리 tooreduce hello 위험을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="abe84-197">임의 포리스트 범주 기능을 처리할 수 있는 toohello 다중 클래스 분류 설정을 확장를 기능 크기 조정이 필요 하지 않은 미치며 수 toocapture 비 및 상호 작용 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="abe84-198">임의 포리스트는 분류 및 회귀에 대 한 모델을 학습 하는 hello 성공적으로 컴퓨터 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="abe84-199">[spark.mllib](http://spark.apache.org/mllib/) 는 연속 기능과 범주 기능을 둘 다 사용하여 이진 및 다중 클래스 분류와 회귀에 대해 임의 포리스트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="abe84-200">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-200">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-201">셀 위에서 tooexecute에 걸린 시간: 31.07 초</span><span class="sxs-lookup"><span data-stu-id="abe84-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="abe84-202">분류 및 회귀 점진적 향상 트리 모델 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="abe84-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="abe84-203">이 섹션의 hello 코드 tooload 분류 및 회귀 그라데이션 승격 트리 모델에서 Azure blob 저장소, 표준 분류자 및 회귀 측정값을 성능을 점수를 매깁니다. 하 한 다음 hello 결과 백 tooblob 저장소 저장 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="abe84-204">**spark.mllib** 는 연속 기능과 범주 기능을 둘 다 사용하여 이진 분류 및 회귀에 대해 GBT를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="abe84-205">[그라데이션 향상 트리](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT)는 결정 트리의 결합체입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="abe84-206">GBTs 학습 의사 결정 트리 반복적으로 toominimize 손실 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="abe84-207">GBTs 범주 기능을 처리할 수 있는 기능 확장 필요 하지 않으며 수 toocapture 비 미치며는 및 상호 작용 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="abe84-208">또한 다중 클래스 분류 설정에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="abe84-209">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-209">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-210">셀 위에서 tooexecute에 걸린 시간: 14.6 초</span><span class="sxs-lookup"><span data-stu-id="abe84-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="abe84-211">메모리에서 개체 정리 및 점수가 매겨진 파일 위치 인쇄</span><span class="sxs-lookup"><span data-stu-id="abe84-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="abe84-212">**출력:**</span><span class="sxs-lookup"><span data-stu-id="abe84-212">**OUTPUT:**</span></span>

<span data-ttu-id="abe84-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="abe84-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="abe84-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="abe84-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="abe84-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="abe84-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="abe84-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="abe84-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="abe84-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="abe84-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="abe84-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="abe84-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="abe84-219">웹 인터페이스를 통해 Spark 모델 사용</span><span class="sxs-lookup"><span data-stu-id="abe84-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="abe84-220">리비 라는 구성 요소와 상호 작용할는 REST 통해 대화형 쿼리 또는 Spark tooremotely 전송 일괄 처리 작업 하는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="abe84-221">Livy는 HDInsight Spark 클러스터에서 기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="abe84-222">Livy에 대한 자세한 내용은 [Livy를 사용하여 원격으로 Spark 작업 제출](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abe84-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="abe84-223">리비 tooremotely 제출 점수를 일괄 처리 작업을 Azure blob에 저장 한 후 hello 결과 tooanother blob이 작성 하는 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="abe84-224">toodo이 hello Python 스크립트에서 업로드</span><span class="sxs-lookup"><span data-stu-id="abe84-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="abe84-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) hello Spark 클러스터의 toohello blob입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="abe84-226">와 같은 도구를 사용할 수 있습니다 **Microsoft Azure 저장소 탐색기** 또는 **AzCopy** toocopy hello 스크립트 toohello 클러스터 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="abe84-227">이 예에서는 업로드 hello 스크립트 너무***wasb:///example/python/ConsumeGBNYCReg.py***합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="abe84-228">선택 키 hello Spark 클러스터와 연결 된 hello 저장소 계정에 대 한 hello 포털에서 찾을 수 있습니다 필요한 있는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="abe84-229">Toothis 위치를 업로드 한 후이 스크립트는 분산 컨텍스트에서 hello Spark 클러스터 내에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="abe84-230">Hello 모델을 로드 하 고 hello 모델을 기반으로 하는 입력된 파일에서 예측을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="abe84-231">Livy에서 간단한 HTTPS/REST 요청을 만들어 이 스크립트를 원격으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="abe84-232">curl 명령 tooconstruct hello HTTP 요청 tooinvoke hello Python 스크립트를 원격으로 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="abe84-233">CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME hello Spark 클러스터에 대 한 적절 한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="abe84-234">기본 인증과 함께 간단한 HTTPS 호출 하 여 모든 언어 리비 통해 hello 원격 시스템 tooinvoke hello Spark 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="abe84-235">이 HTTP 호출을 수행할 때 편리한 toouse hello Python 요청 라이브러리 것 것 이지만 Azure 함수에서 기본적으로 현재 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="abe84-236">따라서 이전 HTTP 라이브러리가 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="abe84-237">Hello HTTP 호출에 대 한 hello Python 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="abe84-238">이 Python 코드를 너무 추가할 수도 있습니다[Azure 함수](https://azure.microsoft.com/documentation/services/functions/) tootrigger 타이머, 작성, 또는 blob의 업데이트와 같은 다양 한 이벤트에 따라 blob의 점수는 Spark 작업 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="abe84-239">Hello를 사용 하 여 코드 무료 클라이언트 환경을 원한다 면 [Azure 논리 앱](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark 일괄 처리를 hello에 HTTP 동작을 정의 하 여 점수 매기기 **논리 앱 디자이너** 하 고 해당 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="abe84-240">Azure Portal에서 **+새로 만들기** -> **웹 + 모바일** -> **논리 앱**을 선택하여 새 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="abe84-241">hello toobring **논리 앱 디자이너**, hello 이름 hello 논리 앱 및 앱 서비스 계획을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="abe84-242">HTTP 작업을 선택 하 고 hello 다음 그림에에서 표시 된 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe84-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![논리 앱 디자이너](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="abe84-244">다음 작업</span><span class="sxs-lookup"><span data-stu-id="abe84-244">What's next?</span></span>
<span data-ttu-id="abe84-245">**교차 유효성 검사 및 하이퍼 매개 변수 비우기**: 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark를 사용한 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abe84-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

