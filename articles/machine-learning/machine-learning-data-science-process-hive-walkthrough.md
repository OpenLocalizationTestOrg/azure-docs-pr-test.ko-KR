---
title: "aaaExplore 데이터에는 Hadoop 클러스터 및 Azure 기계 학습에서 모델을 만들 | Microsoft Docs"
description: "HDInsight Hadoop을 사용 하는 종단 간 시나리오에 대 한 hello 팀 데이터 과학 프로세스를 사용 하 여 toobuild 클러스터 되 고 공개적으로 사용할 수 있는 데이터 집합을 사용 하 여 모델을 배포 합니다."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>작업에 팀 데이터 과학 프로세스 hello: 사용 하 여 Azure HDInsight Hadoop 클러스터
이 연습을 사용 하 여 hello [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md) 사용 하 여 종단 간 시나리오에는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/) toostore, 탐색 하 고 공개적으로 hello에서 엔지니어 데이터 기능 사용 가능한 [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 집합과 toodown hello 데이터 샘플입니다. Azure 기계 학습 toohandle 이진 및 다중 클래스 분류와 회귀를 예측 작업 hello 데이터의 모델 작성 됩니다.

어떻게 toohandle (1tb) dataset HDInsight Hadoop을 사용 하 여 비슷한 시나리오에 대 한 클러스터를 데이터 처리를 보여 주는 연습을 참조 하십시오. [팀 데이터 과학 프로세스 1TB dataset에서AzureHDInsightHadoop클러스터를사용하여](machine-learning-data-science-process-hive-criteo-walkthrough.md).

이기도 가능한 toouse IPython 노트북 tooaccomplish hello 발표 된 hello 연습 hello 1TB 데이터 집합을 사용 하 여 작업 합니다. 사용자에 게는이 방법을 문의 해야 tootry 같은 hello [하이브 ODBC 연결을 사용 하 여 Criteo 연습](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 항목입니다.

## <a name="dataset"></a>NYC Taxi Trips 데이터 집합 설명
hello NYC 택시 여행 데이터는 약 20GB의 압축 된 쉼표로 구분 된 값 (CSV) 파일 (~ 48 GB 압축 되지 않음), 구성 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다. 각 여행 레코드 hello 픽업 및 자동 전송 위치 및 시간, 익명화 된 해킹 (드라이버의) 라이선스 번호 및 메달 (택시의 고유 id) 번호를 포함합니다. hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.

1. hello 'trip_data' CSV 파일 승객, 픽업 및 dropoff 포인트, 여행 기간 및 여행 길이 수와 같이 여행 세부 정보를 포함합니다. 다음은 몇 가지 샘플 레코드입니다.
   
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

hello 고유 키 toojoin 여행\_데이터와 여행\_요금 가지 hello 필드로 구성 됩니다: 메달 해킹\_사용권 및 픽업\_날짜/시간입니다.

모든 tooget 되었기 세 개의 키가 있는 충분 한 toojoin hello 세부 정보 관련 tooa 특정 시간이: "메달" hello "해킹\_라이선스" 및 "픽업\_날짜/시간"입니다.

저장을 Hive 테이블에 곧 때 hello 데이터의 좀 더 자세히 설명 합니다.

## <a name="mltasks"></a>예측 작업의 예제
데이터에 근접 하 고, 예측 분석에 따라 toomake 원하는 hello 종류를 결정 하는 데 도움이 됩니다 명확히 hello 작업 프로세스에서 tooinclude가 필요 합니다.
다음은이 연습에서는 해당 구문이 hello 기반 그렇다면 해결 하는 예측 문제의 세 가지 예제 *팁\_양*:

1. **이진 분류**: 여정에 대해 팁이 지불되었는지 여부를 예측합니다. 즉, *tip\_amount*가 $0보다 크면 지불된 것이고 *tip\_amount*가 $0이면 지불되지 않은 것입니다.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **다중 클래스 분류**: hello 여행에 대 한 팁 수량의 toopredict hello 범위 지불 합니다. Hello 나눕니다 *팁\_양* 다섯 개의 bin 또는 클래스에:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **회귀 작업**: toopredict hello 양을 hello 팁은 여행에 대 한 지불 합니다.  

## <a name="setup"></a>고급 분석용 HDInsight Hadoop 클러스터 설정
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

다음 세 단계를 통해 HDInsight 클러스터를 사용하는 고급 분석용 Azure 환경을 설정할 수 있습니다.

1. [저장소 계정 만들기](../storage/common/storage-create-storage-account.md):이 저장소 계정은 Azure Blob 저장소에 데이터를 저장하는 데 사용됩니다. HDInsight 클러스터에서 사용 하는 hello 데이터 여기에 저장 됩니다.
2. [Azure HDInsight Hadoop 사용자 지정 고급 분석 프로세스 및 기술 hello에 대 한 클러스터](machine-learning-data-science-customize-hadoop-cluster.md)합니다. 이 단계에서는 모든 노드에 64비트 Anaconda Python 2.7이 설치된 Azure HDInsight Hadoop 클러스터를 만듭니다. HDInsight 클러스터를 사용자 지정 하는 동안 중요 한 단계 tooremember 두 가지가 있습니다.
   
   * Toolink hello 저장소 계정을 만들 때 HDInsight 클러스터와 1 단계에서 만든 기억 합니다. 이 저장소 계정은 hello 클러스터 내에서 처리 되는 사용 되는 tooaccess 데이터입니다.
   * Hello 클러스터를 만든 후 원격 액세스 toohello hello 클러스터의 헤드 노드를 사용 하도록 설정 합니다. Toohello 이동 **구성** 탭을 클릭 **원격 사용**합니다. 이 단계는 원격 로그인에 사용 되는 hello 사용자 자격 증명을 지정 합니다.
3. [Azure 기계 학습 작업 영역을 만들](machine-learning-create-workspace.md):이 Azure 기계 학습 작업 영역을 사용 하는 toobuild 기계 학습 모델입니다. 이 태스크는 초기 데이터 탐색을 완료 한 후] 및 [아래로 hello HDInsight 클러스터를 사용 하 여 샘플링 처리 됩니다.

## <a name="getdata"></a>공개 소스에서 hello 데이터 가져오기
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

tooget hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 공용 위치에서 데이터 집합을 사용할 수 있습니다에 설명 된 hello 메서드의 [Azure Blob 저장소에서 데이터 이동 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 데이터 tooyour 컴퓨터입니다.

여기 AzCopy tootransfer hello를 사용 하 여 데이터가 포함 된 파일을 방법 설명 하십시오. toodownload 및 설치 AzCopy hello 지침에 따라 [hello AzCopy 명령줄 유틸리티 시작](../storage/common/storage-use-azcopy.md)합니다.

1. 명령 프롬프트 창에서 발급 hello는 AzCopy 명령 뒤, 대체 *< path_to_data_folder >* hello 원하는 대상으로 합니다.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Hello 복사가 완료 되 면 선택 hello data 폴더에는 총 24 압축 된 파일 됩니다. 다운로드 한 hello 파일 toohello의 압축을 푸는 로컬 컴퓨터에서 동일한 디렉터리입니다. Hello 압축 되지 않은 파일이 있는 hello 폴더를 기록해 둡니다. 이 폴더에는 참조 된 tooas hello 됩니다 *< 경로\_를\_unzipped_data\_파일\>*  뒤에 나오는 설명이 됩니다.

## <a name="upload"></a>Azure HDInsight Hadoop 클러스터의 hello toohello 기본 컨테이너를 데이터 업로드
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

Hello 다음 AzCopy 명령 hello Hadoop 클러스터를 만들 때 지정한 hello 실제 값으로 매개 변수를 따르고 hello 데이터 파일 압축을 푼 hello를 대체 합니다.

* ***&#60; path_to_data_folder >*** hello 디렉터리 경로) (함께 hello에 압축을 데이터 파일을 포함 하는 컴퓨터에  
* ***&#60; Hadoop 클러스터의 저장소 계정 이름 >*** hello HDInsight 클러스터와 연결 된 저장소 계정
* ***&#60; Hadoop 클러스터의 기본 컨테이너 >*** 클러스터에서 사용 하는 hello 기본 컨테이너입니다. 해당 hello 이름을 적어 둡니다 hello 기본의 컨테이너는 일반적으로 hello hello 클러스터 자체와 동일한 이름을 지정 합니다. 예를 들어 hello 클러스터 "abc123.azurehdinsight.net"를 호출 하는 경우 hello 기본 컨테이너는 abc123입니다.
* ***&#60; 저장소 계정 키 >*** 클러스터에서 사용 하는 hello 저장소 계정에 대 한 hello 키

명령 프롬프트 또는 컴퓨터에서 Windows PowerShell 창에서 다음 두 가지는 AzCopy 명령 hello를 실행 합니다.

이 명령은 hello 여행 데이터를 너무 업로드***nyctaxitripraw*** hello Hadoop 클러스터의 hello 기본 컨테이너에 있는 디렉터리입니다.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

이 명령은 hello 요금 데이터를 너무 업로드***nyctaxifareraw*** hello Hadoop 클러스터의 hello 기본 컨테이너에 있는 디렉터리입니다.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

hello 데이터 Azure Blob 저장소 및 hello HDInsight 클러스터 내에 사용 되는 준비 toobe 이제 해야 합니다.

## <a name="#download-hql-files"></a>Hadoop 클러스터의 헤드 노드 hello에 로그인 하 고 예비 데이터 분석을 위해 준비 하 고
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

에 설명 된 hello 절차를 수행 하는 hello tooaccess 예비 데이터 분석을 위해이 고 hello 데이터 샘플링 아래로 hello 클러스터의 헤드 노드에 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.

이 연습에서는 주로 사용 하 여 작성 된 쿼리 [하이브](https://hive.apache.org/), SQL 방식 쿼리 언어, tooperform 임시 데이터 탐색 합니다. hello 하이브 쿼리.hql 파일에 저장 됩니다. 에서는 다음 아래로 샘플 모델을 작성 하기 위한 Azure 기계 학습에서 사용 되는이 데이터 toobe 합니다.

hello 관련 하이브 스크립트를 포함 하는 hello.hql 파일 다운로드 예비 데이터 분석을 위해 tooprepare hello 클러스터 [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) hello 헤드 노드에서 tooa 로컬 디렉터리 (: C:\temp). toodo이, 열기 hello **명령 프롬프트** 내에서 다음 두 명령을 hello 클러스터와 문제 hello의 헤드 노드를 hello:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

이 두 명령은이 연습에서는 toohello 로컬 디렉터리에 필요한 모든.hql 파일을 다운로드 합니다 ***C:\temp &#92;*** hello 헤드 노드에 있습니다.

## <a name="#hive-db-tables"></a>월별로 분할된 Hive 데이터베이스 및 테이블 만들기
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

이제 준비 toocreate 하이브 테이블 우리의 NYC 택시 데이터 집합에 대 한 합니다.
Hello hello Hadoop 클러스터의 헤드 노드를 열고 hello ***Hadoop 명령줄*** hello 헤드 노드의 데스크톱 hello 되 고 hello 명령을 입력 하 여 hello 하이브 디렉터리를 입력 합니다.

    cd %hive_home%\bin

> [!NOTE]
> **하이브 bin 위에 hello에서이 연습에서 모든 하이브 명령을 실행 / directory 프롬프트입니다. 경로 문제가 자동으로 해결됩니다. Hello 용어 "하이브 디렉터리 프롬프트"를 사용 하 여 "하이브 bin / directory 프롬프트", 및 Hadoop에서에서 명령줄 "" 구분 없이이 연습 합니다.**
> 
> 

Hello 하이브 디렉터리 프롬프트에서 다음 명령을 명령 줄에서 Hadoop hello 헤드 노드 toosubmit hello 하이브 쿼리 toocreate 하이브 데이터베이스 및 테이블의 hello를 입력 합니다.

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Hello 내용의 hello 같습니다 ***C:\temp\sample\_하이브\_만들\_db\_및\_tables.hql*** 하이브 데이터베이스를 만드는 파일 ***nyctaxidb *** 및 테이블 ***여행*** 및 ***요금***합니다.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

이 Hive 스크립트는 두 개의 테이블을 만듭니다.

* hello "여행" 테이블의 각 안에서 (드라이버 정보, 픽업 시간, 여행 거리 및 시간이) 여행 세부 정보를 포함합니다.
* hello "요금" 테이블 (요금 금액, 팁, 통행료가 양과 surcharges) 요금 세부 정보를 포함합니다.

이러한 절차는 추가 도움이 필요한 tooinvestigate 대체 구성을 원하는 경우 hello 섹션을 참조 하세요. [제출 Hive 쿼리 직접에서 hello Hadoop 명령줄 ](machine-learning-data-science-move-hive-tables.md#submit)합니다.

## <a name="#load-data"></a>파티션에서 데이터 tooHive 테이블 로드
> [!NOTE]
> 이는 일반적으로 **관리자** 작업입니다.
> 
> 

hello NYC 택시 dataset tooenable 처리 및 쿼리를 보다 빠르게 사용 하 여 월별로 자연 분할에 있습니다. 아래의 PowerShell 명령 hello (hello를 사용 하 여 hello 하이브 디렉터리에서 발급 한 **Hadoop 명령줄**) 데이터 toohello "여행" 및 "요금" 하이브 테이블 분할을 로드 합니다.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

hello *샘플\_하이브\_로드\_데이터\_여\_partitions.hql* hello 다음을 포함 하는 파일 **로드** 명령입니다.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

여기에서 hello 탐색 프로세스에서 사용 하는 하이브 쿼리 수가 단일 파티션으로 또는 파티션의 두에서 보고와 관련 참고 합니다. 하지만 hello 전체 데이터에서 이러한 쿼리를 실행할 수 있습니다.

### <a name="#show-db"></a>데이터베이스 hello HDInsight Hadoop 클러스터에 표시
HDInsight Hadoop 클러스터 hello 다음 명령을 Hadoop 명령 줄에서 실행 되는 hello Hadoop 명령줄 창 내에서 생성 된 tooshow hello 데이터베이스:

    hive -e "show databases;"

### <a name="#show-tables"></a>Hello nyctaxidb 데이터베이스에 있는 hello 하이브 테이블을 보려면
hello nyctaxidb 데이터베이스에서 다음 명령을 Hadoop Command Line hello 실행 tooshow hello 테이블:

    hive -e "show tables in nyctaxidb;"

Hello 테이블 아래 hello 명령을 실행 하 여 분할 됩니다 확인할 수 있습니다.

    hive -e "show partitions nyctaxidb.trip;"

hello 예상 출력은 다음과 같습니다.

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

마찬가지로, 아래 hello 명령을 실행 하 여 해당 hello 요금 테이블이 분할 된 보장이:

    hive -e "show partitions nyctaxidb.fare;"

hello 예상 출력은 다음과 같습니다.

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Hive에서 데이터 탐색 및 기능 엔지니어링
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

데이터 탐색 hello 및 기능 엔지니어링 작업에 대 한 hello hello Hive 테이블에 로드 된 데이터는 하이브 쿼리를 사용 하 여 수행할 수 있습니다. 다음은 이 섹션에서 설명할 이러한 작업의 예입니다.

* 두 테이블의 hello 상위 10 개의 레코드를 봅니다.
* 다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.
* Hello 경도 및 위도 필드의 데이터 품질을 조사 합니다.
* 이진 및 다중 클래스 분류 레이블을 hello에 따라 생성 **팁\_양**합니다.
* Hello 직접 여행 거리를 계산 하 여 기능을 생성 합니다.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>탐색: hello 상위 10 개의 레코드를 테이블 정의 보기
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

hello 데이터 모양을 toosee, 각 테이블에서 10 개의 레코드를 살펴보겠습니다. Hello 두 개의 쿼리를 별도로 hello Hadoop 명령줄 콘솔 tooinspect hello 레코드의 hello 하이브 디렉터리 프롬프트에서 다음을 실행 합니다.

tooget hello 상위 10 개의 테이블의 레코드 hello "여행" hello 첫 번째 월에서:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello 상위 10 개의 테이블의 레코드 hello "요금" hello 첫 번째 월에서:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

것이 편리 하 게 보기에 대 한 유용한 toosave hello 레코드 tooa 파일입니다. 쿼리 위에 작은 변경 toohello이를 수행합니다.

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>각 파티션을 12 hello 레코드 수가 보기 hello 탐색:
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

관심 있는 hello 역 년 동안와의 hello 횟수 변화 하는 hello입니다. Toosee 월별로 그룹화를 통해이 배포와 같습니다.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

이 목록에 hello 출력:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Hello 첫 번째 열은 hello 달 하 고 해당 월에 대 한 두 번째는 hello 번호와 hello 여기에서 합니다.

Hello 다음 hello 하이브 디렉터리 프롬프트에서 명령을 실행 하 여 학습 데이터 집합에 hello 레코드의 총 수를 계산할 수도 했습니다.

    hive -e "select count(*) from nyctaxidb.trip;"

다음과 같은 결과가 산출됩니다.

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

명령을 비슷한 toothose hello 학습 데이터 집합에 대 한 표시를 사용 하 여 우리 hello 요금 데이터 집합 toovalidate hello 레코드 개수에 대 한 hello 하이브 디렉터리 프롬프트에서 하이브 쿼리를 실행할 수 있습니다.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

이 목록에 hello 출력:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Hello 정확히 동일한 수와 한 달의 두 데이터 집합에 대해 반환 되는 참고 합니다. 데이터를 올바르게 로드 하는 hello hello 첫 번째 유효성 검사를 제공 합니다.

Hello hello 요금 데이터 집합에 있는 레코드의 총 수를 계산을 수행할 수 있습니다 hello 하이브 디렉터리 프롬프트에서 아래 hello 명령을 사용 하 여:

    hive -e "select count(*) from nyctaxidb.fare;"

다음과 같은 결과가 산출됩니다.

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

hello 두 테이블 모두에 있는 레코드의 총 수는 동일한 hello도 합니다. 데이터를 올바르게 로드 하는 hello 두 번째 유효성 검사를 제공 합니다.

### <a name="exploration-trip-distribution-by-medallion"></a>탐색: medallion별 여정 분포
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

이 예에서는 지정 된 기간 내에서 100 개 이상의 트립을 있는 hello 메달 (택시 번호)를 식별합니다. hello에서 hello 쿼리 혜택 hello 파티션 변수 전제로 이후 테이블 액세스를 분할 **월**합니다. hello 쿼리 결과가 작성 tooa 로컬 파일 queryoutput.tsv `C:\temp` hello 헤드 노드에서 합니다.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Hello 내용의 다음과 같습니다 *샘플\_하이브\_여행\_count\_여\_medallion.hql* 검사에 대 한 파일입니다.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

hello 메달 hello NYC 택시 데이터 집합의 고유한 cab 파일을 식별합니다. 특정 기간에 특정 여정 수를 초과하는 택시를 조회하여 "운행량이 많은" 택시를 식별할 수 있습니다. hello 다음 예제에서는 식별 cabs 처음 3 개월 동안 백 개 이상의 trips hello에 대 한 저장 쿼리 결과 tooa 로컬 파일을 C:\temp\queryoutput.tsv hello 합니다.

Hello 내용의 다음과 같습니다 *샘플\_하이브\_여행\_count\_여\_medallion.hql* 검사에 대 한 파일입니다.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

Hello에서 하이브 아래의 문제 hello 명령을 디렉터리 프롬프트:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>탐색: medallion 및 hack_license별 여정 분포
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

데이터 집합을 탐색 하는 경우 그룹 값의 발생 하는 공동 tooexamine hello 수 자주 하려고 합니다. 이 섹션 어떻게 toodo이에 대 한 cab 및 드라이버의 예제를 제공 합니다.

hello *샘플\_하이브\_여행\_count\_여\_메달\_license.hql* "메달" 및 "hack_license"에 설정 하는 hello 요금 데이터를 그룹화 하는 파일 및 각 조합 수가 반환 합니다. 내용은 다음과 같습니다.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

이 쿼리는 택시와 특정 운전 기사의 조합을 여정 수 내림차순으로 반환합니다.

Hello에서 하이브 디렉터리 프롬프트를 실행 합니다.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

쿼리 결과 hello C:\temp\queryoutput.tsv tooa 로컬 파일에 기록 됩니다.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>탐색: 잘못된 경도/위도 레코드를 확인하여 데이터 품질 평가
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

예비 데이터 분석의 일반적인 목표에는 tooweed 잘못 되었거나 잘못 된 레코드입니다. hello이 섹션의 예 포함할 수 있는지를 결정 하거나 hello 위도 나 경도의 필드 hello NYC 영역에서 멀리 떨어진 값입니다. 레코드가 있는 경우 잘못 된 경도 위도 값 이므로 tooeliminate 모델링에 사용 되는 모든 데이터를 toobe에서 확인할 수 있습니다.

다음의 hello 콘텐츠는 *샘플\_하이브\_품질\_assessment.hql* 검사에 대 한 파일.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


Hello에서 하이브 디렉터리 프롬프트를 실행 합니다.

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

hello *-S* 이 명령에 포함 하는 인수 hello 하이브 Map/Reduce 작업의 상태 화면 인쇄물 hello를 표시 하지 않습니다. 하이브 보다 읽기 쉬운 쿼리 출력의 hello hello 화면 인쇄를 수행 하기 때문에 유용 합니다.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>탐색: 여정 팁의 이진 클래스 분포
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

Hello에 설명 된 hello 이진 분류 문제에 대 한 [예측 작업의 예제](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 섹션 것이 유용한 tooknow 팁 여부를 지정 했는지 여부입니다. 이 팁 분포는 이진입니다.

* tip given(Class 1, tip\_amount > $0)  
* no tip (Class 0, tip\_amount = $0).

hello *샘플\_하이브\_크리스마스\_frequencies.hql* 파일 아래에 표시 된이 작업을 수행 합니다.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

Hello에서 하이브 디렉터리 프롬프트를 실행 합니다.

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>탐색: hello 다중 클래스 설정에 대 한 분포 클래스
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

Hello에 설명 된 hello 다중 클래스 분류 문제에 대 한 [예측 작업의 예제](machine-learning-data-science-process-hive-walkthrough.md#mltasks) 섹션이 데이터 집합 또한 경우가 많으므로 tooa 자연 분류 toopredict hello 양을 지정 하는 hello 팁 싶습니다. Hello 쿼리에서 bin toodefine 팁 범위를 사용할 수 있습니다. tooget hello hello에 대 한 클래스 분포 다양 한 팁 범위, 사용 하 여 hello *샘플\_하이브\_팁\_범위\_frequencies.hql* 파일입니다. 내용은 다음과 같습니다.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Hello Hadoop 명령줄 콘솔에서 다음 명령을 실행 합니다.

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>탐색: 두 경도-위도 위치 간의 직접 거리 계산
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

Hello 직접 거리를 측정 하면 us hello 간의 hello 불일치 아웃 toofind 실제 여행 거리입니다. 이 기능을 승객 작을 수 있으며 알려 동기 우리 해당 hello 드라이버를 파악 하는 경우 가능성이 tootip 의도적으로 통합 하였습니다에 긴 경로 의해 합니다.

실제 여행 거리 및 hello toosee hello 비교 [Haversine 거리](http://en.wikipedia.org/wiki/Haversine_formula) 두 경도 위도 점 (hello "좋은 circle" 거리) 간 사용 hello 삼각 함수를 사용할 수 있는, 하이브에 내 따라서:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

위의 hello 쿼리 R hello radius 마일에 hello 지구의 이며 pi는 변환 된 tooradians 합니다. Hello 경도 위도 포인트 hello NYC 영역 멀리 떨어져 있는 "필터링된" tooremove 값 되지 않았는지 note 합니다.

이 경우 "queryoutputdir" 라는 우리의 결과 tooa 디렉터리를 작성 합니다. hello 명령 시퀀스를 아래 표시 된 먼저이 출력 디렉터리를 만들고 hello 하이브 명령을 실행 합니다.

Hello에서 하이브 디렉터리 프롬프트를 실행 합니다.

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


hello 쿼리 결과가 작성 되 too9 Azure blob ***queryoutputdir/000000\_0*** 너무 ***queryoutputdir/000008\_0*** hello Hadoop 클러스터의 hello 기본 컨테이너에서 합니다.

toosee hello 각 blob의 크기를 hello, hello hello 하이브 디렉터리 프롬프트에서 다음 명령을 실행 합니다.

    hdfs dfs -ls wasb:///queryoutputdir

지정된 된 파일의 toosee hello 내용을 말 000000\_0, 사용 하 여 Hadoop의 `copyToLocal` 명령, 따라서 합니다.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal`은 파일이 큰 경우 매우 느려질 수 있으므로 큰 파일에 사용하지 않는 것이 좋습니다.  
> 
> 

Azure blob에 있는이 데이터를 포함 하는 주요 이점이 hello를 사용 하 여 Azure 기계 학습에서 hello 데이터를 탐색할 수 있습니다 있습니다 [데이터 가져오기] [ import-data] 모듈입니다.

## <a name="#downsample"></a>Azure 기계 학습에서 데이터 다운 샘플링 및 모델 빌드
> [!NOTE]
> 이는 일반적으로 **데이터 과학자** 작업입니다.
> 
> 

Hello 예비 데이터 분석 단계 이후에 이제 Azure 기계 학습에서 모델을 작성 하기 위한 준비 toodown 샘플 hello 데이터입니다. 이 섹션에서는 toouse 하이브 액세스 하는 다음 hello toodown 샘플 hello 데이터를 쿼리 하는 방법을 보여줍니다 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다.

### <a name="down-sampling-hello-data"></a>아래로 hello 데이터 샘플링
이 절차에는 두 단계가 있습니다. Hello 가입 म **nyctaxidb.trip** 및 **nyctaxidb.fare** 모든 레코드에 있는 3 개의 키에서 테이블: "메달", "해킹\_라이선스", 및 "픽업\_날짜/시간"입니다. 그런 다음, 이진 분류 레이블 **tipped**와 다중 클래스 분류 레이블 **tip\_class**를 생성합니다.

hello에서 직접 데이터를 샘플링 toobe 수 toouse hello [데이터 가져오기] [ import-data] 모듈의 쿼리 tooan 내부 하이브 테이블 위에 hello 필요한 toostore hello 결과 Azure 기계 학습 합니다. 뒤에 오는, 내부 하이브 테이블을 만든 하 가입 hello로 및 샘플링된 한 데이터를 해당 콘텐츠를 채울 합니다.

hello 쿼리 함수를 적용 표준 하이브 직접 toogenerate hello 시간, 요일 (1, 월요일은 및 일요일 7 의미 함) hello에서 연도의 주 "pickup\_datetime" 필드 및 hello 픽업 사이의 dropoff hello 직접 거리 위치입니다. 사용자가 너무 참조할 수[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) 전체 목록은 이러한 기능에 대 한 합니다.

쿼리 hello 다음 hello 쿼리 결과 hello Azure 기계 학습 스튜디오에 넣을 수 있도록 샘플 hello 데이터 다운 합니다. Hello 원래 데이터 집합의 약 1% Studio hello로 가져옵니다.

다음의 hello 내용을 *샘플\_하이브\_준비\_에 대 한\_aml\_full.hql* Azure 기계 학습에서 작성 하는 모델에 대 한 데이터를 준비 하는 파일입니다.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

toorun hello 하이브 디렉터리에서이 쿼리를 표시 합니다.

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

이제는 내부 테이블이 있다고 hello를 사용 하 여 액세스할 수 있는 "nyctaxidb.nyctaxi_downsampled_dataset" [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다. 또한 이 데이터 집합을 사용하여 기계 학습 모델을 빌드할 수 있습니다.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>샘플링된 한 데이터를 Azure 기계 학습 tooaccess hello hello 데이터 가져오기 모듈 사용
Hello에서 하이브 쿼리를 실행 하는 것에 대 한 필수 구성 요소로 [데이터 가져오기] [ import-data] tooan Azure 기계 학습 작업 영역 액세스 및 hello의 toohello 자격 증명에 액세스 해야 Azure 기계 학습의 모듈을 클러스터 및 해당 연결 된 저장소 계정입니다.

Hello에 대 한 일부 내용은 [데이터 가져오기] [ import-data] 모듈과 hello 매개 변수 tooinput:

**HCatalog 서버 URI**: hello 클러스터 이름 abc123 경우이 단순히: https://abc123.azurehdinsight.net

**Hadoop 사용자 계정 이름을** : hello 클러스터에 대 한 선택한 hello 사용자 이름 (**하지** hello 원격 액세스 사용자 이름)

**Hadoop 사용자 계정 암호** : hello 클러스터에 대 한 선택한 hello 암호 (**하지** hello 원격 액세스 암호)

**출력 데이터의 위치** :이 Azure toobe 있다고 표시 합니다.

**Azure 저장소 계정 이름** : hello 클러스터와 연결 된 hello 기본 저장소 계정의 이름입니다.

**Azure 컨테이너 이름을** : hello 클러스터에 대 한 기본 컨테이너 이름이 hello 이며 일반적으로 hello 클러스터 이름으로 같은 hello 됩니다. "abc123"이라는 클러스터의 경우 단순히 abc123입니다.

> [!IMPORTANT]
> **Hello를 사용 하 여 tooquery 했는데도 테이블 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈에는 내부 테이블 이어야 합니다.** 데이터베이스 D.db의 테이블 T가 내부 테이블인지 확인하기 위한 팁은 다음과 같습니다.
> 
> 

Hello에서 하이브 디렉터리 프롬프트 문제 hello 명령:

    hdfs dfs -ls wasb:///D.db/T

Hello 테이블은 내부 테이블을 채웁니다 내용이 여기에 표시 해야 합니다. 또 다른 방법은 toodetermine toouse hello Azure 저장소 탐색기는 테이블 한 내부 테이블 인지 합니다. Hello 클러스터의 toonavigate toohello 기본 컨테이너 이름을 사용 하 고 hello 테이블 이름으로 필터링 한 다음 키를 누릅니다. Hello 테이블 및 해당 내용을 표시 되는, 내부 테이블 인지 확인 합니다.

여기 hello 하이브 쿼리 및 hello 스냅숏일 [데이터 가져오기] [ import-data] 모듈:

![데이터 가져오기 모듈에 대한 Hive 쿼리](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

에 불과하며 샘플링된 한 데이터 hello 기본 컨테이너에 있는 다운, 이후 Azure 기계 학습에서 hello 결과 하이브 쿼리는 매우 간단 단지는 "선택 * nyctaxidb.nyctaxi에서\_다운 샘플링\_데이터".

이제 시작 지점 기계 학습 모델을 작성 하기 위한 hello로 hello 데이터 집합을 사용할 수 있습니다.

### <a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드
수 tooproceed toomodel 건물과 모델 배포에는 이제 [Azure 기계 학습](https://studio.azureml.net)합니다. hello 데이터가 우리 준비 되어 toouse 위에 명시 된 hello 예측 문제 해결:

**1. 이진 분류**: toopredict 트립이 팁 지불 여부.

**사용된 학습자:** 2클래스 로지스틱 회귀

a. 이 문제의 경우 대상(또는 클래스) 레이블은 "tipped"입니다. 원래 다운 샘플링된 데이터 집합에는 이 분류 실험에 대한 대상 누수인 몇 가지 열이 있습니다. 특히: 팁\_클래스, 팁\_금액과 총\_금액 테스트 시간에 사용할 수 없는 hello 대상 레이블에 대 한 정보를 표시 합니다. Hello를 사용 하 여 고려 대상에서 이러한 열을 제거 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

hello 스냅숏 아래 우리의 실험 toopredict 주어진된 여행에 대 한 팁은 지불 여부를 보여 줍니다.

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. 이 실험의 경우 대상 레이블 분포는 약 1:1입니다.

아래 hello 스냅숏 hello 이진 분류 문제에 대 한 팁 클래스 레이블의 hello 분포를 보여 줍니다.

![팁 클래스 레이블의 분포](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

따라서 아래 hello 그림에 나와 있는 것 처럼 0.987의 AUC를 얻습니다.

![AUC 값](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. 다중 클래스 분류**: hello를 사용 하 여 이전에 hello 여행용 지불 팁 금액 toopredict hello 범위에 정의 된 클래스입니다.

**사용된 학습자:** 다중 클래스 로지스틱 회귀

a. 이 문제의 경우 대상(또는 클래스) 레이블은 5개 값(0, 1, 2, 3, 4) 중 하나일 수 있는 "tip\_class"입니다. Hello 이진 분류 경우 처럼이 실험에 대 한 대상 누수 되는 몇 가지 열 했습니다. 특히: 팁, 크리스마스\_금액, 총\_금액 테스트 시간에 사용할 수 없는 hello 대상 레이블에 대 한 정보를 표시 합니다. Hello를 사용 하 여 이러한 열을 제거 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

어떤 bin 팁은 가능성이 toofall 우리의 실험 toopredict 다음 hello 스냅숏 (클래스 0: 팁 = $0, 1 클래스: > \ 0 및 팁 팁 < = $5, 클래스 2: > $5 및 팁 팁 < = $10, Class 3: > $10에서 팁 팁 < = $20 를 클래스 4: > $20 팁)

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

실제 테스트 클래스 분포는 다음과 같습니다. 클래스 0 및 1 클래스는 널리 알려진, hello 다른 클래스는 드문 표시 됩니다.

![테스트 클래스 분포](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. 이 실험에는 예측 정확도에 혼동 행렬 toolook을 사용합니다. 다음과 같습니다.

![혼동 행렬](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Note는 hello 많이 사용 된 클래스에는 클래스 정확도 활동적 상태인 동안 hello 모델 하지 않습니다 "학습"이의 hello 드문 클래스에 있습니다.

**3. 회귀 작업**: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.

**사용된 학습자:** 향상된 의사 결정 트리

a. 이 문제의 경우 대상(또는 클래스) 레이블은 "tip\_amount"입니다. 우리의 대상 누수가 경우에: 팁, 크리스마스\_클래스, 총\_크기, 이러한 테스트 시간에서 일반적으로 사용할 수 있는 hello 팁 금액에 대 한 정보를 노출 하는 모든이 변수입니다. Hello를 사용 하 여 이러한 열을 제거 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

hello 스냅숏 belows 팁을 제공 하는 hello 우리의 실험 toopredict hello 시간이 표시 됩니다.

![실험 스냅숏](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. 회귀 문제에 대 한 म hello 예측에 대 한 제곱 hello 오류가 확인 하 여 우리의 예측의 hello 정확도 측정, 결정 계수 hello 및 같은 hello 합니다. 아래와 같이 표시됩니다.

![예측 통계](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Hello에 대 한 결정 계수는 0.709, 모델 계수 취급 하 여 설명 hello 차이의 약 71% 암시 합니다.

> [!IMPORTANT]
> toolearn Azure 기계 학습에 대 한 자세한 방법과 tooaccess 및 사용에 너무 참조[기계 학습 란?](machine-learning-what-is-machine-learning.md)합니다. 다양 한 Azure 기계 학습에서 기계 학습 실험으로 게임에 대 한 매우 유용한 리소스는 hello [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com/)합니다. hello 갤러리의 실험 하는 영역에 설명 하 고 Azure 기계 학습의 철저 한 소개할 기능의 hello 범위를 제공 합니다.
> 
> 

## <a name="license-information"></a>라이선스 정보
이 샘플 연습 및 함께 제공 되는 스크립트는 hello MIT 라이선스에 따라 Microsoft에서 공유 됩니다. 자세한 내용은 GitHub에서 hello 샘플 코드의 hello 디렉터리에 hello LICENSE.txt 파일 확인 하십시오.

## <a name="references"></a>참조
• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)  
• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
