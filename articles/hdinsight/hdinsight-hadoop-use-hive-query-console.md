---
title: "HDInsight의 쿼리 콘솔에서 Hadoop Hive 사용 - Azure | Microsoft Docs"
description: "브라우저에서 웹 기반 쿼리 콘솔을 사용하여 HDInsight Hadoop 클러스터에 대한 Hive 쿼리를 실행하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="e96d2-103">쿼리 콘솔을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="e96d2-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="e96d2-104">이 문서에서는 브라우저에서 HDInsight Hadoop 클러스터의 Hive 쿼리를 실행하려면 HDInsight 쿼리 콘솔을 사용하는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e96d2-105">HDInsight 쿼리 콘솔은 Windows 기반 HDInsight 클러스터에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="e96d2-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e96d2-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e96d2-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="e96d2-108">HDInsight 3.4 이상의 경우 웹 브라우저에서 Hive 쿼리 실행에 대한 자세한 내용은 [Ambari Hive 보기에서 Hive 쿼리 실행](hdinsight-hadoop-use-hive-ambari-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e96d2-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="e96d2-109"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="e96d2-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="e96d2-110">이 문서의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="e96d2-111">Windows 기반 HDInsight Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="e96d2-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="e96d2-112">최신 웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="e96d2-112">A modern web browser</span></span>

## <span data-ttu-id="e96d2-113"><a id="run"></a> 쿼리 콘솔을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="e96d2-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="e96d2-114">웹 브라우저를 열고 **https://CLUSTERNAME.azurehdinsight.net**으로 이동합니다. 여기서 **CLUSTERNAME**은 HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="e96d2-115">메시지가 표시되면 클러스터를 만들 때 사용한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="e96d2-116">페이지 위쪽에 있는 링크 중 **Hive 편집기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="e96d2-117">HDInsight 클러스터에서 실행하려는 HiveQL 문을 입력하는 데 사용할 수 있는 양식이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![Hive 편집기](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="e96d2-119">`Select * from hivesampletable` 텍스트를 다음 HiveQL 문으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="e96d2-120">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="e96d2-121">**DROP TABLE**: 테이블이 이미 있는 경우 테이블과 데이터 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="e96d2-122">**CREATE EXTERNAL TABLE**: Hive에서 새 ‘외부’ 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="e96d2-123">외부 테이블은 Hive에 테이블 정의만 저장하고, 데이터는 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e96d2-124">자동화된 데이터 업로드 프로세스와 같은 외부 원본이나 또 다른 MapReduce 작업을 통해 기본 데이터를 업데이트해야 하지만 Hive 쿼리에서 항상 최신 데이터를 사용하려고 할 경우 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="e96d2-125">외부 테이블을 삭제하면 데이터는 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="e96d2-126">**ROW FORMAT**: 데이터의 형식 지정 방식을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="e96d2-127">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="e96d2-128">**STORED AS TEXTFILE LOCATION**: 데이터가 저장된 위치(example/data 디렉터리) 및 텍스트로 저장되었음을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="e96d2-129">**SELECT**: **t4** 열에 **[ERROR]** 값이 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="e96d2-130">이 경우 이 값을 포함하는 행이 3개 있으므로 **3** 값이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="e96d2-131">**INPUT__FILE__NAME LIKE '%.log'** - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="e96d2-132">데이터를 포함하는 sample.log 파일로 검색을 제한하며, 정의한 스키마와 일치하지 않는 다른 예제 데이터 파일의 데이터가 반환되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="e96d2-133">**Submit**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-133">Click **Submit**.</span></span> <span data-ttu-id="e96d2-134">페이지 아래쪽의 **작업 세션** 에는 작업에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="e96d2-135">**상태** 필드가 **완료**로 변경되면 작업에 대한 **세부 정보 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="e96d2-136">세부 정보 페이지의 **작업 출력**에는 `[ERROR]    3`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="e96d2-137">이 필드 아래의 **다운로드** 단추를 사용하여 작업의 출력을 포함하는 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="e96d2-138"><a id="summary"></a>요약</span><span class="sxs-lookup"><span data-stu-id="e96d2-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="e96d2-139">여기에서 볼 수 있듯이 Query 콘솔은 HDInsight 클러스터에서 Hive 쿼리 실행 작업 상태를 모니터링하고, 출력을 검색하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="e96d2-140">Hive 쿼리 콘솔을 사용하여 Hive 작업을 실행하는 방법에 대한 자세한 내용을 보려면 쿼리 콘솔의 위쪽에서 **시작** 을 선택한 다음 제공되는 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="e96d2-141">각 샘플은 샘플에 사용된 HiveQL 문의 설명을 포함하여 Hive를 사용하여 데이터를 분석하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e96d2-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="e96d2-142"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="e96d2-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="e96d2-143">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="e96d2-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="e96d2-144">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="e96d2-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="e96d2-145">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="e96d2-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e96d2-146">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="e96d2-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e96d2-147">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="e96d2-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e96d2-148">Hive와 함께 Tez를 사용하는 경우 디버깅 정보에 대한 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e96d2-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="e96d2-149">Windows 기반 HDInsight 클러스터에서 Tez UI 사용</span><span class="sxs-lookup"><span data-stu-id="e96d2-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="e96d2-150">Linux 기반 HDInsight에서 Ambari Tez 보기 사용</span><span class="sxs-lookup"><span data-stu-id="e96d2-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
