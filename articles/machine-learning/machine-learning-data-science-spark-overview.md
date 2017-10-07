---
title: "Azure HDInsight의 Spark를 사용 하 여 데이터 과학자의 aaaOverview | Microsoft Docs"
description: "hello Spark MLlib 도구 키트는 상당한 기계 학습 기능 distributed toohello HDInsight 환경 모델링을 제공 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Azure HDInsight에서 Spark를 사용하는 데이터 과학 개요
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

이 도구 모음 항목의 데이터를 수집, 기능 엔지니어링, 모델링 및 모델 평가 경우 같은 toouse HDInsight Spark toocomplete 일반 데이터 과학 작업 하는 방법을 보여 줍니다. 사용 되는 hello 데이터는 hello 2013 NYC 택시 여행 및 요금 데이터 집합의 샘플입니다. 작성 된 hello 모델에 물류 및 선형 회귀, 임의 포리스트 및 그라데이션 승격 된 트리에 포함 됩니다. hello 항목도 표시 방법을 toostore 이러한 모델에서 Azure blob 저장소 (WASB)와 방법을 tooscore 하 고 예측의 성능을 평가 합니다. 고급 항목에서는 교차 유효성 검사 및 하이퍼 매개 변수 스위핑을 사용하여 모델을 학습할 수 있는 방법을 다룹니다. 또한이 개요 항목 tooset를 제공 하는 hello 연습에서 toocomplete hello 단계를 보려면 Spark 클러스터 hello 하는 방법을 설명 하는 hello 항목을 참조 합니다. 

## <a name="spark-and-mllib"></a>Spark 및 MLlib
[Spark](http://spark.apache.org/) 빅 데이터 분석 응용 프로그램의 tooboost hello 성능을 처리에서 메모리를 지 원하는 오픈 소스 병렬 처리 프레임 워크입니다. hello Spark 처리 엔진에 대 한 속도, 사용 및 복잡 한 분석의 용이성 만들어집니다. 메모리 내 분산된 계산 기능으로 Spark의 게 hello 반복 알고리즘 컴퓨터 학습 및 그래프 계산에 사용 하기에 적합 합니다. [MLlib](http://spark.apache.org/mllib/) 기능 toothis 분산된 환경 모델링 Spark의 확장 가능한 시스템 학습 라이브러리 hello 알고리즘을 제공 하는 것입니다. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure 호스팅되는 오픈 소스 Spark의 제공 합니다. 에 대 한 지원도 포함 됩니다 **Jupyter PySpark 노트북** Spark SQL 변환, 필터링 및 Azure Blob (WASB)에 저장 된 데이터를 시각화에 대 한 대화형 쿼리를 실행할 수 있는 hello Spark 클러스터에 있습니다. PySpark는 hello Spark에 대 한 Python API입니다. hello 솔루션을 제공 하 고 여기 Jupyter 노트북 hello Spark 클러스터에 설치에서 실행 하는 hello 관련 점도 toovisualize hello 데이터를 보여 주는 hello 코드 조각입니다. 이 항목의 hello 모델링 단계 tootrain를 평가, 저장 및 각 모델 유형에 사용 방법을 보여 주는 코드가 포함 됩니다. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>설정: Spark 클러스터 및 Jupyter Notebook
설치 단계와 코드는 HDInsight Spark 1.6을 사용하는 이 연습에 제공됩니다. 하지만 Jupyter Notebook은 HDInsight Spark 1.6과 Spark 2.0 클러스터 둘 다에 제공됩니다. Hello에 전자 필기장 및 링크 toothem hello에 대 한 설명을 제공 됩니다 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 이 포함 하는 hello GitHub 리포지토리에 대 한 합니다. 또한 hello 코드와 연결 된 hello 전자 필기장에서 제네릭 인데 어떤 Spark 클러스터에서 작동 해야 합니다. HDInsight Spark를 사용 하지 않는 경우 hello 클러스터 설치 및 관리 단계는 여기 표시 된에서 약간 다를 수 있습니다. 편의 위해 링크는 다음과 같습니다 hello Spark 1.6 (toobe hello pySpark 커널의 hello Jupyter 노트북 서버에서 실행) 및 Spark 2.0 (toobe hello pySpark3 커널의 hello Jupyter 노트북 서버에서 실행)에 대 한 toohello Jupyter 노트북:

### <a name="spark-16-notebooks"></a>Spark 1.6 Notebook
이러한 전자 필기장 toobe hello pySpark 커널의 Jupyter 노트북 서버에서 실행 됩니다.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): 방법에 대해 설명 tooperform 데이터 탐색, 모델링 및 다양 한 알고리즘이 점수 매기기입니다.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): 노트북 #1의 토픽과 하이퍼 매개 변수 조정 및 교차 유효성 검사를 사용하는 모델 개발을 포함합니다.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): 방법을 toooperationalize HDInsight에서 Python을 사용 하 여 저장 된 모델 클러스터를 보여 줍니다.

### <a name="spark-20-notebooks"></a>Spark 2.0 Notebook
이러한 전자 필기장 toobe hello pySpark3 커널의 Jupyter 노트북 서버에서 실행 됩니다.

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

Spark 2.0 모델 및 점수 매기기에 대 한 모델 소비 화 hello에 대 한 지침을 참조 hello [Spark 1.6 문서 사용에 대 한](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) 필요한 hello 단계 개요 예에 대 한 합니다. hello Python 코드 파일을 Spark 2.0에 대 한 대체 toouse [이 파일](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py)합니다.

### <a name="prerequisites"></a>필수 조건
다음 절차를 수행 하는 hello 관련된 tooSpark 1.6 됩니다. 사용 하 여 hello 전자 필기장 hello Spark 2.0 버전에 대 한 설명 하 고 toopreviously 연결 합니다. 

1. Azure 구독이 있어야 합니다. 아직 가지고 있지 않은 경우 [Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

2.가 연습이에서는 1.6 Spark 클러스터 toocomplete 할 수 있습니다. toocreate 하나, 참조에 제공 된 hello 지침 [시작: Azure HDInsight의 Apache Spark 만들기](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)합니다. hello 클러스터 유형 및 버전 hello에서 지정 된 **클러스터 유형 선택** 메뉴. 

![클러스터 구성](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Toouse Python 보다는 Scala toocomplete 종단 간 데이터 과학 프로세스에 대 한 작업 하는 방법을 보여 주는 항목에 대 한 참조 hello [Scala Azure의 Spark와 함께 사용 하 여 데이터 과학](machine-learning-data-science-process-scala-walkthrough.md)합니다.
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>hello NYC 2013 택시 데이터
hello NYC 택시 여행 데이터는 약 20GB의 압축 된 쉼표로 구분 된 값 (CSV) 파일 (~ 48 GB 압축 되지 않음), 구성 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다. 각 여행 레코드 hello 선택 및 자동 전송 위치 및 시간, 익명화 된 해킹 (드라이버의) 라이선스 번호 및 메달 (택시의 고유 id) 번호를 포함합니다. hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.

1. hello 'trip_data' CSV 파일 승객 수와 같이 여행 세부 정보를 포함 하려면를 선택 하 고 기간과 여행 길이 여행 dropoff 가리킵니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. hello 'trip_fare' CSV 파일 hello 요금을 지불 유형, 요금 크기, 추가 요금 및 세금, 팁 및 통행료가, 및 유료 hello 총 금액 등 각 여정에 대해 지불한의 세부 정보를 포함 합니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

이러한 파일 및 조인 된 hello 여행의 0.1% 샘플 이동\_데이터와 여행\_hello이이 연습에 대 한 입력된 데이터 집합으로 CVS 파일에 단일 데이터 집합 toouse 있어 합니다. hello 고유 키 toojoin 여행\_데이터와 여행\_요금 가지 hello 필드로 구성 됩니다: 메달 해킹\_사용권 및 픽업\_날짜/시간입니다. Hello 데이터 집합의 각 레코드는 hello를 NYC 택시 출장을 나타내는 특성에 따라 포함 되어 있습니다.

| 필드 | 간략한 설명 |
| --- | --- |
| medallion |익명 처리된 택시 medallion(고유 택시 id) |
| hack_license |익명 처리된 Hackney 운전 면허 번호 |
| vendor_id |택시 공급 업체 id |
| rate_code |NYC 택시 요율 |
| store_and_fwd_flag |저장소 및 전달 플래그 |
| pickup_datetime |승차 날짜 및 시간 |
| dropoff_datetime |내린 날짜 및 시간 |
| pickup_hour |승차 시간 |
| pickup_week |Hello 연도의 주를 선택 합니다. |
| weekday |요일(범위 1-7) |
| passenger_count |택시 여정의 승객 수 |
| trip_time_in_secs |여정 시간(초) |
| trip_distance |주행한 여정 거리(마일 단위) |
| pickup_longitude |승차 경도 |
| pickup_latitude |승차 위도 |
| dropoff_longitude |내린 경도 |
| dropoff_latitude |내린 위도 |
| direct_distance |승차 및 하차 위치 사이의 직접 거리 |
| payment_type |지불 유형(cas, 신용 카드 등) |
| fare_amount |요금 금액 |
| surcharge |추가 요금 |
| mta_tax |Mta 세금 |
| tip_amount |팁 금액 |
| tolls_amount |통행료 금액 |
| total_amount |총 금액 |
| tipped |팁 지불 여부(아니요 또는 예에 대해 0/1 지정) |
| tip_class |팁 클래스(0: $0, 1: $0-5, 2: $6-10, 3: $11-20, 4: > $20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Hello Spark 클러스터에서 Jupyter 노트북에서 코드를 실행 합니다.
Hello Jupyter 노트북 hello Azure 포털에서에서 시작할 수 있습니다. 대시보드에 Spark 클러스터를 찾아 클러스터에 대해 tooenter 관리 페이지를 클릭 합니다. hello Spark 클러스터와 연결 된 tooopen hello 노트북 클릭 **클러스터 대시보드** -> **Jupyter 노트북** 합니다.

![클러스터 대시보드](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

너무 찾아볼 수도 있습니다***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello Jupyter 노트북 합니다. 이 URL의 hello CLUSTERNAME 부분을 사용자 고유의 클러스터의 hello 이름을 바꿉니다. 관리자 계정 tooaccess hello 전자 필기장에 대 한 hello 암호가 필요 합니다.

![Jupyter 노트북 찾아보기](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

PySpark toosee Spark 항목의이 도구 모음에 대 한 hello 코드 샘플이 포함 된 PySpark API.hello 전자 필기장에서 사용할 수 있는 hello를 사용 하는 패키지 전자 필기장의 몇 가지 예제가 포함 된 디렉터리를 선택 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Hello 전자 필기장에서 직접 업로드할 수 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) Spark 클러스터에서 toohello Jupyter 노트북 서버입니다. 프로그램 Jupyter hello 홈 페이지에서 클릭 hello **업로드** hello hello 화면의 오른쪽 부분에 단추입니다. 파일 탐색기가 열립니다. Hello 노트북 한 hello GitHub (원시 콘텐츠) URL을 붙여넣을 수 여기 **열려**합니다. 

Hello 파일 이름으로 Jupyter 파일 목록에 표시 된 **업로드** 단추를 다시 합니다. 이 **업로드** 버튼을 클릭합니다. 이제 hello 노트북을 가져왔습니다. 이 연습에서 다른 전자 필기장 이러한 단계 tooupload hello를 반복 합니다.

> [!TIP]
> 브라우저 및 선택 사항에 대 한 hello 링크를 마우스 오른쪽 단추로 클릭 수 **링크 복사** tooget hello github의 원시 콘텐츠 URL입니다. Hello Jupyter 업로드 파일 탐색기 대화 상자에이 URL을 붙여넣을 수 있습니다.
> 
> 

이제 다음을 수행할 수 있습니다.

* Hello 노트북을 클릭 하 여 hello 코드를 참조 하십시오.
* **Shift+Enter**를 눌러 각 셀을 실행합니다.
* 클릭 하 여 hello 전체 전자 필기장 실행 **셀** -> **실행**합니다.
* 쿼리의 자동 시각화 hello를 사용 합니다.

> [!TIP]
> hello PySpark 커널 hello 출력 (HiveQL) SQL 쿼리를 자동으로 시각화합니다. Hello를 사용 하 여 다양 한 유형의 시각화 (테이블, 원형, 꺾은선형, 영역 또는 막대) 간에 hello 옵션 tooselect 증명이 **형식** hello 전자 필기장의 메뉴 단추:
> 
> 

![일반적인 접근 방식에 대한 로지스틱 회귀 분석 ROC 곡선](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>다음 작업
HDInsight Spark 클러스터를 사용 하 여 설정 되 고 hello Jupyter 노트북 업로드 했으므로 toohello 세 PySpark 전자 필기장에 해당 하는 hello 항목을 통해 준비 toowork 됩니다. 보여 줍니다 어떻게 tooexplore 데이터와 다음 방법을 toocreate 및 모델을 사용 합니다. 고급 데이터 탐색 및 노트북 표시 방법을 모델링 하는 hello tooinclude 교차 유효성 검사, 하이퍼 매개 변수 비우기 및 모델 평가 합니다. 

**데이터 탐색 및 모델링 spark:** hello 데이터 집합을 탐색 하 고, 점수를 만들고 hello 통해 작업 하 여 hello 기계 학습 모델을 평가 [hello Spark 데이터에 대 한 이진 분류 및 회귀 모델 만들기 MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) 항목입니다.

**소비 모델:** toolearn tooscore hello 분류 및 회귀 모델은이 항목에서 생성 하는 방법 참조 [점수 Spark 작성 기계 학습 모델을 평가 하 고](machine-learning-data-science-spark-model-consumption.md)합니다.

**교차 유효성 검사 및 하이퍼 매개 변수 비우기**: 교차 유효성 검사 및 하이퍼 매개 변수 비우기를 사용하여 모델을 학습하는 방법은 [Spark로 고급 데이터 탐색 및 모델링](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) 을 참조하세요.

