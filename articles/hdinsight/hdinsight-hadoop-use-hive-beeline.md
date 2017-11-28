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
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="abea9-105">Apache Hive와 hello Beeline 클라이언트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="abea9-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="abea9-106">자세한 방법을 toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) HDInsight의 Hive toorun를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="abea9-107">Beeline는 HDInsight 클러스터의 헤드 노드에 hello에 포함 된 하이브 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="abea9-108">Beeline는 JDBC tooconnect tooHiveServer2 HDInsight 클러스터에서 호스트 되는 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="abea9-109">HDInsight에 Beeline tooaccess 하이브 이상 원격으로 사용할 수도 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="abea9-110">다음 표에서 hello Beeline와 함께 사용할 연결 문자열을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="abea9-111">Beeline을 실행하는 위치</span><span class="sxs-lookup"><span data-stu-id="abea9-111">Where you run Beeline from</span></span> | <span data-ttu-id="abea9-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abea9-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abea9-113">SSH 연결 tooa 헤드 노드에 또는 가장자리 노드</span><span class="sxs-lookup"><span data-stu-id="abea9-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="abea9-114">외부 hello 클러스터</span><span class="sxs-lookup"><span data-stu-id="abea9-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="abea9-115">대체 `admin` 클러스터에 대 한 hello 클러스터 로그인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="abea9-116">대체 `password` hello 클러스터 로그인 계정에 대 한 hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="abea9-117">대체 `clustername` HDInsight 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="abea9-118"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="abea9-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="abea9-119">HDInsight 클러스터의 Linux 기반 Hadoop</span><span class="sxs-lookup"><span data-stu-id="abea9-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="abea9-120">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="abea9-121">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abea9-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="abea9-122">SSH 클라이언트 또는 로컬 Beeline 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="abea9-123">대부분의 hello이이 문서의 단계 Beeline SSH 세션 toohello 클러스터에서 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="abea9-124">참조 hello Beeline hello 클러스터 외부에서 실행에 대 한 내용은 [Beeline를 원격으로 사용 하 여](#remote) 섹션.</span><span class="sxs-lookup"><span data-stu-id="abea9-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="abea9-125">SSH를 사용하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abea9-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="abea9-126"><a id="beeline"></a>Beeline 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="abea9-127">Beeline을 시작할 때 HDInsight 클러스터에서 HiveServer2에 대한 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="abea9-128">hello 클러스터 외부에서 toorun hello 명령을 제공 해야 hello 클러스터 로그인 계정 이름 (기본 `admin`) 및 암호.</span><span class="sxs-lookup"><span data-stu-id="abea9-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="abea9-129">다음 테이블 toofind hello 연결 문자열 형식 및 매개 변수 toouse hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="abea9-130">Beeline을 실행하는 위치</span><span class="sxs-lookup"><span data-stu-id="abea9-130">Where you run Beeline from</span></span> | <span data-ttu-id="abea9-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="abea9-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="abea9-132">SSH 연결 tooa 헤드 노드에 또는 가장자리 노드</span><span class="sxs-lookup"><span data-stu-id="abea9-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="abea9-133">외부 hello 클러스터</span><span class="sxs-lookup"><span data-stu-id="abea9-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="abea9-134">예를 들어 다음 명령을 hello SSH 세션 toohello 클러스터에서 사용 되는 toostart Beeline 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="abea9-135">이 명령은 hello Beeline 클라이언트를 시작 하 고 tooHiveServer2 hello 클러스터 헤드 노드에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="abea9-136">Hello 명령이 완료 된 후 본사에 도착 하면는 `jdbc:hive2://headnodehost:10001/>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="abea9-137">Beeline 명령은 일반적으로 `!` 문자로 시작합니다. 예를 들어 `!help`는 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="abea9-138">그러나 hello `!` 일부 명령에 대 한 생략 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="abea9-139">예를 들어 `help`도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-139">For example, `help` also works.</span></span>

    <span data-ttu-id="abea9-140">`!sql`, 어떤 HiveQL 문은 tooexecute 사용된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="abea9-141">그러나 HiveQL 하므로 일반적으로 사용 되므로 이전 hello를 생략할 수 있습니다 `!sql`합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="abea9-142">다음 두 조건 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="abea9-143">새 클러스터에서는 **hivesampletable**이라는 테이블 하나만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="abea9-144">Hello hivesampletable에 대 한 명령 toodisplay hello 스키마를 따르는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="abea9-145">이 명령은 hello 다음 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="abea9-146">이 정보는 hello 테이블의 hello 열에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="abea9-147">이 데이터에 대 한 일부 쿼리를 수행할 수 있습니다, 동안 대신 만들겠습니다 완전히 새로운 테이블 toodemonstrate 어떻게 하이브에 tooload 데이터 및 스키마를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="abea9-148">Hello 문을 toocreate 라는 테이블을 다음 입력 **log4jLogs** hello HDInsight 클러스터와 함께 제공 되는 샘플 데이터를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="abea9-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="abea9-149">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="abea9-150">`DROP TABLE`-Hello 테이블이 있는 경우 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="abea9-151">`CREATE EXTERNAL TABLE` - Hive에서 **외부** 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="abea9-152">외부 테이블만 하이브에 hello 테이블 정의 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="abea9-153">hello 데이터는 hello 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="abea9-154">`ROW FORMAT`-어떻게 hello 데이터의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="abea9-155">이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="abea9-156">`STORED AS TEXTFILE LOCATION`-Hello 데이터가 저장 되 고 어떤 파일 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="abea9-157">`SELECT`-모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="abea9-158">이 값을 포함하는 세 개의 행이 있으므로 이 쿼리는 **3** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="abea9-159">`INPUT__FILE__NAME LIKE '%.log'`-하이브 tooapply hello 스키마 tooall hello 디렉터리에 파일을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="abea9-160">이 경우 hello 디렉터리 hello 스키마와 일치 하지 않는 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="abea9-161">tooprevent 가비지 데이터 hello 결과에,이 문은 알 수 하이브 것만 반환할지 여부를 데이터 파일의 끝에서. 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="abea9-162">외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="abea9-163">예를 들어 자동화된 데이터 업로드 프로세스 또는 MapReduce 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="abea9-164">외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="abea9-165">hello이 명령의 비슷한 toohello 팔 로우 텍스트 출력:</span><span class="sxs-lookup"><span data-stu-id="abea9-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="abea9-166">tooexit Beeline를 사용 하 여 `!exit`합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="abea9-167"><a id="file"></a>Beeline toorun HiveQL 파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="abea9-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="abea9-168">다음 단계는 파일 toocreate Beeline를 사용 하 여를 실행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="abea9-169">사용 하 여 hello 다음 명령은 toocreate 이라는 파일로 내보내집니다 **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="abea9-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="abea9-170">콘텐츠로 사용 hello hello 파일 텍스트를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="abea9-171">이 쿼리는 **errorLogs**라는 새 '내부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="abea9-172">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="abea9-173">**만들 테이블 IF NOT EXISTS** -hello 테이블이 아직 없는 경우 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="abea9-174">Hello 이후 **외부** 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="abea9-175">내부 테이블 hello 하이브 데이터 웨어하우스에 저장 되 고 하이브에서 완전히 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="abea9-176">**AS ORC 저장** -hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="abea9-177">ORC 형식은 Hive 데이터를 저장하기 위해 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="abea9-178">**덮어쓰기 삽입... 선택** -hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="abea9-179">외부 테이블의 경우와 달리 hello 기본 데이터도 삭제 내부 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="abea9-180">toosave hello 파일을 사용 하 여 **Ctrl**+**_X**, 다음 입력 **Y**, 마지막으로 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="abea9-181">다음 toorun hello 파일 Beeline를 사용 하 여 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="abea9-182">hello `-i` 매개 변수 Beeline 시작, 실행 hello hello query.hql 파일에는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="abea9-183">Hello에 도착 하는 hello 쿼리 완료 되 면 `jdbc:hive2://headnodehost:10001/>` 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="abea9-184">Hello를 사용 하는 파일을 실행할 수도 있습니다 `-f` 매개 변수는 hello 쿼리 완료 후 Beeline 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="abea9-185">hello tooverify **살펴볼** 테이블을 만든 다음 행에서 hello 모든 문을 tooreturn hello를 사용 하 여, **살펴볼**:</span><span class="sxs-lookup"><span data-stu-id="abea9-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="abea9-186">데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="abea9-187"><a id="remote"></a>Beeline을 원격으로 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="abea9-188">로컬에 설치 되어 Beeline 했거나 사용 Docker 이미지를 통해와 같은 경우 [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), 매개 변수 뒤 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="abea9-189">__연결 문자열__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="abea9-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="abea9-190">__클러스터 로그인 이름__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="abea9-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="abea9-191">__클러스터 로그인 암호__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="abea9-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="abea9-192">Hello 대체 `clustername` HDInsight 클러스터의 hello 이름의 hello 연결 문자열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="abea9-193">대체 `admin` 클러스터 로그인 및 바꾸기의 hello 이름의 `password` 클러스터 로그인에 대 한 hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="abea9-194"><a id="sparksql"></a>Spark와 함께 Beeline 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="abea9-195">Spark는 종종 참조 된 tooas hello Spark Thrift 서버는 HiveServer2의 자체 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="abea9-196">이 서비스는 하이브를 대신 Spark SQL tooresolve 쿼리를 사용 하며 쿼리에 따라 더 나은 성능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="abea9-197">HDInsight 클러스터를 사용 하 여 포트의 Spark의 tooconnect toohello Spark Thrift 서버 `10002` 대신 `10001`합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="abea9-198">예: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="abea9-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abea9-199">hello Spark Thrift 서버가 액세스할 수 있는 조치 hello 인터넷 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="abea9-200">만 tooit 대 한 SSH 세션에서 연결 하거나 HDInsight 클러스터를 hello 대로 hello 동일한 Azure 가상 네트워크 내 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abea9-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="abea9-201"><a id="summary"></a><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="abea9-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="abea9-202">HDInsight의 Hive 대 한 일반적인 정보에 대 한 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="abea9-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="abea9-203">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="abea9-204">HDInsight의 Hadoop 작업할 수는 다른 방법에 대 한 자세한 내용은 다음 문서는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="abea9-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="abea9-205">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="abea9-206">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="abea9-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="abea9-207">Tez 하이브가 있는 사용 하는 경우 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="abea9-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="abea9-208">Windows 기반 HDInsight의 hello Tez UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="abea9-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="abea9-209">Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="abea9-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
