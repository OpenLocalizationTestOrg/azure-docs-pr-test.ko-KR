---
title: "1TB 데이터 집합에는 Azure HDInsight Hadoop 클러스터를 사용 하 여 작업-에 팀 데이터 과학 프로세스 hello | Microsoft Docs"
description: "HDInsight Hadoop을 사용 하는 종단 간 시나리오에 대 한 hello 팀 데이터 과학 프로세스를 사용 하 여 클러스터링 toobuild 하 고 큰 (1TB) 공개적으로 사용할 수 있는 데이터 집합을 사용 하 여 모델 배포"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>1TB 데이터 집합에는 Azure HDInsight Hadoop 클러스터를 사용 하 여 작업-에 hello 팀 데이터 과학 프로세스

이 연습에 대해서도 설명를 사용 하 여 데이터 과학 팀 프로세스를 사용 하는 종단 간 시나리오에서 hello는 [Azure HDInsight Hadoop 클러스터](https://azure.microsoft.com/services/hdinsight/) toostore, 탐색, 엔지니어, 기능 및 hello 중 하나에서 예제 데이터를 공개적으로 아래쪽 사용 가능한 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 데이터 집합입니다. 이 데이터에 대해 Azure 기계 학습 toobuild 이진 분류 모델을 사용합니다. 또한 어떻게 toopublish 다음 중 하나를 모델링 웹 서비스로 보여 줍니다.

이 연습에서 수행할는 IPython 노트북 tooaccomplish hello 작업 가능한 toouse 이기도 합니다. 사용자에 게는이 방법을 문의 해야 tootry 같은 hello [하이브 ODBC 연결을 사용 하 여 Criteo 연습](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 항목입니다.

## <a name="dataset"></a>데이터 집합 설명
hello Criteo 데이터는 클릭 예측 데이터 집합을 gzip 압축 TSV 파일 (~1.3TB 압축 되지 않은)의 약 370 g B 이상 4.3 십억 레코드를 구성 합니다. [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)에서 사용할 수 있는 24일간의 클릭 데이터를 가져옵니다. 데이터 과학자의 hello 편의 위해 데이터를 사용할 수 있는 toous tooexperiment에 압축을 했습니다.

이 데이터 집합의 각 레코드에는 40개의 열이 있습니다.

* hello 첫 번째 열은 사용자가 클릭 여부를 나타내는 레이블 열은 **추가** (값 1) (값 0) 하나를 클릭 하지 않는 또는
* 다음 13개의 열은 숫자입니다.
* 마지막 26개는 범주 열입니다.

hello 열은 익명으로 처리 및 여러 개의 열거 된 이름 사용 하 여: (hello 레이블 열)에 대 한 "Col1" 너무 ' Col40 "(마지막 범주 열 hello)에 대 한 합니다.            

여기서는 hello의 일부 먼저 20의 열이 데이터이 집합에서 두 가지 사항을 확인할 (행):

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

이 데이터 집합에 두 hello 숫자 및 범주 열에 누락 값이 있습니다. Hello 누락 값을 처리 하는 간단한 방법을 설명 합니다. Hello 데이터에 대 한 자세한 내용은 Hive 테이블에 저장 하는 경우에 대해서는 합니다.

**정의:** *클릭 광고 속도 (CTR):* hello 데이터 â hello 비율입니다. 이 Criteo 데이터 집합에 hello CTR는 약 3.3% 또는 0.033 합니다.

## <a name="mltasks"></a>예측 작업의 예제
이 연습에서는 두 가지 샘플 예측 문제를 처리합니다.

1. **이진 분류**: 사용자가 광고를 클릭했는지 여부를 예측합니다.
   
   * 클래스 0: 클릭 안 함
   * 클래스 1: 클릭
2. **회귀**: 사용자 기능에서 클릭 광고의 hello 확률을 예측 합니다.

## <a name="setup"></a>데이터 과학용 HDInsight Hadoop 클러스터 설정
**참고:** 일반적으로 **관리** 태스크입니다.

다음 3단계에 따라 HDInsight 클러스터를 사용하여 예측 분석 솔루션을 빌드하기 위한 Azure 데이터 과학 환경을 설정합니다.

1. [저장소 계정 만들기](../storage/common/storage-create-storage-account.md):이 저장소 계정은 Azure Blob 저장소에 사용 되는 toostore 데이터입니다. HDInsight 클러스터에 사용 되는 hello 데이터 여기에 저장 됩니다.
2. [데이터 과학용 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md):이 단계에서는 모든 노드에 설치된 64비트 Anaconda Python 2.7을 사용하여 Azure HDInsight Hadoop 클러스터를 만듭니다. Hello HDInsight 클러스터를 사용자 지정할 때 두 가지 중요 한 단계 (이 항목에서 설명) toocomplete가 있습니다.
   
   * Hello 저장소 계정을 만들 때 HDInsight 클러스터와 1 단계에서 만든 연결 해야 합니다. 이 저장소 계정은 hello 클러스터 내에서 처리할 수 있는 데이터에 액세스 하기 위해 사용 됩니다.
   * 만든 후 원격 액세스 toohello hello 클러스터의 헤드 노드를 사용 하도록 설정 해야 합니다. Hello 원격 액세스 (생성 시 hello 클러스터에 대 한 지정 된 것과 다른) 여기에서 지정한 자격 증명 기억: toocomplete 필요한 경우 다음 절차 hello 합니다.
3. [Azure ML 작업 영역을 만들](machine-learning-create-workspace.md):이 Azure 기계 학습 작업 영역은 초기 데이터 탐색 후] 및 [아래로 hello HDInsight 클러스터에서 샘플링 기계 학습 모델을 구축 하기 위한 사용 됩니다.

## <a name="getdata"></a>공용 원본에서 데이터 가져오기 및 사용
hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) hello 링크를 클릭 하면 hello 사용 약관을 수락 하 고 이름을 제공 하 여 데이터 집합을 액세스할 수 있습니다. 다음과 같은 스냅숏이 나타납니다.

![Criteo 조건 동의](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

클릭 **계속 tooDownload** tooread hello 데이터 집합 및 가용성에 대 한 자세한 합니다.

공용에서 hello 데이터가 있는 [Azure blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 위치: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/합니다. "wasb" hello tooAzure Blob 저장소 위치를 참조합니다. 

1. 이 공용 blob 저장소에 hello 데이터 압축 푼된 데이터의 세 가지 하위 구성 됩니다.
   
   1. 하위 폴더를 hello *원시/count/* hello 데이터 요금-날부터의 첫 번째 21 일 포함\_00 tooday\_20
   2. 하위 폴더를 hello *원시/학습/* 데이터의 하루 이루어져 일\_21
   3. 하위 폴더를 hello *원시/테스트/* 2 일 분량의 데이터를 이루어져 일\_22 및 day\_23
2. 사람들 toostart hello 원시 gzip 데이터와, 이러한 사용할 수도 있습니다 hello 기본 폴더에 *원시 /* 00 too23에서 NN 흐름 방향은 day_NN.gz로 합니다.

다른 접근 방식은 tooaccess 탐색 하 고 로컬 다운로드 하이브 테이블을 만들 때이 연습 뒷부분에서 설명 하지 않아도이 데이터를 모델링 합니다.

## <a name="login"></a>Toohello 클러스터 헤드 노드에 로그인
사용 하 여 hello hello 클러스터의 헤드 노드에 toohello toolog [Azure 포털](https://ms.portal.azure.com) toolocate hello 클러스터입니다. 왼쪽 hello에 hello HDInsight 코끼리 아이콘을 클릭 하 고 클러스터의 hello 이름을 두 번 클릭 합니다. Toohello 이동 **구성** 탭 hello hello 페이지 아래쪽에 hello 연결 아이콘을 두 번 클릭 하 고 메시지가 표시 되 면 원격 액세스 자격 증명을 입력 합니다. Hello 클러스터의 헤드 노드에 toohello 이동합니다.

클러스터 헤드 노드에 toohello에 일반적인 첫 번째 로그의 모양은 다음과 같습니다.

![Toocluster 로그인](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Hello 왼쪽에 "Hadoop 명령" 하는 줄 hello 데이터 탐색에 대 한 우리의 즐겨 hello를 보면 됩니다. 두 가지 유용한 URL인 "Hadoop Yarn Status" 및 "Hadoop Name Node"도 있습니다. hello yarn 상태 URL 작업 진행 상황을 표시 하 고 hello 이름 노드 URL hello 클러스터 구성에 세부 정보를 제공 합니다.

이제 우리는를 설정 하 고 hello 연습의 첫 번째 부분 toobegin 준비 됨: 데이터 탐색 하이브를 사용 하 여 및 Azure 기계 학습에 대 한 데이터를 준비 합니다.

## <a name="hive-db-tables"></a> Hive 데이터베이스 및 테이블 만들기
하이브 toocreate 우리의 Criteo 데이터 집합 열기 hello에 대 한 테이블 ***Hadoop 명령줄*** hello 헤드 노드의 데스크톱 hello 되 고 hello 명령을 입력 하 여 hello 하이브 디렉터리를 입력 합니다.

    cd %hive_home%\bin

> [!NOTE]
> Hello 하이브 bin에서이 연습에서 모든 하이브 명령을 실행 / directory 프롬프트입니다. 경로 문제가 자동으로 해결됩니다. Hello 용어 "하이브 디렉터리 프롬프트"를 사용 하 여 "하이브 bin / directory 프롬프트", "Hadoop 명령줄" 같은 의미로 합니다.
> 
> [!NOTE]
> tooexecute 모든 하이브 쿼리 하나 명령 뒤 hello 항상 사용할 수 있습니다.
> 
> 

        cd %hive_home%\bin
        hive

Hello 후 하이브 REPL 표시는 "하이브 >" 서명, 단순히에서 잘라내기 및 붙여넣기 hello 쿼리 tooexecute 것입니다.

hello 다음 코드에서는 "criteo" 데이터베이스 만들고 4 테이블을 생성 합니다.

* *개수를 생성 하기 위한 테이블이* 일 날에 빌드된\_00 tooday\_20 일
* *사용 하기 위해 테이블에 hello 학습 데이터 집합으로* 날에 빌드된\_21, 및
* 두 개의 *hello로 사용 하기 위해 테이블 테스트 데이터 집합* 날에 빌드된\_22 및 day\_23 각각.

우리는 휴일, 고 hello 모델 hello 클릭 광고 속도에서 공휴일 및 비 휴일 간의 차이점을 검색할 수 있는 경우 원하는 toodetermine hello 일 중 하나 때문에 서로 다른 두 테이블으로 우리의 테스트 데이터 집합을 분할 합니다.

스크립트 hello [샘플 &#95; 하이브 &#95; 만들기 &#95; criteo &#95; 데이터베이스 &#95; 및 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) 편의 위해 여기에 표시 됩니다.

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

이러한 모든 테이블은 단순히 지점 tooAzure Blob 저장소 (wasb) 위치에서는으로 외부 기록한 합니다.

**두 가지 방법 tooexecute ANY 하이브 쿼리 이제 언급 하는 있습니다.**

1. **하이브 REPL 명령줄 hello를 사용 하 여**: hello 먼저 tooissue "하이브" 명령과 복사 되며 hello 하이브 REPL 명령줄에서 쿼리를 붙여 넣습니다. toodo이를이 수행 합니다.
   
        cd %hive_home%\bin
        hive
   
     명령줄 REPL hello에 잘라내기 및 붙여넣기 이제 hello 쿼리를 실행 하 고 있습니다.
2. **저장 쿼리 tooa 파일과 hello 명령을 실행**: hello toosave hello 쿼리 tooa.hql 파일을 두 번째는 ([샘플 &#95; 하이브 &#95; 만들기 &#95; criteo &#95; 데이터베이스 &#95; 및 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql))과 다음 문제 hello 다음 명령 tooexecute hello 쿼리:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>데이터베이스 및 테이블 만들기 확인
다음으로 hello 하이브 bin에서 다음 명령을 hello로 hello hello 데이터베이스 만들기 확인 / directory 프롬프트:

        hive -e "show databases;"

다음 출력이 표시됩니다.

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Hello "criteo" hello 새 데이터베이스 만들기를 확인합니다.

toosee 만든 테이블에서는 단순히 hello에서에서 명령을 실행할 여기 hello 하이브 bin / directory 프롬프트:

        hive -e "show tables in criteo;"

다음 출력을 따라 hello 표시:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Hive에서 데이터 탐색
이제 toodo 하이브에 몇 가지 기본 데이터 탐색을 준비 합니다. Hello hello 학습의 예제 수를 계산 하 여 시작 하 고 테스트 데이터 테이블입니다.

### <a name="number-of-train-examples"></a>train 예제 수
내용을 hello [샘플 &#95; 하이브 #95 개수 및 #95; 기차 및 #95; 테이블 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) 여기에 표시 됩니다.

        SELECT COUNT(*) FROM criteo.criteo_train;

다음과 같은 결과가 산출됩니다.

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

또는 하나 또한 발행 hello 하이브 bin에서 다음 명령을 hello / directory 프롬프트:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>테스트 예제 hello 두 테스트 데이터 집합의 수
에서는 이제 hello 두 개의 테스트 데이터 집합의 예제에서는 hello 수를 계산 합니다. 내용을 hello [샘플 &#95; 하이브 및 #95 개수 및 #95; criteo &#95; 테스트 및 #95; 일 및 #95; 22 &#95; 테이블 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) 는 여기에서:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

다음과 같은 결과가 산출됩니다.

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

일반적으로 म 호출할 수도 있습니다 hello 스크립트 hello 하이브 bin에서 /directory hello 명령을 실행 하 여 프롬프트:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Hello hello 일을 기준으로 테스트 데이터 집합에 테스트 예제 수가 마지막으로 살펴볼\_23입니다.

hello 명령 toodo 이것은 앞서 설명한 하나 비슷한 toohello (너무 참조[샘플 &#95; 하이브 및 #95; 개수 및 #95; criteo #95 테스트 및 #95; 일 및 #95; 23 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

다음 출력이 표시됩니다.

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Hello 학습 데이터 집합의 레이블 배포
hello 학습 데이터 집합의 레이블 배포 hello은 합니다. toosee이 내용의 알아보겠습니다 [샘플 &#95; 하이브 및 #95; criteo #95 레이블 및 #95; 배포 &#95; 기차 &; #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

이 식이 hello 레이블 배포가 됩니다.

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

양수 레이블 백분율로 hello 참고는 3.3% 정도 (원래 hello 데이터 집합과 일치)입니다.

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>데이터 집합을 학습 하는 hello의 일부 숫자 변수 histogram 분포
하이브의 네이티브를 사용할 수 있습니다 "히스토그램\_숫자" hello 숫자 변수 어떤 hello 분포 처럼 보이는 아웃 toofind 작동 합니다. 다음은 hello 내용의 [샘플 &#95; 하이브 및 #95; criteo #95 히스토그램 &; #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

이 hello 다음을 대화 상자가 나타납니다.

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

hello 측면 뷰-폭발에서 하이브 처리 tooproduce hello 일반적인 목록 대신 SQL과 유사한 출력을 조합 합니다. 참고는에 hello 테이블, hello 첫 번째 열이 해당 toohello bin 중심과 hello 두 번째 toohello bin 빈도.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>데이터 집합을 학습 하는 hello의 일부 숫자 변수 대략적인 백분위 수
또한 관심 있는 숫자 변수와 함께 대략적인 백분위 수의 hello 계산이 됩니다. 여기에는 Hive의 기본 "percentile\_approx"가 사용됩니다. 내용을 hello [샘플 &#95; hive &#95; criteo &; #95; 근사치 &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) 됩니다:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

다음과 같은 결과가 산출됩니다.

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

에서는 주석 백분위 수의 hello 분포는 숫자 변수 밀접 한 관련이 toohello 히스토그램 분포 일반적으로 표시 합니다.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Hello 학습 데이터 집합의 일부 범주 열에 대 한 고유 값 수 찾기
지속적 hello 데이터 탐색, 이제 보면 일부 범주 열의 경우 hello 가지도록 고유 값 수가 있습니다. toodo이의 콘텐츠를 표시 했습니다 [샘플 &#95; hive &#95; criteo &; #95 고유; &#95; 값 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

다음과 같은 결과가 산출됩니다.

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Col15에 1,900만 개의 고유 값이 있습니다. Tooencode "하나 핫 인코딩"와 같은 naïve 기법을 사용 하 여 이러한 차원 범주 변수는 쉽지 않습니다. 따라서 여기에서는 이 문제를 효과적으로 해결하는 [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 라는 강력한 기술을 설명하고 알아봅니다.

몇 가지 다른 범주 열에 대 한 고유 값 수가 hello 확인 하 여에이 하위 섹션을 종료 합니다. 내용을 hello [샘플 &#95; hive &#95; criteo &; #95 고유; & #95, 값 및 #95, 여러 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) 됩니다:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

다음과 같은 결과가 산출됩니다.

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

다시 보면 있는지 Col20를 제외한 모든 hello 다른 많은 고유 값이 있는 열입니다.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Hello 학습 데이터 집합의 범주 변수의 쌍 공동 발생 횟수

hello 공동 발생 횟수 범주 변수의 쌍은도 합니다. hello 코드를 사용 하 여 확인할 수 있습니다 [샘플 &#95; hive &#95; criteo &; #95 쌍을 이루는; &#95; 범주 &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

म 발생 하 여 주문 hello 수량이 역방향으로 한이 예에서 hello 상위 15 확인 합니다. 다음 출력이 표시됩니다.

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Azure 기계 학습에 대 한 샘플 hello 데이터 집합 아래로
데이터 집합 탐색된 hello 필요 하 고 있습니다 방법은 이러한 유형의 샘플 hello 데이터 집합 아래로 이제 우리는 변수 (포함 하 여 조합)에 대 한 탐색 하 여 Azure 기계 학습에서 모델을 작성할 수 있습니다를 살펴보았습니다. 에 대해 살펴볼 해당 hello 문제는 회수: Col1은 0 (클릭 없음) 또는 1 (클릭) 하는 경우 예측 예제 특성 (c o l 2-Col40에서에서 기능 값)의 집합을 지정 했습니다.

toodown 샘플 우리의 학습 및 테스트 데이터 집합 too1 %hello 원래 크기의, 하이브의 네이티브 rand () 함수를 사용 합니다. 다음 스크립트를 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 기차 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hello 학습 데이터 집합에 대해이 작업을 수행 합니다.

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

다음과 같은 결과가 산출됩니다.

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

스크립트 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 테스트 및 #95; 일 및 #95; 22 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) 테스트 데이터에는 하루\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

다음과 같은 결과가 산출됩니다.

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


마지막으로 스크립트를 hello [샘플 &#95; 하이브 및 #95; criteo &#95; 저해상도 #95 테스트 및 #95; 일 및 #95; 23 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) 테스트 데이터에는 하루\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

다음과 같은 결과가 산출됩니다.

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

이 준비 toouse 우리의 다운 샘플링 하는 학습 및 테스트에 Azure 기계 학습 모델을 작성 하는 것에 대 한 데이터 집합입니다.

문제 hello 개수 테이블은 기계 학습에서는 tooAzure 넘어가기 전에는 최종 중요 한 요소입니다. Hello 다음 하위 섹션에서이 부분은 자세히 살펴봅니다.

## <a name="count"></a>Hello 개수 테이블에 대 한 간단한 설명
몇몇 범주 변수는 차원이 매우 높습니다. 이 연습에서는 강력한 기술을 소개 [학습와 계산](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode 효율적이 고 강력한 방식으로 이러한 변수입니다. 이 방법에 대 한 자세한 내용은 hello에 제공 된 링크입니다.

[!NOTE]
>이 연습에서는 차원 범주 기능의 개수 테이블 tooproduce compact 표현을 사용 하 여 집중 합니다. 이 hello 유일한 방법은 tooencode 범주 기능입니다. 다른 기술에 대 한 자세한 내용은 사용자가 관심된을 체크 아웃할 수 [하나 핫-인코딩](http://en.wikipedia.org/wiki/One-hot) 및 [기능 해시](http://en.wikipedia.org/wiki/Feature_hashing)합니다.
>

hello 개수 데이터에서 toobuild 개수 테이블에서 개수 폴더 원시/hello hello 데이터 사용합니다. 사용자가 알아보겠습니다 섹션을 모델링 하는 hello에 어떻게 toobuild 이러한 계산 테이블은 처음부터 새로, 또는 또는 toouse 범주 기능에 대 한 해당 탐색에 대 한 미리 작성 된 개수 테이블 합니다. 기능에서 참조 하는 경우 다음과 같이 너무 "미리 작성 된 개수 테이블", 제공 하는 hello 개수 테이블을 사용 하 여 의미 합니다. Tooaccess 이러한 테이블 제공 방법을 hello 다음 섹션에 대 한 자세한 설명입니다.

## <a name="aml"></a> Azure 기계 학습에서 모델 빌드
Azure Machine Learning의 모델 빌드 프로세스는 다음 단계를 따릅니다.

1. [Azure 기계 학습에 Hive 테이블에서 hello 데이터 가져오기](#step1)
2. [Hello 실험 만들기: hello 데이터 및 기능 화할 개수 테이블 정리](#step2)
3. [빌드, 학습 및 점수 hello 모델](#step3)
4. [Hello 모델 평가](#step4)
5. [Hello 모델을 웹 서비스로 게시](#step5)

이제는 Azure 기계 학습 스튜디오에서 준비 toobuild 모델입니다. 아래쪽 샘플링 된 데이터는 hello 클러스터의 Hive 테이블으로 저장 됩니다. Hello Azure 기계 학습 사용 하 여 **데이터 가져오기** 모듈 tooread이이 데이터입니다. 이 클러스터의 hello 자격 증명 tooaccess hello 저장소 계정 다음에 제공 됩니다.

### <a name="step1"></a>1 단계: hello 데이터 가져오기 모듈을 사용 하 여 Azure 기계 학습에 Hive 테이블에서 데이터 가져오기 및 기계 학습 실험에 대 한 선택
**+새로 만들기** -> **실험** -> **빈 실험**을 선택하여 시작합니다. 그런 다음 hello에서 **검색** 상자 위에 표시 hello, "데이터"에 대 한 검색입니다. 끌어서 놓기 hello **데이터 가져오기** 모듈 데이터 액세스를 위한 toohello 실험 캔버스 (hello 화면의 중간 부분 hello) toouse hello 모듈에 저장 합니다.

이 어떤 hello **데이터 가져오기** hello Hive 테이블에서 데이터를 가져오는 동안 것 같습니다.

![데이터 가져오기로 데이터 가져오기](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Hello에 대 한 **데이터 가져오기** hello hello 매개 변수 값의 hello 그래픽은 일종의 값의 hello 예일 뿐 제공 되는 모듈 tooprovide 필요 합니다. Hello 매개 변수는 toofill hello에 대 한 설정 하는 방법에 몇 가지 일반적인 지침 같습니다 **데이터 가져오기** 모듈입니다.

1. **데이터 원본**
2. Hello에 **하이브 데이터베이스 쿼리** 상자의 간단한 SELECT * FROM < 프로그램\_데이터베이스\_name.your\_테이블\_이름 >-충분 합니다.
3. **Hcatalog 서버 URI**: 클러스터가 "abc"인 경우 간단하게 https://abc.azurehdinsight.net입니다.
4. **Hadoop 사용자 계정 이름을**: hello 클러스터 위탁 hello 시 선택한 hello 사용자 이름입니다. Hello 원격 액세스 사용자 이름이 아닌!
5. **Hadoop 사용자 계정 암호**: hello hello 사용자 이름의 암호를 위탁 hello 클러스터의 hello 타임에 선택 합니다. (하지 hello 원격 액세스 암호!)
6. **Location of output data**(출력 데이터 위치): "Azure"를 선택합니다.
7. **Azure 저장소 계정 이름**: hello hello 클러스터와 연결 된 저장소 계정
8. **Azure 저장소 계정 키**: hello 클러스터와 연결 된 hello 저장소 계정의 hello 키입니다.
9. **Azure 컨테이너 이름을**: hello 클러스터 이름에 "abc"는 경우 일반적으로이 단순히 "abc".

한 번 hello **데이터 가져오기** (녹색 hello 눈금에 표시 hello 모듈) 데이터를 가져오기 완료 (사용자가 선택한 이름)으로 데이터 집합으로이 데이터를 저장 합니다. 다음과 같이 표시됩니다.

![데이터 가져오기로 데이터 저장](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

마우스 오른쪽 단추로 클릭 hello 출력 포트의 hello **데이터 가져오기** 모듈입니다. **데이터 집합으로 저장** 옵션 및 **시각화** 옵션이 표시됩니다. hello **시각화** 옵션을 클릭 하면 hello 데이터 일부 요약 통계에 대 한 유용한 오른쪽 패널 100 개 행 표시 됩니다. toosave 데이터를 선택 하기만 하면 **데이터 집합으로 저장할** 지침을 따릅니다.

컴퓨터 학습 실험에서 사용 하기 위해 tooselect hello 저장 된 데이터 집합 hello를 사용 하 여 hello 데이터 집합을 찾을 **검색** 상자 hello 다음 그림에에서 표시 된 것입니다. Hello 이름을 제공한 형식만 hello dataset 다음 tooaccess 하 고 끌어서 hello 데이터 집합의 주 패널 hello 부분적으로 합니다. Hello 기본 패널에 놓으면 컴퓨터 학습 모델링에 사용 하기 위해 선택 합니다.

![Hello 주 패널 끌기 데이터 집합](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Hello 학습 및 테스트 데이터 집합 hello 모두에 대해이 작업을 수행 합니다. 또한 toouse hello 데이터베이스 이름 및이 위해 지정한 테이블 이름을 기억해 야 합니다. 만 위한 그림 purposes.* * hello 그림에 사용 되는 hello 값은
> 
> 

### <a name="step2"></a>2 단계: Azure 기계 학습 toopredict 번의 클릭에서 간단한 실험 만들기 / 클릭 없음
Azure ML 실험은 다음과 같이 표시됩니다.

![기계 학습 실험](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

이제이 실험의 주요 구성 요소를 hello 살펴보겠습니다. 참고로이 저장 된 학습 및 테스트 데이터 집합 tooour 실험 캔버스에 먼저 toodrag이 필요 합니다.

#### <a name="clean-missing-data"></a>누락 데이터 정리
hello **누락 데이터 정리** 모듈 이름을 제안지 않습니다: 사용자 지정 될 수 있는 방법으로 누락 된 데이터를 정리 합니다. 이 모듈을 다음과 같습니다.

![누락 데이터 정리](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

여기에서 선택한 이유 tooreplace 0 인 누락 된 모든 값. Hello 드롭다운 목록 hello 모듈에서 확인 하 여 볼 수 있는 다른 옵션을도 있습니다.

#### <a name="feature-engineering-on-hello-data"></a>Hello 데이터에서 기능 엔지니어링
큰 데이터 집합의 범주 기능 중 일부에는 수백 만개의 고유 값이 있을 수 있습니다. 원 핫(one-hot) 인코딩과 같은 미숙한 방법을 사용하여 이러한 고차원 범주 기능을 나타내는 것은 전적으로 불가능합니다. 이 연습에서는 기본 제공 Azure 기계 학습 모듈 toogenerate를 사용 하 여 toouse 개수 기능 이러한 차원 범주 변수의 표현을 압축 하는 방법을 보여 줍니다. hello 최종 결과 더 작은 모델 크기, 더 빠른 학습 시간 및 toousing 매우 비교할 수 있는 성능 메트릭을 기타 기술 합니다.

##### <a name="building-counting-transforms"></a>개수 변환 작성
toobuild 수 기능을 사용 하 여 hello **변환 계산 빌드** Azure 기계 학습에서 사용할 수 있는 모듈입니다. hello 모듈은 다음과 같습니다.

![개수 변환 모듈 빌드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![개수 변환 모듈 작성](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> Hello에 **열 개수를 계산할** 상자에서 원하는 म tooperform 계산 열에서는 입력 합니다. 이미 설명한 대로 이러한 열은 일반적으로 고차원 범주의 열입니다. Hello 시작 부분에 설명한 대로 해당 hello Criteo 데이터 집합에 범주 열이 26: Col15 tooCol40에서 합니다. 모든 속성에 수는 여기에서 (쉼표로 구분 하 여 표시 된 것 처럼 15 too40)에서 해당 인덱스를 제공 합니다.
> 

toouse hello 모듈에 hello MapReduce 모드 (큰 데이터 집합에 대 한 적절 한), (hello 기능 탐색을 위해 사용 되는 이러한 용도로 다시 사용할 수 있습니다) tooan HDInsight Hadoop 클러스터 및 해당 자격 증명에 액세스할 필요 있습니다. 이전 그림 hello 모양을 (replace hello 값에 직접 사용 사례에 대 한 관련 내용과 제공) 채워진 값을 hello를 보여 줍니다.

![모듈 매개 변수](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

Tooenter hello blob를 입력 하는 방법을 알아보겠습니다 위 hello 그림에 위치 합니다. 이 위치에 hello 데이터가 개수 테이블을 기반으로 구축 하기 위해 예약 되어 있습니다.

이 모듈에서 실행을 완료 한 후 수 저장에 대 한 hello 변환을 나중 hello 모듈을 마우스 오른쪽 단추로 클릭 하 고 hello를 선택 하 여 **변환으로 저장** 옵션:

!["변환으로 저장" 옵션](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

위에 표시 된 가이드의 실험 아키텍처에서 hello 데이터 집합 "ytransform2" count 변환을 저장 tooa 정확 하 게 해당 합니다. 사용 되는 해당 hello 판독기 가정이 실험 hello 나머지 인는 **변환 계산 빌드** 모듈에 일부 데이터 toogenerate 횟수 및 있습니다 hello 학습에서 해당 개수 toogenerate 수 기능을 사용 하 고 테스트 데이터 집합입니다.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>어떤 기능 tooinclude hello 학습의 일부로 계산 및 테스트 데이터 집합 선택
Hello 사용자가 기차에서 어떤 기능 tooinclude를 선택할 수 있으며 테스트 hello를 사용 하 여 데이터 집합 준비 변형할 수 있으면, **개수 테이블 매개 변수 수정** 모듈입니다. 완성된 모양을 보여 주기 위해 이 모듈을 여기 표시해 놓기는 했지만 실험을 단순하게 하려면 이 모듈을 실제로 사용하지 마세요.

![개수 테이블 매개 변수를 수정합니다.](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

이 예에서 볼 수 있듯이 선택한 toouse 정당한 hello 로그 확률 및 tooignore hello 열 백오프입니다. Hello 휴지통 임계값, 다듬기에 대 한 이전 의사 예제 tooadd 개수 등의 매개 변수도 설정할 수 있습니다 및 여부 toouse 모든 라플라스 노이즈 여부. 이러한 모든 고급 기능 아니며 toobe hello 기본 값 새로운 toothis 유형의 기능 생성이 사용자를 위한 좋은 출발점으로 언급 합니다.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Hello 수 기능을 생성 하기 전에 데이터 변환
이제 우리의 기차 변형 하는 방법에 대 한 중요 한 내용에 집중 하 고 데이터 사전 tooactually 생성 개수 기능 테스트. 두 개의 **R 스크립트 실행** hello count tooour 데이터 변환 적용 하기 전에 사용 되는 모듈입니다.

![R 스크립트 모듈 실행](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Hello 첫 번째 R 스크립트는 다음과 같습니다.

![첫 번째 R 스크립트](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

이 R 스크립트에서 이름을 바꾸지 우리의 열 toonames "Col1" 너무 "Col40"입니다. Hello count 변환에서는이 형식의 이름을 때문입니다.

두 번째 R 스크립트 hello 양수 및 음수 클래스 간의 hello 배포 고려해 (각각 클래스 1과 0) 샘플링 hello 음수 클래스에 의해 합니다. hello R 스크립트 방법에서는 여기 toodo이:

![두 번째 R 스크립트](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

이 간단한 R 스크립트를 사용 하 여 "pos\_neg\_비율" tooset hello 양을 hello 양수 및 음수 클래스 hello 간의 균형입니다. 이 과정이 중요 toodo hello 클래스 분포는 여기서 분류 문제에 대 한 성능상의 이점을 일반적으로 클래스 불균형 향상 때문에 왜곡 (회수 경우에 있는지 3.3% 양의 클래스와 96.7% 음수 클래스).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Hello 개수 변환을 데이터에 적용
마지막으로, 우리 צ ְ ײ hello **변환 적용** 모듈 tooapply 우리의 학습에는 개수 변환을 hello 및 테스트 데이터 집합입니다. 이 모듈 학습 또는 테스트 데이터 집합의 다른 입력 hello 하나의 입력과 hello 저장 hello count 변형 됩니다 하 고 개수 기능을 사용 하 여 데이터를 반환 합니다. 다음과 같이 표시됩니다.

![변환 모듈 적용](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>hello 개수 기능 모양을 발췌 한 구문
것이 좋습니다 toosee hello 개수 기능에는 어떤 경우에는 유사 합니다. 다음은 이 기능이 보이는 부분을 발췌한 것입니다.

![개수 기능](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

발췌 한이 म 입증 계산 म 있는 hello 열에 대 한 म hello 개수를 가져올 추가 tooany 관련 backoffs 확률 로그인 합니다.

이제는 준비 toobuild 이러한 변환 된 데이터 집합을 사용 하는 Azure 기계 학습 모델입니다. Hello 다음 섹션에서는 수 수행 방법을 보여 줍니다.

### <a name="step3"></a>3 단계: 작성, 학습 및 hello 모델 점수 매기기

#### <a name="choice-of-learner"></a>학습자의 선택
먼저 toochoose는 학습자입니다. 이 학습자로 진행 중인 toouse 2 클래스 승격 된 의사 결정 트리는입니다. 다음은이 학습자에 대 한 hello 기본 옵션입니다.

![2 클래스 향상된 의사 결정 트리 매개 변수](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

이 실험에 대 한 진행 중인 toochoose hello 기본 값은 했습니다. 해당 hello 기본값은 일반적으로 의미 있는 성능에 좋은 방법 tooget 빠른 기준을 기록한 합니다. 스윕 매개 변수 있는 tooonce를 선택 하는 경우 초기 하 여 성능을 개선할 수 있습니다.

#### <a name="train-hello-model"></a>Hello 모델 학습
학습용으로 간단히 **모델 학습** 모듈을 호출합니다. 두 입력 tooit hello는 hello 2 클래스 승격 된 의사 결정 트리 학습자 및 우리의 학습 데이터 집합입니다. 다음과 같습니다.

![모델 학습 모듈](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Hello 모델 점수 매기기
준비 하는 학습된 된 모델 상태, tooscore hello에 테스트 데이터 집합 및 tooevaluate 성능을 합니다. Hello를 사용 하 여 수행 **모델 점수 매기기** hello 그림에서는 아래에 표시 된 모듈은 **모델 평가** 모듈:

![모델 점수 매기기 모듈](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>4 단계: hello 모델 평가
마지막으로, tooanalyze 모델 성능을 하겠습니다. 일반적으로 두 가지 클래스 (이진) 분류 문제에 대 한 유용한 척도 hello AUC입니다. toovisualize이 hello 후크 했습니다 **모델 점수 매기기** 모듈 tooan **모델 평가** 이 대 한 모듈입니다. 클릭 하면 **시각화** hello에 **모델 평가** 모듈 하나를 따르는 hello와 같은 그래픽을 생성 합니다.

![Evaluate module BDT 모델](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

이진 (또는 두 개의 클래스)에서 분류 문제를 예측 정확도 측정 한 값 영역에서 곡선 (AUC) hello 됩니다. 다음은 테스트 데이터 집합에서 이 모델을 사용한 결과입니다. tooget hello이를 마우스 오른쪽 단추로 클릭 hello 출력 포트 **모델 평가** 모듈 차례로 **시각화**합니다.

![Evaluate Model 모듈 시각화](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>5 단계: 웹 서비스로 hello 모델 게시
hello 기능 toopublish 간단 하 게 최소화 하 여 웹 서비스로 Azure 기계 학습 모델은 광범위 하 게 제공 하기 위한 중요 한 기능입니다. 작업이 완료 되 면 누구나 호출 toohello 웹 서비스는 필요한 예측을 하 고 hello 웹 서비스는 hello 모델 tooreturn 이러한 예상 입력된 데이터를 만들 수 있습니다.

toodo이를 먼저 예제의 학습 된 모델 학습 된 모델 개체와 저장 합니다. Hello를 마우스 오른쪽 단추로 클릭 하 여 이렇게 **모델 학습** 모듈과 hello를 사용 하 여 **학습 된 모델로 저장** 옵션입니다.

다음으로, toocreate 입력 및 출력 해야 웹 서비스에 대 한 포트:

* 입력된 포트에 대 한 예측 해야 하는 hello 데이터로 형성 동일 hello의 데이터를 받아
* 출력 포트 hello 점수가 매겨진 레이블 및 hello 관련 된 확률을 반환합니다.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Hello 입력된 포트에 대 한 데이터 행을 몇 개를 선택 합니다.
편리한 toouse는는 **SQL 변환 적용** hello로 모듈 tooselect 정당한 10 행 tooserve 입력 포트 데이터를 필터링 합니다. 여기에 표시 된 hello SQL 쿼리를 사용 하 여 입력된 포트에 대 한 데이터의 이러한 행을 선택 합니다.

![입력 포트 데이터](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>웹 서비스
이제 toorun toopublish 사용된 될 수 있는 작은 실험 웹 서비스를 준비 합니다.

#### <a name="generate-input-data-for-webservice"></a>웹 서비스에 대한 입력 데이터 생성
0 번째 단계로, 있으므로 hello 개수 테이블 크기가 클에서는 테스트 데이터의 하면 몇 줄 되 고 개수 기능에서 데이터 출력을 생성 합니다. 이 통해 웹 서비스에 대 한 hello 입력된 데이터 형식으로 사용할 수 있습니다. 다음과 같습니다.

![BDT 입력 데이터 만들기](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Hello 입력된 데이터 형식에서는 이제 사용 hello hello의 출력 **Count Featurizer** 모듈입니다. 이 실행이 완료 될 실험해 보고 되 면 hello에서 hello 출력을 저장 **Count Featurizer** 데이터 집합으로 모듈입니다. 이 데이터 집합은 hello hello 웹 서비스에서 입력된 데이터에 사용 됩니다.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>웹 서비스 게시를 위한 실험 점수 매기기
먼저 구조를 확인합니다. hello 필수 구조는 한 **모델 점수 매기기** 우리의 학습 된 모델 개체와 hello를 사용 하 여 hello 이전 단계에서 생성 우리는 입력된 데이터의 몇 줄을 허용 하는 모듈 **Count Featurizer** 모듈입니다. "Dataset에서 열 선택" tooproject hello 점수가 매겨진 레이블 및 hello 점수 확률을 사용합니다.

![데이터 집합의 열 선택](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Hello 어떻게 확인 **데이터 집합의 열 선택** 모듈 '필터링 하는 데' 데이터는 데이터 집합에서 사용할 수 있습니다. Hello 내용 표시:

![데이터 집합 모듈에서 열 선택 hello를 사용 하 여 필터링](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

tooget hello 파란색 입력 및 출력 포트를 클릭 하면 **webservice 준비** 오른쪽 hello 아래에 있습니다. 이 실험을 실행할 수도 있습니다 toopublish hello 웹 서비스: hello 클릭 **웹 서비스 게시** 아이콘 hello 맨 아래 오른쪽, 표시 된 여기에서:

![PUBLISH WEB SERVICE](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Hello 웹 서비스를 게시 하면 리디렉션된 tooa 페이지가 따라서 구했습니다.

![웹 서비스 대시보드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

웹 서비스에 대 한 두 개의 링크가 hello 왼쪽에 표시 합니다.

* hello **요청/응답** 서비스 (또는 RR) 단일 예측에 대 한 것 이며이 워크샵에 사용 했습니다.
* hello **일괄 처리 실행** 서비스 (BES) 일괄 처리 예측에 사용 되 고 hello 사용 되는 입력된 데이터 toomake 예측 Azure Blob 저장소에 상주 하는 필요 합니다.

Hello 링크를 클릭 하면 **요청/응답** tooa는 페이지를 제공 하는 C#, python 및 오른쪽에서 코드를 미리 고정 이 코드 toohello 웹 서비스 호출 하기 위한 편리 하 게 사용할 수 있습니다. Note 해당 hello이이 페이지의 API 키 toobe 인증에 사용 해야 합니다.

것이 편리한 toocopy hello IPython 전자 필기장의 tooa 새로운 셀을 통해이 python 코드입니다.

여기 hello 올바른 API 키 python 코드 세그먼트를 표시합니다.

![Python 코드](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Note 우리의 webservices API 키와 hello 기본 API 키를 교체 했습니다. 클릭 하면 **실행** 이 셀에 IPython 노트북 생성 응답 다음 hello:

![IPython 응답](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Hello에 대 한 예제에 대 한 hello python 스크립트의 hello JSON 프레임 워크) (에 요청한 테스트 두 보면, 구했습니다 다시 hello 형태로 답변 "점수가 매겨진 레이블, 점수가 매겨진 확률"입니다. 참고는이 경우 선택한 이유 hello 기본값 hello 미리 준비 된 코드 (0의 모든 숫자 열과 모든 범주 열에 대 한 "value" hello 문자열)를 제공 합니다.

이것으로 마칩니다 우리의 종단 간 연습 보여 주는 방법을 Azure 기계 학습을 사용 하 여 toohandle 대규모 데이터 집합입니다. 우리는 테라바이트 임 데이터의 시작, 예측 모델을 생성 및 hello 클라우드에서 웹 서비스로 배포 합니다.

