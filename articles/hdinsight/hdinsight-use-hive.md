---
title: "Apache Hive 및 HiveQL-Azure HDInsight aaaWhat은 | Microsoft Docs"
description: "Apache Hive는 Hadoop용 데이터 웨어하우스 시스템입니다. HiveQL을 비슷한 tooTransact-SQL을 사용 하 여 하이브에 저장 된 데이터를 쿼리할 수 있습니다. 이 문서에서는 설명 toouse 하이브 방법 및 Azure HDInsight와 HiveQL 합니다."
keywords: "hiveql, hive, hadoop hiveql 이란 toouse 하이브 하는 방법에 대해 알아봅니다 하이브를 하이브 란"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Azure HDInsight의 Apache Hive 및 HiveQL이란?

[Apache Hive](http://hive.apache.org/)는 Hadoop용 데이터 웨어하우스 시스템입니다. Hive를 사용하면 데이터의 요약, 쿼리 및 분석을 수행할 수 있습니다. 하이브 쿼리는 쿼리 언어와 유사한 tooSQL HiveQL로 작성 됩니다.

하이브 주로 구조화 되지 않은 데이터에 tooproject 구조를 허용 합니다. Hello 구조를 정의한 후에 Java 또는 MapReduce 지식 없이 HiveQL tooquery hello 데이터를 사용할 수 있습니다.

HDInsight는 특정 워크로드에 맞게 조정되는 여러 클러스터 형식을 제공합니다. 클러스터 유형만 hello 하이브 쿼리에 대 한 가장 자주 사용 됩니다.

* __대화형 하이브__:를 제공 하는 Hadoop 클러스터 [낮은 대기 시간 분석 처리 (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) 대화형 쿼리에 대 한 기능 tooimprove 응답 시간입니다. 자세한 내용은 참조 hello [대화형 HDInsight의 Hive 시작](hdinsight-hadoop-use-interactive-hive.md) 문서.

* __Hadoop__: 배치 프로세싱 워크로드에 대해 조정된 Hadoop 클러스터입니다. 자세한 내용은 참조 hello [HDInsight에서 Hadoop으로 시작](hdinsight-hadoop-linux-tutorial-get-started.md) 문서.

* __Spark__: Apache Spark는 Hive로 작업하기 위한 기본 제공 기능입니다. 자세한 내용은 참조 hello [HDInsight의 spark 시작](hdinsight-apache-spark-jupyter-spark-sql.md) 문서.

* __HBase__: HiveQL HBase에서 저장 된 데이터를 사용 하는 tooquery 될 수 있습니다. 자세한 내용은 참조 hello [HDInsight에서 HBase 시작](hdinsight-hbase-tutorial-get-started-linux.md) 문서.

## <a name="how-toouse-hive"></a>Toouse 하이브 하는 방법

HDInsight와 toouse 하이브 어떻게 테이블 toodiscover 다음 hello를 사용 합니다.

| 다음을 원하는 경우 **이 메서드를 사용**... | ... **대화형** 셸 | ...**배치** 처리 | ... **클러스터 운영 체제** | ... **클라이언트 운영 체제** |
|:--- |:---:|:---:|:--- |:--- |
| [Hive 보기](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |모두(브라우저 기반) |
| [Beeline 클라이언트](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X, 또는 Windows |
| [REST API](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux 또는 Windows* |Linux, Unix, Mac OS X, 또는 Windows |
| [Visual Studio용 HDInsight 도구](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux 또는 Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux 또는 Windows* |Windows |

> [!IMPORTANT]
> \*Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.
>
> Windows 기반 HDInsight 클러스터를 사용 하는 경우에 hello을 사용할 수 있습니다 [쿼리 콘솔](hdinsight-hadoop-use-hive-query-console.md) 브라우저에서 또는 [원격 데스크톱](hdinsight-hadoop-use-hive-remote-desktop.md) toorun 하이브 쿼리 합니다.

## <a name="hiveql-language-reference"></a>HiveQL 언어 참조

HiveQL 언어 참조는 hello에서 사용할 수 있는 [언어 설명서 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)합니다.

## <a name="hive-and-data-structure"></a>Hive 및 데이터 구조

하이브는 toowork로 구성 하는 방식을 반 구조화 된 데이터를 이해 합니다. 예를 들어 텍스트 파일 hello 필드 특정 문자로 구분 되는 위치입니다. HiveQL 문 다음 hello 공백으로 구분 된 데이터에 대해 테이블을 만듭니다.

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

또한 Hive는 복잡하거나 불규칙하게 구조화된 데이터에 대한 사용자 지정을 **serializer/deserializers(SerDe)** 지원합니다. 자세한 내용은 참조 hello [어떻게 toouse HDInsight와 사용자 지정 JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) 문서.

하이브에서 지 원하는 파일 형식에 대 한 자세한 내용은 참조 hello [언어 설명서 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Hive 내부 테이블과 외부 테이블 비교

Hive로 다음과 같은 두 가지 형식의 테이블을 만들 수 있습니다.

* __내부__: hello 하이브 데이터 웨어하우스에 저장 된 데이터입니다. hello 데이터 웨어하우스는에 `/hive/warehouse/` hello 클러스터에 대 한 hello 기본 저장소에 있습니다.

    다음과 같은 경우에 내부 테이블을 사용합니다.

    * 데이터가 일시적입니다.
    * 하이브 toomanage hello 수명 주기를 hello 테이블 및 데이터를 사용 하는 것이 좋습니다.

* __외부__: hello 데이터 웨어하우스 외부 데이터에 저장 합니다. hello 데이터 hello 클러스터에서 액세스할 수 있는 저장소에 저장할 수 있습니다.

    다음과 같은 경우에 외부 테이블을 사용합니다.

    * 하이브 외부 hello 데이터도 사용 됩니다. 예를 들어 hello 데이터 파일 (즉 잠그지 않습니다 hello 파일.) 다른 프로세스에 의해 업데이트 됩니다.
    * 데이터의 위치를 hello 테이블을 삭제 한 후에 기본 hello tooremain이 필요 합니다.
    * 기본이 아닌 저장소 계정과 같은 사용자 지정 위치가 필요합니다.
    * 하이브 이외의 프로그램 hello 데이터 형식, 위치 등을 관리합니다.

자세한 내용은 참조 hello [하이브 내부 및 외부 테이블 소개] [ cindygross-hive-tables] 블로그 게시물입니다.

## <a name="user-defined-functions-udf"></a>UDF(사용자 정의 함수)

Hive는 **사용자 정의 함수(UDF)**를 통해 확장 될 수도 있습니다. UDF는 tooimplement 기능이 나 HiveQL에서 쉽게 모델링 되지 논리를 있습니다. 하이브 Udf 사용의 예를 들어 hello 다음 문서를 참조 하십시오.

* [Hive와 함께 Java 사용자 정의 함수 사용](hdinsight-hadoop-hive-java-udf.md)

* [Hive 및 Pig와 함께 Python 사용자 정의 함수 사용](hdinsight-python.md)

* [Hive 및 Pig와 함께 C# 사용자 정의 함수 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [사용자 정의 사용자 지정 하이브 tooadd tooHDInsight 작동 하는 방법](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [예제 하이브 사용자 정의 함수 tooconvert 날짜/시간 형식 tooHive 타임 스탬프](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>예제 데이터

HDInsight에서 Hive는 `hivesampletable`이라는 내부 테이블로 미리 로드됩니다. 또한 HDInsight는 Hive와 함께 사용할 수 있는 예제 데이터 집합을 제공합니다. 이러한 데이터 집합 hello에 저장 된 `/example/data` 및 `/HdiSamples` 디렉터리입니다. 이 디렉터리는 클러스터에 대 한 hello 기본 저장소에 존재합니다.

## <a id="job"></a>예제 Hive 쿼리

HiveQL 문은 프로젝트 열 hello에 끌어 다음 hello `/example/data/sample.log` 파일:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

Hello 앞의 예제에서 hello HiveQL 문은 hello 다음 작업을 수행 합니다.

* `set hive.execution.engine=tez;`: 세트 실행 엔진 toouse Tez hello 합니다. MapReduce 대신 Tez를 사용하면 쿼리 성능 향상을 제공할 수 있습니다. Tez에 자세한 내용은 참조 hello [성능 향상된을 위해 사용 하 여 Apache Tez](#usetez) 섹션.

    > [!NOTE]
    > 이 문은 Windows 기반 HDInsight 클러스터를 사용할 경우에만 필요합니다. Tez은 Linux 기반 HDInsight 용 hello 기본 실행 엔진입니다.

* `DROP TABLE`: Hello 테이블이 이미 존재 하는 경우이 삭제 합니다.

* `CREATE EXTERNAL TABLE`: Hive에서 새 **외부** 테이블을 만듭니다. 외부 테이블만 하이브에 hello 테이블 정의 저장합니다. hello 데이터 hello 원래 형태로 표시 하 고 hello 원래 위치에 그대로 유지 됩니다.

* `ROW FORMAT`: 하이브 hello 데이터 형식 지정 방법을 알려 줍니다. 이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.

* `STORED AS TEXTFILE LOCATION`: 지시 하이브 여기서 hello 데이터가 저장 됩니다 (hello `example/data` 디렉터리) 텍스트로 저장 됩니다. hello 데이터 hello 디렉터리 내에서 여러 파일에 걸쳐 분산 또는 한 파일에 수 있습니다.

* `SELECT`: 모든 행의 개수를 hello 선택 열 **t4** hello 값이 포함 된 **[오류]**합니다. 이 값을 포함하는 행이 3개 있으므로 이 문은 **3** 값을 반환합니다.

* `INPUT__FILE__NAME LIKE '%.log'`-하이브 tooapply hello 스키마 tooall hello 디렉터리에 파일을 시도합니다. 이 경우 hello 디렉터리 hello 스키마와 일치 하지 않는 파일을 포함 합니다. tooprevent 가비지 데이터 hello 결과에,이 문은 알 수 하이브 것만 반환할지 여부를 데이터 파일의 끝에서. 로그입니다.

> [!NOTE]
> 외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다. 예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.
>
> 외부 테이블 삭제는 **하지** hello 데이터 삭제 hello 테이블 정의 삭제 합니다.

toocreate는 **내부** 대신 외부 테이블에서 다음 HiveQL hello를 사용 하 여:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

이러한 문은 hello 다음 작업을 수행 합니다.

* `CREATE TABLE IF NOT EXISTS`: Hello 테이블이 존재 하지 않는 경우 만듭니다. 때문에 hello **외부** 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다. hello hello 하이브 데이터 웨어하우스에 저장 된 테이블과 하이브에서 완전히 관리 됩니다.

* `STORED AS ORC`: Hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장합니다. ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.

* `INSERT OVERWRITE ... SELECT`: Hello에서 행을 선택 합니다. **log4jLogs** 포함 된 테이블 **[오류]**, 다음 hello에 데이터 hello를 삽입 하 고 **살펴볼** 테이블입니다.

> [!NOTE]
> 외부 테이블의 경우와 달리 hello 기본 데이터를 삭제도 내부 테이블을 삭제 합니다.

## <a name="improve-hive-query-performance"></a>Hive 쿼리 성능 향상

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) 는 하이브를 규모에 훨씬 더 효율적으로 toorun 등 데이터 중심 응용 프로그램을 허용 하는 프레임 워크입니다. Tez는 Linux 기반 HDInsight 클러스터에 대해 기본값으로 사용할 수 있습니다.

> [!NOTE]
> Tez는 현재 Windows 기반 HDInsight 클러스터에 대해 기본적으로 꺼져 있으며 사용하도록 설정해야 합니다. 하이브 쿼리용 tootake 활용 Tez, 다음 값 hello 설정 해야 합니다.
>
> `set hive.execution.engine=tez;`
>
> Tez은 Linux 기반 HDInsight 클러스터에 대 한 hello 기본 엔진입니다.

hello [Tez 디자인 문서에서 하이브](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) hello 구현 선택 항목 및 튜닝 구성 하는 방법에 대 한 세부 정보를 포함 합니다.

작업을 디버깅 tooaid Tez를 사용 하 여 실행, HDInsight hello 다음 Tez 작업의 tooview 세부 정보를 사용할 수 있는 웹 Ui를 제공 합니다.

* [Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여](hdinsight-debug-ambari-tez-view.md)

* [Windows 기반 HDInsight의 hello Tez UI를 사용 하 여](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>LLAP(짧은 대기 시간 분석 처리)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP)(Live Long and Process라고도 함)는 쿼리의 메모리 내 캐싱을 수행할 수 있는 Hive 2.0의 새로운 기능입니다. LLAP는 하이브 쿼리를 훨씬 빠르게 너무[26 x 일부 경우에는 1.x 하이브 보다 더 빠르게](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/)합니다.

HDInsight은 클러스터 유형 대화형 하이브 hello LLAP를 제공합니다. 자세한 내용은 참조 hello [대화형 하이브 시작](hdinsight-hadoop-use-interactive-hive.md) 문서.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Hive 작업 및 SQL Server Integration Services

SQL Server Integration Services (SSIS) toorun 하이브 작업을 사용할 수 있습니다. SSIS 용 Azure 기능 팩 hello 다음과 같은 구성 요소가 HDInsight의 Hive 작업을 사용 하는 hello를 제공 합니다.

* [Azure HDInsight Hive 작업][hivetask]

* [Azure 구독 연결 관리자][connectionmanager]

자세한 정보 hello Azure 기능 팩에 대 한 SSIS [여기][ssispack]합니다.

## <a id="nextsteps"></a>다음 단계

하이브 이란 배운 했으므로 방식과 HDInsight 사용 하 여 hello 뒤에서 Hadoop으로 연결 tooexplore Azure HDInsight와 다른 방법으로 toowork toouse 합니다.

* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight에서 MapReduce 작업 사용][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
