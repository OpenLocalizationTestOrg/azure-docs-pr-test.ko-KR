---
title: "HDInsight에서 Hadoop Hive 및 원격 데스크톱 사용 - Azure | Microsoft Docs"
description: "원격 데스크톱을 사용하여 HDInsight의 Hadoop 클러스터에 연결한 다음 Hive CLI(명령줄 인터페이스)를 사용하여 Hive 쿼리를 실행하는 방법을 배웁니다."
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
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="322b5-103">원격 데스크톱을 사용하여 HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="322b5-104">이 문서에서는 원격 데스크톱을 사용하여 HDInsight 클러스터에 연결한 다음 Hive CLI(명령줄 인터페이스)를 사용하여 Hive 쿼리를 실행하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="322b5-105">원격 데스크톱은 Windows를 운영 체제로 사용하는 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="322b5-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="322b5-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="322b5-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="322b5-108">HDInsight 3.4 이상의 경우 명령줄에서, 클러스터에서 Hive 쿼리 직접 실행에 대한 자세한 내용은 [HDInsight 및 Beeline으로 Hive 사용](hdinsight-hadoop-use-hive-beeline.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="322b5-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="322b5-109"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="322b5-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="322b5-110">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="322b5-111">Windows 기반 HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="322b5-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="322b5-112">Windows 10, Window 8 또는 Windows 7을 실행하는 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="322b5-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="322b5-113"><a id="connect"></a>원격 데스크톱을 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="322b5-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="322b5-114">HDInsight 클러스터에 대해 원격 데스크톱을 사용하도록 설정한 다음 [RDP를 사용하여 HDInsight 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)의 지침에 따라 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="322b5-115"><a id="hive"></a>Hive 명령 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="322b5-116">HDInsight 클러스터용 데스크톱에 연결되면, Hive에서 작업하기 위해 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="322b5-117">HDInsight 데스크톱에서 **Hadoop 명령줄**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="322b5-118">Hive CLI를 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="322b5-119">CLI가 시작되면 Hive CLI 프롬프트 `hive>`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="322b5-120">CLI에서 다음 문을 입력하여 샘플 데이터를 사용하는 **log4jLogs** 라는 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="322b5-121">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="322b5-122">**DROP TABLE**: 테이블이 이미 있는 경우 테이블과 데이터 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="322b5-123">**CREATE EXTERNAL TABLE**: Hive에서 새 ‘외부’ 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="322b5-124">외부 테이블은 Hive에 테이블 정의만 저장하고, 데이터는 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="322b5-125">자동화된 데이터 업로드 프로세스와 같은 외부 원본이나 또 다른 MapReduce 작업을 통해 기본 데이터를 업데이트해야 하지만 Hive 쿼리에서 항상 최신 데이터를 사용하려고 할 경우 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="322b5-126">외부 테이블을 삭제하면 데이터는 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="322b5-127">**ROW FORMAT**: 데이터의 형식 지정 방식을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="322b5-128">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="322b5-129">**STORED AS TEXTFILE LOCATION**: 데이터가 저장된 위치(example/data 디렉터리)에 텍스트로 저장되었음을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="322b5-130">**SELECT**: **t4** 열에 **[ERROR]** 값이 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="322b5-131">이 경우 이 값을 포함하는 행이 3개 있으므로 **3** 값이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="322b5-132">**INPUT__FILE__NAME LIKE '%.log'** - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="322b5-133">데이터를 포함하는 sample.log 파일로 검색을 제한하며, 정의한 스키마와 일치하지 않는 다른 예제 데이터 파일의 데이터가 반환되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="322b5-134">다음 문을 사용하여 **errorLogs**라는 새 ‘내부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="322b5-135">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="322b5-136">**CREATE TABLE IF NOT EXISTS**: 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="322b5-137">**EXTERNAL** 키워드가 사용되지 않으면 Hive 데이터 웨어하우스에 저장되고 Hive에서 완전히 관리되는 내부 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="322b5-138">**EXTERNAL** 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="322b5-139">**STORED AS ORC**: 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="322b5-140">Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="322b5-141">**덮어쓰기 삽입... SELECT**: **[ERROR]**가 포함된 **log4jLogs** 테이블에서 행을 선택하고 데이터를 **errorLogs** 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="322b5-142">t4 열에 **[ERROR]**가 포함된 행만 **errorLogs** 테이블에 저장되었는지 확인하려면 다음 문을 사용하여 **errorLogs**의 모든 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="322b5-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="322b5-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="322b5-144">데이터 중 t4 열에 모두 **[ERROR]** 가 포함된 3개 행이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="322b5-145"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="322b5-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="322b5-146">여기에서 볼 수 있듯이 Hive 명령은 HDInsight 클러스터에서 Hive 쿼리 실행 작업 상태를 모니터링하고, 출력을 검색하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="322b5-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="322b5-147"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="322b5-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="322b5-148">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="322b5-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="322b5-149">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="322b5-150">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="322b5-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="322b5-151">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="322b5-152">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="322b5-153">Hive와 함께 Tez를 사용하는 경우 디버깅 정보에 대한 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="322b5-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="322b5-154">Windows 기반 HDInsight 클러스터에서 Tez UI 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="322b5-155">Linux 기반 HDInsight에서 Ambari Tez 보기 사용</span><span class="sxs-lookup"><span data-stu-id="322b5-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
