---
title: "Apache Hive와 함께 Beeline 사용 - Azure HDInsight | Microsoft Docs"
description: "Beeline 클라이언트를 사용하여 HDInsight에서 Hadoop과 Hive 쿼리를 실행하는 방법을 알아봅니다. Beeline은 JDBC를 통한 HiveServer2 작업을 위한 유틸리티입니다."
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
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="8010d-105">Apache Hive와 함께 Beeline 클라이언트 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="8010d-106">[Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell)을 사용하여 HDInsight에서 Hive 쿼리를 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="8010d-107">Beeline은 HDInsight 클러스터의 헤드 노드에 포함된 Hive 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="8010d-108">Beeline은 JDBC를 사용하여 HDInsight 클러스터에서 호스팅되는 서비스인 HiveServer2에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="8010d-109">또한 Beeline을 사용하면 인터넷을 통해 HDInsight의 Hive에 원격으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="8010d-110">다음 표에서는 Beeline과 함께 사용할 연결 문자열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="8010d-111">Beeline을 실행하는 위치</span><span class="sxs-lookup"><span data-stu-id="8010d-111">Where you run Beeline from</span></span> | <span data-ttu-id="8010d-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8010d-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8010d-113">헤드 노드 또는 에지 노드에 대한 SSH 연결</span><span class="sxs-lookup"><span data-stu-id="8010d-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="8010d-114">클러스터 외부</span><span class="sxs-lookup"><span data-stu-id="8010d-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="8010d-115">`admin`을 클러스터의 클러스터 로그인 계정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="8010d-116">`password`를 클러스터 로그인 계정의 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="8010d-117">`clustername`을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="8010d-118"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="8010d-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="8010d-119">HDInsight 클러스터의 Linux 기반 Hadoop</span><span class="sxs-lookup"><span data-stu-id="8010d-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8010d-120">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8010d-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8010d-122">SSH 클라이언트 또는 로컬 Beeline 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="8010d-123">이 문서에 나온 대부분의 단계는 SSH 세션에서 클러스터까지 Beeline을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="8010d-124">클러스터 외부에서 Beeline을 실행하는 것에 대한 내용은 [Beeline를 원격으로 사용](#remote) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="8010d-125">SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="8010d-126"><a id="beeline"></a>Beeline 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="8010d-127">Beeline을 시작할 때 HDInsight 클러스터에서 HiveServer2에 대한 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="8010d-128">클러스터 외부에서 명령을 실행하려면 클러스터 로그인 계정 이름 (기본값: `admin`)과 암호도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="8010d-129">다음 테이블을 사용하여 연결 문자열 형식 및 사용할 매개 변수를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="8010d-130">Beeline을 실행하는 위치</span><span class="sxs-lookup"><span data-stu-id="8010d-130">Where you run Beeline from</span></span> | <span data-ttu-id="8010d-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8010d-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="8010d-132">헤드 노드 또는 에지 노드에 대한 SSH 연결</span><span class="sxs-lookup"><span data-stu-id="8010d-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="8010d-133">클러스터 외부</span><span class="sxs-lookup"><span data-stu-id="8010d-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="8010d-134">예를 들어 다음 명령은 SSH 세션에서 클러스터까지 Beeline을 시작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="8010d-135">이 명령은 Beeline 클라이언트를 시작하고 클러스터 헤드 노드의 HiveServer2에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="8010d-136">명령이 완료되면 `jdbc:hive2://headnodehost:10001/>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="8010d-137">Beeline 명령은 일반적으로 `!` 문자로 시작합니다. 예를 들어 `!help`는 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="8010d-138">그러나 일부 명령에서는 `!`를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="8010d-139">예를 들어 `help`도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-139">For example, `help` also works.</span></span>

    <span data-ttu-id="8010d-140">HiveQL 문을 실행하는 데 사용되는 `!sql`이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="8010d-141">그러나 HiveQL은 너무 일반적으로 사용되어 이전의 `!sql`를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="8010d-142">다음 두 문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="8010d-143">새 클러스터에서는 **hivesampletable**이라는 테이블 하나만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="8010d-144">다음 명령을 사용하여 hivesampletable의 스키마를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="8010d-145">이 명령은 다음 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-145">This command returns the following information:</span></span>

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

    <span data-ttu-id="8010d-146">이 정보는 테이블의 열을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-146">This information describes the columns in the table.</span></span> <span data-ttu-id="8010d-147">이 데이터에 대한 일부 쿼리를 수행하는 동안 대신 새 테이블을 만들어서 데이터를 Hive에 로드하고 스키마를 적용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="8010d-148">다음 문을 입력하여 HDInsight 클러스터와 함께 제공되는 샘플 데이터로 **log4jLogs**라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="8010d-149">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="8010d-150">`DROP TABLE` - 테이블이 있으면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="8010d-151">`CREATE EXTERNAL TABLE` - Hive에서 **외부** 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="8010d-152">외부 테이블만 테이블 정의를 Hive에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="8010d-153">데이터는 원래 위치에 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="8010d-154">`ROW FORMAT` - 데이터의 형식을 지정하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="8010d-155">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="8010d-156">`STORED AS TEXTFILE LOCATION` - 데이터를 저장하는 위치 및 파일 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="8010d-157">`SELECT` - 열 **t4**에 값 **[ERROR]**가 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="8010d-158">이 값을 포함하는 세 개의 행이 있으므로 이 쿼리는 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="8010d-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive는 디렉터리의 모든 파일에 스키마를 적용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="8010d-160">이 경우 디렉터리에 스키마와 일치하지 않는 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="8010d-161">결과에 가비지 데이터가 나타나는 것을 방지하기 위해 이 문은 .log로 끝나는 파일의 데이터만 반환해야 함을 Hive에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8010d-162">외부 원본에서 기본 데이터를 업데이트하길 원하는 경우에는 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="8010d-163">예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="8010d-164">외부 테이블을 삭제하면 데이터는 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="8010d-165">이 명령의 출력은 다음 텍스트와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-165">The output of this command is similar to the following text:</span></span>

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

5. <span data-ttu-id="8010d-166">Beeline을 종료하려면 `!exit`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="8010d-167"><a id="file"></a>Beeline을 사용하여 HiveQL 파일 실행</span><span class="sxs-lookup"><span data-stu-id="8010d-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="8010d-168">다음 단계를 사용하여 파일을 만든 다음 Beeline를 사용하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="8010d-169">다음 명령을 사용하여 **query.hql**이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="8010d-170">다음 텍스트를 파일의 내용으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="8010d-171">이 쿼리는 **errorLogs**라는 새 '내부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="8010d-172">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="8010d-173">**CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없으면 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="8010d-174">**EXTERNAL** 키워드가 사용되지 않으므로 이 문은 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="8010d-175">내부 테이블은 Hive 데이터 웨어하우스에 저장되며 Hive에 서 완전히 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="8010d-176">**STORED AS ORC** - 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="8010d-177">ORC 형식은 Hive 데이터를 저장하기 위해 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="8010d-178">**덮어쓰기 삽입... SELECT** - **[ERROR]**가 포함된 **log4jLogs** 테이블에서 행을 선택하고 데이터를 **errorLogs** 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8010d-179">외부 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="8010d-180">파일을 저장하려면 **Ctrl**+**_X**을 사용한 다음 **Y**를 입력하고 마지막으로 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="8010d-181">다음을 사용하여 Beeline을 통해 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="8010d-182">`-i` 매개 변수는 Beeline을 시작하고 query.hql 파일의 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="8010d-183">쿼리가 완료되면 `jdbc:hive2://headnodehost:10001/>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="8010d-184">쿼리 완료 후 Beeline을 종료하는 `-f` 매개 변수를 사용하여 파일을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="8010d-185">**errorLogs** 테이블을 만들었는지 확인하려면 다음 문을 사용하여 **errorLogs**에서 모든 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="8010d-186">데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="8010d-187"><a id="remote"></a>Beeline을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="8010d-188">Beeline을 로컬로 설치했거나 [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/)과 같은 Docker 이미지를 통해 Beeline을 사용하는 경우 다음 매개 변수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="8010d-189">__연결 문자열__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="8010d-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="8010d-190">__클러스터 로그인 이름__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="8010d-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="8010d-191">__클러스터 로그인 암호__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="8010d-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="8010d-192">연결 문자열의 `clustername`을 HDInsight 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="8010d-193">`admin`을 클러스터 로그인 이름으로 바꾸고, `password`를 클러스터 로그인 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="8010d-194"><a id="sparksql"></a>Spark와 함께 Beeline 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="8010d-195">Spark는 자체적으로 HiveServer2를 구현하며, HiveServer2는 종종 Spark Thrift 서버라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="8010d-196">이 서비스는 Hive 대신 Spark SQL을 사용하여 쿼리를 해결하고, 쿼리에 따라 더 나은 성능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="8010d-197">HDInsight 클러스터에서 Spark의 Spark Thrift 서버에 연결하려면 `10001` 대신 `10002` 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="8010d-198">예: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`</span><span class="sxs-lookup"><span data-stu-id="8010d-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8010d-199">Spark Thrift 서버는 인터넷을 통해 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="8010d-200">SSH 세션이나 HDInsight 클러스터와 동일한 Azure Virtual Network에서만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8010d-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="8010d-201"><a id="summary"></a><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="8010d-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="8010d-202">HDInsight의 Hive에 대한 보다 일반적인 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="8010d-203">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="8010d-204">HDInsight에서 Hadoop을 사용하여 작업할 수 있는 다른 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="8010d-205">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8010d-206">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="8010d-207">Hive와 함께 Tez를 사용하는 경우 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8010d-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="8010d-208">Windows 기반 HDInsight 클러스터에서 Tez UI 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="8010d-209">Linux 기반 HDInsight에서 Ambari Tez 보기 사용</span><span class="sxs-lookup"><span data-stu-id="8010d-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
