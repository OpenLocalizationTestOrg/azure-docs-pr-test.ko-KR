---
title: "데이터 레이크 (Hadoop) tools for Visual Studio-Azure HDInsight aaaHive | Microsoft Docs"
description: "어떻게 toouse hello 데이터 레이크 용 도구 Visual Studio toorun Apache Hive Azure HDInsight의 Apache Hadoop으로 쿼리를 알아봅니다."
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
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7e073-103">Visual Studio에 대 한 hello 데이터 레이크 도구를 사용 하는 하이브 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="7e073-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7e073-104">Apache Hive는 Visual Studio tooquery 용 toouse hello 데이터 레이크 도구 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="7e073-105">데이터 레이크 도구 hello 허용 tooeasily 만들고, 제출 하 고 Azure HDInsight의 Hive 쿼리 tooHadoop를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="7e073-106"><a id="prereq"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="7e073-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7e073-107">Azure HDInsight(HDInsight의 Hadoop) 클러스터</span><span class="sxs-lookup"><span data-stu-id="7e073-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7e073-108">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7e073-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e073-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7e073-110">Visual Studio (hello 버전을 다음 중 하나):</span><span class="sxs-lookup"><span data-stu-id="7e073-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="7e073-111">Visual Studio 2013 Community/Professional/Premium/Ultimate 업데이트 4</span><span class="sxs-lookup"><span data-stu-id="7e073-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="7e073-112">Visual Studio 2015(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="7e073-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="7e073-113">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="7e073-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="7e073-114">Visual Studio용 HDInsight 도구 또는 Visual Studio용 Azure Data Lake 도구</span><span class="sxs-lookup"><span data-stu-id="7e073-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="7e073-115">참조 [HDInsight에 대 한 Visual Studio Hadoop 도구 사용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md) 설치 및 구성 hello 도구에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="7e073-116"><a id="run"></a>Hello Visual Studio를 사용 하 여 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="7e073-117">**Visual Studio**를 열고 **새로 만들기** > **프로젝트** > **Azure Data Lake** > **HIVE** > **Hive 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="7e073-118">이 프로젝트에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="7e073-119">열기 hello **Script.hql** 이 프로젝트 및 다음 HiveQL 조건 hello에 붙여넣기를 사용 하 여 만든 파일:</span><span class="sxs-lookup"><span data-stu-id="7e073-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="7e073-120">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7e073-121">`DROP TABLE`: Hello 테이블이 존재 하는 경우이 문은으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="7e073-122">`CREATE EXTERNAL TABLE`: Hive에서 새 '외부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="7e073-123">외부 테이블 (데이터는 hello 원래 위치에 그대로 남아 hello) 하이브에 hello 테이블 정의만 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="7e073-124">외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="7e073-125">MapReduce 작업 또는 Azure 서비스를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="7e073-126">외부 테이블 삭제는 **하지** hello 데이터를 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="7e073-127">`ROW FORMAT`: 하이브 hello 데이터 형식 지정 방법을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="7e073-128">이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="7e073-129">`STORED AS TEXTFILE LOCATION`: 지시 하이브 여기서 hello 데이터가 저장 됩니다 (hello 예제/데이터 디렉터리) 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="7e073-130">`SELECT`: 모든 행의 개수를 선택 합니다. 여기서 열 `t4` hello 값이 포함 된 `[ERROR]`합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="7e073-131">이 문에서는 이 값을 포함하는 행이 3개 있으므로 `3` 값이 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="7e073-132">`INPUT__FILE__NAME LIKE '%.log'` - .log로 끝나는 파일의 데이터만 반환하도록 Hive에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="7e073-133">이 절 hello 데이터가 포함 된 hello 검색 toohello sample.log 파일을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="7e073-134">Hello 도구 모음에서 선택 hello **HDInsight 클러스터** 이 쿼리에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="7e073-135">선택 **전송** 하이브 작업으로 toorun hello 문.</span><span class="sxs-lookup"><span data-stu-id="7e073-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![제출 표시줄](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="7e073-137">hello **작업 요약 하이브** 표시 되 고 작업을 실행 하는 hello에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="7e073-138">사용 하 여 hello **새로 고침** hello까지 toorefresh hello 작업 정보를 연결 **작업 상태** 쪽 변경**Completed**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![완료된 작업을 표시하는 작업 요약](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="7e073-140">사용 하 여 hello **작업 출력** 이 작업의 tooview hello 출력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="7e073-141">표시 `[ERROR] 3`, 값은이 쿼리에서 반환 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="7e073-142">또한 프로젝트를 만들지 않고도 Hive 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="7e073-143">**서버 탐색기**에서 **Azure** > **HDInsight**를 확장하고, HDInsight 서버를 마우스 오른쪽 단추로 클릭한 다음 **Hive 쿼리 작성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="7e073-144">Hello에 **temp.hql** 나타나는 문서 hello 다음 HiveQL 조건 추가:</span><span class="sxs-lookup"><span data-stu-id="7e073-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="7e073-145">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="7e073-146">`CREATE TABLE IF NOT EXISTS`: 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="7e073-147">때문에 hello `EXTERNAL` 키워드가 사용 되지 않습니다,이 문은 내부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="7e073-148">내부 테이블 hello 하이브 데이터 웨어하우스에 저장 되 고 하이브에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7e073-149">와 달리 `EXTERNAL` hello 내부 데이터를 삭제 하는 테이블의 경우 내부 테이블도 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="7e073-150">`STORED AS ORC`: 저장소 hello 최적화 된 행의 열 (ORC) 형식 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="7e073-151">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="7e073-152">`INSERT OVERWRITE ... SELECT`: Hello에서 행을 선택 합니다. `log4jLogs` 이 있는 테이블 `[ERROR]`, 삽입 hello에 데이터를 hello 다음 `errorLogs` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="7e073-153">Hello 도구 모음에서 선택 **전송** toorun hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="7e073-154">사용 하 여 hello **작업 상태** toodetermine 해당 hello 작업이 성공적으로 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="7e073-155">작업을 만들었습니다. hello 테이블을 사용 하 여 hello tooverify **서버 탐색기** 확장 **Azure** > **HDInsight** > HDInsight 클러스터에 > **하이브 데이터베이스** > **기본**합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="7e073-156">hello **살펴볼** 테이블과 hello **log4jLogs** 테이블 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="7e073-157"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e073-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7e073-158">볼 수 있듯이 Visual Studio 용 HDInsight 도구 hello HDInsight의 Hive 쿼리를 쉽게 toowork를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e073-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="7e073-159">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="7e073-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="7e073-160">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="7e073-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7e073-161">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="7e073-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7e073-162">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="7e073-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="7e073-163">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="7e073-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7e073-164">Hello에 대 한 자세한 내용은 Visual Studio 용 HDInsight 도구:</span><span class="sxs-lookup"><span data-stu-id="7e073-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="7e073-165">Visual Studio용 HDInsight 도구 시작</span><span class="sxs-lookup"><span data-stu-id="7e073-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
