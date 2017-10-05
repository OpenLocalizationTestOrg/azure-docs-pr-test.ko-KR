---
title: "SQL Data Warehouse의 테이블 분할 | Microsoft Docs"
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
ms.openlocfilehash: 3edfd34d368228be32afef48688739639a3b03ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="8bc05-103">SQL 데이터 웨어하우스의 테이블 분할</span><span class="sxs-lookup"><span data-stu-id="8bc05-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="8bc05-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="8bc05-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="8bc05-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="8bc05-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="8bc05-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8bc05-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="8bc05-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="8bc05-107">[Index][Index]</span></span>
> * <span data-ttu-id="8bc05-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="8bc05-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="8bc05-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8bc05-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="8bc05-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8bc05-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="8bc05-111">분할은 클러스터형 columnstore, 클러스터형 인덱스 및 힙을 포함하는 모든 SQL 데이터 웨어하우스 테이블 형식에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="8bc05-112">또한 해시 또는 라운드 로빈 배포를 비롯한 모든 배포 유형에서도 분할이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="8bc05-113">분할을 하면 데이터가 좀 더 작은 데이터 그룹으로 나뉘며 대부분의 경우 날짜 열에서 분할이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-113">Partitioning enables you to divide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="8bc05-114">분할의 이점</span><span class="sxs-lookup"><span data-stu-id="8bc05-114">Benefits of partitioning</span></span>
<span data-ttu-id="8bc05-115">분할은 데이터 유지 관리 및 쿼리 성능에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="8bc05-116">분할이 이러한 두 가지 측면 모두에 효과적인지 아니면 한 가지 측면에만 효과적인지는 데이터의 로드 방식, 동일한 열이 두 가지 용도로 사용될 수 있는지에 따라 좌우됩니다. 분할은 한 열에 대해서만 수행할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-116">Whether it benefits both or just one is dependent on how data is loaded and whether the same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-to-loads"></a><span data-ttu-id="8bc05-117">로드에 대한 이점</span><span class="sxs-lookup"><span data-stu-id="8bc05-117">Benefits to loads</span></span>
<span data-ttu-id="8bc05-118">SQL 데이터 웨어하우스에서 분할이 가져오는 주요 이점은 파티션 삭제, 전환 및 병합을 사용하여 데이터 로드의 효율성과 성능을 향상시킨다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-118">The primary benefit of partitioning in SQL Data Warehouse is improve the efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="8bc05-119">대부분의 경우 데이터는 데이터가 데이터베이스에 로드되는 순서에 밀접하게 관련된 날짜 열에서 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-119">In most cases data is partitioned on a date column that is closely tied to the sequence which the data is loaded to the database.</span></span>  <span data-ttu-id="8bc05-120">파티션을 사용하여 데이터를 유지 관리할 때의 가장 큰 장점 중 하나는 트랜잭션 로깅이 방지된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-120">One of the greatest benefits of using partitions to maintain data it the avoidance of transaction logging.</span></span>  <span data-ttu-id="8bc05-121">단순히 데이터를 삽입, 업데이트 또는 삭제하는 것이 생각과 노력이 거의 필요하지 않은 가장 간단한 방법일 수 있지만, 로드 프로세스 중에 분할을 사용하면 성능을 크기 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-121">While simply inserting, updating or deleting data can be the most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="8bc05-122">파티션 전환을 사용하여 테이블 섹션을 빠르게 제거하거나 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-122">Partition switching can be used to quickly remove or replace a section of a table.</span></span>  <span data-ttu-id="8bc05-123">예를 들어 판매 팩트 테이블은 지난 36개월 동안의 데이터만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-123">For example, a sales fact table might contain just data for the past 36 months.</span></span>  <span data-ttu-id="8bc05-124">매월 말에 가장 오래된 달의 판매 데이터는 테이블에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-124">At the end of every month, the oldest month of sales data is deleted from the table.</span></span>  <span data-ttu-id="8bc05-125">이 데이터는 delete 문을 사용하여 가장 오래된 월의 데이터를 삭제하는 방식으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-125">This data could be deleted by using a delete statement to delete the data for the oldest month.</span></span>  <span data-ttu-id="8bc05-126">그러나 delete 문을 사용하여 행별로 대량의 데이터를 삭제하는 데 시간이 오래 걸릴 수 있으며, 문제가 있는 경우 롤백하는 데 시간이 오래 걸리는 대형 트랜잭션이 발생할 위험도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create the risk of large transactions which could take a long time to rollback if something goes wrong.</span></span>  <span data-ttu-id="8bc05-127">좀 더 최적의 접근 방법은 데이터의 가장 오래된 파티션을 단순히 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-127">A more optimal approach is to simply drop the oldest partition of data.</span></span>  <span data-ttu-id="8bc05-128">개별 행을 삭제하는 데는 몇 시간이 걸리지만 전체 파티션을 삭제하는 데는 몇 초면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-128">Where deleting the individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-to-queries"></a><span data-ttu-id="8bc05-129">쿼리에 대한 이점</span><span class="sxs-lookup"><span data-stu-id="8bc05-129">Benefits to queries</span></span>
<span data-ttu-id="8bc05-130">분할은 쿼리 성능 향상을 위해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-130">Partitioning can also be used to improve query performance.</span></span>  <span data-ttu-id="8bc05-131">쿼리가 분할된 열에 필터를 적용하는 경우 전체 테이블 검색이 방지되고 훨씬 더 작은 데이터 부분이 될 수 있는 한정된 파티션만 검색하도록 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-131">If a query applies a filter on a partitioned column, this can limit the scan to only the qualifying partitions which may be a much smaller subset of the data, avoiding a full table scan.</span></span>  <span data-ttu-id="8bc05-132">클러스터형 columnstore 인덱스가 사용되면서 조건자 제거에 따른 성능상의 이점은 줄어들었지만 경우에 따라 쿼리에는 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-132">With the introduction of clustered columnstore indexes, the predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit to queries.</span></span>  <span data-ttu-id="8bc05-133">예를 들어 판매 팩트 테이블은 판매 날짜 필드를 사용하여 36개월로 분할된 다음 판매 날짜를 필터링하는 쿼리가 필터와 일치하지 않는 파티션의 검색을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-133">For example, if the sales fact table is partitioned into 36 months using the sales date field, then queries that filter on the sale date can skip searching in partitions that don’t match the filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="8bc05-134">파티션 크기 조정 지침</span><span class="sxs-lookup"><span data-stu-id="8bc05-134">Partition sizing guidance</span></span>
<span data-ttu-id="8bc05-135">일부 시나리오에서 분할을 사용하여 성능을 향상시킬 수 있지만 **너무 많은** 파티션이 있는 테이블을 만들면 경우에 따라 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-135">While partitioning can be used to improve performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="8bc05-136">특히 클러스터형 columnstore 테이블에서 이러한 점이 우려됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="8bc05-137">분할이 도움이 되려면 분할을 사용하는 시기 및 만들려는 파티션 수를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-137">For partitioning to be helpful, it is important to understand when to use partitioning and the number of partitions to create.</span></span>  <span data-ttu-id="8bc05-138">파티션 수가 너무 많은 경우와 관련해서는 엄격한 규칙이 없지만 데이터 및 데이터를 동시에 로드하는 파티션 수에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-138">There is no hard fast rule as to how many partitions are too many, it depends on your data and how many partitions you are loading to simultaneously.</span></span>  <span data-ttu-id="8bc05-139">하지만 일반적으로 1,000개의 파티션이 아닌 10개~100개의 파티션을 추가하는 경우를 생각해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-139">But as a general rule of thumb, think of adding 10s to 100s of partitions, not 1000s.</span></span>

<span data-ttu-id="8bc05-140">**클러스터형 columnstore** 테이블에서 분할을 만들 때 각 파티션에 놓을 행 수를 고려하는 것은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-140">When creating partitioning on **clustered columnstore** tables, it is important to consider how many rows will land in each partition.</span></span>  <span data-ttu-id="8bc05-141">클러스터형 columnstore 테이블에 대한 최적의 압축 및 성능을 고려할 때, 배포 및 파티션당 최소 1백만 개의 행이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="8bc05-142">파티션이 생성되기 전에 SQL 데이터 웨어하우스는 미리 각 테이블을 60개의 분산된 데이터베이스로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="8bc05-143">백그라운드에서 생성된 배포 외에, 테이블에 분할이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-143">Any partitioning added to a table is in addition to the distributions created behind the scenes.</span></span>  <span data-ttu-id="8bc05-144">이 예제에서 사용 판매 팩트 테이블이 36개의 월별 파티션을 포함하고 SQL 데이터 웨어하우스에 60개의 배포판이 있다면 판매 팩트 테이블은 모든 달이 채워지는 경우 매월 6천만 개의 행 또는 21억 개의 행을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-144">Using this example, if the sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then the sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="8bc05-145">테이블이 파티션당 권장되는 최소 행 수보다 훨씬 적은 행을 포함하면 파티션당 행 수를 늘리기 위해 더 적은 수의 파티션을 사용할 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-145">If a table contains significantly less rows than the recommended minimum number of rows per partition, consider using fewer partitions in order to make increase the number of rows per partition.</span></span>  <span data-ttu-id="8bc05-146">또한 SQL Data Warehouse에서 실행될 수 있는 쿼리를 포함하는 [인덱싱][Index] 문서를 참조하여 클러스터 columnstore 인덱스의 품질을 평가하세요.</span><span class="sxs-lookup"><span data-stu-id="8bc05-146">Also see the [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse to assess the quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="8bc05-147">SQL Server와의 구문 차이</span><span class="sxs-lookup"><span data-stu-id="8bc05-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="8bc05-148">SQL 데이터 웨어하우스는 SQL Server와는 약간 다른 단순화된 파티션의 정의를 도입합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="8bc05-149">파티션 함수 및 구성표는 SQL Server에서는 사용되지만 SQL 데이터 웨어하우스에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="8bc05-150">대신 분할된 열 및 경계 지점을 식별하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-150">Instead, all you need to do is identify partitioned column and the boundary points.</span></span>  <span data-ttu-id="8bc05-151">분할의 구문은 SQL Server와 약간 다르지만 기본 개념은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-151">While the syntax of partitioning may be slightly different from SQL Server, the basic concepts are the same.</span></span>  <span data-ttu-id="8bc05-152">SQL Server 및 SQL 데이터 웨어하우스는 테이블당 하나의 파티션 열(범위가 지정된 파티션)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="8bc05-153">분할에 대한 자세한 내용은 [분할된 테이블 및 인덱스][Partitioned Tables and Indexes]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bc05-153">To learn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="8bc05-154">아래의 SQL Data Warehouse 분할 [CREATE TABLE][CREATE TABLE] 문 예제에서는 FactInternetSales 테이블을 OrderDateKey 열에서 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-154">The below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions the FactInternetSales table on the OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="8bc05-155">SQL Server에서 분할 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="8bc05-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="8bc05-156">SQL Server 파티션 정의를 SQL 데이터 웨어하우스에 마이그레이션하려면</span><span class="sxs-lookup"><span data-stu-id="8bc05-156">To migrate SQL Server partition definitions to SQL Data Warehouse simply:</span></span>

* <span data-ttu-id="8bc05-157">SQL Server [파티션 구성표][partition scheme]를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-157">Eliminate the SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="8bc05-158">[파티션 함수][partition function] 정의를 CREATE TABLE에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-158">Add the [partition function][partition function] definition to your CREATE TABLE.</span></span>

<span data-ttu-id="8bc05-159">SQL Server 인스턴스에서 분할된 테이블을 마이그레이션하는 경우 아래 SQL이 각 파티션에 있는 행의 수를 조사하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-159">If you are migrating a partitioned table from a SQL Server instance the below SQL can help you to interrogate the number of rows that are in each partition.</span></span>  <span data-ttu-id="8bc05-160">SQL 데이터 웨어하우스에서 동일한 분할 세분성이 사용될 경우 파티션당 행 수가 60의 배율로 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-160">Keep in mind that if the same partitioning granularity is used on SQL Data Warehouse, the number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="8bc05-161">워크로드 관리</span><span class="sxs-lookup"><span data-stu-id="8bc05-161">Workload management</span></span>
<span data-ttu-id="8bc05-162">테이블 파티션 의사 결정 시 고려해야 하는 마지막 부분이 [워크로드 관리][workload management]입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-162">One final piece consideration to factor in to the table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="8bc05-163">SQL 데이터 웨어하우스의 워크로드 관리는 주로 메모리 및 동시성에 대한 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-163">Workload management in SQL Data Warehouse is primarily the management of memory and concurrency.</span></span>  <span data-ttu-id="8bc05-164">SQL 데이터 웨어하우스에서 쿼리 실행 중 각 배포에 할당된 최대 메모리는 리소스 클래스를 통해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-164">In SQL Data Warehouse the maximum memory allocated to each distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="8bc05-165">이상적으로 파티션은 클러스터형 columnstore 인덱스 작성에 필요한 메모리 등의 다른 요소를 고려해서 크기가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-165">Ideally your partitions will be sized in consideration of other factors like the memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="8bc05-166">더 많은 메모리가 할당되면 클러스터형 columnstore 인덱스에 훨씬 유리합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="8bc05-167">따라서 파티션 인덱스 다시 작성이 메모리를 부족하게 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-167">Therefore, you will want to ensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="8bc05-168">쿼리에 사용할 수 있는 메모리의 양을 늘리면 기본 역할, smallrc에서 다른 역할 중 하나(예: largerc)로 전환하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-168">Increasing the amount of memory available to your query can be achieved by switching from the default role, smallrc, to one of the other roles such as largerc.</span></span>

<span data-ttu-id="8bc05-169">배포 당 메모리의 할당에 관한 정보는 리소스 관리자 동적 관리 뷰를 쿼리하여 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-169">Information on the allocation of memory per distribution is available by querying the resource governor dynamic management views.</span></span> <span data-ttu-id="8bc05-170">실제로 아래 그림 보다 작은 프로그램 메모리가 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-170">In reality your memory grant will be less than the figures below.</span></span> <span data-ttu-id="8bc05-171">그러나 데이터 관리 작업에 대한 파티션의 크기를 조정할 때 사용할 수 있는 지침의 수준을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="8bc05-172">초대형 리소스 클래스에서 제공하는 메모리를 초과하는 파티션의 크기는 피합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-172">Try to avoid sizing your partitions beyond the memory grant provided by the extra large resource class.</span></span> <span data-ttu-id="8bc05-173">이 그림을 초과하여 파티션을 확대하는 경우, 최적의 압축 상태가 아닌 메모리 부족의 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-173">If your partitions grow beyond this figure you run the risk of memory pressure which in turn leads to less optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="8bc05-174">파티션 전환</span><span class="sxs-lookup"><span data-stu-id="8bc05-174">Partition switching</span></span>
<span data-ttu-id="8bc05-175">SQL 데이터 웨어하우스는 파티션 분할, 병합 및 전환을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="8bc05-176">이러한 각 함수는 [ALTER TABLE][ALTER TABLE] 문을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-176">Each of these functions is excuted using the [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="8bc05-177">두 테이블 간에 파티션을 전환하려면 파티션을 각 해당 경계에 맞추고 테이블 정의와 일치하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-177">To switch partitions between two tables you must ensure that the partitions align on their respective boundaries and that the table definitions match.</span></span> <span data-ttu-id="8bc05-178">Check 제약 조건은 테이블에 있는 값의 범위를 적용하는 데 사용할 수 없으므로 원본 테이블은 대상 테이블과 동일한 파티션 경계를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-178">As check constraints are not available to enforce the range of values in a table the source table must contain the same partition boundaries as the target table.</span></span> <span data-ttu-id="8bc05-179">이 경우가 아닌 경우 파티션 전환은 파티션 메타데이터가 동기화되지 않아 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-179">If this is not the case, then the partition switch will fail as the partition metadata will not be synchronized.</span></span>

### <a name="how-to-split-a-partition-that-contains-data"></a><span data-ttu-id="8bc05-180">데이터를 포함하는 파티션을 분할하는 방법</span><span class="sxs-lookup"><span data-stu-id="8bc05-180">How to split a partition that contains data</span></span>
<span data-ttu-id="8bc05-181">데이터가 이미 들어 있는 파티션을 분할 하는 가장 효율적인 방법은 `CTAS` 문을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-181">The most efficient method to split a partition that already contains data is to use a `CTAS` statement.</span></span> <span data-ttu-id="8bc05-182">분할된 테이블이 CCL(clustered columnstore)인 경우 테이블 파티션이 비어 있어야 분할될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-182">If the partitioned table is a clustered columnstore then the table partition must be empty before it can be split.</span></span>

<span data-ttu-id="8bc05-183">다음은 각 파티션에 하나의 행을 포함하는 샘플 분할된 columnstore 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="8bc05-184">통계 개체를 만들어 해당 테이블 메타데이터가 더 정확함을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-184">By Creating the statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="8bc05-185">통계 작성을 생략하는 경우 SQL 데이터 웨어하우스는 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="8bc05-186">통계에 대한 자세한 내용은 [통계][statistics]를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="8bc05-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="8bc05-187">`sys.partitions` 카탈로그 뷰를 사용하여 행 개수에 대해 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-187">We can then query for the row count using the `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="8bc05-188">이 테이블을 분할하는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-188">If we try to split this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8bc05-189">파티션이 비어 있어 Msg 35346, 수준 15, 상태 1, 44행 ALTER PARTITION 문의 SPLIT 절이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because the partition is not empty.</span></span>  <span data-ttu-id="8bc05-190">Columnstore 인덱스가 테이블에 있는 경우 빈 파티션만 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-190">Only empty partitions can be split in when a columnstore index exists on the table.</span></span> <span data-ttu-id="8bc05-191">ALTER PARTITION 문을 실행한 다음 ALTER PARTITION 완료된 후에 Columnstore 인덱스를 다시 작성하기 전에 Columnstore 인덱스를 비활성화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-191">Consider disabling the columnstore index before issuing the ALTER PARTITION statement, then rebuilding the columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="8bc05-192">그러나 `CTAS` 를 사용하여 데이터를 저장할 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-192">However, we can use `CTAS` to create a new table to hold our data.</span></span>

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

<span data-ttu-id="8bc05-193">파티션 경계가 정렬되므로 전환이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-193">As the partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="8bc05-194">이후에 나눌 수 있는 빈 파티션이 있는 원본 테이블이 남습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-194">This will leave the source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="8bc05-195">`CTAS` 를 사용하여 새 파티션 경계에 데이터를 정렬하고 데이터를 다시 기본 테이블로 전환하는 것이 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-195">All that is left to do is to align our data to the new partition boundaries using `CTAS` and switch our data back in to the main table</span></span>

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

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 TO dbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="8bc05-196">데이터의 이동을 완료한 후에 각 분할에 있는 데이터의 새 배포를 정확히 반영되도록 대상 테이블에서 통계를 새로 고치는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-196">Once you have completed the movement of the data it is a good idea to refresh the statistics on the target table to ensure they accurately reflect the new distribution of the data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="8bc05-197">소스 제어를 분할하는 테이블</span><span class="sxs-lookup"><span data-stu-id="8bc05-197">Table partitioning source control</span></span>
<span data-ttu-id="8bc05-198">소스 제어 시스템에서 사용자 테이블 정의가 **녹슬지** 않도록 다음 방법을 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-198">To avoid your table definition from **rusting** in your source control system you may want to consider the following approach:</span></span>

1. <span data-ttu-id="8bc05-199">파티션 값이 없는 분할된 테이블로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-199">Create the table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="8bc05-200">`SPLIT` 배포 프로세스의 일부로서의 테이블:</span><span class="sxs-lookup"><span data-stu-id="8bc05-200">`SPLIT` the table as part of the deployment process:</span></span>

```sql
-- Create a table containing the partition boundaries

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

-- Iterate over the partition boundaries and split the table

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

<span data-ttu-id="8bc05-201">이 방법으로 소스 제어의 코드는 정적으로 유지되며 파티션 경계 값은 동적이 될 수 있습니다. 시간이 지남에 따라 웨어하우스가 발전됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bc05-201">With this approach the code in source control remains static and the partitioning boundary values are allowed to be dynamic; evolving with the warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bc05-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bc05-202">Next steps</span></span>
<span data-ttu-id="8bc05-203">자세히 알아보려면 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블 배포][Distribute], [테이블 인덱싱][Index], [테이블 통계 유지 관리][Statistics] 및 [임시 테이블][Temporary]에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bc05-203">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="8bc05-204">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bc05-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
