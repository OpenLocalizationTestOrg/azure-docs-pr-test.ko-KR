---
title: "Azure HDInsight의 Hive aaaOptimize 쿼리 | Microsoft Docs"
description: "어떻게 toooptimize 프로그램 하이브 쿼리를 HDInsight의 Hadoop에 대 한 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Azure HDInsight에서 Hive 쿼리를 최적화

기본적으로 Hadoop 클러스터는 성능을 위해 최적화되지 않습니다. 이 문서에서는 tooyour 쿼리를 적용할 수 있는 하 몇 가지 가장 일반적인 하이브 성능 최적화 방법에 설명 합니다.

## <a name="scale-out-worker-nodes"></a>작업자 노드 확장

Hello 클러스터의 작업자 노드 수를 늘리면 병렬로 실행 하는 자세한 매퍼 및 이경소켓 toobe를 활용할 수 있습니다. HDInsight에서 크기를 확장할 수 있는 두 가지 방법이 있습니다.

* Hello 프로 비전 시 hello hello Azure 포털, Azure PowerShell 또는 플랫폼 간 명령줄 인터페이스를 사용 하 여 작업자 노드 수를 지정할 수 있습니다.  자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요. hello 다음 스크린샷은 hello 작업자 노드 구성 hello Azure 포털에서:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Hello 실행 시간에 수평 확장할 수 있습니다는 클러스터 하나를 다시 만들지 않고:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

HDInsight에서 지 원하는 hello 서로 다른 가상 컴퓨터에 대 한 자세한 내용은 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.

## <a name="enable-tez"></a>TCP 사용

[Apache Tez](http://hortonworks.com/hadoop/tez/) 는 대체 실행 엔진 toohello MapReduce 엔진:

![tez_1][image-hdi-optimize-hive-tez_1]

다음의 이유로 Tez가 훨씬 빠릅니다.

* **비순환 그래프 지시 (DAG) hello MapReduce 엔진에서 단일 작업으로 실행**합니다. hello DAG 이경소켓 집합이 하나 옵니다 매퍼 toobe 각 집합이 필요 합니다. 이렇게 하면 각 하이브 쿼리에 대 한 분리 된 여러 MapReduce 작업 toobe 됩니다. Tez는 이러한 제약 조건이 없으며 복잡한 DAG를 작업 시작 오버 헤드를 최소화하는 하나의 작업으로 처리할 수 있습니다.
* **불필요한 쓰기를 방지**합니다. Hello에 대 한 생성 되 고 toomultiple 작업 인해 hello MapReduce 엔진, 각 작업의 hello 출력에서에서 동일한 하이브 쿼리 tooHDFS 중간 데이터에 기록 됩니다. Tez 각 하이브 쿼리에 대 한 작업의 수를 최소화 되므로 수 tooavoid 불필요 한 쓰기입니다.
* **시작 지연을 최소화**합니다. Tez은 toostart 및 전체 또한 개선 최적화 필요한 매퍼 hello 수를 줄여 보다 나은 수 toominimize 시작 지연 됩니다.
* **컨테이너를 다시 사용**합니다. 경우 언제 든 지 가능한 Tez 수 tooreuse 컨테이너 tooensure 해당 대기 시간 때문에 컨테이너를 toostarting이 줄어듭니다.
* **연속 최적화 기술**. 일반적으로 최적화는 컴파일 단계 중에 수행됩니다. Hello 입력에 대 한 자세한 정보를 사용할 수 있지만 런타임에 더 나은 최적화를 허용 합니다. Tez는 hello 런타임 단계로 추가로 toooptimize hello 계획 수 있는 연속 최적화 기술을 사용 합니다.

이러한 개념에 대한 자세한 내용은 [Apache Tez](http://hortonworks.com/hadoop/tez/)를 참조하세요.

하이브 쿼리 Tez 아래 hello 설정을 사용 하 여 hello 쿼리를 접두사로 사용을 만들 수 있습니다.

    set hive.execution.engine=tez;

Linux 기반 HDInsight 클러스터는 Tez를 기본적으로 사용합니다.


## <a name="hive-partitioning"></a>Hive 분할

I/O 작업이 하이브 쿼리를 실행 하기 위한 hello 주요 성능 병목 현상입니다. hello toobe 해야 하는 데이터 양을 읽을 수 있습니다 하는 경우에 hello 성능을 향상 시킬 수 감소 합니다. 기본적으로 Hive 쿼리는 전체 Hive 테이블을 검사합니다. 테이블 검사와 같은 쿼리에 적합합니다. 그러나 tooscan 적은 양의 데이터 (예: 필터링 된 쿼리) 하기만 하는 쿼리의 경우이 동작에서는 불필요 한 오버 헤드 하이브 분할 Hive 테이블에 하이브 쿼리 tooaccess만 hello 필요한 만큼의 데이터를 허용합니다.

하이브 분할 hello 원시 데이터를 다시 구성 하면 각 파티션에 자체 directory-hello 파티션 hello 사용자가 정의 되어 있는 새 디렉터리에 의해 구현 됩니다. hello 다음 다이어그램에서는 hello 열별로 Hive 테이블 분할 *연도*합니다. 각 연도로 새 디렉터리가 생성됩니다.

![분할][image-hdi-optimize-hive-partitioning_1]

일부 분할 고려 사항:

* **언더 분할 안 함** - 몇 개의 값만 있는 열에서 분할하면 적은 파티션을 발생할 수 있습니다. 예를 들어 gender에 분할만 (male 및 female)를 생성 하는 두 개의 파티션을 toobe, 따라서 절반 최대 여만 hello 대기 시간을 줄일.
* **파티션을 통해 하지 않는** -hello 다른 한편으로 파티션이 여러 개 지정 하면 고유 값 (예를 들어 사용자 id)으로 열에 파티션 만들기. 파티션을 통해 하면 많은 스트레스 hello 클러스터 namenode toohandle hello 많은 수의 디렉터리 이름이 됩니다.
* **데이터 오차 방지** -모든 파티션의 크기가 고르도록 현명하게 분할 키를 선택합니다. 예로 분할을 *상태* hello 캘리포니아 toobe 레코드 수가 거의 30 발생할 수 있습니다는 버몬트 채우기의 toohello 차이 때문에 x입니다.

파티션 테이블 toocreate hello를 사용 하 여 *분할 하 여* 절:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Hello 분할 된 테이블을 만든 후 정적 분할 또는 동적 분할 만들 수 있습니다.

* **정적 분할** 하이브 파티션을 hello 디렉터리 위치에 따라 수동으로 요청 하 고 의미 hello에 이미 분할 된 데이터가 있는 경우 해당 디렉터리입니다. 다음 코드 조각 hello 예입니다.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **동적 분할** 의미 하이브 toocreate 파티션이 자동으로 드립니다. Hello 준비 테이블에서에서 테이블을 분할 하는 hello를 이미 만들었습니다 toodo 필요한 것 이므로 데이터 toohello 분할 된 테이블에 삽입 합니다.
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

자세한 내용은 [분할된 테이블](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)을 참조하세요.

## <a name="use-hello-orcfile-format"></a>Hello ORCFile 형식을 사용 하 여
Hive는 다양한 파일 형식을 지원합니다. 예:

* **텍스트**: hello 기본 파일 형식 이므로 대부분의 시나리오와 작동 합니다.
* **Avro**: 상호 운용성 시나리오에 대해 제대로 작동합니다.
* **ORC/Parquet**: 성능에 가장 적합합니다.

ORC (최적화 된 행 칼럼 형식) 형식은 매우 효율적으로 toostore 하이브 데이터입니다. 비교 tooother 형식, ORC hello 장점 뒤에 있습니다.

* DateTime 및 복잡 및 반구조화된 형식을 포함하는 복합 형식 지원
* too70% 압축을
* 행을 건너뛸 수 있는 10,000행마다 인덱스
* 런타임 실행 시 현저하게 감소

tooenable ORC 형식으로 먼저 테이블을 만들면 hello 절과 함께 *ORC로 저장*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

다음으로 hello 준비 테이블에서에서 데이터 toohello ORC 테이블을 삽입 합니다. 예:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

자세한 내용은 hello ORC 형식에 [여기](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)합니다.

## <a name="vectorization"></a>벡터화

벡터화 허용 하이브 tooprocess 1024 일괄 처리 행을 한 번에 하나의 행을 처리 하는 대신 함께 합니다. 더 적은 내부 코드 toorun 해야 하기 때문에 간단한 작업은 더 빠르게 수행 의미 합니다.

tooenable 벡터화 접두사로 설정에 따라 hello를 사용 하 여 하이브 쿼리:

    set hive.vectorized.execution.enabled = true;

자세한 내용은 [벡터화된 쿼리 실행](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)을 참조하세요.

## <a name="other-optimization-methods"></a>다른 최적화 방법
예를 들어 다음은 고려할 수 있는 추가 최적화 방법입니다.

* **버킷 팅 하이브:** 대량의 데이터 toooptimize 쿼리 성능 toocluster 또는 세그먼트를 허용 하는 기술입니다.
* **조인 최적화:** 하이브의 쿼리 실행 tooimprove 계획의 최적화 조인 효율성 hello 및 사용자 힌트에 대 한 hello 필요한 줄어듭니다. 자세한 내용은 [조인 최적화](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)를 참조하세요.
* **리듀서 증가**

## <a name="next-steps"></a>다음 단계
이 기사에서는 몇가지 일반적인 하이브 쿼리 최적화 방법을 배웠습니다. 더 toolearn hello 다음 문서를 참조:

* [HDInsight에서 Apache Hive 사용](hdinsight-use-hive.md)
* [HDInsight의 Hive를 사용하여 비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)
* [HDInsight에서 Hive를 사용하여 Twitter 데이터 분석](hdinsight-analyze-twitter-data.md)
* [HDInsight에서 Hadoop에서 하이브 쿼리 콘솔 hello를 사용 하 여 센서 데이터 분석](hdinsight-hive-analyze-sensor-data.md)
* [하이브를 사용 하 여 웹 사이트에서 HDInsight tooanalyze 로그](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
