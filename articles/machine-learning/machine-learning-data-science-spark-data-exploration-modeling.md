---
title: "aaaData 탐색 및 모델링 spark | Microsoft Docs"
description: "전시는 데이터 탐색 및 모델링 기능 hello Spark MLlib 도구 키트에서 Azure의 hello 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Spark로 데이터 탐색 및 모델링
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

이 연습에서는 HDInsight Spark toodo 데이터 탐색을 사용 및 택시 여행 및 2013 dataset 있어 이진 분류 및 회귀 샘플 hello NYC 모델링 하는 작업.  Hello hello 단계가 안내 합니다 [데이터 과학 프로세스](http://aka.ms/datascienceprocess), HDInsight Spark를 사용 하 여 끝에 처리를 위해 클러스터 및 Azure blob toostore hello 데이터 및 hello 모델. hello 프로세스 탐색 하 고, Azure 저장소 Blob에서 가져온 데이터를 시각화 합니다. 하 고, 다음 예측 모델 hello 데이터 toobuild를 준비 합니다. 이러한 모델은 hello Spark MLlib toolkit toodo 이진 분류 및 회귀 모델링 작업을 사용 하 여 빌드입니다.

* hello **이진 분류** 작업이 toopredict hello 여행에 대 한 팁을 지불 여부. 
* hello **회귀** 작업은 toopredict hello 양의 hello 팁 다른 팁 기능을 기반으로 합니다. 

hello 모델을 사용 하 여 로지스틱 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리에 포함:

* [선형 회귀와 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 추측 기울기 하강 SGD () 메서드를 사용 하는 선형 회귀 모델은 및 최적화 및 기능에 대 한 결제 toopredict hello 팁 금액을 확장 합니다. 
* [로지스틱 회귀와 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 또는 "logit" 회귀는 hello 종속 변수는 범주 toodo 데이터 분류에 사용할 수 있는 회귀 모델입니다. LBFGS는 제한 된 양의 컴퓨터 메모리를 사용 하 여 hello Broyden – Fletcher – Goldfarb – (SHANNO) 알고리즘의 근사치를 계산 하 고 기계 학습에서 널리 사용 되는 준 뉴턴 최적화 알고리즘입니다.
* [임의 포리스트](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 는 결정 트리의 결합체입니다.  과잉 맞춤의 많은 의사 결정 트리 tooreduce hello 위험을 결합 합니다. 임의 포리스트는 분류 및 회귀에 사용 범주 기능을 처리할 수 있습니다 및 toohello 다중 클래스 분류 설정을 확장 될 수 있습니다. 기능 크기 조정 및가 수 toocapture 비 미치며 및 상호 작용 기능이 필요 하지 않습니다. 임의 포리스트는 분류 및 회귀에 대 한 모델을 학습 하는 hello 성공적으로 컴퓨터 중 하나입니다.
* [GBT](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (그라데이션 승격 트리)는 결정 트리의 결합체입니다. GBTs 학습 의사 결정 트리 반복적으로 toominimize 손실 함수입니다. GBTs 회귀 및 분류에 대 한 사용 및 범주 기능을 처리할 수 있는, 기능 크기 조정이 필요 하지 않습니다 이며 미치며 수 toocapture 비 및 상호 작용 기능입니다. 또한 다중 클래스 분류 설정에도 사용할 수 있습니다.

hello 모델링 단계 tootrain를 평가 하 고 각 유형의 모델을 저장 하는 방법을 보여 주는 코드도 포함 됩니다. Python은 사용 되는 toocode hello 솔루션과 tooshow hello 관련 점도 되었습니다.   

> [!NOTE]
> Hello Spark MLlib toolkit은 큰 데이터 집합에서 설계 된 toowork를 상대적으로 작은 샘플 (행 170 K hello 원래 NYC 데이터 집합의 0.1%에 대 한 정보를 사용 하 여 최대 30 Mb) 편의 위해 사용 됩니다. hello 연습 여기에 나와 효율적으로 (약 10 분 후에) 작업자 노드 2 개 사용 하는 HDInsight 클러스터에서 실행 됩니다. hello 약간의 수정 된 동일한 코드 수 tooprocess 사용 되는 데이터 집합이 큰 경우-, 적절 한 수정이 데이터를 메모리에에서 캐시 하 고 hello 클러스터 크기를 변경 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
Azure 계정 및는 Spark 1.6 (또는)가 필요한 Spark 2.0 HDInsight 클러스터 toocomplete이이 연습 합니다. Hello 참조 [개요의 데이터 과학 Azure HDInsight의 Spark를 사용 하 여](machine-learning-data-science-spark-overview.md) 방법에 대 한 지침은 toosatisfy 이러한 요구 사항입니다. 해당 항목에는 여기에 NYC 2013 택시 데이터 hello 및 tooexecute hello Spark 클러스터에서 Jupyter 노트북에서 코드가 하는 방식에 대 한 지침에 대 한 설명을 포함 되어 있습니다. 

## <a name="spark-clusters-and-notebooks"></a>Spark 클러스터 및 Notebook
설치 단계와 코드는 HDInsight Spark 1.6을 사용하는 이 연습에 제공됩니다. 하지만 Jupyter Notebook은 HDInsight Spark 1.6과 Spark 2.0 클러스터 둘 다에 제공됩니다. Hello에 전자 필기장 및 링크 toothem hello에 대 한 설명을 제공 됩니다 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 이 포함 하는 hello GitHub 리포지토리에 대 한 합니다. 또한 hello 코드와 연결 된 hello 전자 필기장에서 제네릭 인데 어떤 Spark 클러스터에서 작동 해야 합니다. HDInsight Spark를 사용 하지 않는 경우 hello 클러스터 설치 및 관리 단계는 여기 표시 된에서 약간 다를 수 있습니다. 편의 위해 링크는 다음과 같습니다 hello Spark 1.6 (toobe hello pySpark 커널의 hello Jupyter 노트북 서버에서 실행) 및 Spark 2.0 (toobe hello pySpark3 커널의 hello Jupyter 노트북 서버에서 실행)에 대 한 toohello Jupyter 노트북:

### <a name="spark-16-notebooks"></a>Spark 1.6 Notebook

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): 방법에 대해 설명 tooperform 데이터 탐색, 모델링 및 다양 한 알고리즘이 점수 매기기입니다.

### <a name="spark-20-notebooks"></a>Spark 2.0 Notebook
2.0 Spark 클러스터를 사용 하 여 구현 되는 hello 분류 및 회귀 작업 별도 노트북에 있고 다른 데이터 집합을 사용 하 여 hello 분류 노트북:

- [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb):이 파일 어떻게 tooperform 데이터 탐색, 모델링 및 Spark 2.0에서 점수 매기기 클러스터 NYC 택시 여행 hello를 사용 하 여에 정보를 제공 합니다. 및 데이터 집합 설명 요금 [여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)합니다. 이 전자 필기장 신속 하 게 Spark 2.0를 제공 하는 hello 코드를 탐색 하기 위한 좋은 출발점 수도 있습니다. 더 자세한 노트북 hello NYC 택시 데이터를 분석에 대 한이 목록에 다음 노트북을 hello를 참조 하십시오. 이러한 전자 필기장을 비교 하는이 목록 다음 되는 hello 메모를 참조 하세요. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb):이 파일은 NYC 택시 여행 및 요금 데이터 집합 설명 tooperform 데이터 wrangling (Spark SQL 및 데이터 프레임 작업) 탐색을 모델링 하 고 사용 하 여 점수 매기기 hello 하는 방법을 보여 줍니다. [ 여기](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)합니다.
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb):이 파일은 tooperform 데이터 wrangling (Spark SQL 및 데이터 프레임 작업) 탐색을 모델링 하 고 사용 하 여 점수 매기기 잘 알려진 Airline 정시 출발 hello 하는 방법을 보여 줍니다. 2011 및 2012에서 데이터 집합입니다. 에서는 통합 hello airline 데이터 집합 hello 공항 날씨 데이터 (예:: windspeed, 온도, 고도 등) 이전 toomodeling, 되므로 이러한 날씨 기능 hello 모델에 포함 될 수 있습니다.

<!-- -->

> [!NOTE]
> hello airline 데이터 집합 추가 toohello Spark 2.0 전자 필기장 toobetter 분류 알고리즘의 hello 사용을 보여 줍니다. Airline 정시 출발 집합과 날씨 데이터 집합에 대 한 정보에 대 한 링크를 따라 hello 참조:

>- 항공사 정시 출발 데이터: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- 공항 날씨 데이터: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
hello NYC 택시에서 hello Spark 2.0 전자 필기장 및 airline 비행 지연 데이터 집합에는 10 분 또는 (hello의 크기에 따라 HDI 클러스터) 자세한 toorun 걸릴 수 있습니다. hello 목록 위의 hello에서 첫 번째 노트북 hello 데이터 탐색의 다양 한 부분, 시각화 및 기계 학습 모델 교육 축소 샘플링 NYC 데이터 집합으로는 hello 택시 및 요금 파일 미리 조인 했습니다 적은 시간 toorun 받아들이는 노트북: [ Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) 이 노트북은 훨씬 더 짧은 시간 toofinish (2-3 분) 걸리고 있습니다 수 좋은 시작 지점 신속 하 게 hello 코드 탐색에 대 한 했으므로 Spark 2.0에 대 한 제공 합니다. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
hello 설명은 아래에 관련된 toousing Spark 1.6 됩니다. Spark 2.0 버전에 대 한 설명 하 고 위에 링크 된 hello 노트북을 사용 하십시오. 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>설정: 저장소 위치, 라이브러리 및 hello Spark 컨텍스트 사전 설정
Spark 수 tooread 및 쓰기 tooAzure Blob 저장소 (WASB)입니다. 따라서 여기에 저장 된 기존 데이터의 Spark를 사용 하 여 처리할 수 하 고 hello에 다시 저장된 WASB 있습니다.

toosave 모델 또는 WASB의 파일을 제대로 지정 toobe hello 경로 필요 합니다. hello 기본 연결 된 컨테이너 toohello Spark 클러스터를 참조할 수 있습니다로 시작 하는 경로 사용 하 여: "wasb: / / /"입니다. 다른 위치를 “wasb://”에서 참조합니다.

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>WASB의 저장소 위치에 대한 디렉터리 경로를 설정합니다.
hello 다음 코드 샘플 hello의 위치를 지정 hello 데이터 toobe 읽기 및 hello 모델 저장소 디렉터리 toowhich hello 모델 출력에 대 한 hello 경로가 저장 됩니다.

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>라이브러리 가져오기
또한 필요한 라이브러리를 가져와야 합니다. Spark 컨텍스트를 설정 하 여 코드 다음 hello로 필요한 라이브러리를 가져옵니다.

    # IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a>미리 설정된 Spark 컨텍스트 및 PySpark 매직
Jupyter 노트북에 제공 되는 hello PySpark 커널에는 미리 설정 된 컨텍스트가 제공 합니다. 따라서 불필요 tooset hello Spark 또는 Hive 컨텍스트 명시적으로 개발 하는 hello 응용 프로그램 사용을 시작 하기 전에. 이러한 컨텍스트는 기본적으로 사용할 수 있습니다. 이러한 컨텍스트는 다음과 같습니다.

* sc - Spark용 
* sqlContext - Hive용

hello PySpark 커널 제공 일부 미리 정의 된 "마법"으로 호출할 수 있는 특수 명령을 % %입니다. 이러한 코드 샘플에 사용되는 다음과 같은 두 가지 명령이 있습니다.

* **% % 로컬** hello 코드 줄에는 로컬로 실행 toobe 임을 지정 합니다. 코드는 유효한 Python 코드여야 합니다.
* **%%sql o <variable name>**  sqlContext hello에 대 한 하이브 쿼리를 실행 합니다. Hello 쿼리의 hello 결과 hello에서 유지 되 hello-o 매개 변수에 전달 되 면 % % 팬더 데이터 프레임으로 로컬 Python 컨텍스트.

Hello 커널에서 Jupyter 노트북 및 미리 정의 된 hello에 대 한 자세한 내용은 "magics"는에 대 한 제공, 참조 [HDInsight Spark Linux 커널을 Jupyter 노트북에 사용할 수 있는 HDInsight 클러스터로](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)합니다.

## <a name="data-ingestion-from-public-blob"></a>공용 blob에서 데이터 수집
hello hello 데이터 과학 프로세스의 첫 번째 단계는 원본에서 분석 tooingest hello 데이터 toobe 여기서는 데이터 탐색 및 모델링 환경에 상주 합니다. hello 환경은이 연습에서 Spark입니다. 이 섹션에는 hello 코드 toocomplete 일련의 작업이 포함 됩니다.

* hello 데이터 샘플 toobe 모델링 수집
* hello 입력된 데이터 집합 (.tsv 파일으로 저장 됨)의 읽기
* 형식 및 정리 hello 데이터
* 메모리에 개체 만들기 및 캐시(RDD 또는 데이터 프레임)
* SQL 컨텍스트에 임시 테이블로 등록

데이터 수집에 대 한 hello 코드는 다음과 같습니다.

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**출력:**

셀 위에서 tooexecute에 걸린 시간: 51.72 초

## <a name="data-exploration--visualization"></a>데이터 탐색 및 시각화
가져온 후에 hello 데이터에 Spark에, hello hello 데이터 과학 프로세스의 다음 단계는 toogain hello 데이터 탐색 및 시각화를 통해 더 깊이 이해 합니다. 이 섹션에서는 visual 검사에 대 한 SQL 쿼리 및 점도 hello 대상 변수 및 잠재 기능을 사용 하 여 hello 택시 데이터를 살펴보겠습니다. 특히, 우리 택시 trips, 팁 수량의 hello 빈도 및 어떻게 팁에 따라 다른 지불 양 및 형식은 승객 카운트 hello 주파수를 그립니다.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>히스토그램 승객 count 주파수 택시와 hello 샘플에서의 출력
이 코드와 이후의 코드 조각을 로컬 매직 tooplot hello 데이터 및 SQL 매직 tooquery hello 샘플을 사용 합니다.

* **SQL 매직 (`%%sql`)** hello HDInsight PySpark 커널 지원 sqlContext hello에 대 한 쉬운 인라인 HiveQL 쿼리 합니다. hello (-o VARIABLE_NAME) 인수 hello Jupyter 서버의 팬더 데이터 프레임으로 hello 출력 hello SQL 쿼리를 유지 합니다. 즉, hello 로컬 모드에서 사용할 수 있습니다.
* hello  **`%%local` 매직** 는 hello HDInsight 클러스터의 헤드 노드에 hello hello Jupyter 서버에서 로컬로 toorun 코드를 사용 합니다. 일반적으로 사용 `%%local` hello와 함께에서 매직 `%%sql` 매직-o 매개 변수를 사용 합니다. hello-o 매개 변수는 hello SQL 쿼리를 로컬로의 hello 출력을 유지 한 다음 % % 로컬 매직 hello 다음 코드 조각 toorun 로컬로 유지 되는 hello SQL 쿼리의 hello 출력에 대해 로컬로 집합이 트리거할지 합니다.

hello 출력은 hello 코드를 실행 한 후에 자동으로 시각화 됩니다.

이 쿼리는 hello와 승객 수에 따라 검색합니다. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

이 코드는 로컬 데이터 프레임 hello 쿼리 결과에서 만들고 hello 데이터 데이터를 표시 합니다. hello `%%local` 매직 한 로컬 데이터 프레임을 만듭니다 `sqlResults`, matplotlib를 그리기에 사용할 수 있습니다. 

> [!NOTE]
> 이 PySpark 매직은 이 연습에서 여러 번 사용됩니다. Hello 양의 데이터가 클 경우 toocreate 로컬 메모리에 들어갈 수 있는 데이터 프레임을 샘플 해야 합니다.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

여기가 hello 코드 tooplot hello trips 승객 개수

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**출력:**

![승객 수에 따른 여정 빈도](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Hello를 사용 하 여 다양 한 유형의 시각화 (테이블, 원형, 꺾은선형, 영역 또는 막대) 간에 선택할 수 있습니다 **형식** hello 전자 필기장의 메뉴 버튼. hello 모음 그림에는 다음과 같습니다.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>승객 수 및 요금 금액에 따라 팁 금액이 어떻게 달라지는지와 팁 금액에 대한 히스토그램을 그립니다.
SQL 쿼리 toosample 데이터를 사용 합니다.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


이 코드 셀 hello SQL 쿼리 toocreate 세 점도 hello 데이터를 사용합니다.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**출력:** 

![팁 금액 분포](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![승객 수에 따른 여정 수](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![금액으로 녀건 금액](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>모델링에 대한 기능 엔지니어링, 변환 및 데이터 준비
이 섹션에 설명 하 고 ML 모델링에 사용 하기 위해 사용 되는 tooprepare 데이터 hello 프로시저의 코드를 제공 합니다. Toodo hello 다음 작업 방법을 보여 줍니다.

* 시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기
* 범주 기능 인덱스 및 인코딩
* 기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기
* Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다
* 기능 크기 조정
* 메모리에서 개체 캐시

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>시간을 트래픽 시간 버킷으로 범주화하여 새로운 기능 만들기
이 코드에 어떻게 toocreate 트래픽 시간에 시간을 범주화 하 여 새로운 기능 버킷 및 toocache 메모리에 결과 데이터 프레임을 hello 하는 방법을 보여 줍니다. 복원 력 있는 분산 데이터 집합 (RDDs) 및 데이터 프레임은 사용 되는 반복 해 서, tooimproved 실행 시간 연결 캐시 됩니다. 따라서 캐시 RDDs 및 데이터 프레임 hello 연습에서 여러 단계에서 합니다. 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**출력:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>모델링 기능에 입력에 대한 범주 기능 인덱스 및 인코딩
이 섹션에서는 어떻게 tooindex 하거나 함수를 모델링 하는 hello에 대 한 입력에 대 한 범주 기능 인코딩합니다. hello 모델링 하 고 범주 입력된 데이터 toobe 기능과 인덱싱된 또는 이전 toouse 인코딩된 MLlib의 기능 필요를 예측 합니다. Hello 모델에 따라 tooindex 필요 하거나 다른 방법으로 인코딩합니다.  

* **트리 기반 모델링** 숫자 값으로 인코딩된 범주 toobe 필요 (예를 들어 세 가지 범주의 기능으로 인코딩할 수 0, 1, 2). MLlib의 [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 함수에서 제공됩니다. 이 함수는 레이블 주파수로 정렬 됩니다 레이블 인덱스의 레이블 tooa 열의 문자열 열을 인코딩합니다. 입력 및 데이터 처리에 대 한 숫자 값을 사용 하 여 인덱싱할 있지만 hello 트리 기반 알고리즘 지정된 tootreat 수 항목으로 적절 하 게 합니다. 
* **로지스틱 및 선형 회귀 모델** 하나 핫 인코딩이 필요 where, 예를 들어 세 가지 범주의 기능 구조로 확장할 수 있습니다 각 포함 된 0 또는 1 관찰의 hello 범주에 따라 세 개의 기능 열입니다. MLlib 제공 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo 인코딩 하나 핫 작동 합니다. 이 인코더도 최대 단일 한 값을 이진 벡터의 인덱스 tooa 열을 레이블 열을 매핑합니다. 로지스틱 회귀와 같은 숫자 중요 기능을 예상 하는 알고리즘을 사용 하면이 인코딩 적용 toobe toocategorical 기능입니다.

다음은 코드 tooindex hello와 범주 기능 인코딩합니다.

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

셀 위에서 tooexecute에 걸린 시간: 1.28 초

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>기계 학습 함수에 입력에 대한 레이블이 지정된 지점 개체 만들기
이 섹션에는 레이블이 지정 된 지점 데이터로 tooindex 범주 텍스트 데이터를 입력 하 고 사용 하는 테스트 및 tootrain MLlib 로지스틱 회귀 및 다른 분류 모델 될 수 있도록 인코딩할 하는 방법을 보여 주는 코드가 들어 있습니다. 레이블이 지정된 지점 개체는 대부분 MLlib의 기계 학습 알고리즘에서 입력 데이터로 필요한 방식으로 형식이 지정된 RDD(Resilient Distributed Datasets)입니다. [레이블이 지정된 지점](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 은 레이블/응답과 연결된 로컬 벡터, 밀도 또는 스파스입니다.  

이 섹션에서는 보여 주는 코드 방법을 tooindex 범주 텍스트 데이터를는 [지점 레이블이 지정 된](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 데이터 형식를 사용 하는 테스트 및 tootrain MLlib 로지스틱 회귀 및 다른 분류 모델 될 수 있도록 인코딩합니다. 레이블이 지정된 지점 개체는 레이블(대상/응답 변수) 및 기능 벡터로 구성된 RDD(Resilient Distributed Datasets)입니다. 이 서식은 MLlib의 많은 기계 학습 알고리즘에서 입력으로 필요합니다.

다음은 코드 tooindex hello와 이진 분류에 대 한 텍스트 형식 기능을 인코딩합니다.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


선형 회귀 분석을 위한 tooencode 및 인덱스 범주 텍스트 기능 hello 코드는 다음과 같습니다.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Hello 데이터의 하위 무작위 샘플링을 만들고 학습 및 테스트 집합으로 분했습니다
이 코드는 hello 데이터 (25% 여기에서 사용 됨)의 무작위 샘플링을 만듭니다. Hello 데이터 집합의 toohello 크기 때문에이 예제에 대 한 필요 하지 않더라도 대해서도 설명 방법을 샘플링할 수 있습니다 여기 알 수 있도록 어떻게 toouse 필요할 때 자신의 문제에 대 한 것입니다. 샘플이 큰 경우 모델을 학습하는 동안 상당한 시간을 절약할 수 있습니다. 다음 hello 샘플 학습 부분 (75% 여기) 및 분류 및 회귀 모델링에 테스트 부분 (25% 여기) toouse로 분할 합니다.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

셀 위에서 tooexecute에 걸린 시간: 0.24 초

### <a name="feature-scaling"></a>기능 크기 조정
데이터 정규화 라고도 기능 크기 조정 시나리오는 광범위 하 게 분산된 값이 포함 된 기능은 과도 하 게 지정 된 하지 입니까 hello 목표 함수. hello 코드 크기를 조정 하는 기능 사용 하 여 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 기능 toounit 분산 합니다. 정칙 회귀 또는 SVM(support vector machine)과 같은 광범위한 다른 기계 학습 모델을 학습하기 위한 인기 있는 알고리즘인 SGD(Stochastic Gradient Descent)와 함께 선형 회귀에 사용하기 위해 MLlib에서 제공합니다.

> [!NOTE]
> Hello LinearRegressionWithSGD 알고리즘 toobe 중요 한 toofeature 배율 발견 했습니다.
> 
> 

정규화 된 hello 선형 SGD 알고리즘과 함께 사용 하기 위해 hello 코드 tooscale 변수는 다음과 같습니다.

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

셀 위에서 tooexecute에 걸린 시간: 13.17 초

### <a name="cache-objects-in-memory"></a>메모리에서 개체 캐시
hello 시간 분류와 회귀를 사용 하는 hello 입력된 데이터 프레임 개체를 캐시 하 여 학습 및 테스트 기계 학습 알고리즘 중을 줄일 수 있습니다에 대해 수행 되 고 기능을 확장 합니다.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:** 

셀 위에서 tooexecute에 걸린 시간: 0.15 초

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>팁이 지불되었는지 여부를 이진 분류 모델로 예측합니다.
이 섹션에서는 택시 여행에 대 한 팁을 지불 여부 3 개 사용 하 여 예측의 hello 이진 분류 작업에 대 한 모델링 방법을 보여 줍니다. 제공 된 hello 모델은 같습니다.

* 정칙 로지스틱 회귀 
* 임의 포리스트 모델
* 그라데이션 향상 트리

코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다. 

1. **모델 교육** 데이터
2. **모델 평가** 
3. **모델 저장** 

### <a name="classification-using-logistic-regression"></a>로지스틱 회귀를 사용하는 분류
이 섹션의 hello 코드 tootrain를 평가 하 고 사용 하 여 로지스틱 회귀 모델을 저장 하는 방법을 보여 줍니다. [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부 예측 합니다.

**CV 및 hyperparameter 비우기 사용 하 여 hello 로지스틱 회귀 모델 학습**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**출력:** 

Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercept: -0.0111216486893

셀 위에서 tooexecute에 걸린 시간: 14.43 초

**표준 메트릭 사용 하 여 hello 이진 분류 모델 평가**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**출력:** 

Area under PR = 0.985297691373

Area under ROC = 0.983714670256

Summary Stats

Precision = 0.984304060189

Recall = 0.984304060189

F1 Score = 0.984304060189

셀 위에서 tooexecute에 걸린 시간: 57.61 초

**Hello ROC 곡선을 그립니다.**

hello *predictionAndLabelsDF* 테이블로 등록 *tmp_results*, hello 이전 셀에 있습니다. *tmp_results* toodo 사용 되는 쿼리 수 있고 hello sqlResults 데이터-프레임으로 그래프에 표시 하는 것에 대 한 결과 출력 합니다. Hello 코드는 다음과 같습니다.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


다음은 hello 코드 toomake 예측 및 플롯 hello ROC 곡선입니다.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**출력:**

![로지스틱 회귀 ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>임의 포리스트 분류
이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 임의 포리스트 모델을 저장 하는 방법을 보여 줍니다.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

Area under ROC = 0.985297691373

셀 위에서 tooexecute에 걸린 시간: 31.09 초

### <a name="gradient-boosting-trees-classification"></a>그라데이션 향상 트리 분류
이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 및 요금 데이터 집합에는 여행에 대 한 팁을 지불 여부를 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**출력:**

Area under ROC = 0.985297691373

셀 위에서 tooexecute에 걸린 시간: 19.76 초

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>회귀 모델로 Taxi Trip에 대한 팁 금액을 예측합니다.
이 섹션에서는 다른 팁 기능을 기반으로 택시 여정에 대해 지불한 hello 팁 hello 양을 예측 hello 회귀 작업에 대 한 3 개 사용 하 여 모델링 하는 방법을 보여 줍니다. 제공 된 hello 모델은 같습니다.

* 정칙 선형 회귀
* 임의 포리스트
* 그라데이션 향상 트리

이러한 모델은 hello 소개에 설명 했습니다. 코드 섹션을 빌드하는 각 모델은 다음과 같은 단계로 분할됩니다. 

1. **모델 교육** 데이터
2. **모델 평가** 
3. **모델 저장** 

### <a name="linear-regression-with-sgd"></a>SGD로 선형 회귀
hello이 섹션의 코드를 보여 줍니다 toouse 확장 되는 방식 기능 tootrain 추측 기울기 하강 (SGD) 최적화를 위해 사용 하는 선형 회귀 방법을 tooscore, 평가 및 Azure Blob 저장소 (WASB) hello 모델을 저장 하 고 있습니다.

> [!TIP]
> 경험에 따르면 LinearRegressionWithSGD 모델의 hello 수렴 문제가 있을 수 있으며 매개 변수 변경 된/최적화 된 신중 하 게 유효한 모델을 얻기 위한 toobe 필요 합니다. 변수의 크기를 조정하면 수렴에 큰 도움이 됩니다. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

Intercept: 0.853872718283

RMSE = 1.24190115863

R-sqr = 0.608017146081

셀 위에서 tooexecute에 걸린 시간: 58.42 초

### <a name="random-forest-regression"></a>임의 포리스트 회귀
이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 임의 포리스트 회귀를 저장 하는 방법을 보여 줍니다.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

RMSE = 0.891209218139

R-sqr = 0.759661334921

셀 위에서 tooexecute에 걸린 시간: 49.21 초

### <a name="gradient-boosting-trees-regression"></a>그라데이션 향상 트리 회귀
이 섹션의 hello 코드 tootrain를 평가 하 고 hello NYC 택시 여행 데이터에 대 한 팁 금액을 예측 하는 그라데이션 승격 트리 모델을 저장 하는 방법을 보여 줍니다.

**학습 및 평가**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**출력:**

RMSE = 0.908473148639

R-sqr = 0.753835096681

셀 위에서 tooexecute에 걸린 시간: 34.52 초

**그림**

*tmp_results* hello 이전 셀의 Hive 테이블으로 등록 됩니다. Hello 테이블의 결과가 hello에 출력 되는 *sqlResults* 그리기에 대 한 데이터 프레임입니다. 다음은 hello 코드

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Hello Jupyter 서버를 사용 하 여 hello 코드 tooplot hello 데이터는 다음과 같습니다.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**출력:**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>메모리에서 개체 정리
사용 하 여 `unpersist()` toodelete 개체 메모리에 캐시 합니다.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>소비와 점수 매기기에 대 한 hello 모델의 저장소 위치 레코드
독립적인 데이터 집합을 사용 하 여 hello에 설명 된 점수와 tooconsume [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md) toocopy 및 이러한 파일 이름을 hello에 여기에 생성 된 포함 된 저장 hello 모델 붙여넣기 필요한 항목 Jupyter 노트북을 사용 합니다. Hello 코드 tooprint 발생 해야 하는 hello 경로 toomodel 파일은 다음과 같습니다.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**출력**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>다음 작업
준비 toolearn 어떻게는 Spark MlLib hello로 분류 및 회귀 모델을 만든 tooscore 하 고 이러한 모델을 평가 합니다. 고급 데이터 탐색 및 교차 유효성 검사, 하이퍼 매개 변수를 포함 하 여으로 깊은 노트북 다이브 모델링 hello 스윕, 및 평가 모델링 합니다. 

**소비 모델:** toolearn 어떻게 tooscore이이 항목에서 만든 hello 분류 및 회귀 모델을 평가 하 고, 참조 및 [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md)합니다.

**교차 유효성 검사 및 하이퍼 매개 변수 비우기**: 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark로 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) 을 참조하세요.

