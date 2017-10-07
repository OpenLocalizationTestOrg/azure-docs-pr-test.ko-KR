---
title: "Azure HDInsight의 응용 프로그램을 학습 aaaBuild Apache Spark 컴퓨터 | Microsoft Docs"
description: "어떻게 toobuild Apache Spark 기계 HDInsight Spark에서 응용 프로그램을 학습 Jupyter 노트북을 사용 하는 클러스터에 대 한 단계별 지침"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Azure HDInsight에서 Apache Spark 기계 학습 응용 프로그램 빌드

어떻게 toobuild는 Spark를 사용 하 여 Apache Spark 컴퓨터 학습 응용 프로그램는 HDInsight의을 클러스터에 대해 알아봅니다. 이 문서에서는 toouse Jupyter 노트북 hello 클러스터 toobuild 사용할 수 있는 hello 하 고이 응용 프로그램을 테스트 하는 방법을 보여 줍니다. hello 응용 프로그램에는 기본적으로 모든 클러스터에서 사용할 수 있는 hello 샘플 HVAC.csv 데이터 사용 합니다.

**필수 조건:**

Hello 다음이 필요 합니다.

* HDInsight의 Apache Spark 클러스터입니다. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요. 

## <a name="data"></a>Hello 데이터 집합 이해
Hello 응용 프로그램 작성을 시작 하기 전에 hello 데이터를 빌드합니다 hello 응용 프로그램 및 hello 종류의 분석을 수행 합니다 hello 데이터의 hello 구조를 이해 알려 주세요. 

이 문서에서는 사용 하 여 hello 샘플 **HVAC.csv** hello hello HDInsight 클러스터와 연결 된 Azure 저장소 계정에서에서 사용할 수 있는 데이터 파일. Hello 저장소 계정 내에서 hello 파일은 **\HdiSamples\HdiSamples\SensorSampleData\hvac**합니다. 다운로드 하 고 hello CSV 파일 tooget hello 데이터의 스냅숏을 엽니다.  

![Spark 기계 학습 예제에 사용되는 데이터의 스냅숏](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Spark 기계 학습 예제에 사용되는 데이터의 스냅숏")

hello 데이터 hello 대상 온도 HVAC 시스템이 설치 되어 있는 건물 hello 실제 온도 보여 줍니다. Hello를 가정해 보겠습니다 **시스템** 열 hello 시스템 ID 나타내고 hello **SystemAge** 열 hello HVAC 시스템에 이미 사용 되 고 hello 건물에서 년 hello 수를 나타냅니다.

이 데이터 toopredict 건물 hotter 또는 됩니다 colder 기반 hello 대상 온도, 시스템 ID 및 시스템 사용 기간에 있는지 여부를 사용 합니다.

## <a name="app"></a>Spark MLlib를 사용하여 Spark 기계 학습 응용 프로그램 작성
이 응용 프로그램에서 Spark ML 파이프라인 tooperform 문서 분류를 사용합니다. Hello 파이프라인에서는 hello 문서를 단어로 분할 단어 hello를 숫자 기능 벡터를 변환 하 고 마지막으로 hello 기능 벡터 및 레이블을 사용 하 여 예측 모델을 작성 합니다. Hello 단계 toocreate hello 응용 프로그램에 다음을 수행 합니다.

1. Hello에서 [Azure 포털](https://portal.azure.com/), (toohello 시작 보드 고정) 하는 경우 hello 시작 보드에서 Spark 클러스터에 대 한 hello 타일을 클릭 합니다. 아래 tooyour 클러스터를 탐색할 수도 **모두 찾아보기** > **HDInsight 클러스터**합니다.   
2. Hello Spark 클러스터 블레이드에서 클릭 **클러스터 대시보드**, 클릭 하 고 **Jupyter 노트북**합니다. 메시지가 표시 되 면 hello 클러스터에 대 한 hello 관리자 자격 증명을 입력 합니다.
   
   > [!NOTE]
   > 또한 열어 hello URL을 브라우저에서 다음을 통해 클러스터에 대 한 hello Jupyter 노트북에 도달할 수 있습니다. 대체 **CLUSTERNAME** 클러스터의 hello 이름의:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. 새 Notebook을 만듭니다. **새로 만들기**를 클릭한 다음 **PySpark**를 클릭합니다.
   
    ![Spark 기계 학습 예제에 대한 Jupyter 노트북 만들기](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Spark 기계 학습 예제에 대한 Jupyter 노트북 만들기")
4. 새 전자 필기장 만들어지고 Untitled.pynb hello 이름으로 열립니다. Hello 전자 필기장 이름 hello 위쪽에를 클릭 하 고 식별 이름을 입력 하세요.
   
    ![Spark 기계 학습 예제에 대한 노트북 이름 제공](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Spark 기계 학습 예제에 대한 노트북 이름 제공")
5. Hello PySpark 커널을 사용 하 여 노트북에 만들어지므로, 않아도 toocreate 컨텍스트에 명시적으로 합니다. hello Spark 및 하이브 컨텍스트에 자동으로 만들어집니다 드립니다 hello 첫 번째 코드 셀을 실행 하는 경우. 이 시나리오에 대 한 필요한 hello 형식은 가져와서 시작할 수 있습니다. 다음 코드 조각에서 빈 셀을 hello를 붙여 넣고 다음 키를 누릅니다 **SHIFT + ENTER**합니다. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. 이제 hello 데이터 (hvac.csv)를 로드, 구문 분석 하 고, 하며 tootrain hello 모델을 사용 합니다. 이 경우 hello 건물의 실제 온도 hello hello 대상 온도 보다 큰지 여부를 확인 하는 함수를 정의 합니다. Hello 값으로 표시 됨 hello 건물은, 관심 hello 실제 온도 큰 경우 **1.0**합니다. Hello 값으로 표시 됨 hello 건물은 콜드, 더 적은 실제 온도 hello 이면 **0.0**합니다. 
   
    다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. 다음 세 단계로 구성 된 hello Spark 기계 학습 파이프라인 구성: 토크 나이저, hashingTF, 및 lr 합니다. 파이프라인의 정의 및 작동 방법에 대한 자세한 내용은 <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark 기계 학습 파이프라인</a>을 참조하세요.
   
    다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. 적합된 한 hello 파이프라인 toohello 학습 문서입니다. 다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.
   
        model = pipeline.fit(training)
3. Hello 학습 문서 toocheckpoint hello 응용 프로그램을 확인 합니다. 다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.
   
        training.show()
   
    Hello 출력 유사한 toohello 다음과 비슷할 수 있습니다.
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    이전 단계로 이동 하 고 hello 원시 CSV 파일에 대 한 hello 출력을 확인 합니다. 예를 들어 hello 첫 번째 행 hello CSV 파일은이 데이터:

    ![Spark 기계 학습 예제에 대한 출력 데이터 스냅숏](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Spark 기계 학습 예제에 대한 출력 데이터 스냅숏")

    Hello 실제 온도 hello 대상 온도 hello 건물을 제안 하는 것 보다 작습니다는 콜드 하는 방법을 확인 합니다. 따라서 hello 교육 출력에 대 한 값을 hello **레이블** hello에 첫 번째 행은 **0.0**, hello 건물 핫 하지 않음을 의미 합니다.

1. 데이터 집합 toorun hello 학습된 된 모델에 대해 준비 합니다. toodo, 시스템 ID 및 시스템 사용 기간에 전달 합니다 (로 표시 된 **SystemInfo** hello 교육 출력에), hello 모델은 예측 및 여부는 hotter (구분 1.0) 해당 시스템 ID와 시스템 기간이 작성 또는 냉각기 (hello 로 표시 한 0.0)입니다.
   
   다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. 마지막으로 hello 테스트 데이터에서 예측을 수행 합니다. 다음 코드 조각에서 빈 셀과 키를 눌러 붙여넣기 hello **SHIFT + ENTER**합니다.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. 출력 유사한 toohello 다음을 나타나야 합니다.
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   Hello hello 예측의 첫 번째 행을 볼 수 있습니다 ID 20 및 시스템 기간을 25 년 HVAC 시스템에 대 한 hello 건물 되도록 핫 (**예측 = 1.0**). hello DenseVector (0.49999)에 대 한 첫 번째 값 0.0 toohello 예측을 해당 하 고 hello 두 번째 값 (0.5001) toohello 예측 1.0에 해당 합니다. Hello 출력에 있지만 hello 두 번째 값은 훨씬 더 높거나만 hello 모델은 **예측 = 1.0**합니다.
4. Hello 응용 프로그램 실행을 완료 한 후 종료 hello 노트북 toorelease hello 리소스 해야 합니다. toodo hello에서 그러한 **파일** hello 노트북에서 메뉴를 클릭 **닫고 중단**합니다. 이 종료 및 닫기 hello 전자 필기장 합니다.

## <a name="anaconda"></a>Spark 기계 학습에 대한 Anaconda scikit-learn 라이브러리 사용
HDInsight에서 Apache Spark 클러스터에는 Anaconda 라이브러리가 포함되어 있습니다. 또한 hello 포함 **scikit-자세한** 기계 학습에 대 한 라이브러리입니다. 또한 hello 라이브러리 Jupyter 노트북에서 직접 toobuild 샘플 응용 프로그램을 사용할 수 있는 다양 한 데이터 집합을 포함 합니다. 사용 하는 예제 scikit hello에 대 한-라이브러리에 알아보기, 참조 [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html)합니다.

## <a name="seealso"></a>참고 항목
* [개요: Azure HDInsight에서 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>시나리오
* [BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행](hdinsight-apache-spark-use-bi-tools.md)
* [Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight의 Spark를 사용하여 웹 사이트 로그 분석](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>응용 프로그램 만들기 및 실행
* [Scala를 사용하여 독립 실행형 응용 프로그램 만들기](hdinsight-apache-spark-create-standalone-application.md)
* [Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장
* [IntelliJ 아이디어 toocreate에 대 한 HDInsight 도구 플러그 인을 사용 하 고 스파크 Scala 개 제출](hdinsight-apache-spark-intellij-tool-plugin.md)
* [IntelliJ 아이디어 toodebug Spark 응용 프로그램에 대 한 HDInsight 도구 플러그 인을 원격으로 사용](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>리소스 관리
* [Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.](hdinsight-apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
