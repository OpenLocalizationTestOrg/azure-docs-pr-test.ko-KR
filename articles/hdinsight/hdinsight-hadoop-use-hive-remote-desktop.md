---
title: "aaaUse Hadoop 하이브 및 HDInsight-Azure의에서 원격 데스크톱 | Microsoft Docs"
description: "원격 데스크톱을 사용 하 여 HDInsight의 클러스터 tooconnect tooHadoop 방법을 알아보고 hello 하이브 명령줄 인터페이스를 사용 하 여 하이브 쿼리를 실행 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="5da31-103">원격 데스크톱을 사용하여 HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="5da31-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="5da31-104">이 문서에서는 hello 하이브 명령줄 인터페이스 (CLI)를 사용 하 여 HDInsight 클러스터 원격 데스크톱을 사용 하 여 다음을 실행 하이브 tooconnect tooan 쿼리 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5da31-105">원격 데스크톱은만 hello 운영 체제로 Windows를 사용 하는 HDInsight 클러스터에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="5da31-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5da31-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5da31-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="5da31-108">참조에 대 한 HDInsight 3.4 또는 큰 [HDInsight Beeline와 사용 하 여 하이브](hdinsight-hadoop-use-hive-beeline.md) 명령줄에서 직접 hello 클러스터에서 하이브 쿼리 실행에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="5da31-109"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="5da31-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="5da31-110">이 문서의 toocomplete hello 단계 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="5da31-111">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="5da31-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="5da31-112">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="5da31-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="5da31-113"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="5da31-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="5da31-114">Hello HDInsight 클러스터에 대 한 원격 데스크톱을 사용 합니다. 다음 hello 지침에 따라 tooit 연결 [RDP를 사용 하 여 tooHDInsight 클러스터 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="5da31-115"><a id="hive"></a>Hello 하이브 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5da31-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="5da31-116">Hello HDInsight 클러스터에 대해 toohello 데스크톱에 연결 했으므로 때 하이브가 있는 toowork 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="5da31-117">Hello HDInsight 바탕 화면에서 시작 hello **Hadoop 명령줄**합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="5da31-118">Hello 명령 toostart hello 하이브 CLI 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="5da31-119">나타납니다 hello CLI 시작 되 면 hello 하이브 CLI 프롬프트: `hive>`합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="5da31-120">Hello CLI를 사용 하 여 hello 문을 toocreate 라는 새 테이블을 다음 입력 **log4jLogs** 예제 데이터를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5da31-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="5da31-121">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5da31-122">**DROP TABLE**: hello 테이블이 이미 있는 경우 hello 테이블 및 hello 데이터 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="5da31-123">**CREATE EXTERNAL TABLE**: Hive에서 새 ‘외부’ 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="5da31-124">외부 테이블 (데이터는 hello 원래 위치에 그대로 남아 hello) 하이브에 hello 테이블 정의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="5da31-125">외부 소스 (예: 자동화 된 데이터 업로드 프로세스) 또는 다른 MapReduce 작업을 업데이트할 데이터 toobe 기본 hello 예상 으로만 toouse hello에 대 한 최신 데이터를 쿼리 하는 하이브 항상 하려는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="5da31-126">외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="5da31-127">**행 형식**: hello 데이터 형식 지정 방법을 하이브 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="5da31-128">이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="5da31-129">**AS 텍스트 파일 저장 위치**: hello 데이터를 하이브 지시 (hello 예제/데이터 디렉터리)를 저장 하 고 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="5da31-130">**선택**: 모든 행의 개수를 선택 합니다. 여기서 열 **t4** hello 값이 포함 된 **[오류]**합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="5da31-131">이 경우 이 값을 포함하는 행이 3개 있으므로 **3** 값이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="5da31-132">**INPUT__FILE__NAME LIKE '%.log'** - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="5da31-133">이 제한 hello 검색 toohello sample.log 파일 hello 데이터가 포함 되 고 반환 하는 데이터 다른 예제에서 정의한 hello 스키마와 일치 하지 않는 데이터 파일 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="5da31-134">다음 문은 toocreate 라는 새 'internal' 테이블이 사용 하 여 hello **살펴볼**:</span><span class="sxs-lookup"><span data-stu-id="5da31-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="5da31-135">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5da31-136">**CREATE TABLE IF NOT EXISTS**: 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="5da31-137">때문에 hello **외부** 이 hello 하이브 데이터 웨어하우스에 저장 된 Hive에서 완전히 관리 되 고 있는 내부 테이블에는, 키워드가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5da31-138">와 달리 **외부** hello 내부 데이터를 삭제 하는 테이블의 경우 내부 테이블도 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="5da31-139">**AS ORC 저장**: 최적화 된 행의 열 (ORC) 형식의 hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="5da31-140">Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="5da31-141">**덮어쓰기 삽입... 선택**: hello에서 행을 선택 **log4jLogs** 이 있는 테이블 **[오류]**, 삽입 hello에 데이터를 hello 다음 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="5da31-142">포함 하는 행만 tooverify **[오류]** 열 t4 저장된 toohello 있었습니다 **살펴볼** 테이블에서 다음 행에서 hello 모든 문을 tooreturn hello를 사용 하 여 **살펴볼**:</span><span class="sxs-lookup"><span data-stu-id="5da31-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="5da31-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="5da31-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="5da31-144">데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="5da31-145"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="5da31-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="5da31-146">볼 수 있듯이 hello hello 하이브 명령을 제공 하는 HDInsight 클러스터에서 하이브 쿼리를 실행 하는 쉽게 toointeractively, 모니터 hello 상태, 작업 및 hello 출력을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5da31-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="5da31-147"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="5da31-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="5da31-148">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="5da31-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="5da31-149">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="5da31-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="5da31-150">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="5da31-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5da31-151">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="5da31-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5da31-152">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="5da31-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5da31-153">Tez 하이브가 있는 사용 하는 경우 hello 다음 디버깅 정보에 대 한 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5da31-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="5da31-154">Windows 기반 HDInsight의 hello Tez UI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5da31-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="5da31-155">Linux 기반 HDInsight에서 Ambari Tez 보기 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5da31-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
