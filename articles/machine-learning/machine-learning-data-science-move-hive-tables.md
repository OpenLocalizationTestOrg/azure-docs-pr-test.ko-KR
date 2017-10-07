---
title: "aaaCreate 하이브 테이블 및 Azure Blob 저장소에서 데이터를 로드 합니다. | Microsoft Docs"
description: "Hive 테이블을 만들고 blob toohive 테이블의 데이터를 로드 합니다."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Hive 테이블을 만들고 Azure Blob Storage에서 데이터 로드
이 토픽에서는 Hive 테이블을 만들고 Azure blob 저장소의 데이터를 로드하는 일반 Hive 쿼리를 보여 줍니다. Hello에 최적화 된 행 열 형식 (ORC) 서식 tooimprove 쿼리 성능을 사용 하 여 및 Hive 테이블 분할에 지침이 제공 됩니다.

이 **메뉴** tootopics hello 데이터 저장 끌어다 하는 동안 처리할 수 있는 대상 환경으로 데이터 tooingest 팀 데이터 과학 프로세스 (TDSP) hello 하는 방법을 설명 하는 링크입니다.

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.

* Azure 저장소 계정을 만들었습니다. 지침이 필요한 경우 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.
* Hello HDInsight 서비스를 사용 하 여 사용자 지정 된 Hadoop 클러스터 프로 비전 합니다.  지침이 필요한 경우 [고급 분석을 위한 Azure HDInsight Hadoop 클러스터 사용자 지정](machine-learning-data-science-customize-hadoop-cluster.md)을 참조하세요.
* 사용 가능한 원격 액세스 toohello 클러스터 로그인 하 고 hello Hadoop 명령줄 콘솔을 열립니다. 지침이 필요한 경우 참조 [액세스 hello Hadoop 클러스터의 헤드 노드](machine-learning-data-science-customize-hadoop-cluster.md#headnode)합니다.

## <a name="upload-data-tooazure-blob-storage"></a>데이터 tooAzure blob 저장소에 업로드
에 제공 된 hello 지침에 따라 Azure 가상 컴퓨터를 만든 경우 [고급 분석을 위해 Azure 가상 컴퓨터를 설정](machine-learning-data-science-setup-virtual-machine.md),이 스크립트 파일 되 었어야 다운로드 한 toohello *c:\\ 사용자가\\\<사용자 이름\>\\문서\\데이터 과학 스크립트* hello 가상 컴퓨터에 디렉터리입니다. 이러한 하이브 쿼리 데이터 스키마 및 hello 적절 한 필드 toobe 제출할 준비가에서 Azure blob 저장소 구성을 플러그 인만 필요 합니다.

라고 가정 Hive 테이블에 대 한 hello 데이터에는 **압축 되지 않은** 테이블 형식 및 hello 데이터 되었음을 업로드 toohello 기본 (또는 추가 tooan) hello Hadoop 클러스터에서 사용 하는 hello 저장소 계정의 컨테이너입니다.

Hello에 toopractice 하려는 경우 **NYC 택시 여행 데이터**, 해야 합니다.

* **다운로드** hello 24 [NYC 택시 여행 데이터](http://www.andresmh.com/nyctaxitrips) 파일 (12 개의 여행 파일 및 12 개의 요금 파일)
* **압축을 풉니다** .
* **업로드** 해당 toohello 기본 적절 한 컨테이너의 또는 hello hello에 설명 된 hello 프로시저에 의해 생성 된 Azure 저장소 계정 [고급 분석 프로세스 및 기술에 대 한 사용자 지정 Azure HDInsight Hadoop 클러스터 ](machine-learning-data-science-customize-hadoop-cluster.md) 항목입니다. hello 프로세스 tooupload hello.csv 파일 toohello 기본 hello 저장소 계정에 있을 수 있습니다이 [페이지](machine-learning-data-science-process-hive-walkthrough.md#upload)합니다.

## <a name="submit"></a>어떻게 toosubmit 하이브 쿼리
다음을 사용하여 Hive 쿼리를 제출할 수 있습니다.

1. [Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출](#headnode)
2. [Hello 하이브 편집기로 하이브 쿼리를 제출 합니다.](#hive-editor)
3. [Azure PowerShell 명령을 사용하여 Hive 쿼리 제출](#ps)

Hive 쿼리는 SQL과 유사하므로, SQL에 익숙한 경우 사용할 수 있습니다 hello [SQL 사용자 치트 시트에 대 한 하이브](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) 유용 합니다.

하이브 쿼리를 전송할 때 hello 화면 또는 tooa 로컬 파일에 hello 헤드 노드 또는 Azure blob tooan에서 든 관계 없이 하이브 쿼리에서 hello 출력의 hello 대상을 제어할 수 있습니다.

### <a name="headnode"></a> 1. Hadoop 클러스터 헤드 노드의 Hadoop 명령줄을 통해 Hive 쿼리 제출
Hello 하이브 쿼리가 복잡 한 하이브 편집기 또는 Azure PowerShell 스크립트를 제출 하는 것 보다 toofaster 반환 일반적으로 인해 hello Hadoop 클러스터의 헤드 노드 hello에서 직접 전송 됩니다.

Hello Hadoop 클러스터의 헤드 노드 toohello 로그인 hello Hadoop 명령줄 hello 헤드 노드의 hello 데스크톱에서 열고 명령을 입력 `cd %hive_home%\bin`합니다.

세 가지 방법으로 toosubmit 하이브 쿼리 hello Hadoop 명령줄 있습니다:

* 직접 제출
* .hql 파일을 사용하여 제출
* hello로 하이브 명령 콘솔

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Hadoop 명령줄에서 직접 Hive 쿼리를 제출합니다.
다음과 같은 명령을 실행할 수 있습니다 `hive -e "<your hive query>;` toosubmit 간단한 하이브 쿼리에서 직접에서 Hadoop 명령줄입니다. 예를 들어 여기서 hello 빨간색 상자 윤곽선 hello 명령 hello 하이브 쿼리를 전송 하 고 hello 하이브 쿼리에서 녹색 상자 윤곽선 hello 출력 hello 다음과 같습니다.

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>.hql 파일로 Hive 쿼리 제출
Hello 하이브 쿼리는 더 복잡 하 고 여러 줄에, 하이브 명령 콘솔 또는 명령줄에서 쿼리 편집은 바람직하지 않습니다. 대신은 hello Hadoop 클러스터 toosave hello에서에서 하이브 쿼리에 hello 헤드 노드의 로컬 디렉터리에 있는.hql 파일의 헤드 노드 hello toouse 텍스트 편집기입니다. Hello를 사용 하 여 hello.hql 파일에 hello 하이브 쿼리를 제출할 수 있습니다 다음 `-f` 다음과 같이 인수:

    hive -f "<path toohello .hql file>"

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Hive 쿼리의 진행 상태 화면 인쇄 숨기기**

기본적으로 Command Line Hadoop에서 하이브 쿼리 제출 hello Map/Reduce 작업의 진행률 hello에 인쇄 됩니다 화면. toosuppress hello hello Map/Reduce 작업 진행률의 인쇄 화면, 인수를 사용할 수 있습니다 `-S` (대문자로 "S")의 hello 명령 줄 다음과 같습니다.

    hive -S -f "<path toohello .hql file>"
에서도 확인할 수 있습니다.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Hive 명령 콘솔에서 Hive 쿼리를 제출합니다.
명령을 실행 하 여 먼저 hello 하이브 명령 콘솔을 입력할 수 있습니다 `hive` Hadoop 명령 줄에서 한 다음 하이브 명령 콘솔에서 하이브 쿼리를 제출 합니다. 다음은 예제입니다. 이 예제에서는 hello 두 빨간 상자 강조 hello 사용 되는 명령 tooenter 하이브 명령 콘솔 hello 및 hello 각각 하이브 명령 콘솔에서 제출 하는 하이브 쿼리 합니다. hello 녹색 상자 hello 하이브 쿼리에서 hello 출력 강조 표시합니다.

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

hello 앞의 예제는 hello 하이브 쿼리 결과 화면에 직접 출력합니다. Hello 출력 tooa hello 헤드 노드 또는 Azure blob tooan에 로컬 파일을 작성할 수도 있습니다. 그런 다음 다른 도구를 사용할 수 있습니다 toofurther 하이브 쿼리 hello 출력을 분석 합니다.

**하이브 쿼리 결과 tooa 로컬 파일을 출력 합니다.**
toooutput 하이브 쿼리 결과 tooa 로컬 디렉터리에 hello 헤드 노드를 해야 toosubmit hello 하이브 쿼리 hello Hadoop 명령줄에서에서 다음과 같습니다.

    hive -e "<hive query>" > <local path in hello head node>

다음 예제는 hello, Hive 쿼리의 hello 출력 파일에 작성 된 `hivequeryoutput.txt` 디렉터리에 `C:\apps\temp`합니다.

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**하이브 쿼리 결과 tooan Azure blob를 출력 합니다.**

Hello 하이브 쿼리 결과 tooan hello Hadoop 클러스터의 hello 기본 컨테이너 내에서 Azure blob를 출력할 수 있습니다. 이 대 한 hello 하이브 쿼리는 다음과 같습니다.

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

다음 예제는 hello, Hive 쿼리의 hello 출력 tooa blob 디렉터리 작성 된 `queryoutputdir` hello Hadoop 클러스터의 hello 기본 컨테이너 내에서. 여기에서는 tooprovide hello 디렉터리 이름이 hello blob 이름 없이 필요합니다. `wasb:///queryoutputdir/queryoutput.txt`처럼 디렉터리 이름과 blob 이름을 모두 입력하면 오류가 발생합니다.

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Azure 저장소 탐색기를 사용 하 여 hello Hadoop 클러스터의 hello 기본 컨테이너를 열면 hello 다음 그림에에서 표시 된 대로 hello 하이브 쿼리의 hello 출력을 볼 수 있습니다. Hello (빨간색 상자 강조 표시) 필터 tooonly 검색 hello 사용 하 여 blob 이름 다음에 지정 된 문자를 적용할 수 있습니다.

![작업 영역 만들기](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Hello 하이브 편집기로 하이브 쿼리를 제출 합니다.
Hello 양식의 URL을 입력 하 여 hello 쿼리 콘솔 (하이브 편집기)를 사용할 수도 있습니다 *https://&#60; Hadoop 클러스터 이름 >.azurehdinsight.net/Home/HiveEditor* 웹 브라우저에 있습니다. 있어야이 콘솔 hello 참조에 로그인 하 고 여기에 Hadoop 클러스터 자격 따라서 해야 합니다.

### <a name="ps"></a> 3. Azure PowerShell 명령을 사용하여 Hive 쿼리 제출
또한 PowerShell toosubmit 하이브 쿼리를 사용할 수 있습니다. 자세한 내용은 [PowerShell을 사용하여 Hive 작업 제출](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.

## <a name="create-tables"></a>Hive 데이터베이스 및 테이블 만들기
hello 하이브 쿼리 공유 hello [GitHub 리포지토리](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) 여기에서 다운로드할 수 있습니다.

하이브 테이블을 만드는 hello 하이브 쿼리는 다음과 같습니다.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

tooplug 해야 하는 hello 필드 및 기타 구성 hello 설명은 다음과 같습니다.

* **&#60; 데이터베이스 이름 >**: toocreate hello 데이터베이스의 이름을 hello 합니다. Toouse hello 기본 데이터베이스를 원하는 경우 hello 쿼리 *데이터베이스를 만드는 중...*  생략할 수 있습니다.
* **&#60; 테이블 이름 >**: hello 이름 hello 지정 된 데이터베이스 내에서 toocreate hello 테이블입니다. Toouse hello 기본 데이터베이스를 원하는 경우 hello 테이블 참조 될 수 있습니다 직접 *&#60; 테이블 이름 >* 없이 &#60; 데이터베이스 이름 >.
* **&#60; 필드 구분 >**: hello 데이터 파일 toobe의 필드를 구분 하는 hello 구분 기호 toohello Hive 테이블을 업로드 합니다.
* **&#60; 선 구분 기호가 >**: hello 데이터 파일에 있는 줄을 구분 하는 hello 구분 기호입니다.
* **&#60; 저장소 위치 >**: hello Azure 저장소 위치 toosave hello 하이브 테이블의 데이터입니다. 지정 하지 않으면 *위치 &#60; 저장소 위치 >*, 데이터베이스 hello 및 hello 테이블에 저장 됩니다 *hive/웨어하우스/* 디렉터리에서 기본적으로 hello 하이브 클러스터의 hello 기본 컨테이너입니다. Toospecify hello 저장소 위치를 원하는 경우 hello 저장소 위치 toobe hello 데이터베이스 및 테이블에 대 한 hello 기본 컨테이너 내에 있습니다. 이 위치에 hello 형태로 표시의 hello 클러스터의 위치 상대 toohello 기본 컨테이너 라고 toobe *' wasb: / / / &#60; 1 디렉터리 > /'* 또는 *' wasb: / / / &#60; 1 디렉터리 > / &#60; 2 디렉터리 > /'*등입니다. Hello 쿼리를 실행 한 후에 hello 기본 컨테이너에서 hello 상대 디렉터리가 만들어집니다.
* **TBLPROPERTIES("skip.header.line.count"="1")**: hello 데이터 파일에 헤더 줄을 있으면 tooadd이이 속성 **hello 끝** 의 hello *테이블을 만들* 쿼리 합니다. 그렇지 않으면 hello 헤더 줄은 레코드 toohello 테이블로 로드 됩니다. Hello 데이터 파일에 헤더 줄이 없는 경우이 구성은 hello 쿼리에서 생략할 수 있습니다.

## <a name="load-data"></a>데이터 tooHive 테이블 로드
Hive 테이블에 데이터를 로드 하는 hello 하이브 쿼리는 다음과 같습니다.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; 경로 tooblob 데이터 >**: hello blob 파일 업로드 toobe toohello Hive 테이블 hello HDInsight Hadoop 클러스터의 hello 기본 컨테이너 이면 hello *&#60; 경로 tooblob 데이터 >* hello 형식 이어야 합니다 *' wasb: / / / &#60;이 컨테이너에 디렉터리 > / &#60; blob 파일 이름 >'*합니다. 또한 hello HDInsight Hadoop 클러스터의 추가 컨테이너에서 hello blob 파일 수 있습니다. 이 경우 *&#60; 경로 tooblob 데이터 >* hello 형식은 *' wasb: / / &#60; 컨테이너 이름 > @&#60; 저장소 계정 이름 >.blob.core.windows.net/ &#60; blob 파일 이름 >'*.

  > [!NOTE]
  > hello blob 데이터 업로드 toobe tooHive 테이블에 toobe hello 기본 또는 hello Hadoop 클러스터에 대 한 hello 저장소 계정의 컨테이너를 추가 합니다. 그렇지 않으면 hello *데이터 로드* hello 데이터를 액세스할 수 없다고 메시지가 쿼리가 실패 합니다.
  >
  >

## <a name="partition-orc"></a>고급 토픽: 분할된 테이블 및 ORC 형식으로 Hive 데이터 저장
Hello 데이터가 클 경우 hello 테이블 분할은 tooscan hello 테이블의 몇 가지 파티션을 하기만 하는 쿼리에 유용 합니다. 예를 들어, 날짜별으로 웹 사이트의 적절 한 toopartition hello 로그 데이터 됩니다.

또한 toopartitioning에서 하이브 테이블, hello에 최적화 된 행 열 형식 (ORC) 형식에 유용한 toostore hello 하이브 데이터 이기도 합니다. ORC 형식에 대한 자세한 내용은 <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">ORC 파일을 사용하면 Hive에서 데이터를 읽고, 쓰고, 처리할 때 성능 향상</a>을 참조하세요.

### <a name="partitioned-table"></a>분할된 테이블
분할된 된 테이블을 만들고 데이터를 로드 하는 hello 하이브 쿼리는 다음과 같습니다.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

분할 된 테이블을 쿼리할 때 것이 좋습니다 hello에 tooadd hello 파티션 조건을 **시작** hello의 `where` 절이 크게 검색의 hello 효율성을 향상 시킵니다.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>ORC 형식으로 Hive 데이터 저장
직접 hello ORC 형식에 저장 된 Hive 테이블에 blob 저장소에서 데이터를 로드할 수 없습니다. 다음은 hello 단계 tootake tooload 데이터 Azure에서 유지 해야 하는 hello blob tooHive 테이블 ORC 형식으로 저장 합니다.

외부 테이블 만들기 **AS 텍스트 파일 저장** 및 blob 저장소 toohello 테이블에서 데이터를 로드 합니다.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

내부 테이블을 만듭니다 hello로 필드를 구분 기호가 동일 하 고 저장 하는 hello로 1 단계에서 hello 외부 테이블과 같은 스키마 hello 하이브 데이터 hello ORC 형태로 표시 합니다.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

1 단계에서 hello 외부 테이블에서 데이터를 선택 하 고 hello ORC 테이블에 삽입

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> 경우 hello 텍스트 파일 테이블 *&#60; 데이터베이스 이름 >. &#60; 텍스트 파일 외부 테이블 이름 >* 에 파티션이 3 단계에서에서 hello `SELECT * FROM <database name>.<external textfile table name>` 선택 hello에 필드가 데이터 집합을 반환 하는 대로 파티션 변수 hello 명령입니다. Hello에 삽입 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* 이후 실패 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* hello 파티션 변수로 없는 hello 테이블 스키마의 필드입니다. Toospecifically 선택 hello 필드 toobe 너무 삽입이 경우 해야*&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >* 다음과 같습니다.
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

안전 toodrop hello *&#60; 텍스트 파일 외부 테이블 이름 >* 경우 모든 데이터 후 다음 쿼리는 hello를 사용 하 여 삽입 한 *&#60; 데이터베이스 이름 >. &#60; ORC 테이블 이름 >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

이 절차를 수행 후 hello ORC 형식 준비 toouse에 데이터가 있는 테이블을 있어야 합니다.  
