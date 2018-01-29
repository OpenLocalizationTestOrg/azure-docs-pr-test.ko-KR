---
title: "HDInsight의 Spark MLlib에서 Machine Learning 예제 - Azure | Microsoft Docs"
description: "로지스틱 회귀를 통해 분류를 사용하여 데이터 집합을 분석하는 Machine Learning 앱을 만드는 데 Spark MLlib를 사용하는 방법에 대해 알아봅니다."
keywords: "Spark Machine Learning, Spark Machine Learning 예제"
services: hdinsight
documentationcenter: 
author: mumian
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
ms.date: 12/11/2017
ms.author: jgao
ms.openlocfilehash: 864d34306dad2915a15b032a27600cefdc632bb9
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a>Spark MLlib을 사용하여 Machine Learning 응용 프로그램 빌드 및 데이터 집합 분석

Spark **MLlib**을 사용하여 열린 데이터 집합의 간단한 예측 분석을 수행하기 위해 Machine Learning 응용 프로그램을 만드는 방법에 대해 알아봅니다. Spark의 기본 제공 Machine Learning 라이브러리에서 이 예제는 로지스틱 회귀를 통해 *분류*를 사용합니다. 

> [!TIP]
> 이 예제는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter Notebook으로 사용할 수도 있습니다. Notebook 환경을 통해 Notebook 자체에서 Python 코드 조각을 실행할 수 있습니다. Notebook 내에서 자습서를 수행하려면 Spark 클러스터를 만들고 Jupyter Notebook(`https://CLUSTERNAME.azurehdinsight.net/jupyter`)을 시작합니다. **Python** 폴더에서 Notebook **Spark Machine Learning - MLlib.ipynb를 사용하여 음식 검사 데이터에 대한 예측 분석**을 실행합니다.
>
>

MLlib은 다음 작업에 적합한 유틸리티를 비롯하여 Machine Learning 작업에 유용한 여러 유틸리티를 제공하는 코어 Spark 라이브러리입니다.

* 분류
* 회귀
* 클러스터링
* 항목 모델링
* SVD(특이값 분해) 및 PCA(주성분 분석)
* 가설 테스트 및 샘플 통계 계산

## <a name="what-are-classification-and-logistic-regression"></a>분류 및 로지스틱 회귀란 무엇입니까?
널리 사용되는 Machine Learning 작업인 *분류*는 입력 데이터를 범주로 정렬하는 프로세스입니다. 사용자가 제공하는 입력 데이터에 "레이블"을 할당하는 방법을 파악하는 분류 알고리즘 작업입니다. 예를 들어 입력으로 주식 정보를 받아서 판매할 주식과 보유할 주식의 두 가지 범주로 주식을 나누는 Machine Learning 알고리즘을 고려합니다.

로지스틱 회귀는 분류에 사용되는 알고리즘입니다. Spark의 로지스틱 회귀 API는 *이진 분류*또는 입력 데이터를 두 그룹 중 하나로 분류하는 데 유용합니다. 로지스틱 회귀에 대한 자세한 내용은 [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression)를 참조하세요.

요약하자면, 로지스틱 회귀 프로세스는 입력 벡터가 한 그룹 또는 다른 그룹에 속할 확률을 예측할 수 있는 *로지스틱 함수* 를 만듭니다.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>식품 검사 데이터에 대한 예측 분석 예제
이 예제에서는 [시카고 데이터 포털](https://data.cityofchicago.org/)을 통해 획득한 식품 검사 데이터(**Food_Inspections1.csv**)에 대한 예측 분석을 수행하기 위해 Spark를 사용합니다. 이 데이터 집합에는 각 식품 회사에 대한 정보, 발견된 위반 사항(있는 경우), 검사 결과를 포함하여 시카고에서 수행한 식품 회사 검사에 대한 정보가 포함되어 있습니다. CSV 데이터 파일은 **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**에 있는 클러스터와 연결된 저장소 계정에서 이미 사용할 수 있습니다.

아래 단계에서는 음식 검사에 합격 또는 불합격하는 조건을 볼 수 있는 모델을 개발할 것입니다.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Spark MMLib Machine Learning 앱 빌드 시작
1. [Azure Portal](https://portal.azure.com/)의 시작 보드에서 Spark 클러스터의 타일을 클릭합니다(시작 보드에 고정한 경우). **모두 찾아보기** > **HDInsight 클러스터**에서 클러스터로 이동할 수도 있습니다.   
1. Spark 클러스터 블레이드에서 **클러스터 대시보드**를 클릭하고 **Jupyter Notebook**을 클릭합니다. 메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다.

   > [!NOTE]
   > 또한 브라우저에서 다음 URL을 열어 클러스터에 대한 Jupyter Notebook에 접근할 수 있습니다. **CLUSTERNAME** 을 클러스터의 이름으로 바꿉니다.
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.

    ![Jupyter Notebook 만들기](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "새 Jupyter Notebook 만들기")
1. 새 노트북이 만들어지고 Untitled.pynb 이름으로 열립니다. 맨 위에서 노트북 이름을 클릭하고 식별하기 쉬운 이름을 입력합니다.

    ![노트북 이름 제공](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "노트북 이름 제공")
1. PySpark 커널을 사용하여 노트북을 만들었기 때문에 컨텍스트를 명시적으로 만들 필요가 없습니다. 첫 번째 코드 셀을 실행하면 Spark 및 Hive 컨텍스트가 자동으로 만들어집니다. 이 시나리오에 필요한 형식을 가져와 기계 학습 응용 프로그램 빌드를 시작할 수 있습니다. 그렇게 하려면 셀에 커서를 놓고 **Shift + Enter**를 누릅니다.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>입력 데이터 프레임 구축
`sqlContext` 를 사용하여 구조화된 데이터에 대해 변환을 수행할 수 있습니다. 첫 번째 작업으로 Spark SQL *데이터 프레임*에 샘플 데이터((**Food_Inspections1.csv**))를 로드합니다.

1. 원시 데이터가 CSV 형식이기 때문에 Spark 컨텍스트를 사용하여 파일의 모든 줄을 메모리에 구조화되지 않은 데이터로 가져와야 합니다. 그런 다음 Python의 CSV 라이브러리를 사용하여 각 줄을 개별적으로 구문 분석합니다.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. 이제 RDD로 CSV 파일이 생겼습니다.  데이터 스키마를 이해하기 위해 RDD의 한 행을 검색해 보겠습니다.

        inspections.take(1)

    다음과 유사한 출력이 표시됩니다.

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
1. 위의 출력을 보면 입력 파일의 스키마를 알 수 있습니다. 파일에는 모든 회사의 이름, 회사의 종류, 주소, 검사 데이터 및 위치가 포함되어 있습니다. 예측 분석에 유용한 열 몇 개를 골라서 결과를 데이터 프레임으로 그룹화한 다음 이를 사용하여 임시 테이블을 만들어 보겠습니다.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. 이제 분석을 수행할 수 있는 `df` *데이터 프레임*이 있습니다. 임시 테이블 호출 **CountResults**도 있습니다. 관심이 있는 네 개의 열, 즉 **ID**, **이름**, **결과** 및 **위반**이 이 데이터 프레임에 포함되었습니다.

    작은 데이터 샘플을 가져오겠습니다.

        df.show(5)

    다음과 유사한 출력이 표시됩니다.

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

## <a name="understand-the-data"></a>데이터 이해
1. 데이터 집합에 무엇이 들어 있는지 알아보겠습니다. 예를 들어 **결과** 열에 어떤 값이 있을까요?

        df.select('results').distinct().show()

    다음과 유사한 출력이 표시됩니다.

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
1. 신속한 시각화는 이러한 결과 분포가 나온 이유를 알 수 있게 도와줍니다. 임시 테이블 **CountResults**에 데이터가 이미 있습니다. 테이블에 대해 다음 SQL 쿼리를 실행하여 결과가 배포되는 방법을 보다 잘 이해할 수 있습니다.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    `-o countResultsdf` 앞의 `%%sql` 매직은 쿼리 출력이 Jupyter 서버(일반적으로 클러스터의 헤드 노드)에서 로컬로 유지되도록 합니다. 출력은 [countResultsdf](http://pandas.pydata.org/) 라는 이름이 지정된 **Pandas**데이터 프레임으로 유지됩니다.

    다음과 유사한 출력이 표시됩니다.

    ![SQL 쿼리 출력](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL 쿼리 출력")

    `%%sql` 매직 및 기타 PySpark 커널에서 사용 가능한 매직에 대한 자세한 내용은 [Spark HDInsight 클러스터와 함께 Jupyter Notebook에서 사용 가능한 커널](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)을 참조하세요.
1. 또한 데이터 시각화를 구성하는 데 사용되는 라이브러리인 Matplotlib를 사용하여 플롯을 만들 수 있습니다. 로컬로 유지되는 **countResultsdf** 데이터 프레임에서 플롯을 만들어야 하므로 코드 조각은 `%%local` 매직으로 시작해야 합니다. 그러면 코드가 Jupyter 서버에서 로컬로 실행됩니다.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    다음과 유사한 출력이 표시됩니다.

    ![Spark Machine Learning 응용 프로그램 출력 - 5개의 고유한 검사 결과를 포함하는 원형 차트](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark Machine Learning 결과 출력")
1. 아래는 검사에서 나올 수 있는 5가지 고유한 결과입니다.

   * 회사를 찾을 수 없음
   * 불합격
   * 합격
   * 조건부 합격
   * 폐업

     위반이 있을 때 음식 검사의 결과를 추측할 수 있는 모델을 개발해 보겠습니다. 로지스틱 회귀는 이진 분류 방법이므로 데이터를 두 가지 범주, 즉 **불합격** 및 **합격**으로 그룹화할 수 있습니다. "조건부 합격"도 합격이기 때문에 모델을 학습할 때 두 가지 결과를 동일한 것으로 간주해야 합니다. 나머지 결과("회사를 찾을 수 없음" 또는 "폐업")를 포함한 데이터는 쓸모가 없으므로 교육 집합에서 제거할 것입니다. 이 두 범주는 결과의 극히 일부분에 불과하기 때문에 제거해도 상관 없습니다.
1. 계속해서 기존 데이터 프레임(`df`)을 각 검사가 레이블-위반 쌍으로 표시되는 새 데이터 프레임으로 변환하겠습니다. 이 예에서 레이블 `0.0`은 불합격, 레이블 `1.0`은 합격, 레이블 `-1.0`은 앞의 두 결과를 제외한 기타 결과를 나타냅니다. 새 데이터 프레임을 계산할 때 이러한 기타 결과를 필터링할 것입니다.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    레이블이 지정된 데이터의 한 행을 검색하여 어떤 모양인지 살펴보겠습니다.

        labeledData.take(1)

    다음과 유사한 출력이 표시됩니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a>입력 데이터 프레임으로 로지스틱 회귀 모델 만들기
마지막 작업은 레이블이 지정된 데이터를 로지스틱 회귀로 분석할 수 있는 형식으로 변환하는 것입니다. 로지스틱 회귀 알고리즘에 대한 입력은 *레이블-기능 벡터 쌍*의 집합이어야 하며, 여기서 "기능 벡터"는 입력 지점을 나타내는 숫자의 벡터입니다. 따라서 반구조화되고 자유로운 형식의 주석이 많이 포함된 "위반" 열을 컴퓨터가 쉽게 이해할 수 있는 실수 배열로 변환해야 합니다.

자연 언어를 처리하기 위한 표준 기계 학습 접근 방법 중 하나는 고유한 각 단어에 "인덱스"를 할당한 다음 각 인덱스의 값이 해당 단어의 상대 빈도를 텍스트 문자열에 포함하도록 기계 학습 알고리즘에 벡터를 보내는 것입니다.

MLlib은 이 작업을 간단하게 수행할 수 있는 방법을 제공합니다. 첫째, 각 문자열에서 개별 단어를 가져오기 위해 각 위반 문자열을 "토큰화"합니다. 그런 다음 `HashingTF`을 사용하여 모델을 생성하는 로지스틱 회귀 알고리즘에 전달될 수 있는 기능 벡터로 각 토큰 집합을 변환합니다. "파이프라인"를 사용하여 이 모든 단계를 차례로 수행합니다.

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a>별도의 테스트 데이터 집합에서 모델 평가
앞에 만든 모델을 사용하여 관찰된 위반을 기반으로 새 검사의 결과를 *예측* 할 수 있습니다. **Food_Inspections1.csv** 데이터 집합에서 이 모델을 학습했습니다. 두 번째 데이터 집합인 **Food_Inspections2.csv**를 사용하여 새 데이터에서 이 모델의 강도를 *평가*해 보겠습니다. 이 두 번째 데이터 집합(**Food_Inspections2.csv**)은 이미 클러스터와 연결된 기본 저장소 컨테이너에 있어야 합니다.

1. 다음은 모델에서 생성한 예측을 포함하는 새 데이터 프레임 **predictionsDf**를 만드는 코드 조각입니다. 이 조각은 데이터 프레임을 기반으로 **Predictions**라는 임시 테이블도 만듭니다.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    다음과 유사한 출력이 표시됩니다.

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
1. 예측 중 하나를 살펴보겠습니다. 이 코드 조각을 실행합니다.

        predictionsDf.take(1)

   테스트 데이터 집합에 첫 번째 항목에 대한 예측이 있습니다.
1. `model.transform()` 메서드는 스키마가 같은 모든 새 데이터에 동일한 변환 방법을 적용하여 데이터 분류 방법에 대한 예측에 도달합니다. 몇 가지 간단한 통계를 수행하여 예측의 정확도를 알아볼 수 있습니다.

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    출력은 다음과 같이 표시됩니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Spark에서 로지스틱 회귀를 사용하면 영어로 된 위반 설명과 특정 회사의 음식 검사 합격 또는 불합격 가능성 사이의 관계를 정확하게 예측하는 모델을 얻을 수 있습니다.

## <a name="create-a-visual-representation-of-the-prediction"></a>예측의 시각적 표현 만들기
이제 이 테스트 결과의 이유를 파악하는 데 도움이 되는 최종 시각화를 만들 수 있습니다.

1. 먼저 이전에 만든 **Predictions** 임시 테이블에서 여러 예측 및 결과를 추출합니다. 다음 쿼리는 출력을 *true_positive*, *false_positive*, *true_negative* 및 *false_negative*로 구분합니다. 아래 쿼리에서는 `-q`를 사용하여 시각화를 해제하고 `%%local` 매직에서 사용할 수 있는 데이터 프레임으로 출력을 저장(`-o` 사용)합니다.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. 마지막으로, 다음 조각을 사용하여 **Matplotlib**를 통해 플롯을 생성합니다.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    다음 출력이 표시됩니다.

    ![Spark Machine Learning 응용 프로그램 출력 - 실패한 식품 검사의 원형 차트 비율.](./media/apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark Machine Learning 결과 출력")

    이 차트에서 "긍정" 결과는 불합격한 음식 검사를 참조하는 반면, 부정 결과는 합격한 검사를 참조합니다.

## <a name="shut-down-the-notebook"></a>Notebook 종료
응용 프로그램 실행을 완료한 후 리소스를 해제하도록 Notebook을 종료해야 합니다. 이렇게 하기 위해 Notebook의 **파일** 메뉴에서 **닫기 및 중지**를 클릭합니다. 그러면 Notebook을 종료하고 닫습니다.

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](apache-spark-use-bi-tools.md)
* 
            [Machine Learning과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](apache-spark-ipython-notebook-machine-learning.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark Scala 응용 프로그램 만들기 및 제출](apache-spark-intellij-tool-plugin.md)
* [IntelliJ IDEA용 HDInsight 도구 플러그 인을 사용하여 Spark 응용 프로그램을 원격으로 디버그](apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](apache-spark-jupyter-notebook-use-external-packages.md)
* [컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결](apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리](apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](apache-spark-job-debugging.md)
