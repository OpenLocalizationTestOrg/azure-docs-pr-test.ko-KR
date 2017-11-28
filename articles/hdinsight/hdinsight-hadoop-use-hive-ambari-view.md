---
title: "하이브 (Hadoop)-Azure HDInsight에 있는 aaaUse Ambari 뷰 toowork | Microsoft Docs"
description: "웹 브라우저 toosubmit 하이브 쿼리에서 toouse 하이브 보기 hello 하는 방법에 대해 알아봅니다. hello 하이브 보기에는 Linux 기반 HDInsight 클러스터와 Ambari 웹 UI를 제공 하는 hello의 일부입니다."
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
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="f083d-104">HDInsight에서 Hadoop으로 hello 하이브 보기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f083d-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="f083d-105">Ambari 하이브 보기를 사용 하 여 하이브 toorun을 쿼리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="f083d-106">Ambari는 Linux 기반 HDInsight 클러스터와 함께 제공되는 관리 및 모니터링 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="f083d-107">Ambari를 통해 제공 하는 hello 기능 중 하나 사용 하는 toorun 하이브 쿼리 될 수 있는 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="f083d-108">Ambari에는 이 문서에 설명되지 않은 여러 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="f083d-109">자세한 내용은 참조 [hello Ambari 웹 UI를 사용 하 여 관리 하는 HDInsight 클러스터](hdinsight-hadoop-manage-ambari.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f083d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f083d-110">Prerequisites</span></span>

* <span data-ttu-id="f083d-111">Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="f083d-112">클러스터를 만드는 방법에 대한 정보는 [Linux 기반 HDInsight 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f083d-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f083d-113">이 문서의 단계 hello Linux를 사용 하는 HDInsight 클러스터를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="f083d-114">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f083d-115">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f083d-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="f083d-116">Hello 하이브 보기 열기</span><span class="sxs-lookup"><span data-stu-id="f083d-116">Open hello Hive view</span></span>

<span data-ttu-id="f083d-117">Ambari 뷰 hello; Azure 포털에서에서 할 수 있습니다. HDInsight 클러스터를 선택한 다음 선택 **Ambari 뷰** hello에서 **빠른 링크** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f083d-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![hello 포털의 빠른 링크 섹션](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="f083d-119">뷰의 hello 목록에서 선택 hello __하이브 보기__합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-119">From hello list of views, select hello __Hive View__.</span></span>

![hello 하이브 보기가 선택](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="f083d-121">Ambari를 액세스할 때 메시지 표시 tooauthenticate toohello 사이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="f083d-122">Admin 님 안녕하세요 입력 (기본 `admin`) 계정 이름 및 암호를 만들 때 사용한 hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="f083d-123">다음 이미지는 페이지와 유사한 toohello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-123">You should see a page similar toohello following image:</span></span>

![Hello 하이브 보기에 대 한 hello 쿼리 워크시트의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="f083d-125"><a name="hivequery"></a>쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="f083d-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="f083d-126">하이브 쿼리 toorun hello hello 하이브 보기에서 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="f083d-127">Hello에서 __쿼리__ 탭에서 다음 HiveQL 조건 hello 워크시트로 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="f083d-128">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f083d-129">`DROP TABLE`-Hello 테이블이 이미 존재 하는 경우 사용할 삭제 hello 테이블 및 hello 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="f083d-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="f083d-130">`CREATE EXTERNAL TABLE` - Hive에서 새 '외부' 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="f083d-131">외부 테이블 하이브에 hello 테이블 정의 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="f083d-132">hello 데이터는 hello 원래 위치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="f083d-133">`ROW FORMAT`-어떻게 hello 데이터의 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="f083d-134">이 경우 각 로그에 hello 필드는 공백으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="f083d-135">`STORED AS TEXTFILE LOCATION`-Hello 데이터가 저장 되 고 텍스트로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="f083d-136">`SELECT`-열 t4 hello [오류] 값을 포함 하는 모든 행의 개수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="f083d-137">외부 원본에 의해 업데이트 hello 원본으로 사용 되는 데이터 toobe 예상 되는 경우 외부 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="f083d-138">예: 자동화된 데이터 업로드 프로세스나 또 다른 MapReduce 작업 사용</span><span class="sxs-lookup"><span data-stu-id="f083d-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="f083d-139">외부 테이블 삭제는 *하지* hello 데이터를 hello 테이블 정의 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f083d-140">Hello 둡니다 __데이터베이스__ 선택 항목에 __기본__합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="f083d-141">이 문서에 hello 예제 HDInsight에 포함 된 hello 기본 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="f083d-142">toostart hello 쿼리를 사용 하 여 hello **Execute** hello 워크시트 아래 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="f083d-143">너무 주황색 및 hello 텍스트 변경 내용으로**중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="f083d-144">Hello 쿼리 완료 되 면 hello **결과** hello 연산의 hello 결과 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="f083d-145">hello 텍스트 다음은 hello 쿼리의 hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="f083d-146">hello **로그** 탭 사용된 tooview hello 로깅 정보 hello 작업에 의해 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="f083d-147">hello **결과 저장** hello 위쪽의 드롭다운 목록 대화 상자 왼쪽의 hello **쿼리 프로세스 결과** 섹션 toodownload를 허용 하거나 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="f083d-148">선택 hello 처음 네 개의 줄이 쿼리의 선택 **Execute**합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="f083d-149">결과가 없습니다 hello 작업이 완료 되었을 때 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="f083d-150">Hello를 사용 하 여 **Execute** 실행 hello 선택한 문을 하면 hello 쿼리의 일부로 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="f083d-151">이 경우 hello 선택 영역 hello 테이블에서 행을 검색 하는 hello 마지막 문을 포함 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="f083d-152">해당 줄만 선택 하 고 사용 하 여 **Execute**, hello 예상 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="f083d-153">tooadd 워크시트를 사용 하 여 hello **새 워크시트** hello 아래쪽 hello의 단추 **쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="f083d-154">Hello 새 워크시트에 hello HiveQL 문은 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="f083d-155">이러한 문은 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f083d-156">**CREATE TABLE IF NOT EXISTS** - 테이블이 아직 없는 경우 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="f083d-157">Hello 이후 **외부** 키워드가 사용 되지 않습니다, 내부 테이블이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="f083d-158">내부 테이블 hello 하이브 데이터 웨어하우스의 저장 되 고 하이브에서 완전히 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="f083d-159">외부 테이블의 경우와 달리 hello 기본 데이터도 삭제 내부 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="f083d-160">**AS ORC 저장** -hello 데이터 액세스에 최적화 된 행 열 형식 (ORC) 형식으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="f083d-161">ORC는 Hive 데이터를 저장하기 위한 고도로 최적화되고 효율적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="f083d-162">**덮어쓰기 삽입... 선택** -hello에서 행을 선택 **log4jLogs** 이 있는 테이블 `[ERROR]`, 다음 hello에 데이터 hello를 삽입 하 고 **살펴볼** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="f083d-163">사용 하 여 hello **Execute** toorun이이 쿼리 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="f083d-164">hello **결과** hello 쿼리가 0 개의 행을 반환할 때 탭 정보를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="f083d-165">hello로 표시 되어야 **SUCCEEDED** hello 쿼리가 완료 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="f083d-166">시각적 개체 설명</span><span class="sxs-lookup"><span data-stu-id="f083d-166">Visual explain</span></span>

<span data-ttu-id="f083d-167">toodisplay hello 쿼리 계획을 선택 하는 hello의 시각화 **Visual 설명** hello 워크시트 아래 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="f083d-168">hello **Visual 설명** hello 쿼리의 보기 hello 흐름 복잡 한 쿼리를 이해 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="f083d-169">Hello를 사용 하 여이 보기의 텍스트는 항목을 볼 수 있습니다 **설명** hello 쿼리 편집기의에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="f083d-170">Tez UI</span><span class="sxs-lookup"><span data-stu-id="f083d-170">Tez UI</span></span>

<span data-ttu-id="f083d-171">toodisplay 선택 hello hello 쿼리용 Tez UI hello **Tez** hello 워크시트 아래 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f083d-172">Tez은 사용된 되지 않습니다 tooresolve 모든 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="f083d-173">많은 쿼리는 Tez를 사용하지 않고도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="f083d-174">Tez를 사용 하는 tooresolve hello 쿼리 한 경우 전달 된 비순환 그래프 (DAG) hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="f083d-175">Hello를 사용 하 여 쿼리 hello, 이전에 실행 한 또는 디버그 hello Tez 프로세스에 대 한 tooview hello DAG를 원하는 경우 [Tez 보기](hdinsight-debug-ambari-tez-view.md) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="f083d-176">작업 기록 보기</span><span class="sxs-lookup"><span data-stu-id="f083d-176">View job history</span></span>

<span data-ttu-id="f083d-177">hello __작업__ 하이브 쿼리에서의 기록 탭에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Hello 작업 기록의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="f083d-179">데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="f083d-179">Database tables</span></span>

<span data-ttu-id="f083d-180">Hello를 사용할 수 있습니다 __테이블__ toowork 하이브 데이터베이스 내에서 테이블을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Hello 테이블 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="f083d-182">저장된 쿼리</span><span class="sxs-lookup"><span data-stu-id="f083d-182">Saved queries</span></span>

<span data-ttu-id="f083d-183">Hello 쿼리 탭에서 필요에 따라 쿼리를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="f083d-184">저장 한 후 다시 사용할 수 있습니다 hello에서 hello 쿼리 __저장 된 쿼리__ 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![저장된 쿼리 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="f083d-186">사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="f083d-186">User-defined functions</span></span>

<span data-ttu-id="f083d-187">Hive는 UDF(사용자 정의 함수)를 통해 확장될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="f083d-188">UDF는 tooimplement 기능이 나 HiveQL에서 쉽게 모델링 되지 논리를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="f083d-189">hello hello 하이브 보기의 hello 위쪽 UDF 탭 toodeclare 있으며 Udf의 집합을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="f083d-190">이러한 Udf hello 사용 하 여 **쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-190">These UDFs can be used with hello **Query Editor**.</span></span>

![UDF 탭의 이미지](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="f083d-192">UDF toohello 하이브 보기를 추가 하 고 나면는 **udf 삽입** hello hello 맨 아래에 단추가 나타납니다 **쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="f083d-193">이 항목을 선택 하면 hello hello 하이브 보기에에서 정의 된 Udf의 드롭다운 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="f083d-194">UDF를 선택 합니다. HiveQL 문은 tooyour 쿼리 tooenable hello UDF를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="f083d-195">예를 들어, 다음과 같은 속성 hello로 UDF를 정의한 경우:</span><span class="sxs-lookup"><span data-stu-id="f083d-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="f083d-196">리소스 이름: myudfs</span><span class="sxs-lookup"><span data-stu-id="f083d-196">Resource name: myudfs</span></span>

* <span data-ttu-id="f083d-197">리소스 경로: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="f083d-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="f083d-198">UDF 이름: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="f083d-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="f083d-199">UDF 클래스 이름: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="f083d-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="f083d-200">Hello를 사용 하 여 **udf 삽입** 단추 표시 라는 항목이 **myudfs**, 드롭 다운 해당 리소스에 대해 정의 된 각 UDF에 대 한 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="f083d-201">이 경우 **myawesomeudf**입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="f083d-202">이 항목을 선택 하면 hello hello 쿼리의 toohello 시작 부분에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="f083d-203">다음 쿼리에서 hello UDF를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="f083d-204">예: `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="f083d-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="f083d-205">HDInsight의 Hive Udf 사용에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f083d-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f083d-206">HDInsight에서 Hive 및 Pig와 함께 Python 사용</span><span class="sxs-lookup"><span data-stu-id="f083d-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="f083d-207">어떻게 tooadd 사용자 지정 하이브 UDF tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="f083d-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="f083d-208">Hive 설정</span><span class="sxs-lookup"><span data-stu-id="f083d-208">Hive settings</span></span>

<span data-ttu-id="f083d-209">설정 수 있는 다양 한 하이브 설정을 사용 하는 toochange 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="f083d-210">예를 들어 Tez hello 기본값인 tooMapReduce에서 하이브에 대 한 hello 실행 엔진을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f083d-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="f083d-211"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f083d-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f083d-212">HDInsight의 Hive에 대한 일반적인 정보:</span><span class="sxs-lookup"><span data-stu-id="f083d-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="f083d-213">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="f083d-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="f083d-214">HDInsight에서 Hadoop으로 작업하는 다른 방법에 관한 정보:</span><span class="sxs-lookup"><span data-stu-id="f083d-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f083d-215">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="f083d-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f083d-216">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="f083d-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
