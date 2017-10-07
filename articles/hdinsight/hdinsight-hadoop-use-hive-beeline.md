---
title: "Apache Hive-Azure HDInsight와 Beeline aaaUse | Microsoft Docs"
description: "HDInsight에서 Hadoop으로 toouse hello Beeline 클라이언트 toorun 하이브 쿼리 하는 방법에 대해 알아봅니다. Beeline은 JDBC를 통한 HiveServer2 작업을 위한 유틸리티입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Apache Hive와 hello Beeline 클라이언트를 사용 하 여

자세한 방법을 toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) HDInsight의 Hive toorun를 쿼리 합니다.

Beeline는 HDInsight 클러스터의 헤드 노드에 hello에 포함 된 하이브 클라이언트입니다. Beeline는 JDBC tooconnect tooHiveServer2 HDInsight 클러스터에서 호스트 되는 서비스를 사용 합니다. HDInsight에 Beeline tooaccess 하이브 이상 원격으로 사용할 수도 인터넷 hello 합니다. 다음 표에서 hello Beeline와 함께 사용할 연결 문자열을 제공 합니다.

| Beeline을 실행하는 위치 | 매개 변수 |
| --- | --- | --- |
| SSH 연결 tooa 헤드 노드에 또는 가장자리 노드 | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| 외부 hello 클러스터 | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> 대체 `admin` 클러스터에 대 한 hello 클러스터 로그인 계정을 사용 합니다.
>
> 대체 `password` hello 클러스터 로그인 계정에 대 한 hello 암호를 사용 합니다.
>
> 대체 `clustername` HDInsight 클러스터의 hello 이름의 합니다.

## <a id="prereq"></a>필수 조건

* HDInsight 클러스터의 Linux 기반 Hadoop

  > [!IMPORTANT]
  > Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* SSH 클라이언트 또는 로컬 Beeline 클라이언트입니다. 대부분의 hello이이 문서의 단계 Beeline SSH 세션 toohello 클러스터에서 사용 한다고 가정 합니다. 참조 hello Beeline hello 클러스터 외부에서 실행에 대 한 내용은 [Beeline를 원격으로 사용 하 여](#remote) 섹션.

    SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

## <a id="beeline"></a>Beeline 사용

1. Beeline을 시작할 때 HDInsight 클러스터에서 HiveServer2에 대한 연결 문자열을 제공해야 합니다. hello 클러스터 외부에서 toorun hello 명령을 제공 해야 hello 클러스터 로그인 계정 이름 (기본 `admin`) 및 암호. 다음 테이블 toofind hello 연결 문자열 형식 및 매개 변수 toouse hello를 사용 합니다.

    | Beeline을 실행하는 위치 | 매개 변수 |
    | --- | --- | --- |
    | SSH 연결 tooa 헤드 노드에 또는 가장자리 노드 | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | 외부 hello 클러스터 | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    예를 들어 다음 명령을 hello SSH 세션 toohello 클러스터에서 사용 되는 toostart Beeline 될 수 있습니다.

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    이 명령은 hello Beeline 클라이언트를 시작 하 고 tooHiveServer2 hello 클러스터 헤드 노드에 연결 합니다. Hello 명령이 완료 된 후 본사에 도착 하면는 `jdbc:hive2://headnodehost:10001/>` 프롬프트입니다.

2. Beeline 명령은 일반적으로 `!` 문자로 시작합니다. 예를 들어 `!help`는 도움말을 표시합니다. 그러나 hello `!` 일부 명령에 대 한 생략 될 수 있습니다. 예를 들어 `help`도 작동합니다.

    `!sql`, 어떤 HiveQL 문은 tooexecute 사용된 됩니다. 그러나 HiveQL 하므로 일반적으로 사용 되므로 이전 hello를 생략할 수 있습니다 `!sql`합니다. 다음 두 조건 hello 동일 합니다.

    ```hiveql
    !sql show tables;
    show tables;
    ```

    새 클러스터에서는 **hivesampletable**이라는 테이블 하나만 나열됩니다.

3. Hello hivesampletable에 대 한 명령 toodisplay hello 스키마를 따르는 hello를 사용 합니다.

    ```hiveql
    describe hivesampletable;
    ```

    이 명령은 hello 다음 정보를 반환 합니다.

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    이 정보는 hello 테이블의 hello 열에 설명 합니다. 이 데이터에 대 한 일부 쿼리를 수행할 수 있습니다, 동안 대신 만들겠습니다 완전히 새로운 테이블 toodemonstrate 어떻게 하이브에 tooload 데이터 및 스키마를 적용 합니다.

4. Hello 문을 toocreate 라는 테이블을 다음 입력 **log4jLogs** hello HDInsight 클러스터와 함께 제공 되는 샘플 데이터를 사용 하 여:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    이러한 문은 hello 다음 작업을 수행 합니다.

    * `DROP TABLE`-Hello 테이블이 있는 경우 삭제 됩니다.

    * `CREATE EXTERNAL TABLE` - Hive에서 **외부** 테이블을 만듭니다. 외부 테이블만 하이브에 hello 테이블 정의 저장합니다. hello 데이터는 hello 원래 위치에 남아 있습니다.

    * `ROW FORMAT`-어떻게 hello 데이터의 서식을 지정 합니다. 이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.

    * `STORED AS TEXTFILE LOCATION`-Hello 데이터가 저장 되 고 어떤 파일 형태로 표시 합니다.

    * `SELECT`-모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다. 이 값을 포함하는 세 개의 행이 있으므로 이 쿼리는 **3** 값을 반환합니다.

    * `INPUT__FILE__NAME LIKE '%.log'`-하이브 tooapply hello 스키마 tooall hello 디렉터리에 파일을 시도합니다. 이 경우 hello 디렉터리 hello 스키마와 일치 하지 않는 파일을 포함 합니다. tooprevent 가비지 데이터 hello 결과에,이 문은 알 수 하이브 것만 반환할지 여부를 데이터 파일의 끝에서. 로그입니다.

  > [!NOTE]
  > 외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다. 예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.
  >
  > 외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.

    hello이 명령의 비슷한 toohello 팔 로우 텍스트 출력:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. tooexit Beeline를 사용 하 여 `!exit`합니다.

## <a id="file"></a>Beeline toorun HiveQL 파일을 사용 하 여

다음 단계는 파일 toocreate Beeline를 사용 하 여를 실행 하는 hello를 사용 합니다.

1. 사용 하 여 hello 다음 명령은 toocreate 이라는 파일로 내보내집니다 **query.hql**:

    ```bash
    nano query.hql
    ```

2. 콘텐츠로 사용 hello hello 파일 텍스트를 다음 hello를 사용 합니다. 이 쿼리는 **errorLogs**라는 새 '내부' 테이블을 만듭니다.

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    이러한 문은 hello 다음 작업을 수행 합니다.

    * **만들 테이블 IF NOT EXISTS** -hello 테이블이 아직 없는 경우 자동으로 만들어집니다. Hello 이후 **외부** 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다. 내부 테이블 hello 하이브 데이터 웨어하우스에 저장 되 고 하이브에서 완전히 관리 됩니다.
    * **AS ORC 저장** -hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장 합니다. ORC 형식은 Hive 데이터를 저장하기 위해 고도로 최적화되고 효율적인 형식입니다.
    * **덮어쓰기 삽입... 선택** -hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.

    > [!NOTE]
    > 외부 테이블의 경우와 달리 hello 기본 데이터도 삭제 내부 테이블을 삭제 합니다.

3. toosave hello 파일을 사용 하 여 **Ctrl**+**_X**, 다음 입력 **Y**, 마지막으로 **Enter**합니다.

4. 다음 toorun hello 파일 Beeline를 사용 하 여 hello를 사용 합니다.

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > hello `-i` 매개 변수 Beeline 시작, 실행 hello hello query.hql 파일에는 문입니다. Hello에 도착 하는 hello 쿼리 완료 되 면 `jdbc:hive2://headnodehost:10001/>` 프롬프트입니다. Hello를 사용 하는 파일을 실행할 수도 있습니다 `-f` 매개 변수는 hello 쿼리 완료 후 Beeline 종료 됩니다.

5. hello tooverify **살펴볼** 테이블을 만든 다음 행에서 hello 모든 문을 tooreturn hello를 사용 하 여, **살펴볼**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Beeline을 원격으로 사용

로컬에 설치 되어 Beeline 했거나 사용 Docker 이미지를 통해와 같은 경우 [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), 매개 변수 뒤 hello를 사용 해야 합니다.

* __연결 문자열__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __클러스터 로그인 이름__: `-n admin`

* __클러스터 로그인 암호__ `-p 'password'`

Hello 대체 `clustername` HDInsight 클러스터의 hello 이름의 hello 연결 문자열에 있습니다.

대체 `admin` 클러스터 로그인 및 바꾸기의 hello 이름의 `password` 클러스터 로그인에 대 한 hello 암호를 사용 합니다.

## <a id="sparksql"></a>Spark와 함께 Beeline 사용

Spark는 종종 참조 된 tooas hello Spark Thrift 서버는 HiveServer2의 자체 구현을 제공 합니다. 이 서비스는 하이브를 대신 Spark SQL tooresolve 쿼리를 사용 하며 쿼리에 따라 더 나은 성능을 제공할 수 있습니다.

HDInsight 클러스터를 사용 하 여 포트의 Spark의 tooconnect toohello Spark Thrift 서버 `10002` 대신 `10001`합니다. 예: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> hello Spark Thrift 서버가 액세스할 수 있는 조치 hello 인터넷 직접 합니다. 만 tooit 대 한 SSH 세션에서 연결 하거나 HDInsight 클러스터를 hello 대로 hello 동일한 Azure 가상 네트워크 내 수 있습니다.

## <a id="summary"></a><a id="nextsteps"></a>다음 단계

HDInsight의 Hive 대 한 일반적인 정보에 대 한 참조 문서 다음 hello:

* [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md)

HDInsight의 Hadoop 작업할 수는 다른 방법에 대 한 자세한 내용은 다음 문서는 hello를 참조 하십시오.

* [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md)

Tez 하이브가 있는 사용 하는 경우 다음 문서는 hello 참조:

* [Windows 기반 HDInsight의 hello Tez UI를 사용 하 여](hdinsight-debug-tez-ui.md)
* [Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
