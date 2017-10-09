---
title: "Azure HDInsight의 Hive aaaOptimize 쿼리 | Microsoft Docs"
description: "어떻게 toooptimize 프로그램 하이브 쿼리를 HDInsight의 Hadoop에 대 한 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="d2d01-103">Azure HDInsight에서 Hive 쿼리를 최적화</span><span class="sxs-lookup"><span data-stu-id="d2d01-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="d2d01-104">기본적으로 Hadoop 클러스터는 성능을 위해 최적화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="d2d01-105">이 문서에서는 tooyour 쿼리를 적용할 수 있는 하 몇 가지 가장 일반적인 하이브 성능 최적화 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="d2d01-106">작업자 노드 확장</span><span class="sxs-lookup"><span data-stu-id="d2d01-106">Scale out worker nodes</span></span>

<span data-ttu-id="d2d01-107">Hello 클러스터의 작업자 노드 수를 늘리면 병렬로 실행 하는 자세한 매퍼 및 이경소켓 toobe를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="d2d01-108">HDInsight에서 크기를 확장할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="d2d01-109">Hello 프로 비전 시 hello hello Azure 포털, Azure PowerShell 또는 플랫폼 간 명령줄 인터페이스를 사용 하 여 작업자 노드 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="d2d01-110">자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d01-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="d2d01-111">hello 다음 스크린샷은 hello 작업자 노드 구성 hello Azure 포털에서:</span><span class="sxs-lookup"><span data-stu-id="d2d01-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="d2d01-113">Hello 실행 시간에 수평 확장할 수 있습니다는 클러스터 하나를 다시 만들지 않고:</span><span class="sxs-lookup"><span data-stu-id="d2d01-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="d2d01-115">HDInsight에서 지 원하는 hello 서로 다른 가상 컴퓨터에 대 한 자세한 내용은 참조 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="d2d01-116">TCP 사용</span><span class="sxs-lookup"><span data-stu-id="d2d01-116">Enable Tez</span></span>

<span data-ttu-id="d2d01-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) 는 대체 실행 엔진 toohello MapReduce 엔진:</span><span class="sxs-lookup"><span data-stu-id="d2d01-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="d2d01-119">다음의 이유로 Tez가 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-119">Tez is faster because:</span></span>

* <span data-ttu-id="d2d01-120">**비순환 그래프 지시 (DAG) hello MapReduce 엔진에서 단일 작업으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="d2d01-121">hello DAG 이경소켓 집합이 하나 옵니다 매퍼 toobe 각 집합이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="d2d01-122">이렇게 하면 각 하이브 쿼리에 대 한 분리 된 여러 MapReduce 작업 toobe 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="d2d01-123">Tez는 이러한 제약 조건이 없으며 복잡한 DAG를 작업 시작 오버 헤드를 최소화하는 하나의 작업으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="d2d01-124">**불필요한 쓰기를 방지**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="d2d01-125">Hello에 대 한 생성 되 고 toomultiple 작업 인해 hello MapReduce 엔진, 각 작업의 hello 출력에서에서 동일한 하이브 쿼리 tooHDFS 중간 데이터에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="d2d01-126">Tez 각 하이브 쿼리에 대 한 작업의 수를 최소화 되므로 수 tooavoid 불필요 한 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="d2d01-127">**시작 지연을 최소화**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="d2d01-128">Tez은 toostart 및 전체 또한 개선 최적화 필요한 매퍼 hello 수를 줄여 보다 나은 수 toominimize 시작 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="d2d01-129">**컨테이너를 다시 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-129">**Reuses containers**.</span></span> <span data-ttu-id="d2d01-130">경우 언제 든 지 가능한 Tez 수 tooreuse 컨테이너 tooensure 해당 대기 시간 때문에 컨테이너를 toostarting이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="d2d01-131">**연속 최적화 기술**.</span><span class="sxs-lookup"><span data-stu-id="d2d01-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="d2d01-132">일반적으로 최적화는 컴파일 단계 중에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="d2d01-133">Hello 입력에 대 한 자세한 정보를 사용할 수 있지만 런타임에 더 나은 최적화를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="d2d01-134">Tez는 hello 런타임 단계로 추가로 toooptimize hello 계획 수 있는 연속 최적화 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="d2d01-135">이러한 개념에 대한 자세한 내용은 [Apache Tez](http://hortonworks.com/hadoop/tez/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d01-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="d2d01-136">하이브 쿼리 Tez 아래 hello 설정을 사용 하 여 hello 쿼리를 접두사로 사용을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="d2d01-137">Linux 기반 HDInsight 클러스터는 Tez를 기본적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="d2d01-138">Hive 분할</span><span class="sxs-lookup"><span data-stu-id="d2d01-138">Hive partitioning</span></span>

<span data-ttu-id="d2d01-139">I/O 작업이 하이브 쿼리를 실행 하기 위한 hello 주요 성능 병목 현상입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="d2d01-140">hello toobe 해야 하는 데이터 양을 읽을 수 있습니다 하는 경우에 hello 성능을 향상 시킬 수 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="d2d01-141">기본적으로 Hive 쿼리는 전체 Hive 테이블을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="d2d01-142">테이블 검사와 같은 쿼리에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-142">This is great for queries like table scans.</span></span> <span data-ttu-id="d2d01-143">그러나 tooscan 적은 양의 데이터 (예: 필터링 된 쿼리) 하기만 하는 쿼리의 경우이 동작에서는 불필요 한 오버 헤드</span><span class="sxs-lookup"><span data-stu-id="d2d01-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="d2d01-144">하이브 분할 Hive 테이블에 하이브 쿼리 tooaccess만 hello 필요한 만큼의 데이터를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="d2d01-145">하이브 분할 hello 원시 데이터를 다시 구성 하면 각 파티션에 자체 directory-hello 파티션 hello 사용자가 정의 되어 있는 새 디렉터리에 의해 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="d2d01-146">hello 다음 다이어그램에서는 hello 열별로 Hive 테이블 분할 *연도*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="d2d01-147">각 연도로 새 디렉터리가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-147">A new directory is created for each year.</span></span>

![분할][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="d2d01-149">일부 분할 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="d2d01-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="d2d01-150">**언더 분할 안 함** - 몇 개의 값만 있는 열에서 분할하면 적은 파티션을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="d2d01-151">예를 들어 gender에 분할만 (male 및 female)를 생성 하는 두 개의 파티션을 toobe, 따라서 절반 최대 여만 hello 대기 시간을 줄일.</span><span class="sxs-lookup"><span data-stu-id="d2d01-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="d2d01-152">**파티션을 통해 하지 않는** -hello 다른 한편으로 파티션이 여러 개 지정 하면 고유 값 (예를 들어 사용자 id)으로 열에 파티션 만들기.</span><span class="sxs-lookup"><span data-stu-id="d2d01-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="d2d01-153">파티션을 통해 하면 많은 스트레스 hello 클러스터 namenode toohandle hello 많은 수의 디렉터리 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="d2d01-154">**데이터 오차 방지** -모든 파티션의 크기가 고르도록 현명하게 분할 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="d2d01-155">예로 분할을 *상태* hello 캘리포니아 toobe 레코드 수가 거의 30 발생할 수 있습니다는 버몬트 채우기의 toohello 차이 때문에 x입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="d2d01-156">파티션 테이블 toocreate hello를 사용 하 여 *분할 하 여* 절:</span><span class="sxs-lookup"><span data-stu-id="d2d01-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="d2d01-157">Hello 분할 된 테이블을 만든 후 정적 분할 또는 동적 분할 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="d2d01-158">**정적 분할** 하이브 파티션을 hello 디렉터리 위치에 따라 수동으로 요청 하 고 의미 hello에 이미 분할 된 데이터가 있는 경우 해당 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="d2d01-159">다음 코드 조각 hello 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="d2d01-160">**동적 분할** 의미 하이브 toocreate 파티션이 자동으로 드립니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="d2d01-161">Hello 준비 테이블에서에서 테이블을 분할 하는 hello를 이미 만들었습니다 toodo 필요한 것 이므로 데이터 toohello 분할 된 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="d2d01-162">자세한 내용은 [분할된 테이블](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d01-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="d2d01-163">Hello ORCFile 형식을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d2d01-163">Use hello ORCFile format</span></span>
<span data-ttu-id="d2d01-164">Hive는 다양한 파일 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-164">Hive supports different file formats.</span></span> <span data-ttu-id="d2d01-165">예:</span><span class="sxs-lookup"><span data-stu-id="d2d01-165">For example:</span></span>

* <span data-ttu-id="d2d01-166">**텍스트**: hello 기본 파일 형식 이므로 대부분의 시나리오와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="d2d01-167">**Avro**: 상호 운용성 시나리오에 대해 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="d2d01-168">**ORC/Parquet**: 성능에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="d2d01-169">ORC (최적화 된 행 칼럼 형식) 형식은 매우 효율적으로 toostore 하이브 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="d2d01-170">비교 tooother 형식, ORC hello 장점 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="d2d01-171">DateTime 및 복잡 및 반구조화된 형식을 포함하는 복합 형식 지원</span><span class="sxs-lookup"><span data-stu-id="d2d01-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="d2d01-172">too70% 압축을</span><span class="sxs-lookup"><span data-stu-id="d2d01-172">up too70% compression</span></span>
* <span data-ttu-id="d2d01-173">행을 건너뛸 수 있는 10,000행마다 인덱스</span><span class="sxs-lookup"><span data-stu-id="d2d01-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="d2d01-174">런타임 실행 시 현저하게 감소</span><span class="sxs-lookup"><span data-stu-id="d2d01-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="d2d01-175">tooenable ORC 형식으로 먼저 테이블을 만들면 hello 절과 함께 *ORC로 저장*:</span><span class="sxs-lookup"><span data-stu-id="d2d01-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="d2d01-176">다음으로 hello 준비 테이블에서에서 데이터 toohello ORC 테이블을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="d2d01-177">예:</span><span class="sxs-lookup"><span data-stu-id="d2d01-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="d2d01-178">자세한 내용은 hello ORC 형식에 [여기](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="d2d01-179">벡터화</span><span class="sxs-lookup"><span data-stu-id="d2d01-179">Vectorization</span></span>

<span data-ttu-id="d2d01-180">벡터화 허용 하이브 tooprocess 1024 일괄 처리 행을 한 번에 하나의 행을 처리 하는 대신 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="d2d01-181">더 적은 내부 코드 toorun 해야 하기 때문에 간단한 작업은 더 빠르게 수행 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="d2d01-182">tooenable 벡터화 접두사로 설정에 따라 hello를 사용 하 여 하이브 쿼리:</span><span class="sxs-lookup"><span data-stu-id="d2d01-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="d2d01-183">자세한 내용은 [벡터화된 쿼리 실행](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d01-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="d2d01-184">다른 최적화 방법</span><span class="sxs-lookup"><span data-stu-id="d2d01-184">Other optimization methods</span></span>
<span data-ttu-id="d2d01-185">예를 들어 다음은 고려할 수 있는 추가 최적화 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="d2d01-186">**버킷 팅 하이브:** 대량의 데이터 toooptimize 쿼리 성능 toocluster 또는 세그먼트를 허용 하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="d2d01-187">**조인 최적화:** 하이브의 쿼리 실행 tooimprove 계획의 최적화 조인 효율성 hello 및 사용자 힌트에 대 한 hello 필요한 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="d2d01-188">자세한 내용은 [조인 최적화](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2d01-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="d2d01-189">**리듀서 증가**</span><span class="sxs-lookup"><span data-stu-id="d2d01-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d01-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2d01-190">Next steps</span></span>
<span data-ttu-id="d2d01-191">이 기사에서는 몇가지 일반적인 하이브 쿼리 최적화 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d01-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="d2d01-192">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="d2d01-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="d2d01-193">HDInsight에서 Apache Hive 사용</span><span class="sxs-lookup"><span data-stu-id="d2d01-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d2d01-194">HDInsight의 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="d2d01-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="d2d01-195">HDInsight에서 Hive를 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="d2d01-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="d2d01-196">HDInsight에서 Hadoop에서 하이브 쿼리 콘솔 hello를 사용 하 여 센서 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="d2d01-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="d2d01-197">하이브를 사용 하 여 웹 사이트에서 HDInsight tooanalyze 로그</span><span class="sxs-lookup"><span data-stu-id="d2d01-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
