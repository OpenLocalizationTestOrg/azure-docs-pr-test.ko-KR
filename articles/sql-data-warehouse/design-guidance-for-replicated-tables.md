---
title: "복제 된 테이블-Azure SQL 데이터 웨어하우스에 대 한 aaaDesign 가이드 | Microsoft Docs"
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
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="658f2-103">Azure SQL Data Warehouse에서 복제 테이블 사용에 대한 디자인 지침</span><span class="sxs-lookup"><span data-stu-id="658f2-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="658f2-104">이 문서는 SQL Data Warehouse 스키마로 복제 테이블을 디자인하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="658f2-105">이러한 권장 사항을 tooimprove 쿼리 성능을 사용 하 여 데이터 이동 및 쿼리 복잡성을 줄여 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="658f2-106">hello 복제 테이블 기능은 현재 공개 미리 보기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="658f2-107">일부 동작은 주체 toochange는.</span><span class="sxs-lookup"><span data-stu-id="658f2-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="658f2-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="658f2-108">Prerequisites</span></span>
<span data-ttu-id="658f2-109">이 문서에서는 사용자가 SQL Data Warehouse의 데이터 배포 및 데이터 이동 개념에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="658f2-110">자세한 내용은 [분산 데이터](sql-data-warehouse-distributed-data.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="658f2-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="658f2-111">테이블 디자인의 일환으로, 데이터 및 hello 데이터를 쿼리 하는 방법에 대 한 가능한 한을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="658f2-112">예를 들어 다음 질문을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-112">For example, consider these questions:</span></span>

- <span data-ttu-id="658f2-113">향 테이블인 hello?</span><span class="sxs-lookup"><span data-stu-id="658f2-113">How large is hello table?</span></span>   
- <span data-ttu-id="658f2-114">Hello 테이블은 얼마나 자주 새로?</span><span class="sxs-lookup"><span data-stu-id="658f2-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="658f2-115">데이터 웨어하우스에 팩트 및 차원 테이블이 있나요?</span><span class="sxs-lookup"><span data-stu-id="658f2-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="658f2-116">복제 테이블이란?</span><span class="sxs-lookup"><span data-stu-id="658f2-116">What is a replicated table?</span></span>
<span data-ttu-id="658f2-117">복제 된 테이블에는 각 계산 노드가에 액세스할 수 있는 hello 테이블의 전체 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="658f2-118">테이블을 복제 하기 전에 조인 또는 집계를 계산 노드 간에 hello 필요 tootransfer 데이터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="658f2-119">Hello 테이블에 복사본을 여러 개 있으므로 hello 테이블 크기는 2GB 미만 압축 하는 경우 복제 된 테이블 가장 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="658f2-120">hello 다음 다이어그램에서는 각 계산 노드에 액세스할 수 있는 복제 테이블</span><span class="sxs-lookup"><span data-stu-id="658f2-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="658f2-121">SQL 데이터 웨어하우스 hello 복제 된 테이블에는 각 계산 노드에 대해 배포 데이터베이스를 완벽 하 게 복사 tooa은.</span><span class="sxs-lookup"><span data-stu-id="658f2-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="658f2-122">![복제 테이블](media/guidance-for-using-replicated-tables/replicated-table.png "복제 테이블")</span><span class="sxs-lookup"><span data-stu-id="658f2-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="658f2-123">복제 테이블은 별모양 스키마의 작은 차원 테이블에 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="658f2-124">차원 테이블에는 일반적으로 불가능 toostore 있도록 크기의 개와 여러 복사본을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="658f2-125">차원에는 고객 이름 및 주소, 제품 세부 정보와 같이 느리게 변하는 설명 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="658f2-126">느린 hello 데이터의 특성을 변경 하는 hello 안내 hello 복제 된 테이블의 toofewer 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="658f2-127">복제 테이블 사용을 고려하는 것이 좋은 경우:</span><span class="sxs-lookup"><span data-stu-id="658f2-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="658f2-128">디스크 hello 테이블 크기는 2GB 미만인, hello 행 개수에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="658f2-129">테이블의 toofind hello 크기 hello를 사용할 수 있습니다 [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) 명령: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="658f2-130">hello 테이블 데이터를 이동 해야 하는 조인에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="658f2-131">예를 들어 해시 distributed 테이블에 대 한 조인을 hello 조인 열은 동일한 배포 열 hello 하지 하는 경우 데이터 이동이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="658f2-132">Hello 해시 distributed 테이블 중 하나의 값이 작으면 복제 된 테이블을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="658f2-133">라운드 로빈 테이블에 조인하려면 데이터 이동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="658f2-134">대부분의 경우 라운드 로빈 테이블 대신 복제 테이블을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="658f2-135">복제 된 테이블 tooa distributed 기존 변환 하는 것이 좋습니다. 하면 테이블:</span><span class="sxs-lookup"><span data-stu-id="658f2-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="658f2-136">쿼리 계획을 사용 하 여 hello 데이터 tooall hello 계산 노드를 브로드캐스트하는 데이터 이동 작업.</span><span class="sxs-lookup"><span data-stu-id="658f2-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="658f2-137">hello BroadcastMoveOperation 상당히 소모 되며 쿼리 성능이 느려집니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="658f2-138">사용 하 여 쿼리 계획에서 데이터 이동 작업 tooview [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="658f2-139">복제 된 테이블 hello 최고의 쿼리 성능을 얻을 수 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="658f2-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="658f2-140">hello 테이블에는 빈번한 삽입, 업데이트 및 삭제 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="658f2-141">이러한 데이터 조작 언어 (DML) 작업 hello 복제 된 테이블의 다시 작성을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="658f2-142">다시 빌드가 빈번하면 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="658f2-143">데이터 웨어하우스 hello 자주 크기가 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="658f2-144">Hello 수가 계산 노드를 다시 발생 하는 변경 데이터 웨어하우스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="658f2-145">hello 테이블에 많은 수의 열, 하지만 데이터 작업에는 일반적으로 적은 수의 열만 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="658f2-146">Hello 전체 테이블을 복제 하는 대신이 시나리오에서 보다 효과적인 toohash 수도 hello 테이블을 배포 하 고 다음 자주 액세스 하는 hello 열에 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="658f2-147">필요한 경우에 쿼리 데이터 이동, SQL 데이터 웨어하우스만 hello에 대 한 이동 데이터 열을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="658f2-148">단순 쿼리 조건자로 복제 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="658f2-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="658f2-149">Toodistribute 선택 하거나 테이블을 복제 하기 전에 hello 유형의 쿼리 toorun hello 테이블에 대 한 계획에 대해 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="658f2-150">가능하면,</span><span class="sxs-lookup"><span data-stu-id="658f2-150">Whenever possible,</span></span>

- <span data-ttu-id="658f2-151">같음 또는 같지 않음과 같은 단순 쿼리 조건자를 사용한 쿼리에는 복제 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="658f2-152">LIKE 또는 NOT LIKE와 같은 복잡한 쿼리 조건자를 사용한 쿼리에는 분산 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="658f2-153">CPU 사용량이 많은 쿼리 hello 작업 모든 hello 계산 노드 배포 된 경우 가장 잘 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="658f2-154">예를 들어 테이블의 각 행에서 계산을 실행하는 쿼리는 복제 테이블에 비해 분산 테이블에서 성능이 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="658f2-155">복제 된 테이블, 각 계산 노드에 전체에 저장 되므로 모든 계산 노드에서 복제 된 테이블에 대 한 CPU 사용량이 많은 쿼리 hello 전체 테이블에 대해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="658f2-156">hello 추가 계산 성능이 느려질 수 있습니다 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="658f2-157">예를 들어 이 쿼리에는 복잡한 조건자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="658f2-158">이 쿼리는 공급자가 복제 테이블이 아니라 분산 테이블일 때 실행 속도가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="658f2-159">이 예제에서 공급자는 해시 분산 또는 라운드 로빈 분산 테이블일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="658f2-160">기존 라운드 로빈 테이블 tooreplicated 테이블 변환</span><span class="sxs-lookup"><span data-stu-id="658f2-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="658f2-161">라운드 로빈 테이블이 이미 있는 경우 권장 변환한 tooreplicated 테이블이이 문서에 설명 된 조건으로 충족 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="658f2-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="658f2-162">복제 된 테이블 데이터 이동에 대 한 hello 필요 하지 않으므로 라운드 로빈 테이블에 대해 성능을 향상 시킬.</span><span class="sxs-lookup"><span data-stu-id="658f2-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="658f2-163">라운드 로빈 테이블은 조인을 위해 데이터 이동이 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="658f2-164">이 예에서는 [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory 테이블 tooa 복제 된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="658f2-165">이 예제는 DimSalesTerritory가 해시 분산이거나 라운드 로빈이거나 상관없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="658f2-166">라운드 로빈 대비 복제에 대한 쿼리 성능 예제</span><span class="sxs-lookup"><span data-stu-id="658f2-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="658f2-167">복제 된 테이블 hello 전체 테이블은 각 계산 노드가 이미 있으므로 데이터 이동을 조인에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="658f2-168">Hello 차원 테이블은 라운드 로빈 배포, 조인 전체 tooeach 계산 노드에 hello 차원 테이블에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="658f2-169">toomove hello 데이터 hello 쿼리 계획 BroadcastMoveOperation 이라는 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="658f2-170">이런 유형의 데이터 이동 작업은 쿼리 성능을 저하시키며 복제 테이블을 사용하면 필요가 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="658f2-171">tooview 쿼리 계획 단계를 사용 하 여 hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) 시스템 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="658f2-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="658f2-172">예를 들어 hello AdventureWorks 스키마에 대해 다음 쿼리를 hello ` FactInternetSales` 테이블은 해시 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="658f2-173">hello `DimDate` 및 `DimSalesTerritory` 테이블은 작은 차원 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="658f2-174">이 쿼리 북미 지역에 2004 회계 연도 대 한 hello 총 판매액을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="658f2-175">`DimDate` 및 `DimSalesTerritory`를 라운드 로빈 테이블로 다시 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="658f2-176">결과적으로, hello 쿼리는 여러 브로드캐스트 이동 작업에 쿼리 계획을 따르는 hello 없다고 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![라운드 로빈 쿼리 계획](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="658f2-178">다시 생성 `DimDate` 및 `DimSalesTerritory` 로 복제 된 테이블을과 hello 쿼리를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="658f2-179">hello 결과 쿼리 계획은 훨씬 더 짧은 하 고 있는 모든 브로드캐스트되지 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![복제된 쿼리 계획](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="658f2-181">복제 테이블 수정에 대한 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="658f2-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="658f2-182">SQL 데이터 웨어하우스 hello 테이블의 마스터 버전을 유지 하 여 복제 된 테이블을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="658f2-183">각 계산 노드에 대해 hello 마스터 버전 tooone 배포 데이터베이스를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="658f2-184">변경 내용이 있을 때 SQL 데이터 웨어하우스는 먼저 hello 마스터 테이블을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="658f2-185">각 계산 노드에 대해 hello 테이블 다시 빌드할이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="658f2-186">Hello 테이블 tooeach 계산 노드를 복사 하 고 hello 인덱스 다시 작성 한 다음 복제 된 테이블 다시 빌드에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="658f2-187">다시 빌드가 필요한 경우:</span><span class="sxs-lookup"><span data-stu-id="658f2-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="658f2-188">데이터가 로드되었거나 수정된 후</span><span class="sxs-lookup"><span data-stu-id="658f2-188">Data is loaded or modified</span></span>
- <span data-ttu-id="658f2-189">hello 데이터 웨어하우스는 크기 조정 된 tooa 다른 DWU 설정</span><span class="sxs-lookup"><span data-stu-id="658f2-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="658f2-190">테이블 정의가 업데이트된 후</span><span class="sxs-lookup"><span data-stu-id="658f2-190">Table definition is updated</span></span>

<span data-ttu-id="658f2-191">다시 빌드가 필요하지 않은 경우:</span><span class="sxs-lookup"><span data-stu-id="658f2-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="658f2-192">작업 일시 중지 후</span><span class="sxs-lookup"><span data-stu-id="658f2-192">Pause operation</span></span>
- <span data-ttu-id="658f2-193">작업 일시 다시 시작 후</span><span class="sxs-lookup"><span data-stu-id="658f2-193">Resume operation</span></span>

<span data-ttu-id="658f2-194">데이터 수정 된 후에 즉시 hello 다시 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="658f2-195">Hello rebuild 대신 트리거되는 hello 처음으로 쿼리는 hello 테이블에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="658f2-196">Hello 테이블에서 초기 select 문의 hello 단계 toorebuild hello에 대 한 복제 된 테이블은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="658f2-197">Hello rebuild hello 쿼리 내에서 완료 되 면 hello 영향 toohello 초기 select 문의 hello 테이블의 hello 크기에 따라 중요 한 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="658f2-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="658f2-198">여러 복제 된 테이블에는 다시 작성 해야 하는 관련 된, 각 복사본 hello 문 내에서 단계로 순차적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="658f2-199">hello hello 다시 작성 하는 동안 데이터 일관성 toomaintain hello 테이블에서 사용 하는 배타적 잠금이 테이블을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="658f2-200">hello 잠금 hello 다시 작성 hello 기간에 대 한 모든 액세스 toohello 테이블을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="658f2-201">신중하게 인덱스 사용</span><span class="sxs-lookup"><span data-stu-id="658f2-201">Use indexes conservatively</span></span>
<span data-ttu-id="658f2-202">기본적인 인덱싱 tooreplicated 테이블을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="658f2-203">SQL 데이터 웨어하우스 hello 다시 작성의 일부로 각 복제 테이블 인덱스를 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="658f2-204">Hello 인덱스 다시 작성의 hello 비용을 능가 하는 hello 성능 향상에 도움이 되는 경우에 인덱스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="658f2-205">일괄 처리 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="658f2-205">Batch data loads</span></span>
<span data-ttu-id="658f2-206">복제 된 테이블에 데이터를 로드할 때 로드를 함께 일괄 처리 하 여 toominimize 다시 작성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="658f2-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="658f2-207">Select 문을 실행 하기 전에 모든 hello 일괄 처리 로드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="658f2-208">예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하고 4개의 다시 빌드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="658f2-209">원본 1에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-209">Load from source 1.</span></span>
- <span data-ttu-id="658f2-210">Select 문이 다시 빌드 1을 호출.</span><span class="sxs-lookup"><span data-stu-id="658f2-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="658f2-211">원본 2에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-211">Load from source 2.</span></span>
- <span data-ttu-id="658f2-212">Select 문이 다시 빌드 2를 호출.</span><span class="sxs-lookup"><span data-stu-id="658f2-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="658f2-213">원본 3에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-213">Load from source 3.</span></span>
- <span data-ttu-id="658f2-214">Select 문이 다시 빌드 3을 호출.</span><span class="sxs-lookup"><span data-stu-id="658f2-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="658f2-215">원본 4에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-215">Load from source 4.</span></span>
- <span data-ttu-id="658f2-216">Select 문이 다시 빌드 4를 호출.</span><span class="sxs-lookup"><span data-stu-id="658f2-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="658f2-217">예를 들어 다음 부하 패턴은 4개의 원본에서 데이터를 로드하지만 다시 빌드를 1개만 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="658f2-218">원본 1에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-218">Load from source 1.</span></span>
- <span data-ttu-id="658f2-219">원본 2에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-219">Load from source 2.</span></span>
- <span data-ttu-id="658f2-220">원본 3에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-220">Load from source 3.</span></span>
- <span data-ttu-id="658f2-221">원본 4에서 로드.</span><span class="sxs-lookup"><span data-stu-id="658f2-221">Load from source 4.</span></span>
- <span data-ttu-id="658f2-222">Select 문이 다시 빌드를 호출.</span><span class="sxs-lookup"><span data-stu-id="658f2-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="658f2-223">일괄 처리 로드 후 복제 테이블 다시 빌드</span><span class="sxs-lookup"><span data-stu-id="658f2-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="658f2-224">tooensure 일관성 있는 쿼리 실행 시간, 일괄 처리 로드 후 hello 복제 된 테이블의 새로 고침을 강제 적용 하면 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="658f2-225">그렇지 않으면 첫 번째 쿼리에서 hello hello 인덱스 다시 작성을 포함 하는 hello 테이블 toorefresh 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="658f2-226">Hello 크기 및 영향을 받는 복제 된 테이블의 수에 따라 hello 성능에 미치는 영향 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="658f2-227">이 쿼리에서 hello를 사용 하 여 [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello 수정 되었지만 다시 작성 하지 않은 테이블을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="658f2-228">tooforce 다시 작성, hello 문 hello 출력 앞의 각 테이블에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="658f2-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="658f2-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="658f2-229">Next steps</span></span> 
<span data-ttu-id="658f2-230">toocreate 복제 된 테이블을 사용 하 여 이러한 문 중 하나:</span><span class="sxs-lookup"><span data-stu-id="658f2-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="658f2-231">CREATE TABLE(Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="658f2-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="658f2-232">CREATE TABLE AS SELECT(Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="658f2-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="658f2-233">분산 테이블에 대한 개요는 [분산 테이블](sql-data-warehouse-tables-distribute.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="658f2-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



