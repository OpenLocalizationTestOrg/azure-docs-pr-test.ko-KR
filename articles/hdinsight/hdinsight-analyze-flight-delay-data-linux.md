---
title: "Azure HDInsight의 Hive와 aaaAnalyze 비행 연착 데이터 | Microsoft Docs"
description: "Toouse을 hello 데이터 tooSQL 내보낼 tooanalyze 비행 데이터 Linux 기반 HDInsight의 Hive 수에 대해 알아봅니다 Sqoop를 사용 하 여 데이터베이스입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Linux 기반 HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석

방법에서 사용 하 여 하이브 Linux 기반 HDInsight 다음 tooanalyze 비행 연착 데이터 내보내기 hello 데이터 tooAzure SQL 데이터베이스에 알아봅니다 Sqoop를 사용 하 여 합니다.

> [!IMPORTANT]
> 이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

### <a name="prerequisites"></a>필수 조건

* **HDInsight 클러스터**. 새 Linux 기반 HDInsight 클러스터를 만드는 단계는 [Linux의 HDInsight에서 Hive와 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.

* **Azure SQL 데이터베이스**. Azure SQL Database를 대상 데이터 저장소로 사용합니다. SQL 데이터베이스가 없는 경우 [SQL 데이터베이스 자습서: 몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)를 참조하세요.

* **Azure CLI**. Hello Azure CLI를 설치 하지 않은 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) 더 많은 단계에 대 한 합니다.

## <a name="download-hello-flight-data"></a>Hello 비행 데이터 다운로드

1. 너무 찾아보기[연구 및 운송 통계 Bureau 혁신적인 기술을 관리][rita-website]합니다.

2. Hello 페이지에서 다음 값에는 hello를 선택 합니다.

   | 이름 | 값 |
   | --- | --- |
   | Filter Year |2013 |
   | Filter Period |January |
   | 필드 |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. 기타 모든 필드 지우기 |

3. **다운로드**를 클릭합니다.

## <a name="upload-hello-data"></a>Hello 데이터 업로드

1. 노드 다음에 오는 명령 tooupload hello zip 파일 toohello HDInsight 클러스터 헤드 hello를 사용 합니다.

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    대체 **FILENAME** hello zip 파일의 hello 이름을 사용 합니다. 대체 **USERNAME** hello HDInsight 클러스터에 대 한 hello SSH 로그인을 사용 합니다. CLUSTERNAME를 hello HDInsight 클러스터의 hello 이름을 바꿉니다.

   > [!NOTE]
   > 암호 tooauthenticate SSH 로그인을 사용 하면 hello 암호에 대 한 메시지가 표시 됩니다. 공개 키를 사용한 경우 toouse hello 할 수 있습니다 `-i` 매개 변수 하 고 개인 키와 일치 하는 hello 경로 toohello를 지정 합니다. 예: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Hello 업로드가 완료 되 면 연결 SSH를 사용 하 여 toohello 클러스터:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.

3. 연결 되 면 hello 다음 toounzip hello.zip 파일을 사용 합니다.

    ```
    unzip FILENAME.zip
    ```

    이 명령은 크기가 약 60MB인 .csv 파일의 압축을 풉니다.

4. 명령 toocreate 디렉터리에 나오는 HDInsight 저장소에 hello를 사용 하 고 hello 파일 toohello 디렉터리를 복사 합니다.

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>만들기 및 hello HiveQL를 실행 합니다.

사용 하 여 hello 다음 tooimport 데이터 hello CSV 파일에서 명명 된 Hive 테이블에 단계 **지연**합니다.

1. 사용 하 여 hello 다음 toocreate 명령 및 라는 새 파일을 편집 **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. toosave hello 파일을 사용 하 여 **Ctrl + X**, 다음 **Y** 합니다.

3. toostart Hive 및 실행된 hello **flightdelays.hql** 파일에서 다음 명령을 hello를 사용 하 여:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > 이 예제에서는 `localhost` HiveServer2 실행 되 고 hello HDInsight 클러스터의 헤드 노드에 연결 된 toohello 되므로 사용 됩니다.

4. 한 번 hello __flightdelays.hql__ 스크립트 실행이 완료 될을 사용 하 여 hello 다음 명령은 대화형 Beeline 세션 tooopen:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Hello를 받는 경우 `jdbc:hive2://localhost:10001/>` 가져온 hello 비행 연착 데이터에서 같은 쿼리 tooretrieve 데이터가 hello를 사용 하 여, 메시지를 표시 합니다.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    이 쿼리는 hello 평균 함께 숙련 된 날씨 지연 시간을 지연 하 고 너무 저장 도시 목록을 검색`/tutorials/flightdelays/output`합니다. 나중에, Sqoop hello 데이터를이 위치 읽고 tooAzure SQL 데이터베이스 내보내기.

6. tooexit Beeline, 입력 `!quit` hello 프롬프트입니다.

## <a name="create-a-sql-database"></a>SQL 데이터베이스 만들기

SQL 데이터베이스를 이미 있는 경우에 hello 서버 이름을 가져와야 합니다. Hello에 hello 서버 이름을 찾을 수 있습니다 [Azure 포털](https://portal.azure.com) 선택 하 여 **SQL 데이터베이스**, 데이터베이스의 hello hello 이름에 대해 다음 필터링 하 고 원하는 toouse 합니다. hello에 hello 서버 이름이 나열 되어 **서버** 열입니다.

SQL 데이터베이스 아직 없는 경우에 hello 정보 사용 [SQL 데이터베이스 자습서: 분 후에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md) toocreate 하나입니다. Hello 데이터베이스에 사용 되는 hello 서버 이름을 저장 합니다.

## <a name="create-a-sql-database-table"></a>SQL 데이터베이스 테이블 만들기

> [!NOTE]
> 여러 가지 방법 tooconnect tooSQL 데이터베이스는 고 테이블을 만듭니다. 다음 단계 사용 하 여 hello [FreeTDS](http://www.freetds.org/) hello HDInsight 클러스터에서 합니다.


1. SSH tooconnect toohello Linux 기반 HDInsight 클러스터와 hello SSH 세션에서 단계를 수행 하는 실행된 hello를 사용 합니다.

2. 다음 명령은 tooinstall FreeTDS hello를 사용 합니다.

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Hello 설치 완료 되 면 다음 명령 tooconnect toohello SQL 데이터베이스 서버 hello를 사용 합니다. 대체 **serverName** hello SQL 데이터베이스 서버 이름으로 합니다. 대체 **adminLogin** 및 **adminPassword** SQL 데이터베이스에 대 한 hello 로그인을 사용 합니다. 대체 **databaseName** hello 데이터베이스 이름으로 합니다.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    텍스트 다음 출력 유사한 toohello를 나타납니다.

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. Hello에 `1>` 프롬프트 hello 줄을 다음을 입력 합니다.

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Hello 때 `GO` hello 이전 문이 계산을 문을 입력 합니다. 이 쿼리는 클러스터형 인덱스가 있는 **지연**이라는 테이블을 만듭니다.

    다음 테이블 hello 쿼리 tooverify 사용 하 여 hello가 만들어졌습니다.

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    hello는 텍스트 다음 비슷한 toohello 출력:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. 입력 `exit` hello에 `1>` tooexit hello tsql 유틸리티 메시지를 표시 합니다.

## <a name="export-data-with-sqoop"></a>Sqoop으로 데이터 내보내기

1. 사용 하 여 hello 다음 명령 tooverify Sqoop SQL 데이터베이스를 볼 수 있습니다.

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    이 명령은 hello 지연 테이블에서 이전에 만든 hello 데이터베이스를 포함 하 여 데이터베이스의 목록을 반환 합니다.

2. Hello 명령 tooexport 데이터 hivesampletable toohello mobiledata 테이블에서 다음을 사용 합니다.

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop hello 지연 테이블이 포함 된 toohello 데이터베이스를 연결 하 고 hello에서 데이터를 내보내는 `/tutorials/flightdelays/output` 디렉터리 toohello 지연 테이블입니다.

3. Hello 명령이 완료 된 후 다음 TSQL을 사용 하 여 tooconnect toohello 데이터베이스 hello를 사용 합니다.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    연결 되 면 다음 문을 tooverify hello 데이터 내보낸된 toohello mobiledata 테이블 했음을 hello를 사용 합니다.

    ```
    SELECT * FROM delays
    GO
    ```

    Hello 테이블의에서 데이터를 목록이 표시 됩니다. 형식 `exit` tooexit hello tsql 유틸리티입니다.

## <a id="nextsteps"></a> 다음 단계

toolearn HDInsight의 데이터로 자세한 방법으로 toowork 참조 문서 다음 hello:

* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Oozie 사용][hdinsight-use-oozie]
* [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]
* [HDInsight용 Python Hadoop 스트리밍 프로그램 개발][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
