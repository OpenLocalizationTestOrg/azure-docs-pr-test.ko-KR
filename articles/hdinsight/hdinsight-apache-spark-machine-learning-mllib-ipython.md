---
title: "Azure HDInsight의 Spark MLlib 예제 학습 aaaMachine | Microsoft Docs"
description: "자세한 내용은 방법 toouse Spark MLlib toocreate 로지스틱 회귀를 통해 분류를 사용 하는 데이터 집합을 분석 하는 컴퓨터 학습 응용 프로그램입니다."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Spark MLlib toobuild 기계 학습 응용 프로그램을 사용 하 고 데이터 집합 분석

자세한 내용은 방법 toouse Spark **MLlib** toocreate 응용 프로그램 toodo 간단한 예측 분석에는 열려 데이터 집합을 학습 하는 컴퓨터입니다. Spark의 기본 제공 Machine Learning 라이브러리에서 이 예제는 로지스틱 회귀를 통해 *분류*를 사용합니다. 

> [!TIP]
> 이 예제는 HDInsight에서 만드는 Spark(Linux) 클러스터에서 Jupyter Notebook으로 사용할 수도 있습니다. hello 노트북 경험 자체 hello 노트북에서 Python 코드 조각을 hello를 실행할 수 있습니다. 노트북, 내에서 toofollow hello 자습서를 만들고는 Spark 클러스터 Jupyter 노트북 시작 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). 그런 다음 실행 하는 hello 노트북 **Spark 기계 학습 MLlib.ipynb를 사용 하 여 음식 검사 데이터에서 예측 분석** hello에서 **Python** 폴더입니다.
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
*분류*, 인기 있는 기계 학습 작업을 hello 프로세스 범주로 입력된 데이터 정렬입니다. Hello 작업 방법에 대해 분류 알고리즘 toofigure의 tooassign "데이터 레이블 지정" tooinput 제공 하는 경우 예를 들어 주식 정보를 입력으로 허용 하는 기계 학습 알고리즘의 고려해 볼 수 있습니다 및 분할의 두 범주에 재고 hello: 주식 판매 해야 하 고 주식 고려해 야 합니다.

로지스틱 회귀는 분류에 사용할 수 있는 hello 알고리즘입니다. Spark의 로지스틱 회귀 API는 *이진 분류*또는 입력 데이터를 두 그룹 중 하나로 분류하는 데 유용합니다. 로지스틱 회귀에 대한 자세한 내용은 [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression)를 참조하세요.

요약 하자면, 로지스틱 회귀의 hello 프로세스는 다음과 같이 생성 됩니다. 한 *로지스틱 함수* 사용된 toopredict hello 속할 확률을 입력된 벡터 한 그룹 또는 다른 hello 일 수 있는 합니다.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>식품 검사 데이터에 대한 예측 분석 예제
이 예제를 사용 하 여 Spark tooperform 일부 예측 분석 음식 검사 데이터에 (**Food_Inspections1.csv**) hello를 통해 획득 [시카고 도시 데이터 포털](https://data.cityofchicago.org/)합니다. 각 설정에 대 한 정보를 포함 하 여 시카고에 수행 되었습니다 음식 설정 검사 하는 방법에 대 한 정보를 포함 하는이 데이터 집합, hello 위반 (있는 경우)을 찾을 수 없으며 hello hello 검사 결과입니다. hello CSV 데이터 파일에서 hello 클러스터와 연결 된 hello 저장소 계정에 이미 있는 **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**합니다.

다음 hello 단계에서 개발 모델 toosee toopass 필요한 것 하거나 음식 검사에 실패 합니다.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Spark MMLib Machine Learning 앱 빌드 시작
1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   
1. Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.

   > [!NOTE]
   > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.

    ![Jupyter Notebook 만들기](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "새 Jupyter Notebook 만들기")
1. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.

    ![Hello 전자 필기장에 대 한 이름을 제공](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "hello 전자 필기장에 대 한 이름을 제공 합니다.")
1. Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다. hello 첫 번째 코드 셀을 실행할 때 사용자에 대 한 hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다. 이 시나리오에 필요한 hello 형식을 가져오는으로 응용 프로그램을 학습 하는 컴퓨터 작성을 시작할 수 있습니다. toodo 누릅니다 hello 셀에 등 hello 커서를 놓고 **SHIFT + ENTER**합니다.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>입력 데이터 프레임 구축
사용할 수 `sqlContext` 구조화 된 데이터에 대 한 tooperform 변형 합니다. hello 첫 번째 작업은 tooload hello 예제 데이터 ((**Food_Inspections1.csv**)) Spark SQL로 *데이터 프레임*합니다.

1. Hello 원시 데이터를 CSV 형식에서 이므로 필요 toouse hello Spark 컨텍스트 toopull hello 파일의 모든 줄을 메모리에 구조화 되지 않은 텍스트로; 그런 다음에서는 Python의 CSV 라이브러리 tooparse 각 줄 개별적으로 합니다.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. 했습니다 hello CSV 파일은 RDD로 합니다.  hello 데이터의 toounderstand hello 스키마, RDD hello에서 한 행을 검색 합니다.

        inspections.take(1)

    Hello 다음과 같은 출력을 표시 되어야 합니다.

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. hello 위의 출력 목록에 hello 입력된 파일의 hello 스키마의 관념 있습니다. 모든 설정, 설정, hello 주소, hello 검사, 및 무엇 보다도 hello 위치 hello 데이터 hello 유형의 hello 이름을 포함합니다. 이제는 예측 분석에 유용 하 고 어떤 म 데이터 프레임으로 hello 결과 그룹화 합니다. 다음 toocreate 임시 테이블을 사용 하 여 몇 가지 열을 선택 하십시오.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. 이제 분석을 수행할 수 있는 `df` *데이터 프레임*이 있습니다. 임시 테이블 호출 **CountResults**도 있습니다. Hello 데이터 프레임에 대 한 관심의 열 4 개 포함 되어: **id**, **이름**, **결과**, 및 **위반**합니다.

    Hello 데이터의 일부 예제를 살펴보겠습니다.

        df.show(5)

    Hello 다음과 같은 출력을 표시 되어야 합니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>Hello 데이터 이해
1. 이 데이터 집합의 포함의 의미 tooget을 시작 하겠습니다. 예를 들어 hello hello에 서로 다른 값 이란 **결과** 열?

        df.select('results').distinct().show()

    Hello 다음과 같은 출력을 표시 되어야 합니다.

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
1. 빠른 시각화는 데 도움이 될 수 이러한 결과의 hello 분포에 대 한 이유입니다. 임시 테이블에 이미 hello 데이터 **CountResults**합니다. hello 결과 어떻게 분포 되어 있는지 알아보려면 hello 다음 테이블 tooget hello에 대 한 SQL 쿼리를 실행할 수 있습니다.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    hello `%%sql` 매직 뒤 `-o countResultsdf` hello 쿼리의 hello 출력 (일반적으로 hello의 헤드 노드에 hello 클러스터) hello Jupyter 서버에서 로컬로 유지 되도록 보장 합니다. hello 출력으로 유지 되는 [팬더](http://pandas.pydata.org/) 데이터 프레임 hello로 이름을 지정 **countResultsdf**합니다.

    Hello 다음과 같은 출력을 표시 되어야 합니다.

    ![SQL 쿼리 출력](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL 쿼리 출력")

    Hello에 대 한 자세한 내용은 `%%sql` 매직, 및 기타 마법 hello PySpark 커널 사용할 수 있는 참조 [Jupyter 노트북 HDInsight Spark 클러스터에서 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)합니다.
1. Matplotlib를 사용할 수도 있습니다, 라이브러리의 데이터를 toocreate 플롯을 tooconstruct 시각화를 사용 합니다. 로컬로 hello에서 hello 플롯을 만들어야 하기 때문에 유지 **countResultsdf** 데이터 프레임을 hello 코드 조각 hello로 시작 해야 `%%local` 매직 합니다. 이렇게 하면 hello 코드 hello Jupyter 서버에서 로컬로 실행 됩니다.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Hello 다음과 같은 출력을 표시 되어야 합니다.

    ![Spark Machine Learning 응용 프로그램 출력 - 5개의 고유한 검사 결과를 포함하는 원형 차트](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark Machine Learning 결과 출력")
1. 아래는 검사에서 나올 수 있는 5가지 고유한 결과입니다.

   * 회사를 찾을 수 없음
   * 불합격
   * 합격
   * 조건부 합격
   * 폐업

     주세요 음식 검사를 특정된 hello 위반의 hello 결과 추측할 수 있는 모델을 개발 해야 합니다. 로지스틱 회귀는 이진 분류 메서드이기 때문에 의미 toogroup 데이터 두 가지 범주로: **실패** 및 **전달**합니다. "통과 지 원하는 조건"은 여전히 패스를, 두 결과 해당 하므로 hello 이라고 생각 hello 모델을 학습 우리는 경우. 데이터 hello로 ("비즈니스 위치 하지 않고" 또는 "Out of 비즈니스")에 다른 결과 유용 하지 않은 학습 집합에서 제거 했습니다. 이이 두 가지 범주 그래도 hello 결과의 매우 작은 비율을 구성 하는 이후을 덮어쓰려면 이어야 합니다.
1. 계속해서 기존 데이터 프레임(`df`)을 각 검사가 레이블-위반 쌍으로 표시되는 새 데이터 프레임으로 변환하겠습니다. 이 예에서 레이블 `0.0`은 불합격, 레이블 `1.0`은 합격, 레이블 `-1.0`은 앞의 두 결과를 제외한 기타 결과를 나타냅니다. Hello 새 데이터 프레임을 계산할 때 해당 다른 결과 필터링 했습니다.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee 어떤 hello 레이블이 지정 된 다음과 같은 데이터, 한 행을 검색 해 보겠습니다.

        labeledData.take(1)

    Hello 다음과 같은 출력을 표시 되어야 합니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Hello 입력된 데이터 프레임에서 로지스틱 회귀 모델 만들기
우리의 마지막 태스크는 tooconvert hello 로지스틱 회귀에서 분석할 수 있는 형식으로 데이터를 표시 합니다. hello 입력된 tooa 로지스틱 회귀 알고리즘 집합이 있어야 합니다. *레이블 기능 벡터 쌍*, 여기서 "기능 벡터" hello는 hello 입력된 시점을 나타내는 숫자의 벡터입니다. 따라서 tooconvert 위반"hello" 열은 반 구조화 된를 실수 하는 컴퓨터에서 쉽게 인식할 수 있는 일반 텍스트 tooan 배열에 설명을 포함 합니다. 필요 합니다.

자연어 처리에 대 한 표준 시스템 학습 방법 중 하나는 tooassign 각 고유한 단어는 "index", 한 다음 벡터 toohello 기계 학습 알고리즘 hello 텍스트에서 단어의 hello 상대 빈도가 각 인덱스의 값이 포함 되도록를 전달합니다 문자열입니다.

MLlib 쉽게 tooperform이이 작업을 제공합니다. 첫째, "토큰화" 각 위반 문자열 tooget hello 개별 단어 각 문자열에서 합니다. 다음을 사용 하 여 한 `HashingTF` 모델 전달된 toohello 로지스틱 회귀 알고리즘 tooconstruct 수 있는 기능 벡터에 각각의 설정 tooconvert 토큰입니다. "파이프라인"를 사용하여 이 모든 단계를 차례로 수행합니다.

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>별도 테스트 데이터 집합에 대해 hello 모델 평가
앞에서 만든 hello 모델을 사용할 수 있습니다 너무*예측* 관찰 hello 위반을 기준으로 새 검사의 결과 될 어떤 hello 합니다. Hello 데이터 집합에이 모델을 학습 우리 **Food_Inspections1.csv**합니다. 두 번째 데이터 집합을 사용 하 여 알려 주세요 **Food_Inspections2.csv**역시*평가* hello 새 데이터에이 모델의 강도입니다. 이 두 번째 데이터 집합 (**Food_Inspections2.csv**) hello 클러스터와 연결 된 hello 기본 저장소 컨테이너에 이미 있어야 합니다.

1. hello 다음 조각에서는 새 데이터 프레임이 **predictionsDf** hello 모델에서 생성 하는 hello 예측 들어 있는입니다. hello 조각도 이라는 임시 테이블을 만들어 **예측** hello 데이터 프레임에 기반 합니다.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Hello 다음과 같은 출력을 표시 되어야 합니다.

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
1. Hello 예측 중 하나를 살펴봅니다. 이 코드 조각을 실행합니다.

        predictionsDf.take(1)

   Hello hello 테스트 데이터 집합의 첫 번째 항목에 대 한 예측이 있습니다.
1. hello `model.transform()` 메서드 적용 hello 동일한 변환 tooany 새 데이터를 동일한 스키마를 hello 및 어떻게 tooclassify hello 데이터의 예측에 도착 합니다. 몇 가지 간단한 통계 tooget 정확도 예측 된 의미를 수행할 수 있습니다.

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    hello 출력 hello 다음과 같습니다.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    로지스틱 회귀를 사용 하 여 Spark와 함께 목록에 정확한 모델의 hello 관계 영어로 위반 설명 및 지정 된 비즈니스 전달 또는 음식 검사 실패는 있습니다.

## <a name="create-a-visual-representation-of-hello-prediction"></a>시각적으로 hello 예측 만들기
이제이 테스트의 결과 hello에 대 한 이유 우리 최종 시각화 toohelp을 만들 수 있습니다.

1. Hello 다양 한 예측을 추출 하 여 시작 하 고 결과를 hello **예측** 앞에서 만든 임시 테이블입니다. hello 쿼리인 별도 hello 출력으로 *true_positive*, *false_positive*, *true_negative*, 및 *false_negative*합니다. Hello 쿼리 아래에 해제 시각화를 사용 하 여 `-q` 도 hello 출력을 저장 하 고 (사용 하 여 `-o`) 다음 hello로 사용할 수 있는 데이터 프레임으로 `%%local` 매직 합니다.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. 마지막으로, 다음 코드 조각 toogenerate hello 점도 사용 하 여 hello를 사용 하 여 **Matplotlib**합니다.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    다음 출력 hello를 표시 되어야 합니다.

    ![Spark Machine Learning 응용 프로그램 출력 - 실패한 식품 검사의 원형 차트 비율.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark Machine Learning 결과 출력")

    이 차트에서는 "positive" 결과 음수 결과 참조 tooa 검사를 전달 하는 동안 실패 toohello 음식 검사를 참조 합니다.

## <a name="shut-down-hello-notebook"></a>Hello 노트북 종료
Hello 응용 프로그램 실행을 완료 한 후 hello 노트북 toorelease hello 리소스를 종료 해야 합니다. toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다. 이 종료 되 고 닫히는 hello 전자 필기장 합니다.

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 응용 프로그램 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)
