---
title: "HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석 - Azure | Microsoft Docs"
description: "Hive를 사용하여 Linux 기반 HDInsight에서 비행 데이터를 분석한 다음 Sqoop을 사용하여 SQL 데이터베이스에 데이터를 내보내는 방법에 대해 알아봅니다 "
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="07e98-103">Linux 기반 HDInsight에서 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="07e98-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="07e98-104">Linux 기반 HDInsight에서 Hive를 사용하여 비행 지연 데이터를 분석한 다음 Sqoop을 사용하여 Azure SQL 데이터베이스에 데이터를 내보내는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07e98-105">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="07e98-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="07e98-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="07e98-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="07e98-108">Prerequisites</span></span>

* <span data-ttu-id="07e98-109">**HDInsight 클러스터**.</span><span class="sxs-lookup"><span data-stu-id="07e98-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="07e98-110">새 Linux 기반 HDInsight 클러스터를 만드는 단계는 [Linux의 HDInsight에서 Hive와 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="07e98-111">**Azure SQL 데이터베이스**.</span><span class="sxs-lookup"><span data-stu-id="07e98-111">**Azure SQL Database**.</span></span> <span data-ttu-id="07e98-112">Azure SQL Database를 대상 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="07e98-113">SQL 데이터베이스가 없는 경우 [SQL 데이터베이스 자습서: 몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="07e98-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="07e98-114">**Azure CLI**.</span></span> <span data-ttu-id="07e98-115">Azure CLI를 설치하지 않은 경우 자세한 단계는 [Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="07e98-116">비행 데이터 다운로드</span><span class="sxs-lookup"><span data-stu-id="07e98-116">Download the flight data</span></span>

1. <span data-ttu-id="07e98-117">[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website](영문)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="07e98-118">페이지에서 다음 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="07e98-119">이름</span><span class="sxs-lookup"><span data-stu-id="07e98-119">Name</span></span> | <span data-ttu-id="07e98-120">값</span><span class="sxs-lookup"><span data-stu-id="07e98-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="07e98-121">Filter Year</span><span class="sxs-lookup"><span data-stu-id="07e98-121">Filter Year</span></span> |<span data-ttu-id="07e98-122">2013</span><span class="sxs-lookup"><span data-stu-id="07e98-122">2013</span></span> |
   | <span data-ttu-id="07e98-123">Filter Period</span><span class="sxs-lookup"><span data-stu-id="07e98-123">Filter Period</span></span> |<span data-ttu-id="07e98-124">January</span><span class="sxs-lookup"><span data-stu-id="07e98-124">January</span></span> |
   | <span data-ttu-id="07e98-125">필드</span><span class="sxs-lookup"><span data-stu-id="07e98-125">Fields</span></span> |<span data-ttu-id="07e98-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="07e98-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="07e98-127">기타 모든 필드 지우기</span><span class="sxs-lookup"><span data-stu-id="07e98-127">Clear all other fields</span></span> |

3. <span data-ttu-id="07e98-128">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="07e98-129">데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="07e98-129">Upload the data</span></span>

1. <span data-ttu-id="07e98-130">다음 명령을 사용하여 HDInsight 클러스터 헤드 노드에 zip 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="07e98-131">**FILENAME**을 zip 파일의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="07e98-132">**USERNAME**을 HDInsight 클러스터에 대한 SSH 로그인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="07e98-133">CLUSTERNAME을 HDInsight 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="07e98-134">SSH 로그인을 인증하는 암호를 사용한 경우 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="07e98-135">공용 키를 사용하는 경우, `-i` 매개 변수를 사용하고 개인 키와 일치하는 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="07e98-136">예: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="07e98-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="07e98-137">업로드가 완료되면 SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="07e98-138">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="07e98-139">연결되면 다음을 사용하여.zip 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="07e98-140">이 명령은 크기가 약 60MB인 .csv 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="07e98-141">다음 명령을 사용하여 HDInsight 저장소에 디렉터리를 만들고 파일을 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="07e98-142">HiveQL 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="07e98-142">Create and run the HiveQL</span></span>

<span data-ttu-id="07e98-143">다음 단계를 사용하여 CSV 파일에서 **지연**라는 Hive 테이블로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="07e98-144">다음 명령을 사용하여 **flightdelays.hql**이라는 새 파일을 만들고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="07e98-145">이 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="07e98-146">파일을 저장하려면 **Ctrl + X**, **Y**를 차례로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="07e98-147">Hive를 시작하고 **flightdelays.hql** 파일을 실행하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="07e98-148">이 예제에서 HDInsight 클러스터의 헤드 노드에 연결되어 있기 때문에 `localhost`을 사용합니다. 여기서 HiveServer2가 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="07e98-149">__flightdelays.hql__ 스크립트 실행이 완료되면 다음 명령을 사용하여 대화형 Beeline 세션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="07e98-150">`jdbc:hive2://localhost:10001/>` 프롬프트를 수신하면, 다음 쿼리를 사용하여 가져온 비행 지연 데이터에서 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="07e98-151">이 쿼리는 평균 지연 시간과 함께 날씨 지연이 발생된 도시 목록이 검색된 후 `/tutorials/flightdelays/output`에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="07e98-152">나중에 Sqoop는 이 위치에서 데이터를 읽어 Azure SQL Database로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="07e98-153">Beeline을 종료하려면 프롬프트에 `!quit`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="07e98-154">SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="07e98-154">Create a SQL Database</span></span>

<span data-ttu-id="07e98-155">SQL 데이터베이스가 이미 있는 경우 서버 이름을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="07e98-156">[SQL Databases](https://portal.azure.com)를 선택하여 **Azure Portal**에서 서버 이름을 찾은 다음 사용하려는 데이터베이스의 이름을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="07e98-157">서버 이름은 **서버** 열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="07e98-158">SQL 데이터베이스가 없는 경우 [SQL 데이터베이스 자습서: 몇 분 만에 SQL 데이터베이스 만들기](../sql-database/sql-database-get-started.md) 의 정보를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="07e98-159">데이터베이스에 사용한 서버 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="07e98-160">SQL 데이터베이스 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="07e98-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="07e98-161">여러 가지 방법으로 SQL Database에 연결하고 테이블을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="07e98-162">다음 단계는 HDInsight 클러스터의 [FreeTDS](http://www.freetds.org/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="07e98-163">SSH를 사용하여 Linux 기반 HDInsight 클러스터에 연결하고 SSH 세션에서 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="07e98-164">다음 명령을 사용하여 FreeTDS:를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="07e98-165">설치가 끝나면 다음 명령을 사용하여 SQL Database 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="07e98-166">**serverName**을 SQL 데이터베이스 서버 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="07e98-167">**adminLogin** 및 **adminPassword**를 SQL Database의 로그인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="07e98-168">**databaseName**을 데이터베이스 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="07e98-169">다음 텍스트와 비슷한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="07e98-170">`1>` 프롬프트에 다음 행을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="07e98-171">`GO` 문을 입력하면 이전 문이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="07e98-172">이 쿼리는 클러스터형 인덱스가 있는 **지연**이라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="07e98-173">다음 쿼리를 사용하여 테이블이 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="07e98-174">다음 텍스트와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="07e98-175">`exit` at the `1>`를 입력하여 tsql 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="07e98-176">Sqoop으로 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="07e98-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="07e98-177">다음 명령을 사용하여 Sqoop이 SQL 데이터베이스를 볼 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="07e98-178">이 명령은 지연 테이블을 만든 데이터베이스를 포함한 데이터베이스 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="07e98-179">다음 명령을 사용하여 hivesampletable에서 mobiledata 테이블로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="07e98-180">Sqoop은 지연 테이블을 포함하는 데이터베이스에 연결되고 `/tutorials/flightdelays/output` 디렉터리에서 지연 테이블로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="07e98-181">명령이 완료되면 다음을 통해 TSQL을 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="07e98-182">연결되면 다음 명령문을 사용하여 데이터가 mobiledata 테이블로 내보내기되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="07e98-183">테이블에 데이터 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="07e98-184">`exit` 를 입력하여 tsql 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="07e98-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="07e98-185"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="07e98-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="07e98-186">HDInsight에서 데이터 사용에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e98-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="07e98-187">[HDInsight에서 Hive 사용][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="07e98-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="07e98-188">[HDInsight에서 Oozie 사용][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="07e98-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="07e98-189">[HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="07e98-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="07e98-190">[HDInsight에서 Pig 사용][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="07e98-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="07e98-191">[HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="07e98-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="07e98-192">[HDInsight용 Python Hadoop 스트리밍 프로그램 개발][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="07e98-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
