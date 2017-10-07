---
title: "하이브 쿼리를 사용 하 여 Hadoop 클러스터에는 데이터에 대 한 aaaCreate 기능 | Microsoft Docs"
description: "Azure HDInsight Hadoop 클러스터에 저장된 데이터의 기능을 생성하는 Hive 쿼리의 예입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Hive 쿼리를 사용하여 Hadoop 클러스터의 데이터에 대한 기능 만들기
이 문서에서는 toocreate 기능 데이터에 대 한 하이브 쿼리를 사용 하 여 Azure HDInsight Hadoop 클러스터에 저장 하는 방법을 보여 줍니다. 포함 된 하이브 사용자 정의 함수 (Udf)를 사용 하는 이러한 하이브 쿼리를 hello 스크립트 제공 됩니다.

hello 필요한 작업 toocreate 기능이 메모리를 많이 사용 될 수 있습니다. 하이브 쿼리 성능을 hello 이러한 경우에 특히 중요 한 되며 특정 매개 변수를 조정 하 여 향상 될 수 있습니다. 이러한 매개 변수 중 hello 튜닝 hello 마지막 섹션에서 설명 합니다.

표시 되는 hello 쿼리의 예는 특정 toohello [NYC 택시 여행 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/) 시나리오에도 제공 되어 [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts)합니다. 이러한 쿼리 이미 지정 된 데이터 스키마 않으며 제출 준비 toobe toorun 합니다. Hello 마지막 섹션에서 하이브 쿼리 hello 성능을 향상 시킬 수 있도록 사용자가 튜닝할 수 있는 매개 변수 에서도 설명 합니다.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

이 **메뉴** tootopics toocreate 다양 한 환경에서 데이터에 대 한 기능 하는 방법을 설명 하는 링크입니다. 이 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.

* Azure 저장소 계정을 만들었습니다. 지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.
* Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다.  지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.
* hello 데이터가 Azure HDInsight Hadoop 클러스터에서 업로드 된 tooHive 테이블 되었습니다. 그렇지 않은 경우 따르십시오 [데이터 tooHive 테이블을 만들고 부하](machine-learning-data-science-move-hive-tables.md) tooupload 데이터 tooHive 먼저 테이블입니다.
* 원격 액세스 toohello 클러스터를 사용할 수 있습니다. 지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.

## <a name="hive-featureengineering"></a>기능 생성
이 섹션에 있는 기능 수 생성 하이브 쿼리를 사용 하 여 hello 방법의 몇 가지 예가 설명 되어 있습니다. 추가 기능을 생성 한 후 toohello 기존 테이블 열으로 추가 하거나 hello 추가 기능 및 hello 원래 테이블과 조인할 수 있는 기본 키를 사용 하 여 새 테이블을 만듭니다. 에 소개 된 hello 예제는 다음과 같습니다.

1. [빈도 기반 기능 생성](#hive-frequencyfeature)
2. [이진 분류에서 범주 변수의 위험](#hive-riskfeature)
3. [날짜/시간 필드에서 기능 추출](#hive-datefeatures)
4. [텍스트 필드에서 기능 추출](#hive-textfeatures)
5. [GPS 좌표 사이의 거리 계산](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>빈도 기반 기능 생성
것이 유용한 toocalculate hello 주파수 범주 변수의 hello 수준 또는 수준 여러 범주 변수에서의 특정 조합은의 hello 빈도. 사용자 이러한 주파수 스크립트 toocalculate 다음 hello를 사용할 수 있습니다.

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>이진 분류에서 범주 변수의 위험
이진 분류에 hello 모델에만 사용 되 고 숫자 기능을 수행 하는 경우 숫자 기능으로 tooconvert 숫자가 아닌 범주 변수가 필요 합니다. 그러려면 숫자가 아닌 각 수준을 숫자 위험으로 바꾸면 됩니다. 이 섹션에서는 범주 변수 hello 위험 값 (로그 확률)을 계산 하는 일부 제네릭 하이브 쿼리를 보여줍니다.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

이 예에서는 변수 `smooth_param1` 및 `smooth_param2` hello 데이터에서 계산 된 toosmooth hello 위험 값을 설정 합니다. 위험 범위는 -Inf~Inf입니다. 위험 > 0 hello 대상으로 하는 같은 too1 hello 확률 0.5 보다 큰 임을 나타냅니다.

Hello 위험 테이블이 계산 된 후 hello 위험 테이블과 조인 하 여 위험 tooa 표를 지정할 수 있습니다. hello 하이브 조인 쿼리는 이전 섹션에서 제공 되었습니다.

### <a name="hive-datefeatures"></a>날짜/시간 필드에서 기능 추출
Hive는 날짜/시간 필드를 처리할 수 있는 UDF가 함께 제공됩니다. 하이브에, hello 기본 날짜/시간 형식은 ' yyyy-월-일 00시: 00' ('1970-01-01 12시 21분: 32' 예를 들어). 이 섹션에서는 hello 일, 월, 날짜/시간 필드에서 hello 월을 추출 하는 예제 및 hello 기본 형식 tooa datetime 문자열 기본 형식 이외의 형식으로 날짜/시간 문자열을 변환 하는 다른 예를 보여줍니다.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

이 하이브 쿼리 가정 해당 hello *&#60; datetime 필드 >* hello 기본 날짜/시간 형식으로 되어 있습니다.

날짜/시간 필드가 hello 기본 형식에 없으면, 해야 tooconvert hello datetime 필드 Unix 타임 스탬프에 먼저, 다음 convert hello Unix 시간 스탬프 tooa datetime 문자열에 있고 hello 기본 형식입니다. Hello 날짜/시간 형식 기본 이면 hello 포함 된 datetime Udf tooextract 기능 적용할 수 있습니다.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

이 쿼리에서 경우 hello *&#60; datetime 필드 >* 같은 hello 패턴이 *03/26/2015 12시 04분: 39*, hello *' &#60; hello 날짜/시간 필드의 패턴 >'* 이어야 합니다 `'MM/dd/yyyy HH:mm:ss'`. tootest 사용자가 실행할 수

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

hello *hivesampletable* 이 쿼리의 미리 설치 된 모든 Azure HDInsight Hadoop 클러스터에서 기본적으로 때 도착 hello 클러스터 프로 비전 됩니다.

### <a name="hive-textfeatures"></a>텍스트 필드에서 기능 추출
Hello Hive 테이블에 공백으로 구분 되는 단어의 문자열이 포함 된 텍스트 필드가 hello 다음 쿼리를 추출 hello 길이 hello 문자열 및 hello 문자열에서 단어 hello 수 있습니다.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>GPS 좌표 사이의 거리 계산
이 섹션에 지정 된 hello 쿼리 직접 적용 된 toohello NYC 택시 여행 데이터 될 수 있습니다. hello이이 쿼리는 tooshow 어떻게 tooapply 포함 된 하이브 toogenerate 기능의 수치 연산 함수입니다.

hello이 쿼리에 사용 되는 필드는 명명 된 픽업 및 dropoff 위치 hello GPS 좌표 *픽업\_경도*, *픽업\_위도*,  *dropoff\_경도*, 및 *dropoff\_위도*합니다. hello 픽업 및 dropoff 좌표 간의 hello 직접 거리를 계산 하는 hello 쿼리가 됩니다.

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

hello에 두 GPS 좌표 사이의 hello 거리를 계산 하는 hello 수식이 있습니다 <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">이동 유형 스크립트</a> Peter Lapisu가 만든 사이트입니다. 그의 javascript 함수 hello `toRad()` 단지 *lat_or_lon*pi/180 *도 tooradians로 변환 하는 합니다. 여기에서 *lat_or_lon* hello 위도 또는 경도의 합니다. 하이브 hello 함수를 제공 하지 않는 `atan2`, hello 함수를 제공 하지만 `atan`, hello `atan2` 함수를 구현 하 여 `atan` 함수에 제공 된 hello 정의 사용 하는 하이브 쿼리 위에 hello에 <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>합니다.

![작업 영역 만들기](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Hello에 포함 된 Udf 있습니다 하이브의 전체 목록은 **기본 제공 함수** hello 섹션 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>고급 항목: 하이브 매개 변수 조정 tooImprove 쿼리 속도
hello 하이브 클러스터의 설정을 맞지 않을 hello 하이브 쿼리 및 처리 하는 hello 쿼리 hello 데이터에 대 한 기본 매개 변수입니다. 이 섹션에서는 hello 하이브 쿼리 성능을 개선 하는 사용자가 조정할 수 있는 몇 가지 매개에 설명 합니다. 사용자는 hello 쿼리 데이터를 처리 하기 전에 쿼리를 튜닝 tooadd hello 매개 변수가 필요 합니다.

1. **Java의 힙 공간이**: 큰 데이터 집합 조인 또는 긴 레코드를 처리 하는 쿼리에 대해 **힙 공간이 부족** hello에서 발생 하는 일반적인 오류 중 하나입니다. 이 매개 변수를 설정 하 여 튜닝할 수 *mapreduce.map.java.opts* 및 *mapreduce.task.io.sort.mb* toodesired 값입니다. 다음은 예제입니다.
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    이 매개 변수 4GB 메모리 tooJava 힙 공간을 할당 하 고 또한 하면 정렬 보다 효율적으로 더 많은 메모리를 할당 합니다. 이러한 할당이 포함 된 것이 좋습니다 tooplay는 하는 경우에 포함 된 작업 실패 오류 관련된 tooheap 공간입니다.

1. **DFS 블록 크기** :이 매개 변수는 hello hello 파일 시스템 저장소는 데이터의 가장 작은 단위를 설정 합니다. 예를 들어 hello DFS 블록 크기는 128mb로, 않으면 크기의 모든 데이터 미만 및 too128MB 드릴업은 저장 하는 동안 추가 블록 할당 128MB 보다 큰 데이터는 단일 블록에서입니다. Hello 이름 노드에서 tooprocess 많은 더 많은 요청 toofind hello 관련 블록 toohello 파일 관련 되어 있으므로 Hadoop에서 큰 오버 헤드가 발생 매우 작은 블록 크기를 선택 합니다. 기가바이트 단위(또는 그 이상) 데이터를 처리할 때 권장하는 설정은 다음과 같습니다.
   
        set dfs.block.size=128m;
2. **하이브 join 연산의 최적화** : hello 맵/감소 프레임 워크에서 조인 작업 hello에서 일반적으로 수행 하는 동안 경우에 따라 단계를 줄이려면, 조인 hello 매핑 단계 ("mapjoins" 라고도 함)에 예약 하 여 엄청난 향상이 이루어질 수 있습니다. toodirect 하이브 toodo이 가능 하다 면 설정할 수 있습니다.
   
        set hive.auto.convert.join=true;
3. **매퍼 tooHive hello 개수를 지정 하면** : 동안 Hadoop hello 사용자 tooset hello의 허용 이경소켓, 매퍼 hello 수는 대개 hello 사용자가 설정할 수 없습니다. 이 숫자에는 컨트롤의 어느 정도 허용 하는 트릭은 toochoose hello Hadoop 변수 *mapred.min.split.size* 및 *mapred.max.split.size* 각 맵의 hello 크기와 작업에 의해 결정 됩니다.
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    기본값을 일반적으로 hello *mapred.min.split.size* 은 0으로의 *mapred.max.split.size* 은 **Long.MAX** 요구 사항과 *dfs.block.size* 는 64MB입니다. 볼 수 있듯이, 주어진된 hello 데이터 크기 "설정" 하 여 이러한 매개 변수를 튜닝을 통해 tootune hello 수가 매퍼 사용 있습니다.
4. 아래에 Hive 성능을 최적화하는 **고급 옵션** 몇 가지가 추가로 설명되어 있습니다. 이러한 tooset hello 할당 된 메모리 toomap를 허용 하 고 작업을 줄여 및 작업은 성능 조정 하는 데 유용할 수 있습니다. 명심 하십시오 해당 hello *mapreduce.reduce.memory.mb* hello Hadoop 클러스터의 각 작업자 노드의 hello 실제 메모리 크기 보다 클 수 없습니다.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

