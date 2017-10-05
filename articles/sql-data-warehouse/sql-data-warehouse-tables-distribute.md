---
title: "SQL Data Warehouse의 테이블 배포 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 테이블 배포 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="c3b2e-103">SQL 데이터 웨어하우스의 테이블 배포</span><span class="sxs-lookup"><span data-stu-id="c3b2e-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c3b2e-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c3b2e-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="c3b2e-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="c3b2e-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-107">[Index][Index]</span></span>
> * <span data-ttu-id="c3b2e-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="c3b2e-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="c3b2e-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="c3b2e-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="c3b2e-111">SQL 데이터 웨어하우스는 방대한 병렬 처리(MPP) 분산 데이터베이스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="c3b2e-112">여러 노드에 걸쳐 데이터와 처리 용량을 구분하여 SQL 데이터 웨어하우스는 모든 단일 시스템을 넘어서는 매우 큰 확장성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="c3b2e-113">SQL 데이터 웨어하우스 내에서 데이터를 배포하는 방법을 결정하는 일은 최적의 성능을 달성하는 데 있어서 가장 중요한 요소 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="c3b2e-114">성능을 최적화하기 위한 핵심 요인은 데이터 이동을 최소화하는 것이며, 데이터 이동을 최소화하는 핵심 요인은 올바른 배포 전략을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="c3b2e-115">데이터 이동 이해</span><span class="sxs-lookup"><span data-stu-id="c3b2e-115">Understanding data movement</span></span>
<span data-ttu-id="c3b2e-116">MPP 시스템에서 각 테이블의 데이터는 여러 기본 데이터베이스 간에 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="c3b2e-117">MPP 시스템에서 가장 최적화된 쿼리는 다른 데이터베이스 간의 상호 작용 없이 개별 분산 데이터베이스에서 실행하기 위해 간단히 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="c3b2e-118">예를 들어 영업과 고객이란 두 테이블을 포함하는 판매 데이터를 가진 데이타베이스가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="c3b2e-119">영업 테이블을 고객 테이블에 조인해야 하는 쿼리 있고 영업 및 고객 테이블을 고객 번호별로 나눠 각 고객이 다른 데이터베이스에 들어가게 한다면 영업과 고객을 조인하는 쿼리는 다른 데이터베이스에 대해 알지 못해도 각 데이터베이스 내에서 해결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="c3b2e-120">반면, 영업 데이터를 주문 번호별로 그리고 고객 데이터를 고객 번호별로 분할한 경우 지정된 데이터베이스는 각 고객에 대해 해당 데이터를 갖지 않으므로 영업 데이터를 고객 데이터에 조인하려는 경우 다른 데이터베이스에서 각 고객에 대한 데이터를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="c3b2e-121">이 두 번째 예제에서는 두 테이블을 조인할 수 있도록 고객 데이터를 영업 데이터로 이동하기 위해 데이터 이동이 일어나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="c3b2e-122">데이터 이동이 항상 나쁜 것은 아닙니다. 때로 쿼리를 해결하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="c3b2e-123">그러나 이 추가 단계를 피할 수 있다면, 자연스럽게 쿼리는 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="c3b2e-124">데이터 이동은 테이블이 조인되거나 집계가 수행될 때 흔히 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="c3b2e-125">조인과 같은 한 가지 시나리오에 대한 최적화를 할 수 있는 한편 집계와 같은 다른 시나리오를 해결하기 위해 데이터 이동이 여전히 필요하므로 흔히 두 작업을 모두 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="c3b2e-126">어느 쪽이 더 적은 작업을 하는지 파악하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="c3b2e-127">대부분의 경우 일반적으로 조인된 열에 대형 팩트 테이블을 분산하는 것이 대부분의 데이터 이동을 줄이는 가장 효과적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="c3b2e-128">조인 열에서의 데이터 배포는 집계와 관련된 열에서 데이터를 배포하는 것보다 데이터 이동을 줄이기 위한 훨씬 더 일반적인 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="c3b2e-129">배포 방법 선택</span><span class="sxs-lookup"><span data-stu-id="c3b2e-129">Select distribution method</span></span>
<span data-ttu-id="c3b2e-130">내부적으로 SQL 데이터 웨어하우스는 데이터를 60개의 데이터베이스로 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="c3b2e-131">각 개별 데이터베이스를 **배포**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="c3b2e-132">데이터가 각 테이블에 로드되면 SQL 데이터 웨어하우스는 데이터를 이러한 60개 배포로 나누는 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="c3b2e-133">배포 방법은 테이블 수준에서 정의되며 현재 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="c3b2e-134">**라운드 로빈** : 데이터를 임의로 균일하게 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="c3b2e-135">**해시 분산** : 단일 열의 해싱 값에 따라 데이터를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="c3b2e-136">기본적으로 데이터 배포 메서드를 정의하지 않으면 테이블이 **라운드 로빈** 배포 방법을 사용하여 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="c3b2e-137">그러나 구현이 좀 더 정교해 질수록 **해시 분산** 테이블을 사용하여 데이터 이동을 최소화하고 쿼리 성능을 최적화하는 것을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="c3b2e-138">라운드 로빈 테이블</span><span class="sxs-lookup"><span data-stu-id="c3b2e-138">Round Robin Tables</span></span>
<span data-ttu-id="c3b2e-139">라운드 로빈 데이터 배포 방법은 표현 그대로입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="c3b2e-140">데이터가 로드될 때 각 행은 단순히 다음 배포로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="c3b2e-141">이 데이터 배포 방법은 항상 모든 배포에 무작위로 균일하게 데이터를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="c3b2e-142">즉, 데이터를 배치하는 라운드 로빈 프로세스 중에 정렬이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="c3b2e-143">이러한 이유로 라운드 로빈 배포를 임의 해시라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="c3b2e-144">라운드 로빈 분산된 테이블을 사용하면 데이터를 이해하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="c3b2e-145">이러한 이유로 라운드 로빈 테이블은 종종 좋은 로드 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="c3b2e-146">기본적으로 배포 방법을 선택하지 않으면 라운드 로빈 배포 방법이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="c3b2e-147">그러나 라운드 로빈 테이블은 사용하기 쉽지만 데이터가 시스템에서 무작위로 분산되므로 각 행이 어떤 배포에 포함되는지 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="c3b2e-148">결과적으로 경우에 따라 시스템은 쿼리를 해결하기 위해 먼저 데이터 이동 작업을 호출하여 데이터를 좀 더 나은 방식으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="c3b2e-149">이 추가 단계로 인해 쿼리 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="c3b2e-150">다음 시나리오에서는 테이블에 대해 라운드 로빈 배포를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="c3b2e-151">간단한 시작점으로 시작하는 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="c3b2e-152">명백한 조인 키가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="c3b2e-153">테이블의 해시 분산에 적합한 후보 열이 없는 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="c3b2e-154">테이블이 다른 테이블과 공통 조인 키를 공유하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="c3b2e-155">조인이 쿼리의 다른 조인보다 덜 중요한 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="c3b2e-156">테이블이 임시 준비 테이블인 경우</span><span class="sxs-lookup"><span data-stu-id="c3b2e-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="c3b2e-157">다음 두 예제에서는 라운드 로빈 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="c3b2e-158">라운드 로빈이 기본 테이블 형식이지만, 테이블 레이아웃의 의도가 다른 사용자에게 명확하게 드러나도록, DDL에서 명시적으로 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="c3b2e-159">해시 분산 테이블</span><span class="sxs-lookup"><span data-stu-id="c3b2e-159">Hash Distributed Tables</span></span>
<span data-ttu-id="c3b2e-160">**해시 분산** 알고리즘을 사용하여 테이블을 배포하면 쿼리 시간에 데이터 이동이 감소되어 다양한 시나리오에 대한 성능이 향상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="c3b2e-161">해시 분산 테이블이란 선택한 단일 열에서 해시 알고리즘을 사용하여 분산 데이터베이스 간에 분할되는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="c3b2e-162">배포 열은 분산된 데이터베이스 간에 데이터가 분할되는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="c3b2e-163">해시 함수는 배포 열을 사용하여 배포에 행을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="c3b2e-164">해시 알고리즘 및 결과 배포는 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="c3b2e-165">동일한 데이터 형식의 동일한 값은 항상 동일한 배포를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="c3b2e-166">이 예제에서는 ID에 따라 분산된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="c3b2e-167">배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="c3b2e-167">Select distribution column</span></span>
<span data-ttu-id="c3b2e-168">테이블을 **해시 분산** 하기로 선택하는 경우 단일 배포 열을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="c3b2e-169">배포 열을 선택할 때 세 가지 주요 요소를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="c3b2e-170">다음과 같은 단일 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-170">Select a single column which will:</span></span>

1. <span data-ttu-id="c3b2e-171">업데이트되지 않는 열</span><span class="sxs-lookup"><span data-stu-id="c3b2e-171">Not be updated</span></span>
2. <span data-ttu-id="c3b2e-172">데이터를 고르게 분산하는 열(데이터 오차 방지에 필요)</span><span class="sxs-lookup"><span data-stu-id="c3b2e-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="c3b2e-173">데이터 이동 최소화</span><span class="sxs-lookup"><span data-stu-id="c3b2e-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="c3b2e-174">업데이트되지 않을 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="c3b2e-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="c3b2e-175">배포 열은 업데이트할 수 없으므로 정적 값을 갖는 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="c3b2e-176">업데이트해야 하는 열은 적합한 배포 후보가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="c3b2e-177">배포 열을 업데이트해야 하는 경우 먼저 해당 행을 삭제한 다음 새 행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="c3b2e-178">데이터를 균일하게 분산하는 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="c3b2e-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="c3b2e-179">분산 시스템은 가장 느린 배포 정도의 속도로 수행되므로 시스템에서 분산된 실행을 구현하려면 배포 간에 작업을 균일하게 분산하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="c3b2e-180">분산 시스템에서 작업이 분할되는 방식은 각 배포의 데이터가 있는 위치에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="c3b2e-181">따라서 각 배포가 같은 작업을 포함하고 해당 작업 부분을 완료하는 데 동일한 시간이 소요되도록 데이터를 분산하기 위한 적합한 배포 열을 선택하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="c3b2e-182">시스템 전체에서 작업이 적절하게 분할되면 분산된 작업 간에 데이터가 적절하게 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="c3b2e-183">데이터가 균등하게 분산되지 않은 상태를 **데이터 오차**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="c3b2e-184">데이터를 균일하게 나누고 데이터 오차를 방지하려면 배포 열을 선택할 때 다음 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="c3b2e-185">많은 수의 고유 값을 포함하는 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="c3b2e-186">고유 값이 많지 않은 열에는 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="c3b2e-187">null 수가 많은 열에는 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="c3b2e-188">날짜 열에 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="c3b2e-189">각 값은 60개 분산 중 하나로 해시되므로 데이터를 균일하게 분산하기 위해 고유한 값이 60개보다 많이 포함된 매우 고유한 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="c3b2e-190">예를 들어 열에 고유 값이 40개만 있는 경우를 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="c3b2e-191">이 열을 배포 키로 선택한 경우 해당 테이블의 데이터는 최대 40개 분산에만 할당되며 20개 분산에는 데이터가 포함되지 않으므로 처리 작업도 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="c3b2e-192">반대로, 다른 40개 배포는 데이터가 60개 넘는 배포에 균일하게 분산되는 경우보다 수행할 작업이 더 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="c3b2e-193">이 시나리오가 데이터 오차를 보여 주는 예라 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="c3b2e-194">MPP 시스템에서 각 쿼리 단계는 모든 분산이 각기 할당된 작업을 완료할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="c3b2e-195">특정 분산이 다른 분산보다 더 많은 작업을 수행하는 경우 다른 분산은 작업량이 더 많은 분산의 작업이 완료될 때까지 기다려야 하므로 해당 리소스가 낭비됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="c3b2e-196">모든 분산으로 작업이 균일하게 분산되지 않은 상태를 **처리 오차**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="c3b2e-197">처리 오차가 발생하면 워크로드를 모든 분산에 균일하게 분산할 수 있는 경우보다 쿼리가 더 느리게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="c3b2e-198">데이터 오차가 있으면 처리 오차가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="c3b2e-199">null 값은 모두 같은 분산에 할당되므로 null이 많은 열에는 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="c3b2e-200">날짜 열에 데이터를 분산해도 처리 오차가 발생할 수 있습니다. 지정된 날짜의 모든 데이터는 같은 분산에 할당되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="c3b2e-201">여러 사용자가 모두 같은 날짜를 기준으로 필터링하는 쿼리를 실행하는 경우, 지정된 날짜가 분산 하나에만 포함되어 있으므로 60개 분산 중 하나만 모든 작업을 수행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="c3b2e-202">따라서 이 시나리오에서는 데이터를 모든 분산에 균일하게 분산한 경우에 비해 쿼리 실행 속도가 60배 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="c3b2e-203">좋은 후보 열이 없으면 배포 방법으로 라운드 로빈을 사용하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="c3b2e-204">데이터 이동을 최소화하는 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="c3b2e-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="c3b2e-205">올바른 배포 열을 선택하여 데이터 이동을 최소화하는 일은 SQL 데이터 웨어하우스의 성능을 최적화하기 위한 가장 중요한 전략 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="c3b2e-206">데이터 이동은 테이블이 조인되거나 집계가 수행될 때 흔히 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="c3b2e-207">`JOIN`, `GROUP BY`, `DISTINCT`, `OVER` 및 `HAVING` 절에 사용한 열이 모두 해시 분산 후보로 **적합**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="c3b2e-208">반면 `WHERE` 절의 열은 쿼리에 참여하는 배포를 제한하여 처리 오차를 발생시키므로 해시 열 후보로 적합하지 **않습니다** .</span><span class="sxs-lookup"><span data-stu-id="c3b2e-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="c3b2e-209">데이터를 분산시키기에 적합해 보이지만 이와 같은 처리 오차를 발생시키기가 많은 열의 대표적인 예로 날짜 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="c3b2e-210">일반적으로 두 개의 대형 팩트 테이블이 조인에 자주 포함될 경우 조인 열 중 하나에 두 테이블을 모두 배포함으로써 최적의 성능을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="c3b2e-211">다른 대형 팩트 테이블에 조인되지 않는 테이블이 있는 경우 `GROUP BY` 절에서 자주 나오는 열을 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="c3b2e-212">조인하는 동안 데이터 이동을 피하기 위해서는 몇 가지 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="c3b2e-213">조인에 관련된 테이블은 조인에 포함되는 열 중 **하나** 에서 해시 분산해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="c3b2e-214">조인 열의 데이터 형식은 두 테이블 간에 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="c3b2e-215">같음 연산자로 열을 조인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="c3b2e-216">조인 형식은 `CROSS JOIN`이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="c3b2e-217">데이터 오차 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c3b2e-217">Troubleshooting data skew</span></span>
<span data-ttu-id="c3b2e-218">해시 분산 방법을 사용하여 테이블 데이터를 분산하는 경우 일부 분산에 불균형하게 다른 분산보다 데이터가 더 많은 오차가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="c3b2e-219">분산 쿼리의 최종 결과는 가장 오래 실행되는 분산이 완료될 때까지 대기해야 하므로 과도한 데이터 오차는 쿼리 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="c3b2e-220">데이터 오차 정도에 따라 이 문제를 해결해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="c3b2e-221">오차 식별</span><span class="sxs-lookup"><span data-stu-id="c3b2e-221">Identifying skew</span></span>
<span data-ttu-id="c3b2e-222">테이블을 오차 상태로 식별하는 간단한 방법은 `DBCC PDW_SHOWSPACEUSED`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="c3b2e-223">각각의 60개 데이터베이스 배포에 저장된 테이블 행 수를 매우 빠르고 간편하게 보는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="c3b2e-224">가장 균형 있는 성능을 얻으려면 분산 테이블의 행을 모든 배포에 균등하게 나누어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="c3b2e-225">그러나 SQL 데이터 웨어하우스 DMV(동적 관리 뷰)를 쿼리하는 경우 보다 자세한 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="c3b2e-226">분석을 시작하려면 [테이블 개요][Overview] 문서의 SQL을 사용하여 [dbo.vTableSizes][dbo.vTableSizes] 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="c3b2e-227">뷰가 생성되면 이 쿼리를 실행하여 데이터 오차가 10%보다 큰 테이블을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="c3b2e-228">데이터 오차 해결</span><span class="sxs-lookup"><span data-stu-id="c3b2e-228">Resolving data skew</span></span>
<span data-ttu-id="c3b2e-229">모든 오차가 해결을 보장할 만큼 충분한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="c3b2e-230">경우에 따라 일부 쿼리에서는 테이블 성능이 매우 중요해서 데이터 오차가 발생할 위험도 용인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="c3b2e-231">테이블의 데이터 오차를 해결해야 하는지 결정하려면 워크로드의 데이터 볼륨 및 쿼리를 최대한 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="c3b2e-232">오차의 영향을 확인하는 한 가지 방법은 [쿼리 모니터링][Query Monitoring] 문서의 단계를 사용하여 쿼리 성능에 오차가 미치는 영향, 특히 개별 분산에서 쿼리가 완료되는 데 소요되는 시간에 대한 영향을 모니터링하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="c3b2e-233">데이터 분산은 데이터 오차 최소화와 데이터 이동 최소화 간의 적절한 균형을 찾는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="c3b2e-234">이는 반대되는 목표일 수 있으며, 경우에 따라 데이터 이동을 줄이기 위해 데이터 오차를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="c3b2e-235">예를 들어 분산 열이 종종 조인 및 집계에서 공유 열인 경우 데이터 이동을 최소화하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="c3b2e-236">데이터 이동을 최소화할 경우의 이점은 데이터 오차의 영향을 능가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="c3b2e-237">데이터 오차를 해결하는 일반적인 방법은 다른 분산 열이 있는 테이블을 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="c3b2e-238">기존 테이블에서 배포 열을 변경할 방법이 없으므로 테이블의 배포를 변경하는 방법은 [CTAS][]를 사용하여 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="c3b2e-239">데이터 오차를 해결하는 방법의 두 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="c3b2e-240">예제 1: 새 배포 열로 테이블 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="c3b2e-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="c3b2e-241">이 예제에서는 [CTAS][]를 사용하여 다른 해시 분산 열로 테이블을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="c3b2e-242">예제 2: 라운드 로빈 배포를 사용하여 테이블 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="c3b2e-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="c3b2e-243">이 예제에서는 [CTAS][]를 사용하여 해시 분산 대신, 라운드 로빈으로 테이블을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="c3b2e-244">이렇게 변경하면 데이터 이동이 증가하지만 데이터가 균일하게 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="c3b2e-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3b2e-245">Next steps</span></span>
<span data-ttu-id="c3b2e-246">테이블 디자인에 대한 자세한 내용은 [분산][Distribute], [인덱스][Index], [파티션][Partition], [데이터 형식][Data Types], [통계][Statistics] 및 [임시 테이블][Temporary] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="c3b2e-247">모범 사례의 개요는 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3b2e-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
