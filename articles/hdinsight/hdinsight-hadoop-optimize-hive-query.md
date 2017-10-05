---
title: "Azure HDInsight에서 Hive 쿼리를 최적화 | Microsoft Docs"
description: "HDInsight에서 Hadoop에 대한 Hive 쿼리를 최적화하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="66ef3-103">Azure HDInsight에서 Hive 쿼리를 최적화</span><span class="sxs-lookup"><span data-stu-id="66ef3-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="66ef3-104">기본적으로 Hadoop 클러스터는 성능을 위해 최적화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="66ef3-105">이 문서에서는 쿼리에 적용할 수 있는 가장 일반적인 Hive 성능 최적화 방법 중 몇 가지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="66ef3-106">작업자 노드 확장</span><span class="sxs-lookup"><span data-stu-id="66ef3-106">Scale out worker nodes</span></span>

<span data-ttu-id="66ef3-107">클러스터의 작업자 노드 수를 늘리면 더 많은 매퍼와 리듀서를 활용하여 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="66ef3-108">HDInsight에서 크기를 확장할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="66ef3-109">프로비전 시 Azure Portal, Azure PowerShell 또는 플랫폼 간 명령줄 인터페이스를 사용하여 작업자 노드의 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="66ef3-110">자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="66ef3-111">다음 스크린샷에는 Azure Portal의 작업자 노드 구성이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="66ef3-113">런타임 시, 클러스터를 다시 만들지 않고 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="66ef3-115">HDInsight에서 지원하는 다른 가상 컴퓨터에 대한 자세한 내용은 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="66ef3-116">TCP 사용</span><span class="sxs-lookup"><span data-stu-id="66ef3-116">Enable Tez</span></span>

<span data-ttu-id="66ef3-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) 는 MapReduce 엔진에 대한 대체 실행 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="66ef3-119">다음의 이유로 Tez가 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-119">Tez is faster because:</span></span>

* <span data-ttu-id="66ef3-120">**MapReduce 엔진에서 단일 작업으로 DAG(방향성 비순환 그래프)를 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="66ef3-121">DAG를 사용하려면 각 매퍼 집합 다음에 하나의 리듀서 집합이 나와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="66ef3-122">이렇게 하면 여러 MapReduce 작업이 각 Hive 쿼리에 대해 분리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="66ef3-123">Tez는 이러한 제약 조건이 없으며 복잡한 DAG를 작업 시작 오버 헤드를 최소화하는 하나의 작업으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="66ef3-124">**불필요한 쓰기를 방지**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="66ef3-125">MapReduce 엔진에서 동일한 Hive 쿼리에 대해 여러 작업을 분리하기 때문에, 각 작업의 출력은 중간 데이터로 HDFS로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="66ef3-126">Tez는 각 하이브 쿼리에 대한 작업 수를 최소화하므로 불필요한 쓰기를 피할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="66ef3-127">**시작 지연을 최소화**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="66ef3-128">Tez는 시작하는데 필요한 매퍼의 수를 줄여 시작 지연 시간을 최소화할 수 있으며 최적화 처리량을 개선하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="66ef3-129">**컨테이너를 다시 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-129">**Reuses containers**.</span></span> <span data-ttu-id="66ef3-130">가능할 때마다 Tez가 컨테이너를 다시 시작하여 컨테이너 시작으로 인한 대기 시간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="66ef3-131">**연속 최적화 기술**.</span><span class="sxs-lookup"><span data-stu-id="66ef3-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="66ef3-132">일반적으로 최적화는 컴파일 단계 중에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="66ef3-133">런타임 중 더 나은 최적화를 허용하는 입력에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="66ef3-134">Tez는 계획을 런타임 단계로 추가로 최적화할 수 있는 연속 최적화 기법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="66ef3-135">이러한 개념에 대한 자세한 내용은 [Apache Tez](http://hortonworks.com/hadoop/tez/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="66ef3-136">아래 설정을 사용하여 쿼리를 접두사로 지정하여 모든 Hive 쿼리 Tez를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="66ef3-137">Linux 기반 HDInsight 클러스터는 Tez를 기본적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="66ef3-138">Hive 분할</span><span class="sxs-lookup"><span data-stu-id="66ef3-138">Hive partitioning</span></span>

<span data-ttu-id="66ef3-139">I/O 작업이 Hive 쿼리를 실행하기 위한 주요 성능 병목 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="66ef3-140">읽어야 하는 데이터 양을 줄일 수 있는 경우 성능이 향상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="66ef3-141">기본적으로 Hive 쿼리는 전체 Hive 테이블을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="66ef3-142">테이블 검사와 같은 쿼리에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-142">This is great for queries like table scans.</span></span> <span data-ttu-id="66ef3-143">그렇지만 적은 양의 데이터(예: 필터링된 쿼리)를 검색해야 하는 쿼리의 경우 이 동작은 불필요한 오버 헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="66ef3-144">Hive 분할을 사용하면 Hive 쿼리가 Hive 테이블의에서 데이터를 필요한 만큼만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="66ef3-145">Hive 분할은 원시 데이터를 자체 디렉터리가 있는 각 파티션이 있는 새 디렉터리로 재구성하여 구현됩니다. 여기서 파티션은 사용자가 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="66ef3-146">다음 다이어그램에서는 Hive 테이블을 *년* 열로 분할하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="66ef3-147">각 연도로 새 디렉터리가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-147">A new directory is created for each year.</span></span>

![분할][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="66ef3-149">일부 분할 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="66ef3-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="66ef3-150">**언더 분할 안 함** - 몇 개의 값만 있는 열에서 분할하면 적은 파티션을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="66ef3-151">예를 들어 성별에 관한 분할은 두 파티션(남성과 여성)을 만드므로 최대 절반으로 대기 시간을 단축합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="66ef3-152">**오버 분할 안 함** - 반대로 고유 값(예: userid)을 갖는 열에서 분할을 만들면 여러 파티션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="66ef3-153">오버 분할의 경우 많은 수의 디렉터리를 처리해야 하므로 클러스터 namenode에 과도한 스트레스가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="66ef3-154">**데이터 오차 방지** -모든 파티션의 크기가 고르도록 현명하게 분할 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="66ef3-155">예제에서 *State* 에 대한 분할로 인구 파이 때문에 캘리포니아에서 레코드 수가 버몬트 레코드 수의 거의 30배일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="66ef3-156">파티션 테이블을 만들려면 *Partitioned By* 절을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="66ef3-157">분할된 테이블을 만든 후 정적 분할 또는 동적 분할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="66ef3-158">**정적 분할** 은 적절한 디렉터리에서 데이터를 이미 공유하고 있고 디렉터리 위치에 따라 수동으로 Hive 파티션을 요청할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="66ef3-159">다음 코드 조각은 예제로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="66ef3-160">**동적 분할** 은 하이브가 파티션을 자동으로 만들수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="66ef3-161">스테이징 테이블에서 분할 테이블을 이미 만들었으므로, 분할된 테이블에 데이터를 삽입하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="66ef3-162">자세한 내용은 [분할된 테이블](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="66ef3-163">ORCFile 형식 사용</span><span class="sxs-lookup"><span data-stu-id="66ef3-163">Use the ORCFile format</span></span>
<span data-ttu-id="66ef3-164">Hive는 다양한 파일 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-164">Hive supports different file formats.</span></span> <span data-ttu-id="66ef3-165">예:</span><span class="sxs-lookup"><span data-stu-id="66ef3-165">For example:</span></span>

* <span data-ttu-id="66ef3-166">**텍스트**: 기본 파일 형식으로 대부분의 시나리오와 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="66ef3-167">**Avro**: 상호 운용성 시나리오에 대해 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="66ef3-168">**ORC/Parquet**: 성능에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="66ef3-169">ORC(최적화된 행 칼럼 형식) 형식은 Hive 데이터를 저장하는 매우 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="66ef3-170">다른 형식에 비해, ORC는 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="66ef3-171">DateTime 및 복잡 및 반구조화된 형식을 포함하는 복합 형식 지원</span><span class="sxs-lookup"><span data-stu-id="66ef3-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="66ef3-172">최대 70% 압축</span><span class="sxs-lookup"><span data-stu-id="66ef3-172">up to 70% compression</span></span>
* <span data-ttu-id="66ef3-173">행을 건너뛸 수 있는 10,000행마다 인덱스</span><span class="sxs-lookup"><span data-stu-id="66ef3-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="66ef3-174">런타임 실행 시 현저하게 감소</span><span class="sxs-lookup"><span data-stu-id="66ef3-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="66ef3-175">ORC 형식을 사용하려면 먼저 *Stored as ORC*절로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="66ef3-176">다음으로 스테이징 테이블에서 ORC 테이블로 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="66ef3-177">예:</span><span class="sxs-lookup"><span data-stu-id="66ef3-177">For example:</span></span>

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

<span data-ttu-id="66ef3-178">ORC 형식에 대한 자세한 내용은 [여기](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="66ef3-179">벡터화</span><span class="sxs-lookup"><span data-stu-id="66ef3-179">Vectorization</span></span>

<span data-ttu-id="66ef3-180">벡터화를 사용하면 하이브가 한번에 하나의 행을 처리하는 대신 함께 1024행을 일괄 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="66ef3-181">즉, 실행할 내부 코드가 적기 때문에 간단한 작업은 더 빠르게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="66ef3-182">다음 설정을 사용하여 Hive 쿼리에 벡터화 접두사를 사용할 수 있도록 하려면:</span><span class="sxs-lookup"><span data-stu-id="66ef3-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="66ef3-183">자세한 내용은 [벡터화된 쿼리 실행](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="66ef3-184">다른 최적화 방법</span><span class="sxs-lookup"><span data-stu-id="66ef3-184">Other optimization methods</span></span>
<span data-ttu-id="66ef3-185">예를 들어 다음은 고려할 수 있는 추가 최적화 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="66ef3-186">**Hive 버킷팅:** 대형 데이터 집합을 클러스터 또는 세그먼트하여 쿼리 성능을 최적화할 수 있는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="66ef3-187">**조인 최적화:** 조인의 효율성을 높이고 사용자 힌트에 대한 필요성을 줄이는 Hive의 쿼리 실행 계획 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="66ef3-188">자세한 내용은 [조인 최적화](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="66ef3-189">**리듀서 증가**</span><span class="sxs-lookup"><span data-stu-id="66ef3-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66ef3-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66ef3-190">Next steps</span></span>
<span data-ttu-id="66ef3-191">이 기사에서는 몇가지 일반적인 하이브 쿼리 최적화 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="66ef3-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="66ef3-192">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66ef3-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="66ef3-193">HDInsight에서 Apache Hive 사용</span><span class="sxs-lookup"><span data-stu-id="66ef3-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="66ef3-194">HDInsight의 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="66ef3-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="66ef3-195">HDInsight에서 Hive를 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="66ef3-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="66ef3-196">HDInsight의 Hadoop에서 Hive 쿼리 콘솔을 사용하여 센서 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="66ef3-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="66ef3-197">HDInsight와 함께 Hive를 사용하여 웹 사이트의 로그 분석</span><span class="sxs-lookup"><span data-stu-id="66ef3-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
