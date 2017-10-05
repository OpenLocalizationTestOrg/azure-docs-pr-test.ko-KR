---
title: "SQL Data Warehouse에 대해 트랜잭션 최적화 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 효율적인 트랜잭션 업데이트를 작성하는 모범 사례 가이드"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="deb90-103">SQL 데이터 웨어하우스에 대해 트랜잭션 최적화</span><span class="sxs-lookup"><span data-stu-id="deb90-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="deb90-104">이 문서에서는 긴 롤백에 대한 위험을 최소화하면서 트랜잭션 코드의 성능을 최적화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="deb90-105">트랜잭션 및 로깅</span><span class="sxs-lookup"><span data-stu-id="deb90-105">Transactions and logging</span></span>
<span data-ttu-id="deb90-106">트랜잭션은 관계형 데이터베이스 엔진의 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="deb90-107">SQL 데이터 웨어하우스는 데이터를 수정하는 동안 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="deb90-108">이러한 트랜잭션은 명시적일 수도 있고 암시적일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="deb90-109">단일 `INSERT`, `UPDATE` 및 `DELETE` 문은 모두 암시적 트랜잭션의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="deb90-110">명시적 트랜잭션은 개발자가 `BEGIN TRAN`, `COMMIT TRAN` 또는 `ROLLBACK TRAN`을 사용하여 명시적으로 작성하며, 일반적으로 단일 원자 단위에 여러 수정 문을 연결해야 하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="deb90-111">Azure SQL 데이터 웨어하우스는 트랜잭션 로그를 사용하여 데이터베이스에 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="deb90-112">각 분산에는 고유한 트랜잭션 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="deb90-113">트랜잭션 로그 쓰기는 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="deb90-114">구성이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-114">There is no configuration required.</span></span> <span data-ttu-id="deb90-115">그러나 이 프로세스는 쓰기를 보장하지만 시스템에 오버헤드가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="deb90-116">트랜잭션 측면에서 효율적인 코드를 작성하면 이 영향을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="deb90-117">트랜잭션 측면에서 효율적인 코드는 크게 두 범주로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="deb90-118">가능한 최소한의 로깅 구문 활용</span><span class="sxs-lookup"><span data-stu-id="deb90-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="deb90-119">한 트랜잭션이 오래 실행되지 않도록 범위가 지정된 배치 사용</span><span class="sxs-lookup"><span data-stu-id="deb90-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="deb90-120">지정된 파티션에 대규모 수정을 위한 파티션 전환 패턴 사용</span><span class="sxs-lookup"><span data-stu-id="deb90-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="deb90-121">최소 로깅 및 전체 로깅 비교</span><span class="sxs-lookup"><span data-stu-id="deb90-121">Minimal vs. full logging</span></span>
<span data-ttu-id="deb90-122">트랜잭션 로그를 사용하여 모든 행 변경을 추적하는 전체 로깅 작업과는 달리, 최소 로깅 작업은 규모 할당 및 메타 데이터 변경 내용만 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="deb90-123">따라서 최소 로깅은 장애 발생 시 또는 명시적 요청이 있을 시 트랜잭션을 롤백(`ROLLBACK TRAN`)하는 데 필요한 정보만 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="deb90-124">최소 로깅 작업은 트랜잭션 로그에서 추적하는 정보의 양이 훨씬 적기 때문에 비슷한 크기의 전체 로깅 작업보다 성능이 우수합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="deb90-125">뿐만 아니라 트랜잭션 로그에 전달되는 쓰기 작업이 적기 때문에 훨씬 적은 양의 로그 데이터가 생성되고 따라서 I/O가 훨씬 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="deb90-126">트랜잭션 안전성 제한은 전체 로깅 작업에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="deb90-127">최소 로깅 작업은 명시적 트랜잭션에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="deb90-128">할당 구조의 모든 변경 내용이 추적되므로 최소 로깅 작업을 롤백할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="deb90-129">변경 내용이 전혀 로깅되지 않는 것이 아니라 "최소로" 로깅된다는 점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="deb90-130">최소 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="deb90-130">Minimally logged operations</span></span>
<span data-ttu-id="deb90-131">다음은 최소한으로 로깅 가능한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="deb90-132">[CTAS][CTAS](CREATE TABLE AS SELECT)</span><span class="sxs-lookup"><span data-stu-id="deb90-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="deb90-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="deb90-133">INSERT..SELECT</span></span>
* <span data-ttu-id="deb90-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="deb90-134">CREATE INDEX</span></span>
* <span data-ttu-id="deb90-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="deb90-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="deb90-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="deb90-136">DROP INDEX</span></span>
* <span data-ttu-id="deb90-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="deb90-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="deb90-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="deb90-138">DROP TABLE</span></span>
* <span data-ttu-id="deb90-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="deb90-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="deb90-140">내부 데이터 이동 작업(예: `BROADCAST` 및 `SHUFFLE`)은 트랜잭션 안전성 제한의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="deb90-141">대량 로드를 사용하여 최소 로깅</span><span class="sxs-lookup"><span data-stu-id="deb90-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="deb90-142">`CTAS` 및 `INSERT...SELECT`는 대량 로드 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="deb90-143">그러나 둘 다 대상 테이블 정의의 영향을 받으며 부하 시나리오에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="deb90-144">아래는 대량 작업이 전부 로깅되는지 아니면 최소한으로 로깅되는지를 설명하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="deb90-145">기본 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-145">Primary Index</span></span> | <span data-ttu-id="deb90-146">부하 시나리오</span><span class="sxs-lookup"><span data-stu-id="deb90-146">Load Scenario</span></span> | <span data-ttu-id="deb90-147">로깅 모드</span><span class="sxs-lookup"><span data-stu-id="deb90-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="deb90-148">힙</span><span class="sxs-lookup"><span data-stu-id="deb90-148">Heap</span></span> |<span data-ttu-id="deb90-149">모두</span><span class="sxs-lookup"><span data-stu-id="deb90-149">Any</span></span> |<span data-ttu-id="deb90-150">**최소**</span><span class="sxs-lookup"><span data-stu-id="deb90-150">**Minimal**</span></span> |
| <span data-ttu-id="deb90-151">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-151">Clustered Index</span></span> |<span data-ttu-id="deb90-152">빈 대상 테이블</span><span class="sxs-lookup"><span data-stu-id="deb90-152">Empty target table</span></span> |<span data-ttu-id="deb90-153">**최소**</span><span class="sxs-lookup"><span data-stu-id="deb90-153">**Minimal**</span></span> |
| <span data-ttu-id="deb90-154">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-154">Clustered Index</span></span> |<span data-ttu-id="deb90-155">로드된 행이 대상의 기존 페이지와 겹치지 않음</span><span class="sxs-lookup"><span data-stu-id="deb90-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="deb90-156">**최소**</span><span class="sxs-lookup"><span data-stu-id="deb90-156">**Minimal**</span></span> |
| <span data-ttu-id="deb90-157">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-157">Clustered Index</span></span> |<span data-ttu-id="deb90-158">로드된 행이 대상의 기존 페이지와 겹침</span><span class="sxs-lookup"><span data-stu-id="deb90-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="deb90-159">전체</span><span class="sxs-lookup"><span data-stu-id="deb90-159">Full</span></span> |
| <span data-ttu-id="deb90-160">클러스터형 Clustered 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="deb90-161">배치 크기는 파티션 정렬 분산당 102,400 이상</span><span class="sxs-lookup"><span data-stu-id="deb90-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="deb90-162">**최소**</span><span class="sxs-lookup"><span data-stu-id="deb90-162">**Minimal**</span></span> |
| <span data-ttu-id="deb90-163">클러스터형 Clustered 인덱스</span><span class="sxs-lookup"><span data-stu-id="deb90-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="deb90-164">배치 크기는 파티션 정렬 분산당 102,400 미만</span><span class="sxs-lookup"><span data-stu-id="deb90-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="deb90-165">전체</span><span class="sxs-lookup"><span data-stu-id="deb90-165">Full</span></span> |

<span data-ttu-id="deb90-166">보조 또는 비클러스터형 인덱스를 업데이트하는 모든 쓰기 작업은 항상 전체 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="deb90-167">SQL 데이터 웨어하우스에는 60개의 분산이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="deb90-168">따라서 모든 행이 균등하게 분산되고 단일 파티션에 도착한다고 가정하면, 클러스터형 Columnstore 인덱스에 쓸 때 최소한으로 로깅하려면 배치에 6,144,000개 이상의 행이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="deb90-169">테이블이 분할되어 있고, 삽입되는 행이 파티션 경계에 걸쳐 있는 경우에는 데이터가 균등하게 분산된다는 가정하에 파티션 경계당 6,144,000개의 행이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="deb90-170">삽입 작업을 분산에 최소한으로 로깅하려면 각 분산의 각 파티션이 행 임계값 102,400을 독립적으로 초과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="deb90-171">클러스터형 인덱스가 포함된 비어 있지 않은 테이블로 데이터를 로드하면 전체 로깅 행과 최소 로깅 행이 모두 포함되는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="deb90-172">클러스터형 인덱스는 균형 잡힌 페이지 트리(b-트리)입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="deb90-173">쓰여지고 있는 페이지가 이미 다른 트랜잭션의 행을 포함하고 있으면 쓰기 작업이 전체 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="deb90-174">그러나 페이지가 비어 있으면 해당 페이지에 대한 쓰기 작업이 최소한으로 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="deb90-175">삭제 최적화</span><span class="sxs-lookup"><span data-stu-id="deb90-175">Optimizing deletes</span></span>
<span data-ttu-id="deb90-176">`DELETE` 는 전체 로깅 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="deb90-177">테이블 또는 파티션에서 대량의 데이터를 삭제해야 하는 경우 보관하려는 데이터에 대해 최소 로깅 작업으로 실행할 수 있는 `SELECT` 를 사용하는 것이 적절한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="deb90-178">이를 위해서는 [CTAS][CTAS]를 사용하여 새 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="deb90-179">새 테이블을 만든 후에는 [RENAME][RENAME]을 사용하여 이전 테이블을 새로 만든 테이블로 교체합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="deb90-180">업데이트 최적화</span><span class="sxs-lookup"><span data-stu-id="deb90-180">Optimizing updates</span></span>
<span data-ttu-id="deb90-181">`UPDATE` 는 전체 로깅 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="deb90-182">테이블 또는 파티션에서 행을 대량으로 업데이트해야 하는 경우 [CTAS][CTAS] 처럼 최소 로깅 작업을 사용하는 것이 훨씬 효율적일 때가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="deb90-183">아래 예에서는 최소 로깅이 가능하도록 전체 테이블 업데이트가 `CTAS` 로 변환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="deb90-184">이 예에서는 테이블의 판매 금액에 할인 금액을 소급하여 추가하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="deb90-185">대규모 테이블을 다시 만들면 SQL 데이터 웨어하우스 워크로드 관리 기능의 이점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="deb90-186">자세한 내용은 [동시성][concurrency] 문서의 워크로드 관리 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="deb90-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="deb90-187">파티션 전환을 사용하여 최적화</span><span class="sxs-lookup"><span data-stu-id="deb90-187">Optimizing with partition switching</span></span>
<span data-ttu-id="deb90-188">[테이블 파티션][table partition] 내부에서 대규모 수정 작업에 직면하는 경우 파티션 전환 패턴을 사용하는 것이 훨씬 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="deb90-189">데이터 수정 작업이 대규모이고 여러 파티션에 걸쳐 있는 경우 파티션을 반복해도 동일한 결과를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="deb90-190">파티션 전환을 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="deb90-191">빈 외부 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="deb90-191">Create an empty out partition</span></span>
2. <span data-ttu-id="deb90-192">CTAS로 '업데이트' 수행</span><span class="sxs-lookup"><span data-stu-id="deb90-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="deb90-193">기존 데이터를 외부 테이블로 전환</span><span class="sxs-lookup"><span data-stu-id="deb90-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="deb90-194">새 데이터를 내부로 전환</span><span class="sxs-lookup"><span data-stu-id="deb90-194">Switch in the new data</span></span>
5. <span data-ttu-id="deb90-195">데이터 정리</span><span class="sxs-lookup"><span data-stu-id="deb90-195">Clean up the data</span></span>

<span data-ttu-id="deb90-196">그러나 전환할 파티션을 식별하려면 먼저 아래와 같은 도우미 프로시저를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="deb90-197">이 프로시저는 코드 재사용률을 최대화하고 파티션 전환 예를 보다 작게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="deb90-198">아래 코드는 위에서 언급한 전체 파티션 전환 루틴을 달성하는 다섯 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update the data in the select portion of the CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="deb90-199">작은 배치를 사용하여 로깅 최소화</span><span class="sxs-lookup"><span data-stu-id="deb90-199">Minimize logging with small batches</span></span>
<span data-ttu-id="deb90-200">대규모 데이터 수정 작업의 경우 작업을 청크 또는 배치로 나누어서 작업 단위의 범위를 지정하는 것이 더 편할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="deb90-201">아래는 작업 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-201">A working example is provided below.</span></span> <span data-ttu-id="deb90-202">방법을 강조하기 위해 배치 크기가 간단한 숫자로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="deb90-203">현실에서는 배치 크기가 엄청나게 거대합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-203">In reality the batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="deb90-204">일시 중지 및 크기 조정 지침</span><span class="sxs-lookup"><span data-stu-id="deb90-204">Pause and scaling guidance</span></span>
<span data-ttu-id="deb90-205">Azure SQL 데이터 웨어하우스를 사용하여 필요에 따라 데이터 웨어하우스를 일시 중지하고, 다시 시작하고, 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="deb90-206">SQL 데이터 웨어하우스를 일시 중지하거나 규모를 조정하면 진행 중인 모든 트랜잭션이 즉시 종료되고 열려 있는 모든 트랜잭션이 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="deb90-207">일시 중지 또는 규모 조정 작업을 수행하기 전에 워크로드에서 실행 시간이 길고 불완전한 데이터 수정 작업을 실행하면 이 작업을 실행 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="deb90-208">이로 인해 Azure SQL 데이터 웨어하우스 데이터베이스를 일시 중지하거나 크기를 조정하는 데 걸리는 시간이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="deb90-209">`UPDATE` 및 `DELETE`는 전체 로깅 작업이므로 이러한 실행 취소/다시 실행 작업이 최소 로깅에 비해 훨씬 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="deb90-210">가장 좋은 시나리오는 진행 중인 데이터 수정 트랜잭션이 완료된 후 SQL 데이터 웨어하우스를 일시 중지하거나 규모를 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="deb90-211">그러나 이 방법이 불가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-211">However, this may not always be practical.</span></span> <span data-ttu-id="deb90-212">긴 롤백의 위험을 완화하기 위해 다음 옵션 중 하나를 고려해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="deb90-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="deb90-213">[CTAS][CTAS]를 사용하여 실행 시간이 긴 작업을 다시 작성</span><span class="sxs-lookup"><span data-stu-id="deb90-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="deb90-214">작업을 청크로 나누어서 행의 하위 집합에서 작동</span><span class="sxs-lookup"><span data-stu-id="deb90-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="deb90-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="deb90-215">Next steps</span></span>
<span data-ttu-id="deb90-216">격리 수준 및 트랜잭션 제한에 대해 자세히 알아보려면 [SQL Data Warehouse의 트랜잭션][Transactions in SQL Data Warehouse]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="deb90-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="deb90-217">기타 모범 사례의 개요에 대해서는 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="deb90-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

