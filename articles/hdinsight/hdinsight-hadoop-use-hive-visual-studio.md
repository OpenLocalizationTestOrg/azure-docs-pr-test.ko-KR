---
title: "Visual Studio용 Data Lake(Hadoop) 도구를 사용한 Hive - Azure HDInsight | Microsoft Docs"
description: "Azure HDInsight의 Apache Hadoop에서 Data Lake Tools for Visual Studio를 사용하여 Apache Hive 쿼리를 실행하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="066de-103">Data Lake Tools for Visual Studio를 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="066de-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="066de-104">Data Lake Tools for Visual Studio를 사용하여 Apache Hive를 쿼리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="066de-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="066de-105">Data Lake 도구를 사용하면 Azure HDInsight에서 Hadoop에 대해 Hive 쿼리를 쉽게 만들고, 제출하고, 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066de-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="066de-106"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="066de-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="066de-107">Azure HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="066de-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="066de-108">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="066de-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="066de-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066de-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="066de-110">Visual Studio(다음 버전 중 하나)</span><span class="sxs-lookup"><span data-stu-id="066de-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="066de-111">Visual Studio 2013 Community/Professional/Premium/Ultimate 업데이트 4</span><span class="sxs-lookup"><span data-stu-id="066de-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="066de-112">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="066de-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="066de-113">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="066de-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="066de-114">Visual Studio용 HDInsight 도구 또는 Visual Studio용 Azure Data Lake 도구</span><span class="sxs-lookup"><span data-stu-id="066de-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="066de-115">도구 설치 및 구성에 대한 내용은 [HDInsight용 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066de-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="066de-116"><a id="run"></a> Visual Studio를 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="066de-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="066de-117">**Visual Studio**를 열고 **새로 만들기** > **프로젝트** > **Azure Data Lake** > **HIVE** > **Hive 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="066de-118">이 프로젝트에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="066de-119">이 프로젝트에서 만든 **Script.hql** 파일을 열고 아래 HiveQL 문을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="066de-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="066de-120">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="066de-121">`DROP TABLE`: 테이블이 있는 경우 이 문에서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="066de-122">`CREATE EXTERNAL TABLE`: Hive에서 새 '외부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="066de-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="066de-123">외부 테이블은 Hive에 테이블 정의만 저장하고, 데이터는 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066de-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="066de-124">외부 원본에서 기본 데이터를 업데이트하길 원하는 경우에는 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="066de-125">MapReduce 작업 또는 Azure 서비스를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066de-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="066de-126">외부 테이블을 삭제하면 데이터는 삭제되지 **않고** 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="066de-127">`ROW FORMAT`: 데이터의 형식 지정 방식을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="066de-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="066de-128">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="066de-129">`STORED AS TEXTFILE LOCATION`: 데이터가 저장된 위치(example/data 디렉터리) 및 텍스트로 저장되었음을 Hive에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="066de-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="066de-130">`SELECT`: `t4` 열에 `[ERROR]` 값이 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="066de-131">이 문에서는 이 값을 포함하는 행이 3개 있으므로 `3` 값이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="066de-132">`INPUT__FILE__NAME LIKE '%.log'` - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="066de-133">이 절은 데이터가 포함된 sample.log 파일로 검색을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="066de-134">도구 모음에서 쿼리에 사용할 **HDInsight 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="066de-135">**제출**을 선택하여 Hive 작업으로 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![제출 표시줄](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="066de-137">**Hive 작업 요약** 이 표시되고 실행 중인 작업 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="066de-138">**작업 상태**가 **완료**로 변경될 때까지 **새로 고침** 링크를 사용하여 작업 정보를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![완료된 작업을 표시하는 작업 요약](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="066de-140">이 작업의 출력을 보려면 **작업 출력** 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="066de-141">이 쿼리로 반환된 값으로 `[ERROR] 3`이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="066de-142">또한 프로젝트를 만들지 않고도 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="066de-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="066de-143">**서버 탐색기**에서 **Azure** > **HDInsight**를 확장하고, HDInsight 서버를 마우스 오른쪽 단추로 클릭한 다음 **Hive 쿼리 작성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="066de-144">나타나는 **temp.hql** 문서에서 다음 HiveQL 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="066de-145">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="066de-146">`CREATE TABLE IF NOT EXISTS`: 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="066de-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="066de-147">`EXTERNAL` 키워드가 사용되지 않으므로 이 문으로 내부 테이블이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="066de-148">내부 테이블은 Hive 데이터 웨어하우스에 저장되며 Hive에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="066de-149">`EXTERNAL` 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="066de-150">`STORED AS ORC`: 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="066de-151">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="066de-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="066de-152">`INSERT OVERWRITE ... SELECT`: `[ERROR]`가 포함된 `log4jLogs` 테이블에서 행을 선택하고 데이터를 `errorLogs` 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="066de-153">도구 모음에서 **제출** 을 선택하여 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="066de-154">**작업 상태** 를 사용하여 작업이 성공적으로 완료되었는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="066de-155">작업에서 테이블이 만들어졌는지 확인하려면 **서버 탐색기**를 사용하여 **Azure** > **HDInsight** > HDInsight 클러스터 > **Hive 데이터베이스** > **기본값**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="066de-156">**errorLogs** 및 **log4jLogs** 테이블이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="066de-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="066de-157"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="066de-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="066de-158">여기에서 볼 수 있듯이 Visual Studio용 HDInsight 도구는 HDInsight에서 Hive 쿼리를 수행하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="066de-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="066de-159">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="066de-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="066de-160">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="066de-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="066de-161">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="066de-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="066de-162">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="066de-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="066de-163">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="066de-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="066de-164">Visual Studio용 HDInsight 도구에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="066de-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="066de-165">Visual Studio용 HDInsight 도구 시작</span><span class="sxs-lookup"><span data-stu-id="066de-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
