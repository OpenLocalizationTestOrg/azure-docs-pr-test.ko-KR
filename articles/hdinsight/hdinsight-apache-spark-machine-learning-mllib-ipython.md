---
title: "HDInsight의 Spark MLlib에서 Machine Learning 예제 - Azure | Microsoft Docs"
description: "로지스틱 회귀를 통해 분류를 사용하여 데이터 집합을 분석하는 Machine Learning 앱을 만드는 데 Spark MLlib를 사용하는 방법에 대해 알아봅니다."
keywords: "Spark Machine Learning, Spark Machine Learning 예제"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="c5a24-104">Spark MLlib을 사용하여 Machine Learning 응용 프로그램 빌드 및 데이터 집합 분석</span><span class="sxs-lookup"><span data-stu-id="c5a24-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="c5a24-105">Spark **MLlib**을 사용하여 열린 데이터 집합의 간단한 예측 분석을 수행하기 위해 Machine Learning 응용 프로그램을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="c5a24-106">Spark의 기본 제공 Machine Learning 라이브러리에서 이 예제는 로지스틱 회귀를 통해 *분류*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="c5a24-107">이 예제는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter Notebook으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="c5a24-108">Notebook 환경을 통해 Notebook 자체에서 Python 코드 조각을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="c5a24-109">Notebook 내에서 자습서를 수행하려면 Spark 클러스터를 만들고 Jupyter Notebook(`https://CLUSTERNAME.azurehdinsight.net/jupyter`)을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="c5a24-110">**Python** 폴더에서 Notebook **Spark Machine Learning - MLlib.ipynb를 사용하여 음식 검사 데이터에 대한 예측 분석**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="c5a24-111">MLlib은 다음 작업에 적합한 유틸리티를 비롯하여 Machine Learning 작업에 유용한 여러 유틸리티를 제공하는 코어 Spark 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="c5a24-112">분류</span><span class="sxs-lookup"><span data-stu-id="c5a24-112">Classification</span></span>
* <span data-ttu-id="c5a24-113">회귀</span><span class="sxs-lookup"><span data-stu-id="c5a24-113">Regression</span></span>
* <span data-ttu-id="c5a24-114">클러스터링</span><span class="sxs-lookup"><span data-stu-id="c5a24-114">Clustering</span></span>
* <span data-ttu-id="c5a24-115">항목 모델링</span><span class="sxs-lookup"><span data-stu-id="c5a24-115">Topic modeling</span></span>
* <span data-ttu-id="c5a24-116">SVD(특이값 분해) 및 PCA(주성분 분석)</span><span class="sxs-lookup"><span data-stu-id="c5a24-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="c5a24-117">가설 테스트 및 샘플 통계 계산</span><span class="sxs-lookup"><span data-stu-id="c5a24-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="c5a24-118">분류 및 로지스틱 회귀란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c5a24-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="c5a24-119">널리 사용되는 Machine Learning 작업인 *분류*는 입력 데이터를 범주로 정렬하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="c5a24-120">사용자가 제공하는 입력 데이터에 "레이블"을 할당하는 방법을 파악하는 분류 알고리즘 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="c5a24-121">예를 들어 입력으로 주식 정보를 받아서 판매할 주식과 보유할 주식의 두 가지 범주로 주식을 나누는 Machine Learning 알고리즘을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="c5a24-122">로지스틱 회귀는 분류에 사용되는 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="c5a24-123">Spark의 로지스틱 회귀 API는 *이진 분류*또는 입력 데이터를 두 그룹 중 하나로 분류하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="c5a24-124">로지스틱 회귀에 대한 자세한 내용은 [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5a24-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="c5a24-125">요약하자면, 로지스틱 회귀 프로세스는 입력 벡터가 한 그룹 또는 다른 그룹에 속할 확률을 예측할 수 있는 *로지스틱 함수* 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="c5a24-126">식품 검사 데이터에 대한 예측 분석 예제</span><span class="sxs-lookup"><span data-stu-id="c5a24-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="c5a24-127">이 예제에서는 [시카고 데이터 포털](https://data.cityofchicago.org/)을 통해 획득한 식품 검사 데이터(**Food_Inspections1.csv**)에 대한 예측 분석을 수행하기 위해 Spark를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="c5a24-128">이 데이터 집합에는 각 식품 회사에 대한 정보, 발견된 위반 사항(있는 경우), 검사 결과를 포함하여 시카고에서 수행한 식품 회사 검사에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="c5a24-129">CSV 데이터 파일은 **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**에 있는 클러스터와 연결된 저장소 계정에서 이미 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="c5a24-130">아래 단계에서는 음식 검사에 합격 또는 불합격하는 조건을 볼 수 있는 모델을 개발할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="c5a24-131">Spark MMLib Machine Learning 앱 빌드 시작</span><span class="sxs-lookup"><span data-stu-id="c5a24-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="c5a24-132">[Azure Portal](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터의 타일을 클릭합니다(시작 보드에 고정한 경우).</span><span class="sxs-lookup"><span data-stu-id="c5a24-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="c5a24-133">**모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="c5a24-134">Spark 클러스터 블레이드에서 **클러스터 대시보드**를 클릭하고 **Jupyter Notebook**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="c5a24-135">메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c5a24-136">또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="c5a24-137">**CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="c5a24-138">Notebook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-138">Create a notebook.</span></span> <span data-ttu-id="c5a24-139">**새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="c5a24-140">![Jupyter Notebook 만들기](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "새 Jupyter Notebook 만들기")</span><span class="sxs-lookup"><span data-stu-id="c5a24-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="c5a24-141">새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="c5a24-142">맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="c5a24-143">![노트북 이름 제공](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "노트북 이름 제공")</span><span class="sxs-lookup"><span data-stu-id="c5a24-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="c5a24-144">PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="c5a24-145">첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="c5a24-146">이 시나리오에 필요한 형식을 가져와 기계 학습 응용 프로그램 빌드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="c5a24-147">그렇게 하려면 셀에 커서를 놓고 **Shift + Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="c5a24-148">입력 데이터 프레임 구축</span><span class="sxs-lookup"><span data-stu-id="c5a24-148">Construct an input dataframe</span></span>
<span data-ttu-id="c5a24-149">`sqlContext` 를 사용하여 구조화된 데이터에 대해 변환을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="c5a24-150">첫 번째 작업으로 Spark SQL *데이터 프레임*에 샘플 데이터((**Food_Inspections1.csv**))를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="c5a24-151">원시 데이터가 CSV 형식이기 때문에 Spark 컨텍스트를 사용하여 파일의 모든 줄을 메모리에 구조화되지 않은 데이터로 가져와야 합니다. 그런 다음 Python의 CSV 라이브러리를 사용하여 각 줄을 개별적으로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="c5a24-152">이제 RDD로 CSV 파일이 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="c5a24-153">데이터 스키마를 이해하기 위해 RDD의 한 행을 검색해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="c5a24-154">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="c5a24-155">위의 출력을 보면 입력 파일의 스키마를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="c5a24-156">파일에는 모든 회사의 이름, 회사의 종류, 주소, 검사 데이터 및 위치가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="c5a24-157">예측 분석에 유용한 열 몇 개를 골라서 결과를 데이터 프레임으로 그룹화한 다음 이를 사용하여 임시 테이블을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="c5a24-158">이제 분석을 수행할 수 있는 `df` *데이터 프레임*이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="c5a24-159">임시 테이블 호출 **CountResults**도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="c5a24-160">관심이 있는 네 개의 열, 즉 **ID**, **이름**, **결과** 및 **위반**이 이 데이터 프레임에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="c5a24-161">작은 데이터 샘플을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="c5a24-162">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="c5a24-163">데이터 이해</span><span class="sxs-lookup"><span data-stu-id="c5a24-163">Understand the data</span></span>
1. <span data-ttu-id="c5a24-164">데이터 집합에 무엇이 들어 있는지 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="c5a24-165">예를 들어 **결과** 열에 어떤 값이 있을까요?</span><span class="sxs-lookup"><span data-stu-id="c5a24-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="c5a24-166">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="c5a24-167">신속한 시각화는 이러한 결과 분포가 나온 이유를 알 수 있게 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="c5a24-168">임시 테이블 **CountResults**에 데이터가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="c5a24-169">테이블에 대해 다음 SQL 쿼리를 실행하여 결과가 배포되는 방법을 보다 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="c5a24-170">`-o countResultsdf` 앞의 `%%sql` 매직은 쿼리 출력이 Jupyter 서버(일반적으로 클러스터의 헤드 노드)에서 로컬로 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="c5a24-171">출력은 [countResultsdf](http://pandas.pydata.org/) 라는 이름이 지정된 **Pandas**데이터 프레임으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="c5a24-172">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-172">You should see an output like the following:</span></span>

    <span data-ttu-id="c5a24-173">![SQL 쿼리 출력](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL 쿼리 출력")</span><span class="sxs-lookup"><span data-stu-id="c5a24-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="c5a24-174">`%%sql` 매직 및 기타 PySpark 커널에서 사용 가능한 매직에 대한 자세한 내용은 [Spark HDInsight 클러스터와 함께 Jupyter Notebook에서 사용 가능한 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5a24-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="c5a24-175">또한 데이터 시각화를 구성하는 데 사용되는 라이브러리인 Matplotlib를 사용하여 플롯을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="c5a24-176">로컬로 유지되는 **countResultsdf** 데이터 프레임에서 플롯을 만들어야 하므로 코드 조각은 `%%local` 매직으로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="c5a24-177">그러면 코드가 Jupyter 서버에서 로컬로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="c5a24-178">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-178">You should see an output like the following:</span></span>

    <span data-ttu-id="c5a24-179">![Spark Machine Learning 응용 프로그램 출력 - 5개의 고유한 검사 결과를 포함하는 원형 차트](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark Machine Learning 결과 출력")</span><span class="sxs-lookup"><span data-stu-id="c5a24-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="c5a24-180">아래는 검사에서 나올 수 있는 5가지 고유한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="c5a24-181">회사를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="c5a24-181">Business not located</span></span>
   * <span data-ttu-id="c5a24-182">불합격</span><span class="sxs-lookup"><span data-stu-id="c5a24-182">Fail</span></span>
   * <span data-ttu-id="c5a24-183">합격</span><span class="sxs-lookup"><span data-stu-id="c5a24-183">Pass</span></span>
   * <span data-ttu-id="c5a24-184">조건부 합격</span><span class="sxs-lookup"><span data-stu-id="c5a24-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="c5a24-185">폐업</span><span class="sxs-lookup"><span data-stu-id="c5a24-185">Out of Business</span></span>

     <span data-ttu-id="c5a24-186">위반이 있을 때 음식 검사의 결과를 추측할 수 있는 모델을 개발해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="c5a24-187">로지스틱 회귀는 이진 분류 방법이므로 데이터를 두 가지 범주, 즉 **불합격** 및 **합격**으로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="c5a24-188">"조건부 합격"도 합격이기 때문에 모델을 학습할 때 두 가지 결과를 동일한 것으로 간주해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="c5a24-189">나머지 결과("회사를 찾을 수 없음" 또는 "폐업")를 포함한 데이터는 쓸모가 없으므로 교육 집합에서 제거할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="c5a24-190">이 두 범주는 결과의 극히 일부분에 불과하기 때문에 제거해도 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="c5a24-191">계속해서 기존 데이터 프레임(`df`)을 각 검사가 레이블-위반 쌍으로 표시되는 새 데이터 프레임으로 변환하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="c5a24-192">이 예에서 레이블 `0.0`은 불합격, 레이블 `1.0`은 합격, 레이블 `-1.0`은 앞의 두 결과를 제외한 기타 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="c5a24-193">새 데이터 프레임을 계산할 때 이러한 기타 결과를 필터링할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="c5a24-194">레이블이 지정된 데이터의 한 행을 검색하여 어떤 모양인지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="c5a24-195">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="c5a24-196">입력 데이터 프레임으로 로지스틱 회귀 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="c5a24-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="c5a24-197">마지막 작업은 레이블이 지정된 데이터를 로지스틱 회귀로 분석할 수 있는 형식으로 변환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="c5a24-198">로지스틱 회귀 알고리즘에 대한 입력은 *레이블-기능 벡터 쌍*의 집합이어야 하며, 여기서 "기능 벡터"는 입력 지점을 나타내는 숫자의 벡터입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="c5a24-199">따라서 반구조화되고 자유로운 형식의 주석이 많이 포함된 "위반" 열을 컴퓨터가 쉽게 이해할 수 있는 실수 배열로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="c5a24-200">자연 언어를 처리하기 위한 표준 기계 학습 접근 방법 중 하나는 고유한 각 단어에 "인덱스"를 할당한 다음 각 인덱스의 값이 해당 단어의 상대 빈도를 텍스트 문자열에 포함하도록 기계 학습 알고리즘에 벡터를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="c5a24-201">MLlib은 이 작업을 간단하게 수행할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="c5a24-202">첫째, 각 문자열에서 개별 단어를 가져오기 위해 각 위반 문자열을 "토큰화"합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="c5a24-203">그런 다음 `HashingTF`을 사용하여 모델을 생성하는 로지스틱 회귀 알고리즘에 전달될 수 있는 기능 벡터로 각 토큰 집합을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="c5a24-204">"파이프라인"를 사용하여 이 모든 단계를 차례로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="c5a24-205">별도의 테스트 데이터 집합에서 모델 평가</span><span class="sxs-lookup"><span data-stu-id="c5a24-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="c5a24-206">앞에 만든 모델을 사용하여 관찰된 위반을 기반으로 새 검사의 결과를 *예측* 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="c5a24-207">**Food_Inspections1.csv** 데이터 집합에서 이 모델을 학습했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="c5a24-208">두 번째 데이터 집합인 **Food_Inspections2.csv**를 사용하여 새 데이터에서 이 모델의 강도를 *평가*해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="c5a24-209">이 두 번째 데이터 집합(**Food_Inspections2.csv**)은 이미 클러스터와 연결된 기본 저장소 컨테이너에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="c5a24-210">다음은 모델에서 생성한 예측을 포함하는 새 데이터 프레임 **predictionsDf**를 만드는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="c5a24-211">이 조각은 데이터 프레임을 기반으로 **Predictions**라는 임시 테이블도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="c5a24-212">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="c5a24-213">예측 중 하나를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-213">Look at one of the predictions.</span></span> <span data-ttu-id="c5a24-214">이 코드 조각을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="c5a24-215">테스트 데이터 집합에 첫 번째 항목에 대한 예측이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="c5a24-216">`model.transform()` 메서드는 스키마가 같은 모든 새 데이터에 동일한 변환 방법을 적용하여 데이터 분류 방법에 대한 예측에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="c5a24-217">몇 가지 간단한 통계를 수행하여 예측의 정확도를 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="c5a24-218">출력은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="c5a24-219">Spark에서 로지스틱 회귀를 사용하면 영어로 된 위반 설명과 특정 회사의 음식 검사 합격 또는 불합격 가능성 사이의 관계를 정확하게 예측하는 모델을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="c5a24-220">예측의 시각적 표현 만들기</span><span class="sxs-lookup"><span data-stu-id="c5a24-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="c5a24-221">이제 이 테스트 결과의 이유를 파악하는 데 도움이 되는 최종 시각화를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="c5a24-222">먼저 이전에 만든 **Predictions** 임시 테이블에서 여러 예측 및 결과를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="c5a24-223">다음 쿼리는 출력을 *true_positive*, *false_positive*, *true_negative* 및 *false_negative*로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="c5a24-224">아래 쿼리에서는 `-q`를 사용하여 시각화를 해제하고 `%%local` 매직에서 사용할 수 있는 데이터 프레임으로 출력을 저장(`-o` 사용)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="c5a24-225">마지막으로, 다음 조각을 사용하여 **Matplotlib**를 통해 플롯을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="c5a24-226">다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-226">You should see the following output:</span></span>

    <span data-ttu-id="c5a24-227">![Spark Machine Learning 응용 프로그램 출력 - 실패한 식품 검사의 원형 차트 비율.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark Machine Learning 결과 출력")</span><span class="sxs-lookup"><span data-stu-id="c5a24-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="c5a24-228">이 차트에서 "긍정" 결과는 불합격한 음식 검사를 참조하는 반면, 부정 결과는 합격한 검사를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="c5a24-229">Notebook 종료</span><span class="sxs-lookup"><span data-stu-id="c5a24-229">Shut down the notebook</span></span>
<span data-ttu-id="c5a24-230">응용 프로그램 실행을 완료한 후 리소스를 해제하도록 Notebook을 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="c5a24-231">이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="c5a24-232">그러면 Notebook을 종료하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a24-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="c5a24-233"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="c5a24-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c5a24-234">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="c5a24-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c5a24-235">시나리오</span><span class="sxs-lookup"><span data-stu-id="c5a24-235">Scenarios</span></span>
* [<span data-ttu-id="c5a24-236">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="c5a24-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c5a24-237">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="c5a24-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c5a24-238">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c5a24-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c5a24-239">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="c5a24-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c5a24-240">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="c5a24-240">Create and run applications</span></span>
* [<span data-ttu-id="c5a24-241">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c5a24-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c5a24-242">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c5a24-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c5a24-243">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="c5a24-243">Tools and extensions</span></span>
* [<span data-ttu-id="c5a24-244">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="c5a24-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c5a24-245">IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그</span><span class="sxs-lookup"><span data-stu-id="c5a24-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c5a24-246">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="c5a24-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c5a24-247">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="c5a24-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c5a24-248">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="c5a24-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c5a24-249">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="c5a24-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c5a24-250">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="c5a24-250">Manage resources</span></span>
* [<span data-ttu-id="c5a24-251">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="c5a24-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c5a24-252">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="c5a24-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
