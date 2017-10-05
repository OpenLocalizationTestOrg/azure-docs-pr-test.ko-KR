---
title: "복제 테이블에 대한 디자인 지침 - Azure SQL Data Warehouse | Microsoft Docs"
description: "Azure SQL Data Warehouse 스키마로 복제 테이블을 디자인하기 위한 권장 사항입니다."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="6b328-103">Azure SQL Data Warehouse에서 복제 테이블 사용에 대한 디자인 지침</span><span class="sxs-lookup"><span data-stu-id="6b328-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6b328-104">이 문서는 SQL Data Warehouse 스키마로 복제 테이블을 디자인하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="6b328-105">이러한 권장 사항을 사용하여 데이터 이동 및 쿼리 복잡성을 줄여서 쿼리 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="6b328-106">복제 테이블 기능은 현재 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="6b328-107">일부 동작은 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="6b328-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6b328-108">Prerequisites</span></span>
<span data-ttu-id="6b328-109">이 문서에서는 사용자가 SQL Data Warehouse의 데이터 배포 및 데이터 이동 개념에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="6b328-110">자세한 내용은 [분산 데이터](sql-data-warehouse-distributed-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b328-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="6b328-111">테이블 디자인의 일환으로 데이터 및 데이터가 쿼리되는 방식에 대해 최대한 많이 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="6b328-112">예를 들어 다음 질문을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-112">For example, consider these questions:</span></span>

- <span data-ttu-id="6b328-113">테이블이 얼마나 큰가요?</span><span class="sxs-lookup"><span data-stu-id="6b328-113">How large is the table?</span></span>   
- <span data-ttu-id="6b328-114">테이블을 얼마나 자주 새로 고치나요?</span><span class="sxs-lookup"><span data-stu-id="6b328-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="6b328-115">데이터 웨어하우스에 팩트 및 차원 테이블이 있나요?</span><span class="sxs-lookup"><span data-stu-id="6b328-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="6b328-116">복제 테이블이란?</span><span class="sxs-lookup"><span data-stu-id="6b328-116">What is a replicated table?</span></span>
<span data-ttu-id="6b328-117">복제 테이블에는 각 계산 노드에서 액세스할 수 있는 테이블의 전체 복사본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="6b328-118">테이블을 복제하면 조인 또는 집계 전에 계산 노드 간에 데이터를 전송하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="6b328-119">테이블에 여러 복사본이 있으므로 복제 테이블은 테이블 크기가 2GB 미만으로 압축되어 있을 때 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="6b328-120">다음은 각 계산 노드에서 액세스할 수 있는 복제 테이블을 보여 주는 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="6b328-121">SQL Data Warehouse에서 복제 테이블은 각 계산 노드의 배포 데이터베이스로 완벽하게 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="6b328-122">![복제 테이블](media/guidance-for-using-replicated-tables/replicated-table.png "복제 테이블")</span><span class="sxs-lookup"><span data-stu-id="6b328-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="6b328-123">복제 테이블은 별모양 스키마의 작은 차원 테이블에 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="6b328-124">차원 테이블은 대개 여러 복사본을 저장하고 유지 관리하기에 적당한 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="6b328-125">차원에는 고객 이름 및 주소, 제품 세부 정보와 같이 느리게 변하는 설명 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="6b328-126">느리게 변하는 데이터의 특성으로 인해 복제 테이블을 다시 빌드하는 경우가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="6b328-127">복제 테이블 사용을 고려하는 것이 좋은 경우:</span><span class="sxs-lookup"><span data-stu-id="6b328-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="6b328-128">행의 수에 관계없이 디스크의 테이블 크기가 2GB미만입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="6b328-129">테이블 크기를 알아보려면 [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) 명령을 사용하세요. `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="6b328-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="6b328-130">복제 테이블이 아니면 데이터 이동이 필요한 조인에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="6b328-131">예를 들어 해시 분산 테이블의 조인은 조인하는 열이 배포 열과 같지 않은 경우 데이터 이동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="6b328-132">해시 분산 테이블 중 하나가 작으면 복제 테이블을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="6b328-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="6b328-133">라운드 로빈 테이블에 조인하려면 데이터 이동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="6b328-134">대부분의 경우 라운드 로빈 테이블 대신 복제 테이블을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="6b328-135">기존 분산 테이블을 복제 테이블로 변환하는 것이 좋은 경우:</span><span class="sxs-lookup"><span data-stu-id="6b328-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="6b328-136">쿼리 계획이 데이터를 모든 계산 노드에 브로드캐스트하는 데이터 이동 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="6b328-137">BroadcastMoveOperation은 비용이 많이 들고 쿼리 성능이 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="6b328-138">쿼리 계획에서 데이터 이동 작업을 보려면 [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="6b328-139">복제 테이블이 최상의 쿼리 성능을 얻을 수 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6b328-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="6b328-140">테이블에 삽입, 업데이트 및 삭제 작업이 빈번합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="6b328-141">이러한 DML(데이터 조작 언어) 작업에는 복제 테이블 다시 빌드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="6b328-142">다시 빌드가 빈번하면 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="6b328-143">데이터 웨어하우스의 크기가 자주 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="6b328-144">데이터 웨어하우스의 크기를 조정하면 계산 노드의 수가 변경되고 이로 인해 다시 빌드가 필요해집니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="6b328-145">테이블에는 다수의 열이 있지만 데이터 작업은 대개 작은 수의 열에만 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="6b328-146">이 시나리오에서는 전체 테이블을 복제하는 대신 테이블을 해시 분산한 다음 자주 액세스하는 열의 인덱스를 만드는 것이 보다 효과적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="6b328-147">쿼리에 데이터 이동이 필요하면 SQL Data Warehouse는 요청된 열의 데이터만 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="6b328-148">단순 쿼리 조건자로 복제 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="6b328-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="6b328-149">테이블 분산 또는 복제를 선택하기 전에 테이블에 실행할 쿼리 유형에 대해 생각해보세요.</span><span class="sxs-lookup"><span data-stu-id="6b328-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="6b328-150">가능하면,</span><span class="sxs-lookup"><span data-stu-id="6b328-150">Whenever possible,</span></span>

- <span data-ttu-id="6b328-151">같음 또는 같지 않음과 같은 단순 쿼리 조건자를 사용한 쿼리에는 복제 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="6b328-152">LIKE 또는 NOT LIKE와 같은 복잡한 쿼리 조건자를 사용한 쿼리에는 분산 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="6b328-153">CPU를 많이 사용하는 쿼리는 모든 계산 노드에 작업이 분산되면 성능이 가장 좋아집니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="6b328-154">예를 들어 테이블의 각 행에서 계산을 실행하는 쿼리는 복제 테이블에 비해 분산 테이블에서 성능이 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="6b328-155">복제 테이블은 각 계산 노드에 전체가 저장되므로 복제 테이블에 대해 CPU를 많이 사용하는 쿼리는 각 계산 노드의 전체 테이블에 대해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="6b328-156">추가 계산은 쿼리 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="6b328-157">예를 들어 이 쿼리에는 복잡한 조건자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="6b328-158">이 쿼리는 공급자가 복제 테이블이 아니라 분산 테이블일 때 실행 속도가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="6b328-159">이 예제에서 공급자는 해시 분산 또는 라운드 로빈 분산 테이블일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="6b328-160">기존의 라운드 로빈 테이블을 복제 테이블로 변환</span><span class="sxs-lookup"><span data-stu-id="6b328-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="6b328-161">라운드 로빈 테이블이 이미 있는 경우 이 문서에 설명된 조건을 충족한다면 복제 테이블로 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="6b328-162">복제 테이블은 데이터 이동의 필요성을 없애기 때문에 라운드 로빈 테이블보다 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="6b328-163">라운드 로빈 테이블은 조인을 위해 데이터 이동이 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="6b328-164">이 예제는 [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)를 사용하여 DimSalesTerritory 테이블을 복제 테이블로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="6b328-165">이 예제는 DimSalesTerritory가 해시 분산이거나 라운드 로빈이거나 상관없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="6b328-166">라운드 로빈 대비 복제에 대한 쿼리 성능 예제</span><span class="sxs-lookup"><span data-stu-id="6b328-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="6b328-167">복제 테이블은 각각의 계산 노드에 전체 테이블이 이미 존재하기 때문에 조인을 위해 데이터를 이동할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="6b328-168">차원 테이블이 라운드 로빈 분산이면 조인은 각각의 계산 노드에 차원 테이블 전체를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="6b328-169">데이터를 이동하려면 쿼리 계획에 BroadcastMoveOperation이라는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="6b328-170">이런 유형의 데이터 이동 작업은 쿼리 성능을 저하시키며 복제 테이블을 사용하면 필요가 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="6b328-171">쿼리 계획 단계를 보려면 [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) 시스템 카탈로그 보기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="6b328-172">예를 들어 AdventureWorks 스키마에 대한 다음 쿼리에서 ` FactInternetSales` 테이블은 해시 분산입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="6b328-173">`DimDate` 및 `DimSalesTerritory` 테이블은 작은 차원 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="6b328-174">이 쿼리는 회계 연도 2004년에 대한 북아메리카 지역의 총 매출을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="6b328-175">`DimDate` 및 `DimSalesTerritory`를 라운드 로빈 테이블로 다시 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="6b328-176">그에 따라 쿼리에 다수의 브로드캐스트 이동 작업이 포함된 다음과 같은 쿼리 계획이 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![라운드 로빈 쿼리 계획](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="6b328-178">`DimDate` 및 `DimSalesTerritory`를 복제 테이블로 다시 만들고 쿼리를 다시 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="6b328-179">결과 쿼리 계획은 훨씬 더 짧으며 브로드캐스트 이동이 하나도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![복제된 쿼리 계획](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="6b328-181">복제 테이블 수정에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6b328-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="6b328-182">SQL Data Warehouse는 테이블의 마스터 버전을 유지하여 복제 테이블을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="6b328-183">마스터 버전을 각 계산 노드에 있는 하나의 배포 데이터베이스에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="6b328-184">변경 내용이 있으면 SQL Data Warehouse는 먼저 마스터 테이블을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="6b328-185">그런 다음 각각의 계산 노드에 테이블 다시 빌드를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="6b328-186">복제 테이블 다시 빌드에는 각 계산 노드로 테이블을 복사한 다음 인덱스를 다시 빌드하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="6b328-187">다시 빌드가 필요한 경우:</span><span class="sxs-lookup"><span data-stu-id="6b328-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="6b328-188">데이터가 로드되었거나 수정된 후</span><span class="sxs-lookup"><span data-stu-id="6b328-188">Data is loaded or modified</span></span>
- <span data-ttu-id="6b328-189">데이터 웨어하우스가 다른 DWU 설정으로 크기가 조정된 후</span><span class="sxs-lookup"><span data-stu-id="6b328-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="6b328-190">테이블 정의가 업데이트된 후</span><span class="sxs-lookup"><span data-stu-id="6b328-190">Table definition is updated</span></span>

<span data-ttu-id="6b328-191">다시 빌드가 필요하지 않은 경우:</span><span class="sxs-lookup"><span data-stu-id="6b328-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="6b328-192">작업 일시 중지 후</span><span class="sxs-lookup"><span data-stu-id="6b328-192">Pause operation</span></span>
- <span data-ttu-id="6b328-193">작업 일시 다시 시작 후</span><span class="sxs-lookup"><span data-stu-id="6b328-193">Resume operation</span></span>

<span data-ttu-id="6b328-194">다시 빌드는 데이터가 수정된 직후 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="6b328-195">대신 쿼리가 테이블에서 처음 선택하면 다시 빌드가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="6b328-196">테이블의 초기 select 문에 복제 테이블을 다시 빌드하는 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="6b328-197">다시 빌드는 쿼리 내에서 수행되므로 초기 select 문에 미치는 영향은 테이블 크기에 따라 크게 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="6b328-198">다시 빌드가 필요한 다수의 복제 테이블이 관련된 경우 각 복사본은 명령문 내의 단계로 순차적으로 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="6b328-199">복제 테이블을 다시 빌드하는 동안 데이터 일관성을 유지하기 위해 테이블에 배타적 잠금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="6b328-200">잠금은 다시 빌드하는 동안 테이블에 대한 모든 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="6b328-201">신중하게 인덱스 사용</span><span class="sxs-lookup"><span data-stu-id="6b328-201">Use indexes conservatively</span></span>
<span data-ttu-id="6b328-202">표준 인덱싱 작업은 복제 테이블에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="6b328-203">SQL Data Warehouse는 다시 빌드의 일환으로 각 복제 테이블 인덱스를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="6b328-204">인덱스는 해당 성능이 인덱스를 다시 빌드하는 비용보다 높은 경우에만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="6b328-205">일괄 처리 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="6b328-205">Batch data loads</span></span>
<span data-ttu-id="6b328-206">복제 테이블로 데이터를 로드하는 경우 로드를 함께 일괄 처리하여 다시 빌드를 최소화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="6b328-207">select 문을 실행하기 전에 일괄 처리된 모든 로드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="6b328-208">예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하고 4개의 다시 빌드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="6b328-209">원본 1에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-209">Load from source 1.</span></span>
- <span data-ttu-id="6b328-210">Select 문이 다시 빌드 1을 호출.</span><span class="sxs-lookup"><span data-stu-id="6b328-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="6b328-211">원본 2에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-211">Load from source 2.</span></span>
- <span data-ttu-id="6b328-212">Select 문이 다시 빌드 2를 호출.</span><span class="sxs-lookup"><span data-stu-id="6b328-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="6b328-213">원본 3에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-213">Load from source 3.</span></span>
- <span data-ttu-id="6b328-214">Select 문이 다시 빌드 3을 호출.</span><span class="sxs-lookup"><span data-stu-id="6b328-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="6b328-215">원본 4에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-215">Load from source 4.</span></span>
- <span data-ttu-id="6b328-216">Select 문이 다시 빌드 4를 호출.</span><span class="sxs-lookup"><span data-stu-id="6b328-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="6b328-217">예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하지만 다시 빌드를 1개만 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="6b328-218">원본 1에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-218">Load from source 1.</span></span>
- <span data-ttu-id="6b328-219">원본 2에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-219">Load from source 2.</span></span>
- <span data-ttu-id="6b328-220">원본 3에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-220">Load from source 3.</span></span>
- <span data-ttu-id="6b328-221">원본 4에서 로드.</span><span class="sxs-lookup"><span data-stu-id="6b328-221">Load from source 4.</span></span>
- <span data-ttu-id="6b328-222">Select 문이 다시 빌드를 호출.</span><span class="sxs-lookup"><span data-stu-id="6b328-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="6b328-223">일괄 처리 로드 후 복제 테이블 다시 빌드</span><span class="sxs-lookup"><span data-stu-id="6b328-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="6b328-224">일관적인 쿼리 실행 시간을 보장하기 위해 일괄 처리 로드 후 복제 테이블을 강제로 새로 고치는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="6b328-225">그렇지 않으면 첫 번째 쿼리는 테이블을 새로 고칠 때까지 기다렸다가 인덱스를 다시 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="6b328-226">영향을 받는 복제 테이블의 크기와 수에 따라 성능에 미치는 영향을 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="6b328-227">다음 쿼리는 [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV를 사용하여 수정되었지만 다시 빌드되지 않은 복제 테이블을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="6b328-228">다시 빌드를 강제 적용하려면 위의 출력의 각 테이블에 다음 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="6b328-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b328-229">Next steps</span></span> 
<span data-ttu-id="6b328-230">복제 테이블을 만들려면 다음 문 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b328-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="6b328-231">CREATE TABLE(Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="6b328-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="6b328-232">CREATE TABLE AS SELECT(Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6b328-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="6b328-233">분산 테이블에 대한 개요는 [분산 테이블](sql-data-warehouse-tables-distribute.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b328-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



