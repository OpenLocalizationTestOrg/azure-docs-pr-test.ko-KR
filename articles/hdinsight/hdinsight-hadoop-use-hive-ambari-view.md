---
title: "Ambari 보기를 사용하여 HDInsight(Hadoop)에서 Hive 작업 - Azure | Microsoft Docs"
description: "웹 브라우저에서 Hive 뷰를 사용하여 Hive 쿼리를 제출하는 방법을 알아봅니다. Hive 뷰는 Linux 기반 HDInsight 클러스터와 함께 제공되는 Ambari 웹 UI의 일부입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="2875e-104">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2875e-105">Ambari Hive View를 사용하여 Hive 쿼리를 실행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="2875e-106">Ambari는 Linux 기반 HDInsight 클러스터와 함께 제공되는 관리 및 모니터링 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="2875e-107">Ambari를 통해 제공되는 기능 중 하나는 Hive 쿼리를 실행하는 데 사용할 수 있는 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="2875e-108">Ambari에는 이 문서에 설명되지 않은 여러 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="2875e-109">자세한 내용은 [Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리](hdinsight-hadoop-manage-ambari.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2875e-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2875e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2875e-110">Prerequisites</span></span>

* <span data-ttu-id="2875e-111">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2875e-112">클러스터를 만드는 방법에 대한 정보는 [Linux 기반 HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2875e-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2875e-113">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2875e-114">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2875e-115">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2875e-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="2875e-116">Hive 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-116">Open the Hive view</span></span>

<span data-ttu-id="2875e-117">Azure Portal에서 HDInsight 클러스터를 선택한 다음 **빠른 링크** 섹션에서 **Ambari 보기**를 선택하면 Ambari 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![포털의 빠른 링크 섹션](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="2875e-119">보기 목록에서 __Hive 보기__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-119">From the list of views, select the __Hive View__.</span></span>

![Hive 보기 선택](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="2875e-121">Ambari에 액세스할 때 사이트에 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="2875e-122">클러스터를 만들 때 사용한 관리자(기본값 `admin`) 계정 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="2875e-123">다음 이미지와 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-123">You should see a page similar to the following image:</span></span>

![Hive 보기에 대한 쿼리 워크시트 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="2875e-125"><a name="hivequery"></a>쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="2875e-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="2875e-126">Hive 쿼리를 실행하려면 Hive 보기에서 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="2875e-127">__쿼리__ 탭에서 다음 HiveQL 문을 워크시트에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="2875e-128">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2875e-129">`DROP TABLE` - 테이블이 이미 있는 경우 테이블과 데이터 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="2875e-130">`CREATE EXTERNAL TABLE` - Hive에서 새 '외부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="2875e-131">외부 테이블은 테이블 정의만 Hive에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="2875e-132">데이터는 원래 위치에 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="2875e-133">`ROW FORMAT` - 데이터의 형식을 지정하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="2875e-134">이 경우, 각 로그의 필드는 공백으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="2875e-135">`STORED AS TEXTFILE LOCATION` - 데이터가 저장된 위치 및 텍스트로 저장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="2875e-136">`SELECT` - 열 t4에 값 [ERROR]가 포함된 모든 행의 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="2875e-137">외부 원본에서 기본 데이터를 업데이트하길 원하는 경우에는 외부 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="2875e-138">예: 자동화된 데이터 업로드 프로세스나 또 다른 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="2875e-139">외부 테이블을 삭제하면 데이터는 삭제되지 *않고* 테이블 정의만 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2875e-140">__데이터베이스__ 선택 영역을 __기본값__으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="2875e-141">이 문서의 예제에서는 HDInsight에 포함된 기본 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="2875e-142">쿼리를 시작하려면 워크시트 아래에서 **실행** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="2875e-143">그러면 주황색으로 바뀌고 텍스트가 **중지**로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="2875e-144">쿼리가 완료되면 **결과** 탭에 작업 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="2875e-145">다음 텍스트는 쿼리 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="2875e-146">**로그** 탭을 사용하면 작업에서 생성된 로깅 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="2875e-147">**프로세스 결과 쿼리** 섹션 맨 위 왼쪽에서 **결과 저장** 드롭다운 대화 상자를 사용하여 결과를 다운로드하거나 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="2875e-148">이 쿼리의 처음 네 줄을 선택한 다음 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="2875e-149">작업이 완료되어도 결과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="2875e-150">쿼리의 일부를 선택했을 때 **실행** 단추를 사용하면 선택한 문만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="2875e-151">이 예에서는 테이블에서 행을 검색하는 최종 문이 선택한 네 줄에 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="2875e-152">해당 줄만 선택하고 **실행**단추를 사용하면 예상된 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="2875e-153">워크시트를 추가하려면 **쿼리 편집기** 아래쪽의 **새 워크시트** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="2875e-154">새 워크시트에 다음 HiveQL 문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="2875e-155">이러한 문은 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2875e-156">**CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="2875e-157">**EXTERNAL** 키워드가 사용되지 않으므로 내부 테이블이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="2875e-158">내부 테이블은 Hive 데이터 웨어하우스에 저장되며 Hive에서 전적으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="2875e-159">외부 테이블과 달리 내부 테이블을 삭제하면 기본 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="2875e-160">**STORED AS ORC** - 데이터를 ORC(Optimized Row Columnar) 형식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="2875e-161">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="2875e-162">**덮어쓰기 삽입... SELECT** - `[ERROR]`가 포함된 **log4jLogs** 테이블에서 행을 선택한 다음 **errorLogs** 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="2875e-163">**실행** 단추를 사용하여 해당 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="2875e-164">쿼리가 0개의 행을 반환할 때 **결과** 탭에는 어떠한 정보도 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="2875e-165">쿼리가 완료되면 상태는 **SUCCEEDED**로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="2875e-166">시각적 개체 설명</span><span class="sxs-lookup"><span data-stu-id="2875e-166">Visual explain</span></span>

<span data-ttu-id="2875e-167">쿼리 계획의 시각화를 표시하려면 워크시트 아래에서 **시각적 개체 설명** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="2875e-168">쿼리의 **시각적 개체 설명** 보기는 복잡한 쿼리 흐름을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="2875e-169">[쿼리 편집기]의 **설명** 단추를 사용하면 이 보기에 해당하는 텍스트 명령을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="2875e-170">Tez UI</span><span class="sxs-lookup"><span data-stu-id="2875e-170">Tez UI</span></span>

<span data-ttu-id="2875e-171">쿼리에 대한 Tez UI를 표시하려면 워크시트 아래에서 **Tez** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2875e-172">Tez는 모든 쿼리를 해결하는 데 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="2875e-173">많은 쿼리는 Tez를 사용하지 않고도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="2875e-174">Tez가 쿼리를 해결하는 데 사용된 경우 DAG(방향성 비순환 그래프)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="2875e-175">이전에 실행한 쿼리에 대한 DAG를 보거나 Tez 프로세스를 디버그하려면 [Tez 뷰](hdinsight-debug-ambari-tez-view.md) 를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="2875e-176">작업 기록 보기</span><span class="sxs-lookup"><span data-stu-id="2875e-176">View job history</span></span>

<span data-ttu-id="2875e-177">__작업__ 탭에 Hive 쿼리의 기록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![작업 기록 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="2875e-179">데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="2875e-179">Database tables</span></span>

<span data-ttu-id="2875e-180">__테이블__ 탭을 사용하여 Hive 데이터베이스 내의 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![테이블 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="2875e-182">저장된 쿼리</span><span class="sxs-lookup"><span data-stu-id="2875e-182">Saved queries</span></span>

<span data-ttu-id="2875e-183">쿼리 탭에서 필요에 따라 쿼리를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="2875e-184">쿼리를 저장하면 __저장된 쿼리__ 탭에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![저장된 쿼리 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="2875e-186">사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="2875e-186">User-defined functions</span></span>

<span data-ttu-id="2875e-187">Hive는 UDF(사용자 정의 함수)를 통해 확장될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="2875e-188">UDF를 사용하면 HiveQL에서 쉽게 모델링할 수 있는 기능 또는 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="2875e-189">Hive 보기 위쪽의 UDF 탭에서는 UDF 집합을 선언하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="2875e-190">UDF는 **쿼리 편집기**를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-190">These UDFs can be used with the **Query Editor**.</span></span>

![UDF 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="2875e-192">UDF를 Hive 보기에 추가하면 **쿼리 편집기** 아래쪽에 **udf 삽입** 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="2875e-193">이 항목을 선택하면 Hive 뷰에서 정의된 UDF의 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="2875e-194">UDF를 선택하면 쿼리에 HiveQL 문을 추가하여 UDF를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="2875e-195">예를 들어 다음 속성으로 UDF를 정의하는 경우:</span><span class="sxs-lookup"><span data-stu-id="2875e-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="2875e-196">리소스 이름: myudfs</span><span class="sxs-lookup"><span data-stu-id="2875e-196">Resource name: myudfs</span></span>

* <span data-ttu-id="2875e-197">리소스 경로: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="2875e-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="2875e-198">UDF 이름: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="2875e-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="2875e-199">UDF 클래스 이름: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="2875e-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="2875e-200">**udf 삽입** 단추를 사용하면 해당 리소스에 정의된 각 UDF에 대한 또 다른 드롭다운 목록과 함께 **myudfs**라는 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="2875e-201">이 경우 **myawesomeudf**입니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="2875e-202">이 항목을 선택하면 쿼리의 시작 부분에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="2875e-203">그런 다음 쿼리에서 UDF를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="2875e-204">예: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="2875e-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="2875e-205">HDInsight에서 Hive를 통해 UDF를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2875e-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="2875e-206">HDInsight에서 Hive 및 Pig와 함께 Python 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="2875e-207">HDInsight에 사용자 지정 하이브 UDF를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2875e-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="2875e-208">Hive 설정</span><span class="sxs-lookup"><span data-stu-id="2875e-208">Hive settings</span></span>

<span data-ttu-id="2875e-209">설정을 사용하여 다양한 Hive 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="2875e-210">예를 들어 Tez(기본값)에서 MapReduce로 Hive에 대한 실행 엔진을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2875e-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="2875e-211"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="2875e-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="2875e-212">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="2875e-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="2875e-213">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2875e-214">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="2875e-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2875e-215">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2875e-216">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="2875e-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
