---
title: "SQL 데이터 웨어하우스 테이블 aaaOverview | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 테이블로 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="70812-103">SQL 데이터 웨어하우스의 테이블 개요</span><span class="sxs-lookup"><span data-stu-id="70812-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="70812-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="70812-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="70812-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="70812-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="70812-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="70812-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="70812-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="70812-107">[Index][Index]</span></span>
> * <span data-ttu-id="70812-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="70812-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="70812-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="70812-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="70812-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="70812-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="70812-111">SQL 데이터 웨어하우스에서 테이블을 만드는 과정은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="70812-112">기본 hello [CREATE TABLE] [ CREATE TABLE] 구문을 따르는 가능성이 가장 hello 공통 된 구문과 방법을 이미 알고 있는 다른 데이터베이스와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="70812-113">테이블 toocreate 하기만 하면 tooname 테이블에 열 이름을 지정 하 고 각 열에 대 한 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="70812-114">다른 데이터베이스의 테이블을 작성 했으므로,이 전혀 낯설지 tooyou 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="70812-115">위 예제는 hello FirstName 및 LastName의 두 열을 가진 Customers 라는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70812-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="70812-116">각 열이 VARCHAR(25) hello 데이터 too25 문자 제한의 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="70812-117">테이블을 다른 사용자에 게 이러한 기본적인 특성은 다른 데이터베이스와 같은 hello 대부분 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="70812-118">데이터 형식은 각 열에 대해 정의 되 고 데이터의 hello 무결성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="70812-119">인덱스는 I/O를 줄임으로써 tooimprove 성능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70812-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="70812-120">분할 tooimprove 성능 때 추가 toomodify 데이터 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="70812-121">SQL Data Warehouse 테이블 [이름 바꾸기][RENAME] 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70812-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="70812-122">분산 테이블</span><span class="sxs-lookup"><span data-stu-id="70812-122">Distributed tables</span></span>
<span data-ttu-id="70812-123">SQL 데이터 웨어하우스는 hello와 같은 분산된 시스템에 의해 도입 된 새 기본 특성 **배포 열**합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="70812-124">hello 배포 열은 크게 그 말입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="70812-125">hello 열 결정 하는 방법을 toodistribute, 또는 나누기, hello 내부적 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="70812-126">Hello 배포 열을 지정 하지 않고 테이블을 만들 때 hello 테이블은 자동으로 배포를 사용 하 여 **라운드 로빈**합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="70812-127">일부 시나리오에서는 라운드 로빈 테이블로 충분할 수 있지만 배포 열을 정의하면 쿼리 중에 데이터 이동을 크게 줄일 수 있으므로 성능이 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="70812-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="70812-128">경우에 테이블의 데이터 적은 양의 있는 hello로 toocreate hello 테이블을 선택 합니다. **복제** 분포 유형 데이터 tooeach 계산 노드를 복사 하 고 쿼리 실행 시 데이터 이동을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="70812-129">참조 [테이블 배포] [ Distribute] toolearn 방법에 대 한 자세한 tooselect는 배포 열입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="70812-130">테이블 인덱싱 및 분할</span><span class="sxs-lookup"><span data-stu-id="70812-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="70812-131">SQL 데이터 웨어하우스를 사용 하 여 더 높은 수준의 되 고 toooptimize 성능을 toolearn 테이블 디자인에 대 한 자세한 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70812-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="70812-132">toolearn에 hello 문서를 더 참조 [테이블 데이터 형식][Data Types], [테이블 배포][Distribute], [테이블 인덱스를 만들] [ Index] 및 [테이블 분할][Partition]합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="70812-133">테이블 통계</span><span class="sxs-lookup"><span data-stu-id="70812-133">Table statistics</span></span>
<span data-ttu-id="70812-134">통계는 매우 중요 toogetting hello 성능을 극대화 하 여 SQL 데이터 웨어하우스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="70812-135">SQL 데이터 웨어하우스는 아직 자동으로 만들고 업데이트 통계, 처럼 tooexpect Azure SQL 데이터베이스에서 발견 했을 수 있습니다, 때문에 문서를 읽는 [통계] [ Statistics] hello 중 하나일 수 있습니다 tooensure를 읽는 가장 중요 한 문서에서 쿼리 hello 최상의 성능을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70812-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="70812-136">임시 테이블</span><span class="sxs-lookup"><span data-stu-id="70812-136">Temporary tables</span></span>
<span data-ttu-id="70812-137">임시 테이블은만 사용자의 로그온의 hello 기간에 대 한 존재 하 고 다른 사용자가 볼 수 없는 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="70812-138">임시 테이블 한 임시 결과 보지 못하도록 좋은 방법 tooprevent 다른 사용자를 수 있으며 정리에 대 한 hello 필요성을 줄일 수도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70812-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="70812-139">임시 테이블은 로컬 저장소를 활용하므로 일부 작업에 대해 더 빠른 성능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70812-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="70812-140">Hello 참조 [임시 테이블] [ Temporary] 임시 테이블에 대 한 자세한 내용은 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="70812-141">외부 테이블</span><span class="sxs-lookup"><span data-stu-id="70812-141">External tables</span></span>
<span data-ttu-id="70812-142">외부 테이블의 경우 라고도 Polybase 테이블은 SQL 데이터 웨어하우스, 하지만 SQL 데이터 웨어하우스 로부터 외부 지점 toodata에서 쿼리할 수 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="70812-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="70812-143">예를 들어 만들면 외부 테이블 어떤 지점 toofiles Azure Blob 저장소에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70812-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="70812-144">에 대 한 자세한 내용은 toocreate 및 쿼리는 외부 테이블이 참조 하는 방법을 [Polybase 사용 하 여 데이터 로드][Load data with Polybase]합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="70812-145">지원되지 않는 테이블 기능</span><span class="sxs-lookup"><span data-stu-id="70812-145">Unsupported table features</span></span>
<span data-ttu-id="70812-146">SQL 데이터 웨어하우스 hello 다른 데이터베이스에서 제공 하는 동일한 테이블 기능을 많이 포함 되 고, 지원 되지 않는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70812-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="70812-147">다음은 목록 hello 중 일부의 지원 되지 않는 테이블 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="70812-148">지원되지 않는 기능</span><span class="sxs-lookup"><span data-stu-id="70812-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="70812-149">기본 키, 외래 키, 고유 및 검사 [테이블 제약 조건][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="70812-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="70812-150">[고유 인덱스][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="70812-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="70812-151">[계산된 열][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="70812-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="70812-152">[스파스 열][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="70812-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="70812-153">[사용자 정의 형식][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="70812-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="70812-154">[시퀀스][Sequence]</span><span class="sxs-lookup"><span data-stu-id="70812-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="70812-155">[트리거][Triggers]</span><span class="sxs-lookup"><span data-stu-id="70812-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="70812-156">[인덱싱된 뷰][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="70812-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="70812-157">[동의어][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="70812-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="70812-158">테이블 크기 쿼리</span><span class="sxs-lookup"><span data-stu-id="70812-158">Table size queries</span></span>
<span data-ttu-id="70812-159">하나의 간단한 방법 tooidentify 공간과 hello 60 배포의 각 테이블에서 사용 하는 행은 toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED]합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="70812-160">그러나 DBCC 명령을 사용하면 작업이 상당히 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70812-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="70812-161">동적 관리 뷰 (Dmv)를 toosee 통해 훨씬 더 자세히 설명으로 hello 쿼리 결과 대 한 훨씬 더 세부적인 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="70812-162">이 예제와 다른 문서 참조 tooby 됩니다이 보기에서는 다양 한 예제를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a><span data-ttu-id="70812-163">테이블 공간 요약</span><span class="sxs-lookup"><span data-stu-id="70812-163">Table space summary</span></span>
<span data-ttu-id="70812-164">이 쿼리에서 테이블 여 hello 행과 공간을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="70812-165">테이블은 가장 큰 테이블 및은 라운드 로빈, 복제 또는 해시 distributed 좋은 쿼리 toosee 이며</span><span class="sxs-lookup"><span data-stu-id="70812-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="70812-166">또한 배포 되는 해시 테이블에 대 한 hello 배포 열을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="70812-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="70812-167">대부분의 경우 가장 큰 테이블은 클러스터된 columnstore 인덱스로 배포된 해시여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="70812-168">배포 유형별 테이블 공간</span><span class="sxs-lookup"><span data-stu-id="70812-168">Table space by distribution type</span></span>
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a><span data-ttu-id="70812-169">인덱스 유형별 테이블 공간</span><span class="sxs-lookup"><span data-stu-id="70812-169">Table space by index type</span></span>
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a><span data-ttu-id="70812-170">배포 공간 요약</span><span class="sxs-lookup"><span data-stu-id="70812-170">Distribution space summary</span></span>
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a><span data-ttu-id="70812-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70812-171">Next steps</span></span>
<span data-ttu-id="70812-172">toolearn에 hello 문서를 더 참조 [테이블 데이터 형식][Data Types], [테이블 배포][Distribute], [테이블 인덱스를 만들] [ Index], [테이블 분할][Partition], [테이블 통계를 유지 관리] [ Statistics] 및 [ 임시 테이블][Temporary]합니다.</span><span class="sxs-lookup"><span data-stu-id="70812-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="70812-173">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70812-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
