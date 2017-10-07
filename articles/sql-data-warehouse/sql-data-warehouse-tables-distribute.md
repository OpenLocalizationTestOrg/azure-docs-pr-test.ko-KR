---
title: "SQL 데이터 웨어하우스에 aaaDistributing 테이블 | Microsoft Docs"
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="aedbd-103">SQL 데이터 웨어하우스의 테이블 배포</span><span class="sxs-lookup"><span data-stu-id="aedbd-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="aedbd-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="aedbd-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="aedbd-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="aedbd-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="aedbd-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="aedbd-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="aedbd-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="aedbd-107">[Index][Index]</span></span>
> * <span data-ttu-id="aedbd-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="aedbd-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="aedbd-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="aedbd-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="aedbd-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="aedbd-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="aedbd-111">SQL 데이터 웨어하우스는 방대한 병렬 처리(MPP) 분산 데이터베이스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="aedbd-112">여러 노드에 걸쳐 데이터와 처리 용량을 구분하여 SQL 데이터 웨어하우스는 모든 단일 시스템을 넘어서는 매우 큰 확장성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="aedbd-113">어떻게 toodistribute SQL 데이터 웨어하우스 내에서 데이터를 결정 tooachieving 최적의 성능을 요소 가장 중요 한 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="aedbd-114">hello 키 toooptimal 성능 데이터 이동은 최소화 하 고 hello 키 toominimizing 데이터 이동 hello 오른쪽 배포 전략을 선택 하 차례로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="aedbd-115">데이터 이동 이해</span><span class="sxs-lookup"><span data-stu-id="aedbd-115">Understanding data movement</span></span>
<span data-ttu-id="aedbd-116">MPP 시스템에서 각 테이블에서 hello 데이터가 여러 개의 기본 데이터베이스에 걸쳐 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="aedbd-117">MPP 시스템에서 가장 액세스에 최적화 된 hello 쿼리 수 전달 tooexecute hello에 상호 작용 없이 개별 분산된 데이터베이스 간에 다른 데이터베이스를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="aedbd-118">예를 들어 영업과 고객이란 두 테이블을 포함하는 판매 데이터를 가진 데이타베이스가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="aedbd-119">각 판매 및 고객을 가입 된 모든 쿼리를 해결할 수 toojoin 판매 테이블 tooyour 고객 테이블을 해야 하는 쿼리 있고 판매 및 고객 테이블을 둘 다로 나누면 고객 번호, 별도 데이터베이스에 각 고객을 넣는 경우 지식이 없는 사용 하 여 데이터베이스에는 다른 데이터베이스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="aedbd-120">반면, 주문 번호, 고객 번호에서 고객 데이터 판매 데이터를 분할 한 다음 지정된 된 데이터베이스는 포함 하지 않습니다 hello 해당 데이터 각 고객에 대 한 이므로 toojoin 판매 데이터 tooyour 고객 데이터를 려는 경우에 필요 tooget hello 데이터 hello에서 각 고객에 대 한 다른 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="aedbd-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="aedbd-121">이 두 번째 예제에서 데이터 이동을 hello 두 테이블을 조인할 수 있도록 toooccur toomove hello 고객 데이터 toohello 판매 데이터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="aedbd-122">데이터 이동이 항상 않습니다 나쁜 것, 경우에 따라 필요한 toosolve 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="aedbd-123">그러나 이 추가 단계를 피할 수 있다면, 자연스럽게 쿼리는 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="aedbd-124">데이터 이동은 테이블이 조인되거나 집계가 수행될 때 흔히 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="aedbd-125">종종 하고자 하는 동안 toooptimize 있습니다 여전히 조인 같은 한 가지 시나리오 데이터 이동을 toohelp에 대 한 해결을 위해 hello 집계와 같은 다른 시나리오에서는 하므로 toodo 두 위치에서 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="aedbd-126">hello 트릭은 변수인 보다 간단 하 게 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="aedbd-127">대부분의 경우에서 일반적으로 조인된 된 열에서 큰 팩트 테이블이 배포는 hello hello를 줄이는 가장 효과적인 방법 대부분 데이터 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="aedbd-128">집계에 관련 된 열에 데이터를 배포 하는 보다 훨씬 더 일반적 메서드 tooreduce 데이터 이동은 조인 열에 데이터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="aedbd-129">배포 방법 선택</span><span class="sxs-lookup"><span data-stu-id="aedbd-129">Select distribution method</span></span>
<span data-ttu-id="aedbd-130">Hello 백그라운드 SQL 데이터 웨어하우스 데이터베이스 60으로 데이터를 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="aedbd-131">각 개별 데이터베이스가 참조 tooas는 **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="aedbd-132">SQL 데이터 웨어하우스에 tooknow를 어떻게는 각 테이블에 데이터를 로드 하는 경우 toodivide 60 배포 간에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="aedbd-133">hello 테이블 수준에서 정의 된 hello 배포 방법 및 현재 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="aedbd-134">**라운드 로빈** : 데이터를 임의로 균일하게 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="aedbd-135">**해시 분산** : 단일 열의 해싱 값에 따라 데이터를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="aedbd-136">기본적으로 데이터 배포 방법을 정의 하지 않으면 테이블에 배포 됩니다 hello를 사용 하 여 **라운드 로빈** 배포 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="aedbd-137">그러나 보다 복잡 한 구현에서 있을 때 됩니다 tooconsider 사용 하 여 원하는 **distributed 해시** 테이블 toominimize 데이터 이동을 다시 쿼리 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="aedbd-138">라운드 로빈 테이블</span><span class="sxs-lookup"><span data-stu-id="aedbd-138">Round Robin Tables</span></span>
<span data-ttu-id="aedbd-139">데이터를 배포 하는 라운드 로빈 방법은 hello를 사용 하 여 거의 방법을 제공 하므로입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="aedbd-140">데이터를 로드할 때 각 행 toohello 다음 배포를 전송 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="aedbd-141">이러한 방식의 hello 데이터 배포는 항상 임의로 균등 hello 데이터 매우 hello 분포의 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="aedbd-142">즉,은 정렬 없음 완료 hello 라운드 로빈 프로세스 데이터를 배치 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="aedbd-143">이러한 이유로 라운드 로빈 배포를 임의 해시라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="aedbd-144">라운드 로빈 분산된 테이블 필요 toounderstand hello 데이터가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="aedbd-145">이러한 이유로 라운드 로빈 테이블은 종종 좋은 로드 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="aedbd-146">기본적으로 없습니다 배포 방법이 선택 될 경우 hello 라운드 로빈 배포 방법을 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="aedbd-147">그러나 데이터 hello 시스템 배포를 보장할 수 없습니다 것을 의미 하는 hello 시스템에 임의로 분산 되므로 쉽게 toouse 라운드 로빈 테이블에 있는 동안에 각 행은 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="aedbd-148">Hello 시스템 경우에 따라 결과 데이터 이동 작업 toobetter tooinvoke 요구에 따라 쿼리를 해결 하기 전에 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="aedbd-149">이 추가 단계로 인해 쿼리 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="aedbd-150">Hello 다음 시나리오에서에서 테이블에 대 한 라운드 로빈 배포를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="aedbd-151">간단한 시작점으로 시작하는 경우</span><span class="sxs-lookup"><span data-stu-id="aedbd-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="aedbd-152">명백한 조인 키가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="aedbd-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="aedbd-153">Hello 테이블을 배포 하는 해시에 대 한 적절 한 후 열 없는 경우</span><span class="sxs-lookup"><span data-stu-id="aedbd-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="aedbd-154">테이블이 다른 테이블을 일반적인 조인 키 공유 하지 않는 경우 hello</span><span class="sxs-lookup"><span data-stu-id="aedbd-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="aedbd-155">Hello 조인 hello 쿼리에서 다른 조인 보다 덜 중요 한 경우</span><span class="sxs-lookup"><span data-stu-id="aedbd-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="aedbd-156">때 hello 테이블은 임시 준비 테이블</span><span class="sxs-lookup"><span data-stu-id="aedbd-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="aedbd-157">다음 두 예제에서는 라운드 로빈 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="aedbd-158">라운드 로빈은 hello 기본 테이블 형식 DDL에 명시적 테이블 레이아웃의 hello 의도 지우기 tooothers 되도록 가장 좋은 방법은 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="aedbd-159">해시 분산 테이블</span><span class="sxs-lookup"><span data-stu-id="aedbd-159">Hash Distributed Tables</span></span>
<span data-ttu-id="aedbd-160">사용 하는 **distributed 해시** 알고리즘 toodistribute 테이블 쿼리 단계에서 데이터 이동을 줄이면 대부분의 시나리오에 대 한 성능 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="aedbd-161">분산된 테이블 hello 분산 되어 있는 테이블은 해시에 해싱 알고리즘을 사용 하 여 단일 열에는 선택한 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="aedbd-162">hello 배포 열을 프로그램 분산된 데이터베이스에 걸쳐 hello 데이터가 분할 되는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="aedbd-163">hello 해시 함수는 배포 열 tooassign 행 toodistributions hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="aedbd-164">hello 해싱 알고리즘 및 결과 분포는 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="aedbd-165">즉 hello 동일한 데이터 형식은 항상 hello로 동일한 값에 toohello 동일 하 게 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="aedbd-166">이 예제에서는 ID에 따라 분산된 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="aedbd-167">배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="aedbd-167">Select distribution column</span></span>
<span data-ttu-id="aedbd-168">선택 하면 해당 항목이 너무**해시 배포** 테이블을 단일 배포 열 tooselect 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="aedbd-169">배포 열을 선택 하면 세 가지 주요 요소 tooconsider가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="aedbd-170">다음과 같은 단일 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-170">Select a single column which will:</span></span>

1. <span data-ttu-id="aedbd-171">업데이트되지 않는 열</span><span class="sxs-lookup"><span data-stu-id="aedbd-171">Not be updated</span></span>
2. <span data-ttu-id="aedbd-172">데이터를 고르게 분산하는 열(데이터 오차 방지에 필요)</span><span class="sxs-lookup"><span data-stu-id="aedbd-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="aedbd-173">데이터 이동 최소화</span><span class="sxs-lookup"><span data-stu-id="aedbd-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="aedbd-174">업데이트되지 않을 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="aedbd-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="aedbd-175">배포 열은 업데이트할 수 없으므로 정적 값을 갖는 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="aedbd-176">열에서 toobe 업데이트 필요로 하는 경우 일반적으로 되지 적절 한 배포 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="aedbd-177">배포 열을 업데이트 해야 하는 경우 경우이 먼저 hello 행을 삭제 한 다음 새 행을 삽입 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="aedbd-178">데이터를 균일하게 분산하는 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="aedbd-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="aedbd-179">분산된 시스템만 만큼 빠르게 가장 느린 해당 배포에서 수행 이므로 중요 toodivide hello 작업 균등 하 게 분산 tooachieve 실행 순서에에서 hello 분포에서 hello 시스템 전체에서.</span><span class="sxs-lookup"><span data-stu-id="aedbd-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="aedbd-180">각 배포에 대 한 hello 데이터 거주 기반 hello 방법은 hello 작업 분산된 시스템에서 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="aedbd-181">이렇게 하면 각 분포에는 같은 작업은 take hello 동일한 시간 toocomplete hello 작업의 해당 부분 있도록 hello 데이터 배포에 대 한 매우 중요 한 tooselect hello 오른쪽 배포 열.</span><span class="sxs-lookup"><span data-stu-id="aedbd-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="aedbd-182">작업은 hello 시스템에서 잘 나뉘어 있는 경우 hello 데이터 hello 분포에서 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="aedbd-183">데이터가 균등하게 분산되지 않은 상태를 **데이터 오차**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="aedbd-184">toodivide 데이터 균등 하 게 시간차 데이터가 포함 되지 않도록 하 고, 배포 열을 선택할 때 hello 다음 사항을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="aedbd-185">많은 수의 고유 값을 포함하는 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="aedbd-186">고유 값이 많지 않은 열에는 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="aedbd-187">null 수가 많은 열에는 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="aedbd-188">날짜 열에 데이터를 분산하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="aedbd-189">각 값에 60 배포판의 해시 된 too1 이므로 tooachieve 균등 한 분포가 싶을 것 tooselect 고유 이며 60 개 이상의 고유 값을 포함 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="aedbd-190">tooillustrate, 여기서 열에만 있는 고유 값을 40 경우를 가정해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="aedbd-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="aedbd-191">Hello 배포 키로이 열을 선택한 경우 해당 테이블에 대 한 hello 데이터는 배치 40 분포에서 많아야 없는 데이터와 없는 처리 toodo 20 분포를 유지.</span><span class="sxs-lookup"><span data-stu-id="aedbd-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="aedbd-192">반대로, hello 40 다른 배포는 한 더 많은 작업 toodo는 hello 데이터를 고르게 분산 된 경우 60 개 이상의 배포가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="aedbd-193">이 시나리오가 데이터 오차를 보여 주는 예라 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="aedbd-194">MPP 시스템 각 쿼리 단계 hello 작업 한 모든 배포 toocomplete 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="aedbd-195">하나의 배포 hello 다른 사용자에 게 보다 많은 작업을 수행 하는 다음 리소스의 hello hello 경우 다른 배포는 기본적으로 불필요 하 게 hello 사용 중인 배포 작업 만으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="aedbd-196">모든 분산으로 작업이 균일하게 분산되지 않은 상태를 **처리 오차**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="aedbd-197">처리 기울이기 경우 hello 작업 부하 균등 하 게 분산 hello 배포 보다 느린 쿼리 toorun을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="aedbd-198">데이터 기울이기 tooprocessing 시간차를 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="aedbd-199">Null 값 hello 모든 배치 되며 hello에 동일한 대로 항상 null 허용 열에 분산 시키고 방지 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="aedbd-200">배포 날짜 열에도 발생할 수 있습니다 시간차 처리 한 특정된 날짜에 대 한 모든 데이터를 놓을 hello에서 동일 하기 때문에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="aedbd-201">여러 사용자에 게 hello에서 모든 필터링 된 쿼리를 실행 중인 경우 동일한 날짜를 1만 hello 60 분포의 하 게 될 것 hello 작업을 모두 지정된 된 날짜에 하나의 배포만 있으므로 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="aedbd-202">이 시나리오에서는 hello 쿼리는 hello 데이터 hello 분포의 모든 조치 동일 하 게 분포 된 경우 보다 느린 60 번 실행 될 가능성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="aedbd-203">좋은 후보 열이 없는 경우는 것이 좋습니다 hello 배포 방법으로 라운드 로빈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="aedbd-204">데이터 이동을 최소화하는 배포 열 선택</span><span class="sxs-lookup"><span data-stu-id="aedbd-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="aedbd-205">Hello 오른쪽 배포 열을 선택 하 여 데이터 이동을 최소화 hello SQL 데이터 웨어하우스의 성능을 최적화 하기 위한 가장 중요 한 전략 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="aedbd-206">데이터 이동은 테이블이 조인되거나 집계가 수행될 때 흔히 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="aedbd-207">`JOIN`, `GROUP BY`, `DISTINCT`, `OVER` 및 `HAVING` 절에 사용한 열이 모두 해시 분산 후보로 **적합**합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="aedbd-208">반면, hello의 열에 hello `WHERE` 절 do **하지** 시간차 분포를 따릅니다 hello 쿼리를 일으키는 처리에 참여를 제한 하기 때문에 좋은 해시 열 후보에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="aedbd-209">열을 유도할 toodistribute 않을 수 있지만 종종 시간차이 처리 될 수 있습니다는 좋은 예에는 날짜 열입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="aedbd-210">일반적으로 두 개의 큰 팩트 테이블에 자주 사용 되는 조인에 있으면 하면 얻게 됩니다 hello 대부분의 성능 두 테이블 모두 hello 조인 열 중 하나에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="aedbd-211">조인 된 tooanother 큰 팩트 테이블은 테이블의 경우 다음 toocolumns 자주 hello에 있는 확인 `GROUP BY` 절.</span><span class="sxs-lookup"><span data-stu-id="aedbd-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="aedbd-212">조인 하는 동안 met tooavoid 데이터 이동 해야 하는 몇 가지 키 기준 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="aedbd-213">hello hello 조인에 포함 된 테이블 이어야 합니다로 배포 하는 해시 **하나의** hello 조인에 참여 하는 hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="aedbd-214">hello hello 조인 열의 데이터 형식은 두 테이블 간에 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="aedbd-215">equals 연산자와 함께 hello 열 조인 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="aedbd-216">hello 조인 유형이 되지 않을 수 있습니다는 `CROSS JOIN`합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="aedbd-217">데이터 오차 문제 해결</span><span class="sxs-lookup"><span data-stu-id="aedbd-217">Troubleshooting data skew</span></span>
<span data-ttu-id="aedbd-218">테이블 데이터는 hello 해시를 배포 하는 메서드를 사용 하 여 배포 된 경우 일부 배포판 될 가능성이 일치 하지 않아 toohave 다른 항목 보다 크게 더 많은 데이터.</span><span class="sxs-lookup"><span data-stu-id="aedbd-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="aedbd-219">시간차 과도 한 데이터 분산 쿼리의 최종 결과 hello hello 가장 긴 실행 중인 배포 toofinish 기다려야 하므로 쿼리 성능이 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="aedbd-220">에 따라 hello 수준의 hello 데이터 tooaddress 해야 시간차 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="aedbd-221">오차 식별</span><span class="sxs-lookup"><span data-stu-id="aedbd-221">Identifying skew</span></span>
<span data-ttu-id="aedbd-222">간단한 방법을 tooidentify 일치 하지 않아 테이블은 toouse `DBCC PDW_SHOWSPACEUSED`합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="aedbd-223">이 매우 빠르고 간편한 방식으로 toosee hello 각 데이터베이스의 60 hello 배포판에 저장 된 테이블 행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="aedbd-224">분산 된 가장 hello 성능에 대 한 분산된 테이블의 행 hello 나뉘어집니다 균등 하 게 모든 hello 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="aedbd-225">그러나 hello Azure SQL 데이터 웨어하우스 동적 관리 뷰 (DMV)를 쿼리 하는 경우 보다 자세한 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="aedbd-226">toostart, hello 보기를 만들 [dbo.vTableSizes] [ dbo.vTableSizes] 사용 하 여 볼에서 sql 문을 hello [테이블 개요] [ Overview] 문서.</span><span class="sxs-lookup"><span data-stu-id="aedbd-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="aedbd-227">Hello 보기를 만든 후 테이블 개가 넘는 데이터 10% 오차가이 쿼리 tooidentify를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="aedbd-228">데이터 오차 해결</span><span class="sxs-lookup"><span data-stu-id="aedbd-228">Resolving data skew</span></span>
<span data-ttu-id="aedbd-229">모든 시간차 하지 충분 한 toowarrant 수정입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="aedbd-230">경우에 따라 일부 쿼리에서 테이블의 hello 성능 시간차 데이터의 hello 위험 보다 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="aedbd-231">데이터를 해결 해야 하는 경우 toodecide 테이블을 왜곡 작업에서 hello 데이터 볼륨 및 쿼리에 대 한 가능한 만큼 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="aedbd-232">오차의 hello 영향에는 한 가지 방법은 toolook hello의 toouse hello 단계는 [쿼리 모니터링] [ Query Monitoring] 영향 toohow 긴 쿼리를 구체적으로 hello 및 쿼리 성능 시간차의 toomonitor hello 영향 문서 hello 개별 분포에서 toocomplete를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="aedbd-233">데이터 배포는 찾기 hello 적절 한 균형점 데이터 오차를 최소화 하 고 데이터 이동을 최소화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="aedbd-234">이러한 목표를 반대 될 수 있습니다 및 할 경우도 있습니다 tookeep 데이터 순서 tooreduce 데이터 이동에 기울기입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="aedbd-235">예를 들어 hello 배포 열이 자주 hello 공유 열 조인 및 집계 일 때 데이터 이동을 최소화 하 될 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="aedbd-236">hello hello 최소한의 데이터 이동 있으면 얻는 hello 영향을 왜곡 시킬 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="aedbd-237">hello 일반적인 방법은 tooresolve 데이터 오차는 toore-다른 배포 열이 있는 hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="aedbd-238">방법이 있으면 기존 toochange hello 배포 열 테이블을 테이블의 hello 방식으로 toochange hello 분포 그 이후 toorecreate [CTAS] 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="aedbd-239">데이터 오차를 해결하는 방법의 두 가지 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="aedbd-240">예제 1: 새 배포 열이 있는 hello 테이블을 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="aedbd-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="aedbd-241">이 예에서는 [CTAS] toore-다른 해시 배포 열이 있는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="aedbd-242">예제 2: 라운드 로빈 배포를 사용 하 여 hello 테이블을 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="aedbd-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="aedbd-243">이 예에서는 [CTAS] toore-해시 분포로 대신 라운드 로빈 가진 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="aedbd-244">이 변경은 hello 비용 증가 데이터 이동에 데이터 분포를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="aedbd-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aedbd-245">Next steps</span></span>
<span data-ttu-id="aedbd-246">테이블 디자인에 대해 자세히 toolearn 참조 hello [Distribute][Distribute], [인덱스][Index], [파티션] [ Partition], [데이터 형식][Data Types], [통계] [ Statistics] 및 [임시 테이블] [ Temporary] 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="aedbd-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="aedbd-247">모범 사례의 개요는 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aedbd-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
