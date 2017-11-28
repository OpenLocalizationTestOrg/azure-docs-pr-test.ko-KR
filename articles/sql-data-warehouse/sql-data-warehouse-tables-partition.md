---
title: "SQL 데이터 웨어하우스에 aaaPartitioning 테이블 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 테이블 분할 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="688c8-103">SQL 데이터 웨어하우스의 테이블 분할</span><span class="sxs-lookup"><span data-stu-id="688c8-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="688c8-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="688c8-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="688c8-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="688c8-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="688c8-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="688c8-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="688c8-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="688c8-107">[Index][Index]</span></span>
> * <span data-ttu-id="688c8-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="688c8-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="688c8-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="688c8-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="688c8-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="688c8-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="688c8-111">분할은 클러스터형 columnstore, 클러스터형 인덱스 및 힙을 포함하는 모든 SQL 데이터 웨어하우스 테이블 형식에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="688c8-112">또한 해시 또는 라운드 로빈 배포를 비롯한 모든 배포 유형에서도 분할이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="688c8-113">분할 하면 더 작은 그룹으로의 데이터 및 대부분의 경우에서 분할 데이터 날짜 열에 의해 이루어진다는 toodivide 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="688c8-114">분할의 이점</span><span class="sxs-lookup"><span data-stu-id="688c8-114">Benefits of partitioning</span></span>
<span data-ttu-id="688c8-115">분할은 데이터 유지 관리 및 쿼리 성능에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="688c8-116">하나 또는 둘 다 이용 여부 hello 동일한 열 사용할 수 있는지 여부에 대 한 두 가지 목적으로 하나의 열만 수행할 수 분할 이후 및 데이터를 로드 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="688c8-117">이점 tooloads</span><span class="sxs-lookup"><span data-stu-id="688c8-117">Benefits tooloads</span></span>
<span data-ttu-id="688c8-118">SQL 데이터 웨어하우스에서 분할의 주요 이점은 hello hello 효율성과 파티션 삭제를 사용 하 여 데이터를 로드, 전환 및 병합의 성능을 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="688c8-119">대부분의 경우 데이터를 날짜에 분할 열은 밀접 하 게 toohello 시퀀스는 hello 데이터는 로드 toohello 데이터베이스 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="688c8-120">트랜잭션 로그 방지를 hello 파티션을 toomaintain 데이터를 사용 하 여 hello 가장 큰 장점 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="688c8-121">단순히 삽입, 업데이트 또는 데이터 삭제와 약간 노력과, hello 가장 간단한 방법은 수 있지만 로드 프로세스 중 분할을 사용 하 여 실질적으로 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="688c8-122">파티션 전환을 사용 하는 tooquickly 제거 될 하거나 테이블의 한 섹션을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="688c8-123">예를 들어 판매 팩트 테이블 hello에 대 한 설정은 데이터 뿐 지난 36 개월 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="688c8-124">매월 hello 끝 hello 판매 데이터의 가장 오래 된 월은 테이블에서 삭제 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="688c8-125">사용 하 여 delete 문의 toodelete hello 데이터 hello에 대 한 가장 오래 된 월이이 데이터를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="688c8-126">그러나 많은 양의 데이터-행 delete 문과 함께 삭제 수 시간이 오래 걸릴를 hello 위험 큰 트랜잭션 문제가 발생 한 경우 시간이 오래 toorollback 소요 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="688c8-127">Toosimply 놓기 hello 가장 오래 된 데이터 파티션을 위한 더 최적의 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="688c8-128">여기서 hello 개별 행 삭제 걸리는 시간을 초 걸릴 수 있습니다 전체 파티션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="688c8-129">이점 tooqueries</span><span class="sxs-lookup"><span data-stu-id="688c8-129">Benefits tooqueries</span></span>
<span data-ttu-id="688c8-130">분할 하는 경우에 사용 되는 tooimprove 쿼리 성능이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="688c8-131">분할 된 열에 필터를 적용 하는 쿼리를 훨씬 더 작은 하위 집합만 전체 테이블 검색을 방지 하는 hello 데이터 일 수 있는 파티션을 한 정하는 hello 스캔 tooonly hello를 제한할 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="688c8-132">클러스터형된 columnstore 인덱스의 hello 도입으로 hello 조건자 제거 제공 하는 덜 유용한 있지만 경우도 있을 수 혜택 tooqueries.</span><span class="sxs-lookup"><span data-stu-id="688c8-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="688c8-133">예를 들어 hello 판매 팩트 테이블에 36 개월 hello 판매 날짜 필드를 사용 하 여 분할 된 경우 다음 hello 판매 날짜에 필터링 하는 쿼리를 건너뛸 수 파티션에 hello 필터 일치 하지 않는 검색.</span><span class="sxs-lookup"><span data-stu-id="688c8-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="688c8-134">파티션 크기 조정 지침</span><span class="sxs-lookup"><span data-stu-id="688c8-134">Partition sizing guidance</span></span>
<span data-ttu-id="688c8-135">분할 하는 동안 일부 시나리오에서는 포함 된 테이블을 만드는 사용 되는 tooimprove 성능 수 **너무 많은** 파티션을 상황에 따라 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="688c8-136">특히 클러스터형 columnstore 테이블에서 이러한 점이 우려됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="688c8-137">것이 중요 한 toounderstand toobe 유용한 분할 때 파티션 toocreate toouse 분할 및 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="688c8-138">있습니다 toohow로 빠른 규칙이 없습니다. 하드 파티션 수는 너무 많은 데이터에 따라 있고, 개수 분할 toosimultaneously를 로드 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="688c8-139">일반으로 생각 하면 단위: 10에 추가 하지만 too100s 파티션의 1000s 없습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="688c8-140">분할을 만들 때 **클러스터형된 columnstore** 테이블 것이 중요 한 tooconsider 각 파티션에 배치 되며 행의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="688c8-141">클러스터형 columnstore 테이블에 대한 최적의 압축 및 성능을 고려할 때, 배포 및 파티션당 최소 1백만 개의 행이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="688c8-142">파티션이 생성되기 전에 SQL 데이터 웨어하우스는 미리 각 테이블을 60개의 분산된 데이터베이스로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="688c8-143">모든 분할 추가 tooa 테이블은 또한 hello 백그라운드 만든 toohello 분포입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="688c8-144">이 예제를 사용 하 여 hello 판매 팩트 테이블 36 월별 파티션을 포함 하 고 판매 팩트 테이블 한 달, 60 백만 행 또는 2.1 십억 행 때에 모든 월이 채워져 hello 다음 SQL 데이터 웨어하우스에 60 분포 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="688c8-145">Hello 권장 되는 행 수의 최소 수 보다 훨씬 더 적은 행을 포함 하는 테이블을 파티션당 행의 순서 toomake 증가 hello 번호에 적은 수의 파티션이 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="688c8-146">또한 hello 참조 [인덱싱] [ Index] 클러스터는 columnstore 인덱스의 SQL 데이터 웨어하우스 tooassess hello 품질에 실행할 수 있는 쿼리를 포함 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="688c8-147">SQL Server와의 구문 차이</span><span class="sxs-lookup"><span data-stu-id="688c8-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="688c8-148">SQL 데이터 웨어하우스는 SQL Server와는 약간 다른 단순화된 파티션의 정의를 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="688c8-149">파티션 함수 및 구성표는 SQL Server에서는 사용되지만 SQL 데이터 웨어하우스에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="688c8-150">대신, toodo 있으면 분할된 열과 hello 경계 지점을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="688c8-151">분할의 hello 구문은 SQL Server와에서 약간 다릅니다 수 있지만, hello 기본 개념 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="688c8-152">SQL Server 및 SQL 데이터 웨어하우스는 테이블당 하나의 파티션 열(범위가 지정된 파티션)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="688c8-153">분할에 대해 자세히 toolearn 참조 [Partitioned Tables and Indexes][Partitioned Tables and Indexes]합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="688c8-154">아래 예제에서는 분할 된 SQL 데이터 웨어하우스의 hello [CREATE TABLE] [ CREATE TABLE] 문을 hello OrderDateKey 열에 hello FactInternetSales 테이블 분할:</span><span class="sxs-lookup"><span data-stu-id="688c8-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="688c8-155">SQL Server에서 분할 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="688c8-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="688c8-156">SQL Server toomigrate 정의 tooSQL 데이터 웨어하우스를 단순히 분할:</span><span class="sxs-lookup"><span data-stu-id="688c8-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="688c8-157">SQL Server hello 제거 [파티션 구성표][partition scheme]합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="688c8-158">Hello 추가 [파티션 함수] [ partition function] 정의 tooyour CREATE TABLE입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="688c8-159">SQL 아래의 SQL Server 인스턴스 hello에서 분할된 된 테이블을 마이그레이션하는 경우 유용 toointerrogate hello 수에 각 파티션에 있는 행 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="688c8-160">Hello 동일한 분할 세분성이 사용 되는 경우 SQL 데이터 웨어하우스, 60의 비율로 hello 파티션당 행 수가 감소 합니다 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="688c8-161">워크로드 관리</span><span class="sxs-lookup"><span data-stu-id="688c8-161">Workload management</span></span>
<span data-ttu-id="688c8-162">Toohello 테이블 파티션 의사 결정의 마지막 부분 고려 toofactor 하나는 [작업 관리][workload management]합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="688c8-163">SQL 데이터 웨어하우스에 작업 관리는 주로 hello 관리의 메모리와 동시성입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="688c8-164">SQL 데이터 웨어하우스 hello tooeach 배포 쿼리 실행 중 할당 된 최대 메모리가 관리 되는 리소스 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="688c8-165">이상적으로 파티션은 hello의 클러스터형된 columnstore 인덱스 작성에 필요한 메모리와 같은 다른 요소 점을 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="688c8-166">더 많은 메모리가 할당되면 클러스터형 columnstore 인덱스에 훨씬 유리합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="688c8-167">따라서 tooensure 파티션 인덱스 다시 작성 하는 메모리의 중단 하지는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="688c8-168">Largerc 비롯 한 다른 역할 hello hello hello 기본 역할, smallrc의 tooone 전환 하 여 사용 가능한 tooyour 쿼리를 수행할 수 있습니다 하는 메모리 양을 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="688c8-169">Hello 리소스 관리자 동적 관리 뷰를 쿼리하여 hello 분포는 메모리 할당에 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="688c8-170">실제로 아래 hello 그림 보다 작은 메모리 부여가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="688c8-171">그러나 데이터 관리 작업에 대한 파티션의 크기를 조정할 때 사용할 수 있는 지침의 수준을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="688c8-172">Tooavoid hello 초대형 리소스 클래스에서 제공 하는 hello 메모리 부여 초과 하는 파티션을 크기 조정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="688c8-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="688c8-173">파티션을이 그림을 초과할 경우 hello 위험 차례로 tooless 최적의 압축 하는 메모리가 중을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="688c8-174">파티션 전환</span><span class="sxs-lookup"><span data-stu-id="688c8-174">Partition switching</span></span>
<span data-ttu-id="688c8-175">SQL 데이터 웨어하우스는 파티션 분할, 병합 및 전환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="688c8-176">이러한 각 함수는 hello를 사용 하 여 excuted [ALTER TABLE] [ ALTER TABLE] 문.</span><span class="sxs-lookup"><span data-stu-id="688c8-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="688c8-177">두 테이블 간에 파티션을 tooswitch hello 파티션이 각 해당 경계에 맞추고 hello 테이블 정의와 일치 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="688c8-178">테이블 hello 원본 테이블에 있는 값의 tooenforce hello 범위 hello를 포함 해야 합니다 check 제약 조건을 사용할 수 있는 경계 hello 대상 테이블로 분할 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="688c8-179">이 정보가 hello 대/소문자를 hello 파티션 메타 데이터가 동기화 되지 것입니다 hello 파티션 전환은 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="688c8-180">어떻게 toosplit 데이터가 들어 있는 파티션</span><span class="sxs-lookup"><span data-stu-id="688c8-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="688c8-181">hello 가장 효율적인 방법 toosplit 이미 데이터를 포함 하는 파티션에 toouse는 `CTAS` 문.</span><span class="sxs-lookup"><span data-stu-id="688c8-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="688c8-182">Hello 분할 된 테이블은 클러스터형된 columnstore 하는 경우 다음 hello 테이블 파티션 비어 있어야 분할 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="688c8-183">다음은 각 파티션에 하나의 행을 포함하는 샘플 분할된 columnstore 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="688c8-184">Creating hello 통계 개체에 의해 해당 테이블 메타 데이터를 보다 정확 하 게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="688c8-185">통계 작성을 생략하는 경우 SQL 데이터 웨어하우스는 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="688c8-186">통계에 대한 자세한 내용은 [통계][statistics]를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="688c8-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="688c8-187">Hello를 사용 하 여 hello 행 개수에 대 한 쿼리할 수 있습니다 `sys.partitions` 카탈로그 뷰:</span><span class="sxs-lookup"><span data-stu-id="688c8-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="688c8-188">Toosplit이이 테이블을 시도 하는 경우에서는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="688c8-189">메시지, 상태 1, ALTER PARTITION 문의 절 줄 44 분할 수준 15 35346 hello 파티션이 비어 있지 않으면 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="688c8-190">빈 파티션만 hello 테이블에 columnstore 인덱스가 있는 경우에 분할 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="688c8-191">Hello ALTER PARTITION 문을 실행 한 다음 ALTER PARTITION이 완료 한 후에 hello columnstore 인덱스를 다시 작성 하기 전에 hello columnstore 인덱스를 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="688c8-192">사용할 수 있습니다 `CTAS` toocreate 새 테이블 toohold 사항은 데이터를 공개 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="688c8-193">hello 파티션 경계는 정렬 하는 스위치 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="688c8-194">이렇게 하면 분할 이후에 우리는 빈 파티션이 hello 원본 테이블을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="688c8-195">Tooalign 우리의 데이터 toohello에 경계를 사용 하 여 새로운 분할은 toodo 남았습니다 `CTAS` toohello 주 테이블에 다시 데이터를 전환</span><span class="sxs-lookup"><span data-stu-id="688c8-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="688c8-196">좋습니다 toorefresh hello 통계는 hello hello 데이터 이동을 완료 한 후 대상 테이블 tooensure hello에 정확 하 게 hello 파티션의 데이터에는 각각의 새 배포 hello을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="688c8-197">소스 제어를 분할하는 테이블</span><span class="sxs-lookup"><span data-stu-id="688c8-197">Table partitioning source control</span></span>
<span data-ttu-id="688c8-198">tooavoid에서 테이블 정의 **rusting** 소스 제어 시스템에 방법 tooconsider hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="688c8-199">분할 된 테이블로 하지만 파티션 값이 없는 hello 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="688c8-199">Create hello table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="688c8-200">`SPLIT`hello 배포 프로세스의 일부로 hello 표:</span><span class="sxs-lookup"><span data-stu-id="688c8-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="688c8-201">소스 제어의 코드를이 접근 방식 hello로 정적 유지 되며 hello 분할 경계 값은 허용 toobe 동적입니다. hello 웨어하우스 시간에 따라 진화 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="688c8-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="688c8-202">Next steps</span></span>
<span data-ttu-id="688c8-203">toolearn에 hello 문서를 더 참조 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블배포] [ Distribute], [테이블 인덱스를 만들][Index], [테이블 통계를 유지 관리] [ Statistics] 및 [ 임시 테이블][Temporary]합니다.</span><span class="sxs-lookup"><span data-stu-id="688c8-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="688c8-204">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="688c8-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
