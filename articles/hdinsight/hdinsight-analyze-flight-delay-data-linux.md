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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="67cbd-103">Linux 기반 HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="67cbd-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="67cbd-104">방법에서 사용 하 여 하이브 Linux 기반 HDInsight 다음 tooanalyze 비행 연착 데이터 내보내기 hello 데이터 tooAzure SQL 데이터베이스에 알아봅니다 Sqoop를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67cbd-105">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="67cbd-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67cbd-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cbd-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="67cbd-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="67cbd-108">Prerequisites</span></span>

* <span data-ttu-id="67cbd-109">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="67cbd-110">새 Linux 기반 HDInsight 클러스터를 만드는 단계는 [Linux의 HDInsight에서 Hive와 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cbd-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="67cbd-111">**Azure SQL 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-111">**Azure SQL Database**.</span></span> <span data-ttu-id="67cbd-112">Azure SQL Database를 대상 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="67cbd-113">SQL 데이터베이스가 없는 경우 [SQL 데이터베이스 자습서: 몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cbd-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="67cbd-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="67cbd-114">**Azure CLI**.</span></span> <span data-ttu-id="67cbd-115">Hello Azure CLI를 설치 하지 않은 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) 더 많은 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="67cbd-116">Hello 비행 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="67cbd-116">Download hello flight data</span></span>

1. <span data-ttu-id="67cbd-117">너무 찾아보기[연구 및 운송 통계 Bureau 혁신적인 기술을 관리][rita-website]합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="67cbd-118">Hello 페이지에서 다음 값에는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="67cbd-119">이름</span><span class="sxs-lookup"><span data-stu-id="67cbd-119">Name</span></span> | <span data-ttu-id="67cbd-120">값</span><span class="sxs-lookup"><span data-stu-id="67cbd-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="67cbd-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="67cbd-121">Filter Year</span></span> |<span data-ttu-id="67cbd-122">2013</span><span class="sxs-lookup"><span data-stu-id="67cbd-122">2013</span></span> |
   | <span data-ttu-id="67cbd-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="67cbd-123">Filter Period</span></span> |<span data-ttu-id="67cbd-124">January</span><span class="sxs-lookup"><span data-stu-id="67cbd-124">January</span></span> |
   | <span data-ttu-id="67cbd-125">필드</span><span class="sxs-lookup"><span data-stu-id="67cbd-125">Fields</span></span> |<span data-ttu-id="67cbd-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="67cbd-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="67cbd-127">기타 모든 필드 지우기</span><span class="sxs-lookup"><span data-stu-id="67cbd-127">Clear all other fields</span></span> |

3. <span data-ttu-id="67cbd-128">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="67cbd-129">Hello 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="67cbd-129">Upload hello data</span></span>

1. <span data-ttu-id="67cbd-130">노드 다음에 오는 명령 tooupload hello zip 파일 toohello HDInsight 클러스터 헤드 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="67cbd-131">대체 **FILENAME** hello zip 파일의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="67cbd-132">대체 **USERNAME** hello HDInsight 클러스터에 대 한 hello SSH 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="67cbd-133">CLUSTERNAME를 hello HDInsight 클러스터의 hello 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="67cbd-134">암호 tooauthenticate SSH 로그인을 사용 하면 hello 암호에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="67cbd-135">공개 키를 사용한 경우 toouse hello 할 수 있습니다 `-i` 매개 변수 하 고 개인 키와 일치 하는 hello 경로 toohello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="67cbd-136">예: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="67cbd-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="67cbd-137">Hello 업로드가 완료 되 면 연결 SSH를 사용 하 여 toohello 클러스터:</span><span class="sxs-lookup"><span data-stu-id="67cbd-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="67cbd-138">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cbd-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="67cbd-139">연결 되 면 hello 다음 toounzip hello.zip 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="67cbd-140">이 명령은 크기가 약 60MB인 .csv 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="67cbd-141">명령 toocreate 디렉터리에 나오는 HDInsight 저장소에 hello를 사용 하 고 hello 파일 toohello 디렉터리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="67cbd-142">만들기 및 hello HiveQL를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="67cbd-143">사용 하 여 hello 다음 tooimport 데이터 hello CSV 파일에서 명명 된 Hive 테이블에 단계 **지연**합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="67cbd-144">사용 하 여 hello 다음 toocreate 명령 및 라는 새 파일을 편집 **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="67cbd-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="67cbd-145">이 파일의 내용에 hello 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="67cbd-146">toosave hello 파일을 사용 하 여 **Ctrl + X**, 다음 **Y** 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="67cbd-147">toostart Hive 및 실행된 hello **flightdelays.hql** 파일에서 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="67cbd-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="67cbd-148">이 예제에서는 `localhost` HiveServer2 실행 되 고 hello HDInsight 클러스터의 헤드 노드에 연결 된 toohello 되므로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="67cbd-149">한 번 hello __flightdelays.hql__ 스크립트 실행이 완료 될을 사용 하 여 hello 다음 명령은 대화형 Beeline 세션 tooopen:</span><span class="sxs-lookup"><span data-stu-id="67cbd-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="67cbd-150">Hello를 받는 경우 `jdbc:hive2://localhost:10001/>` 가져온 hello 비행 연착 데이터에서 같은 쿼리 tooretrieve 데이터가 hello를 사용 하 여, 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="67cbd-151">이 쿼리는 hello 평균 함께 숙련 된 날씨 지연 시간을 지연 하 고 너무 저장 도시 목록을 검색`/tutorials/flightdelays/output`합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="67cbd-152">나중에, Sqoop hello 데이터를이 위치 읽고 tooAzure SQL 데이터베이스 내보내기.</span><span class="sxs-lookup"><span data-stu-id="67cbd-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="67cbd-153">tooexit Beeline, 입력 `!quit` hello 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="67cbd-154">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="67cbd-154">Create a SQL Database</span></span>

<span data-ttu-id="67cbd-155">SQL 데이터베이스를 이미 있는 경우에 hello 서버 이름을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="67cbd-156">Hello에 hello 서버 이름을 찾을 수 있습니다 [Azure 포털](https://portal.azure.com) 선택 하 여 **SQL 데이터베이스**, 데이터베이스의 hello hello 이름에 대해 다음 필터링 하 고 원하는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="67cbd-157">hello에 hello 서버 이름이 나열 되어 **서버** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="67cbd-158">SQL 데이터베이스 아직 없는 경우에 hello 정보 사용 [SQL 데이터베이스 자습서: 분 후에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md) toocreate 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="67cbd-159">Hello 데이터베이스에 사용 되는 hello 서버 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="67cbd-160">SQL 데이터베이스 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="67cbd-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="67cbd-161">여러 가지 방법 tooconnect tooSQL 데이터베이스는 고 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="67cbd-162">다음 단계 사용 하 여 hello [FreeTDS](http://www.freetds.org/) hello HDInsight 클러스터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="67cbd-163">SSH tooconnect toohello Linux 기반 HDInsight 클러스터와 hello SSH 세션에서 단계를 수행 하는 실행된 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="67cbd-164">다음 명령은 tooinstall FreeTDS hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="67cbd-165">Hello 설치 완료 되 면 다음 명령 tooconnect toohello SQL 데이터베이스 서버 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="67cbd-166">대체 **serverName** hello SQL 데이터베이스 서버 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="67cbd-167">대체 **adminLogin** 및 **adminPassword** SQL 데이터베이스에 대 한 hello 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="67cbd-168">대체 **databaseName** hello 데이터베이스 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="67cbd-169">텍스트 다음 출력 유사한 toohello를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="67cbd-170">Hello에 `1>` 프롬프트 hello 줄을 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="67cbd-171">Hello 때 `GO` hello 이전 문이 계산을 문을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="67cbd-172">이 쿼리는 클러스터형 인덱스가 있는 **지연**이라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="67cbd-173">다음 테이블 hello 쿼리 tooverify 사용 하 여 hello가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="67cbd-174">hello는 텍스트 다음 비슷한 toohello 출력:</span><span class="sxs-lookup"><span data-stu-id="67cbd-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="67cbd-175">입력 `exit` hello에 `1>` tooexit hello tsql 유틸리티 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="67cbd-176">Sqoop으로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="67cbd-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="67cbd-177">사용 하 여 hello 다음 명령 tooverify Sqoop SQL 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="67cbd-178">이 명령은 hello 지연 테이블에서 이전에 만든 hello 데이터베이스를 포함 하 여 데이터베이스의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="67cbd-179">Hello 명령 tooexport 데이터 hivesampletable toohello mobiledata 테이블에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="67cbd-180">Sqoop hello 지연 테이블이 포함 된 toohello 데이터베이스를 연결 하 고 hello에서 데이터를 내보내는 `/tutorials/flightdelays/output` 디렉터리 toohello 지연 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="67cbd-181">Hello 명령이 완료 된 후 다음 TSQL을 사용 하 여 tooconnect toohello 데이터베이스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="67cbd-182">연결 되 면 다음 문을 tooverify hello 데이터 내보낸된 toohello mobiledata 테이블 했음을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="67cbd-183">Hello 테이블의에서 데이터를 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="67cbd-184">형식 `exit` tooexit hello tsql 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="67cbd-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="67cbd-185"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="67cbd-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="67cbd-186">toolearn HDInsight의 데이터로 자세한 방법으로 toowork 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="67cbd-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="67cbd-187">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="67cbd-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="67cbd-188">[HDInsight에서 Oozie 사용][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="67cbd-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="67cbd-189">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="67cbd-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="67cbd-190">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="67cbd-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="67cbd-191">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="67cbd-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="67cbd-192">[HDInsight용 Python Hadoop 스트리밍 프로그램 개발][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="67cbd-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
